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
        self.items = []     # 初始化空栈

    '''
        检查栈是否为空
    '''
    def isEmpty(self):
        return self.items == []

    '''
        将一个元素添加到栈的顶端
    '''
    def push(self, item):
        self.items.append(item)
        # self.items.insert(0, item) 慢

    '''
        将栈顶端的元素移出
    '''
    def pop(self):
        return self.items.pop()

    '''
        返回栈顶端的元素，并不是移出该元素
    '''
    def peek(self):
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