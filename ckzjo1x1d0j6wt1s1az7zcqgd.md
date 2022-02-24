## Tic Tac Toe - Python Tkinter GUI

Would you like to have some fun ?What about playing XO ?Today we will make this game alone even we are able to CUSTOMIZE IT! Like X will be a 💖 and O is 😀! It's possible @everyone! Let's further ado, let's get into it!

---------------------------------------------------
# We have 2 parts! ( Click on the part to jump to it , WITH MAGIC )

[Multiplayer](https://omardevblog.toolsandapps4us.site/tic-tac-toe#:~:text=Multiplayer%201.%20Basics)

[PC](https://omardevblog.toolsandapps4us.site/tic-tac-toe#:~:text=Single%20Player%20%2D%201.%20Basics)

--------------------------------------------------------------------------------------



### Multiplayer 1. Basics

We are going to make a tic tac toe game, this game can be played VS any friend next to you, on same PC.!1. Create Tkinter WindowOf course we need a window for our game! So let's start by importing Tkinter
```
# Import Tkinter

from tkinter import *

import tkinter

# Create the window

window = Tk()

window.title("Tic Tac Toe - PC")

window.resizable(0, 0) # Use this secret command to make the window fits all needs, buttons and etc.
```


-----------------------------------------


### 2. Main buttons
To make the perfect game, we need buttons which are clickable, the final result should be 3x3 buttons.
```py
# Create the 9 buttons

button1 = Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: button_click(button1))

button1.grid(row=1, column=1)

button2 = Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: button_click(button2))

button2.grid(row=1, column=2)

button3 = Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: button_click(button3))

button3.grid(row=1, column=3)

button4 = Button(window, text=" ", font='Times 20 bold', bg='white',  height=4, width=8, command=lambda: button_click(button4))

button4.grid(row=2, column=1)

button5 = Button(window, text=" ", font='Times 20 bold', bg='white',  height=4, width=8, command=lambda: button_click(button5))

button5.grid(row=2, column=2)

button6 = Button(window, text=" ", font='Times 20 bold', bg='white',  height=4, width=8, command=lambda: button_click(button6))

button6.grid(row=2, column=3)

button7 = Button(window, text=" ", font='Times 20 bold', bg='white',  height=4, width=8, command=lambda: button_click(button7))

button7.grid(row=3, column=1)

button8 = Button(window, text=" ", font='Times 20 bold', bg='white',  height=4, width=8, command=lambda: button_click(button8))

button8.grid(row=3, column=2)

button9 = Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: button_click(button9))

button9.grid(row=3, column=3)

# Store buttons in a list

buttons = [button1, button2, button3, button4, button5, button6, button7, button8, button9]
```


Note : We added a list to store the buttons, this is optional, but it will help you in the next steps!


--------------------------------------

### 3. Change the text

This part seems a little big, but also in the same time easy but little complicated, in this part, as you saw the buttons run a function called button_click and it provides a parameter which is the button name like b1 , b2 or b3 . It will be stored in a variable called button_clicked so let's make the function, then it will change the color and text of the button depending on the turn, so if it is X turn, it will be X, so of course we will need to set the turn variable to X otherwise, each time the button is clicked, it will be X and never be O also set it global in the function. Let's do it! Try doing it yourself, it's easy and simple!
```py
# Button_click function

def button_click(button_clicked):

    global turn

    # We won't need to check if button is empty, because we will make

    # it disabled when we click on it. So it cannot be clicked again.

    if turn == "X":

        # Button text is X and disabled

        button_clicked.config(text="X", state=DISABLED)

        # Button background color

        button_clicked.config(bg="red")

        turn = "O"

    elif turn == "O": # We will use elif here not if, or then, it won't work properly

        # Button text is O and disabled

        button_clicked.config(text="O", state=DISABLED)

        # Button background color

        button_clicked.config(bg="blue")

        turn = "X"
```



 ------------------------------------------------------


### 4. Check winner
Of course to get the game working properly we need to detect who is the winner, which is easy but you might need to focus in this part especially because it is a little bit about Mathematics. So be a mathematician 😂! So, a sample to check, like if the first row is X
```
# if first row is X

    if button1["text"] == "X" and button2["text"] == "X" and button3["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)
```



So we need now to do for X and O the rest, like row, column and diagonal and so on. It takes time, but it's easy to understand the sample which makes the process easier to do! Just try following the sample given above, just be sure to change buttons and be sure these buttons make a row, column, or diagonal. 
We made the buttons disabled to identify that they are clicked to be able to detect a DRAW!
```py
    # if first row is X

    if button1["text"] == "X" and button2["text"] == "X" and button3["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if first row is O

    elif button1["text"] == "O" and button2["text"] == "O" and button3["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if second row is X

    elif button4["text"] == "X" and button5["text"] == "X" and button6["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if second row is O

    elif button4["text"] == "O" and button5["text"] == "O" and button6["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if third row is X

    elif button7["text"] == "X" and button8["text"] == "X" and button9["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if third row is O

    elif button7["text"] == "O" and button8["text"] == "O" and button9["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if first column is X

    elif button1["text"] == "X" and button4["text"] == "X" and button7["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if first column is O

    elif button1["text"] == "O" and button4["text"] == "O" and button7["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if second column is X

    elif button2["text"] == "X" and button5["text"] == "X" and button8["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if second column is O

    elif button2["text"] == "O" and button5["text"] == "O" and button8["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if third column is X

    elif button3["text"] == "X" and button6["text"] == "X" and button9["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if third column is O

    elif button3["text"] == "O" and button6["text"] == "O" and button9["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if first diagonal is X

    elif button1["text"] == "X" and button5["text"] == "X" and button9["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if first diagonal is O

    elif button1["text"] == "O" and button5["text"] == "O" and button9["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if second diagonal is X

    elif button3["text"] == "X" and button5["text"] == "X" and button7["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if second diagonal is O

    elif button3["text"] == "O" and button5["text"] == "O" and button7["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if all buttons are disabled

    elif button1["state"] == DISABLED and button2["state"] == DISABLED and button3["state"] == DISABLED and button4["state"] == DISABLED and button5["state"] == DISABLED and button6["state"] == DISABLED and button7["state"] == DISABLED and button8["state"] == DISABLED and button9["state"] == DISABLED:

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="Draw!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)
```


---------------------------------------------



### 5. Final Step - Run Tkinter in a main loop

Now the final step is to run the actual game, in this part we will use `if __name__ == "__main__"`
to avoid errors xD!

```py
if __name__ == "__main__":

    window.mainloop()
```


-----------------------------------------------------------------------


### Final Code and Video
```py
# Import Tkinter

from tkinter import *

import tkinter

# Create the window

window = Tk()

window.title("Tic Tac Toe - PC")

window.resizable(0, 0) # Use this secret command to make the window fits all needs, buttons and etc.

# Create the 9 buttons

button1 = Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: button_click(button1))

button1.grid(row=1, column=1)

button2 = Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: button_click(button2))

button2.grid(row=1, column=2)

button3 = Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: button_click(button3))

button3.grid(row=1, column=3)

button4 = Button(window, text=" ", font='Times 20 bold', bg='white',  height=4, width=8, command=lambda: button_click(button4))

button4.grid(row=2, column=1)

button5 = Button(window, text=" ", font='Times 20 bold', bg='white',  height=4, width=8, command=lambda: button_click(button5))

button5.grid(row=2, column=2)

button6 = Button(window, text=" ", font='Times 20 bold', bg='white',  height=4, width=8, command=lambda: button_click(button6))

button6.grid(row=2, column=3)

button7 = Button(window, text=" ", font='Times 20 bold', bg='white',  height=4, width=8, command=lambda: button_click(button7))

button7.grid(row=3, column=1)

button8 = Button(window, text=" ", font='Times 20 bold', bg='white',  height=4, width=8, command=lambda: button_click(button8))

button8.grid(row=3, column=2)

button9 = Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: button_click(button9))

button9.grid(row=3, column=3)

# Store buttons in a list

buttons = [button1, button2, button3, button4, button5, button6, button7, button8, button9]

# Create turn variable

turn = "X"

# Button_click function

def button_click(button_clicked):

    global turn

    # We won't need to check if button is empty, because we will make

    # it disabled when we click on it. So it cannot be clicked again.

    if turn == "X":

        # Button text is X and disabled

        button_clicked.config(text="X", state=DISABLED)

        # Button background color

        button_clicked.config(bg="red")

        turn = "O"

    elif turn == "O": # We will use elif here not if, or then, it won't work properly

        # Button text is O and disabled

        button_clicked.config(text="O", state=DISABLED)

        # Button background color

        button_clicked.config(bg="blue")

        turn = "X"

    

    # if first row is X

    if button1["text"] == "X" and button2["text"] == "X" and button3["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if first row is O

    elif button1["text"] == "O" and button2["text"] == "O" and button3["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if second row is X

    elif button4["text"] == "X" and button5["text"] == "X" and button6["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if second row is O

    elif button4["text"] == "O" and button5["text"] == "O" and button6["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if third row is X

    elif button7["text"] == "X" and button8["text"] == "X" and button9["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if third row is O

    elif button7["text"] == "O" and button8["text"] == "O" and button9["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if first column is X

    elif button1["text"] == "X" and button4["text"] == "X" and button7["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if first column is O

    elif button1["text"] == "O" and button4["text"] == "O" and button7["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if second column is X

    elif button2["text"] == "X" and button5["text"] == "X" and button8["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if second column is O

    elif button2["text"] == "O" and button5["text"] == "O" and button8["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if third column is X

    elif button3["text"] == "X" and button6["text"] == "X" and button9["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if third column is O

    elif button3["text"] == "O" and button6["text"] == "O" and button9["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if first diagonal is X

    elif button1["text"] == "X" and button5["text"] == "X" and button9["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if first diagonal is O

    elif button1["text"] == "O" and button5["text"] == "O" and button9["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if second diagonal is X

    elif button3["text"] == "X" and button5["text"] == "X" and button7["text"] == "X":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="X wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if second diagonal is O

    elif button3["text"] == "O" and button5["text"] == "O" and button7["text"] == "O":

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="O wins!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

    # if all buttons are disabled

    elif button1["state"] == DISABLED and button2["state"] == DISABLED and button3["state"] == DISABLED and button4["state"] == DISABLED and button5["state"] == DISABLED and button6["state"] == DISABLED and button7["state"] == DISABLED and button8["state"] == DISABLED and button9["state"] == DISABLED:

        # Disable all buttons

        for button in buttons:

            button.config(state=DISABLED)

        tkinter.Message(window, text="Draw!", font='Times 20 bold').grid(row=4, column=1, columnspan=3)

if __name__ == "__main__":

    window.mainloop()
```

<iframe width="560" height="315" src="https://www.youtube.com/embed/WWVod8fzIVc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


------------------------------------------

### Single Player - 1. Basics
As we know we need to make some basics for the game.So basics for our game we will use
```py
# import tkinter

import tkinter

# create the window

window = tkinter.Tk()

window.title("Tic Tac Toe")

window.resizable(0, 0) # Use this secret command to make the window fits all needs, buttons and etc.
```


--------------------------------


### 2. Buttons
We will make 9 buttons, and when they are clicked they run a function called btn_click which makes further process to make the game functional and fun.
```py
# create 9 buttons and grid them 3x3

b1 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b1)) # create button

b1.grid(row=1, column=1) # arrange the buttons in a 3x3 grid

b2 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b2))

b2.grid(row=1, column=2)

b3 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b3))

b3.grid(row=1, column=3)

b4 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b4))

b4.grid(row=2, column=1)

b5 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b5))

b5.grid(row=2, column=2)

b6 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b6))

b6.grid(row=2, column=3)

b7 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b7))

b7.grid(row=3, column=1)

b8 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b8))

b8.grid(row=3, column=2)

b9 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b9))

b9.grid(row=3, column=3)

# store buttons in a list

buttons = [b1, b2, b3, b4, b5, b6, b7, b8, b9]






3. Change button specifications when clicked
As we know, when the button is clicked, it calls 📞 btn_click function. Let's create the function!

```py
# create btn_click function

def btn_click(btn_clicked):

    btn_clicked['text'] = "X" # change the text of the button

    btn_clicked['state'] = 'disabled' # disable the button

    btn_clicked['bg'] = 'red' # change the background color of the button
```

----------------------------------------------------------------------



### 4. Check for winner

We will do some if statements to check if someone won or not yet, and if not yet “ else " the PC will filter the not disabled buttons then randomly choose from them an button and fill with O and disable it and change color to Blue (in the next part).
```py
    def checkforwinner():

        # if first row is X

        if b1['text'] == 'X' and b2['text'] == 'X' and b3['text'] == 'X':

             # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

        # if second row is X

        elif b4['text'] == 'X' and b5['text'] == 'X' and b6['text'] == 'X':

             # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

        # if third row is X

        elif b7['text'] == 'X' and b8['text'] == 'X' and b9['text'] == 'X':

             # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

        # if first column is X

        elif b1['text'] == 'X' and b4['text'] == 'X' and b7['text'] == 'X':

             # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

        # if second column is X

        elif b2['text'] == 'X' and b5['text'] == 'X' and b8['text'] == 'X':

             # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

        # if third column is X

        elif b3['text'] == 'X' and b6['text'] == 'X' and b9['text'] == 'X':

             # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

        # if first diagonal is X

        elif b1['text'] == 'X' and b5['text'] == 'X' and b9['text'] == 'X':

            # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

        # if second diagonal is X

        elif b3['text'] == 'X' and b5['text'] == 'X' and b7['text'] == 'X':

            # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)
```
            

----------------------------------------------------




### 5. Fill non-disabled random button and check if PC wins

We will check and filter the buttons which are not disabled and store them in a list, then randomly choose a button and then do the next.
```py
else:

            emptybuttons = []

            if b1['text'] == " ":

                emptybuttons.append(b1)

            if b2['text'] == " ":

                emptybuttons.append(b2)

            if b3['text'] == " ":

                emptybuttons.append(b3)

            if ['text'] == " ":

                emptybuttons.append(b4)

            if b5 == " ":

                emptybuttons.append(b5)

            if b6['text'] == " ":

                emptybuttons.append(b6)

            if b7['text'] == " ":

                emptybuttons.append(b7)

            if b8['text'] == " ":

                emptybuttons.append(b8)

            if b9['text'] == " ":

                emptybuttons.append(b9)

            # randomly select a button from the list

            import random

            random_button = random.choice(emptybuttons)

            # change button text to O

            random_button.config(text="O")

            # make button disabled

            random_button.config(state=tkinter.DISABLED)

            # make O blue

            random_button.config(bg="blue")

            # clear the list

            emptybuttons.clear()

            

            # if first row is O

            if b1['text'] == 'O' and b2['text'] == 'O' and b3['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

            # if second row is O

            elif b4['text'] == 'O' and b5['text'] == 'O' and b6['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

            # if third row is O

            elif b7['text'] == 'O' and b8['text'] == 'O' and b9['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

            # if first column is O

            elif b1['text'] == 'O' and b4['text'] == 'O' and b7['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

            # if second column is O

            elif b2['text'] == 'O' and b5['text'] == 'O' and b8['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

            # if third column is O

            elif b3['text'] == 'O' and b6['text'] == 'O' and b9['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

            # if first diagonal is O

            elif b1['text'] == 'O' and b5['text'] == 'O' and b9['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

            # if second diagonal is O

            elif b3['text'] == 'O' and b5['text'] == 'O' and b7['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

    checkforwinner()
```


----------------------------------------


### Final Step - 6. Run Tkinter

The final step is to run tkinter so the game works, we will use if `if __name__ == "__main__"` then we can run tkinter to avoid errors.
```py
if __name__ == "__main__":

    window.mainloop()

```


----------------------------------------------------------

### Full code and Video
```py
# import tkinter

import tkinter

# create the window

window = tkinter.Tk()

window.title("Tic Tac Toe")

window.resizable(0, 0) # Use this secret command to make the window fits all needs, buttons and etc.

# create 9 buttons and grid them 3x3

b1 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b1)) # create button

b1.grid(row=1, column=1) # arrange the buttons in a 3x3 grid

b2 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b2))

b2.grid(row=1, column=2)

b3 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b3))

b3.grid(row=1, column=3)

b4 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b4))

b4.grid(row=2, column=1)

b5 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b5))

