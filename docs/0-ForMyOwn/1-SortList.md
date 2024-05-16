# 可排序列表 SortList

## Python

```python
class MyList:
    """列表类"""
    def __init__(self):
        """构造方法"""
        self._capacity: int = 10  # 列表容量
        self._arr: list[int] = [0] * self._capacity  # 数组（存储列表元素）
        self._size: int = 0  # 列表长度（当前元素数量）
        self._extend_ratio: int = 2  # 每次列表扩容的倍数

    def size(self) -> int:
        """获取列表长度（当前元素数量）"""
        return self._size

    def capacity(self) -> int:
        """获取列表容量"""
        return self._capacity

    def get(self, index: int) -> int:
        """访问元素"""
        # 索引如果越界，则抛出异常，下同
        if index < 0 or index >= self._size:
            raise IndexError("索引越界")
        return self._arr[index]

    def set(self, num: int, index: int):
        """更新元素"""
        if index < 0 or index >= self._size:
            raise IndexError("索引越界")
        self._arr[index] = num

    def add(self, num: int):
        """在尾部添加元素"""
        # 元素数量超出容量时，触发扩容机制
        if self.size() == self.capacity():
            self.extend_capacity()
        self._arr[self._size] = num
        self._size += 1

    def insert(self, num: int, index: int):
        """在中间插入元素"""
        if index < 0 or index >= self._size:
            raise IndexError("索引越界")
        # 元素数量超出容量时，触发扩容机制
        if self._size == self.capacity():
            self.extend_capacity()
        # 将索引 index 以及之后的元素都向后移动一位
        for j in range(self._size - 1, index - 1, -1):
            self._arr[j + 1] = self._arr[j]
        self._arr[index] = num
        # 更新元素数量
        self._size += 1

    def remove(self, index: int) -> int:
        """删除元素"""
        if index < 0 or index >= self._size:
            raise IndexError("索引越界")
        num = self._arr[index]
        # 将索引 index 之后的元素都向前移动一位
        for j in range(index, self._size - 1):
            self._arr[j] = self._arr[j + 1]
        # 更新元素数量
        self._size -= 1
        # 返回被删除的元素
        return num

    def extend_capacity(self):
        """列表扩容"""
        # 新建一个长度为原数组 _extend_ratio 倍的新数组，并将原数组复制到新数组
        self._arr = self._arr + [0] * self.capacity() * (self._extend_ratio - 1)
        # 更新列表容量
        self._capacity = len(self._arr)

    def to_array(self) -> list[int]:
        """返回有效长度的列表"""
        return self._arr[: self._size]
```

1. 声明为`class`，没有 `；`只有 `：`。
2. `def __init__`传进去的是 `self 指针`，以及其他构造参数。
3. self.`val: int`，是一个整体，直接 = val。
4. 其余的则是 self.next`:` ListNode。
5. 空值：`None` 

## CPP

```cpp
/* 列表类 */
class MyList {
  private:
    int *arr;             // 数组（存储列表元素）
    int arrCapacity = 10; // 列表容量
    int arrSize = 0;      // 列表长度（当前元素数量）
    int extendRatio = 2;   // 每次列表扩容的倍数

  public:
    /* 构造方法 */
    MyList() {
        arr = new int[arrCapacity];
    }

    /* 析构方法 */
    ~MyList() {
        delete[] arr;
    }

    /* 获取列表长度（当前元素数量）*/
    int size() {
        return arrSize;
    }

    /* 获取列表容量 */
    int capacity() {
        return arrCapacity;
    }

    /* 访问元素 */
    int get(int index) {
        // 索引如果越界，则抛出异常，下同
        if (index < 0 || index >= size())
            throw out_of_range("索引越界");
        return arr[index];
    }

    /* 更新元素 */
    void set(int index, int num) {
        if (index < 0 || index >= size())
            throw out_of_range("索引越界");
        arr[index] = num;
    }

    /* 在尾部添加元素 */
    void add(int num) {
        // 元素数量超出容量时，触发扩容机制
        if (size() == capacity())
            extendCapacity();
        arr[size()] = num;
        // 更新元素数量
        arrSize++;
    }

    /* 在中间插入元素 */
    void insert(int index, int num) {
        if (index < 0 || index >= size())
            throw out_of_range("索引越界");
        // 元素数量超出容量时，触发扩容机制
        if (size() == capacity())
            extendCapacity();
        // 将索引 index 以及之后的元素都向后移动一位
        for (int j = size() - 1; j >= index; j--) {
            arr[j + 1] = arr[j];
        }
        arr[index] = num;
        // 更新元素数量
        arrSize++;
    }

    /* 删除元素 */
    int remove(int index) {
        if (index < 0 || index >= size())
            throw out_of_range("索引越界");
        int num = arr[index];
        // 将索引 index 之后的元素都向前移动一位
        for (int j = index; j < size() - 1; j++) {
            arr[j] = arr[j + 1];
        }
        // 更新元素数量
        arrSize--;
        // 返回被删除的元素
        return num;
    }

    /* 列表扩容 */
    void extendCapacity() {
        // 新建一个长度为原数组 extendRatio 倍的新数组
        int newCapacity = capacity() * extendRatio;
        int *tmp = arr;
        arr = new int[newCapacity];
        // 将原数组中的所有元素复制到新数组
        for (int i = 0; i < size(); i++) {
            arr[i] = tmp[i];
        }
        // 释放内存
        delete[] tmp;
        arrCapacity = newCapacity;
    }

    /* 将列表转换为 Vector 用于打印 */
    vector<int> toVector() {
        // 仅转换有效长度范围内的列表元素
        vector<int> vec(size());
        for (int i = 0; i < size(); i++) {
            vec[i] = arr[i];
        }
        return vec;
    }
};
```

