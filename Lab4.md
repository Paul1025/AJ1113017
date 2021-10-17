# 嵌入式系統 - 實作4: 七段顯示器, LCD 顯示器 + 超音波感測器 (W7, W8) 
## Lab 4-1 用七段顯示器來顯示數字"8."
### 電路:
![401](https://user-images.githubusercontent.com/89329182/135739543-23cce2e4-6bc3-4160-84c7-d8036bffff8b.jpg)
### 程式:
````c
void setup()
{
for(int x = 1; x < 9; x++) 
  {
    pinMode(x,OUTPUT);
  }
}

void seg71(int a, int b, int c, int d, int e, int f, int g, int h)
{
  digitalWrite(1, a);
  digitalWrite(2, b);
  digitalWrite(3, c);
  digitalWrite(4, d);
  digitalWrite(5, e);
  digitalWrite(6, f);
  digitalWrite(7, g);
  digitalWrite(8, h);
  delay(500);
}

void loop()
{
  //    a, b, c, d, e, f, g, h
  seg71(0, 0, 0, 0, 0, 0, 0, 0); // OFF
  seg71(1, 1, 1, 1, 1, 1, 1, 1); // 8
}
````
## Lab 4-2 如下圖的Demo, 用七段顯示器, 顯示 . →1→ ... → 9 → 0 → 全滅, 狀態改變的間隔時間為0.5秒
### 電路:
https://user-images.githubusercontent.com/89329182/137609280-1b12d1ea-66c8-42d0-94f6-8d851e13dd4a.mp4
### 程式:
````c
void setup()
{
  for(int x = 1; x < 9; x++)
  {
  	pinMode(x,OUTPUT);
  }
}

void seg71(int a, int b, int c, int d, int e, int f, int g, int h)
{
  digitalWrite(1, a);
  digitalWrite(2, b);
  digitalWrite(3, c);
  digitalWrite(4, d);
  digitalWrite(5, e);
  digitalWrite(6, f);
  digitalWrite(7, g);
  digitalWrite(8, h);
  delay(500);
}

void loop()
{
  //    a, b, c, d, e, f, g, h
  seg71(0, 0, 0, 0, 0, 0, 0, 0); // OFF
  seg71(1, 1, 1, 1, 1, 1, 0, 1); // 0
  seg71(0, 1, 1, 0, 0, 0, 0, 1); // 1
  seg71(1, 1, 0, 1, 1, 0, 1, 1); // 2
  seg71(1, 1, 1, 1, 0, 0, 1, 1); // 3
  seg71(0, 1, 1, 0, 0, 1, 1, 1); // 4
  seg71(1, 0, 1, 1, 0, 1, 1, 1); // 5
  seg71(1, 0, 1, 1, 1, 1, 1, 1); // 6
  seg71(1, 1, 1, 0, 0, 0, 0, 1); // 7
  seg71(1, 1, 1, 1, 1, 1, 1, 1); // 8
  seg71(1, 1, 1, 1, 0, 1, 1, 1); // 9
}
````
## Lab 4-3 LCD顯示"Hello" + 你的英文名字 (e.g., "Hello Paul")
### 電路:
![4-3](https://user-images.githubusercontent.com/89329182/137610006-6983a0a8-18ca-4fce-a9ce-c36e96f0f94f.jpg)
### 程式:
````c
// include the library code:
#include <LiquidCrystal.h>

// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  lcd.print("hello, Paul!");
}

void loop() {
  // set the cursor to column 0, line 1
  // (note: line 1 is the second row, since counting begins with 0):
  lcd.setCursor(0, 1);
  // print the number of seconds since reset:
  lcd.print("2021/10/17");
}
````
