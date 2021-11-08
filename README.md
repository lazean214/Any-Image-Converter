# Any-Image-Converter
Covert Image format into standard jpg format

### Required Dependency
Install via pip

	pip install tk
	pip install Pillow
	
### Code
	
	import tkinter as tk #pip install tk
import tkinter.ttk as ttk
from tkinter import filedialog,messagebox
from PIL import Image # pip install Pillow
import os
import subprocess

def center_window(w=300, h=200):
    # get screen width and height
    ws = root.winfo_screenwidth()
    hs = root.winfo_screenheight()
    # calculate position x, y
    x = (ws/2) - (w/2)    
    y = (hs/2) - (h/2)
    root.geometry('%dx%d+%d+%d' % (w, h, x, y))

root = tk.Tk()
root.title('Any Image Converter 1.1')
center_window(300, 150) 
style = ttk.Style(root)
style.theme_use("clam")


def open_files():
    rep = filedialog.askopenfilenames(parent=root, initialdir='/', initialfile='tmp',
                                          filetypes = (("WEBP", "*.webp*"), ("JFIF", "*.jfif*"), ("PNG", "*.png*"), ("JPEG", "*.jpeg*"), ("JPG", "*.jpg*"), ("GIF", "*.gif*"), ("all files", "*.*")))
    i = 0
    
    for img in rep:
      
        path = os.path.dirname(img)
        save_path = str(path) + '/jpg'
        if not os.path.exists(save_path):
            os.makedirs(save_path)
        i= i+1
        print(img)
        im = Image.open(img).convert("RGB")
        im.save(str(save_path) + '/' + str(i) + ".jpg", "jpeg")
    #if Process is completed
    print('Processing Completed.')    
    print('Images can be found in ' + str(save_path))
    subprocess.run(['explorer', os.path.realpath(save_path)]) # optional for OSX

#GUI
ttk.Label(root, text='Image to JPG').grid(row=0, column=0, padx=20, pady=5, sticky='ew')
ttk.Label(root, text='Programmer: Neil C. Salazar').grid(row=5, column=0, padx=20, pady=4, sticky='ew')
ttk.Label(root, text='Email: salazar.neil@gmail.com').grid(row=6, column=0, padx=20, pady=4, sticky='ew')
ttk.Button(root, text="Open files", command=open_files).grid(row=1, column=0, padx=20, pady=4, sticky='ew')
ttk.Label(root, text='Supported file types, jfif, webp, png, jpeg, jpg, gif').grid(row=3, column=0, padx=20, pady=4, sticky='ew')

root.mainloop()


