from distutils import command

import speech_recognition as sr
import pyttsx3
import datetime
import pywhatkit


listener = sr.Recognizer()
friday = pyttsx3.init()
voices = friday.getProperty('voices')
friday.setProperty('voice', voices[1].id)

def talk(text):
    friday.say(text)
    friday.runAndWait()
def  take_command():

    try:

        with sr.Microphone() as source:
            print('listening....')
            voice = listener.listen(source)
            command = listener.recognize_google(voice)
            command = command.lower()
            if 'friday' in command:
                command = command.replace('friday', '')
    except:
        pass

    return command

def run_friday():
    command = take_command()
    if 'time' in command:
        time = datetime.datetime.now().strftime('%H:%M')
        print(time)
        talk('boss current time is '+time)
    elif 'play' in command:
        song = command.replace('play', '')
        talk('playing' + song)
        pywhatkit.playonyt(song)



run_friday()
