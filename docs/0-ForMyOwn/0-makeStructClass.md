# 创建类 class

## Python

```python
class ListNode:
    def __init__(self, val: int):
        self.val: int = val                # 节点值
        self.next: ListNode | None = None  # 指向后继节点的引用
        self.prev: ListNode | None = None  # 指向前驱节点的引用
```

1. 声明为`class`，没有 `；`只有 `：`。
2. `def __init__`传进去的是 `self 指针`，以及其他构造参数。
3. self.`val: int`，是一个整体，直接 = val。
4. 其余的则是 self.next`:` ListNode。
5. 空值：`None` 

## CPP

```cpp
struct ListNode {
    int val;         // 节点值
    ListNode *next;  // 指向后继节点的指针
    ListNode *prev;  // 指向前驱节点的指针
    ListNode(int x) : val(x), next(nullptr), prev(nullptr) {}  // 构造函数
};
```

1. 开头声明是 `struct`。

   1. 定义处最后，也要加一个`；`。

2. 指针类型：结构体 `*`名称。

3. 构造函数简写成`：`，填充参数值`名称（）`，然后直接 `{}`。

4. 空值：`nullptr` 

   

## Java

```java
class ListNode {
    int val;        // 节点值
    ListNode next;  // 指向后继节点的引用
    ListNode prev;  // 指向前驱节点的引用
    ListNode(int x) { val = x; }  // 构造函数
}
```

1. Java 中没有 * 和 &

## Go

```go
type DoublyListNode struct {
    Val  int             // 节点值
    Next *DoublyListNode // 指向后继节点的指针
    Prev *DoublyListNode // 指向前驱节点的指针
}

// NewDoublyListNode 初始化
func NewDoublyListNode(val int) *DoublyListNode {
    return &DoublyListNode{
        Val:  val,
        Next: nil,
        Prev: nil,
    }
}
```

1. `type` 名称 `struct`。
2. *注意大小写*！
3. 结构体中，连`：`都不用。
4. 指针类型：名称 `*`结构体。
5. 初始化 方法/函数
   1. 返回值为指针：`*`结构体（指对象）
   2. 实例化对象：return `&`结构体`{`..`}`（引用，指对象）
      1. 1+2 => *结构体(指针) = &结构体(该对象)
   3. 实例化内容：成员名称`：`赋值
6. 空值：`nil` 

## C

```c
typedef struct ListNode {
    int val;               // 节点值
    struct ListNode *next; // 指向后继节点的指针
    struct ListNode *prev; // 指向前驱节点的指针
} ListNode;

ListNode *newListNode(int val) {
    ListNode *node;
    node = (ListNode *) malloc(sizeof(ListNode));
    node->val = val;
    node->next = NULL;
    node->prev = NULL;
    return node;
}
```

1. `typedef struct` 名称 {
   1. 指针类型：**struct** 声明结构体 `*`名称。
   2. } **名称**+`；`
2. 方法中，指针类型：结构体 `*`名称。
   1. 开辟空间：node = (结构体 *) malloc(sizeof(结构体));
   2. 变量`->`成员 = 赋值;
3. 空值：`NULL` 

# coding

```

```



