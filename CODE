from chatterbot import ChatBot
from chatterbot.trainers import ChatterBotCorpusTrainer
import PIL
from PIL import ImageTk
import PIL.Image
import pyttsx3 as pp
import threading
import speech_recognition as s

engine=pp.init()      #it will initialize pyttsx3 module
voices=engine.getProperty('voices')
print(voices)
engine.setProperty('voice',voices[0].id)    #voices[0] means we will get response in the form of male voice

def speak(word):
    engine.say(word)
    engine.runAndWait()

from tkinter import *
bot = ChatBot(" Olive")


bot.set_trainer(ChatterBotCorpusTrainer)
bot.train("chatterbot.corpus.english")


main=Tk()



main.geometry("600x450")

main.title("My chat bot")
img =ImageTk.PhotoImage(PIL.Image.open("image.png"))
photoL=Label(main, image=img)
photoL.pack(side=LEFT,pady=5)

#takey query : it takes audio as input from user and convert it into string

def takeQuery():
    sr=s.Recognizer()
    sr.pause_threshold=1
    with s.Microphone() as m:
       try:
           audio = sr.listen(m)
           query = sr.recognize_google(audio, language='eng-in')
           print(query)
           textF.delete(0, END)
           textF.insert(0, query)
           ask_from_bot()
       except Exception as e:
           print("not recognized")

def ask_from_bot():

    query=textF.get()
    if query == 'what is your name?':
         answer= 'My name is olive'

    elif query == 'bye':
        answer = 'bye'

    elif (query == 'hi' or query == 'hii' or query == 'hello'):
        answer = 'hi'

    elif query == 'how are you':
        answer = 'I am fine.How are you?'


    else:
         answer=bot.get_response(query)
    msgs.insert(END,"user:" + query)
    msgs.insert(END,"bot:" + str(answer))
    speak(answer)
    textF.delete(0, END)
    msgs.yview(END)

frame=Frame(main)
sc=Scrollbar(frame)
msgs=Listbox(frame,width=80,height=20,yscrollcommand=sc.set)
sc.pack(side=RIGHT ,fill=Y)
msgs.pack(side=RIGHT ,fill= BOTH,pady=10)
frame.pack()
textF=Entry(main,font=("verdana",20))
textF.pack(fill=X,pady=10)
btn=Button(main,text="Ask from bot",font=("verdana",20),command=ask_from_bot)
btn.pack()

#creating a function for enter.when we will bind it at that time it will get the object for event

def enter_function(event):
    btn.invoke()

#Bind main window with enter key

main.bind('<Return>',enter_function)

def repeat():
    while True:
        takeQuery()

#we are calling takeQuery in second thread by doing this it won't affect your GUI and this function will also be called


t=threading.Thread(target=repeat)
t.start()
main.mainloop()
