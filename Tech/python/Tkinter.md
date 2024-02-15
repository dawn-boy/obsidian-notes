```python
from tkinter import *
from tkinter import messagebox
window = Tk()
window.title('somethin')
window.geometry('300x300')

label_one = Label(window, text='Username: ', font=('Helvetica',30))
label_one.grid(row=0,column=0)
label_two = Label(window, text='password: ', font=('Helvetica',30))
label_two.grid(row=1,column=0)

username, password = StringVar(),StringVar()

entry_one = Entry(window, textvariable=username)
entry_two= Entry(window, textvariable=password,show='*')
entry_one.grid(row=0,column=1)
entry_two.grid(row=1,column=1)

def auth():
	if username.get() == 'root' and password.get() == 'toor':
		#4th pop-up box
		messagebox.showinfo(title='status',message='Success!')
		emptyLabel.config(text='redirecting..')
	else:
		#3rd pop-up box
		messagebox.showerror(title='status',message='Incorrect username or password. Authentication Failed (Error code 41).')

def cancel():
	#1st pop-up box
	status = messagebox.askyesno(message='Are you sure?', title='Confirmation')
	if status == True:
		#2nd pop-up box
		status = messagebox.askokcancel(message='Are you really sure?',title='shawnAI')
		if status == True:
			#5th pop-up box
			messagebox.showwarning(title='shawnAI',message="Are you really really sure?\nYou're testing my patience here")	
			window.destroy()
	else:
		messagebox.showinfo(title='eh',message='Then please continue to wash him')

button_one = Button(window, text='login',command=auth)
button_two = Button(window, text='cancel', command=cancel)
button_one.grid(row=3,column=0)
button_two.grid(row=3,column=1)

emptyLabel = Label(window,font=('Helvetica',20))
emptyLabel.grid(row=5,column=0)

text_area_one = Text(window, width=10,height=10,wrap=WORD)
text_area_one.grid(row=4,column=0)

from tkinter.ttk import Combobox
combo_box_one = Combobox(window,values=['Blue','Blue','Blue','red'])
combo_box_one.grid(row=6,column=0)

listbox = Listbox(window, selectmode=SINGLE)
listbox.insert(1,'red')
listbox.insert(2,'black')
listbox.insert(3,'green')
listbox.insert(4,'orange')
listbox.grid(row=7,column=0)

window.mainloop()
```