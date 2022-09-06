```.py
fname = input('whats your first name?')
lname = input('whats your last name?')
gradyear = input('when is your gradudation?')
schoolname = input('whats your school name?')
random = 0


overlap = input('Does your name overlap with anyone?')

if overlap == 'yes':
    import random
    random = random.randrange(0, 10)
    print(random)

print(f"Your school account is {gradyear}.{fname}{random}@{schoolname}.jp")
```
