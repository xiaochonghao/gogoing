# Copying a list
完全可以将`python`的**赋值**理解成改变指针指向的操作。
```py
>>> colours1 = ["red", "green"]
>>> colours2 = colours1
>>> colours2 = ["rouge", "vert"]
>>> print colours1
['red', 'green']
```

![deepcopy1](/images/deep_copy_1.png)

```py
>>> colours1 = ["red", "green"]
>>> colours2 = colours1
>>> colours2[1] = "blue"
>>> colours1
['red', 'blue']
```
![deepcopy2](/images/deep_copy_2.png)

# Copy with the Slice Operator

```py
>>> list1 = ['a','b','c','d']
>>> list2 = list1[:]
>>> list2[1] = 'x'
>>> print list2
['a', 'x', 'c', 'd']
>>> print list1
['a', 'b', 'c', 'd']
>>> 
```

![deepcopy3](/images/deep_copy_3.png)

```py
>>> lst1 = ['a','b',['ab','ba']]
>>> lst2 = lst1[:]
```

```py
>>> lst1 = ['a','b',['ab','ba']]
>>> lst2 = lst1[:]
>>> lst2[0] = 'c'
>>> lst2[2][1] = 'd'
>>> print(lst1)
['a', 'b', ['ab', 'd']]
```

![deepcopy4](/images/deep_copy_4.png)

# Using the Method deepcopy from the Module copy

```py
from copy import deepcopy

lst1 = ['a','b',['ab','ba']]

lst2 = deepcopy(lst1)

lst2[2][1] = "d"
lst2[0] = "c";

print lst2
print lst1
```

```
$ python deep_copy.py 
['c', 'b', ['ab', 'd']]
['a', 'b', ['ab', 'ba']]
```
![deepcopy5](/images/deep_copy_5.png)