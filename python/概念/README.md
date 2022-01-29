 ### 行延续

- 在行尾使用反斜杠 \ 分割成多行
```python
question="aaaaaaaaaaaaaaaaaaaaaaa"\
          +"bbbbbbbbbbb" #第一种
print(question,qu)
```
- 使用括号将代码块包括起来
```python
qu=("aaaaaaaaa"+
    "cccccccc") #第二种
print(question,qu)
```

### 运算符

- 条件表达式是计算结果为真值的表达式

假值：False, 0, None, "", [],(),{}

- not ：计算表达式的布尔值，返回与该布尔值相反的布尔值（因此 not 将始终返回 True 或 False）

- and ：返回它遇到的第一个计算为False的表达式的值，如果所有表达式都计算为True，则返回最后一个表达式的值
```python
>>> 1 and none and 2
none
>>> 1 and 2 and 3
3
```
- or返回它遇到的第一个计算为True的表达式的值，如果所有表达式都计算为False，则返回最后一个表达式的值
```python
>>>  1 or 0
1
>>> 0 or 0
0
```

//: 2/3=0

/: 3/4=0.75

%: 3%4=2

** ：2 ** 3=8  (优先级仅次于括号)

