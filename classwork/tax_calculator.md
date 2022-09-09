```.py
salary = int(input('please put intput your salary'))
tax = 0
if salary > 10000:
    tax = 0.25
elif 5000 < salary <= 10000:
    tax = 0.15
elif 1000 < salary <= 5000:
    tax = 0.1
elif 0 < salary <= 1000:
    tax = 0.05

print(f'your tax is {int(salary*tax)} dollars')
```
