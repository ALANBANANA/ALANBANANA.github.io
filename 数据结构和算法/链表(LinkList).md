# 链表(LinkList)

## Day 1 链表

### 链表的定义---->以线性列表为例

> 链表(Linked List): 线性数据结构，有__存储单元组__(可连续，可不连续)，其中存储的数据具有相同的类型，除了存储数据之外，还存储指针也作为数据，一个节点存储着**数据**以及**指针**

![img](https://datawhalechina.github.io/leetcode-notes/images/20211208180037.png)

在上面的图中，链表通过将一组任意的存储单元串联。链节点当中为一个数据元素，而链表的链结点结合在一起则代表数据，数据分开存储在链表的每一个节点里。至于一个数据存放的逻辑关系则通过后继数据元素的RAM地址也存放在一个链节点当中--->为**后继指针next**

### 链表优缺点

| 优点     | 存储空间不用事先分配，可临时申请减少浪费，在插入、移动、删除元素上效率高 |
| -------- | ------------------------------------------------------------ |
| **缺点** | **元素本身占用空间之外，指针也需要，链表结构比数组结构占用空间更大** |

 ### 链表类型

#### 1. 双向链表

> 双向链表：双方指针，双链表，两头相向所指

特点：从任意一个节点开始，很方便访问**前驱节点**和**后继节点**

![img](https://datawhalechina.github.io/leetcode-notes/images/20211208103220.png)

#### 2. 循环链表

> 循环列表：最后一个链节点又指向头节点，形成闭环

特点：从循环链表的任何一个节点都可以访问任意别的节点

![img](https://datawhalechina.github.io/leetcode-notes/images/20211208180048.png)

### 列表的基本操作：增删查改

#### 1. 先建立一个列表的类

```python
"""链结点类"""
class ListNode:
    def __init__(self, val=0, next=0):
        self.val = val
        self.next = next

"""链表类"""
class LinkedList:
    def __init__(self):
        self.head = None  # ---->指向为空
```

**注释：在有头节点的情况之下，head通常指向第一个元素，作用在于在第一个位置和其他位置操作上的统一，至于有无头节点的讨论：如果删除某一个节点链表仍未正常，若没有头节点又删除最后一个节点，链表容易为空**

#### 2. 建立描述链表的方法

```python
    def create(self, data):
        """线性链表建立，cur = cur.next指针域传递"""
        self.head = ListNode(0)  # 指定了头节点
        cur = self.head
        for i in range(len(data)):
            node = ListNode(data[i])  # 链表传递过程---|
            cur.next = node  # 节点传递---------------|------>数据域
            cur = cur.next
```

#### 3. 描述链表长度的方法

```python
    def length(self):
        """描述链表长度"""
        counts = 0
        cur = self.head
        while cur:  # ---->直至cur指到为空为止
            counts += 1
            cur =cur.next
        """假设有链表之中有n个元素那么在链表进行运行当中则有
        在时间复杂度O(n)上为线性"""

        return counts
```

#### 4. **查**询列表当中的元素

```python
    def find(self, val):
        """查找元素"""
        cur = self.head
        while cur:  # 假设数据有n个元素，时间复杂度为O(n), 运行n次
            if val == cur.val:  # val为当前链表节点的元素
                return cur  # 返回当前所查找的链表元素
            cur = cur.next
        return None
```

#### 5. **增**加链表当中的节点(三个位置的方法描述)

```python
    def insert_front(self, val):
        """头部插入元素，并将指针指向头部"""
        node = self.head
        node.next = self.head
        self.head = node  # 时间复杂度上为O(1)

    def insert_tail(self, val):
        """链表尾部插入元素"""
        node = ListNode(val)
        cur = self.head
        while cur.next:  # O(n)
            cur = cur.next
        cur.next = node

    def insert_inside(self, val, index):
        """在链表中间插入元素"""
        cur = self.head
        counts = 0
        while cur and counts < index - 1:  # 在链表中循环直到循环到index位置 平均时间复杂度O(i)
            counts += 1  # index-1,插入位置为index，则先知道index-1的元素
            cur = cur.next  # 原来的链表上的元素数据

        if not cur:
            return 'Error'

        node = ListNode(val)  # 创建新的节点元素满足其术语在链结点类里面
        node.next = cur.next  # 使得下一个节点为上面的原来的数据的下一个节点
        cur.next = node  # 再另上一个的节点转回为新产生的node
```

#### 6. **删**除链表当中的相关节点(三个位置的描述)

```py
    def delete_front(self):
        """删除头部元素"""
        if self.head:
            cur = self.head
            self.head = cur.next

    def delete_tail(self):
        """删除尾部元素"""
        if not self.head:
            return 'Error'
        cur = self.head
        while cur.next.next:  # n-2 时间复杂度取最高此n--->O(n),且最后一项之后实际为None
            cur = cur.next
        cur.next = None

    def delete_inside(self, index):
        """删除中间元素"""
        counts = 0
        cur = self.head
        while cur.next and counts < index - 1:  # 按照索引，假如索引至i所以为O(i)
            counts += 1  # 实际是循环至cur.net之后停止，进行删除元素节点
            cur = cur.next

        if not cur:
            return 'Error'

        del_node = cur.next  # 要删除的实际为索引-1那个
        cur.next = del_node.next  # 新的下一个为删除的再下一个
```

#### 7. **修**改元素和节点

```python
    def change(self, index, val):
        """改变链表中的元素"""
        counts = 0
        cur = self.head
        while cur and counts < index:  # 循环至指针为index的位置就改index位置上元素
            counts += 1  # cur---->index
            cur = cur.next

        if not cur:
            return 'Error'

        cur.val = val  # 改变链表类所需位置的元素
```



## Day 2 关于我的一些做题的理解

### [328. 奇偶链表 - 力扣（LeetCode）](https://leetcode.cn/problems/odd-even-linked-list/)

```python
class Solution:
    def oddEvenList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head:
            return head
        odd = head  # 将指针指向头节点，即第一个节点
        newhead = head.next  # 第二个指针指向第二个节点
        even = newhead
        while odd.next and even.next:  # 因为要将偶数节点的头节点放在奇数节点屁股，到后面即为空
            odd.next = odd.next.next
            even.next = even.next.next
            odd = odd.next
            even = even.next
        odd.next = newhead  # 将奇数节点链表尾部接到偶数节点的第一个
        return head  # 此时head即为奇偶头接尾的链表
```

### [027. 回文链表 - 力扣（LeetCode）](https://leetcode.cn/problems/aMhZSa/description/)

**双指针**一快一慢的解法

```python
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        if not head:
            return head
        
        fast = head
        slow = head
        while fast.next and fast.next.next:  # 双指针，一快一慢，fast是slow行走的两倍，这循环一般用来找中点
            fast = fast.next.next
            slow = slow.next  # slow才走一段


        pre = None
        cur = slow.next  # 这里slow已经是整个链表的一半了，所以slow.next是一半后的链表
        while cur:  # 对一半之后的链表进行反转，这里已经是一般之后的链表了
            next_cur = cur.next
            cur.next = pre
            pre = cur
            cur = next_cur

        p1 = head
        p2 = pre
        while p2:  # 遍历后半部分的链表
            if p1.val != p2.val:
                return False
            p1 = p1.next
            p2 = p2.next
        return True
```



## Day 3 链表排序

数组当中有许多排序算法，但对于链表排序来说，每一次访问要根据开始，对后面的节点只可以依靠next从头部节点往后进行遍历，所以相较于数组排序来说链表更加复杂一下。

**适合链表排序的算法：**冒泡排序、选择排序、**插入排序**、**归并排序**、快速排序、计数排序、桶排序、基数排序

**不适合链表的排序：**希尔排序

**可用于链表但不建议使用的排序：**堆排序

### 3.1 链表的插入排序

1. 使用哑节点dummy_head指向head的指针，则链表可以从head遍历
2. 维护sorted_list为链表已经排序部分的最后一个节点，初始时sorted_list=head。
3. 维护prev为插入元素位置的前一个节点，维护cur为待插入元素，初始时prev=head，cur=head.next
4. 比较sorted_list和cur的节点值
   * 假如sorted_list.val <= cur.val，说明cur应该插入到sort_list之后，则将sorted_list后移动一项
   * 如果sorted_list.val > cur.val，说明cur应该插入head与sorted_list之间。则使用prev从head开始遍历，直到找到插入cur的位置的前一个节点位置。然后将cur进行插入
5. 令cur = sorted_list.next，当时cur为下一个待插入元素
6. 重复4、5步骤，直到cur遍历结束为空。返回dummy_head的下一个节点

**代码实现**

```python
class Solution:
    def insertionSort(self, head: ListNode):
        if not head or not head.next:
            return head
        
        dummy_head = ListNode(-1)
        dummy_head.next = head
        sorted_list = head
        cur = head.next 
        
        while cur:  # O(n) -----> O(n^2)
            if sorted_list.val <= cur.val:
                # 将 cur 插入到 sorted_list 之后
                sorted_list = sorted_list.next 
            else:
                prev = dummy_head
                while prev.next.val <= cur.val:  # O(n)
                    prev = prev.next
                # 将 cur 到链表中间
                sorted_list.next = cur.next
                cur.next = prev.next
                prev.next = cur
            cur = sorted_list.next 
        
        return dummy_head.next

    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        return self.insertionSort(head)

```

### 3.2 链表归并排序

1. 分割环节：找到链表中心链结点位置，从中心节点将链表断开，进行递归分割
   * 使用快慢指针fast=head.next、slow =head，让fast每次移动两步，slow移动1步，fast移动到链表末端，则slow移动到链表中点位置
   * 从中心位置将链表从中心位置进行分割，左边为左链表left_head，右边为右链表right_head，并将其断开，所以slow.next = None
   * 对左右两个链表分别进行递归分割，直到每个链表中只包含一个链节点
2. 归并环节：将递归后的链表进行两两归并，完成一遍后每个子链表长度倍增。重复操作至得到完整链表
   * 使用哑节点dummy_head构造一个头节点，并使用cur指向dummy_head进行遍历
   * 比较两个链表头节点left和right值的大小。将较小的头节点加入到合并后的链表中，并向后移动该链表的头节点指针
   * 然后重复上一步操作，直到两个链表中出现None的情况
   * 将剩余链表插入到合并的链表当中
   * 将哑节点dummy_head的下一个链节点dummy_head.next作为合并后的头节点

```python
class Solution:
    def insertionSort(self, head: ListNode):
        if not head or not head.next:
            return head
        
        dummy_head = ListNode(-1)  # None
        dummy_head.next = head
        sorted_list = head
        cur = head.next 
        
        while cur:
            if sorted_list.val <= cur.val:
                # 将 cur 插入到 sorted_list 之后
                sorted_list = sorted_list.next 
            else:
                prev = dummy_head
                while prev.next.val <= cur.val:
                    prev = prev.next
                # 将 cur 到链表中间
                sorted_list.next = cur.next
                cur.next = prev.next
                prev.next = cur
            cur = sorted_list.next 
        
        return dummy_head.next

    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        return self.insertionSort(head)

```

## Day 4 链表双指针

> **双指针**：指代在遍历链表元素过程中，不是使用单个指针进行防蚊链表中的元素，而是采用两个指针，1. 如果两个指针方向相反，则称为**对撞指针**。如果两个指针方向相同，则称为**快慢指针**。而两个指针分别属于不同数组/链表，则称为**分离指针**

### 双指针的分类

#### 1. 起点不一致的快慢指针

> 指代两个指针从同一侧出发开始对链表进行遍历，但是两个指针的起点不一致。快指针比满指针先走了n步，直到快指针移动到链表尾端为止

**其适用范围**：起点不一致的快慢指针用于找到链表中倒数第k个节点，删除链表中第n个节点

图解关于起步不一致的指针![24500dce1993188e3873b94da7d50da](C:\Users\DELL\Documents\WeChat Files\wxid_r87uet4wdjgp12\FileStorage\Temp\24500dce1993188e3873b94da7d50da.jpg)

#### 2. 步长不一致的双指针

> 指的是两个指针从同一侧开始遍历链表，两个指针的起点一样，但步长不一致，快**fast**的指针走**两步**，而慢**slow**的指针**只走一步**

求解步骤：

1. 使用两个指针**fast**，**slow**, 同时指向头节点head
2. 慢指针走一步：**slow = slow.next**，快指针走两步：**fast = fast.next.next**
3. 等到**fast指针**即将走到末尾的时候，即fast即将到达链表尾部的时候 

具体应用在回文链表当中

**这是正确的代码**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        if not head:
            return head
        fast = head
        slow = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        
        
        prev = None
        cur = slow
        while cur:
            next_ = cur.next
            cur.next = prev
            prev = cur
            cur = next_
        

        p1 = head
        new_head = prev
        while new_head and p1:
            if p1.val != new_head.val:
                return False
            new_head = new_head.next
            p1 = p1.next
        if head.val == prev.val:
            return True
```

**错误代码**

```python
class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        if not head:
            return head
        fast = head
        slow = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        return slow  # 错误1：如果在这里返回掉slow，此时slow为链表上代表节点的指针，指针指向节点，而slow则为节点，所以不是链表，会导致下面代码完全不运行
        
        prev = None
        cur = slow
        while cur:
            next_ = cur.next
            cur.next = prev
            prev = cur
            cur = next_
        return prev  # 错误2：1.对于代码而言：同理错误1因为这里prev代表的是可以指代数据上的指针，而其实prev已经代表着反转链表的头节点，2.对于题目而言：而关于题目的isPalidrome是一个求解bool型的函数，所以这是不能够返回的值，而且这部分不是判断是否为回文的一部分，这部分的return会干扰正确答案的删除，由此做题是和一般的coding是不一样的

        p1 = head
        new_head = prev
        while new_head and p1:
            if p1.val != new_head.val:
                return False
            new_head = new_head.next
            p1 = p1.next
            return True  # 错误3:这个错误很弱智，比较愚蠢，从迭代的角度来讲，没迭代完就要返回一次…………
```

#### 3. 分离双指针

> 两个指针分别属于不同的链表

**其求解步骤**

1. 使用两个指针left_1、left_2。left_1=list1指向第一个链表头节点，同理第二个一样left_2 = list2
2. 当满足一定的条件时，两个指针同时右移，即left_1 = left_1.next， left_2 = left_2.next
3. 当满足另外一定条件时，将left_1指针右移，left_1 = left_1.next
4. 满足再另一个条件时，left_2也如步骤三一样
5. 最后则是等其中一个链表遍历完以及其他条件满足时退出循环(**and**)

## 关于我在学习链表的感受与总结

* 第一点. 以前我从来没有接触过C语言，所以一点关于指针的知识也没有，第一门接触的编程语言就是Python，Python简单就简单在它的变量赋值很方便，所以基本不用考虑什么很底层的问题

* 第二点. 基于第一点的情况来说，我在刚刚接触组队学习还没进行数组的学习，就接触列表多多少少懵圈，一个节点里面居然可以存储两中数据

* 第三点(以下就是我通过这次学习的知识收获). 

  | 标识符(由变量来看)                  | 代表意思                                                     |
  | ----------------------------------- | ------------------------------------------------------------ |
  | cur、prev(多指代指向前面的指针)、…… | 指针(外指针)，当作是一个变量来处理，而在cur = head之后，通过while对链表进行遍历，这时候cur指针则代表着每一个节点 |
  | next                                | 初始化class LinkNode(定义的是节点类)时的初始化属性，self.next = None |
  | head                                | 头节点、头指针(class LinkList(链表类)中的属性self.head = Linknode())、链表 |
  | cur = head                          | 指代着在在指针指着链表当中的头节点，由于每一个链表都会指向下一个节点，相当于是指针指代了链表每一个节点，而节点里面包含了指针数据和数据值，这里的head就表示着链表(**遍历链表**) |
  | head.next                           | 指的是头节点的下一个节点O->O->O->None(这里的第一个即为头节点，第二个则为head.next) |
  | cur.next                            | 当前节点的下一个节点，指针的节点域                           |
  | cur.val                             | 节点的数值域                                                 |

* 第四点. 在学习数据结构之余我居然忘记关于程序语言的的左至右，上至下的重要底层逻辑！其次在遍历循环的选择要注意需求，求中点则需遍历快指针的速度，还有要输出、或者返回的链表到底是慢指针所指还是快指针所指

* 第五点. 在回文链表中的错误，不断的return slow或者return prev只会返回一个节点，此时的指针所代表的为一个单一节点，而不会在进行链表的传输