1. 开头声明是 `struct`。

   1. 定义处最后，也要加一个`；`。

2. 指针类型：结构体 `*`名称。

3. 构造函数简写成`：`，填充参数值`名称（）`，然后直接 `{}`。

4. 空值：`nullptr` 

   

## Java

```java
/* 列表类 */
class MyList {
    private int[] arr; // 数组（存储列表元素）
    private int capacity = 10; // 列表容量
    private int size = 0; // 列表长度（当前元素数量）
    private int extendRatio = 2; // 每次列表扩容的倍数

    /* 构造方法 */
    public MyList() {
        arr = new int[capacity];
    }

    /* 获取列表长度（当前元素数量） */
    public int size() {
        return size;
    }

    /* 获取列表容量 */
    public int capacity() {
        return capacity;
    }

    /* 访问元素 */
    public int get(int index) {
        // 索引如果越界，则抛出异常，下同
        if (index < 0 || index >= size)
            throw new IndexOutOfBoundsException("索引越界");
        return arr[index];
    }

    /* 更新元素 */
    public void set(int index, int num) {
        if (index < 0 || index >= size)
            throw new IndexOutOfBoundsException("索引越界");
        arr[index] = num;
    }

    /* 在尾部添加元素 */
    public void add(int num) {
        // 元素数量超出容量时，触发扩容机制
        if (size == capacity())
            extendCapacity();
        arr[size] = num;
        // 更新元素数量
        size++;
    }

    /* 在中间插入元素 */
    public void insert(int index, int num) {
        if (index < 0 || index >= size)
            throw new IndexOutOfBoundsException("索引越界");
        // 元素数量超出容量时，触发扩容机制
        if (size == capacity())
            extendCapacity();
        // 将索引 index 以及之后的元素都向后移动一位
        for (int j = size - 1; j >= index; j--) {
            arr[j + 1] = arr[j];
        }
        arr[index] = num;
        // 更新元素数量
        size++;
    }

    /* 删除元素 */
    public int remove(int index) {
        if (index < 0 || index >= size)
            throw new IndexOutOfBoundsException("索引越界");
        int num = arr[index];
        // 将将索引 index 之后的元素都向前移动一位
        for (int j = index; j < size - 1; j++) {
            arr[j] = arr[j + 1];
        }
        // 更新元素数量
        size--;
        // 返回被删除的元素
        return num;
    }

    /* 列表扩容 */
    public void extendCapacity() {
        // 新建一个长度为原数组 extendRatio 倍的新数组，并将原数组复制到新数组
        arr = Arrays.copyOf(arr, capacity() * extendRatio);
        // 更新列表容量
        capacity = arr.length;
    }

    /* 将列表转换为数组 */
    public int[] toArray() {
        int size = size();
        // 仅转换有效长度范围内的列表元素
        int[] arr = new int[size];
        for (int i = 0; i < size; i++) {
            arr[i] = get(i);
        }
        return arr;
    }
}
```

1. Java 中没有 * 和 &

## Go

