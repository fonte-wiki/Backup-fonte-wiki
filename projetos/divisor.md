---
title: Divisor
description: 
published: true
date: 2025-07-18T07:11:05.456Z
tags: fonte-wiki, software, apps
editor: markdown
dateCreated: 2025-07-17T21:53:08.947Z
---

# Divisor

Divisor ("de águas") é um aplicativo em Python para automatizar a criação de sites baseados em [Jekyll](https://jekyllrb.com/) a partir de trechos selecionados da [fonte.wiki](https://fonte.wiki). Ele permite replicar partes do repositório [Backup-fonte-wiki](https://github.com/fonte-wiki/Backup-fonte-wiki) com customizações pontuais. O aplicativo permite a publicação do site resultante via GitHub pages.

## Como usar

**1. Clonar o repositório**

`git@github.com:fonte-wiki/Divisor.git`

**2. Instalar as dependências**

`pip install -r requirements.txt`

**3. Editar o arquivo config.yml**

*Informações sobre seu site*

`title: "Nome do site"`

`description: "Descrição do site"`

`theme: "Tema do Jekyll a usar" - o padrão é minima. Ainda precisamos testar a compatibilidade com outros temas.`

`github_pages_url: "URL do seu site no GitHub pages" - opcional.`

`about_page_title: "Título da página sobre o site" - o menu de navegação terá um link para esta página.`

`about_page_body: "Texto da página sobre o site".`

*Informações sobre o repositório-fonte*

`source_repository: "https://github.com/fonte-wiki/Backup-fonte-wiki" - deixe a opção padrão para usar fonte.wiki como base do conteúdo do seu site.`

*Mapeamento de conteúdo*

`home_page_source: "home.md" - caminho no repositório para a página inicial do seu site.`

`subpages_folder: "pages" - caminho no repositório para uma pasta de onde seu site buscará as subpáginas.`

`destination_folder: "site_contents" - nome da pasta onde você quer gravar a seleção de conteúdo convertido e editado.`

`media_destination_folder: "assets/media" - nome da pasta onde gravar os arquivos de mídia copiados do repositório-fonte.`

**4. Gerar o site**

`python cli.py generate`

**5. Testar o site localmente**

Navegue até o diretório onde o site foi gerado. O padrão é `site_contents`.

Instale as dependências do Jekyll:

`bundle install`

Use o servidor interno do Jekyll para testar o site em seu sistema:

`bundle exec jekyll serve`

**6. Se tudo estiver bem, publique o site**

`python cli.py deploy`

---

## TODO

Próximas etapas de desenvolvimento

- CI/CD para atualização automática do conteúdo
- Uso de outros temas do Jekyll
- Mais opções de customização

---

## Lost here?

You will find ENGLISH documentation directly on the [repository](https://github.com/fonte-wiki/divisor).

---

Divisor foi _vibe-coded_ por [Felipe](/pessoas/felipe-fonseca) e [Jules](https://jules.google.com/) a partir de Julho de 2025.
