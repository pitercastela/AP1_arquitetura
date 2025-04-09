# AP1_arquitetura

https://projecthub.arduino.cc/SURYATEJA/use-a-buzzer-module-piezo-speaker-using-arduino-uno-cf4191

https://www.makerhero.com/blog/sensor-ultrassonico-hc-sr04-ao-arduino/?srsltid=AfmBOorhNOONJLwkUA75pYpDuMNfVUfU2_QULKNMa_Sd3lJFDHHgpM7Z

(sensor ultrasônico)

//Programa: Conectando Sensor Ultrassonico HC-SR04 ao Arduino <br>
//Autor: MakerHero <br>

//Carrega a biblioteca do sensor ultrassonico <br>
#include <Ultrasonic.h> <br>

//Define os pinos para o trigger e echo <br>
#define pino_trigger 4 <br>
#define pino_echo 5 <br>

//Inicializa o sensor nos pinos definidos acima <br>
Ultrasonic ultrasonic(pino_trigger, pino_echo); <br>

void setup() <br>
{ <br>
  Serial.begin(9600); <br>
  Serial.println("Lendo dados do sensor..."); <br>
} <br>

void loop() <br>
{ <br>
  //Le as informacoes do sensor, em cm e pol <br>
  float cmMsec, inMsec; <br>
  long microsec = ultrasonic.timing(); <br>
  cmMsec = ultrasonic.convert(microsec, Ultrasonic::CM); <br>
  inMsec = ultrasonic.convert(microsec, Ultrasonic::IN); <br> 
  //Exibe informacoes no serial monitor <br>
  Serial.print("Distancia em cm: "); <br>
  Serial.print(cmMsec); <br>
  Serial.print(" - Distancia em polegadas: "); <br>
  Serial.println(inMsec); <br>
  delay(1000); <br>
}
