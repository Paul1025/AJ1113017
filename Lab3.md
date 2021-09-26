## Lab 3-1: Ultrasonic Sensor (3-pin) + 測距 (以公分顯示即可) + RS232 Output
### 電路1
![5-1-1](https://user-images.githubusercontent.com/89329182/134792472-0bd4f4b9-636c-4757-931d-e31593c0e1a2.jpg)
### 電路2
![5-1-2](https://user-images.githubusercontent.com/89329182/134792473-33ff4389-6fac-4d2b-83c2-b410f72a67d3.jpg)
### 程式碼
````c
int inches = 0;

int cm = 0;

long readUltrasonicDistance(int triggerPin, int echoPin)
{
  pinMode(triggerPin, OUTPUT);  // Clear the trigger
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  // Sets the trigger pin to HIGH state for 10 microseconds
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
  // Reads the echo pin, and returns the sound wave travel time in microseconds
  return pulseIn(echoPin, HIGH);
}

void setup()
{
  Serial.begin(9600);

}

void loop()
{
  // measure the ping time in cm
  cm = 0.01723 * readUltrasonicDistance(7, 7);
  // convert to inches by dividing by 2.54
  inches = (cm / 2.54);
  Serial.print(inches);
  Serial.print("in, ");
  Serial.print(cm);
  Serial.println("cm");
  delay(100); // Wait for 100 millisecond(s)
}
````
## Lab 3-2: 超音波感測器 + LED (紅色LED:亮<70cm, 緑色LED: 亮<270cm, 藍色LED:亮, 介於70cm ~ 270cm之間) + RS232 Output
### 電路1
![3-2-1](https://user-images.githubusercontent.com/89329182/134792772-946f128a-9da1-4536-b052-e3356935b6d0.png)
### 電路2
![3-2-2](https://user-images.githubusercontent.com/89329182/134792773-ba0b763e-ff7e-48d8-a31e-e2dd52bc6cd3.png)
### 程式碼
````c
int inches = 0;
int GLED = 8;
int RLED = 12;
int BLED = 10;
int cm = 0;

void LED(int RH, int GH, int BH)
{
  digitalWrite(RLED, RH);  
  digitalWrite(GLED, GH);
  digitalWrite(BLED, BH);   
}

long readUltrasonicDistance(int triggerPin, int echoPin)
{
  pinMode(triggerPin, OUTPUT);  // Clear the trigger
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  // Sets the trigger pin to HIGH state for 10 microseconds
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
  // Reads the echo pin, and returns the sound wave travel time in microseconds
  return pulseIn(echoPin, HIGH);
}

void setup()
{
  Serial.begin(9600);
  digitalWrite(GLED, OUTPUT);
  digitalWrite(RLED, OUTPUT);  
  digitalWrite(BLED, OUTPUT);    
  
}

void loop()
{
  // measure the ping time in cm
  cm = 0.01723 * readUltrasonicDistance(7, 7);
  // convert to inches by dividing by 2.54
  inches = (cm / 2.54);
  Serial.print(inches);
  Serial.print("in, ");
  Serial.print(cm);
  
  if(cm<70){
    LED(1, 0, 0); //int RH, int GH, int BH    
  }
  else if(cm>270){
    LED(0, 0, 1); //int RH, int GH, int BH      
  }
  else{
    LED(0, 1, 0); //int RH, int GH, int BH      
  }
    
  Serial.println("cm");
  delay(100); // Wait for 100 millisecond(s)
   
}
````