```go
/* 列表类 */
type myList struct {
    arrCapacity int
    arr         []int
    arrSize     int
    extendRatio int
}

/* 构造函数 */
func newMyList() *myList {
    return &myList{
        arrCapacity: 10,              // 列表容量
        arr:         make([]int, 10), // 数组（存储列表元素）
        arrSize:     0,               // 列表长度（当前元素数量）
        extendRatio: 2,               // 每次列表扩容的倍数
    }
}

/* 获取列表长度（当前元素数量） */
func (l *myList) size() int {
    return l.arrSize
}

/*  获取列表容量 */
func (l *myList) capacity() int {
    return l.arrCapacity
}

/* 访问元素 */
func (l *myList) get(index int) int {
    // 索引如果越界，则抛出异常，下同
    if index < 0 || index >= l.arrSize {
        panic("索引越界")
    }
    return l.arr[index]
}

/* 更新元素 */
func (l *myList) set(num, index int) {
    if index < 0 || index >= l.arrSize {
        panic("索引越界")
    }
    l.arr[index] = num
}

/* 在尾部添加元素 */
func (l *myList) add(num int) {
    // 元素数量超出容量时，触发扩容机制
    if l.arrSize == l.arrCapacity {
        l.extendCapacity()
    }
    l.arr[l.arrSize] = num
    // 更新元素数量
    l.arrSize++
}

/* 在中间插入元素 */
func (l *myList) insert(num, index int) {
    if index < 0 || index >= l.arrSize {
        panic("索引越界")
    }
    // 元素数量超出容量时，触发扩容机制
    if l.arrSize == l.arrCapacity {
        l.extendCapacity()
    }
    // 将索引 index 以及之后的元素都向后移动一位
    for j := l.arrSize - 1; j >= index; j-- {
        l.arr[j+1] = l.arr[j]
    }
    l.arr[index] = num
    // 更新元素数量
    l.arrSize++
}

/* 删除元素 */
func (l *myList) remove(index int) int {
    if index < 0 || index >= l.arrSize {
        panic("索引越界")
    }
    num := l.arr[index]
    // 将索引 index 之后的元素都向前移动一位
    for j := index; j < l.arrSize-1; j++ {
        l.arr[j] = l.arr[j+1]
    }
    // 更新元素数量
    l.arrSize--
    // 返回被删除的元素
    return num
}

/* 列表扩容 */
func (l *myList) extendCapacity() {
    // 新建一个长度为原数组 extendRatio 倍的新数组，并将原数组复制到新数组
    l.arr = append(l.arr, make([]int, l.arrCapacity*(l.extendRatio-1))...)
    // 更新列表容量
    l.arrCapacity = len(l.arr)
}

/* 返回有效长度的列表 */
func (l *myList) toArray() []int {
    // 仅转换有效长度范围内的列表元素
    return l.arr[:l.arrSize]
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
/* 列表类 */
typedef struct {
    int *arr;        // 数组（存储列表元素）
    int capacity;    // 列表容量
    int size;        // 列表大小
    int extendRatio; // 列表每次扩容的倍数
} MyList;

/* 构造函数 */
MyList *newMyList() {
    MyList *nums = malloc(sizeof(MyList));
    nums->capacity = 10;
    nums->arr = malloc(sizeof(int) * nums->capacity);
    nums->size = 0;
    nums->extendRatio = 2;
    return nums;
}

/* 析构函数 */
void delMyList(MyList *nums) {
    free(nums->arr);
    free(nums);
}

/* 获取列表长度 */
int size(MyList *nums) {
    return nums->size;
}

/* 获取列表容量 */
int capacity(MyList *nums) {
    return nums->capacity;
}

/* 访问元素 */
int get(MyList *nums, int index) {
    assert(index >= 0 && index < nums->size);
    return nums->arr[index];
}

/* 更新元素 */
void set(MyList *nums, int index, int num) {
    assert(index >= 0 && index < nums->size);
    nums->arr[index] = num;
}

/* 在尾部添加元素 */
void add(MyList *nums, int num) {
    if (size(nums) == capacity(nums)) {
        extendCapacity(nums); // 扩容
    }
    nums->arr[size(nums)] = num;
    nums->size++;
}

/* 在中间插入元素 */
void insert(MyList *nums, int index, int num) {
    assert(index >= 0 && index < size(nums));
    // 元素数量超出容量时，触发扩容机制
    if (size(nums) == capacity(nums)) {
        extendCapacity(nums); // 扩容
    }
    for (int i = size(nums); i > index; --i) {
        nums->arr[i] = nums->arr[i - 1];
    }
    nums->arr[index] = num;
    nums->size++;
}

/* 删除元素 */
// 注意：stdio.h 占用了 remove 关键词
int removeItem(MyList *nums, int index) {
    assert(index >= 0 && index < size(nums));
    int num = nums->arr[index];
    for (int i = index; i < size(nums) - 1; i++) {
        nums->arr[i] = nums->arr[i + 1];
    }
    nums->size--;
    return num;
}

/* 列表扩容 */
void extendCapacity(MyList *nums) {
    // 先分配空间
    int newCapacity = capacity(nums) * nums->extendRatio;
    int *extend = (int *)malloc(sizeof(int) * newCapacity);
    int *temp = nums->arr;

    // 拷贝旧数据到新数据
    for (int i = 0; i < size(nums); i++)
        extend[i] = nums->arr[i];

    // 释放旧数据
    free(temp);

    // 更新新数据
    nums->arr = extend;
    nums->capacity = newCapacity;
}

/* 将列表转换为 Array 用于打印 */
int *toArray(MyList *nums) {
    return nums->arr;
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



