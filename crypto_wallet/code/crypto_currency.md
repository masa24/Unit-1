```,py
from crypto_library import intro, registration, login, color, action_general, typecheck,statistics,sep
import datetime
date = str(datetime.date.today())

#introduction
intro()

# register and login
name = str(input('\nplease enter your username: '))
state = registration(name)
login(state,name)

# action
sep()
tos = str(input(color('For transaction enter 1\nFor statistics enter 2\n\nEnter: ', 'blue')))
while tos != '1' and tos != '2':
    tos = str(input(color('Please enter 1 or 2','red')))
while tos == '1' or tos == '2':
    sep()
    if tos == '1':
        type = typecheck(input(color('\nEnter number\n1.enter\n2.withdraw\n3.check balance\n\nnum:','blue')))
        action_general(type,name,date,state)
    if tos == '2':
        statistics(name)
    sep()
    tos = str(input(color('To continue with transaction enter 1\nTo continue statistics enter 2\nTo finish enter 3\n\nEnter: ', 'blue')))
    while tos != '1' and tos != '2' and tos != '3':
        tos = str(input(color('Please enter 1 or 2', 'red')))
    if tos == '3':
        print(color('Thank you for using!','cyan'))

```
