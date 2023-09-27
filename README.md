# Vinheria Agnello

A tradicional Vinheria Agnello opera como loja física, e agora quer gerar a mesma experiência do usuário na Internet.

## Descrição

A qualidade é influenciada pela temperatura, umidade e luminosidade. Nosso projeto visa desenvolver um monitoramento no ambiente de armazenamento dos vinhos através de etapas. Nesta primeira entrega, iremos monitorar a luminosidade do espaço.

## Funcionalidades

Utilizamos o Arduino para ler a luminosidade do ambiente com um LDR e um sistema de LED's para sinalizar quando o ambiente atender as necessidades de luz (verde = ok, amarelo = atenção e vermelho = risco a qualidade). Adicionamos também um alarme que será tocado quando estiver em nível de alerta.

## Tecnologias utilizadas

- Linguagem C
- IDE Arduino
- Protoboard
- Placa de Arduino
- LEDs
- Resistores
- Buzzer
- LDR

## Rodando o projeto

Basta instalar o Arduino IDE e rodar o código abaixo:

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
  
  if (ldrValue > 170 || ldrValue < 80) {
    digitalWrite(greenLedPin, LOW);
    digitalWrite(yellowLedPin, LOW);
    digitalWrite(redLedPin, HIGH); // LED vermelho para indicar problema
  } else {
    digitalWrite(redLedPin, LOW);
    noTone(buzzerPin); // Desliga o buzzer
    if (ldrValue >= 90 && ldrValue <= 150) { // Evitar oscilação na zona de alerta
      digitalWrite(greenLedPin, HIGH); // LED verde para indicar que está OK
      digitalWrite(yellowLedPin, LOW);
    } else {
      digitalWrite(greenLedPin, LOW);
      digitalWrite(yellowLedPin, HIGH); // LED amarelo para indicar níveis de alerta
      tone(buzzerPin, 1000, 3000); // Liga o buzzer com frequência de 1000 Hz
    }
  }
  delay(1000); // Intervalo de leitura
}
```

# Colaboradores
- Felipe Schneider
- Hugo Santos
- Maria Julia
- Thiago Araujo
- Vinicius Centurion
