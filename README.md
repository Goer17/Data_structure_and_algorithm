# 数据结构与算法



## 数据结构



### 线性结构

#### 线性表

- 顺序表：

  元素在内存中顺序储存，便于查找。

- 链表：

  元素在内存中链式存储，更加灵活，但查找效率低。 

#### 堆栈

> 堆栈是一种先如后出，自顶向下的线性数据结构。
>
> 其有四种常用方法：
> `push(data)` ：将数据压入栈顶
>
> `pop()` ：将栈顶的数据弹出
>
> `top()` : 返回栈顶元素
>
> `isEmpty()` ：判断栈是否为空

其有两种实现方式（数据类型以 `int` 为例）：

- 顺序表实现：

  ```c++
  class Stack {
  private:
  	int* arr;
  
  	int size;
  
  public:
  
  	Stack(void) {
  		arr = new int[MAX_SIZE]();
  		size = 0;
  	}
  
  	void push(int _data) {
  		if (size < MAX_SIZE) {
  			arr[size++] = _data;
  		}
  		else {
  			cout << "Stack overflow !" << endl;
  		}
  	}
  
  	void pop(void) {
  		if (size > 0) {
  			arr[size--] = 0;
  		}
  		else {
  			cout << "Stack Empty !" << endl;
  		}
  	}
  
  	int top(void) {
  		if (size > 0) {
  			return arr[size - 1];
  		}
  		else {
  			cout << "Stack Empty !" << endl;
  			return 0;
  		}
  	}
  
  	bool isEmpty(void) {
  		return size == 0;
  	}
  };
  ```

- 链表实现：

  ```c++
  class Stack {
  private:
  	node* topNode;
  
  public:
  	Stack(void) {
  		topNode = NULL;
  	}
  
  	void push(int _data) {
  		node* p = new node(_data);
  		p->next = topNode;
  		topNode = p;
  	}
  
  	void pop(void) {
  		if (topNode) {
  			node* p = topNode;
  			topNode = topNode->next;
  			delete p;
  			p = NULL;
  		}
  		else {
  			cout << "Stack Empty !" << endl;
  		}
  	}
  
  	int top(void) {
  		return topNode->data;
  	}
  
  	bool isEmpty(void) {
  		return topNode == NULL;
  	}
  
  };
  ```

堆栈的运用：

- **前缀表达式、中缀表达式和后缀表达式**：

  - 中缀表达式：一般的运算表达式书写顺序。
  
    > eg :
    >
    > `a + b , a * (b + c) / d, a + b - c`
  
  - 前缀表达式和后缀表达式：
  
    1. 前缀表达式：先书写二元运算符，再书写两个参与运算的数字。
  
       > eg :
       >
       > `+ a b, / * a + b c d, - + a b c`
       
    1. 后缀表达式：先书写两个参与运算的数字，然后再书写二元运算符。（适合计算机运算）
    
       > eg :
       >
       > `a b +, a b c + * d /, a b + c -`
  
- **函数的调用**：

  函数的调用本身在栈区进行，函数调用结束后栈区的内容会清空，故函数不要返回局部变量的地址。



#### 队列





#### 字符串

**KMP 算法**

```c++
class Solution {
private:
    vector<int> build_next(string needle) {
        // 构造 next 数组
        vector<int> next{ 0 };
        int i = 1, fix_len = 0;
        while (i < needle.size()) {
            if (needle[fix_len] == needle[i]) {
                next.push_back(++fix_len);
                i++;
            }
            else {
                if (fix_len == 0) {
                    next.push_back(0);
                    i++;
                }
                else {
                    fix_len = next[fix_len - 1];
                }
            }
        }

        return next;
    }


public:
    int strStr(string haystack, string needle) {
        vector<int> next = build_next(needle);
        int i = 0, j = 0; // 目标串和模式串的指针
        while (i < haystack.size()) {
            if (haystack[i] == needle[j]) {
                i++;
                j++;
            }
            else {
                if (j == 0) {
                    i++; // 第一个字符就失配
                }
                else {
                    j = next[j - 1];
                }
            }

            if (j == needle.size()) {
                return i - j; // 完全匹配
            }
        }

        return -1;
    }
};
```



### 树结构

#### 树的定义

#### 二叉树

