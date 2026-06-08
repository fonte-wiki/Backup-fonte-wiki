---
title: Tropixel Social Club
description: 
published: true
date: 2026-06-08T01:14:34.492Z
tags: 
editor: markdown
dateCreated: 2026-06-07T17:24:58.671Z
---

# Tropixel Social Club

[Tropixel Social Club](https://social.tropixel.org) é um agregador de perfis de redes sociais federadas ligados a integrantes e iniciativas da rede [Tropixel](https://tropixel.org). Foi criado em junho de 2026 como experiência de curadoria manual de feeds sociais. 

## Detalhes técnicos

*(documentação criada por máquinas)*

> Criando um Agregador do Fediverso (Estilo RSS) com GoToSocial e Python

Este guia documenta o processo de criação de um hub no Fediverso. O objetivo inicial era usar um ActivityPub Relay, mas percebemos que relays funcionam como uma mangueira de incêndio (distribuindo tudo de todos). Como o objetivo era criar uma timeline curada (semelhante a um agregador RSS), a melhor abordagem foi subir uma instância leve e dedicada do GoToSocial pareada com um bot em Python.

Nesta arquitetura, a conta do GoToSocial segue os perfis selecionados, e um bot em Python lê a home timeline dessa conta e automaticamente dá "Boost" (reblog) nas postagens, criando um feed unificado e público que qualquer pessoa no Fediverso pode seguir.

## 1. Infraestrutura Base (Oracle Cloud)

Utilizamos uma instância AlwaysFree da Oracle Cloud com Ubuntu.

### 1.1. Resolvendo a falta de RAM (Swap)

A instância micro da Oracle pode travar por falta de memória (Out-Of-Memory) ao compilar ou rodar serviços novos. A primeira coisa a fazer é criar um arquivo de Swap de 2GB:

```
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

## 1.2. Nginx e Certificado SSL

Usamos o Nginx como proxy reverso para receber o tráfego da web e o Certbot para o SSL gratuito.

```
sudo apt update
sudo apt install nginx certbot python3-certbot-nginx -y
```

Crie o arquivo de configuração do Nginx (/etc/nginx/sites-available/social.seudominio.org):

```
server {
    listen 80;
    server_name social.seudominio.org;

    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```


Ative o site e gere o certificado HTTPS:

```
sudo ln -s /etc/nginx/sites-available/social.seudominio.org /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
sudo certbot --nginx -d social.seudominio.org
```

## 2. Configurando o GoToSocial

O GoToSocial (GTS) é ideal por ser um binário único, leve e que usa um banco SQLite por padrão.

### 2.1. Instalação e Configuração

Baixe o binário em uma pasta dedicada:

```
mkdir -p ~/gotosocial
cd ~/gotosocial
wget https://github.com/superseriousbusiness/gotosocial/releases/latest/download/gotosocial-linux-amd64.tar.gz
tar -xzf gotosocial-linux-amd64.tar.gz
```

Crie o arquivo config.yaml (nano config.yaml). É importante fechar registros e apontar a página inicial para a conta do agregador:

```
host: "social.seudominio.org"
bind-address: "127.0.0.1"
port: 8080
db-type: "sqlite"
db-address: "./sqlite.db"
storage-local-base-path: "./storage"
landing-page-user: "socialclub" # Substitua pelo nome do seu agregador
accounts-registration-open: false
```


### 2.2. Criando o Usuário do Agregador

Gere a conta principal pela linha de comando:

```
./gotosocial --config-path ./config.yaml admin account create --username socialclub --email admin@seudominio.org --password 'SuaSenhaSegura'
```

Nota: Caso precise resetar a senha no futuro, use o comando admin account password.

### 2.3. Configurando como Serviço (Daemon)

Para que o GTS rode no fundo e inicie com o sistema, crie um serviço systemd (sudo nano /etc/systemd/system/gotosocial.service):

```
[Unit]
Description=GoToSocial Hub
After=network.target

[Service]
Type=simple
User=ubuntu
Group=ubuntu
WorkingDirectory=/home/ubuntu/gotosocial
ExecStart=/home/ubuntu/gotosocial/gotosocial --config-path /home/ubuntu/gotosocial/config.yaml server start
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```


Inicie o serviço:

```
sudo systemctl daemon-reload
sudo systemctl enable --now gotosocial
```

### 2.4. Ajuste na Interface Web

Por padrão, o GTS esconde "Boosts" da página web pública do perfil. Para o agregador, precisamos mostrar isso:

Acesse https://social.seudominio.org/settings e faça login.

Em Visibility and Privacy, marque "Include Boosts on the Web View of Your Profile".

Salve.

## 3. O Bot de Agregação (Python)

Vamos usar a biblioteca oficial Mastodon.py (o GTS é compatível com a API do Mastodon) para ler a timeline da conta socialclub e automatizar o boost.

### 3.1. Ambiente Virtual

```
mkdir -p ~/tropixel-booster
cd ~/tropixel-booster
sudo apt install -y python3.12-venv python3-venv
python3 -m venv bot-env
source bot-env/bin/activate
pip install Mastodon.py
```


### 3.2. Autenticação (OAuth)

O GoToSocial não permite login direto por senha via API. Precisamos gerar um token. Entre no shell interativo do Python (python):

```
from mastodon import Mastodon

# 1. Registra o app no servidor

Mastodon.create_app(
    'tropixel-booster',
    api_base_url='https://social.seudominio.org',
    to_file='booster_clientcred.secret'
)

# 2. Carrega as credenciais geradas

mastodon = Mastodon(client_id='booster_clientcred.secret', api_base_url='https://social.seudominio.org')

# 3. Gera o link de autorização

print(mastodon.auth_request_url())
```

Abra o link gerado no navegador, clique em "Authorize" e copie o código. De volta ao Python:
```
# 4. Troca o código pelo token final

mastodon.log_in(code='COLE_O_CODIGO_AQUI', to_file='booster_usercred.secret')
exit()
```

### 3.3. O Script de Boost

Crie o arquivo boost_aggregator.py na pasta do bot:

```
import os
from mastodon import Mastodon

os.chdir(os.path.dirname(os.path.abspath(__file__)))

mastodon = Mastodon(
    client_id='booster_clientcred.secret',
    access_token='booster_usercred.secret',
    api_base_url='https://social.seudominio.org'
)

# Puxa os 40 posts mais recentes da home (perfis que você segue)
timeline = mastodon.timeline_home(limit=40)

for post in timeline:
    # Dá o boost se for um post original e ainda não tiver sido impulsionado
    if not post['reblogged'] and post['reblog'] is None:
        try:
            print(f"Dando boost no post de @{post['account']['acct']}")
            mastodon.status_reblog(post['id'])
        except Exception:
            pass
```

### 3.4. Automação com Cron

Para rodar a cada 10 minutos, adicione ao crontab -e:

```
*/10 * * * * /home/ubuntu/tropixel-booster/bot-env/bin/python /home/ubuntu/tropixel-booster/boost_aggregator.py > /dev/null 2>&1
```

## 4. Como Usar o Agregador

O setup técnico está pronto! Para adicionar ou remover fontes do seu agregador, você não precisa mais tocar em código. Basta acessar seu GoToSocial usando um cliente web (como o Phanpy ou Elk) e Seguir as contas que você deseja agregar. O bot fará o resto automaticamente a cada 10 minutos.