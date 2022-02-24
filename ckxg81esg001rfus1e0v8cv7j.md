## How to --> Convert PY --> EXE

### One of the most frequent asked questions from Python Programmers
### 'How to Convert PY to EXE?'

## The most simplest answer just to say, it is possible, and you can do it, in just a few moments and clicks!

For todays example, I am having the following Python File :)

My Python File is called ``main.py``


```py
name = input('What is your name?')
age = input('What is your age?')
hobby = input('What is your hobby?')
print('Hello ' + name + '! You are ' + age + ' years old. Your hobby is ' + hobby + '.')
``` 

So, let us get into it

## **pyinstaller**

### 1. So first, locate the folder your Python file is located in. And type in the path ``powershell`` and press enter.


![1st.PNG](https://cdn.hashnode.com/res/hashnode/image/upload/v1640097085850/cpZg59H_x.png)

### 2. Enter this command in PowerShell

```cmd
pip install pyinstaller
```


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1640097236406/W5DlLQx03.png)

Then ``pyinstaller`` should install, I installed it before.

### 3. In the PowerShell Window, write the following command & press enter, edit the file name to avoid errors

So for example

```cmd
pyinstaller --onefile filename.py
```


This is an example, so, because my python file name is main.py, I will enter the following command

```cmd
pyinstaller --onefile main.py
```

After the command is executed we should see this message 


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1640097468604/s1U23oCj9.png)


And in our folder, we find some new folders too


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1640097546446/bXc097t5j.png)

### 4. Go into the ``dist`` folder. You will find the exe with your file name. Like main.exe.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1640097656627/6YlkE7lTD.png)

Double-click the exe, and it should run as a Python File.




Possible errors:

When you run the exe, it runs, but when it ends, it closes instantly, so you cannot read the result, to fix the issue, end your Python Code with

```py
input()
```

___________________________________________________________________________________________

# So, you have reached the end of this blog, I hope you liked it, don't forget to smash that like button, and see you in the next!

# **Happy Coding! Best Regards,
# ~ Omar**