##### 二叉树的存储结构

##### 二叉树的遍历

##### 二叉搜索树







##### 平衡二叉树

- 什么是平衡二叉树？

  > 搜索树结点不同插入次序，将导致不同的**树高度**和**平均查找长度ASL**。
  >
  > **平衡因子**（Balance Factor, 简称 BF）：$$BF(T) = h_{left} - h_{right}$$，即 T 的左子树的高度减去右子树的高度。

  **平衡二叉树**（Balanced Binary Tree），也叫 AVL 树， 指：**空树或者任一结点的平衡因子的绝对值不超过1，即$$|BF(T)| \le 1$$**。

  > 设结点数为$$n$$，则平衡二叉树的高度$$h=O(logn)$$。
  
- 平衡二叉树的调整：

  - RR旋转（右单旋）
  
    <center>
        <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220805125930041.png" alt="image-20220805125930041" style="zoom:50%;" />
    </center>
    
  - LL旋转（左单旋）
  
    <center>
        <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220805130105910.png" alt="image-20220805130105910" style="zoom:50%;" />
    </center>
  
  - LR旋转（左右双旋）
  
    <center>
        <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220805130611835.png" alt="image-20220805130611835" style="zoom:50%;" />
    </center>
  
  - RL旋转（左右双选）
  
    <center>
        <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220805131213574.png" alt="image-20220805131213574" style="zoom:50%;" />
    </center>
    
    

#### 堆

> 优先队列（Priority Queue）：特殊的 ”队列“ ，元素的取出顺序由元素的优先权（关键字）决定。



##### 堆（Heap）的定义

- 结构性：用数组表示的**完全二叉树**；
- 有序性：任一结点的关键字大小是其所有子树关键字大小的最大值（或最小值）。

<center>
    <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220805170523922.png" alt="image-20220805170523922" style="zoom: 33%;" />
    <br>
    优先队列的完全二叉树表示
</center>

以最大堆为例，假设关键字数据类型为 `int` , 其封装代码如下：

```c++
class Heap
{
public:
	int* data; // 储存堆元素的数组
	int size; // 堆当前元素个数
	int capacity; // 堆的最大容量

	Heap(int _capacity); // 构造函数

	Heap(vector<int> arr); // 另一种构造方法，将任意数组构建成最大堆

	void insert(int dataAdd); // 插入数据

	int extract_m(void); // 取走最大值

private:
	
	void percDown(int index); // 将以 index 为下标的子堆调整为最大堆

};
```



初始构造：

```c++
Heap::Heap(int _capacity)
{
	capacity = _capacity;
	size = 0;
	data = new int[capacity + 1];
    data[0] = inf; // data[0]作为哨兵，储存一个足够大的数，比任何插入的数字都大，防止插入大数据时出现无限循环
}
```



##### 堆的插入

> 思路：若新插入的结点关键字大小比父节点大，则与父节点交换位置，以此类推，直到插入位置合适。



代码实现：

```c++
void Heap::insert(int dataAdd)
{
	if (size == capacity) {
		cout << "The heap is full !" << endl;
		return;
	}

	int i = ++size; // i指向插入后堆中的最后一个位置
	while (data[i / 2] < dataAdd) {
		data[i] = data[i / 2];
		i /= 2; // 向下过滤结点
	}
	
	data[i] = dataAdd; // 将数据插入
}
```



##### 取走堆的最值

> 思路：堆的最值一定是堆的顶端，即 `data[1]` ，我们指定最后一个结点关键字大小为 `temp` ，从第一个结点，即 `data[1]` 开始，每次与其较大的子节点交换，再以较大的子节点为父节点继续循环，直到其没有子节点或者该父节点的关键字大小小于 `temp` ，则说明此刻父结点的位置刚好可以为 `temp` ，循环结束。



代码实现：

```c++
int Heap::extract_m(void)
{
	if (size) {
		int maxItem = data[1];
		int parent, child;
		int temp = data[size--];
		for (parent = 1; 2 * parent <= size; parent = child) {
			child = 2 * parent;
			if (child != size && data[child] < data[child + 1]) {
				child++;
			}
			// 得到较大的子结点
			if (temp >= data[child]) {
				break;
			}
			else {
				data[parent] = data[child];
			}
		}
		data[parent] = temp;

		return maxItem;
	}
	else {
        
		return 0;
	}
}
```



