---
title: TBox
description: Caixa térmica de incubação microcontrolada
published: true
date: 2025-08-14T19:36:27.211Z
tags: 
editor: markdown
dateCreated: 2025-08-13T17:42:04.656Z
---

## Introdução

O objetivo da Therminator Box **(TBox)** é manter uma incubadora para cultura de bactérias com temperatura controlada. Quando ligada, a caixa porcura se regular automaticamente com a temperatura selecionada pelo botão angular (potenciômetro) desde que a temperatura desejada seja maior que a do ambiente. Caso deseje resfriar o ar da incubadora o lado da pastilha peltier deverá ser invertido ao desta montagem.

## Materiais

- [1 Arduino UNO](https://www.arduino.cc/en/Main/ArduinoBoardUno) atualizado com firmware [therminator-box](https://github.com/guimasan/T-box);
- 1 [Mini BreadBoard](https://www.sparkfun.com/breadboard-mini-modular-white.html);
- 1 [Transistor NPN TIP122](https://cdn-shop.adafruit.com/datasheets/TIP120.pdf) 
- 1 Fonte 12Volts 5A (no mínimo);
- Fios para eletrônica ;
- 1 [Pastilha peltier 12V ~ 40W](http://peltiermodules.com/peltier.datasheet/TEC1-12705.pdf);
![tbox1.png](/projetos/maedagua/tbox1.png)
- 1 Dissipador com relevo do tamanho da pastilha:
![tbox2.png](/projetos/maedagua/tbox2.png)
- 1 Dissipador do tamanho da pastila peltier:
![tbox3.png](/projetos/maedagua/tbox3.png)
- 1 Caixa plástica (Incubadoras que fiquem com temperatura de até 60⁰C):
![tbox4.png](/projetos/maedagua/tbox4.png)
- 1 [Sensor de temperatura](https://wiki.seeedstudio.com/Grove-Temperature_Sensor/):
![tbox5.png](/projetos/maedagua/tbox5.png)
- 1 Display [LCD](https://wiki.seeedstudio.com/Grove-LCD_RGB_Backlight/),e [também](https://wiki.seeedstudio.com/Grove-LCD_RGB_Backlight/)

## Como fazer

Marque o tamanho do relevo do dissipador escolhido, para que apenas essa área fique em contato com a parte interna da incubadora. Faça um corte na caixa plástica:
![tbox6.png](/projetos/maedagua/tbox6.png)

Acople o dissipador, se necessário pode ser colada a parte de baixo na caixa plástica com silicone de alta temperatura:
![tbox7.png](/projetos/maedagua/tbox7.png)

Passe pasta térmica no dissipador e na pastilha peltier. Coloque o lado que resfria da pastilha com o dissipador externo da caixa:
![tbox71.png](/projetos/maedagua/tbox71.png)
Adicione um dissipador menor que fará o papel de aquecer o ar interno da incubadora:
![tbox81.png](/projetos/maedagua/tbox81.png)
![tbox9.png](/projetos/maedagua/tbox9.png)
Coloque o sensor de temperatura próximo de onde ficará a amostra incubada:
![tbox10.png](/projetos/maedagua/tbox10.png)

A amostra não deve ficar sobre o dissipador interno pois o mesmo ficará com temperatura superior enquanto mantém o ar a caixa em temperatura controlada.

Conecte um [Transistor NPN Darlington TIP122 na protoboard](https://cdn-shop.adafruit.com/datasheets/TIP120.pdf):
![tbox11.png](/projetos/maedagua/tbox11.png)

Conecte o fio negativo (preto) da pastilha peltier no pino 2 do transistor TIP122 e o fio positivo (vermelho) da pastilha conecte na saída Vin do arduino
![tbox12.png](/projetos/maedagua/tbox12.png)

Conecte o sensor de temperatura na entrada A0 do Arduino (Neste exemplo o Arduino está com um shield de conexão (Groove Seeedstudio)
![tbox13.png](/projetos/maedagua/tbox13.png)

Conecte um potenciômetro (sensor angular resistivo) na entrada A1 do Arduino
![tbox14.png](/projetos/maedagua/tbox14.png)

Conecte o pino 3 do transistor TIP122 no GND do Arduino
![tbox15.png](/projetos/maedagua/tbox15.png)

Faça um dissipador de calor para o transistor TIP122. Passe pasta térmica na carcaça de junção dos metais
![tbox16.png](/projetos/maedagua/tbox16.png)

Conecte o pino 1 do transistor TIP122 na saída digital 3 ~ PWM do Arduino
![tbox17.png](/projetos/maedagua/tbox17.png)
![tbox18.png](/projetos/maedagua/tbox18.png)

Tampe a caixa e adicione o Display LCD
![tbox19.png](/projetos/maedagua/tbox19.png)
![tbox20.png](/projetos/maedagua/tbox20.png)

Conecte a fonte 12V 5A no Arduino e ajuste no potênciometro a temperatura na qual o dissipador deverá chegar e manter o ar da caixa aquecido
![tbox21.png](/projetos/maedagua/tbox21.png)

> Esta estufa ainda não é capaz de trabalhar com temperaturas maiores que 60⁰C por muito tempo por conta de uma limitação no tip122.
> 
> Pensando em acessibilidade e facilidade de replicação, uma versão simples (SV) foi desenvolvida:
{.is-info}


## Therminator Box SV (Small Version)

![tboxsmall.png](/projetos/maedagua/tboxsmall.png)

[Firmware](https://github.com/guimasan/therminator-box/blob/master/therminatorBoxSV.ino): 

Edite no código a temperatura (em graus Celsius) desejada, ex.: [ ] define TEMP 37 (37 é a temperatura desejada);

Proceda a montagem como no tutorial acima, substituindo o termistor sensor de temperatura da Grove Kit pelo lm35 e a fiação necessária.

Substitua o LCD Display pelo LED RGB Anôdo comum. O TherminatorBox SV ligará:

- LED Azul quando a temperatura estiver abaixo do desejado;
- LED Verde quando a temperatura estiver equilibrada com o desejado;
- LED Vermelho quando a temperatura estiver acima do dejesado.

Pode ser comum o LED Vermelho ligar quando a estufa estiver se equilibrando com a temperatura, por causa do delay entre o aquecimento do ar e o da pastilha.

Espere aproximadamente 10min para que a incubadora fique em temperatura equilibrada.
