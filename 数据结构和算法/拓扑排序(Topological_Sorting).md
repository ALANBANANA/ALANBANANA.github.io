# 拓扑排序(Topological Sorting)

## 定义

> 一种对有向无环图(DAG)的所有顶点进行线性排序的方法，使得图中任意一点u和v，如果存在有向边<u, v>，则u必须在v之前出现。对有向图进行拓扑排序产生的线性序列陈伟满足拓扑次序的序列

**图的拓扑排序是针对有向无环图(DAG)来说的，无向图和有向有环图没有拓扑排序，或者说不存在拓扑排序**

![img](https://datawhalechina.github.io/leetcode-notes/images/ch02/02.06.01-001.png)

上述图中的有向无环图当中，拓扑序列不止一个

其实从这个图这个方法在社区leetcode的笔记本记的太过于专业，以至于我看不懂

实际就是以v1为开始，因为v1指向了连个，所以先去掉v1，然后看到v2和v3，v2指的更多，于是v2删除再到v3，依此类推下去，实际就是不断的把优先多指向的直接越发删去，所以顺序就是1-2-3-4-5-6或者1-2-3-4-6-5，所谓的入度即就是v1，v1入度为0，而把v1删除后就变成v2入度为0

## 基于Kahn算法的实现

> 基本思想：
>
> 1. 不断寻找有向图中入度为0的顶点，将其输出
> 2. 然后删除入度为0的顶点和从该顶点出发的向边
> 3. 重复上述操作直到图为空，或者找不到入度为0的节点

**相关的步骤**

1. 使用一个数组用于记录v1的入度
2. 维护一个入度为0的顶点集合S
3. 每次从集合中选择任何一个没有前驱(即入度为0)的顶点u，将其输出道拓扑序列order中
4. 从图中删除该顶点(相当于遍历过)，并且删除从该顶点出发的有向边<u, >v(也就是把该顶点入度都减1)。如果删除该边后顶点v的入度变为0，则将顶点v放入集合S中
5. 重复上述过程，直到集合S为空，或者途中顶点还未被访问，则还有环路，无法形成拓扑序列
6. 不存在环路，则order中顶点中的顺序就是拓扑排序的结果

```python
import collections

class Solution:
    # 拓扑排序，graph 中包含所有顶点的有向边关系（包括无边顶点）
    def topologicalSortingKahn(self, graph: dict):
        indegrees = {u: 0 for u in graph}   # indegrees 用于记录所有顶点入度
        for u in graph:
            for v in graph[u]:
                indegrees[v] += 1           # 统计所有顶点入度
        
        # 将入度为 0 的顶点存入集合 S 中
        S = collections.deque([u for u in indegrees if indegrees[u] == 0])
        order = []                          # order 用于存储拓扑序列
        
        while S:
            u = S.pop()                     # 从集合中选择一个没有前驱的顶点 0
            order.append(u)                 # 将其输出到拓扑序列 order 中
            for v in graph[u]:              # 遍历顶点 u 的邻接顶点 v
                indegrees[v] -= 1           # 删除从顶点 u 出发的有向边
                if indegrees[v] == 0:       # 如果删除该边后顶点 v 的入度变为 0
                    S.append(v)             # 将其放入集合 S 中
        
        if len(indegrees) != len(order):    # 还有顶点未遍历（存在环），无法构成拓扑序列
            return []
        return order                        # 返回拓扑序列
    
    
    def findOrder(self, n: int, edges):
        # 构建图
        graph = dict()
        for i in range(n):
            graph[i] = []
            
        for u, v in edges:
            graph[u].append(v)
            
        return self.topologicalSortingKahn(graph)

```



## 基于深度优先搜索实现拓扑排序

> 1. 对于一个顶点u，DFS先遍历从该顶点出发的有向边<u, v>。如果从该顶点u出发的所有相邻顶点v已经搜索完毕，则回溯到顶点u，该顶点u应该位于其所有相邻顶点v的前面
> 2. 如此一来，当每一个遍历完然后放入栈中，直至栈顶元素的序列即为一种拓扑排序

**基本步骤**

1. 使用一个集合代表已经遍历过的点
2. 使用集合Onstack记录同一次深度优先搜索，表达当前顶点是否被访问过，如果已经被访问，则无法存在环路，无法构成拓扑排序
3. 利用一个布尔变量验证是否有环
4. 从一个未被访问的点出发，如果顶点在同一次被访问过即有环，当前顶点被访问
5. 将顶点u标记为被访问过，并在本次深度优先搜索中标记为访问过，然后开始遍历有向边
6. 当前顶点被访问过，回溯记录当前节点u(将当前节点u输出到拓扑序列order中)
7. 取消这一次的DFS，顶点u的标记访问
8. 对其他未被访问的顶点重复4-7步过程，直到所有节点都遍历完，或者出现环
9. 不存在环路，则将order逆序排序，顶点顺序就是拓扑排序结果

```python
import collections

class Solution:
    # 拓扑排序，graph 中包含所有顶点的有向边关系（包括无边顶点）
    def topologicalSortingDFS(self, graph: dict):
        visited = set()                     # 记录当前顶点是否被访问过
        onStack = set()                     # 记录同一次深搜时，当前顶点是否被访问过
        order = []                          # 用于存储拓扑序列
        hasCycle = False                    # 用于判断是否存在环
        
        def dfs(u):
            nonlocal hasCycle
            if u in onStack:                # 同一次深度优先搜索时，当前顶点被访问过，说明存在环
                hasCycle = True
            if u in visited or hasCycle:    # 当前节点被访问或者有环时直接返回
                return
            
            visited.add(u)                  # 标记节点被访问
            onStack.add(u)                  # 标记本次深搜时，当前顶点被访问
    
            for v in graph[u]:              # 遍历顶点 u 的邻接顶点 v
                dfs(v)                      # 递归访问节点 v
                    
            order.append(u)                 # 后序遍历顺序访问节点 u
            onStack.remove(u)               # 取消本次深搜时的 顶点访问标记
        
        for u in graph:
            if u not in visited:
                dfs(u)                      # 递归遍历未访问节点 u
        
        if hasCycle:                        # 判断是否存在环
            return []                       # 存在环，无法构成拓扑序列
        order.reverse()                     # 将后序遍历转为拓扑排序顺序
        return order                        # 返回拓扑序列
    
    def findOrder(self, n: int, edges):
        # 构建图
        graph = dict()
        for i in range(n):
            graph[i] = []
        for v, u in edges:
            graph[u].append(v)
        
        return self.topologicalSortingDFS(graph)
```

## 资料来源

1. [开源内容]<https://github.com/datawhalechina/leetcode-notes/blob/main/docs/ch02/index.md>
2. [电子网站]<https://datawhalechina.github.io/leetcode-notes/#/ch02/index.md>
3. [hello算法]<https://www.hello-algo.com/>

