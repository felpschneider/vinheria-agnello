# Vinheria Agnello

A tradicional Vinheria Agnello opera como loja física, e agora quer gerar a mesma experiência do usuário na Internet, para isso, nos contrataram a fim de garantir a qualidade de seus vinhos.

## Descrição

A qualidade do vinho é influenciada pela temperatura, umidade e luminosidade. Nosso projeto visa desenvolver um monitoramento no ambiente de armazenamento dos vinhos através de etapas. Nesta primeira entrega, monitoraremos a luminosidade do ambiente através de um circuito utilizando Arduino UNO e LDR (Light Dependent Resistor ou resistor dependente de luz).

## Funcionalidades

O Arduino UNO utiliza um LDR para captar a luminosidade do ambiente e um sistema de LED's para sinalizar se o ambiente está garantindo a qualidade do vinho (Verde para OK, Amarelo para Atenção e Vermelho para Risco à Qualidade). Adicionamos também um alarme que será tocado quando estiver em nível de alerta.

## Tecnologias e componentes utilizados

- Linguagem C
- IDE Arduino
- Protoboard
- Placa de Arduino
- LEDs (Verde, Amarelo e Vermelho;
- Resistores
- Buzzer
- LDR
- Jumpers

## Rodando o projeto

Para rodar, basta instalar você pode acessar a simulação que fizemos [neste link](https://www.tinkercad.com/things/acs7l5mKNHh) ou então montar o circuito da imagem e rodar o código a seguir:

<div align="center">
<img width="800" alt="image" src="https://github.com/felpschneider/vinheria-agnello/assets/89404927/32b2adbb-00b1-4885-9f61-fdfc0ae604cd">  
</div>

```
const int ldrPin = A0;
const int greenLedPin = 2;
const int yellowLedPin = 3;
const int redLedPin = 4;
const int buzzerPin = 5;

int ldrValue;

void setup() {
  pinMode(greenLedPin, OUTPUT);
  pinMode(yellowLedPin, OUTPUT);
  pinMode(redLedPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  
  noTone(buzzerPin); // Garante que o buzzer esteja desligado no início
  
  Serial.begin(9600);
}

void loop() {
  ldrValue = analogRead(ldrPin);
  
  Serial.print("Luminosidade: ");
  Serial.println(ldrValue);
  
  if (ldrValue < 150) {
    digitalWrite(greenLedPin, LOW);
    digitalWrite(yellowLedPin, LOW);
    digitalWrite(redLedPin, HIGH); // LED vermelho para indicar problema
    tone(buzzerPin, 1000, 3000); // Liga o buzzer com frequência de 1000 Hz
  } else {
    digitalWrite(redLedPin, LOW);
    noTone(buzzerPin); // Desliga o buzzer
    if (ldrValue >= 600) { // Evitar oscilação na zona de alerta
      digitalWrite(greenLedPin, HIGH); // LED verde para indicar que está OK
      digitalWrite(yellowLedPin, LOW);
    } else {
      digitalWrite(greenLedPin, LOW);
      digitalWrite(yellowLedPin, HIGH); // LED amarelo para indicar níveis de alerta
      tone(buzzerPin, 1000, 3000); // Liga o buzzer com frequência de 1000 Hz
      delay(3000); // Intervalo de leitura
    }
  }
  
  delay(1000); // Intervalo de leitura
}
```
# Links
Abaixo você pode acessar os links da apresentação do circuito
- [Video explicativo](https://www.youtube.com/watch?v=bieb-WQjR_w)
- [Link da simulação no Tinkercad](https://www.tinkercad.com/things/acs7l5mKNHh)

# Colaboradores
- Felipe Schneider
- Hugo Santos
- Maria Julia
- Thiago Araujo
- Vinicius Centurion
