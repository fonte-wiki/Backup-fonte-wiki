---
title: HiperGuardiões  - 2015
description: 
published: true
date: 2025-08-14T19:59:01.896Z
tags: 
editor: markdown
dateCreated: 2025-08-14T19:52:27.118Z
---

## O que é

A proposta dos Hiperguardiões reúne a hiperconectividade com o conhecimento ancestral de guardiões míticos da biodiversidade, inspirados nas forças da natureza.Cada Hiperguardião é uma unidade de monitoramento de qualidade da água, ar, e observação de biodiversidade (por meio de câmeras para captura de imagens e sensores que captam sons), utilizando hardware livre/de baixo custo, software livre atrelados ao conhecimento ecológico da população local.

A estação funciona como uma [ZASF](https://web.archive.org/web/20150816061716/http://nuvem.tk/interactivos12/index.php/Redes_Aut%C3%B4nomas_%28Felipe_Fonseca_e_Vincenzo_Tozzi-Brasil%29#Usando_a_raspberry_pi_como_AP) (Zona Autônoma Sem Fio), distribuindo as informações coletadas e da biodiversidade em um determinado raio, acessível para a população local. Os dados coletados cada unidade-guardiã são transmitidos para a plataforma, alimentando o mapa do território. A intenção é formar uma rede de monitoramento que fomente processos de empoderamento, e estimulem a zeladoria dos recursos ecossistêmicos.

## O que desenvolvemos 
### Módulo de Monitoramento de Água
por Guima San e Thiago Baldivieso

**Nome:** Água Parâmetros que Avalia: PH, ORP - Redox, Condutividade elétrica, e temperatura. Materiais que Utiliza: Eletrodo de PH e ORP junto com o circuito amplificador, sonda junto com circuito acionador, sensor de temperatura.

![hiper01.png](/projetos/maedagua/hiper01.png)

**Como fazer:** Circuito de PH junto com ORP são similares, tanto é que podemos utilizar o mesmo sensor. No PH, o bulbo de vidro detecta íons de H+ e gera uma corrente elétrica (59,2 mV por unidade de pH a 25 oC). O sensor de ORP (geralmente é utilizado algum metal nobre no filamento como platina ou ouro), o gel interno é quem recebe a corrente elétrica positiva (+) e re-transmite ao interior do sensor, o fio de prata pura (tratado com cloreto de prata) capta a corrente e transmite ao cabo de conexão, que leva o sinal do sensor de PH ao leitor/controlador. Para leitura de sinais de PH e ORP foi utilizado um circuito amplificador de sinal e de comutação que será disponibilizado. Para o sensor de condutividade elétrica foi utilizado tal esquema:

O qual consiste na utilização do CI 555 de maneira que que ele funcione como um oscilador que envia sinais elétricos em determinados períodos de tempo, enquanto a sonda faz essa leitura de sinal. O sensor de temperatura consiste num transistor LM35 que foi adaptado para ser utilizado na água. O LM35 é um sensor de precisão em centígrados e tem uma tensão de saída analógica, sua faixa de medição é de -55° Ca +150° C. Sua tensão de saída consiste em 10 mV ∕ °C, que pode ser conectado a qualquer microcontrolador.

### Módulo de Monitoramento de Ar
por Guima San e Thiago Baldivieso

Parâmetros que Avalia: Umidade, Temperatura, Gases Estufa, Material particulado. Materiais que Utiliza: Sensor DHT 22, Sensor MQ7, DustSensor (material particulado) Como fazer: Conecta-se os sensores ao dispositivo controlador embarcado, então é realizada a leitura dos parâmetros via software. Sensor Particulado: Utilizado para diferenciar tamanho e quantidade de partículas por m³.

![hiper02.png](/projetos/maedagua/hiper02.png)

### Módulo Câmera de Observação de Biodiversidade e Captura Sonora
por Guima San e Thiago Baldivieso

Parâmetros que Avalia: Ruídos na natureza, presença de fauna e de biodiversidade Materiais que Utiliza: WebCamera compatível com o minicomputador.

**Como fazer:** Conecta-se a câmera junto ao raspberry Pi, então utiliza-se alguns comandos para download dos drivers compatíveis.

## ESTRUTURA

### Totem água
por Thiago Ceratti e Guima San

**O que é:** veículo robótico operado remotamente, construído com materiais de baixo custo.

**Materiais:**

- 01 barra de tubo PVC com Ø20 mm (diâmetro de 20 mm);
- 06 cotovelos 90o de PVC, com encaixe para tubos de Ø20 mm;
- 10 Tee PVC, com encaixa para tubo de Ø20 mm;
- 04 cotovelos 45o, com encaixe para tubo de Ø20mm
- 01 Flutuador de Espuma, para piscinas (macarrão de espuma, espaguete de espuma, etc)
- 01 pacote de abraçadeiras plásticas tipo fita hellerman (laça gato)
- 02 Motores de 6V DC
- 02 Potes para exame de urina (tamanho suficiente para alojar um motor dentro)
- 02 Pinos de dobradiça de porta (diâmetro do pino de 3 mm)
- 02 Hélices de nautimodelismo com duas blades, tamanho 40mm e furo de 3 mm;
- 02 Buchas de acoplamento do pino no eixo do motor (usinado, ou confeccionado em impressora 3D;
- 01 Bateria de 09V (de boa qualidade);
- 01 Ponte H shield (L298) para arduino;
- Fio (aproximadamente 1m para montagem e pelo menos 10 metros para navegação);
- 01 arduino uno;

![hiper03.png](/projetos/maedagua/hiper03.png)


**Como fazer:**
Corte o tubo de PVC em tamanhos conforme quantidades indicadas abaixo: 03 peças com 140 mm de comprimento; 02 peças com 90 mm de comprimento; 08 peças com 36 mm de comprimento; 04 peças com 128 mm de comprimento; 04 peças com 39 mm de comprimento; 04 peças com 125 mm de comprimento. Após o corte, recomenda-se que seja lixado as pontas cortadas, para remover possíveis rebarbas; Cortar o flutuador espuma em 4 peças de 113 mm de comprimento. Passar um tubo de 128mm de comprimento por dentro de cada espuma. Executar essa etapa com cuidado, a fim de executar um furo no centro da espuma. A montagem deverá ser executada conforme desenho anexo, observando-se a posição de cada peça na tabela localizada na legenda do desenho. Reserve a estrutura. Para a montagem dos propulsores faça dois furos passantes nas laterais nos potes, um furo no fundo e outro no centro da tampa. Passe o eixo do motor pelo furo da tampa, fixe a bucha de acoplamento com cola, e em seguida fixe a hélice no pino, e o pino na bucha, também com cola.Passe os fios do motor pelo furo no fundo do pote; Feche a tampa e vede as furações com cola quente (silicone); Fixe os conjuntos propulsores na estrutura através dos furos laterais dos potes, utilizando as fitas hellemans. Faça alguns furos na estrutura para auxiliar na fixação dos propulsores.Utilizar um pote Tupperware para alojamento das baterias e da ponte H, bem como da placa de arduino. Faça as ligações dos motores na ponte H. Alimente os motores com a bateria.


### Totem Terra
por Edgar Navarro
![hiper04.png](/projetos/maedagua/hiper04.png)
Materiais que Utiliza: cola, madeira compensada


----------------------------
> **IMPORTANTE:** Hiperguardiões encontra-se na licença Creative Commons CC BY SA 4.0. Se vc é um caiçara, pescadorx, quilombola, índix, roçeirx - ou faz parte de outra comunidade ou população que necessita de monitoramente - entre em contato conosco que podemos ajudar a desenvolver um hiperguardião pra você. MAS, se você acha que isso tudo é hype e pode ser utilizado como "inovação" "tendência" "emergência" para você ganhar editais, cooptar trabalho alheio, fortalecer sua "rede das redas" ou sei lá o que: Tome cuidado! Os piratas invocados por Hakim Bey guardam esse projeto e podem puxar seu pé no meio da noite.
{.is-warning}
