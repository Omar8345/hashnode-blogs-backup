## Can you do this challenge in Python ?

# Hello reader! Today we have a nice challenge for you 😁 , 'Can you do it in Python ?'

## Today I will give you challenges to do in Python to check your super abilities in Python 😂. So are you ready ? Let's start!

### Today, we have 6 different challenges using Python!

Our challenges!


- Hide the Credit Card Number !
- Give me the discount !
- Repeat the characters !
- Flip the word !
- Random Dice !
- The challenge ! Password Checker !

____________________________________________________________________________________________

### Let us start.
### 1. Hide the Credit Card Number !

I have this Random Credit Card Number ``5837502816340935``

Your mission is to make an app, which makes only the last 4 digits of the number which are ``0935`` , not the whole CC number. Do your code first, don't run it, try guessing the result, and when you are done, check your code below. The card number is assigned on a variable ``CCNum`` (not input) , and the new variable of the 4 digits, , variable is called ``CC4``.

Start now!




The answer:

```py
CCNum = "5837502816340935"

CC4 = CCNum[-4:]

print(CC4)
``` 

The output should be ``0935``

__________________________________________________________________________________________

### 2. Give me a discount !

I have a Coffee shop called 'Coffeeh' . The one Coffee costs 3$. And, I made a discount of 20%, so I want to make Python automate the discount, like I give him 3$, and discount = 20, it returns 2.4$, so, you need 2 inputs, 1 input called ``price`` for 3 $, and the ``discount`` which is 20%. And another variable called ``newprice`` which needs to be set at the output got from your code. Start now!





Answer
```py
price = int(input("Enter price : "))
discount = int(input("Enter discount : "))

discount = 100 - discount
discount = discount / 100
newprice = price * discount

print(newprice)
```

__________________________________________________________________________________________

### 3. Repeat the characters ! 

I have the following word & numbers ``Omar12345`` in a variable called ``word``. I need Python to repeat the characters, like it should be ``OOmmaarr1122334455``, Repeating 2 times, so I will have variable called ``n`` = ``2``, and the new word is assigned in a variable called ``newword``. And you handle the rest of the code, start now!




The answer:

```py
word = 'Omar12345'
n = 2
newword = ''.join([char*n for char in word])

print(newword)
```

__________________________________________________________________________________________


### 4. Flip the word !

I have 2 words, ``omar`` & ``racecar``, I need you to assign them to a variable, ``omar`` to a variable ``word1`` & ``racecar`` to ``word2``, and I need you to flip these words, you need to get the output``ramo`` & ``racecar`` , you need to print them, the new words are assigned on ``newword1`` & ``newword2``, you handle the rest of the function, start now! :) Good luck...




The answer, check it!
```py
word1 = "omar"
word2 = "racecar"

# Getting the new words ...

newword1 = word1[::-1]
newword2 = word2[::-1]

# Print the new words

print(newword1)
print(newword2)
```
__________________________________________________________________________________________

### 5. The Random Dice!

As everyone know, the dice has 6 faces, each face has a number, ``1 , 2 , 3 , 4 , 5 , 6``. You need to make an app, which randomly choose a number of these six and return them by print, start now! Good luck with your mission.




The answer! Check your code!

```py
import random
print (random.randint(1,6))
```

__________________________________________________________________________________________

## The FINAL CHALLANGE ! --> Password Checker !

I have an app for my employees in my company, I need my employees password to be safe, so I want to make a Python App which says if the password is safe or no, the password is given by an input assigned in a variable called ``password``, it should go into the following points:



1. Minimum 8 characters.
2. The alphabets must be between [a-z]
3. At least one alphabet should be of Upper Case [A-Z]
4. At least 1 number or digit between [0-9].
5. At least 1 symbol like [ _ or @ or $ ].

Start now, good luck!





Check your answer here by checking the code if matching or gives same output

```py
# Python program to check validation of password
# Module of regular expression is used with search()
import re
password = input("Enter the password :   ")
flag = 0
while True:
	if (len(password)<8):
		flag = -1
		break
	elif not re.search("[a-z]", password):
		flag = -1
		break
	elif not re.search("[A-Z]", password):
		flag = -1
		break
	elif not re.search("[0-9]", password):
		flag = -1
		break
	elif not re.search("[_@$]", password):
		flag = -1
		break
	elif re.search("\s", password):
		flag = -1
		break
	else:
		flag = 0
		print("Safe Password")
		break

if flag ==-1:
	print("Not a Safe Password")
```

__________________________________________________________________________________________

### So now you have reached the end of this blog. So, to rate your self.

🎉1-2 Challenges done, 4.5 out of 10 🎉🎉🎉

🎉1-4 Challenges done, 6 out of 10 🎉🎉🎉

🎉 1-6 Challenges done, 10 out of 10 🎉🎉🎉

# 🎉🎉🎉! Congrats ! 🎉🎉🎉

So, thank you for reading my blog, have a nice day ! 😀

Happy Coding 😊 !

Best regards,

~ Omar
