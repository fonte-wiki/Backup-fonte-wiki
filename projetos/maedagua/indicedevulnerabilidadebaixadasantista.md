---
title: Siren
description: Índice de Vulnerabilidade Costeira da Baixada Santista
published: true
date: 2026-11-12T18:02:03.014Z
tags: 
editor: markdown
dateCreated: 2026-06-10T13:15:37.220Z
---

# Siren

Na mitologia grega as [sereias](https://www.nationalgeographicbrasil.com/historia/2023/05/a-origem-das-sereias-o-que-diz-a-historia) foram descritas como criaturas híbridas com corpo de pássaros e rosto de mulher, que viviam nos oceanos e mares inebriando marinheiros com canções hipnóticas. Embora as origens dessas histórias sejam difusas, é provável que suas trajetórias estejam relacionadas com o mundo dos mortos, assim como a das [Valquírias](https://pt.wikipedia.org/wiki/Valqu%C3%ADrias). Segundo a lenda, quem ignorasse às canções de uma sereia, deveria morrer. Quando as sereias passaram a ser massivamente ignoradas, perderam o seu dom, e se esconderam no fundo do mar com as criaturas bioluminescentes nas zonas abissais.

Com a emergência climática e a vulnerabilidade das populações costeiras e pesqueiras, acentuanda pelo ["Super" El Niño de 2026-2027](https://wmo-int.translate.goog/news/media-centre/wmo-prepare-el-nino?_x_tr_sl=en&_x_tr_tl=pt&_x_tr_hl=pt&_x_tr_pto=tc), as sereias vieram à tona, novamente, para emitir sirenes em forma de cantos.

![badgesiren.png](/projetos/maedagua/badgesiren.png)

> “(...) é magia que nós fazemos, é sagrado e grandioso. Existem lendas sobre pessoas que nasceram com o dom de fazer música tão autêntica, que pode rasgar o véu entre a vida e a morte, evocando espíritos do passado e do futuro”. [Sinners](https://www.youtube.com/watch?v=S7jo5Cr6WUA).


##### Sirene de  Iemanjá, Oxum, e Olokum - ouça no Spotify ou Podomatic


Siren agrega dados sobre clima, indicadores sociais, aumento do nível do mar, estresse térmico e poluição para mensurar a vulnerabilidade dos nove municípios da Baixada Santista (Bertioga, Cubatão, Guarujá, Itanhaém, Mongaguá, Peruíbe, Praia Grande, Santos, São Vicente ), litoral sul do Estado de São Paulo. 

![baixadasantista.png](/projetos/maedagua/baixadasantista.png)
Fonte: [Quintanilha, 2012](https://www.researchgate.net/publication/275985484_Modelagem_para_integracao_de_dados_sobre_macrobentos_em_Infraestrutura_de_Dados_Espaciais).

A Baixada Santista é  a [17ª região metropolitana](
https://www.emtu.sp.gov.br/emtu/institucional/quem-somos/baixada-santista.fss) mais populosa do Brasil, abriga cerca de 12% da população brasileira,  parque industrial de Cubatão e o complexo portuário de Santos, responsável por mais de um terço de todo o comércio exterior do Brasil e 55% da renda nacional, o Porto de Santos é o maior e mais importante complexo portuário da América do Sul. 

A proposta de Siren consiste em avaliar a Vulnerabilidade Costeira dos 9 Municípios da Baixada Santista, correlacionando diferentes camadas de dados, a partir da perspectiva de uma ["análise quente"](https://www.youtube.com/watch?v=hd7JhiKQmi8&t=20) utilizando: 

- O [Índice de Progresso Social (IPS/Imazon)](https://ipsbrasil.org.br/explore/scorecard/1100015), que mede a qualidade de vida da população a partir da correlação de saneamento, saúde, educação, moradia, segurança e acesso a oportunidades. Quanto maior a nota, melhor a situação. Como o nosso índice mede vulnerabilidade, e não progresso, invertemos essa nota: subtraímos o valor de 100. Assim, uma cidade com nota social mais baixa aparece com mais vulnerabilidade, e todas as variáveis passam a apontar na mesma direção, onde número maior significa situação mais delicada;

- Aumento do Nível do Mar: Usamos a ferramenta [Coastal Risk Screening Tool](http://coastal.climatecentral.org), da Climate Central, com um cenário de 1 metro de elevação do mar. O mapa mostra quais áreas de cada cidade ficariam abaixo da linha da maré. Observamos o tamanho e a natureza dessas áreas: regiões industriais, de estuário e densamente povoadas pesam mais do que trechos de praia pouco ocupados;

- Poluição nas áreas de risco: analisamos se as áreas que podem ser alcançadas pelo mar também sofrem com contaminação, e de que tipo (industrial, portuária, esgoto). As fontes principais são os relatórios da Companhia Ambiental do Estado de São Paulo - CETESB e estudos científicos sobre o estuário e os manguezais da região. O risco é que o avanço do mar remexa e espalhe poluentes que já estão depositados no solo e nos sedimentos;

- Estresse térmico: usamos como base o [Índice Climático Térmico Universal  - UTCI](https://portal.inmet.gov.br/uploads/icones/Conforto_t%C3%A9rmico_inmet.pdf), uma espécie de sensação térmica que combina temperatura, umidade, vento e radiação solar. Como o Instituto Nacional de Meteorologia - INMET não tem estações meteorológicas em todos os municípios, não foi possível calcular esse índice com dados para cada cidade. Por isso, esta variável foi tratada de forma qualitativa: usamos a classificação oficial de estresse térmico do INMET, registros de ondas de calor e a previsão de El Niño forte para a primavera e o verão de 2026. Santos e Bertioga têm registros mais específicos de temperaturas extremas e por isso pontuam mais alto. Nas demais cidades, vale o padrão regional. Essa abordagem foi confirmada pela coordenação do projeto como a forma final de tratar essa variável.

Cada variável foi colocada em uma escala de 0 a 100, em que 100 significa a situação mais vulnerável. Como o IPS já possui uma escala numérica, apenas invertemos. Para o nível do mar e a poluição aplicamos classificações (baixo, moderado, alto, crítico), e para cada classificação atribuímos um valor nessa escala. A medida de 0 a 100 não é uma unidade física, como metros ou toneladas: é uma régua criada para que tipos de dados diferentes possam ser comparados e somados. O índice final é a média das quatro variáveis, todas com o mesmo peso, 25% cada. 

Ao final, foram estabelecidas três escalas de vulnerabilidade para Siren (média até 40 pontos, importante de 40 à 60 pontos, e alta mais de 60 pontos), com cores semafóricas relativas as três Orixás que transitam nos ambientes de água, sendo: Iemanjá/azul-média, Oxum/amarela-importante, e Olokun/preta-alta. Essa escala também gerou três sirenes de alerta específicas. Com isso, criamos uma leitura de cada cidade da Baixada Santista, traduzida em um canto, em uma leitura sonora, que quanto mais vulnerável mais aguda fica.

![tabelasirenajustada.png](/projetos/maedagua/tabelasirenajustada.png)

Ao aplicarmos Siren para toda a Baixada Santista, o resultado mostrado é importante vulnerabilidade (58/100), um número equivalente do município do Guarujá, o quinto mais vulnerável. Um resultado que em números absolutos e no ranking representa exatamente a média geral da pontuação do índice e da quantidade de municípios. Porém esse resultado não mostra um equilíbrio por si só, já que os municípios além de vivenciarem realidades bastantes heterogêneas, também é composto por extremos de Peruíbe e Cubatão.

![tabelasirenbxd.png](/projetos/maedagua/tabelasirenbxd.png)

Em um extremo temos Cubatão, uma cidade rodeada de manguezais alagáveis, com alto passivo de contaminantes, moradias irregulares, Produto Interno Bruto (PIB) de mais de R$ 240.000,00, um modelo que sublinha a lógica de esgotamento e hiperexploração de recursos que trouxe a humanidade às crises que estamos vivenciando. Do outro, Peruíbe um território que abriga uma grande porção de Mata Atlântica mas possui um PIB de pouco mais de R$ 33.000,00 (IPS Brasil, 2026).

O modelo de estruturação da Baixada Santista, focado na exploração de recursos, mão de obra e turismo, sem projetos voltados à estruturas sustentáveis, pagamento de serviços ambientais, inovação e valorização de cultura e características locais, se repete até hoje. Porém, em um contexto temporal que exige urgência e não repetição. 

Os dados de Siren para cada município, juntamente com as composições sonoras foram disponibilizadas em páginas wiki colaborativas (que podem ser acessadas no final dessa página), com uma breve análise crítica de cada cidade, que podem ser editadas posteriormente. Para os municípios Bertioga, Cubatão, Guarujá, Praia Grande, Santos, São Vicente, foi acrescentado um dado descritivo relativo a contaminantes que não foi adicionado como variável em Siren por não haver dados disponíveis para os nove municípios. 

Para a análise de contaminantes, utilizada de forma complementar como crítica territorial, foram levantados 1668 pontos georreferenciados de ocorrência de metais ou metalóides. Os municípios que tiveram valores de concentração de metais foram Santos (837, 50%), Cubatão (477, 29%), São Vicente (171, 10%), Bertioga (107, 6%), Guarujá (65, 4%) e Praia grande (11, 1%). Dentre os metais estudados estão Alumínio (Al), ferro (Fe), prata (Ag), arsênio (As), cádmio (Cd), cobalto (Co), cromo (Cr), cobre (Cu), gálio (Ga), mercúrio (Hg), lantânio (La), lítio (Li), manganês (Mn), níquel (Ni), chumbo (Pb), paládio (Pd), platina (Pt), ródio (Rh), antimônio (Sb), escândio (Sc), selênio (Se), estanho (Sn), estrôncio (Sr), titânio (Ti), vanádio (V) e zinco (Zn). 

As concentrações dos elementos químicos nos sedimentos da Baixada Santista podem estar associadas a diferentes fontes antropogênicas, incluindo atividades industriais, portuárias e navais, lançamento de efluentes urbanos e industriais, escoamento superficial e deposição atmosférica. Processos metalúrgicos e químicos podem contribuir para a presença de elementos como Cr, Cu, Pb, Zn, Cd e Hg, enquanto atividades portuárias e navais podem estar relacionadas à introdução de metais provenientes de tintas anti-incrustantes, corrosão de estruturas e manutenção de embarcações. Além disso, fontes naturais, como o intemperismo de rochas e o transporte de partículas pelos rios, também podem contribuir para as concentrações observadas. Nas tintas utilizadas em embarcações, especialmente nas tintas anti-incrustantes (antifouling), podem estar presentes Cu (cobre), Zn (zinco), Pb (chumbo), Cr (cromo), Hg (mercúrio) e Ag (prata), dependendo da formulação e da época de aplicação. O cobre é utilizado como biocida, enquanto o zinco pode estar presente em biocidas e pigmentos. Chumbo, cromo e mercúrio podem ocorrer em pigmentos ou formulações antigas, embora seu uso seja restrito ou proibido em diversas aplicações. A prata também pode ser empregada em formulações específicas com ação antimicrobiana. Portanto, a presença desses metais e suas possíveis fontes necessitam de uma análise mais robusta para entender sua ocorrência e distribuição no ambiente, assim como seus impactos sistêmicos e exponenciais.


**Limites do Índice de Vulnerabilidade Costeira**
O IPS, os dados referente ao aumento do nível do mar e de poluição têm base sólida e específica para cada município. Porém o estresse térmico é uma variável menos precisa, por falta de estações de medição em cada cidade.

**Contaminantes**
Para o dado de contaminantes foi utilizado o Índice Quociente das Diretrizes de Qualidade de Sedimentos (SQGQ), uma ferramenta importante para identificar pontos de altas concentrações de sedimentos contaminados e avaliar o impacto potencial sobre organismos e a biodiversidade. Seu cálculo envolve os valores de concentração investigados nos locais de interesse, valores-guia que são Threshold Effect Level (TEL) e Probable Effect Level (PEL) e a quantidade de contaminantes presentes. 

**Acesse mais informações sobre as cidades**

[Bertioga](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/bertioga) 
[Cubatão](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/cubatao) 
[Guarujá](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/guaruja)
[Itanhaém](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/itanhaem) 
[Mongaguá](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/monguaga) 
[Peruíbe](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/peruibe) 
[Praia Grande](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/praiagrande) 
[Santos](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/santos) 
[São Vicente](/projetos/maedagua/indicedevulnerabilidadebaixadasantista/saovicente) 