##### 堆的建立



- 方法一：使用 `insert()` 方法将数据逐一插入，时间复杂度 $$O(nlogn)$$。

- 方法二：采用分而治之的思想，先将所有数据按照完全二叉树的方式排好，再对其进行构建，从最后一个结点的父结点开始，直到根结点。

  

  代码实现：

  ```c++
  Heap::Heap(vector<int> arr)
  {
  	capacity = arr.size() + 1;
  	size = arr.size();
  	data = new int[capacity];
  	data[0] = inf;
  	for (int i = 1; i < capacity; i++) {
  		data[i] = arr[i - 1]; // 将数组的元素全部放入堆
  	}
  	
  	for (int i = size / 2; i > 0; i--) {
  		percDown(i); // 从最后一个结点的父结点开始不断下滤操作，直到根结点 1
  	}
  }
  
  void Heap::percDown(int index)
  {
  	int parent, child;
  	int temp = data[index];
  
  	for (parent = index; 2 * parent <= size; parent = child) {
  
  		child = 2 * parent;
  		if (child != size && data[child + 1] > data[child]) {
  			child++;
  		}
  		// 得到较大的子结点
  
  		if (temp >= data[child]) {
  			break;
  		}
  		else {
  			data[parent] = data[child];
  		}
  
  	}
  
  	data[parent] = temp;
  }
  ```



#### 并查集



##### 并查集的定义

集合并、查某元素属于某个集合。



##### 储存结构

并查集可以用树结构表示，树的每个结点代表一个集合元素。

<center>
    <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220807171130357.png" alt="image-20220807171130357" style="zoom: 25%;" />
</center>

存储方式可以采用数组：

<center>
    <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220807171749613.png" alt="image-20220807171749613" style="zoom:33%;" />
</center>

> `Data` 表示该结点存储数据；
>
> `Parent` 表示该节点父节点的下标，-1 表示无父节点。



接下来数据类型以 `int` 为例，代码实现：

```c++
typedef struct {
	int data;
	int parent;
}SetType;

class SetArr
{
public:
	SetType* arr; // 存放集合元素的数组
	int maxSize; // 最大存储大小

	SetArr(int _maxSize)
	{
		maxSize = _maxSize;
		arr = new SetType[_maxSize];
		for (int i = 0; i < maxSize; i++) {
			arr[i].parent = -1;
		}
	}
};
```



##### 查找元素所属集合

```c++
int Find(SetArr S, int targetData)
{
	int i;
	for (i = 0; i < S.maxSize; i++) {
		if (S.arr[i].data == targetData) {
			break;
		}
	}

	if (i == S.maxSize) {
		cout << "Not Found !" << endl;
		return -1;
	}
	else {
		while (S.arr[i].parent > 0) {
			i = S.arr[i].parent; // 一步步向上搜索找到数据所属集合
		}

		return i;
	}
}
```



##### 并运算

```c++
void Union(SetArr S, int data_1, int data_2)
{
	int root_1 = Find(S, data_1);
	int root_2 = Find(S, data_2); // 找到两个元素的根结点

	if (root_1 != root_2) {
		S.arr[root_2].parent = root_1;
	}
}
```

> 缺点：
>
> 如果将大集合的根结点并入小集合的根结点，在查找时会造成时间浪费。
>
> 改进：
>
> 修改成员 `parent` 的定义，用于记录该根结点集合元素个数的相反数。



#### 哈夫曼树



> 带权路径长度（$$WPL$$）：设二叉树有n个叶子结点，每个叶子结点带有权值$$w_k$$，从根节点出发到每个叶子结点的长度为$$l_k$$，则每个叶子结点的带权路径长度和就是$$WPL=\sum_{k=1}^n w_k l_k$$。

<center>
    <img src = "https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220811222113074.png" >
    <br>
    如上图，{1, 2, 3, 4, 5} 五个叶结点构造不同的树及其带权路径长度
</center>
***目的：通过调整树结点的结构使带权路径长度最短。***



##### 哈夫曼树的构造

*思路：每次把权值最小的两棵二叉树合并。*





