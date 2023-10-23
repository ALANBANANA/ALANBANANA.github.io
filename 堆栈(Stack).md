# 堆栈(Stack)

## Day 5栈的定义

> 简称为栈。一种线性表数据结构，是一种只允许在表的一端进行插入和删除操作的线性表，(即先进后出)

![img](https://datawhalechina.github.io/leetcode-notes/images/ch02/02.02.01-001.png)

**三个关键的基本名词**

* 允许在栈中插入和删除的一端称为**[栈顶]**
* 栈顶的*另一端*叫做**[栈底]**
* 当表中没有任何数据元素的时候，称之为**[空栈]**

**栈的两种基本操作**

1. 栈的插入操作称为**[入栈]**和**[进栈]**
2. 栈的删除操作称为**[出栈]**和**[退栈]**

总结一点就是**先进后出**---->**LIFO结构**

**两方面解释栈的定义**

1. **栈是一个线性表**，栈中的元素有前驱后继性。栈中的元素按照a_1, a_2, a_3, ……次序依次进栈。栈顶元素为a_n.
1. **后进先出原则**，根据定义，由于栈的底端为一封闭的元素，最先进栈的必被后面的压在底下，所以后面进栈的将可以在栈顶，获取优先出栈的机会，所以元素对于先进栈的来说是:先进后出，而对于后进栈的则是：后进先出

### 堆栈的顺序存储于链式存储

### 1. 顺序栈

> 即堆栈的顺序存储结构。利用一组地址连续存储单元一次自栈底到栈顶的元素，同时使用**指针top**指示栈顶元素在顺序栈中的位置

### 2.链式栈

> 即堆栈的链式存储结构。利用单链表的方式来实现堆栈。栈中元素按照插入顺序插入到链表的第一个节点之前，使用栈顶指针top指示栈顶元素，**top永远指向链表的头节点**

### 栈的基本操作

理应拥有所有线性表的操作特性，可是后进先出，以下为基本操作：

1. 初始化空栈：创建一个空栈，定义栈的大小size，以及栈顶的指针top
2. 判断栈是否为空：当堆栈为空时，返回True。当堆栈不为空时，返回False。一般至用于栈中删除操作和获取当前栈顶元素操作中
3. 判断栈是否已满：当堆栈已满时，返回True，当堆栈未满时，返回False。一般只用于顺序栈中插入元素和获取当前栈顶元素操作中
4. 插入元素(进栈、入栈)：相当于在线性表最后元素后面插入一个新的数据元素。并改变栈顶指针top的指向位置
5. 删除元素(出栈、退栈)：相当于在线性表最后元素后面删除最后一个数据元素。并改变栈顶指针top的指向位置
6. 获取栈顶元素：相当于获取线性表中的最后一个数据元素。与插入元素、删除元素不同的是，该操作并不改变栈顶指针top的指向位置。

### 基于Python的堆栈顺序存储实现

### **用一个列表来表示堆栈的顺序存储结构，借助list来实现-------->[顺序栈]**

```python
class Stack:
    """初始化一个空栈"""
    def __init__(self, size=100):
        self.stack = []  # 代表一个栈
        self.size = size  # 栈的大小
        self.top = -1  # 栈顶指针:在列表里面可以是指代最后一个元素,列表里面相当于索引
        
 	def is_empty(self):
        """判断栈是否是一个空栈"""
        return self.top == -1  # 空的时候栈为空没有元素，每每添加或者删除指针必须要改变其在列表中的位置
    
    def is_full(self):
        """判断栈是否已经为一个满栈"""
        return self.top + 1 == self.size  # 开始为空栈，长度为0，而列表是从0位开始，栈顶指针从-1开始，对于列表而言，长度是列表中的元素个数，而指针从-1开始所以自然而然还要多加1，相当于$索引位置$
    
    def push(self, value):
        """入栈操作"""
        if self.is_full():
            raise Exception('Stack is full')
        else:
            self.stack.append(value)  # 由于列表的元素添加是加在末尾
            self.top += 1  # 栈顶指针向右移，看起来像是个计时器一样性质的东西
            
	def pop(self):
        """出栈操作"""
        if self.is_empty():
            raise Excoption('Stack is full')
        else:
            self.stack.pop()
            self.top -= 1  # 上述初始化stack为空，所以top为1，在我看来相当于几个计时器因为在Python当中列表的开始是0
	
    def peek(self):
        """获取栈顶的元素"""
        if self.is_empty():
            raise Exception('stack is empty')
        else:
            return self.stack[self.top]  # 因为栈顶指针永远指向栈顶
```

### **基于Python堆栈链式存储的实现**------------>**[链式栈]**

实际将内部每一个元素变成一个节点插入在头节点前面，那么无论如何可以所以就先索引第一个头节点

```python
class Node:
    """建立关于链表的节点，为节点，但不是链表"""
    def __init__(self, value):
        self.value = value
        self.next = None

class Stack:
    """初始化栈的属性"""
    def __init__(self):
        self.top = None  # 栈顶指针
    
    def is_emptty(self):
        """判断栈是否为空栈"""
        return self.top = None
    
    def push(self, value):
        """入栈操作"""
        cur = Node(value)
        cur.next = self.top
        self.top = cur
        
    def pop(self):
        """出栈操作"""
        if self.is_empty():
            raise Exception('Stack is empty')
        else:
            storage = self.top  # 这里的self.top为存储的一个头节点在里面storage，所以self.top为一个节点
            self.top = self.top.next  # 使用目前栈顶指针指向原栈顶的下一个
            del storage  # 这里storage存储的是栈顶指针指代的头节点，删除的为一个节点，而不是栈顶指针
```

## Day 6 单调栈

> 一种特殊的栈，在栈的基础上**[先进后出]**，要求**从栈顶**到**栈底**的元素是单调递增(或者单调递减)。其中满足从栈底到栈底的元素是单调栈，元素**递增到栈底**的叫做**单调递增栈**，元素**递减至栈底**的叫做**单调递减栈**

**Conclusion**：栈顶到栈底呈递增的为单调递增栈，栈顶到栈底呈递减的为单调递减栈

### 单调递增栈

> 只有那些比栈顶元素要大的才可以进栈，否则需要先将栈中比当前压入元素小的移出栈中，再压入当前元素，如此可得单调递增栈

#### 元素进出栈的过程

* 假设有一个元素x，x比栈顶元素小，直接入栈

* 反过来，此时栈顶元素比x要小，甚至于说栈顶之下的元素都要比x要小，直至到下面遇到个比x大的元素为止，比x小的都取出来，再压入栈中

  ![img](https://datawhalechina.github.io/leetcode-notes/images/ch02/02.02.05-001.png)

  

### 单调递减栈

> 只有那些比栈顶元素小的才能够进栈，否则要将比当前需要压入元素大的先移出，再压入当前元素，这样才可以保证栈为单调递减的栈

#### 元素进出栈过程

* 假设目前有一个元素，如果他比栈中任何元素要大，则直接放在栈顶
* 如果压入元素比当前栈中元素都要小，那么当前栈里面的元素会被拿出，直到找到比当前元素还小的，否则大的部分会被拿出，然后当前元素压入栈中

![img](https://datawhalechina.github.io/leetcode-notes/images/ch02/02.02.05-002.png)

### 单调栈一般适用场景

1. 寻找左侧第一个元素比当前元素要大的元素

   从左到右遍历元素，构造单调递增栈(栈顶到栈底)：

   * 一个元素左侧第一个比它大的元素就是就是将其插入单调递增的栈顶元素
   * 如果插入时栈为空，说明左侧不存再比目前当前元素大的元素

2. 寻找左侧第一个比当前元素小的元素

   从左到右遍历元素，构造单调递减栈(栈顶到栈底)：

   * 一个元素如果左侧第一个比它小，则其为插入的单调递减栈的栈顶元素
   * 插入时为空栈，那么当前左侧不存在比它小的元素

3. 寻找右侧第一个比当前元素大的元素

   从左到右遍历元素，构造单调递增栈：

   * 一个元素如果右侧第一个比它大的元素，那么该比较大的元素即为要弹出单调栈时即将插入的元素
   * 如果该元素没有被弹出单调栈，说明右侧不存在比当前元素大的元素

4. 寻找右侧第一个比当前元素小的元素

   从左到右遍历元素，构造单调递减栈

   * 一个元素右侧第一个元素比它小就是将其弹出单调递减栈时即将插入的元素
   * 如果该元素没有被弹出栈，则说明右侧不存在比当前元素小的元素

#### **单调栈的相关模板**

单调**递增**栈模板

```python
def monotIncreasingStack(nums):
    stack = []
    for num in nums:
        while stack and num >= stack[-1]:
            stack.pop()
        stack.append(num)
```

单调**递减**栈模板

```python
def monotoneDecreasingStack(nums):
    stack = []
    for num in nums:
        while stack and num <= stack[-1]:
            stack.pop()
        stack.append(num)
```

Conclusion：这里的栈实际上更可以看成是一般的辅助栈去存储数据，变种来看，无论如何stack作为数组来称为栈，变种而言局部像是单调栈的特点了(存在于我在利用GPT帮我进行一般场景的理解的时候)，对于上两则模板，实际则是单独的计算，并没有对苏剧进行存储功能，所以不可以混为一谈

```python
def find_next_larger_element(nums):
    stack = []  # 创建一个空栈，用于存储元素的索引, 相当于一个辅助作用
    result = [-1]*len(nums)  # 初始化结果数组，用-1进行填充 [-1, -1, -1, -1, …………]
    for i in range(len(nums)):
        while stack and nums[i] > nums[stack[-1]]:  # 固然如此所以是一则单调递增的栈
            top = stack.pop()  # 这里实际上是对数组进行栈的单调递增操作，栈顶至栈底为单调递增，没用的取出去
            result[top] = nums[i]
      	stack.append(i)  # 将当前元素的索引压入栈中
    return result

nums = [2, 1, 2, 4, 3]
result = find_next_larger_element(nums)
print(result)  # [4, 2, 4, -1, -1]  所以具体情况需要具体分析
```

## 总结：

1. 对比链表而言其实堆栈并不难，很容易理解，其次题目上手程度可能在不断随着我的水平也越发有手感
2. 关于单调栈在引用一些数的索取的时候，很容易被单独的stack=[]所影响为非单调栈，或者判断失误，这时候应该好好去重新理解这个数到底是什么东西，是数字是单调栈，还是索引才是单调栈

## 资料来源

1. [开源内容]<https://github.com/datawhalechina/leetcode-notes/blob/main/docs/ch02/index.md>
2. [电子网站]<https://datawhalechina.github.io/leetcode-notes/#/ch02/index.md>
3. [hello算法]<https://www.hello-algo.com/>

