#to make a text editor in custom tkinter
#cmd- E:\CMPSCI\PYTHON\PROJECTS\tkinter_1\ctk_text_editor_final.py
#DEVELOPED BY ANSHUMAN PATTNAIK
#icon[s]_atttribution-'https://www.flaticon.com'
#import all libaries
from tkinter import *
import customtkinter
from PIL import Image
import os
from tkinter import filedialog
from tkinter import messagebox

#---------apperance_theme of the $WINDOW---------
customtkinter.set_appearance_mode("dark")  # Modes: system (default), light, dark
customtkinter.set_default_color_theme("green")  # Themes: blue (default), dark-blue, green

#---------to create the initial attributes of the $WINDOW---------
window = customtkinter.CTk()  # create CTk window like you do with the Tk window
window.title('PEAT') #-PYTHON_EDITOR_AND_TERMINAL-
window.geometry("975x550")
window.minsize(680,550)
#to set window_icon
image=PhotoImage(file='E:\CMPSCI\Requiredfiles\Light-1.png')
window.iconphoto(TRUE,image)

#---------initial_$WINDOW_CLOSE()---------

#to create a folder to store all the files
folder_path="D:\python_txt_editor"
os.makedirs(folder_path, exist_ok=True) #not_make_$os.mkdir
#to save all the saved text into Notepad file [main_sheet.txt]
main_sheet="D:\python_txt_editor\main_sheet.txt"
with open(main_sheet,'a') as file_object_1:
  file_object_1.write("")
#_to make the pyhon[.py] file which will carry the main user coding
py_sheet="D:\python_txt_editor\code_sheet.py"
with open(py_sheet,'w') as file_object_2:
  file_object_2.write("#python_sucessfull_install: 100%\n")
#_to make the terminal_batch[.bat] file
terminal_sheet="D:\python_txt_editor\Terminal_sheet.bat"
with open(terminal_sheet,'w') as file_object_6:
  file_object_6.write("@echo off\nstart D:\python_txt_editor\code_sheet.py")
#_to close the terminal window after the user desires
time_sleep=0
# to import all the icons[.png] required for the change of the $appearance_mode
image_location_bright='E:\CMPSCI\Requiredfiles\Light-1.png' #Brightness.png _ View.png_Light.png_Light-1.png
image_location_dark='E:\CMPSCI\Requiredfiles\Dark-mode.png'
icon_size = 28
image_original=customtkinter.CTkImage(light_image=Image.open(image_location_dark),dark_image=Image.open(image_location_bright),size=(icon_size,icon_size))

#------------$def()_button[s]_actions------------
#to save file into the mainsheet
def sv_file():
  with open(main_sheet,'w') as file_object_3:
   file_object_3.write(text.get(1.0,END)) #(237.0,END)for not including the documentation
  with open(py_sheet,'w') as file_object_7:
   file_object_7.write(text.get(1.0,END))
  print("$sucessfully_saved_the_file_in_dir!")
#to undo the text area
def undo_file(): #-not_activated-
  with open(main_sheet,'w') as file_object_4:
   file_object_4.write(text.get(1.0,END))
  print("$sucessfully_undo_the_file!")  
#to clear the text area
def clr_file():
  if messagebox.askyesno(title="peat: clear-q",message="Do you want to clear the coding area?",icon='warning'):
      text.delete("1.0", "end")
      print("$clear_msg_input(): GRANTED")
  else:
      print("$clear_msg_input(): DENIED")
#to load the existing value in the mainsheet in the text area
def ld_file():
  if messagebox.askyesno(title="peat: load-q",message="Do you want to load from the saved file?",icon='warning'):
    with open(main_sheet) as file_object_5:
     text_insert_n=str(file_object_5.read())
     print("$load_msg_input(): GRANTED")
     text.insert(322.0,text=text_insert_n,tags=None) #322.0
  else :
     print("$load_msg_input(): DENIED")
#to open the batch file[Terminal_sheet.bat]
def trm_file():
  global time_sleep
  time_sleep+=1
  if time_sleep == 1:
   length_tw=float(len(text.get(1.0,END)))
   text.insert(length_tw,text="\nprint(\"exit() - terminate terminal\")\ninput()",tags=None)
  print(time_sleep)
  sv_file()
  os.system(terminal_sheet)
  print("$sucessfully_opened_terminal !")
#to open any text file user wants to open and paste in the $text_area
def open_file():
  global time_sleep
  time_sleep = 0
  file_path=filedialog.askopenfilename(title="$py_select_file")#filetypes=("text files","*.txt"
  print("$file_path: "+str(file_path))
  with open(file_path) as file_object_7:
    file_content=str(file_object_7.read())
    index_text_insert=float(len(text.get(1.0,END)))
    print("$text_area_length: "+str(index_text_insert+1))
    text.insert(index_text_insert,text=file_content,tags=None)
  messagebox.showinfo(title='peat: open-i',message="Sucessfully opened the file !")