<center>
    <center>
        构造方式以下图为例
    </center>
    <br>
    <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220812174736568.png" alt="image-20220812174736568" style="zoom:20%;" />
    <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220812174902173.png" alt="image-20220812174902173" style="zoom:25%;" />
    <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220812175000435.png" alt="image-20220812175000435" style="zoom:25%;" />
    <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220812175152978.png" alt="image-20220812175152978" style="zoom:25%;" />
    <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220812175217645.png" alt="image-20220812175217645" style="zoom:25%;" />
</center>



代码实现：

> 利用最小堆效率最高

最小堆部分：

```c++
#define inf 10e+9

class TreeNode
{
public:
	int data;
	TreeNode* left;
	TreeNode* right;

	TreeNode(int _data)
	{
		data = _data;
		left = NULL;
		right = NULL;
	}
};

class MinHeap
{
public:
	vector<TreeNode*> heapArr;

	MinHeap(vector<int> arr);

	TreeNode* extract_m(void);

	void insert(TreeNode* node_add);

	int size(void);
};

MinHeap::MinHeap(vector<int> arr)
{
	heapArr.push_back(new TreeNode(-inf));

	for (int i = 0; i < arr.size(); i++) {
		insert(new TreeNode(arr[i]));
	}
}

TreeNode* MinHeap::extract_m(void)
{
	if (heapArr.size() <= 1) {
		return NULL;
	}

	TreeNode* ans = heapArr[1];
	TreeNode* endNode = heapArr[heapArr.size() - 1];
	int parent = 1;
	int child;
	while (2 * parent < heapArr.size()) {
		child = 2 * parent;
		if (child != heapArr.size() - 1 && heapArr[child]->data > heapArr[child + 1]->data) {
			child++;
		}
		if (endNode->data <= heapArr[child]->data) {
			break;
		}
		else {
			heapArr[parent] = heapArr[child];
			parent = child;
		}
	}
	heapArr[parent] = endNode;
	heapArr.pop_back();

	return ans;
}

void MinHeap::insert(TreeNode* node_add)
{
	int _data = node_add->data;
	heapArr.push_back(node_add);

	int p = heapArr.size() - 1;
	while (p / 2 > 0) {
		if (_data < heapArr[p / 2]->data) {
			heapArr[p] = heapArr[p / 2];
			p /= 2;
		}
		else {
			break;
		}
	}

	heapArr[p] = node_add;
}

int MinHeap::size(void)
{
	return heapArr.size() - 1;
}
```

哈夫曼树：

```c++
class HuffmanTree
{
public:

	TreeNode* root;

public:

	HuffmanTree(vector<int> arr);

};

HuffmanTree::HuffmanTree(vector<int> arr)
{
	if (arr.size()) {

		MinHeap heap(arr);

		while (heap.size() >= 2) {
			TreeNode* leftNode = heap.extract_m();
			TreeNode* rightNode = heap.extract_m();

			TreeNode* node_add = new TreeNode(leftNode->data + rightNode->data);
			node_add->left = leftNode;
			node_add->right = rightNode;
			heap.insert(node_add);
		}

		root = heap.extract_m();
	}
	else {
		root = NULL;
	}
}
```



### 图结构

- 一组顶点（Vertex）：表示顶点集合；
- 一组边（Edge）：表示边的集合。

> 边是顶点对：$$(v,w) \in E$$，其中$$v,w \in V$$；
>
> 有向边：$$<v,w>$$，表示从$$v$$指向$$w$$的单行边。

- 顶点的度（degree）：一个点连接的边数；

  对于有向图：

  - 出度：从该点指出去的边数；
  - 入度：指向该点的边数。



#### 图的表示

- 邻接矩阵：

  定义二维数组 `G`， `G[i][j]` 为1说明$$<v_i, v_j>$$是 图`G`的边，为0则说明不是。

  <center>
      <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220816132408276.png" alt="image-20220816132408276" style="zoom:40%;" />
  </center>
  
  
- 邻接表：

  定义指针数组 `G[N]` ，对应矩阵每行一个链表，只存非0元素。

  > 注：
  >
  > 邻接表对稀疏图使用才合算。

  <center>
      <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220816132308264.png" alt="image-20220816132308264" style="zoom:50%;" />
  </center>

  代码实现：

  ```c++
  typedef struct _node{
  	int num; // 顶点的编号
  	struct _node* next; // 记录连接的顶点
  }node;
  
  class Graph
  {
  public:
  	vector<node*> nodeSet; // 顶点集合
  };
  ```

  

