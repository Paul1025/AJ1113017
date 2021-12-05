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
