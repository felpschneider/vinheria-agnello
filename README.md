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

<div align="center">
<img width="800" alt="image" src="https">  
</div>

```
#include <DHT.h>
#include <LiquidCrystal.h>
 
#define DHTPIN 13
#define DHTTYPE DHT22
 
DHT dht(DHTPIN, DHTTYPE);  // Inicializa o sensor DHT
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);  // Inicializa o display LCD
 
const int ledRedPin = 8;  // Define o pino para o LED vermelho
const int ledYellowPin = 9;  // Define o pino para o LED amarelo
const int ledGreenPin = 10;  // Define o pino para o LED verde
 
const int lightSensorPin = A0;  // Define o pino para o sensor de luminosidade
const int humidityIdealMin = 60;  // Define a faixa ideal de umidade mínima
const int humidityIdealMax = 80;  // Define a faixa ideal de umidade máxima
const int temperatureIdealMin = 10;  // Define a faixa ideal de temperatura mínima
const int temperatureIdealMax = 15;  // Define a faixa ideal de temperatura máxima
 
void setup() {
  pinMode(ledRedPin, OUTPUT);  // Configura o pino do LED vermelho como saída
  pinMode(ledYellowPin, OUTPUT);  // Configura o pino do LED amarelo como saída
  pinMode(ledGreenPin, OUTPUT);  // Configura o pino do LED verde como saída
  lcd.begin(16, 2);  // Inicializa o display LCD com 16 colunas e 2 linhas
  dht.begin();  // Inicializa o sensor DHT
  lcd.clear();  // Limpa o display
  lcd.print("Inicializando...");  // Exibe uma mensagem de inicialização no display
  delay(2000);  // Aguarda 2 segundos
}
 
void loop() {
  float humidity = 0;
  float temperature = 0;
  int lightValue = analogRead(lightSensorPin);  // Lê o valor do sensor de luminosidade
  float humiditySum = 0;
  float temperatureSum = 0;
 
  for (int i = 0; i < 5; i++) {  // Realiza uma média de 5 leituras de temperatura e umidade
    humidity = dht.readHumidity();  // Lê a umidade do sensor DHT
    temperature = dht.readTemperature();  // Lê a temperatura do sensor DHT
 
    humiditySum += humidity;  // Soma as leituras de umidade
    temperatureSum += temperature;  // Soma as leituras de temperatura
    delay(1000);  // Aguarda 1 segundo entre as leituras
  }
 
  humidity = humiditySum / 5;  // Calcula a média da umidade
  temperature = temperatureSum / 5;  // Calcula a média da temperatura
 
  lcd.clear();  // Limpa o display
 
  // Verifica as condições de luminosidade e exibe mensagens correspondentes
  if (lightValue < 150) {
    digitalWrite(ledGreenPin, LOW);
    digitalWrite(ledYellowPin, LOW);
    digitalWrite(ledRedPin, HIGH); // LED vermelho para indicar problema
    lcd.setCursor(0, 0);
    lcd.print("Amb. muito claro");
  } else {
    digitalWrite(ledRedPin, LOW);
    if (lightValue >= 600) {
      digitalWrite(ledGreenPin, HIGH); // LED verde para indicar que está OK
      digitalWrite(ledYellowPin, LOW);
      lcd.setCursor(0, 0);
      lcd.print("Ambiente escuro");
    } else {
      digitalWrite(ledGreenPin, LOW);
      digitalWrite(ledYellowPin, HIGH); // LED amarelo para indicar níveis de alerta
      lcd.setCursor(0, 0);
      lcd.print("Amb. em meia luz");
      delay(3000); // Intervalo de leitura
    }
}
 
  // Verifica as condições de temperatura e exibe mensagens correspondentes
  if (temperature >= temperatureIdealMin && temperature <= temperatureIdealMax) {
    lcd.setCursor(0, 0);
    lcd.print("Temperatura OK");
  } else if (temperature > temperatureIdealMax) {
    lcd.setCursor(0, 0);
    lcd.print("Temperatura Alta");
  } else if (temperature < temperatureIdealMin) {
    lcd.setCursor(0, 0);
    lcd.print("Temperatura Baixa");
  }
  lcd.setCursor(0, 1);
  lcd.print("T: ");
  lcd.print(temperature);
  lcd.print("C");
  delay(3000);  // Aguarda 3 segundos
 
  // Verifica as condições de umidade e exibe mensagens correspondentes
  lcd.clear();
  if (humidity >= humidityIdealMin && humidity <= humidityIdealMax) {
    lcd.setCursor(0, 0);
    lcd.print("Umidade OK");
  } else if (humidity > humidityIdealMax) {
    lcd.setCursor(0, 0);
    lcd.print("Umidade Alta");
  } else if (humidity < humidityIdealMin) {
    lcd.setCursor(0, 0);
    lcd.print("Umidade Baixa");
  }
  lcd.setCursor(0, 1);
  lcd.print("H: ");
  lcd.print(humidity);
  lcd.print("%");
  delay(3000);  // Aguarda 3 segundos
}

```
# Links
Abaixo você pode acessar os links da apresentação do circuito
- [Video explicativo](https://youtu.be/T2frcA8sxnw?si=vxwQjn2FKPDpRfYJ)
- [Link da simulação no Wokwi](https://www.tinkercad.com/things/acs7l5mKNHh)

# Colaboradores
- Felipe Schneider
- Hugo Santos
- Maria Julia
- Thiago Araujo
- Vinicius Centurion
