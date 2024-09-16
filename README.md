from tkinter import *
from tkinter import messagebox
import random

def g():
    global ch, r, wrong_letters
    x = e.get().lower()
    e.delete(0, END)
    
    if len(x) != 1 or not x.isalpha():
        messagebox.showwarning("خطأ", "يرجى إدخال حرف واحد فقط")
        return
    
    if x in ch:
        nt = list(lbl['text'])
        for i in range(len(ch)):
            if x == ch[i]:
                nt[i] = x
        lbl['text'] = ''.join(nt)
        
        if faz():
            messagebox.showinfo('You Win', '*WIN*')
            res()
    else:
        if x not in wrong_letters:
            r -= 1
            lbl1['text'] = 'Remaining: ' + str(r)
            lbl1['fg'] = 'red'
            wrong_letters.append(x)
            lb2['text'] = 'Wrong: ' + ', '.join(wrong_letters)
            
        if r == 0:
            messagebox.showinfo('You Lost', f'The word was: {ch}\nTry again!')
            res()

def res():
    global ch, r, wrong_letters
    ch = random.choice(c)
    lbl['text'] = '-' * len(ch)
    r = 6
    wrong_letters = []
    lbl1['text'] = 'Remaining: ' + str(r)
    lbl1['fg'] = 'black'
    lb2['text'] = 'Wrong: ' + ', '.join(wrong_letters)

def faz():
    return '-' not in lbl['text']

root = Tk()
root.geometry('300x300')
root.title("Hangman Game")

r = 6
wrong_letters = []
let = [chr(i) for i in range(97, 123)]

c = ['python', 'programming', 'developer', 'hangman']
ch = random.choice(c)

lbl = Label(root, text='-' * len(ch), font='Arial 30', padx=60, bd=10)
lbl.place(x=15, y=10)

e = Spinbox(root, values=let, width=10, font='Arial 22', bd=5)
e.place(x=25, y=70)

lb2 = Label(root, text='⚠️Enter a single letter!!', font='Arial 10')
lb2.place(x=15, y=110)

b = Button(root, text='Guess', bg='skyblue', font='Arial 21', command=g)
b.place(x=65, y=140)

lbl1 = Label(root, text='Remaining: ' + str(r), font='Arial 20')
lbl1.place(x=65, y=220)

lb2 = Label(root, text='Wrong: ' + ', '.join(wrong_letters), font='Arial 20')
lb2.place(x=65, y=255)

root.mainloop()

