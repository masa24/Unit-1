```.py
a = int(input('input your number '))
b = 1
c = 0
while b < a:
    if a % b == 0:
        print(b)
        c += b
    b += 1
print(f'the sum of the factor is {c}')
if a == c:
    print('its a perfect number')
else:
    print('it is not perfect number')
```
