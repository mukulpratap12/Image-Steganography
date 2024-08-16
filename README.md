# Image-Steganography Project By Python 👾👾:-


# STEP 1 :- We are importing Libraries 

from tkinter import *
from tkinter import filedialog, messagebox
from PIL import Image, ImageTk
import os
from stegano import lsb


# Tkinter: Provides the graphical user interface (GUI) components.
# filedialog and messagebox: For file selection dialogs and pop-up messages.
# PIL (Python Imaging Library): Handles image opening, displaying, and manipulation.
# os: Provides functions to interact with the operating system, like file paths.
# stegano: Used for the steganography techniques to hide and reveal messages in images.



# STEP-2 :- Initialize the Main Window

win = Tk()
win.geometry('700x480')
win.config(bg='black')


# Tk(): Creates the main application window.
# geometry(): Sets the window size to 700x480 pixels.
# config(): Sets the background color of the window to black.

# STEP-3 :- Define Button Functions

def open_img():
    global open_file
    open_file = filedialog.askopenfilename(
        initialdir=os.getcwd(),
        title='Select File Type',
        filetypes=(('PNG file', '*.png'), ('JPG file', '*.jpg'), ('All files', '*.*'))
    )
    if open_file:
        img = Image.open(open_file)
        img = ImageTk.PhotoImage(img)
        lf1.configure(image=img)
        lf1.image = img
        

# askopenfilename: Opens a file dialog to select an image file.
# Image.open(open_file): Opens the selected image file.
# ImageTk.PhotoImage(img): Converts the image into a format Tkinter can display.
# lf1.configure(image=img): Updates the label with the image


# STEP-4 :- Hide Data Function

def hide():
    global hide_msg
    password = code.get()
    if password == '1234':
        msg = text1.get(1.0, END)
        hide_msg = lsb.hide(open_file, msg)
        messagebox.showinfo('Success', 'Your message is successfully hidden in the image. Please save the image.')
    elif password == '':
        messagebox.showerror('Error', 'Please enter a Secret Key.')
    else:
        messagebox.showerror('Error', 'Wrong Secret Key.')
        code.set('')
        
        
# code.get(): Retrieves the secret key entered by the user.
# text1.get(1.0, END): Gets the message from the text widget.
# lsb.hide(open_file, msg): Hides the message in the selected image.
# messagebox.showinfo: Displays a success message.


# STEP-5 :- Save Image Function

def save_img():
    if 'hide_msg' in globals():
        hide_msg.save('Secret_file.png')
        messagebox.showinfo('Saved', 'Image has been successfully saved.')
    else:
        messagebox.showwarning('Warning', 'No image to save. Please hide data first.')

        
# hide_msg.save('Secret_file.png'): Saves the image with the hidden message.
# messagebox.showwarning: Alerts the user if there is no image to save.


# STEP-6 :- Show Data Function

def show():
    password = code.get()
    if password == '1234':
        show_msg = lsb.reveal(open_file)
        text1.delete(1.0, END)
        text1.insert(END, show_msg)
    elif password == '':
        messagebox.showerror('Error', 'Please enter a Secret Key.')
    else:
        messagebox.showerror('Error', 'Wrong Secret Key.')
        code.set('')


# lsb.reveal(open_file): Reveals the hidden message from the selected image.
# text1.delete(1.0, END): Clears any existing text in the text widget.
# text1.insert(END, show_msg): Displays the revealed message.


# STEP-7 :- Create and Configure GUI Components  :-

logo = PhotoImage(file='lgo.png')
Label(win, image=logo, bd=0).place(x=190, y=0)
Label(win, text='Cyber Security', font='impact 30 bold', bg='black', fg='red').place(x=260, y=12)


# PhotoImage(file='lgo.png'): Loads an image for the logo.
# Label(..., image=logo): Displays the logo in the window.
# Label(..., text='Cyber Security'): Adds a heading label with a specific font and color.


# STEP-8 :- Frames and Labels

f1 = Frame(win, width=250, height=220, bd=5, bg='purple')
f1.place(x=50, y=100)
lf1 = Label(f1, bg='purple')
lf1.place(x=0, y=0)

f2 = Frame(win, width=320, height=220, bd=5, bg='white')
f2.place(x=330, y=100)
text1 = Text(f2, font='arial 15 bold', wrap=WORD)
text1.place(x=0, y=0, width=310, height=210)

