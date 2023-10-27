# 队列(Queue)

## 队列定义

> 是一种遵循先入后出规则的线性结构，模拟了排队现象，即新来的人不断假如队列的尾部，而位于队列头部的人逐个离开

![img](https://www.hello-algo.com/chapter_stack_and_queue/queue.assets/queue_operations.png)

## 队列的常用操作

| 方法名 | 描述                         | 时间复杂度 |
| ------ | ---------------------------- | ---------- |
| push() | 元素入队，即将元素添加到尾部 | O(1)       |
| pop()  | 队首元素出队                 | O(1)       |
| peek() | 访问队首元素                 | O(1)       |

## 基于链表的队列实现

```python
"""由于队列是队首出，队尾进，仅需在链表当中进行限制"""
class LinkedListQueue:
    """基于链表实现的队列"""
    def __init__(self):
        """构造方法"""
        self.head = ListNode | None = None
        self.rear = ListNode | None = None
        self.size = 0
        
	def size(self):
        """获取队列的长度"""
        return self.size
    
    def is_empty(self):
        """判断队列是否为空队列"""
        return not self.head
    
    def push(self, num):
        """将元素推入队列之中"""
        if self.head is None:
            self.head = node
            self.rear = node
        else:
            self.rear.next = node
            self.rear = node
            
	def pop(self):
        """将元素出队"""
        num = self.peek()
        # 删除头节点
        self.head = self.head.next
        self.size -= 1
        return num
    
    def peek(self):
        """访问队首元素"""
        if self.is_empty():
            raise IndexError('队列为空')
        return self.head.val
    
    def to_list(self):
        """将队列变成数组打印出来"""
        queue = []
        temp = self.head  # 头结点代表链表进行链表的访问
        while temp:
            queue.append(temp.val)
            temp = temp.next
        return queue
```

## 基于数组的队列实现

假如有个数组的长度是n，当遍历到k个元素的时候实际的时间复杂度将去到大概O(k)左右呈现线性的时间复杂性。

基于此设计head代表着队首的元素索引，记录着一个列表的长度size用以记录数组的长度，所以其实关于当前数组的尾部实际为：rear = head + size，于此当前公式即为rear指针指向尾部元素的下一个位置，实际尾部元素为rear-1的位置

**实际数组的有效元素区间为**： [head, rear - 1]

* 入队操作：将输入元素赋值给rear索引出，将size增加1
* 出队操作：只需要将head+1，将数组长度size-1即可

```python
class ArrayQueue:
    """基于环形数组实现的队列"""

    def __init__(self, size: int):
        """构造方法"""
        self._nums: list[int] = [0] * size  # 用于存储队列元素的数组
        self._front: int = 0  # 队首指针，指向队首元素
        self._size: int = 0  # 队列长度

    def capacity(self) -> int:
        """获取队列的容量"""
        return len(self._nums)

    def size(self) -> int:
        """获取队列的长度"""
        return self._size

    def is_empty(self) -> bool:
        """判断队列是否为空"""
        return self._size == 0

    def push(self, num: int):
        """入队"""
        if self._size == self.capacity():
            raise IndexError("队列已满")
        # 计算尾指针，指向队尾索引 + 1，这里的最末端实际上已经是越过了数组正确的位置，所以添加的时候rear就已经指向了新添加的元素
        # 通过取余操作，实现 rear 越过数组尾部后回到头部
        rear: int = (self._front + self._size) % self.capacity()
        # 将 num 添加至队尾
        self._nums[rear] = num
        self._size += 1

    def pop(self) -> int:
        """出队"""
        num: int = self.peek()
        # 队首指针向后移动一位，若越过尾部则返回到数组头部
        self._front = (self._front + 1) % self.capacity()
        self._size -= 1
        return num

    def peek(self) -> int:
        """访问队首元素"""
        if self.is_empty():
            raise IndexError("队列为空")
        return self._nums[self._front]

    def to_list(self) -> list[int]:
        """返回列表用于打印"""
        res = [0] * self.size()
        j: int = self._front
        for i in range(self.size()):
            res[i] = self._nums[(j % self.capacity())]
            j += 1
        return res

```

## 双向队列

> 个人感觉与双向链表十分的相像，可以在队首进行元素删改以及队尾的元素删改，具有更高的灵活性

![双向队列的操作](https://www.hello-algo.com/chapter_stack_and_queue/deque.assets/deque_operations.png)

## 双向队列的常用操作

| 方法名      | 描述             | 时间复杂度 |
| ----------- | ---------------- | ---------- |
| pushFirst() | 将元素添加至队首 | O(1)       |
| pushLast()  | 将元素添加至队尾 | O(1)       |
| popFirst()  | 删除队首元素     | O(1)       |
| peekFirst   | 访问队首元素     | O(1)       |
| peekLast    | 访问队尾元素     | O(1)       |

## 基于双向链表的双向队列实现

其实就是将链表的头节点和尾节点进行只允许其删除和增加的权力

```python
class ListNode:
    """双向链表节点"""

    def __init__(self, val: int):
        """构造方法"""
        self.val: int = val
        self.next: ListNode | None = None  # 后继节点引用
        self.prev: ListNode | None = None  # 前驱节点引用

class LinkedListDeque:
    """基于双向链表实现的双向队列"""

    def __init__(self):
        """构造方法"""
        self._front: ListNode | None = None  # 头节点 front
        self._rear: ListNode | None = None  # 尾节点 rear
        self._size: int = 0  # 双向队列的长度

    def size(self) -> int:
        """获取双向队列的长度"""
        return self._size

    def is_empty(self) -> bool:
        """判断双向队列是否为空"""
        return self.size() == 0

    def push(self, num: int, is_front: bool):
        """入队操作"""
        node = ListNode(num)
        # 若链表为空，则令 front, rear 都指向 node
        if self.is_empty():
            self._front = self._rear = node
        # 队首入队操作
        elif is_front:
            # 将 node 添加至链表头部
            self._front.prev = node
            node.next = self._front
            self._front = node  # 更新头节点
        # 队尾入队操作
        else:
            # 将 node 添加至链表尾部
            self._rear.next = node
            node.prev = self._rear
            self._rear = node  # 更新尾节点
        self._size += 1  # 更新队列长度

    def push_first(self, num: int):
        """队首入队"""
        self.push(num, True)

    def push_last(self, num: int):
        """队尾入队"""
        self.push(num, False)

    def pop(self, is_front: bool) -> int:
        """出队操作"""
        if self.is_empty():
            raise IndexError("双向队列为空")
        # 队首出队操作
        if is_front:
            val: int = self._front.val  # 暂存头节点值
            # 删除头节点
            fnext: ListNode | None = self._front.next
            if fnext != None:
                fnext.prev = None
                self._front.next = None
            self._front = fnext  # 更新头节点
        # 队尾出队操作
        else:
            val: int = self._rear.val  # 暂存尾节点值
            # 删除尾节点
            rprev: ListNode | None = self._rear.prev
            if rprev != None:
                rprev.next = None
                self._rear.prev = None
            self._rear = rprev  # 更新尾节点
        self._size -= 1  # 更新队列长度
        return val

    def pop_first(self) -> int:
        """队首出队"""
        return self.pop(True)

    def pop_last(self) -> int:
        """队尾出队"""
        return self.pop(False)

    def peek_first(self) -> int:
        """访问队首元素"""
        if self.is_empty():
            raise IndexError("双向队列为空")
        return self._front.val

    def peek_last(self) -> int:
        """访问队尾元素"""
        if self.is_empty():
            raise IndexError("双向队列为空")
        return self._rear.val

    def to_array(self) -> list[int]:
        """返回数组用于打印"""
        node = self._front
        res = [0] * self.size()
        for i in range(self.size()):
            res[i] = node.val
            node = node.next
        return res

```

## 基于数组的实现

实际上是一个环形数组，头回到尾部，尾部回到头部

```python
class ArrayDeque:
    """基于环形数组实现的双向队列"""

    def __init__(self, capacity: int):
        """构造方法"""
        self._nums: list[int] = [0] * capacity
        self._front: int = 0
        self._size: int = 0

    def capacity(self) -> int:
        """获取双向队列的容量"""
        return len(self._nums)

    def size(self) -> int:
        """获取双向队列的长度"""
        return self._size

    def is_empty(self) -> bool:
        """判断双向队列是否为空"""
        return self._size == 0

    def index(self, i: int) -> int:
        """计算环形数组索引"""
        # 通过取余操作实现数组首尾相连
        # 当 i 越过数组尾部后，回到头部
        # 当 i 越过数组头部后，回到尾部
        return (i + self.capacity()) % self.capacity()

    def push_first(self, num: int):
        """队首入队"""
        if self._size == self.capacity():
            print("双向队列已满")
            return
        # 队首指针向左移动一位
        # 通过取余操作，实现 front 越过数组头部后回到尾部
        self._front = self.index(self._front - 1)
        # 将 num 添加至队首
        self._nums[self._front] = num
        self._size += 1

    def push_last(self, num: int):
        """队尾入队"""
        if self._size == self.capacity():
            print("双向队列已满")
            return
        # 计算尾指针，指向队尾索引 + 1
        rear = self.index(self._front + self._size)
        # 将 num 添加至队尾
        self._nums[rear] = num
        self._size += 1

    def pop_first(self) -> int:
        """队首出队"""
        num = self.peek_first()
        # 队首指针向后移动一位
        self._front = self.index(self._front + 1)
        self._size -= 1
        return num

    def pop_last(self) -> int:
        """队尾出队"""
        num = self.peek_last()
        self._size -= 1
        return num

    def peek_first(self) -> int:
        """访问队首元素"""
        if self.is_empty():
            raise IndexError("双向队列为空")
        return self._nums[self._front]

    def peek_last(self) -> int:
        """访问队尾元素"""
        if self.is_empty():
            raise IndexError("双向队列为空")
        # 计算尾元素索引
        last = self.index(self._front + self._size - 1)
        return self._nums[last]

    def to_array(self) -> list[int]:
        """返回数组用于打印"""
        # 仅转换有效长度范围内的列表元素
        res = []
        for i in range(self._size):
            res.append(self._nums[self.index(self._front + i)])
        return res

```

