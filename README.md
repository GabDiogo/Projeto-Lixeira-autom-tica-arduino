PROJETO ARDUINO
Lixeira Automática com sensor ultrassônico

Membros do projeto:
191204B16, 2683210, Gabriel Diogo, gabriel.diogo2909@gmail.com, Líder
191204B16, 2451830, Gustavo Severiano dos Santos, gustavocklseveriano@gmail.com, Membro

O que é o projeto? 
O projeto da lixeira inteligente é formado por um sensor ultrassônico, com a função de presenciar a aproximação do lixo, e um servo motor, que tem a função de abrir e fechar a tampa do lixo automaticamente, a lixeira tem objetivo de facilitar o descarte de resíduos, fazendo com que não precise fazer o movimento de abrir e fechar a tampa, somente se aproximar.

Futuras melhorias para o projeto: 
Algumas possíveis futuras melhorias para a lixeira, são a implementação de sensores bluetooth ou wifi, para poder enviar sinais e notificações ao usuario, mostrando o volume da lixeira, ou em qual momento ela foi ativa e desativada, e a segunda melhoria é um sensor de carga, para medir o volume da lixeira e poder comunicar com a implementação de um led, se a lixeira está vazia ou cheia.

Link youtube: https://www.youtube.com/watch?v=FY99PwPNIlw 

Materiais para fazer o projeto:
- Balde de lixo
- Placa fina de isopor
- Bateria de 9V
- Micro servo motor 9g Sg90
- Sensor ultrassonico hc – sr04
- Arduino Uno r3

Código fonte
#include &lt;Servo.h&gt; //servo library
Servo servo;
int trigPin = 5;
int echoPin = 6;
int servoPin = 7;
int led= 10;
long duration, dist, average;
long aver[3]; //array for average
void setup() {
Serial.begin(9600);
servo.attach(servoPin);
pinMode(trigPin, OUTPUT);
pinMode(echoPin, INPUT);
servo.write(0); //close cap on power on
delay(100);
servo.detach();
}
void measure() {
digitalWrite(10,HIGH);
digitalWrite(trigPin, LOW);
delayMicroseconds(5);
digitalWrite(trigPin, HIGH);
delayMicroseconds(15);
digitalWrite(trigPin, LOW);
pinMode(echoPin, INPUT);
duration = pulseIn(echoPin, HIGH);
dist = (duration/2) / 29.1; //obtain distance
}
void loop() {
for (int i=0;i&lt;=2;i++) { //average distance
measure();
aver[i]=dist;
delay(10); //delay between measurements
}
dist=(aver[0]+aver[1]+aver[2])/3;
if ( dist&lt;50 ) {
//Change distance as per your need
servo.attach(servoPin);
delay(1);
servo.write(0);
delay(3000);
servo.write(150);
delay(1000);
servo.detach();
}
Serial.print(dist);
}