Label(win, text='Enter Secret Key', font='10', bg='black', fg='yellow').place(x=250, y=330)

code = StringVar()
e = Entry(win, textvariable=code, bd=2, font='impact 10 bold', show='*')
e.place(x=245, y=360)


# Frames (f1 and f2): Create containers for other widgets.
# Label(f1, bg='purple'): Used to display the selected image.
# Text(f2): Provides a text area for entering or displaying messages.
# Entry(win): A field for entering the secret key.


# STEP-9 :- Buttons

Button(win, text='Open Image', bg='blue', fg='white', font='arial 12 bold', cursor='hand2', command=open_img).place(x=60, y=417)
Button(win, text='Save Image', bg='green', fg='white', font='arial 12 bold', cursor='hand2', command=save_img).place(x=190, y=417)
Button(win, text='Hide Data', bg='red', fg='white', font='arial 12 bold', cursor='hand2', command=hide).place(x=380, y=417)
Button(win, text='Show Data', bg='orange', fg='white', font='arial 12 bold', cursor='hand2', command=show).place(x=510, y=417)





# Full CODE :-

from tkinter import *
from tkinter import filedialog,messagebox
from PIL import Image,ImageTk
import os
from stegano import lsb

win = Tk()
win.geometry('700x480')
win.config(bg='black')
#Button Function
def open_img():
    global open_file
    open_file = filedialog.askopenfilename(initialdir=os.getcwd(),
                                            title='Select File Type',
                                            filetypes=(('PNG file','*.png'),('JPG file','*.jpg'),
                                                        ('All file','*.txt')))
    img = Image.open(open_file)
    img = ImageTk.PhotoImage(img)
    lf1.configure(image=img)
    lf1.image=img
def hide():
    global hide_msg
    password = code.get()
    if password == '1234':

        msg = text1.get(1.0,END)
        hide_msg = lsb.hide(str(open_file),msg)
        messagebox.showinfo('Success','Your message is sucessfully hideen in a image,please save your image')
    elif password == '':
        messagebox.showerror('Error','Please enter Secret key')
    else:
        messagebox.showerror('Error','Wrong Sectret Key')
        code.set('')

def save_img():
    hide_msg.save('Secret file.png')
    messagebox.showinfo('Saved','Image has been successfully saved')
def show():
    password = code.get()
    if password == '1234':
        show_msg = lsb.reveal(open_file)
        text1.delete(1.0,END)
        text1.insert(END,show_msg)
    elif password == '':
        messagebox.showerror('Error', 'Please enter Secret key')
    else:
        messagebox.showerror('Error', 'Wrong Sectret Key')
        code.set('')
#Logo
logo = PhotoImage(file='lgo.png')
Label(win,image=logo,bd=0).place(x=190,y=0)
#Heading
Label(win,text='Cyber Security',font='impack 30 bold',bg='black',fg='red').place(x=260,y=12)
#Frame 1
f1 = Frame(win,width=250,height=220,bd=5,bg='purple')
f1.place(x=50,y=100)
lf1 = Label(f1,bg='purple')
lf1.place(x=0,y=0)

#Frame 2
f2 = Frame(win,width=320,height=220,bd=5,bg='white')
f2.place(x=330,y=100)
text1 = Text(f2,font='ariel 15 bold',wrap=WORD)
text1.place(x=0,y=0,width=310,height=210)

#Label for Secret Key
Label(win,text='Enter Secret Key',font='10',bg='black',fg='yellow').place(x=250,y=330)

#Entry Widget for secret key
code=StringVar()
e = Entry(win,textvariable=code,bd=2,font='impact 10 bold ',show='*')
e.place(x=245,y=360)

#Buttons
open_button = Button(win,text='Open Image',bg='blue',fg='white',font='ariel 12 bold ',cursor='hand2',command=open_img)
open_button.place(x=60,y=417)

save_button = Button(win,text='Save Image',bg='green',fg='white',font='ariel 12 bold ',cursor='hand2',command=save_img)
save_button.place(x=190,y=417)

hide_button = Button(win,text='Hide Data',bg='red',fg='white',font='ariel 12 bold ',cursor='hand2',command=hide)
hide_button.place(x=380,y=417)

show_button = Button(win,text='Show Data',bg='orange',fg='white',font='ariel 12 bold ',cursor='hand2',command=show)
show_button.place(x=510,y=417)
mainloop()







