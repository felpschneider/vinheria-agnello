# Vinheria Agnello

A tradicional Vinheria Agnello opera como loja física, e agora quer gerar a mesma experiência do usuário na Internet, para isso, nos contrataram a fim de garantir a qualidade de seus vinhos.

## Descrição

A qualidade do vinho é influenciada pela temperatura, umidade e luminosidade. Nosso projeto visa desenvolver um monitoramento no ambiente de armazenamento dos vinhos através de etapas. Na primeira entrega, monitoramos a luminosidade do ambiente através de um circuito utilizando Arduino UNO e LDR (Light Dependent Resistor ou resistor dependente de luz).
Na segunda fase, iremos medir a temperatura e a umidade do ambiente utilizando um sensor integra DHT11 e a instalação de um display que mostra ao usuário a temperatura/umidade atual.


## Funcionalidades

O Arduino UNO utiliza um LDR para captar a luminosidade do ambiente e um sistema de LED's para sinalizar se o ambiente está garantindo a qualidade do vinho (Verde para OK, Amarelo para Atenção e Vermelho para Risco à Qualidade). Adicionamos também um alarme que será tocado quando estiver em nível de alerta.
Para monitorar a temperatura,o display mostra "Temperatura OK" enquanto estiver entre 10°C e 15°C, caso abaixo de 10°C, o display deve mostrar "Temp. baixa" e se acima de 15°C, "Temp. Alta". Para a umidade, o display deve mostrar "Umidade OK" entre 60 e 80%, "Umidade Alta" se acima de 70% e "Umidade Baixa" se abaixo de 50%. O alarme deve soar para os casos de Umidade Baixa/Alta e também para Temp. Baixa/Alta.



## Tecnologias e componentes utilizados

- Linguagem C
- IDE Arduino
- Protoboard
- Placa de Arduino
- LEDs (Verde, Amarelo e Vermelho)
- Resistores
- Buzzer
- LDR
- Jumpers
- Sensor DHT11
- Display
- DHT Sensor Library By Adafruit

## Rodando o projeto

Para rodar, basta instalar você pode acessar a simulação que fizemos [neste link](https://wokwi.com/projects/378787494974960641) ou então montar o circuito da imagem e rodar o código a seguir:

![MicrosoftTeams-image](https://github.com/felpschneider/vinheria-agnello/assets/89404927/8b1ffbeb-e785-4b10-92ac-4e6b7521da7e)

# Links
Abaixo você pode acessar os links da apresentação do circuito
- [Video explicativo](https://youtu.be/T2frcA8sxnw?si=vxwQjn2FKPDpRfYJ)
- [Link da simulação no Wokwi](https://wokwi.com/projects/378787494974960641)

# Colaboradores
- Felipe Schneider
- Hugo Santos
- Maria Julia
- Thiago Araujo
- Vinicius Centurion
