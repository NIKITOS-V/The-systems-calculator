from tkinter import *

root = Tk()
root.geometry('800x500')
root.title("Калькулятор систем")
root.resizable(width=False, height=False)
root['bg'] = 'black'


def CALCULATE():
    bykva = ('A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U',
             'V', 'W', 'X', 'Y', "Z")
    bykvaMini = ('a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u'
                 , 'v', 'w', 'x', 'y', 'z')
    perevod = list(enter_number.get())
    systema = int(enter_sistem.get())
    systema2 = int(enter_sistem2.get())
    print('\n')
    if 2 <= systema <= 36 and 2 <= systema2 <= 36:
        for i in perevod:
            for j in bykva:
                if i == j:
                    perevod.insert(perevod.index(i), str(bykva.index(j) + 10))
                    perevod.pop(perevod.index(i))
            for j2 in bykvaMini:
                if i == j2:
                    perevod.insert(perevod.index(i), str(bykvaMini.index(j2) + 10))
                    perevod.pop(perevod.index(i))
        perevod.reverse()
        otvet2 = count = 0
        for i2 in perevod:
            otvet2 += int(i2) * (systema ** count)
            count += 1
        otvet = ' '
        while otvet2 > 0:
            ostatok = otvet2 % systema2
            otvet2 //= systema2
            if systema2 < 10 or ostatok < 10:
                otvet += str(ostatok)
            elif systema2 > 10:
                otvet += bykva[ostatok - 10]
        answer_label_entry.config(text=(otvet[::-1]))
    else:
        answer_label_entry.config(text='Указаны неверные системы счисления')


def CLEAR():
    enter_number.delete(0, END)
    enter_sistem.delete(0, END)
    enter_sistem2.delete(0, END)
    answer_label_entry.config(text='')


hello_label = Label(
    root,
    text='Добро пожаловать в калькулятор систем!',
    bg='black',
    fg='white',
    font=('Times New Roman', 30))

ask_The_number = Label(
    root,
    text='Введите число \n которое нужно перевести',
    font=('Times New Roman', 15),
    width=24)

ask_sistem = Label(
    root,
    text='Введите систему, в которой \n записано ваше число',
    font=('Times New Roman', 15),
    width=24)

ask_sistem2 = Label(
    root,
    text='Введите систему, в которое \n нужно перевести ваше число',
    font=('Times New Roman', 15),
    width=24)

answer_label = Label(
    root,
    text='Ответ',
    font=('Times New Roman', 30),
    width=12)

enter_number = Entry(
    root,
    font=('Times New Roman', 15))

enter_sistem = Entry(
    root,
    font=('Times New Roman', 15))

enter_sistem2 = Entry(
    root,
    font=('Times New Roman', 15))

answer_label_entry = Label(
    root,
    text='',
    font=('Times New Roman', 15),
    width=45,
    height=2)

BUTTON_CALCULATE = Button(
    root,
    text='ВЫЧИСЛИТЬ',
    font=('Times New Roman', 25),
    activeforeground='white',
    activebackground='black',
    command=CALCULATE)

BUTTON_Clear = Button(
    root,
    text='ОЧИСТИТЬ',
    font=('Times New Roman', 25),
    activeforeground='white',
    activebackground='black',
    command=CLEAR)

hello_label.pack(pady=10)

BUTTON_CALCULATE.place(x=290, y=310)
BUTTON_Clear.place(x=530, y=310)

ask_The_number.place(x=10, y=70)
ask_sistem.place(x=10, y=130)
ask_sistem2.place(x=10, y=190)
answer_label.place(x=10, y=250)

enter_number.place(x=290, y=70, width=500, height=50)
enter_sistem.place(x=290, y=130, width=500, height=50)
enter_sistem2.place(x=290, y=190, width=500, height=50)
answer_label_entry.place(x=290, y=250)

root.mainloop()