#to save a file derivated from the $text_area and save it in a desired location
def sv_as_file():
  file_sv=filedialog.asksaveasfile(title="$py_save_as_file")
  file_text=str(text.get(1.0,END))
  print("$sucessfully_saved_tw: "+str(file_sv)+" !")
  file_sv.write(file_text)
  messagebox.showinfo(title='peat: save_as-i',message="Sucessfully saved the file !")
#to hold non_executable statement in window_main
if 1>2:
  label_nexe=customtkinter.CTkLabel(window,text="$python text_editor_ANSHP",font=("sans serif",8,b"bold"),text_color="grey").grid(row=0,column=1)
  label_nexe.pack()
#to change the value of the $appearance_mode
#--------ASSETS_COLOR--------
# dark_grey:       "#474746"
# light_blue:      "#506ba1"
# white:           "white"
# dark_green:      "#90c213"
# light_tone_grey: "#525150"
# light_dark_grey: "#adaba8"
#----------------------------
def mode_function(mode_argument):
    customtkinter.set_appearance_mode(mode_argument) 
mode_value= TRUE
def appear():
    global mode_value
    if  mode_value:
        mode_function("light")
        #to modify $textbox_text_colour_light-mode
        text.configure(text_color="#474746")
        #to modify $button[s]_text_color_light-mode
        button_1.configure(text_color="#506ba1")
        button_2.configure(text_color="#506ba1")
        button_3.configure(text_color="#506ba1")
        button_4.configure(text_color="#506ba1")
        button_5.configure(text_color="#506ba1")
        #to modify $button[s]_hover_colour_light-mode
        button_1.configure(hover_color="white")
        button_2.configure(hover_color="white")
        button_3.configure(hover_color="white")
        button_4.configure(hover_color="white")
        button_5.configure(hover_color="white")
        #---------button_6_undo_not-activated----------
        if 1 > 2:
         button_6.configure(hover_color="white")
         button_6.configure(text_color="#506ba1")
        #----------------------------------------------
        mode_value= FALSE
        print("$set_appearance_mode: LIGHT")
    else:
        mode_function("dark")
        #to modify $textbox_text_colour_dark-mode
        text.configure(text_color="#90c213")
        #to modify $button[s]_text_color_dark-mode
        button_1.configure(text_color="#adaba8")
        button_2.configure(text_color="#adaba8")
        button_3.configure(text_color="#adaba8")
        button_4.configure(text_color="#adaba8")
        button_5.configure(text_color="#adaba8")
        #to modify $button[s]_hover_colour_dark-mode
        button_1.configure(hover_color="#525150")
        button_2.configure(hover_color="#525150")
        button_3.configure(hover_color="#525150")
        button_4.configure(hover_color="#525150")
        button_5.configure(hover_color="#525150")
        #---------button_6_undo_not-activated----------
        if 1 > 2:
         button_6.configure(hover_color="#525150")
         button_6.configure(text_color="#adaba8")
        #----------------------------------------------
        mode_value = TRUE
        print("$set_appearance_mode: DARK")



#---------top-$frame-contain-$label_$button[s]---------
frame=customtkinter.CTkFrame(window,corner_radius=9,height=550,width=600)#,border_width=10,border_color="yellow")fg_color="#455A64
frame.place(x=0,y=0)
frame.pack(side=TOP,pady=10,padx=45) #expand=TRUE

# $label_frame_store_text
label=customtkinter.CTkLabel(frame,text="  $python_version_3.11\t",font=("sans serif",12,"italic"),text_color="grey")
label.pack(side=LEFT)
label=customtkinter.CTkLabel(frame,text="\t")
label.pack(side=RIGHT)

#---------eidt-frame_$button[s]-attributes---------
font_b="arial"
font_size=16
font_colour="#adaba8" 
button_colour="transparent"
hover_colour="#525150" 
px=3 #padx_button_s
py=0 #pady_button_s
c_radius=9 #corner_radius
h=5 #height_button
w=5 #width_button


