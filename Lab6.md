# 嵌入式系統 - 實作6: 4X4鍵盤 + LCD 顯示器 + 回顧 + AI-based嵌入式系統? (W11)
## Lab 6-1 用16X2 LCD 顯示器來顯示4X4鍵盤輸入的數字 (0, 1, 2, .., 9), 若輸入的字數≥16則換到下一列, 若兩皆滿, 則清除劃面重新由Row=0, Col=0開始.
### 電路:
![01](https://user-images.githubusercontent.com/89329182/139566989-f554b502-fc2c-42d7-9dd2-104dd9f0ca3b.png)
### 程式:
````c
// For Embedded System course, VNU, Fall 2021 

#include <Keypad.h>
#include <LiquidCrystal.h>
// 5:RS, 4:E, 3:DB4, 2:DB5, A4:DB6, A5: DB7
// **LCD若只顯示文字，只須使用4-bit模式即可** (LCD腳位DB0, DB1, DB2, DB3就不用接了。)
LiquidCrystal lcd(5, 4, 3, 2, A4, A5);

const byte ROWS = 4; // 4列數(橫的)
const byte COLS = 4; // 4行數(直的)
char keys[ROWS][COLS] = 
 {
  {'1','2','3','A'},
  {'4','5','6','B'},
  {'7','8','9','C'},
  {'*','0','#','D'}
 };

byte rowPins[ROWS] = {A0, A1, 11, 10}; //定義列的腳位
byte colPins[COLS] = {9, 8, 7, 6}; //定義行的腳位

int LCDCol = 0;
int LCDRow = 0;

Keypad keypad = Keypad( makeKeymap(keys), rowPins, colPins, ROWS, COLS );

void setup()
  {
   Serial.begin(9600);
   lcd.begin(16, 2);
   lcd.setCursor(LCDCol, LCDRow);
  }
  
void loop()
 {
  char key = keypad.getKey(); //讀取 Keypad 的輸入
  if (key){
    
    Serial.println(key);
           
    
    if ( LCDCol > 15  )
    {   
     ++LCDRow; // Move to the 2nd row
      
      if (LCDRow>1)
      { LCDRow=0; LCDCol = 0 ;  lcd.clear(); } // clear and move back the 1st row
   
    LCDCol = 0 ;
    }
         
    lcd.setCursor (LCDCol, LCDRow); 
    
       lcd.print(key);
    
    ++LCDCol;
    
  } // end if
 } // end loop

````
## Lab 6-2 分享一個你最喜歡的實作 (電路即可)到你的GitHub，測速照相
### 電路:
![002](https://user-images.githubusercontent.com/89329182/139567115-59690e01-2820-4e5b-beb5-a5d5f0321c30.jpg)
### 程式:
````c
int ledY=13;                                            //整數 LED黃燈為13腳位
int ledG=11;                                            //整數 LED綠燈為11腳位
int ledR=9;                                             //整數 LED紅燈為9腳位
int camera=7;                                           //整數 照相機為7腳位
void setup()                                   
{
  pinMode(ledY, OUTPUT);                                //LED黃燈13輸出腳位
  pinMode(ledG, OUTPUT);                                //LED綠燈11輸出腳位
  pinMode(ledR, OUTPUT);                                //LED紅燈9輸出腳位
  pinMode(camera, OUTPUT);                              //照相機7輸出腳位
  Serial.begin(115200);                                 //讓板子與電腦同步
}
void loop()
{ 
  if(Serial.available())                                //如果 串列監視器傳送訊息
     { 
      float num = Serial.parseFloat();                  //宣告num為浮點數(串列監視器輸入)
      char unit = Serial.read();                        //宣告unit為字元(串列監視器輸入)
      
     
      if ((unit=='K')||(unit=='k'))                     //如果 讀到字元為K或k(公里)
       { 
        Serial.print("The speed is:");                  //串列監視器輸出"The speed is:"
        Serial.print(num);                              //串列監視器輸出"輸入的數字"
        Serial.print("kph = ");                         //串列監視器輸出"kph = "
        Serial.print(num*0.62);                         //串列監視器輸出"輸入的數字*0.62"(公里換英里)
        Serial.println("mph  LEDy ON 1s");              //串列監視器輸出並換行"mph 黃燈亮1秒"
        digitalWrite(ledY, HIGH);                       //黃燈亮
        delay(1000);                                    //持續1秒
        digitalWrite(ledY, LOW);                        //黃燈滅
        delay(1000);                                    //持續1秒
        if (num<70)                                     //如果輸入的數字<70(公里/小時<70)
        {
          Serial.println("Slow!camera ON!LEDw ON!");    //串列監視器輸出"慢!照相機開!白燈亮"
          digitalWrite(camera, HIGH);                   //照相機開啟(含LED白燈)
        }
        else if((num>=70)&&(num<=100))                  //不然 如果(輸入的數字70-100(70-100公里))
        {
          Serial.println("Safety!camera OFF!LEDw OFF!");//串列監視器輸出"安全!照相機關!白燈滅"
          digitalWrite(camera, LOW);                    //照相機關閉(含LED白燈)
        }
        else                                            //不然(輸入的數字>100(高過100公里))
        {
          Serial.println("Speeding!camera ON!LEDw ON!");//串列監視器輸出"超速!照相機開!白燈亮"
          digitalWrite(camera, HIGH);                   //照相機開啟(含LED白燈)
        } 
       }
      else if ((unit=='M')||(unit=='m'))                //不然 如果 讀到字元為M或m
       {
        Serial.print("The speed is:");                  //串列監視器輸出"The speed is:"
        Serial.print(num);                              //串列監視器輸出"輸入的數字"
        Serial.print("mph = ");                         //串列監視器輸出"mph = "
        Serial.print(num/0.62);                         //串列監視器輸出"輸入的數字/0.62"(英里換公里)
        Serial.println("kph  LEDg ON 1s");              //串列監視器輸出並換行"kph  綠燈亮1秒"
        digitalWrite(ledG, HIGH);                       //綠燈亮
        delay(1000);                                    //持續1秒
        digitalWrite(ledG, LOW);                        //綠燈滅
        delay(1000);                                    //持續1秒
        if (num<43.4)                                   //如果輸入的數字<43.4(英里/小時<43.4)
        {
          Serial.println("Slow!camera ON!LEDw ON!");    //串列監視器輸出"慢!照相機開!白燈亮"
          digitalWrite(camera, HIGH);                   //照相機開啟(含LED白燈)
        }
        else if((num>=43.4)&&(num<=62))                 //不然 如果(輸入的數字43.4-62(43.4-62英里))
        {
          Serial.println("Safety!camera OFF!LEDw OFF!");//串列監視器輸出"安全!照相機關!白燈滅"
          digitalWrite(camera, LOW);                    //照相機關閉(含LED白燈)
        }
        else                                            //不然(輸入的數字>62(高過62英里))
        {
          Serial.println("Speeding!camera ON!LEDw ON!");//串列監視器輸出"超速!照相機開!白燈亮"
          digitalWrite(camera, HIGH);                   //照相機開啟(含LED白燈)
        } 
       }
      else                                              //不然
       { 
        Serial.println("error!LEDr ON 1S");             //串列監視器輸出"錯誤!紅燈亮1秒"
        digitalWrite(ledR, HIGH);                       //紅燈亮(含蜂鳴器及震動)
        delay(1000);                                    //持續1秒
        digitalWrite(ledR, LOW);                        //紅燈滅(含蜂鳴器及震動)
        delay(1000);                                    //持續1秒
       }
    }
}
````
