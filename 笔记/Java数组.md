# 数组

避免定义多个重复类型的变量

数组是相同类型数据的有序集合

避免使用C风格的数组声明 int nums[]

nums.length 获取数组长度

数组中元素会有默认值

# 三种初始化

静态初始化

动态初始化

默认初始化：数组是引用类型，会像实例变量一样有默认值

# 数组四个基本特点

1. 数组长度是确定的
2. 元素必须是相同类型
3. 数组中元素可以是任意数据类型
4. 数组本身就是对象，Java中对象是在堆中的

# 数组使用

普通for循环

foreach

数组作为参数

数组作为返回类型

# 多维数组

数组的数组

int[] []  array = {{1,2}, {3,4}};

# 冒泡排序

先找最小，再找第二小，……

# 稀疏数组

二维数组很多值是0，记录了很多没有意义的数据

稀疏数组：记录数组一共有几行几列，有多少个不同值

用坐标的方式把有效值记下来
