# 嵌入式系統 - 實作2: 會呼吸的RGB LED, 按鍵控制, 狀態輸出
## 實作2-1, analogWrite(): 並且觀查LED亮度變化是否有像"呼吸的效果"和示波器的波形有什麼關連性? (互動1), (2021-09-05)
![01](https://user-images.githubusercontent.com/89329182/132114615-b373f731-a875-4b82-8832-bc6515f1c17b.jpg)
### 程式碼
````c
void setup()
{
  pinMode(13, OUTPUT);
}

void loop()
{
  digitalWrite(13, HIGH);
  delay(500); // Wait for 1000 millisecond(s)
  digitalWrite(13, LOW);
  delay(500); // Wait for 1000 millisecond(s)
}
````
## 實作2-2, RGB LED燈全彩模組, 分別讓LED輪流表現正紅、正綠、正藍，三個顏色，時間間隔1秒鐘。並且觀查LED顏色和波形或是電壓有什麼關連性? 可將個人說明在更新GitHub時一起加入. (互動2), (2021-09-05)
![02](https://user-images.githubusercontent.com/89329182/132115101-37e80dca-b328-415b-9f3f-71af4800dd7c.jpg)
### 程式碼
````c
int R = 9;
int G = 10;
int B = 11;

{
  pinMode(R, OUTPUT);
  pinMode(G, OUTPUT);
  pinMode(B, OUTPUT);  
}

void loop()
{
	analogWrite(R, 255);
	analogWrite(G, 0);
	analogWrite(B, 0);
  	delay(1000);
	analogWrite(R, 0);
	analogWrite(G, 255);
	analogWrite(B, 0);
  	delay(1000);
	analogWrite(R, 0);
	analogWrite(G, 0);
	analogWrite(B, 255);
  	delay(1000);  
}
````
## 實作2-3, 讓你的RGB LED燈全彩模組也可會"呼吸", LED顏色變化是否有像"呼吸的效果"和示波器的波形有什麼關連性? (互動3), (2021-09-12)
![3](https://user-images.githubusercontent.com/89329182/132970543-a9fc7444-e71d-4b49-a331-21c55dda596b.png)
### 程式碼
````c
int brightness = 0;

void setup()
{
  pinMode(9, OUTPUT);
}

void loop()
{
  for (brightness = 0; brightness <= 255; brightness += 5) 
  {
    analogWrite(9, brightness);
    delay(50); // Wait for 30 millisecond(s)
  }

  for (brightness = 255; brightness >= 0; brightness -= 5) 
  {
    analogWrite(9, brightness);
    delay(50); // Wait for 30 millisecond(s)
  }
  delay(2000);
}
````
## 參考電路與程式: digitWrite(), analogWrite(), 呼吸效果
![3-1](https://user-images.githubusercontent.com/89329182/132970648-b418fa4f-cc25-4a33-8dd7-b3dd99f63e71.png)
### 程式碼
````c
int R = 9;
int G = 10;
int B = 11;

int DR = 2;
int DG = 4;
int DB = 7;

void setup()
{
  pinMode(13, OUTPUT); // pin 13
  
  pinMode(R, OUTPUT);
  pinMode(G, OUTPUT);
  pinMode(B, OUTPUT);  
  
  pinMode(DR, OUTPUT);
  pinMode(DG, OUTPUT);
  pinMode(DB, OUTPUT);   
}

void loop()
{
  // digitalWrite: 2 state (i.e., 0, 1) Only
  digitalWrite(13, 1); // LED @ pin 13, ON
  
  delay(1000); 
  
  digitalWrite(DR, 1);
  digitalWrite(DG, 0);
  digitalWrite(DB, 0);
  delay(1000);
  digitalWrite(DR, 0);
  digitalWrite(DG, 1);
  digitalWrite(DB, 0);  
  delay(1000);
  digitalWrite(DR, 0);
  digitalWrite(DG, 0);
  digitalWrite(DB, 1);  
  delay(1000);

  digitalWrite(13, 0); // OFF
  digitalWrite(DR, 0); // OFF
  digitalWrite(DG, 0); // OFF
  digitalWrite(DB, 0); // OFF  
  delay(1000);
  
  // analogWrite: The brightness can be adjusted with 256 levels
  for (int i = 0; i<= 255; i++)
  {
   analogWrite(R, i);
   analogWrite(G, 0);
   analogWrite(B, 0);
   delay(10);
  } // from dark to bright 

  for (int i = 255; i>= 0; i--)
  {
   analogWrite(R, i);
   analogWrite(G, 0);
   analogWrite(B, 0);
   delay(10); // 10ms = 0.01s
  }  // from bright to dark
  delay(1000);
}
````
## 實作2-4 analogRead(), 1024解析度 (i.e.,10-bit):
### 可變電阻 + 序列監視器與輸出
> 當你改變可變電阻的阻值(e.g., 10K-ohm)時，序列監視器輸出的數值有什麼改變? 數值又有什麼意義呢? 可試將你的想法寫在你的GitHub Page中喔! (互動4) (2021-09-12)
### 電路
![2-4](https://user-images.githubusercontent.com/89329182/132971285-5946009f-2751-482b-89a2-271d670b4c1f.png)
### 程式碼
````c
int sensorValue = 0;

void setup()
{
  pinMode(A0, INPUT);
  Serial.begin(9600);

}

void loop()
{
  // read the input on analog pin 0:
  sensorValue = analogRead(A0);
  // print out the value you read:
  Serial.println(sensorValue);
  delay(10); // Delay a little bit to improve simulation performance
}
````
### digitalRead(): 按鍵 + 序列監視器與輸出說明與介紹
### 電路
![2-4-1](https://user-images.githubusercontent.com/89329182/132971566-5d2eee39-1f2b-4774-a2ad-7bd9de6bea17.png)
### 程式碼
````c
int buttonState = 0;

void setup()
{
  pinMode(2, INPUT);
  Serial.begin(9600);

}

void loop()
{
  // read the input pin
  buttonState = digitalRead(2);
  // print out the state of the button
  Serial.println(buttonState);
  delay(10); // Delay a little bit to improve simulation performance
}
````

## B5 實作2-5: 按下按鍵, Green LED亮 & Red LED滅; 放開按鍵, Green LED滅 & Red LED亮. 想要再深入的同學可以試試喔. (思考方向: digitalRead(), digitalWrite(): 按鍵 +序列輸出 + LED), (互動5) (2021-09-19) 
### 可變電阻 + 序列監視器與輸出
> 當你改變可變電阻的阻值(e.g., 10K-ohm)時，序列監視器輸出的數值有什麼改變? 數值又有什麼意義呢? 可試將你的想法寫在你的GitHub Page中喔! (互動4) (2021-09-12)
### 電路
![2-4](https://user-images.githubusercontent.com/89329182/134792125-83f09942-6cc7-48ce-888b-a543b8231983.jpg)
![22](https://user-images.githubusercontent.com/89329182/134792191-1983c7f9-110b-4b0a-a0bb-1eb999cf9c07.png)
### 程式碼
````c
int buttonState = 0;
int GLED = 13;
int RLED = 8;

void setup()
{
  pinMode(2, INPUT);
  pinMode(GLED, OUTPUT); // GREEN
  pinMode(RLED, OUTPUT); // RED    
}

void loop()
{
  // read the state of the pushbutton value
  buttonState = digitalRead(2);
  // check if pushbutton is pressed.  if it is, the
  // buttonState is HIGH
  if (buttonState == HIGH) {
    // turn LED on  
    digitalWrite(GLED, HIGH);
    digitalWrite(RLED, LOW);    
  } else {
    // turn LED off    
    digitalWrite(GLED, LOW);
    digitalWrite(RLED, HIGH);
  }
  delay(10); // Delay a little bit to improve simulation performance
}
````
