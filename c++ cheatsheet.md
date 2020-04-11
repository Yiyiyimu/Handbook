#### 结构体struct

```cpp
Struct ListNode{
    int val;
    ListNode *next;
    ListNode(int x): val(x), next(NULL) {}	//构造函数的简写方法
    ListNode(int x) {
        val = x;
        next = NULL;
    }//非简化写法
}
ListNode n;
n.val = 1;	//.成员运算符，左边必须为实体
ListNode *p;
p->val;		//->指针指向的成员
```

struct和class区别：

​	基本没区别，只是class继承默认private，struct继承默认public

​	c（面向过程）里struct不能定义构造函数，没有class

push_back和emplace_back区别：

​	push_back会更慢因为：

​	In emplace_back, the element is constructed in-place. While push_back either copies or moves an existing object into the container.

​	emplace_back/front, emplace在C++11代替push_back/front, insert