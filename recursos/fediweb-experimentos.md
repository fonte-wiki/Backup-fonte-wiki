---
title: Fediweb - experimentos
description: 
published: true
date: 2026-03-06T15:58:22.745Z
tags: 
editor: markdown
dateCreated: 2026-03-06T15:56:50.851Z
---

# Fediwed - experimentos

[Dr. F](/pessoas/felipe-fonseca) fazendo experimentos com fediweb.

## 1. GoToSocial

Instalei o [GoToSocial](https://gotosocial.org/) no meu servidor para montar um [microblog pessoal](https://pub.efeefe.me) simples que também republica os novos links que eu adiciono à [minha lista de bookmarks](htps://links.efeefe.me). Tinha olhado antes o [micro.one](https://micro.one/) mas não permite self-hosting. Documentando abaixo algumas das coisas que fiz no meu servidor para além de instalar o gotosocial, configurar o nginx e rodar o let's encrypt pra gerar os certs de https. 

P.S.: outra coisa que não está abaixo é que precisei criar um swapfile para superar os limites impostos pela pouca memória RAM que tenho nesse VPS.

### 1.1. Registrar meu VPS como instância no gotosocial

Para poder usar o feed2toot (e republicar meus links), precisei gerar um token usando o script abaixo

```
from mastodon import Mastodon
import os

instance_url = 'https://pub.efeefe.me'
target_dir = '/opt/feed2toot'
token_path = os.path.join(target_dir, 'feed2toot.token.json')

if not os.path.exists(target_dir):
    os.makedirs(target_dir)

print("--- Step 1: Registering App ---")
# This creates the client ID and Secret
client_id, client_secret = Mastodon.create_app(
    'Shaarli_Bridge',
    api_base_url=instance_url,
    redirect_uris='urn:ietf:wg:oauth:2.0:oob'
)

print("--- Step 2: Authorizing ---")
# We must pass BOTH client_id and client_secret here
mastodon = Mastodon(
    client_id=client_id, 
    client_secret=client_secret, 
    api_base_url=instance_url
)

url = mastodon.auth_request_url(redirect_uris='urn:ietf:wg:oauth:2.0:oob')

print(f"\n1. Open this URL in your browser:\n{url}")
auth_code = input("\n2. Paste the code from the browser here: ").strip()

print("\n--- Step 3: Saving Token ---")
mastodon.log_in(
    code=auth_code,
    redirect_uri='urn:ietf:wg:oauth:2.0:oob',
    to_file=token_path
)

print(f"\nSuccess! Token created at: {token_path}")
```

### 1.1.2. Feed2toot config

Instalei o feed2toot (`pip3 install feed2toot`) e criei o arquivo ~/.config/feed2toot.ini com o conteúdo abaixo:

```
[rss]
uri = https://links.efeefe.me/?do=rss
toot = Link: {title} - {link}

[cache]
cachefile = /opt/feed2toot/cache

[mastodon]
instance_url = https://pub.efeefe.me
client_credentials = /opt/feed2toot/feed2toot.client.secret
user_credentials = /opt/feed2toot/feed2toot.token.json

[lock]
lock_file = /opt/feed2toot/bridge.lock
```
## 2. Posts archive

Aproveitei para fazer um script que arquiva todos os meus posts em um repositório github. MY_ID é o token criado na administração do gotosocial.

```
#!/bin/bash

# Configuration
DB_PATH="/opt/gotosocial/sqlite.db"
GIT_DIR="/opt/gotosocial/archive"
POSTS_DIR="${GIT_DIR}/posts"
MY_ID=""

mkdir -p "$POSTS_DIR"
cd "$GIT_DIR" || exit

# 1. Export to a standard CSV file (SQLite handles the quoting of HTML content)
sqlite3 -csv "$DB_PATH" "SELECT strftime('%Y%m%d-%H%M%S', created_at), id, content FROM statuses WHERE account_id = '$MY_ID';" > /tmp/gts_export.csv

# 2. Use a specialized loop to handle the CSV
while IFS=, read -r TIMESTAMP ID CONTENT; do
    # Remove surrounding quotes that SQLite adds to CSV fields
    TIMESTAMP=$(echo "$TIMESTAMP" | sed 's/^"//;s/"$//')
    ID=$(echo "$ID" | sed 's/^"//;s/"$//')
    # Content can be long, so we handle it carefully
    
    [ -z "$ID" ] && continue

    FILE_NAME="${POSTS_DIR}/${TIMESTAMP}_${ID}.md"

    if [ ! -f "$FILE_NAME" ]; then
        echo "Archiving: ${TIMESTAMP}"
        
        # We use a temp file for the content to let Pandoc read it cleanly
        echo "$CONTENT" > /tmp/post_content.html
        CLEAN_MD=$(pandoc -f html -t markdown_strict /tmp/post_content.html)

        cat <<EOF > "$FILE_NAME"
---
id: $ID
date: $TIMESTAMP
---

$CLEAN_MD
EOF
    fi
done < /tmp/gts_export.csv

# 3. GitHub Sync
git add .
git diff --quiet && git diff --staged --quiet || (git commit -m "Archive sync: $(date +'%Y-%m-%d %H:%M')" && git push origin main)

```


## 3. Cron jobs

Por fim, acrescentei esses jobs ao meu crontab:

```
0 3 * * * /bin/bash /opt/gotosocial/archive_posts.sh >> /var/log/gts-archive.log 2>&1
30 * * * * rm -f /opt/feed2toot/bridge.lock && /usr/local/bin/feed2toot -c /root/.config/feed2toot.ini > /dev/null 2>&1
```
