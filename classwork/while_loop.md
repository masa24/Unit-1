```.py
start = input('you are counting from,,,')
end = input('you are ending at,,,')
step = input('how many step,,,')
chance = 5
while not start.isdigit() or not end.isdigit() or not step.isdigit() or int(end) < int(start) and chance > 0:
    if not start.isdigit():
        start = input('Please put a intiger for start')
    if not end.isdigit():
        end = input('Please put a intiger for end which is bigger than the start')
    if int(end) < int(start):
        end = input('Please put a intiger for end which is bigger than the start')
    if not step.isdigit():
        step = input('Please put a intiger for step')
    print(f'Your chance is {chance} times left')
    chance -= 1

start = int(start)
end = int(end)
step = int(step)
print('This is the result')
while start <= end:
    print(start)
    start+=step
```
