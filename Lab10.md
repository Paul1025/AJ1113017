# 嵌入式系統 - 實作10: AI最經典火紅的應用之人臉偵測實作 (W16)
## Lab 10-1: 虛擬人臉數據取得
```python
# 000
print('hello AI')

"""##記得要使用GPU (編輯 >> 筆記本設定 >> GPU)"""

# 001 將我們的Google Drive連結上Virtual Machine
from google.colab import drive
drive.mount('/content/drive')

# 002 Check the current working directory
!pwd

# Commented out IPython magic to ensure Python compatibility.
# 003 Change the right working directory
# %cd '/content/drive/MyDrive/ES2021/exp_FD_20211205'

# 004 Check again
!pwd

"""## Topic 1: 人臉數據取得"""

#101 虛擬人造人臉
from IPython.display import Image
print('這都是虛擬人造人臉')
Image('face31.jpg',width=400)

"""## Lab 1"""

"""### Lab1: 讓我們下載2張自選的虛擬人造臉 (VF04.jpg, VF05.jpg), 並且上傳到我們的Google Drive, 並且用以上的指令來顯示出來"""
#102 Lab: 自行下載二張來試試 face generator, https://thispersondoesnotexist.com/

#虛擬人造人臉1
Image('VF04.jpg',width=200)

# 103 虛擬人造人臉2
Image('VF05.jpg',width=200)
```
![001](https://user-images.githubusercontent.com/89329182/144732196-2aa3c218-fb53-45ba-a009-353cc5990e17.jpg)
### 連結:https://colab.research.google.com/drive/1l1Ebszd3PKyK2ygVLf0Bwb-GHAIMIwju#scrollTo=1WUA_pTRnQGx

## Lab 10-2 OpenCV電腦視覺入門
```python
"""## Topic 2: OpenCV`電腦視覺`入門"""

# Commented out IPython magic to ensure Python compatibility.
#201 讀取黑白圖片

# %matplotlib inline
import matplotlib.pyplot as plt
import cv2
cv2.__version__ #版本不斷更新中

#顯示圖片
import numpy as np
img=cv2.imread('face31.jpg',0) #0 grayscale 1 color
from google.colab.patches import cv2_imshow
cv2_imshow(img) # correct method

#202 讀取彩色圖片
img=cv2.imread('face31.jpg',1)
cv2_imshow(img)
img.shape

#203 openCV是 BGR
import matplotlib.pyplot as plt
img = cv2.imread("face31.jpg") # 圖片讀取到img變數
#plt.figure(figsize=(4,3))
#plt.axis("off") 
plt.imshow(img) # 圖片顯示

#204 BGR to RGB

img1=cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.imshow(img1)

#205 openCV簡易繪圖範例
import numpy as np
# 建立一張 256x256 的 RGB 圖片（0黑色）
img = np.zeros((256, 256, 3), np.uint8) #np.zeros建立0矩陣
# 將圖片用淺灰色 (200, 200, 200) 填滿
img.fill(200)
# 在圖片上畫一條紫紅色的對角線，寬度為 5 px (0,0在最左上角)
# cv2.line(影像, 開始座標, 結束座標, 顏色, 線條寬度)
cv2.line(img, (0, 0), (255, 255), (255, 0, 255), 5)
# 顯示圖片
cv2_imshow(img)

'''#206: 在圖片上畫二條交錯的紫紅色的對角線，寬度為 5 px (0,0在最左上角), '''

# Your Code
import numpy as np
# 建立一張 256x256 的 RGB 圖片（0黑色）
img = np.zeros((256, 256, 3), np.uint8) #np.zeros建立0矩陣
# 將圖片用淺灰色 (200, 200, 200) 填滿
img.fill(200)
# 在圖片上畫一條紫紅色的對角線，寬度為 5 px (0,0在最左上角)
# cv2.line(影像, 開始座標, 結束座標, 顏色, 線條寬度)
cv2.line(img, (0, 0), (255, 255), (255, 0, 255), 5)
cv2.line(img, (0, 255), (255, 0), (255, 0, 255), 5)
# 顯示圖片
cv2_imshow(img)
```
![002](https://user-images.githubusercontent.com/89329182/144732497-7724fdc9-1666-448b-84c9-0516ca1d8be0.jpg)
###　連結https://colab.research.google.com/drive/1l1Ebszd3PKyK2ygVLf0Bwb-GHAIMIwju#scrollTo=mJKLkKCLpFg-

## Lab 10-3 人臉辨識實際應用
```python
#311 ### 下載open CV 人臉分類器 

# 下載open CV 人臉分類器!!
# 使用特徵檢測+機器學習演算法，從影像中找到人臉
!wget https://raw.githubusercontent.com/opencv/opencv/master/data/haarcascades/haarcascade_frontalface_default.xml

#312 openCV辨識人臉4步驟 

# ****** openCV辨識人臉4步驟 ******
# 1.載入圖片
image = cv2.imread('face31.jpg')
# 2.載入分類器
haar = cv2.CascadeClassifier('haarcascade_frontalface_default.xml')
# 3.圖片轉灰階
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
# 4.使用分類器從圖片找到人臉
faces = haar.detectMultiScale(gray) #偵測人臉
# 得到的結果是 臉的左上角座標與寬、高的像素座標(0,0在最左上角)
print("找到臉的數量=",len(faces))
print(faces)

#313 把找到的臉加框
for (x,y,w,h) in faces: #左上角座標x,y與寬w、高h
    #圓形 cv2.circle(影像, 圓心座標, 半徑, 顏色, 線條寬度) 負數代表實心
    cv2.circle(image,(x, y), 35, (0, 0, 255), -1) #紅點標示x,y
    #矩形 cv2.rectangle(影像, 頂點座標, 對向頂點座標, 顏色, 線條寬度)
    cv2.rectangle(image,(x,y),(x+w,y+h),(0,255,0),3) #畫矩形框 可改框的顏色/線條粗細
    #文字 cv2.putText(影像, 文字, 座標, 字型, 大小, 顏色, 線條寬度, 線條種類)
    cv2.putText(image, ('x,y'), (x+50, y-50), cv2.FONT_HERSHEY_SIMPLEX,
    3, (0, 255, 255), 5, cv2.LINE_AA)
plt.figure(figsize=(10,4)) #設定顯示尺寸
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB)) #BGR to RGB

#314 Lab
image = cv2.imread('face31.jpg')

for (x,y,w,h) in faces: #左上角座標x,y與寬w、高h
    #圓形 cv2.circle(影像, 圓心座標, 半徑, 顏色, 線條寬度) 負數代表實心
    cv2.circle(image,(x, y), 35, (255, 0, 0), -1) #紅點標示x,y
    #矩形 cv2.rectangle(影像, 頂點座標, 對向頂點座標, 顏色, 線條寬度)
    cv2.rectangle(image,(x,y),(x+w,y+h),(0,0,255),3) #畫矩形框 可改框的顏色/線條粗細
    #文字 cv2.putText(影像, 文字, 座標, 字型, 大小, 顏色, 線條寬度, 線條種類)
    cv2.putText(image, ('Grace Exp'), (x+50, y-50), cv2.FONT_HERSHEY_SIMPLEX,
    3, (0, 255, 255), 5, cv2.LINE_AA)
plt.figure(figsize=(10,4)) #設定顯示尺寸
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB)) #BGR to RGB

#315 實作練習.找一張圖片有10個以上人臉,
img = cv2.imread("face94.jpg") #("/content/face-filters-.jpg")
#plt.figure(figsize=(4,3))
#plt.axis("off")
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB)) #BGR to RGB

#316 練習.找一張圖片有10個以上人臉,並偵測人臉數量
image = cv2.imread('face94.jpg')
haar = cv2.CascadeClassifier('haarcascade_frontalface_default.xml') #載入分類器
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)#圖片轉灰階
faces = haar.detectMultiScale(gray) #偵測人臉
for (x,y,w,h) in faces:
    cv2.rectangle(image,(x,y),(x+w,y+h),(0,255,0),2) #畫矩形框 可改框的顏色/線條粗細
plt.figure(figsize=(12,10)) #設定顯示尺寸
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB)) #BGR to RGB
print('找到臉的數量:',len(faces))

'''' Lab實作: 試試看使用你自己在網路上找到的團體照, 並且加入你的英文名字 '''

# Your Code
image = cv2.imread('paul.jfif')
haar = cv2.CascadeClassifier('haarcascade_frontalface_default.xml') #載入分類器
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)#圖片轉灰階
faces = haar.detectMultiScale(gray) #偵測人臉
for (x,y,w,h) in faces:
    cv2.rectangle(image,(x,y),(x+w,y+h),(0,255,0),2) #畫矩形框 可改框的顏色/線條粗細
plt.figure(figsize=(12,10)) #設定顯示尺寸
cv2.putText(image, ('Paul'), (x+50, y-50), cv2.FONT_HERSHEY_SIMPLEX,
    3, (0, 255, 255), 5, cv2.LINE_AA)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB)) #BGR to RGB
print('找到臉的數量:',len(faces))
```
### 結果
![003](https://user-images.githubusercontent.com/89329182/144733048-ea70074c-39f9-43b1-9993-251a95e0583c.jpg)
```python

#321 face_recognition 是python第三方模組，基於深度學習的人臉辨識功能
!pip install face_recognition #安裝模組

#322 Commented out IPython magic to ensure Python compatibility.

import cv2
import face_recognition
# %matplotlib inline
import matplotlib.pyplot as plt
image = face_recognition.load_image_file("face94.jpg") #92
faces = face_recognition.face_locations(image,model='cnn')
print("找到臉的數量=",len(faces))
for (top, right, bottom, left) in faces: #畫矩形框 可改框的顏色/線條粗細
    cv2.rectangle(image, (left, top), (right, bottom), (0, 255, 0), 2)
plt.figure(figsize=(12,10))
#plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.imshow(image)

'''' Lab實作: 試試看使用你自己在網路上找到的團體照, 並且加入你的英文名字 '''

# Your Code
import cv2
import face_recognition
# %matplotlib inline
import matplotlib.pyplot as plt
image = face_recognition.load_image_file("paul.jfif") #92
faces = face_recognition.face_locations(image,model='cnn')
print("找到臉的數量=",len(faces))
for (top, right, bottom, left) in faces: #畫矩形框 可改框的顏色/線條粗細
    cv2.rectangle(image, (left, top), (right, bottom), (0, 255, 0), 2)
plt.figure(figsize=(12,10))
#plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
cv2.putText(image, ('Paul'), (x+50, y-50), cv2.FONT_HERSHEY_SIMPLEX,
    3, (0, 255, 255), 5, cv2.LINE_AA)
plt.imshow(image)
```
