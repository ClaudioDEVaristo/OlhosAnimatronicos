# OlhosAnimatronicos

// INCLUSÃO DE BIBLIOTECAS
#include <Wire.h>
#include <Adafruit_PWMServoDriver.h>

// INSTANCIANDO OBJETOS
Adafruit_PWMServoDriver pwm = Adafruit_PWMServoDriver();

// DECLARAÇÃO DE FUNÇÕES
void writeServos(int posicao, int tempo);
void beginServos();
void olhaParaLados();
void neutro();
void pisca();

void setup() {
  beginServos(); // INCIA OS SERVOS
  delay(300);
}

void loop() {
      
      writeServos(2, 21);
      writeServos(3, 55);   
      writeServos(4, 40);
      writeServos(5, 40);

      writeServos(2, 11);
      writeServos(4, 50);
      writeServos(1, 180);
      writeServos(0, 160);
      delay(1000);
      writeServos(2, 21);
      writeServos(4, 40);      
      writeServos(1, 160);
      writeServos(0, 80);
      delay(1000);

      neutro();
      pisca();
}

// IMPLEMENTO DE FUNÇÕES
void writeServos(int nServo, int posicao) {
#define SERVOMIN  205 // VALOR PARA UM PULSO MAIOR QUE 1 mS
#define SERVOMAX  409 // VALOR PARA UM PULSO MENOR QUE 2 mS

  int pos = map ( posicao , 0 , 180 , SERVOMIN, SERVOMAX);
  pwm.setPWM(nServo , 0, pos);
}

void beginServos() {

#define Frequencia 50 // VALOR DA FREQUENCIA DO SERVO 

  pwm.begin(); // INICIA O OBJETO PWM
  pwm.setPWMFreq(Frequencia); // DEFINE A FREQUENCIA DE TRABALHO DO SERVO
}

void olhaParaLados(){
  writeServos(0, 160);
  delay(1000);
  writeServos(0, 80);
  delay(1000);
}

void neutro(){
  writeServos(1, 160);
  writeServos(2, 21);
  writeServos(3, 55);   
  writeServos(4, 40);
  writeServos(5, 40);
  writeServos(0, 120);
  delay(2000);
}

void pisca(){

  writeServos(2, 75);
  writeServos(3, 0);
  writeServos(4, 0);
  writeServos(5, 110);
  delay(150);

  writeServos(2, 21);
  writeServos(3, 55);   
  writeServos(4, 40);
  writeServos(5, 40);
  delay(1000);  
}