#### 图的遍历

##### 深度优先搜索 DFS（Depth First Search）

> 利用栈的思想，类似于树的先序遍历。

伪代码：

```c++
void DFS(Vertex V)
{
    V.isVisited = true; // 该点已经检查过
    for all Vertex w near V {
        if( !w.isVisited ){
            DFS(w); // 检查未被检查的相邻顶点
        }
    }
    
}
```

> 若使用邻接表储存图结构，时间复杂度为$$O(N+E)$$



##### 广度优先搜索 BFS（Breadth First Search）

> 利用队列思想，类似于树的层序遍历。

伪代码：

```c++
void BFS(Vertex V)
{
    queue<Vertex> Q; // 队列储存刚发现的点
    
    V.isVisited = true;
    Q.push(V);
    while Q is not empty {
        U = Q.front;
        Q.pop(); // 队首出队
        for all Vertex w near U {
            if( !w.isVisited ){
                w.isVisted = true;
                Q.push(w);
            }
        } 
    }
    
}
```



#### 寻路算法



##### 无权图的单源最短路

- 利用 BFS 实现：

伪代码：

```c++
int pathLen(Vertex S, Vertex target)
{
    queue<Vertex> Q;
    int dist[NUM_OF_VERTEX] = {inf}; // 定义距离数组，初始化都为无穷大
    Vertex parent[NUM_OF_VERTEX] = {-1}; // 定义上记录每一个顶点上一个顶点编号的数组
    S.isVisited = true;
    dist[S] = 0;
    
    while( !target.isVisited ){
        Vertex U = Q.front();
        Q.pop();
        for all Vertex w near U {
            if( !w.isVisited ){
                w.isVisited = true;
                dist[w] = dist[U] + 1;
                parent[w] = U;
                Q.push(w);
            }
        }
    }
    
    return dist[target];
}
```

> 通过 `parent` 数组回溯即可得到最短路径。



##### 有权图的单源最短路 —— Dijkstra算法

> 前提：边的权值不能是负数。

1. 定义集合 $$S = \{源点s+已经确定最短路径的顶点v_i\}$$；
2. 对于任一未收录的顶点$$v_i$$，定义 `dist[i]` 为 $$s$$到$$v_i$$的最短路径长度，**但该路径只经过集合$$S$$中的顶点**；
3. 每次从未收录的点中选一个 `dist` 数值最小的点收录至集合 $$S$$，然后从新收录的点出发对 `dist` 数组进行更新。

> 其本质就是一种贪心算法。
>
> 时间复杂度：
>
> 方法一：直接扫描 `dist` 数组：$$O(V^2 + E)$$；（对于稠密图效果好）
>
> 方法二：将 `dist` 存储在最小堆中：$$O(E \cdot logV)$$ ；（对于稀疏图效果好）



伪代码：

```c++
int Dijkstra(Vertex S)
{
    collect[NUM_OF_VERTEX] = {false}; // 定义收录集合数组
    
    dist[NUM_OF_VERTEX] = {inf}; // 距离数组
    dist[S] = 0;
    
    while(true){
        V = The Vertex which is not collected and whose dist is min;
        if(dist[V] == inf){
            break;
        }
        collect[V] = true;
        
        for all Vertex w not being collected near V {
            dist[w] = min(dist[w], dist[V] + lenth(V, w)); // 更新dist数组
        }
    }
}
```

> 如果要记录路径，应该再定义数组 `pre[NUM_OF_VERTEX]` 记录每个点的前驱。



##### 有权图的多源最短路 —— Floyd算法

1. 定义二维数组 `distMap` ，`distMap[i][j]` 记录 $$v_i, v_j$$ 两点的最短路径，初始对角元赋值为0，其余全部赋值为边的权值，若两点无连接，则权值为无穷大；

2. 利用循环对 `distMap` 数组进行 $$V$$ 次更新，第 k 次更新后 `distMap[i][j]` 记录$$\{i \rightarrow  \{ l \le k\} \rightarrow j \}$$的最小值。

   ```c++
   distMap[i][j] = min(distMap[i][k] + distMap[k][j], distMap[i][j]); // 第k+1次更新
   ```

