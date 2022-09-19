```.py
a = str(input())
count = 0
result = ''
for b in a:
    count = 0
    for i in 'abcdefghijklmnopqrstuvwxyz':
        count+=1
        if b.lower() == i:
            result += str(count)
            result += ','
print(result)
```
![solution to the quiz](quiz1.png)
