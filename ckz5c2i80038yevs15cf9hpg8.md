## Multiplayer Word Guessing Simple Python Game

### I think you are bored, so you just clicked this blog right? Would like to know in the comments below😁 !

# Today's BLOG:
# The Word Guessing Game
# Made by Omar

-------------------------------------------------------

I feel you are bored from programming and want to do something else right? Tell me in the comments. I also sometimes had the same thing 😂 too. Funny, right ?

Without further talking, let's get into it!
-----------------------------------------------------------

### 1. The basics - Libraries

To start our guessing game, we need the help of librares which will make our code much easier, today we will need `random` library. Which will help us to choose a random word from a list of words given by us.

To import `random` let's put the following command!
```py
import random # Import random library
from random import * # Import all submodules in random
```
----------------------------------------------------------
### 1. The basics - Variables & Function for using random word

Also, we need variables which make our game functional and also `fun!` So let's create the variables we need for our game project.

```py
# function for choosing random word.
def choose():
    # list of word
    words = ['rainbow', 'computer', 'science', 'programming',
             'mathematics', 'player', 'condition', 'reverse',
             'water', 'board', 'hashnode']
 
    # choice() method randomly choose
    # any word from the list.
    pick = random.choice(words)
 
    return pick
```

--------------------------------------------------------------
### 2. The real programming time - Dive in

So now lets start making the game functional to be able to played and enjoyed by user.

Part 1:

```py
# Function for shuffling the
# characters of the chosen word.
def jumble(word):
    # sample() method shuffling the characters of the word
    random_word = random.sample(word, len(word))
 
    # join() method join the elements
    # of the iterator(e.g. list) with particular character .
    jumbled = ''.join(random_word)
    return jumbled
 
 
# Function for showing final score.
def thank(p1n, p2n, p1, p2):
    print(p1n, 'Your score is :', p1)
    print(p2n, 'Your score is :', p2)
 
    # check_win() function calling
    check_win(p1n, p2n, p1, p2)
 
    print('Thanks for playing...')
 
 
# Function for declaring winner
def check_win(player1, player2, p1score, p2score):
    if p1score > p2score:
        print("winner is :", player1)
    elif p2score > p1score:
        print("winner is :", player2)
    else:
        print("Draw..Well Played guys..")
```

Part 2:
```py
# Function for playing the game.
def play():
    # enter player1 and player2 name
    p1name = input("player 1, Please enter your name :")
    p2name = input("Player 2 , Please enter your name: ")
 
    # variable for counting score.
    pp1 = 0
    pp2 = 0
 
    # variable for counting turn
    turn = 0
 
    # keep looping
    while True:
 
        # choose() function calling
        picked_word = choose()
 
        # jumble() function calling
        qn = jumble(picked_word)
        print("jumbled word is :", qn)
 
        # checking turn is odd or even
        if turn % 2 == 0:
 
            # if turn no. is even
            # player1 turn
            print(p1name, 'Your Turn.')
 
            ans = input("what is in your mind? ")
 
            # checking ans is equal to picked_word or not
            if ans == picked_word:
 
                # incremented by 1
                pp1 += 1
 
                print('Your score is :', pp1)
                turn += 1
 
            else:
                print("Better luck next time ..")
 
                # player 2 turn
                print(p2name, 'Your turn.')
 
                ans = input('what is in your mind? ')
 
                if ans == picked_word:
                    pp2 += 1
                    print("Your Score is :", pp2)
 
                else:
                    print("Better luck next time...correct word is :", picked_word)
 
                c = int(input("press 1 to continue and 0 to quit :"))
 
                # checking the c is equal to 0 or not
                # if c is equal to 0 then break out
                # of the while loop o/w keep looping.
                if c == 0:
                    # thank() function calling
                    thank(p1name, p2name, pp1, pp2)
                    break
 
        else:
 
            # if turn no. is odd
            # player2 turn
            print(p2name, 'Your turn.')
            ans = input('what is in your mind? ')
 
            if ans == picked_word:
                pp2 += 1
                print("Your Score is :", pp2)
                turn += 1
 
            else:
                print("Better luck next time.. :")
                print(p1name, 'Your turn.')
                ans = input('what is in your mind? ')
 
                if ans == picked_word:
                    pp1 += 1
                    print("Your Score is :", pp1)
 
                else:
                    print("Better luck next time...correct word is :", picked_word)
 
                    c = int(input("press 1 to continue and 0 to quit :"))
 
                    if c == 0:
                        # thank() function calling
                        thank(p1name, p2name, pp1, pp2)
                        break
 
            c = int(input("press 1 to continue and 0 to quit :"))
            if c == 0:
                # thank() function calling
                thank(p1name, p2name, pp1, pp2)
                break
 
 
# Driver code
if __name__ == '__main__':
     
    # play() function calling
    play()
```

