#include<Servo.h>
Servo srv;
//#define maxdistance 1
#include <LiquidCrystal.h>
LiquidCrystal lcd(12, 11, 10, 5, 4, 3, 2);
//const int trigPin1 = 6;
//const int echoPin1= A0;
const int trigPin2 = 8;
const int echoPin2 = A1;
long duration;
int distance;
int backLight = 13;
int sensor=6;
int sensor_value;


void setup()
{
  pinMode(backLight, OUTPUT);
  digitalWrite(backLight, HIGH);
  lcd.begin(16,2);              
  lcd.clear();                  
  pinMode(sensor,INPUT);  
 
  Serial.begin(9600);
  pinMode(6, INPUT);
 // pinMode(A0, INPUT);
  pinMode(8, OUTPUT);
  pinMode(A1, INPUT);
  srv.attach(9);
 
}

void loop()
{
//  digitalWrite(trigPin1, LOW);
//delayMicroseconds(2);
//digitalWrite(trigPin1, HIGH);
//delayMicroseconds(2);
digitalWrite(trigPin2, LOW);
delayMicroseconds(2);
digitalWrite(trigPin2, HIGH);
delayMicroseconds(2);
//duration = pulseIn(echoPin1, HIGH);
//distance= duration*0.034/2;
  //digitalWrite(8, LOW);
  int d=pulseIn(A1,HIGH);
  d=d/29/2;
  lcd.setCursor(0,0);          
  lcd.print("Garbage level: ");
  sensor_value=digitalRead(sensor);
Serial.println(sensor_value);

  if(sensor_value == 1)
  {
    srv.write(90);
   
  }
  else if(sensor_value == 0)
  {
   
    srv.write(0);
  }
  if(d < 25 )
  {
    lcd.setCursor(0,1);
    lcd.print("25 % filled");

   
  }
  else if(d < 50)
  {
   
    lcd.setCursor(0,1);
    lcd.print("50 % filled");

  }  
  else if(d < 75)
  {
    lcd.setCursor(0,1);
    lcd.print("75 % filled");
   
  }
  else if(d = 100)
    {
    lcd.setCursor(0,1);
    lcd.print("Fully filled");
  }
  }
