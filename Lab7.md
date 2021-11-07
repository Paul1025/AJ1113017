# 嵌入式系統 - 實作7: AI-based ES? AI? ML? DL? 要如何入門 (How To Learn)? (W12)
## Lab 7-1 在你的Google Drive, 建立你的第一個Colab Notebook 
### Step 1. 安裝Colab;
### Step 2. 新增ES2021的Folder;
### Step 3. 在此Folder下, 建立你的第一個Colab Notebook (i.e. 'hello-ai'). 將你的Google Drive和Google VM (Virtual Machine)掛接
### Step 4. 在你Colab Notebook顯示以下訊息(OOO: 你的英文名字; e.g., Joe biden)
### Hello AI. I am OOO. Nice to meet you!
### Today is Sunday, 2021.11.07
### Step 5. 新增文字儲存格: Colab也可使用markdown耶. (請用你的英文名字)
![003](https://user-images.githubusercontent.com/89329182/140632044-50142260-97d2-4e26-b78b-3d59ac91cac3.jpg)
## Lab 7-2 十分鐘學會Python!? **Really?**
### 程式
```C
# task 1: string variable
name = "Liang Paul"
print(name)

# task 2: number variable
number = 26
print(number)
print(number*3)
print(number/2)
print(number + number)
print(number - number)

# task 3: function

def printName(firstName, lastName):
  print(lastName + ' ' + firstName)

printName('Paul', 'Liang')

# task 4: if else

def printName(firstName, lastName, isCool):
  if isCool:
    print(lastName + ' ' + firstName + ' very cool!')
  else:
    print(lastName + ' ' + firstName + ' not cool!')

# Start
printName('Paul', 'Liang', True)
printName('Paul', 'Liang', False)

# task 5: for loop

def printName(firstName, lastName, isCool, num):
  for i in range(1, num):
    if isCool:
      print(i, lastName + ' ' + firstName + ' very cool!')
    else:
      print(i, lastName + ' ' + firstName + ' not cool!')

# Start
printName('Paul', 'Liang', True, 10)
```
### Task 5的結果
![005](https://user-images.githubusercontent.com/89329182/140632106-0d6903d6-1a7c-4790-8e40-25956d5ec55f.jpg)
