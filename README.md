#include <Wire.h> 
#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0x27,2,1,0,4,5,6,7,3,POSITIVE);

int sensor1,sensor2,sensor3;
int value1,value2,value3;
unsigned long vaqt=0;
void setup() {
lcd.clear();
Serial.begin(9600); 
lcd.begin(16,2);
pinMode(2,OUTPUT);
pinMode(3,OUTPUT);

}

void loop() {
  value1=analogRead(A0);
  value2=analogRead(A1);
  value3=analogRead(A2);

sensor1=map(value1,0,1023,-50,100);
sensor2=map(value2,0,1023,-50,100);
sensor3=map(value3,0,1023,-50,100);

Serial.print("sensor1 :");
Serial.print(sensor1);
Serial.print("  sensor2 :");
Serial.print(sensor2);
Serial.print("  sensor3 :");
Serial.println(sensor3);
Display();

if(sensor1 >=30 || sensor2 >= 30)
{
  digitalWrite(2,HIGH);
  Nasos();
  }
else
{
  //Display();
  digitalWrite(2,LOW);
  }

  if(sensor3 >=35)
  {
    digitalWrite(3,HIGH);
    Cooler();
    }
    else
    {
      digitalWrite(3,LOW);
      }

}

void Display()
{
  
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("Bir:");
  lcd.setCursor(0,1);
  lcd.print(sensor1);

  lcd.setCursor(6,0);
  lcd.print("Ikki:");
  lcd.setCursor(6,2);
  lcd.print(sensor2);
  
  lcd.setCursor(12,0);
  lcd.print("Uch:");
  lcd.setCursor(12,2);
  lcd.print(sensor3);
  }

  void Cooler()
  {
     
  lcd.clear();
  lcd.setCursor(2,0);
  lcd.print(" Cooler ishladi:");
  lcd.setCursor(8,1);
  lcd.print(sensor3);
  
    delay(500);
    }

  void Nasos()
  {
     
  lcd.clear();
  lcd.setCursor(2,0);
  lcd.print(" Nasos ishladi:");
  lcd.setCursor(4,1);
  lcd.print(sensor1);
  lcd.setCursor(12,1);
  lcd.print(sensor2);
  
    delay(500);
    }
