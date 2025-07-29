---
title: Divisor
description: 
published: true
date: 2025-07-29T21:54:39.922Z
tags: fonte-wiki, software, apps
editor: markdown
dateCreated: 2025-07-17T21:53:08.947Z
---

# Divisor (de águas)

Divisor é uma ferramenta baseada em Python que automatiza a criação de um site com tecnologia Jekyll a partir de um repositório Git. Por padrão, usa o repositório de Backup da fonte.wiki.

A ideia central é fornecer uma maneira simples e flexível de gerar um site estático a partir de conteúdos selecionados, sem ter que configurar manualmente um ambiente Jekyll ou gerenciar o processo de conversão de conteúdo. O site resultante será implantado no GitHub Pages por padrão.

Divisor foi criado no âmbito do [Lab Mãe D'Água](https://fonte.wiki/projetos/maedagua).

## Como funciona

Divisor parte do conteúdo do repositório de origem. Em seguida, a ferramenta gera um site Jekyll com base no arquivo de configuração `config.yml`. O site gerado é salvo na `destination_folder` definida no arquivo de configuração.

O arquivo `config.yml` permite que você personalize o site gerado. Você pode definir o título, a descrição, o tema e outras opções do site. Você também pode mapear arquivos e pastas específicos do seu repositório de origem para o site gerado.

## Configuração

O principal arquivo de configuração é o `config.yml`. Aqui está um detalhamento das opções disponíveis:

```yaml
site_metadata:
  title: "Meu Site Incrível"
  description: "Site criado com fonte.wiki e Divisor"
  theme: "minima"

  github_repository_url: "https://github.com/seu-usuario-git/seu-repositorio.git" # Recomendado: use o URL HTTPS

  github_pages_url: "https://seu-usuario-git.github.io/seu-repositorio/" #edite esta linha

source_repository: "https://github.com/fonte-wiki/Backup-fonte-wiki" #deixe isto para usar o fonte.wiki como o repositório de origem

content_mapping:
  home_page_source: "home.md" #edite esta linha para escolher a página inicial do seu site
  subpages_folder: "<none>" #opcionalmente, adicione uma pasta do repositório de origem cujo conteúdo será importado como subpáginas
  destination_folder: "site_contents"
  media_destination_folder: "assets/media"
```

### `site_metadata`

*   `title`: O título do seu site.
*   `description`: Uma breve descrição do seu site.
*   `theme`: O tema Jekyll a ser usado. O padrão é "minima". Para uma lista de temas disponíveis, execute `python cli.py themes`.
*   `github_repository_url`: O endereço do seu repositório.
*   `github_pages_url`: O URL do seu site do GitHub Pages.

### `source_repository`

URL do repositório Git a ser usado como fonte para o conteúdo do seu site.

### `content_mapping`

*   `home_page_source`: O caminho para o arquivo Markdown a ser usado como página inicial.
*   `subpages_folder`: O caminho para a pasta que contém as subpáginas. Para desativar as subpáginas, defina este campo como `<none>`.
*   `destination_folder`: A pasta onde o site Jekyll gerado será criado.
*   `media_destination_folder`: A pasta para onde os arquivos de mídia serão copiados.

## Começando

Existem duas maneiras de usar o Divisor para gerar e implantar seu site:

### Opção A: Configuração Manual

Esta opção é ideal se você deseja gerar um site estático único a partir do estado atual do seu repositório de origem.

1.  **Clone o repositório:**
    ```bash
    git clone https://github.com/fonte-wiki/divisor.git
    cd divisor
    ```
2.  **Instale as dependências:**
    ```bash
    pip install -r requirements.txt
    ```
3.  **Configure o site:**
    Primeiro, renomeie `config.yml.sample` para `config.yml`. Em seguida, edite o arquivo `config.yml` para personalizar seu site.
4.  **Gere o site:**
    ```bash
    python cli.py generate
    ```
    **Nota:** Este comando sempre buscará o conteúdo mais recente do repositório de origem antes de gerar o site.
5.  **Visualize o site localmente (Requer Ruby/Jekyll):**
    Para visualizar seu site localmente, você precisará ter o Ruby e o Bundler instalados. Em seguida, `cd` no diretório do seu site gerado e execute:
    ```bash
    bundle install
    bundle exec jekyll serve
    ```
6.  **Implante o site (Apenas Manual):**
    Para implantar o site no GitHub Pages, execute:
    ```bash
    python cli.py deploy
    ```
    **Nota:** Este comando destina-se apenas a implantações manuais. Se você estiver usando a configuração automatizada do GitHub Actions, não precisará executar este comando.
    O repositório de destino é configurado no arquivo `config.yml` através do campo `github_repository_url`.
7.  **Configuração do GitHub Pages:**
    Se você implantar manualmente seus arquivos de origem Jekyll gerados em um branch gh-pages, precisará configurar o GitHub Pages:
    * **Certifique-se de que o branch `gh-pages` exista:**
    Se não existir, crie-o:
    ```bash
    git checkout --orphan gh-pages
    git rm -rf . # Remova todos os arquivos do novo branch órfão
    git commit --allow-empty -m "Commit inicial do gh-pages"
    git push origin gh-pages
    git checkout main # Volte para o seu branch principal
    ```

    * **Configure o GitHub Pages:**
    Na seção `Settings > Pages` do seu repositório do GitHub:
        * Defina "Source" como "Deploy from a branch".
        * Selecione o branch `gh-pages` e a pasta / (root).
        * Clique em "Save".

### Opção B: Configuração Automatizada com GitHub Actions

Esta opção fornece uma maneira totalmente automatizada de manter seu site sincronizado com o repositório de origem.

1.  **Faça um fork do Divisor para sua conta do GitHub:**
    Faça um fork deste repositório (`https://github.com/fonte-wiki/divisor`) para sua própria conta ou organização do GitHub.
2.  **Habilite os fluxos de trabalho em seu repositório forkado:**
    Por padrão, os fluxos de trabalho do GitHub Actions são desabilitados em repositórios forkados. Para habilitá-los, vá para a guia "Actions" em seu repositório forkado и clique no botão "I understand my workflows, go ahead and enable them".
3. **Renomeie os Arquivos de Fluxo de Trabalho:**
    Os arquivos de fluxo de trabalho são fornecidos com uma extensão .sample para evitar que sejam executados automaticamente no repositório principal do Divisor. Para implantação automatizada em seu repositório forkado, você precisa renomeá-los:
    * Renomeie `.github/workflows/generate-website.yml-sample` para `.github/workflows/generate-website.yml`
    * Renomeie `.github/workflows/deploy-website.yml-sample` para `.github/workflows/deploy-website.yml`
    Você pode fazer isso diretamente na interface da web do GitHub ou clonando o repositório, renomeando localmente e enviando as alterações.
4.  **Configure as configurações do GitHub Pages:**
    Antes de sua primeira implantação, certifique-se de que suas configurações do GitHub Pages estejam configuradas:
    * Navegue até o seu repositório forkado no GitHub.
    * Vá para `Settings > Pages`.
    * Em "Build and deployment", certifique-se de que:
        * "Source" esteja definido como "Deploy from a branch".
        * "Branch" esteja definido como `gh-pages` e `/ (root)`.
    * Clique em "Save".
    (O GitHub criará automaticamente o branch gh-pages no primeiro push bem-sucedido pela ação de implantação.)
5. **Configure os Segredos do GitHub:**
    O fluxo de trabalho automatizado usa um Token de Acesso Pessoal (PAT) para autenticar e enviar o site Jekyll gerado para o seu branch `gh-pages`. Você precisa criar este PAT e adicioná-lo como um segredo do repositório.
    * **Gere um Token de Acesso Pessoal (PAT):**
        * Vá para as configurações do seu perfil do GitHub: `Settings > Developer settings > Personal access tokens > Tokens (classic)`.
        * Clique em "Generate new token (classic)".
        * **Nota:** Dê um nome descritivo (por exemplo, `Divisor GH Pages Deploy Token`).
        * **Expiração:** Defina uma expiração apropriada (por exemplo, 90 dias, 1 ano ou "Sem expiração" para implantação contínua, embora a rotação regular seja uma boa prática).
        * **Selecione os Escopos:** Crucialmente, habilite o escopo `repo`. Isso concede ao token permissões suficientes para enviar conteúdo para o seu branch `gh-pages`.
        * Clique em "Generate token" e **copie imediatamente o valor do token**. Você não o verá novamente.
    * **Adicione o PAT como um Segredo do Repositório:**
        * Navegue até o seu repositório Divisor forkado no GitHub.
        * Vá para `Settings > Secrets and variables > Actions`.
        * Clique em "New repository secret".
        * **Nome:** Digite `GH_PAGES_TOKEN` (este nome deve corresponder exatamente ao que é usado no fluxo de trabalho `deploy-website.yml`).
        * **Valor:** Cole o PAT que você copiou na etapa anterior.
        * Clique em "Add secret".
6.  **Configure o `config.yml` do Divisor:**
    * Renomeie `config.yml.sample` para `config.yml`.
    * Edite o arquivo `config.yml` para personalizar seu site.
    * Crucialmente, certifique-se de que `site_metadata.github_pages_url` esteja definido corretamente para o URL do GitHub Pages do seu repositório forkado. Por exemplo, se o seu repositório forkado for `seu-nome-de-usuario/divisor`, github_pages_url deve ser `https://seu-nome-de-usuario.github.io/divisor/`.
    * O baseurl gerado pelo Divisor em `_config.yml` (dentro de `site_contents`) será derivado disso e deve corresponder ao caminho do seu GitHub Pages (por exemplo, `/divisor`).
7.  **Configuração dos Arquivos de Fluxo de Trabalho:**
    Os arquivos de fluxo de trabalho do GitHub Actions necessários já estão incluídos no diretório `.github/workflows/` deste repositório, mas requerem renomeação conforme descrito na etapa 3.
8.  **Commit e push:**
    Faça o commit das suas alterações no `config.yml` (e dos arquivos de fluxo de trabalho renomeados da etapa 3) para o seu repositório forkado. Um evento `push` acionará automaticamente o fluxo de trabalho `generate-website.yml`, que, após a conclusão, acionará o fluxo de trabalho `deploy-website.yml`.


## Detalhes do Fluxo de Trabalho Automatizado

Este repositório inclui dois fluxos de trabalho do GitHub Actions que automatizam o processo de geração e implantação do site:

1.  `generate-website.yml`:
    * **Gatilhos:** É executado automaticamente a cada hora (`cron: '0 * * * *'`), pode ser acionado manualmente via `workflow_dispatch` ou a cada `push` no repositório.
    * **Passos:** Faz o checkout do repositório, configura o ambiente Python, instala as dependências, executa `python cli.py generate` para buscar o conteúdo e criar os arquivos de origem do Jekyll em `site_contents`. Em seguida, ele carrega esses arquivos gerados como um artefato do GitHub Action chamado `jekyll-site-source`.
2.  `deploy-website.yml`:
    * **Gatilhos:** Ativado automaticamente (`workflow_run`) assim que o fluxo de trabalho `generate-website.yml` for concluído com sucesso.
    * **Passos:** Faz o checkout do repositório, baixa o artefato `jekyll-site-source` da execução concluída do `generate-website.yml`. Em seguida, ele usa a ação `peaceiris/actions-gh-pages` para enviar a origem do Jekyll para o seu branch `gh-pages`. Crucialmente, a opção `disable_nojekyll: true` é usada para garantir que o GitHub Pages processe seu conteúdo como um site Jekyll (em vez de servi-lo como arquivos estáticos simples).

## Escolhendo um Tema

O Divisor suporta todos os temas Jekyll que são compatíveis com o GitHub Pages. Para ver uma lista de temas disponíveis, execute o seguinte comando:

```bash
python cli.py themes
```

Isso produzirá uma lista de temas que você pode usar no seu arquivo `config.yml`.

Para alterar o tema do seu site, basta atualizar o campo `theme` no seu arquivo `config.yml` com o nome do tema desejado. Por exemplo:

```yaml
site_metadata:
  title: "Meu Site Incrível"
  description: "Site criado com fonte.wiki e Divisor"
  theme: "cayman" # Alterado de "minima"
  # ...
```

Depois de alterar o tema, faça o commit das alterações no seu arquivo `config.yml`. Se você estiver usando a configuração automatizada, o fluxo de trabalho do GitHub Actions irá regenerar e implantar automaticamente seu site com o novo tema.

## Templates e Layouts Personalizados

Você pode personalizar a aparência do seu site fornecendo seus próprios templates e layouts. Para fazer isso, crie os diretórios `_layouts` e `_includes` dentro do diretório `divisor`.

*   `divisor/_layouts`: Coloque seus layouts personalizados neste diretório.
*   `divisor/_includes`: Coloque seus includes personalizados neste diretório.

Quando você executa o comando `generate`, o Divisor copiará o conteúdo desses diretórios para o site gerado, sobrescrevendo quaisquer arquivos padrão com o mesmo nome. Isso permite que você adicione novos templates ou substitua os padrão fornecidos pelo tema.

### Personalizando o CSS

Para adicionar seu próprio CSS personalizado, você pode criar um arquivo chamado `extended.css` no diretório `divisor/assets`. Este arquivo será carregado após o CSS padrão do tema, permitindo que você substitua quaisquer estilos que desejar. Esta é a maneira recomendada de adicionar estilos personalizados para qualquer tema.

## Limpando o ambiente

Para remover os diretórios `source_repo` e `site_contents`, você pode usar o comando `clean`:

```bash
python cli.py clean
```

## `setup.py`

O arquivo `setup.py` é um script Python padrão usado para empacotar e distribuir a ferramenta Divisor. Ele define o nome do pacote, a versão, as dependências e os pontos de entrada. Você não precisa interagir com este arquivo diretamente, a menos que queira modificar o empacotamento da ferramenta.