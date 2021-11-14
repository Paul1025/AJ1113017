# 嵌入式系統 - 實作8: 零基礎Python快速入門與實作 (W13, W14)
## 暖身: 請同學先參考Lab8-3的程式, 並將老虎的圖像在Colab中Show出來. (建議的File Name: ShowPhoto.ipynb)
![001](https://user-images.githubusercontent.com/89329182/141666276-f6bbbc55-3928-4215-9605-586bcc23744d.jpg)
## Lab 8-1 零基礎Python快速入門與實作, 1/2, W13
### -*- coding: utf-8 -*-
"""
#使用Google Colab的Python零基礎快速入門教程
Prepared by Horace, Date: October, 2021
* Colaboratory (簡稱為「Colab」) 可讓你在瀏覽器上撰寫及執行 Python. 
* Colab 筆記本的互動式環境，可讓你撰寫和執行程式碼
### 介紹
> Python 本身就是一種出色的通用編程語言，但在一些流行庫（例如: numpy、matplotlib）的幫助下，它成為了一個強大的科學計算環境。我們希望本節將作為Python 編程語言和人工智慧學習中的使用速成課程。
### 在本教程中，我們將介紹：
* Python必學: Basic data types (Containers, Lists, Dictionaries, Sets, Tuples), loops, flow control, Functions, Classes
* 作圖模組 (Matplotlib): Plotting, Subplots, Images
"""


### P1101
ts3 = 'Liang Paul' # Please input your English name
!python --version #  Python 版本確認

"""### 模組(Module)??
> 模組(Module)就是一個檔案，包含了相關性較高的程式碼。隨著應用程式的開發規模越來越大，我們不可能把所有的程式碼都寫在同一份Python檔案中，一定會將關聯性較高的程式碼抽出來放在不同的檔案中來形成模組(Module)，主程式再透過引用的方式來使用。所以模組(Module)可以提高程式碼的重用性(Reusable)且易於維護。
"""

### P1102 載入Python calendar模組, 輸出月曆
import calendar
print(calendar.calendar(2021))

### 實作1101, 印出明年的年曆(2022) 

print(calendar.calendar(2022))

### P1103
from math import pi
print(pi)
print('pi= ', pi)
print('pi= %.6f' % pi)
print('pi= %.3f' % pi)
print('pi= %.2f' % pi)
print('pi= %d' % pi)

### P1104
print('學AI真是太酷了!!') #print顯示的內容必須是字串或是變數

"""###Basics of Python
> Python 是一種高級的、動態類型的多範式編程語言。 Python 代碼通常被認為幾乎像偽代碼，因為它允許您用很少的代碼行表達非常強大的想法，同時又非常易讀。
###常用運算符號
+（加）、-（減）、*（乘）、/（除）、%（取餘數）
####Numbers
"""

### P1105
x = 3
print(x, x+x, x*x)

### P1106
print(x + 1)   # 加法,Addition
print(x - 1)   # 減法,Subtraction
print(x * 2)   # 乘法,Multiplication
print(x ** 2)  # 指數,Exponentiation (3*3=9)

### P1107
print(x % 2)   # 取餘數, 3%2=1, 5%3=2
print(x/2)     # 除法
print(x//2)     # 整數除法
print(x//4)

### 實作1110
x = 2
y = x + 5
z = x * y
a = x - 3
b = 2**10
print(x, y, z, a, b)
print('x=%d, y=%d, z=%d, a=%d, b=%d' % (x, y, z, a, b))

### P1108
x = 2
x += 1 # x = x + 1
print(x)
x *= 2 # x = x * 2 (i.e., x = 3*2 = 6)
print(x)

### 實作1120
x = 2
x = x + 1 

print('x=x+1, x=?', x)

### 實作1121

x = 2
x += 1 # x = x + 1
print('x += 1, x=?', x)
x *= 2 # x = x * 2 (i.e., x = 3*2 = 6)
print('x *= 2, x=?', x)

"""### python 的內建型態主要分為以下三種：
1. 數值型態：整數 int, 浮點數 float, 布林 bool
2. 字串型態：字串 str, 字元 chr
3. 容器型態：串列 list[], 字典 dict{}, 序對 Tuple(), 集合 Set{}
[重要] python變數:區分大小寫、不可以數字開頭!!
"""

### P1110
y = 2.5
print(type(y)) # Show data type by "type()"
print(y, y + 1, y * 2, y ** 2) # Easy calculation

### 實作1130: check data type

x = 2
print('x=2, type=?', type(x))

y = 2.5
print('y=2.5 type=?', type(y))

z = 'hello'
print('z=hello, typ=?', type(z))

"""### 變數不能使用指令/關鍵字/數字開頭: Python的保留字有哪些? 直接問python吧!"""

### P1112A
import keyword
print(keyword.kwlist,end='')

### P1112B
and = 1
print(and)

### P1113 常用輸入輸出
id ="A1234567"
name = input("請輸入姓名") #可加註解
print("Hello ~ ",id+name)

"""### 重要: 縮進:迴圈類、函數、邏輯判斷等..使用 2 or 4 空格(tab)統一使用4
比較運算符號 包括 <、<=、>、>=、==、!=
"""

### P1114 if判斷很常用，條件成立才執行

x = 7
check = (x >= 5)
print('check ?,', check)
if check:
print(x,"> 5 \n") #迴圈內指令前方要縮進
print(x,'> 5, %s\n' % check) #迴圈內指令前方要縮進    

#雙向if 條件成立~執行，不成立~就執行另一個
if 0:  #在python世界裡 1不只是1，還具有 True、真、成立
    print(True)
else:
    print(False) #0不只是0，還具有 False、偽、不成立

### 實作1135, 請修正以上的Bug

x = 7
check = (x >= 5)
print('check ?,', check)
if check:
  print(x,"> 5 \n") #迴圈內指令前方要縮進
  print(x,'> 5, %s\n' % check) #迴圈內指令前方要縮進 (Tab)   

#雙向if 條件成立~執行，不成立~就執行另一個
if 0:  #在python世界裡 1不只是1，還具有 True、真、成立
    print(True)
else:
    print(False) #0不只是0，還具有 False、偽、不成立

### P1114a
a = 33
b = 200
if b > a:
  print("b is greater than a") # you will get an error

a = 33
b = 33
if b > a:
  print("b > a")
elif a == b:
  print("a == b")
else:
  print("a > b")

"""####布林邏輯
Python implements all of the usual operators for Boolean logic, but uses English words rather than symbols (`&&`, `||`, etc.):
"""

### P1115
print("***** 布林邏輯 *****")
one = 1
two = 2
three = 3

print('one > 0: ', one > 0)
print('two > one:',two > one)
print('three < one:', three < one)

### P1116
t = True
f = False
print(t and f) # Logical AND;
print(t or f)  # Logical OR;
print(not t)   # Logical NOT;
print(t != f)  # Logical XOR;

### 實作1140
ans1 = (two == three) # == = = + =
ans2 = (two != three)
ans3 = (two > three)
ans4 = (two < three)

print("ans1, ans2, ans3, ans4 =", ans1, ans2, ans3, ans4, '\n')
print("ans1, ans2, ans3, ans4 =", ans1, ans2, ans3, ans4)
print("ans1 = %s, ans2 = %s, ans3 = %s, ans4 = %s" % (ans1, ans2, ans3, ans4), '\n')

ans5 = ans2 and ans4
print('ans2 and ans4 = ans5:', ans2, ans4, ans5)

### P1117
f = 3
g = 3.0000 
if f=g: #判斷要使用==
    print("是的")
else:
    print("才不是哩")

### 實作1145: 讓我們一起來除錯吧! (SyntaxError: invalid syntax)
f = 3
g = 3.0000 
if f==g: #判斷要使用 == 
    print("是的")
else:
    print("才不是哩")

"""####字串(Strings)"""

### P1118
hello = '**hello** '   # String literals can use single quotes
world = "++world++"   # or double quotes; it does not matter
print(hello, len(hello))
print(world, len(world))

hh = 'hello world'
print('hello world', len(hh))

### P1119

hw = hello + world  # 字符串連接 (String concatenation)
print(hw)

hw = hello + ' ' + world  # 字符串連接 (String concatenation)
print(hw)

print('%s %s' % (hello, world))

### P1120
hw12 = '{} {} {}'.format(hello, world, 12)  # string formatting
print(hw12)

### 實作1150
wh = world + ' ' + hello
print(wh)

hw12 = '{} {} {}'.format(hello, world, 12)  # string formatting

print(hw12)

hw13 =('%s %s %d' %(hello, world, 12))  # string formatting

print(hw13)

"""String objects have a bunch of useful methods; for example:"""

### P1121
s1 = 'hello'
s2 = '  world '
print(s1.capitalize())  # 將字符串大寫
print(s1.upper())       # 將字符串全部轉換為大寫
print(s1.replace('l', '*'))  # 用另一個替換一個子字符串
print(len(s2), s2.strip(), len(s2.strip()))  # 去除前導和尾隨空格

### 實作1160
s11 = 'good morning'
s12 = '  WORLD aaa AAA'
s13 = 'good#####moring'
print(s11.capitalize())
print(s11.upper())
print(s12.replace("L",'***'))
print(s12.replace("RL",'-----'))
print(len(s12), s12.strip(), len(s12.strip())) 
print(s12.lower())
print(s13, s13.replace('#####',' '))

"""###容器：Python常用內置容器類型：列表(list)、字典(dictionary)
####Lists
列表(List)是數組的 Python 等價物，但可以調整大小並且可以包含不同類型的元素：
"""

### P1122
xs = [3, 2, 1]   # 創立一個List
print(xs)
print(xs[2])
print(xs[0])
print(xs[-1])     
print(xs[-2])
print(xs[-3])
print("Size = ? Ans: ", len(xs))

### 實作1171

ss = [10, 20, 30, 40, 50, 'hello', 'world']
print(ss)

print(ss[0])
print(ss[-1])
print(ss[1])
print(ss[4])

print('Size =?, Ans:', len(ss))

### for idx, animal in enumerate(animals):
for box_number, box_content in enumerate(ss):
  print(box_number, box_content)

### P1123
xs = [10, 20, 30, 40, 50] 
xs[2] = 'cat'    # 列表可以包含不同類型的元素
print(xs)

### 實作1172
xs[2]='dog'
print(xs)

### P1124
xs.append('fish') # 在列表末尾添加一個新元素
print(xs)  
print(len(xs))

### 實作1173

xs.append('bird') # 在列表末尾添加一個新元素
print(xs)  
print(len(xs))

### P1125
x = xs.pop()     # 刪除並返回列表的最後一個元素
print(x, xs)

### 實作1174
x = xs.pop()     # 刪除並返回列表的最後一個元素
print(x, xs)

"""####Slicing: Python 還提供了簡潔的語法來訪問子列表； 這稱為切片："""

### P1126
print(len('hello'))

### P1127
nums = 'hello'
print(nums, len(nums))         
print('nums[2:4] >>',nums[2:4])    
print('nums[2:] >>',nums[2:])     
print(nums[:2])     
print(nums[:])      
print('nums[:-1] >>', nums[:-1])    
print(nums)

### 實作1175
nums = 'world'
print(nums, len(nums))       
print(nums[2:4])    
print(nums[2:])     
print(nums[:2])     
print(nums[:])      
print('nums[:-1] >>', nums[:-1])    
print(nums)

### 實作1175a
x = [0, 1, 2, 3, 4, 5]
print(x)
print('x[:] >> ',x[:])

print(x[:3])

print('x[3:] >>', x[3:])

for i in range(1,10,2):
  print(i)

### Final Result
from datetime import datetime
today = datetime.now()
print('*** Done by %s at ' % ts3,today, type(today))

### 連結 https://colab.research.google.com/drive/1iXyyUEv1VuIMWPJaDbpfPZ-aIanJZ6dB?usp=sharing

## Lab 8-3 建立新的Colab Notebook (e.g., Filename: ShowPhoto.ipynb), 用Python來Show一下圖像, 完成後並更新到GitHub
```python
# 801
import tensorflow as tf
import tensorflow_hub as hub

import requests
from PIL import Image
from io import BytesIO

import matplotlib.pyplot as plt
import numpy as np

from datetime import datetime
now = datetime.now()
print("now =", now)
today = now
image_size = 224
dynamic_size = False
max_dynamic_size = 512

ts3 = 'TA Grace' # Please input your English name

# 802
original_image_cache = {}

def preprocess_image(image):
  image = np.array(image)
  # reshape into shape [batch_size, height, width, num_channels]
  img_reshaped = tf.reshape(image, [1, image.shape[0], image.shape[1], image.shape[2]])
  # Use `convert_image_dtype` to convert to floats in the [0,1] range.
  image = tf.image.convert_image_dtype(img_reshaped, tf.float32)
  return image

def load_image_from_url(url):
  """Returns an image with shape [1, height, width, num_channels]."""
  user_agent = {'User-agent': 'Colab Sample (https://tensorflow.org)'}
  response = requests.get(img_url, headers=user_agent)
  image = Image.open(BytesIO(response.content))
  image = preprocess_image(image)
  return image

def load_image(image_url, image_size=256, dynamic_size=False, max_dynamic_size=512):
  """Loads and preprocesses images."""
  # Cache image file locally.
  if image_url in original_image_cache:
    img = original_image_cache[image_url]
  elif image_url.startswith('https://'):
    img = load_image_from_url(image_url)
  else:
    fd = tf.io.gfile.GFile(image_url, 'rb')
    img = preprocess_image(Image.open(fd))
  original_image_cache[image_url] = img
  # Load and convert to float32 numpy array, add batch dimension, and normalize to range [0, 1].
  img_raw = img
  if tf.reduce_max(img) > 1.0:
    img = img / 255.
  if len(img.shape) == 3:
    img = tf.stack([img, img, img], axis=-1)
  if not dynamic_size:
    img = tf.image.resize_with_pad(img, image_size, image_size)
  elif img.shape[1] > max_dynamic_size or img.shape[2] > max_dynamic_size:
    img = tf.image.resize_with_pad(img, max_dynamic_size, max_dynamic_size)
  return img, img_raw

def show_image(image, title=''):
  image_size = image.shape[1]
  w = (image_size * 6) // 320
  plt.figure(figsize=(w, w))
  plt.imshow(image[0], aspect='equal')
  plt.axis('off')
  plt.title(title)
  plt.show()

"""## 2. 選擇圖像 
您可以選擇以下圖像之一，或使用您自己的圖像。 請記住，模型的輸入大小各不相同，其中一些使用動態輸入大小（啟用對未縮放圖像的推斷）。 鑑於此，方法 load_image 已經將圖像重新縮放為預期格式。

選項: ['老虎'，'公共汽車'，'汽車'，'貓'，'狗'，'蘋果'，'烏龜'，'火烈鳥'，'鋼琴'，'蜂窩'，'茶壺']

param ['tiger', 'bus', 'car', 'cat', 'dog', 'apple', 'turtle', 'flamingo', 'piano', 'honeycomb', 'teapot']
"""

print('*** Done by %s at ' % ts3,today, type(today))
## Demo: Show tiger

image_name = 'tiger' 

images_for_test_map = {
    "tiger": "https://upload.wikimedia.org/wikipedia/commons/b/b0/Bengal_tiger_%28Panthera_tigris_tigris%29_female_3_crop.jpg",
    "bus": "https://upload.wikimedia.org/wikipedia/commons/6/63/LT_471_%28LTZ_1471%29_Arriva_London_New_Routemaster_%2819522859218%29.jpg",
    "car": "https://upload.wikimedia.org/wikipedia/commons/4/49/2013-2016_Toyota_Corolla_%28ZRE172R%29_SX_sedan_%282018-09-17%29_01.jpg",
    "cat": "https://upload.wikimedia.org/wikipedia/commons/4/4d/Cat_November_2010-1a.jpg",
    "dog": "https://upload.wikimedia.org/wikipedia/commons/archive/a/a9/20090914031557%21Saluki_dog_breed.jpg",
    "apple": "https://upload.wikimedia.org/wikipedia/commons/1/15/Red_Apple.jpg",
    "turtle": "https://upload.wikimedia.org/wikipedia/commons/8/80/Turtle_golfina_escobilla_oaxaca_mexico_claudio_giovenzana_2010.jpg",
    "flamingo": "https://upload.wikimedia.org/wikipedia/commons/b/b8/James_Flamingos_MC.jpg",
    "piano": "https://upload.wikimedia.org/wikipedia/commons/d/da/Steinway_%26_Sons_upright_piano%2C_model_K-132%2C_manufactured_at_Steinway%27s_factory_in_Hamburg%2C_Germany.png",
    "honeycomb": "https://upload.wikimedia.org/wikipedia/commons/f/f7/Honey_comb.jpg",
    "teapot": "https://upload.wikimedia.org/wikipedia/commons/4/44/Black_tea_pot_cropped.jpg",
}

img_url = images_for_test_map[image_name]
image, original_image = load_image(img_url, image_size, dynamic_size, max_dynamic_size)
show_image(image, 'Scaled image')

print('*** Done by %s at ' % ts3,today, type(today))
# 實作: Show teapot

# 你的程式

print('*** Done by %s at ' % ts3,today, type(today))
# 實作: Show turtle

# 你的程式

print('*** Done by %s at ' % ts3,today, type(today))
# 實作: 請由以上的選項自選一個來試試

# 你的程式
```
### 連結 https://colab.research.google.com/drive/1swAvhHTWw_1SrInC3aIUFRdzQztjynbs?usp=sharing