--------------------------------------------------------------------

# We are done!

### Let's try it, I will share the output with you, and would like to see your result too in the comments section ! 😁

### Output:

```
player 1, Please enter your name : Omar
Player 2 , Please enter your name: Texas
jumbled word is : darbo
 Omar Your Turn.
what is in your mind? board
Your score is : 1
jumbled word is : ngioragmpmr
Texas Your turn.
what is in your mind? program
Better luck next time.. :
 Omar Your turn.
what is in your mind? programming
Your Score is : 2
press 1 to continue and 0 to quit :1
jumbled word is : aronbiw
Texas Your turn.
what is in your mind? rainbow
Your Score is : 1
press 1 to continue and 0 to quit :0
 Omar Your score is : 2
Texas Your score is : 1
winner is :  Omar
Thanks for playing...
```

### Output Screenshot:


![output.png](https://i.imgur.com/43r18UU.png)

---------------------------------------------------

# Full code : 

```py
# Python program for jumbled words game.

# import random module
import random


# function for choosing random word.
def choose():
	# list of word
	words = ['rainbow', 'computer', 'science', 'programming',
			'mathematics', 'player', 'condition', 'reverse',
			'water', 'board', 'hashnode']

	# choice() method randomly choose
	# any word from the list.
	pick = random.choice(words)

	return pick


# Function for shuffling the
# characters of the chosen word.
def jumble(word):
	# sample() method shuffling the characters of the word
	random_word = random.sample(word, len(word))

	# join() method join the elements
	# of the iterator(e.g. list) with particular character .
	jumbled = ''.join(random_word)
	return jumbled


# Function for showing final score.
def thank(p1n, p2n, p1, p2):
	print(p1n, 'Your score is :', p1)
	print(p2n, 'Your score is :', p2)

	# check_win() function calling
	check_win(p1n, p2n, p1, p2)

	print('Thanks for playing...')


# Function for declaring winner
def check_win(player1, player2, p1score, p2score):
	if p1score > p2score:
		print("winner is :", player1)
	elif p2score > p1score:
		print("winner is :", player2)
	else:
		print("Draw..Well Played guys..")


# Function for playing the game.
def play():
	# enter player1 and player2 name
	p1name = input("player 1, Please enter your name :")
	p2name = input("Player 2 , Please enter your name: ")

	# variable for counting score.
	pp1 = 0
	pp2 = 0

	# variable for counting turn
	turn = 0

	# keep looping
	while True:

		# choose() function calling
		picked_word = choose()

		# jumble() function calling
		qn = jumble(picked_word)
		print("jumbled word is :", qn)

		# checking turn is odd or even
		if turn % 2 == 0:

			# if turn no. is even
			# player1 turn
			print(p1name, 'Your Turn.')

			ans = input("what is in your mind? ")

			# checking ans is equal to picked_word or not
			if ans == picked_word:

				# incremented by 1
				pp1 += 1

				print('Your score is :', pp1)
				turn += 1

			else:
				print("Better luck next time ..")

				# player 2 turn
				print(p2name, 'Your turn.')

				ans = input('what is in your mind? ')

				if ans == picked_word:
					pp2 += 1
					print("Your Score is :", pp2)

				else:
					print("Better luck next time...correct word is :", picked_word)

				c = int(input("press 1 to continue and 0 to quit :"))

				# checking the c is equal to 0 or not
				# if c is equal to 0 then break out
				# of the while loop o/w keep looping.
				if c == 0:
					# thank() function calling
					thank(p1name, p2name, pp1, pp2)
					break

		else:

			# if turn no. is odd
			# player2 turn
			print(p2name, 'Your turn.')
			ans = input('what is in your mind? ')

			if ans == picked_word:
				pp2 += 1
				print("Your Score is :", pp2)
				turn += 1

			else:
				print("Better luck next time.. :")
				print(p1name, 'Your turn.')
				ans = input('what is in your mind? ')

				if ans == picked_word:
					pp1 += 1
					print("Your Score is :", pp1)

				else:
					print("Better luck next time...correct word is :", picked_word)

					c = int(input("press 1 to continue and 0 to quit :"))

					if c == 0:
						# thank() function calling
						thank(p1name, p2name, pp1, pp2)
						break

			c = int(input("press 1 to continue and 0 to quit :"))
			if c == 0:
				# thank() function calling
				thank(p1name, p2name, pp1, pp2)
				break


# Driver code
if __name__ == '__main__':
	
	# play() function calling
	play()
```

----------------------------------------------------

# You reached the end of the blog

I hope you liked it, don't forget to smash the like button, and comment for any new features for the game or new blogs, and see you IN THE NEXT!

Good day!

Kind regards,

~ Omar The Developer