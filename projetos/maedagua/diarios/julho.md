---
title: Diários de Pesquisa - Julho
description: 
published: true
date: 2025-07-29T09:41:58.167Z
tags: 
editor: markdown
dateCreated: 2025-07-12T11:15:04.725Z
---

# Diários de Pesquisa - Julho

Atividades realizadas no lab em Julho de 2025

## FF 

### 29.07.2025

Ao longo dos últimos dias, fiz mais um sprint de desenvolvimento do [Divisor](/projetos/divisor), e acho que por enquanto está estável: consigo gerar o site em jekyll, escolher um tema alternativo, e publicar com GitHub pages. Em futuras etapas, ainda quero implementar um script de configuração e dar uma limpada maior no código.

### 21.07.2025

Terminei a configuração inicial do Divisor e testei o processo de começar com um fork e customizar para publicação, com um site para o Lab Mãe D'água. Está aqui: https://maedagua.github.io/. Vou atualizar a documentação em Português no hotsite [Divisor](https://fonte-wiki.github.io/Divisor/).

### 18.07.2025

Mais algumas iterações com jules e cheguei a um protótipo que parece funcionar. Inspirado pela analogia da *fonte*, resolvi chamar o aplicativo de [Divisor](/projetos/divisor). Está rodando razoavelmente bem no meu ambiente local. Próximas etapas: ~~testar a publicação no GitHub pages~~, permitir usar outros temas do Jekyll compatíveis com GitHub Pages, e oferecer mais opções de customização.

**Atualizando:** a publicação no GitHub pages está funcionando. Fiz um [site para o próprio projeto Divisor](https://fonte-wiki.github.io/Divisor/) e uma ~~primeira versão de site para a Mãe D'água~~ (PS.: tirei esse site do ar mais tarde).

### 14.07.2025

Comecei a experimentar com a publicação automática de conteúdo em um site dedicado, puxando conteúdo do repositório git da fonte wiki e gerando um site Jekyll para GitHub pages. Esotu usando o jules para criar um script. Ele baixa o conteúdo do repositório de fonte.wiki, converte os arquivos .md para transformar a frontmatter e arrumar os links, copia as imagens, e publica como site jekyll. Ainda não consegui fazer funcionar perfeitamente. Localmente o script funciona. Mas não está publicando direito.

---