#---------$define_button--------------
#button_Open()
button_1=customtkinter.CTkButton(frame,command=open_file,text="Open",font=(font_b,font_size),text_color=font_colour,fg_color=button_colour,hover_color=hover_colour,corner_radius=c_radius,height=h,width=w)
button_1.pack(side=LEFT,padx=px,pady=py)
#button_$set_appearance_mode()_fill=image
button_appear=customtkinter.CTkButton(frame,command=appear,text="",image=image_original,fg_color="transparent",hover_color=hover_colour,corner_radius=c_radius,height=h,width=w)
button_appear.pack(side=RIGHT,padx=px,pady=py)
#button_Terminal()
button_run=customtkinter.CTkButton(frame,command=trm_file,text=" Run ",font=(font_b,font_size),text_color="white",fg_color="#506ba1",hover_color=hover_colour,corner_radius=9,height=h,width=w)
button_run.pack(side=RIGHT,padx=px,pady=py)
#button_Load()
button_2=customtkinter.CTkButton(frame,command=ld_file,text="Load",font=(font_b,font_size),text_color=font_colour,fg_color=button_colour,hover_color=hover_colour,corner_radius=c_radius,height=h,width=w)
button_2.pack(side=RIGHT,padx=px,pady=py)
#button_Save()
button_3=customtkinter.CTkButton(frame,command=sv_file,text="Save",font=(font_b,font_size),text_color=font_colour,fg_color=button_colour,hover_color=hover_colour,corner_radius=c_radius,height=h,width=w)
button_3.pack(side=LEFT,padx=px,pady=py)
#button_Clear()
button_4=customtkinter.CTkButton(frame,command=clr_file,text="Clear",font=(font_b,font_size),text_color=font_colour,fg_color=button_colour,hover_color=hover_colour,corner_radius=c_radius,height=h,width=w)
button_4.pack(side=RIGHT,padx=px,pady=py)
#button_Save_As()
button_5=customtkinter.CTkButton(frame,command=sv_as_file,text="Save_As",font=(font_b,font_size),text_color=font_colour,fg_color=button_colour,hover_color=hover_colour,corner_radius=c_radius,height=h,width=17)
button_5.pack(side=LEFT,padx=0,pady=py)
#button_Undo()
if 1>2: #button_Undo()-not_activated
 button_6=customtkinter.CTkButton(frame,command=undo_file,text="Undo",font=(font_b,font_size),text_color=font_colour,fg_color=button_colour,hover_color=hover_colour,corner_radius=c_radius,height=h,width=w)
 button_6.pack(side=RIGHT,padx=px,pady=py)

#--------------Text_editor_area-------------
#text_attributes
#--------fonts_used-------
#0-Lucida Sans Typewriter
#1-courier new
#2-conslas - used by vs_code_default_font
#3-ludica console
#------------------------
font_tw=["Lucida Sans Typewriter","courier new","consolas","ludica console"]
font_index=2 #choose from the $list_font_tw
font_size_tw= 1.0
#--------fonts_color--------
#0-dark_grey:  "#474746"
#1-dark_green: "#90c213"
#2-light_mode: "#c6c7c3"
#3-light_grey: "#918e90"
#4-light_blue: "#506ba1"
#5-white:      "white"
#6-yellow:     "yellow"
#--------------------------
color_tw=["#474746","#90c213","#c6c7c3","#918e90","#506ba1","white","yellow"]
font_color_index=1 #choose from the $list_color_tw
#--------fonts_style--------
#0-normal: normal weight
#1-bold: boldface text
#2-italic: italized text
#3-underline: underlined text
#4-roman: regular slant
#5-overstrike: struck-out text NOTE:it may not work on some systems
#----------------------------
font_style_tw=["normal","bold","italic","underline","roman","overstrike "]
font_style_index=0 #choose from the $list_color_tw
#text_window_attributes 
height_tw=1060 
width_tw=1920
cornor_radius_tw=9
text_color_index= 0
border_width_tw=3 #$ not_activated
border_color_tw="grey"#$ not_activated
px=11
py=11
text_insert="# PYTHON_EDITOR_AND_TERMINAL\n\n# Hello There! this is an open source $python_text_editor made by Anshuman Pattnaik \n\n# To know about the principles of $python please type 'import this' - 'The Zen of Python' by Tim Peters \n\n# NOTE:- input() appears to prevent the abrupt terminaton of the terminal\n\n# The developer wishes you Happy Coding :-)\n#-----------------------------------------------\n"


text=customtkinter.CTkTextbox(window,font=(font_tw[font_index],font_size,font_style_tw[font_style_index]),text_color=color_tw[font_color_index],height=height_tw,width=width_tw,corner_radius=cornor_radius_tw)#,fg_color="transparent")#,border_width=border_width_tw,border_color=border_color_tw)
text.insert(1.0,text=text_insert,tags=None)
text.pack(padx=px,pady=py)

#index, text, tags=None
e=1
if e<2:
 e+=1
 print("$sucessfully_opened_window !")
 print("$tw_length: "+str(len(text.get(1.0,END))))



window.mainloop()