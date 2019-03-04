# Command

1. Shallow copy and Deep copy.

```text
a = object.copy() 等价于 b = copy.deepcopy(object),a和b一样, 都属于深拷贝
copy.copy(object)是浅拷贝，相当于变量引用,等同于下面代码。
a = [1,2,3]
b = a
a = [4,5,6]
>>>b
[1,2,3]
c = b
b[0] = 20
>>>c
[20,2,3]
```

2. 关于Python中复数的说法：

> ```
> 表示复数的语法是real + image j
> 复数的实部与虚部均为浮点数
> 虚部的后缀可以是 “j” 或者 “J”；
> 复数的 conjugate 方法可以返回该复数的共轭复数。
> ```

3. 方括号是list，圆括号是tuple，tuple元素不可改变

