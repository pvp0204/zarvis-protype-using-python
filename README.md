# zarvis-protype-using-python
from distutils.util import strtobool
from doctest import master
#from lib2to3.pytree import _Results
from logging import exception
from nturl2path import url2pathname
from xml.dom import minicompat
import pyttsx3
import speech_recognition as sr
import datetime
import wikipedia
import webbrowser
import os
import smtplib
import pyaudio
 
print("Intialization Jarvis")

master = "hello sir"
 
engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
engine.setProperty('voice',voices[0].id)
 
 #speal function will pronounce the string
 
def speak(text):
     engine.say(text)
     engine.runAndWait()
     
def wishme():
    hour = datetime.datetime.now().hour
    #print(hour) 
    
    
    if hour>=0 and hour<12:
        speak("good morning" + master)
    elif hour>=12 and hour<16:
        speak("afternoon" + master)
    elif hour>=16 and hour<19:
        speak("good evening" + master)
    else:
        speak("good night" + master)
        
    speak("i am zarvis. how may i help you?")
    
def takecommand():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("listening...")
        speak("listening...")
        audio = r.listen(source)
        
    try :
        print("recognizing...")
        speak("recognizing...")
        query = r.recognize_google(audio,language = 'en-in')
        print(f"user said: {query}\n")
        
    except exception as e:
        print("say that again")
        query = None
    return query
    
# main functons start here..
speak("intializing zarvis....")
wishme()
query = takecommand()

# logic for execting basic task
if "wikipedia" in query.lower():
    speak('searchng wikipedia...')
    query = query.replace("wikipedia","")
    results= wikipedia.summary(query, sentences = 2)
    print(results)
    speak(results) 
    
elif 'open youtube' in query.lower():
    webbrowser.open("youtube.com")
    
    
if 'open google' in query.lower():
    webbrowser.open("google.com")
    

#elif'paly music' in query.lower():
    #songs = os.listdir("C:\Users\acer\Music")
    #print(songs)
    #os.startfile(os.path.join(songs_dir,songs[0]))
    
elif 'the time' in query.lower():
    strTime = datetime.datetime.now().strftime("%H:%M:%S")
    speak(f"{master} the time is {strTime}")

#elif 'open code' in query.lower():
    #codePath = "none\\code.exe"
    #os.startfile(codePath)    