b5.grid(row=2, column=2)

b6 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b6))

b6.grid(row=2, column=3)

b7 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b7))

b7.grid(row=3, column=1)

b8 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b8))

b8.grid(row=3, column=2)

b9 = tkinter.Button(window, text=" ", font='Times 20 bold', bg='white', height=4, width=8, command=lambda: btn_click(b9))

b9.grid(row=3, column=3)

# store buttons in a list

buttons = [b1, b2, b3, b4, b5, b6, b7, b8, b9]

# create btn_click function

def btn_click(btn_clicked):

    btn_clicked['text'] = "X" # change the text of the button

    btn_clicked['state'] = 'disabled' # disable the button

    btn_clicked['bg'] = 'red' # change the background color of the button

    def checkforwinner():

        # if first row is X

        if b1['text'] == 'X' and b2['text'] == 'X' and b3['text'] == 'X':

             # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

        # if second row is X

        elif b4['text'] == 'X' and b5['text'] == 'X' and b6['text'] == 'X':

             # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

        # if third row is X

        elif b7['text'] == 'X' and b8['text'] == 'X' and b9['text'] == 'X':

             # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

        # if first column is X

        elif b1['text'] == 'X' and b4['text'] == 'X' and b7['text'] == 'X':

             # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

        # if second column is X

        elif b2['text'] == 'X' and b5['text'] == 'X' and b8['text'] == 'X':

             # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

        # if third column is X

        elif b3['text'] == 'X' and b6['text'] == 'X' and b9['text'] == 'X':

             # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

        # if first diagonal is X

        elif b1['text'] == 'X' and b5['text'] == 'X' and b9['text'] == 'X':

            # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

        # if second diagonal is X

        elif b3['text'] == 'X' and b5['text'] == 'X' and b7['text'] == 'X':

            # make all buttons disabled

            for btn in buttons:

                btn['state'] = 'disabled'

            tkinter.Message(window, text='X wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

        else:

            emptybuttons = []

            if b1['text'] == " ":

                emptybuttons.append(b1)

            if b2['text'] == " ":

                emptybuttons.append(b2)

            if b3['text'] == " ":

                emptybuttons.append(b3)

            if ['text'] == " ":

                emptybuttons.append(b4)

            if b5 == " ":

                emptybuttons.append(b5)

            if b6['text'] == " ":

                emptybuttons.append(b6)

            if b7['text'] == " ":

                emptybuttons.append(b7)

            if b8['text'] == " ":

                emptybuttons.append(b8)

            if b9['text'] == " ":

                emptybuttons.append(b9)

            # randomly select a button from the list

            import random

            random_button = random.choice(emptybuttons)

            # change button text to O

            random_button.config(text="O")

            # make button disabled

            random_button.config(state=tkinter.DISABLED)

            # make O blue

            random_button.config(bg="blue")

            # clear the list

            emptybuttons.clear()

            

            # if first row is O

            if b1['text'] == 'O' and b2['text'] == 'O' and b3['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

            # if second row is O

            elif b4['text'] == 'O' and b5['text'] == 'O' and b6['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

            # if third row is O

            elif b7['text'] == 'O' and b8['text'] == 'O' and b9['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

            # if first column is O

            elif b1['text'] == 'O' and b4['text'] == 'O' and b7['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

            # if second column is O

            elif b2['text'] == 'O' and b5['text'] == 'O' and b8['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

            # if third column is O

            elif b3['text'] == 'O' and b6['text'] == 'O' and b9['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

            # if first diagonal is O

            elif b1['text'] == 'O' and b5['text'] == 'O' and b9['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

            # if second diagonal is O

            elif b3['text'] == 'O' and b5['text'] == 'O' and b7['text'] == 'O':

                # make all buttons disabled

                for btn in buttons:

                    btn['state'] = 'disabled'

                tkinter.Message(window, text='O wins!', width=100, bg='green', font='Times 20 bold').grid(row=4, column=1)

    checkforwinner()

if __name__ == "__main__":

    window.mainloop()


```

<iframe width="560" height="315" src="https://www.youtube.com/embed/Po5UuTsYYms" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>




---------------------------------------------------------------------------





### The End! I hope you ❤️ the blog. Please smash the like button if you 👍 it! 😊, thank you @everyone ! 

Special Thanks to Tealfeed team for promoting my blogs on Tealfeed also Ayush Anand, Community Manager.

Twitter : [@ayush0033](https://twitter.com/ayush0033)


Tealfeed : [@ayush_926238](https://tealfeed.com/ayush_926238)

E-mail : [ayush@tealfeed.com](mailto:ayush@tealfeed.com)

LinkedIn : [Ayush Anand - Community Manager - Tealfeed | LinkedIn](https://in.linkedin.com/in/ayush-anand-67692013a)

[Blog on Tealfeed.com](https://tealfeed.com/tic-tac-toe-game-tkinter-gui-lk61l)


