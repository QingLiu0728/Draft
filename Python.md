# String
1. String is immutable
    Instance: b.replace(b, a), this can return a, but b != a
2. simple test function
```python
def test(got, expected):
  if got == expected:
    prefix = ' OK '
  else:
    prefix = '  X '
  print '%s got: %s expected: %s' % (prefix, repr(got), repr(expected))
```

# List
list.append() return NONE, it cannot be that: lista = lista.append(xx)

sorted makes a new copy of list, it does not modify original list
sorted(list)
sorted(list, key=None, reverse = false)

%% sorted by length
sorted(list, key=len)

force sorting to treat uppercase and lowercase the same:
sorted(list, key=str.lower)

sorted by customized function
def MyFn(s):
    return s[-1]
sorted(list, key=MyFn)

Attention:
sort(): it modify list directly and return nothing
sorted(): on the contrary to sort()

# Tuple
Tuple is a fixed size grouping of elements, such as (x, y) coordinate.
Since it is immutable and does not change size

# List Comprehension

list.index(xxx)
nums = [1, 2, 3, 4]
squares = [n*n for n in nums]

strs = ['hell', 'add', 'good']
strcomb = [s.upper() for s in strs if 'a' in strs]

if intepreter return nothing, then this function will return NONE

# Dict
dict = {}
dict['a'] = 'alpha'
dict['b'] = 'banana'
s = 'I want %(a)s instead of %(b)s' % dict

** Dict is inherently unordered, it is difficult to sord dict especially by its value. But we can sort it by using dict.items(), this function help convert dict to list **


values()
keys()
items(): put all keys and values in tuple

# Filee
open file:
open('name', 'rU')
'r' for reading, 'w' for writing, 'a' for append
'rU' make function convert different line-endings to a simple '\n'

read file:
for line in file:
    print line
read one line at a time

readlines() : reads the whole file into memory and return a list of its lines
read():       read the whole file into a single string, which can be handy with regular expressions
close file:
close()

_trick: in windows, **pwd** can not send out the original path of file, we can use **pwd -W** instead_

**Since there is no cue for what the type of a var, so it is much more important than other language like Java, to have good variables name
First of all, the name can keep track of the type of the variable**

# Python Regular Expressions
```python
import re

```

# Python os
There is huge difference between "C:" and "C:/"("C:\\")
C: means the current directory
C:/ means the actual C drive 

# Python function
```python
def total(a=5, *numbers, **phonebook):
    print('a', a)
    #遍历元组中的所有项目
    for single_item in numbers:
        print('single_item', single_item)
    #遍历字典中的所有项目
    for first_part, second_part in phonebook.items():
        print(first_part,second_part)
print(total(10,1,2,3,Jack=1123,John=2231,Inge=1560))
```

>python sys.argv[0] is the name of the called function, sys.argv[1] is the first argument

Trick of list,dict,tuple slicing:
we can assign specific step for slicing. Default step is 1:`list[::1]`, step 2`list[::2}`, reverse list:`list[::-1]`

**Reference**
```python
print('Simple Assignment')
shoplist = ['apple', 'mango', 'carrot', 'banana']
# mylist 只是指向同一对象的另一种名称
mylist=shoplist
# 我购买了第一项项目，所以我将其从列表中删除
del shoplist[0]
print('shoplist is', shoplist)
print('mylist is', mylist)
# 注意到 shoplist 和 mylist 二者都打印出了其中都没有apple的同样的列表，以此我们确认
# 它们指向的是同一个对象
print('Copy by making a full slice')
# 通过生成一份完整的切片制作一份列表的副本
mylist=shoplist[:]
# 删除第一个项目
del mylist[0]
print('shoplist is', shoplist)
print('mylist is', mylist)
# 注意到现在两份列表已出现不同
```

**list reverse:**
1. list[::-1]
2. sorted(list, reverse=True)
3. list.reverse()

# Exception
```python
try:
    
except Error:

```
