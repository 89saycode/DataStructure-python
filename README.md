## 栈

### 什么是栈?

栈就是一个有序集合，排序的原则是: LIFO(last-in first-out) 后进先出。

例如: 

```python
l = [0, 1, 2, 3, 4]
n = []
```
有两个列表，一个列表名字为 "l", 另一个列表名字为 "n"， 然后将 "l" 列表元素按照顺序移入到 "n" 的列表当中。

```python
l = []
n = [4, 3, 2, 1, 0]
```
这样就形成了一个后进先出的栈，


### 栈中相应方法
- stack() 创建一个空栈。
- push(item) 将一个元素添加到栈的顶端。
- pop() 将栈顶端的元素移出。
- peek() 返回栈顶端的元素，并不移出该元素。
- isEmpty() 检查栈是否为空。
- size() 返回栈中元素的数目。

### 代码实现
```python
class Stack:
    def __init__(self):
        """
            初始化空栈
        """
        
        self.items = []

    def isEmpty(self):
        """
            检查栈是否为空
        """
        
        return self.items == []

    def push(self, item):
        """
            将一个元素添加到栈的顶端
            :param item 元素
        """
        
        self.items.append(item)
        
    def pop(self):
        """
            将栈顶端的元素移出
        """
            
        return self.items.pop()

    def peek(self):
        """
            返回栈顶端的元素，并不是移出该元素
        """
        
        return self.item[len(self.items) - 1]

    '''
        返回栈中元素的数目
    '''
    def size(self):
        return len(self.items)
```

### 相关题目
#### 匹配括号
有如下括号
```
((()))
```
我们要做的是，从左到右依次匹配括号， 一个 "(", 对应一个 ")"。
- 思路: 由一个空栈开始，从左往右依次处理括号。如果遇到左括号，便通过push() 将其加入栈中，等待右括号，在去调用pop() 移出一个左括号。 只要栈中的所有左括号都能匹配到右括号，则栈会为空。

```python
def parChecker(symbolString):
    """
        :param symbolString 符号字符串
    """
    
    s = Stack()  # 创建一个栈
    balanced = True  # 保持括号平衡
    index = 0  # 下标
    
    while index < len(symbolString) and balanced:
        symbol = symbolString[index]  # 获取
        if symbol == "(":  # 如果是左括号，加入到栈中
            s.push(symbol)
        else:  # 如果是右括号，移出一个左括号
            if s.isEmpty():  # 栈是否为空
                balanced = False
            else:
                s.pop()  # 移出一个左括号

        index = index + 1  # 下标 +1

    if balanced and s.  isEmpty():
        return True
    else:
        return False

parChecker("((()))")
```

## 队列

### 什么是队列?

队列是有序集合，添加操作发生在“尾部”，移出操作发生在“头部”。排序的原则是: FIFI (first-in first-out) 先进先出。

如图所示:
![](https://github.com/89saycode/DataStructure-python/blob/main/images/%25E9%2598%259F%25E5%2588%2597%25E5%259B%25BE.png)
### 队列中相应方法
- Queue() 创建一个空队列。
- enqueue(item) 在队列尾部添加一个元素。
- dequeue() 从队列头部移出一个元素。
- isEmpty() 检查队列是否为空。
- size() 返回队列中元素的数目。

### 代码实现
```python
class Queue:
    def __init__(self):
        """
            初始化队列
        """
        
        self.items = []  

    def isEmpty(self):
        """
            检查队列是否为空
        """
        
        return self.items == []

    def enqueue(self, item):
        """
            在队列尾部添加一个元素
            :param item  元素
        """
        
        self.items.insert(0, item)

    def dequeue(self):
        """
            从队列头部移出一个元素
        """
        return self.items.pop()

    def size(self):
        """
            返回队列中元素的数目
        """
        
        return len(self.items)
```

### 相关题目
#### 六人传手雷游戏
六个人顺序传递手雷，传递到某人时，手雷将会爆炸，这个人也就死了，返回最后的胜利者。

![IMG_CE58B9F52DC8-1](media/16902965487867/IMG_CE58B9F52DC8-1.jpeg)

思路: 程序需要两个参数， 一个参数是 名字列表 "nameList" 和 一个爆炸计数常量 "num" (手雷在什么时候爆炸)。

```python
def transferGrenade(nameList, num):
    """
        :param nameList 名字列表
        :param num      计数常量
    """
    queue = Queue()  # 创建一个空队列

    for name in nameList:       # 遍历名字列表
        queue.enqueue(name)     # 添加到队列当中

    while queue.size() > 1:
        for i in range(num):    # 遍历传入计数常量次数
        
             # 移除一个名字元素，并且添加队尾
            queue.enqueue(queue.dequeue())  
            
        # 手雷爆炸，移除一个名字元素
        queue.dequeue()        
    return queue.dequeue()      # 返回最后一个名字元素


if __name__ == '__main__':
    name = transferGrenade(
    ["张三", "李四", "王五", "周六", "赵七", "孙八"], 5)
    print(name) # 周六
```

## 双端队列

### 什么是双端队列?

双端队列是与队列类似的有序集合，它有一前，一后两端，元素在哪一段添加和移除元素都没有任何问题。排序的原则是: 取决于使用者。

### 队列中相应方法
- Queue() 创建一个空双端队列。
- addFront(item) 将一个元素添加到双端队列的前端。
- addRear(item) 将一个元素添加到双端队列的后端。
- removeFront() 从双端队列的前端移除一个元素。
- removeRear() 从双端队列的后端移除一个元素。
- isEmpty() 检查双端队列是否为空。
- size() 返回双端队列中元素的数目。

### 代码实现
```python
class Deque:
    def __init__(self):
        """
            初始化双端队列
        """
        
        self.items = []  

    def isEmpty(self):
        """
            检查双端队列是否为空
        """
        
        return self.items == []

    def addFront(self, item):
        """
            在双端队列前端添加一个元素
            :param item  元素
        """
        
        self.items.append(item)
        
    def addRear(self, item):
        """
            在双端队列后端添加一个元素
            :param item  元素
        """
        
        self.items.insert(0, item)
    
    def removeFront(self):
        """
            从双端队列前端移出一个元素
        """
        return self.items.pop()
    
     def removeRear(self):
        """
            从双端队列后端移出一个元素
        """
        return self.items.pop(0)

    def size(self):
        """
            返回双端队列中元素的数目
        """
        
        return len(self.items)
```

### 相关题目
#### 回文问题
回文问题是指从前往后和从后往前读都一样的字符串，例如oppo、toot等。

思路: 使用双端队列来存储字符串中的字符。按从左往右的顺序将字符串中的字符添加到双端队列的后端。利用双端队列的双重性，前端是字符串的第一个字符，后端是字符串的最后一个字符。

```python
def palChecker(aString):
    """
        :param aString 要判断回文的字符串
    """

    charDeque = Deque()         # 创建双端队列

    for ch in aString:
        # 将字符添加到双端队列前端
        charDeque.addRear(ch)

    stillEqual = True  # 相等 默认True

    while charDeque.size() > 1 and stillEqual:
        # 移除一个双端队列前端元素
        firstChar = charDeque.removeFront()
        # 移除一个双端队列后端元素
        lastChar = charDeque.removeRear()

        # 如果前后两个字符不相等
        if firstChar != lastChar:
            # 相等变为 False
            stillEqual = Fasle

    return stillEqual


if __name__ == '__main__':
    stillEqual = palChecker("tooppoot")

    if stillEqual:
        print("是回文")
    else:
        print("不是回文")
```
