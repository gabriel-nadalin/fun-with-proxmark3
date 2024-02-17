# Fun With Proxmark3
**Ou como clonar o passe de ônibus :P**<br>
(Para propósitos puramente didáticos, claro)

# Introdução
**RFID**<br>
**R**adio-**F**requency **ID**entification, ou identificação por radiofrequência é um método de identificação automática, em que dados, transmitidos por tags RFID através de ondas de rádio, são captados por um leitor. Tags RFID são compostas por, no mínimo, uma antena, responsável por receber sinais de interrogação do leitor e transmitir respostas da tag, e um chip, ou circuito, que armazena e gerencia os dados gravados na tag. Sistemas RFID operam em diferentes frequências e são amplamente utilizados em diversas aplicações, como cartões de identificação, rastreamento de objetos e animais, pagamentos por aproximação e tarifas automáticas em pedágios ou, como veremos adiante, passes de ônibus.<br>
Mais informações sobre RFID [aqui](https://en.wikipedia.org/wiki/Radio-frequency_identification)

**MIFARE**<br>
MIFARE é uma série de chips de circuito integrado usados em cartões de proximidade, baseada em vários níveis do padrão ISO/IEC 14443 Type-A, operando em 13.56 MHz (hf, high frequency). Existem várias versões de tags MIFARE, mas, no geral, seus dados são divididos em blocos, esses agregados em setores, protegidos por chaves.

<img src="./images/MiFare1k.png" alt="mifare1k" height="400"><br>
<img src="./images/mifare1k_legend.png" alt="mifare1klegend" height="150">

Mais notavelmente, o bloco 0 é reservado para o ID único de cada tag (UID) e demais informações de fabricação, e o quarto bloco de cada setor para suas chaves e bits de acesso. Cada uma das chaves (A e B) pode ser associada a diferentes níveis de permissão para o setor, como somente leitura ou leitura e escrita. Basicamente, um leitor só pode ler ou escrever em um setor de alguma tag caso possua a(s) chave(s) correta(s) para aquele setor (e as condições de acesso, definidas pelos bits de acesso, permitam).<br>
Mais informações sobre MIFARE [aqui](https://en.wikipedia.org/wiki/MIFARE)

**Proxmark**<br><img src="url" alt="alt text" width="whatever" height="whatever">
Proxmark é um dispositivo que permite ler, escrever e simular tags RFID e farejar comunicações entre leitor e tag, e suporta tags lf e hf (low frequency [120-150 kHz] e high frequency [13.56 MHz]).

<img src="https://github.com/gabriel-nadalin/fun-with-proxmark3/assets/131068505/b2759fde-1d1c-4f6c-b9de-6e5553795201" alt="proxmark" width="400">

Firmware utilizado: Iceman Fork - Proxmark3, disponível [aqui](https://github.com/RfidResearchGroup/proxmark3)

# Agora sim - o exploit
**Objetivo**: encontrar alguma vulnerabilidade em um sistema RFID.<br>
**Sistema escolhido**: passe de ônibus; cartão de aproximação.<br><br>
Com o proxmark conectado a uma porta USB, podemos acessar sua interface com o comando `pm3`

![pm3](./images/pm3.png)

Com o cartão posicionado em cima do proxmark e o comando `auto` podemos tentar identificar com que tipo de tag estamos lidando:
