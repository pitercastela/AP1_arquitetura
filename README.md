//Carrega a biblioteca do sensor ultrassonico
#include <Ultrasonic.h>

//Define os pinos para o trigger e echo
#define pino_trigger 4
#define pino_echo 5
//Define o buzzer
#define buzzer 6
//Define os LEDs
#define LED1 7
#define LED2 8
#define LED3 9
#define LED4 10
#define LED5 11
#define LED6 23
#define LED7 24
//Define as chaves
#define CHAVE1 12
#define CHAVE2 13



//Inicializa o sensor nos pinos definidos acima
Ultrasonic ultrasonic(pino_trigger, pino_echo);

void setup()
{
//Inicializa o monitor serial e define as entradas e saídas do sistema
  Serial.begin(9600);
  Serial.println("Lendo dados do sensor...");
  pinMode(buzzer,OUTPUT);
  pinMode(LED1,OUTPUT);
  pinMode(LED2,OUTPUT);
  pinMode(LED3,OUTPUT);
  pinMode(LED4,OUTPUT);
  pinMode(LED5,OUTPUT);
  pinMode(CHAVE1,INPUT);
  pinMode(CHAVE2,INPUT);
  pinMode(LED6,OUTPUT);
  pinMode(LED7,OUTPUT);
}

void loop()
{
//Lê o valor das duas chaves do programa
  int val1 = digitalRead(CHAVE1);
  int val2 = digitalRead(CHAVE2);  
  //Le as informacoes do sensor, em cm e pol
  float cmMsec, inMsec;
  long microsec = ultrasonic.timing();
  cmMsec = ultrasonic.convert(microsec, Ultrasonic::CM);
delay(200);

// Verifica se a distancia está entre 4 e dois metros
  if (cmMsec/100 <= 4 && cmMsec/100 >= 2) {
    //verifica se alguma das chaves está ligada
    if(val1 == 1 || val2 == 1){
    // Executa a sequência luminosa
digitalWrite(LED1,HIGH);
delay(100);
digitalWrite(LED1,LOW);
digitalWrite(LED2,HIGH);
delay(100);
digitalWrite(LED2,LOW);
digitalWrite(LED3,HIGH);
delay(100);
digitalWrite(LED3,LOW);} else{ 
//se as chaves estiverem desligadas, nada acontece
  digitalWrite(LED1,LOW);
digitalWrite(LED2,LOW);
digitalWrite(LED3,LOW);
digitalWrite(LED4,LOW);
digitalWrite(LED5,LOW);}
// Verifica se ambas as chaves estão ligadas
if (val1 == 1 && val2 == 1){
//Ativa o buzzer
tone(buzzer, 1000);
delay(250);
  noTone(buzzer);
delay(250);
  } else{ noTone(buzzer);}} else if(cmMsec/100 >= 1 && cmMsec/100 < 2){ //Verifica se a distância é menor que 2 metros e maior ou igual a 1 metro
  //verifica se alguma das chaves está ligada
    if (val1 == 1 || val2 == 1){
    // Executa a sequência luminosa
digitalWrite(LED1,HIGH);
delay(50);
digitalWrite(LED1,LOW);
digitalWrite(LED2,HIGH);
delay(50);
digitalWrite(LED2,LOW);
digitalWrite(LED3,HIGH);
delay(50);
digitalWrite(LED3,LOW);
digitalWrite(LED4,HIGH);
delay(50);
digitalWrite(LED4,LOW);}else{
// Se ambas as chaves estiverem desligadas, nada acotnece
  digitalWrite(LED1,LOW);
digitalWrite(LED2,LOW);
digitalWrite(LED3,LOW);
digitalWrite(LED4,LOW);
digitalWrite(LED5,LOW);}
//Verifica se ambas as chaves estão ligadas
if (val1 == 1 && val2 == 1){
// Ativa o buzzer
tone(buzzer, 600);
delay(150);
  noTone(buzzer);
delay(100);
  }else{ noTone(buzzer);}} else if(cmMsec/100 < 1){ //Verifica se a distância é menor do que 1 metro
  // Verifica se alguma das chaves está ligada
    if (val1 == 1 || val2 == 1){
    //Executa a sequência luminosa
digitalWrite(LED1,HIGH);
digitalWrite(LED2,HIGH);
digitalWrite(LED3,HIGH);
digitalWrite(LED4,HIGH);
digitalWrite(LED5,HIGH);}else{ // Se ambas as chaves estiverem desligadas, nada acontece
  digitalWrite(LED1,LOW);
digitalWrite(LED2,LOW);
digitalWrite(LED3,LOW);
digitalWrite(LED4,LOW);
digitalWrite(LED5,LOW);}
//Verifica se ambas as chaves estão ligadas
if (val1 == 1 && val2 == 1){
// Ativa o buzzer
    tone(buzzer, 200);}else{ noTone(buzzer);}
  } else {noTone(buzzer); // Desliga os leds e o buzzer se ambas as chaves estiverem desativadas
  digitalWrite(LED1,LOW);
digitalWrite(LED2,LOW);
digitalWrite(LED3,LOW);
digitalWrite(LED4,LOW);
digitalWrite(LED5,LOW);}
// Verifica se a chave1 está ligada
if (val1 == 1){
  digitalWrite(LED6,HIGH);
}else{digitalWrite(LED6,LOW);}
// Verifica se a chave2 está ligada
if (val2 == 1){
  digitalWrite(LED7,HIGH);
}else{digitalWrite(LED7,LOW);}
// Escreve a distância em metros no monitor serial.
  Serial.print("Distancia em m: ");
  Serial.println(cmMsec/100);
}