> 时间复杂度：$$O(V^3)$$



代码实现：

```c++
int k, i, j;
for(k = 0; k < V; k++){
    for(i = 0; i < V; i++){
        for(j = 0; j < V; j++){
            distMap[i][j] = min(distMap[i][k] + distMap[k][j], distMap[i][j]);
        }
	}
}
```

> 若要记录最短路径，则应该定义二维数组 `path` ，若$$v_i,v_j$$两点相连，`path[i][j]` 初始化为 `i`，否则为 -1，若第 k+1 次更新时有 `distMap[i][k] + distMap[k][j] < distMap[i][j]` ，则 `path[i][j]` 更新为 k，最后通过递归打印出路径。



代码实现：

```c++
void PrintPath(vector<vector<Vertex>>& path, i, j)
{
    // 前提是 v_i, v_j 两点连通
    if(path[i][j] == i){
        cout << i << ' ';
        return;
    }
    
    PrintPath(path, i, path[i][j]);
    PrintPath(path, path[i][j], j);
}
```



#### 最小生成树

- 生成树：包含一个图中全部顶点的树，若一个图有$$V$$个顶点，则其生成树一定有且仅有$$V-1$$条边。利用数学归纳法易证。
- 最小生成树：边的权值之和最小的生成树。



##### Kruskal 算法

- 「Kruskal 算法」是求解「加权无向图」的「最小生成树」的一种算法。

步骤：

1. 将所有边排序，每次取出最小的边加入图内；
2. 若加入该边会产生环，则跳过该边；
3. 直到加入 $$V-1$$ 条边，循环结束。

> 如何判断图是否存在环？
>
> —— 采用并查集
>
> 时间复杂度：$$O(ElogE)$$

以 leetcode 1584 为例：

