```.py
import pandas as pd
import hashlib
import  getpass

import datetime

def sep():
    print('-'*170)

def typecheck(type):
    while type != '1' and type != '2' and type != '3':
        type = input(color('put a number from 1-3: ', 'red'))
    return type

def isfloat(s):
    try:
        float(s)
    except ValueError:
        return False
    else:
        return True

def typechecka(type):
    while type != '1' and type != '2' and type != '3' and type != '4':
        type = input(color('put a number from 1-3: ', 'red'))
    return type

def checkrate(a):
    while not a.isdigit() and isfloat(a) == False:
        a = input(color('Please enter a integer or float value: ','red'))
    return a

def intcheck(a):
    while not a.isdigit():
        a = input(color('please enter a integer value: ','red'))
    return int(a)

def color (a,color):
    ce = '\033[0m'
    if color == 'black':
        cs ='\033[30m'
    if color == 'red':
        cs = '\033[31m'
    if color =='green':
        cs = '\033[32m'
    if color == 'yellow':
        cs = '\033[33m'
    if color == 'blue':
        cs = '\033[34m'
    if color == 'purple':
        cs = '\033[35m'
    if color == 'cyan':
        cs = '\033[36m'
    if color == 'white':
        cs = '\033[37m'
    return cs+a+ce

def intro():
    opening_message = (color('Welcome to your crypto calculator!!','blue')).center(20)
    explain = '\n>>>To trade crypto currency, You buy it when its low valued and sell it when its expensive.\n'
    cc = color('Cardano','yellow')
    cc_explain = 'Cardano is a blockchain platform for changemakers, innovators, and visionaries,\nwith the tools and technologies required to create possibility for the many,\nas well as the few, and bring about positive global change.'
    return print(opening_message,'\n',explain,'\n',f'you chose:{cc}','\n',cc_explain)

def hash(code):
    code = hashlib.md5(code.encode()).hexdigest()
    return code

def registration(usrname):
    with open('crypto_db.csv','r') as user_data:
        data = user_data.readlines()
    state = 'not user'
    for i in data:
        namedt = i.split(',')
        #print(namedt)
        #namedt = namedt.split(',')
        if namedt[0] == usrname:
            state = 'user'
            break
    if state == 'not user':
        with open('crypto_db.csv','a') as new:
            code = str(input("You are not a user. Set a password to register: "))
            new.write(f'\n{usrname},{hash(code)}')
        with open(f'{usrname}.csv', 'x') as f:
            pass
    return state

def login(state,usrname):
    print(state)
    if state == 'user':#If current user
        with open('crypto_db.csv', 'r') as user_data:
            data = user_data.readlines()
        password = str(input('enter password: '))
#        password = hash(password)
        for i in data:
            namedt = i.split(',')
            if namedt[0] == usrname:
                while (f'{hash(password)}\n' != namedt[1]) and (hash(password) != namedt[1]):
                    password = str(input(color('wrong pass. reenter: ','red')))
        print('login successful')
    else:
        print('registration successful')

def action_1_2(type,name,date,state,value,memo):
    with open(f'{name}.csv', 'r') as f:
        balance = f.readlines()
        if len(balance)>=1:
            balance_value = balance[-1]
            balance_value = balance_value.split(',')
            balance_value = int(balance_value[3])
    if type == '1':
        reason = 'enter'
        with open(f'{name}.csv', 'a') as f:
            f.write(date + ',')
            f.write(str(value) + ',')
            f.write(reason + ',')
            if state == 'user':
                f.write(str(balance_value + value) + ',')
            else:
                f.write(str(value) + ',')
            state = 'user'
    if type == '2':
        reason = 'withdraw'
        if state == 'user':
            while balance_value < int(value):
                value = int(intcheck(input(color('You dont have enough money. Reenter a value: ', 'red'))))
            with open(f'{name}.csv', 'a') as f:
                f.write(date + ',')
                f.write(str(value) + ',')
                f.write(reason + ',')
                f.write(str(balance_value - value) + ',')
        if state == 'not user':
            print('You have no currency in your account')
    rate = checkrate(input('enter the current rate.'))
    with open(f'{name}.csv', 'a') as f:
        f.write(memo + ',')
        f.write(str(rate) + ',\n')
    now = datetime.datetime.now()
    with open('rate.csv', 'a') as a:
        a.write(f'{now},{rate},\n')

def action3(name):
    with open(f'{name}.csv', 'r') as f:
        pre = f.readlines()
        balance = pre[-1].split(',')
    val_len = 5
    balance_len = 7
    reason_len = 6
    memo_len = 11
    rate_len = 4
    for i in pre:
        chr = i.split(',')
        if len(str(chr[1])) > val_len:
            val_len = len(str(chr[1]))
        if len(str(chr[2])) > reason_len:
            reason_len = len(str(chr[2]))
        if len(str(chr[3])) > balance_len:
            balance_len = len(str(chr[3]))
        if len(str(chr[4])) > memo_len:
            memo_len = len(str(chr[4]))
        if len(str(chr[5])) > rate_len:
            rate_len = len(str(chr[5]))

    diagram = ''
    num = 0
    for i in pre:
        num += 1
        count = 0
        for x in i.split(','):
            count += 1
            diagram += ' | '
            if count == 2:
                diagram += (' ' * (val_len - len(x)))
            if count == 3:
                diagram += (' ' * (reason_len - len(x)))
            if count == 4:
                diagram += (' ' * (balance_len - len(x)))
            if count == 5:
                diagram += (' ' * (memo_len - len(x)))
            if count == 6:
                diagram += (' ' * (rate_len - len(x)))
            diagram += str(x)

    message = ''
    intro = '      date,value,action,balance,description,rate,'
    count = 0
    for x in intro.split(','):
        count += 1
        message += ' | '
        if count == 2:
            message += (' ' * (val_len - len(x)))
        if count == 3:
            message += (' ' * (reason_len - len(x)))
        if count == 4:
            message += (' ' * (balance_len - len(x)))
        if count == 5:
            message += (' ' * (memo_len - len(x)))
        if count == 6:
            message += (' ' * (rate_len - len(x)))
        message += str(x)
    sep()
    print(color(message, 'cyan'))
    print(diagram)

def diagram(name,state):
    if state == 'user':
        chart = []
        with open(f'{name}.csv') as f:
            balance = f.readlines()
        for i in balance:
            i.strip()
            i = i.split(',')
            chart.append(i[:5])
        diagram = pd.DataFrame(chart)
        diagram.columns = ['date', 'value', 'action', 'balance', 'memo']
        print(diagram)
    else:
        print(color('No record', 'green'))

def action_general(type,name,date,state):
    while type == '1' or type == '2' or type == '3':
        with open(f'{name}.csv', 'r') as f:
            length = f.readlines()
            if len(length) > 0:
                state = 'user'
        if type == '1' or type == '2':
            value = intcheck(input('Please enter your transaction value: '))
            memo = str(input('enter memo: '))
            action_1_2(type,name,date,state,value,memo)
            if type == '1':
                state = 'user'
            type = str(input('  To see your current record enter 3: '))
        if type == '3':
            action3(name)
        sep()
        type = typechecka(input(color('\nEnter number\n1.enter\n2.withdraw\n3.check balance\n4.End transaction\n\nnum:', 'blue')))
        if type == '4':
            return

def statistics(name):
    act = str(input(color('For change of rate enter 1\nFor your acount value enter 2\n\nEnter: ', 'blue')))
    while act != '1' and act != '2':
        act = str(input(color('Please enter 1 or 2','red')))
    if act == '1':
        with open('rate.csv', 'r') as f:
            data = f.readlines()

        diagram = ''
        length = 4
        for a in data:
            i = a.split(',')
            x = str(i[1])
            if len(x) > length:
                length = len(x)
        pre = 0
        for a in data:
            i = a.split(',')
            diagram += ' | '
            diagram += i[0]
            diagram += ' | '
            num = int(length) - int(len(i[1]))
            diagram += (' ' * num)
            if float(i[1]) >= pre:
                diagram += color(i[1], 'green')
            else:
                diagram += color(i[1], 'red')
            pre = float(i[1])
            diagram += ' |\n'

        space = (' ' * (length - 4))
        print(f' |              date and time | {space}rate | ')
        print(diagram)
    if act == '2':
        with open(f'masamu.csv', 'r') as f:
            data = f.readlines()

        len_balance = 7
        len_rate = 4
        len_value = 0
        for a in data:
            i = a.split(',')
            x = str(i[3])
            y = str(i[5])
            if len(x) > len_balance:
                len_balance = len(x)
            if len(y) > len_balance:
                len_rate = len(y)
            if len(str(int(float(x) * float(y)))) > len_value:
                len_value = len(str(int(float(x) * float(y))))

        diagram = ''
        for a in data:
            i = a.split(',')
            x = str(i[3])
            y = str(i[5])
            diagram += ' | '
            diagram += str(i[0])
            diagram += ' | '
            diagram += (' ' * (int(len_balance) - int(len(x))))
            diagram += str(x)
            diagram += ' | '
            diagram += (' ' * (int(len_rate) - int(len(y))))
            diagram += str(y)
            diagram += ' | '
            diagram += (' ' * (int(len_value) - int(len(str(int(float(x) * float(y)))))))
            diagram += str(int(float(x) * float(y)))
            diagram += ' | '
            diagram += '\n'
        space1 = ' ' * (len_balance - 7)
        space2 = ' ' * (len_rate - 4)
        space3 = ' ' * (len_value - 5)
        print(color(f' |       date | {space1}balance | {space2}rate | {space3}value |', 'blue'))
        print(diagram)
        return




```
