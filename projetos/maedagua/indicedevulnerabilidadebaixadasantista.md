---
title: Siren
description: Índice de Vulnerabilidade Costeira da Baixada Santista
published: true
date: 2026-10-14T23:21:00.018Z
tags: 
editor: markdown
dateCreated: 2026-06-10T13:15:37.220Z
---

# Siren

Na mitologia grega, [sereias](https://www.nationalgeographicbrasil.com/historia/2023/05/a-origem-das-sereias-o-que-diz-a-historia) são criaturas híbridas com corpo de pássaros e rosto de mulher, que viviam nos oceanos e mares atraindo marinheiros com canções hipnóticas. Embora suas origens sejam difusas, é provável que suas tragetórias estejam relacionadas com o mundo dos mortos, assim como a das [Valquírias](https://pt.wikipedia.org/wiki/Valqu%C3%ADrias). Segundo a lenda, aquele que fosse capaz de ignorar às canções de uma sereia, deveria morrer. Quando passaram a ser massivamente ignoradas, perderam o seu dom, e se esconderam no fundo do mar com as [criaturas luminescentes nas zonas abissais](https://revistapesquisa.fapesp.br/wp-content/uploads/2025/07/044-047_bioluminescencia-marinha_354.pdf).

Com a emergência climática e a vulnerabilidade das populações costeiras e pesqueiras, acentuanda pelo ["Super" El Niño de 2026-2027](https://wmo-int.translate.goog/news/media-centre/wmo-prepare-el-nino?_x_tr_sl=en&_x_tr_tl=pt&_x_tr_hl=pt&_x_tr_pto=tc), as sereias vieram à tona, novamente, utilizando tecnomagia como meio e [PureData](https://puredata.info/) para emitir sirenes - em uma analogia aos dados puros, [sem distorções políticas de que é um hoax ou que ainda há tempo](https://apublica.org/2026/02/manipulando-a-ciencia-trump-faz-seu-pior-ataque-a-luta-contra-a-crise-climatica/). 

![badgesiren.png](/projetos/maedagua/badgesiren.png)

A proposta de Siren consiste em avaliar a Vulnerabilidade Costeira dos 9 Municípios da Baixada Santista, correlacionando diferentes camadas de dados, a partir da perspectiva de uma ["análise quente"](https://www.youtube.com/watch?v=hd7JhiKQmi8&t=20) utilizando: 

- O [Índice de Progresso Social (IPS/Imazon)](https://ipsbrasil.org.br/explore/scorecard/1100015), que mede a qualidade de vida da população a partir da correlação de saneamento, saúde, educação, moradia, segurança e acesso a oportunidades. Quanto maior a nota, melhor a situação. Como o nosso índice mede vulnerabilidade, e não progresso, invertemos essa nota: subtraímos o valor de 100. Assim, uma cidade com nota social mais baixa aparece com mais vulnerabilidade, e todas as variáveis passam a apontar na mesma direção, onde número maior significa situação mais delicada;

- Aumento do Nível do Mar: Usamos a ferramenta [Coastal Risk Screening Tool](coastal.climatecentral.org), da Climate Central, com um cenário de 1 metro de elevação do mar. O mapa mostra quais áreas de cada cidade ficariam abaixo da linha da maré. Observamos o tamanho e a natureza dessas áreas: regiões industriais, de estuário e densamente povoadas pesam mais do que trechos de praia pouco ocupados;

- Poluição nas áreas de risco: analisamos se as áreas que podem ser alcançadas pelo mar também sofrem com contaminação, e de que tipo (industrial, portuária, esgoto). As fontes principais são os relatórios da Companhia Ambiental do Estado de São Paulo - CETESB e estudos científicos sobre o estuário e os manguezais da região. O risco é que o avanço do mar remexa e espalhe poluentes que já estão depositados no solo e nos sedimentos;

- Estresse térmico: usamos como base o [Índice Climático Térmico Universal  - UTCI](https://portal.inmet.gov.br/uploads/icones/Conforto_t%C3%A9rmico_inmet.pdf), uma espécie de sensação térmica que combina temperatura, umidade, vento e radiação solar. Como o Instituto Nacional de Meteorologia - INMET não tem estações meteorológicas em todos os municípios, não foi possível calcular esse índice com dados para cada cidade. Por isso, esta variável foi tratada de forma qualitativa: usamos a classificação oficial de estresse térmico do INMET, registros de ondas de calor e a previsão de El Niño forte para a primavera e o verão de 2026. Santos e Bertioga têm registros mais específicos de temperaturas extremas e por isso pontuam mais alto. Nas demais cidades, vale o padrão regional. Essa abordagem foi confirmada pela coordenação do projeto como a forma final de tratar essa variável.

Cada variável foi colocada em uma escala de 0 a 100, em que 100 significa a situação mais vulnerável. Como o IPS já possui uma escala numérica, apenas invertemos. Para o nível do mar e a poluição aplicamos classificações (baixo, moderado, alto, crítico), e para cada classificação atribuímos um valor nessa escala. A medida de 0 a 100 não é uma unidade física, como metros ou toneladas: é uma régua criada para que tipos de dados diferentes possam ser comparados e somados. O índice final é a média das quatro variáveis, todas com o mesmo peso, 25% cada. Esses pesos foram confirmados pela coordenação do projeto.

![ipstabela.png](/projetos/maedagua/ipstabela.png)

**Limites do Índice de Vulnerabilidade Costeira**
O IPS, os dados referente ao aumento do nível do mar e de poluição têm base sólida e específica para cada município. Porém o estresse térmico é uma variável menos precisa, por falta de estações de medição em cada cidade.

Com isso, criamos uma leitura crítica de cada cidade da Baixada Santista, traduzida em um canto, em uma leitura sonoro: quanto mais grave a situação, mais grave (literalmente) o som.

[Bertioga](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/bertioga) 
[Cubatão](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/cubatao) 
[Guarujá](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/guaruja)
[Itanhaém](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/itanhaem) 
[Mongaguá](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/monguaga) 
[Peruíbe](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/peruibe) 
[Praia Grande](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/praiagrande) 
[Santos](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/santos) 
[São Vicente](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/saovicente) 