[连接所有点的最小费用](https://leetcode.cn/leetbook/read/graph/rqdl1d/)

```c++
class UnionFind
{
    
    // 判断是否产生环路

private:
    vector<int> root;
    vector<int> rank;

public:

    UnionFind(int _size)
    {
        for(int i = 0; i < _size; i++){
            root.push_back(i);
            rank.push_back(1);
        }
    }

    int findRoot(int index)
    {
        return root[index] == index ? index : root[index] = findRoot(root[index]); // 状态压缩
    }

    void unionNode(int x, int y)
    {
        int root_x = findRoot(x);
        int root_y = findRoot(y);

        if(root_x == root_y){
            return;
        }

        if(rank[x] > rank[y]){
            root[root_y] = root_x;
        }else if(rank[root_x] < rank[root_y]){
            root[root_x] = root_y; 
        }else{
            root[root_x] = root_y;
            rank[root_x]++; // 同秩合并，秩加一
        }
    }

    bool isConnected(int x, int y)
    {
        return findRoot(x) == findRoot(y);
    }
     
};


class Solution {
public:

    int minCostConnectPoints(vector<vector<int>>& points)
    {
        int total_nums = points.size();
        UnionFind uf(total_nums);

        int sum_cost = 0;

        vector<vector<int>> edge; // {start, end, cost}
        for(int i = 0; i < total_nums - 1; i++){
            for(int j = i + 1; j < total_nums; j++){
                edge.push_back({i, j, abs(points[i][0] - points[j][0]) + abs(points[i][1] - points[j][1])});
            }
        }

        sort(edge.begin(), edge.end(), [](auto& a, auto& b){ return a[2] < b[2]; });

        for(int i = 0; i < edge.size(); i++){
            if(!uf.isConnected(edge[i][0], edge[i][1])){
                uf.unionNode(edge[i][0], edge[i][1]);
                sum_cost += edge[i][2];
            }
        }

        return sum_cost;
    }

};
```





##### Prim 算法

- 「Prim 算法」是求解「加权无向图」的「最小生成树」的另一种算法。

核心：从某个源点开始，让一棵树逐渐长大，有些类似于 Dijkstra 算法。

步骤：

1. 选取图中的任意一点为源点；
2. 设最小生成树结点集合为 $$S$$，初始只包括源点，随后进行 $$V-1$$ 轮循环，每次将与当前树的某个结点距离最短的未收纳点收纳至集合 $$S$$ 直至循环结束，这样我们就得到了一棵最小生成树。

> 若要记录该最小生成树，可以采用并查集的方式。
>
> 时间复杂度：
>
> 普通二叉堆：$$O(ElogV)$$
>
> 斐波那契堆：$$O(E + VlogV)$$









### 哈希表



#### 哈希函数与散列表

利用关于元素特征的映射函数查找某个元素的地址或下标，这样的函数我们称为**哈希函数（Hash Function）**。利用该方式储存元素的数据结构称为**散列表或哈希表（Hash Table）**。

利用哈希函数映射可以使得查找效率接近$$O(1)$$。

eg：

将不同的单词储存进一个散列表，我们定义哈希函数 `h(key) = key[0] - 'a'`；

散列表使用二维数组 `dict[26][2]` 实现，则若在存储单词时没有冲突，则最多存储 $$26 \times 2$$ 个单词，查找效率为 几乎为$$O(1)$$；

> 一个好的散列函数一般考虑以下两个因素：
>
> 1. 计算简单；
> 2. 关键字对应的地址分布相对均匀，能有效减少冲突。
>
> 常用哈希函数：
>
> - 关键字为数字：
>   1. 数字直接取模；
>   2. 平方取中；
>   3. 关键位组合...
> - 关键字为字符串：
>   1. 每一位的 `ASCII` 码相加然后关于表的大小取模；
>   2. 字符位移；



#### 冲突处理方法



##### 开放地址法（Open Addressing）

即一旦产生冲突，就按照某种方式去寻找其他地址。

eg：

设计哈希函数$$h_i(key)=(h(key) + d_i) \quad mod \quad tablesize$$，表示发生第 i 次冲突时 `key` 对应的哈希函数。

$$d_i$$在这里则确定了不同的解决冲突方案：

1. 线性探测：$$d_i = i$$；

   > 缺点：易出现聚集现象。

2. 平方探测：$$d_i = \pm i^2$$；

   > 以增量序列 $$1^2, -1^2, 2^2, -2^2,..., q^2, -q^2$$且$$q \le tablesize/2$$ 循环试探下一个存储地址。
   >
   > **若散列表长度为某个$$4k+3$$的素数时，平方探测法就可以查到整个散列表空间。**

3. 双散列：$$d_i = i \times h_2(key)$$。

   > $$h_2(key)$$ 是另一个散列函数，探测序列组成为：$$h_2(key)、2h_2(key)、3h_2(key)、...$$
   >
   > **注：对任意的 $$key$$，$$h_2(key) \neq 0$$。**

   eg：对于整数的双散列：
   $$
   h(key) = key \quad mod \quad p \\
   h_2(key) = p - (key \quad mod \quad p)
   $$

- **再散列（Rehashing）**

  当散列表元素太多时，查找效率会下降；

  此时可以扩充散列表，但原先所有的散列表元素的地址都要重新计算。



##### 分离链表法（Separate Chaining）

即将相应位置上冲突的所有关键字储存在同一个单链表中。

eg：

<center>
    <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220823104719648.png" alt="image-20220823104719648" style="zoom: 33%;" />
</center>



#### 散列表的性能分析

- 平均查找长度（ASL）用来度量散列表查找效率；

- 关键词的比较次数，取决于产生冲突的多少，影响产生冲突的多少，有以下三个因素：

  1. 散列函数是否均匀；
  2. 处理冲突的方法；
  3. 散列表的填装因子$$\alpha$$（即散列表填装元素的密度）。

  <center>
      <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220823111419929.png" alt="image-20220823111419929" style="zoom:25%;" />
      <br>
      <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220823111513284.png" alt="image-20220823111513284" style="zoom:25%;" />
  </center>
  
  

  期望探测次数和填装因子的关系：

  <center>
      <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220823112358967.png" alt="image-20220823112358967" style="zoom:33%;" />
  </center>

  对于分离链表法，其期望探测次数 p 与装填因子 $$\alpha$$ 的关系如下：

  <center>
      <img src="https://typora-1313035735.cos.ap-nanjing.myqcloud.com/img/image-20220823112926234.png" alt="image-20220823112926234" style="zoom:33%;" />
  </center>
  
  

