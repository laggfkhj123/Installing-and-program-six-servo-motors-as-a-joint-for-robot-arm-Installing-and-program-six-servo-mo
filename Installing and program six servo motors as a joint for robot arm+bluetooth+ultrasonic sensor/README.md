Installing and program six servo motors as a joint for robot arm+bluetooth+ultrasonic sensor
this is the second part of the project, it is the same first, but we added Bluetooth + ultrasonic sensor
if someone stops 3 second front of the ultrasonic sensor will play video, I used LED as a video simulator

Bluetooth module will send a signal for playing the video

#include <SoftwareSerial.h>
#include <Servo.h>
  SoftwareSerial BT(A0,A1);
  long duration;
  long distance;
  Servo servo1;
  Servo servo2;
  Servo servo3;
  Servo servo4;
  Servo servo5;
  Servo servo6;
  int state=0;


  
void setup() {
  Serial.begin(9600);
  Serial.begin(38400);
  BT.begin(38400);
  pinMode(A5,OUTPUT);
  pinMode(A4,INPUT);
  pinMode(13,OUTPUT);
  servo1.attach(11);
  servo2.attach(10);
  servo3.attach(9);
  servo4.attach(6);
  servo5.attach(5);
  servo6.attach(3);

}

void loop() {
 int servo1_1=0, servo1_2=0, servo1_3=0, servo2_1=0, servo2_2=0, servo2_3=0; //start point (Here where the mechanical engineer will set a appropriate degree(0-180)
 servo1.write(servo1_1);   
 servo2.write(servo1_2);
 servo3.write(servo1_3);
 servo4.write(servo2_1);
 servo5.write(servo2_2);
 servo6.write(servo2_3);
 //delay(500);


 servo1_1=120; servo1_2=135; servo1_3=90; servo2_1=120; servo2_2=135; servo2_3=90; // Here where the mechanical engineer will set a appropriate degree for robot motion(0-180)
 servo1.write(servo1_1);   
 servo2.write(servo1_2);
 servo3.write(servo1_3);
 servo4.write(servo2_1);
 servo5.write(servo2_2);
 servo6.write(servo2_3);
//delay (100);



 {
  digitalWrite(A5,LOW);  //ultra sonic code
  delayMicroseconds(2);
  digitalWrite(A5,HIGH);
  delayMicroseconds(10);
  digitalWrite(A5,LOW);
  duration= pulseIn(A4,HIGH);
  distance=duration*0.034/2;



  while(distance==25){      //signal for led (represin vedio that wiil show)
    delay(3000);
    digitalWrite(13,HIGH);
    delay(3000);

{
    if(Serial.available() > 0){ 
    state = Serial.read();
    if (distance == 25) {
   Serial.write('1'); 
 }
 else {
   Serial.write('0');}
}

}
  duration= pulseIn(A4,HIGH);
    distance=duration*0.034/2;  
  }
  digitalWrite(13,LOW);
  delay(200);
  }




}
