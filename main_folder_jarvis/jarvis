import pyttsx3
import datetime
import speech_recognition as sr
import wikipedia
import webbrowser
import pyautogui as pg
import time
import os
import smtplib
import requests
from bs4 import BeautifulSoup
from word2number import w2n

def instruction():
    print('''
    ####### COMMANDS_OF_JERVIS ########
    1) SEARCH IN WIKIPEDIA .YOU SHOULD HAVE TO INCLUDE WIKIPEDIA TO THE SEARCH YOU WANT TO GET
    2) SEARCH IN GOOGLE .YOU SHOULD HAVE TO INCLUDE THE WORLD "GOOGLE" FOR SEARCHING
    3) OPEN {YOUTUBE,GOOGLE,STACKOVERFLOW,WHATS_APP}
    4) PLAY MUSIC
    5) FAVOURITE SONG : TO LISTEN YOUR LIKED SONGS IN SPOTIFY
    6) STOP SONG
    7) PLAY AGAIN
    8) INCREASE VOLUME
    9) DECREASE VOLUME
    10) MUTE
    11) TIME
    12) TEMPERATURE

    ''')

'''CODE STARTED FROM HERE : '''

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')

def speak(audio):
    engine.say(audio)
    engine.runAndWait()

def wishMe():
    hour = int(datetime.datetime.now().hour)
    if hour >= 0 and hour < 12:
        speak('Good morning sir! ')
    elif hour >= 12 and hour < 18:
        speak('Good Afternoon sir!')
    else:
        speak("Good evening sir! ")
    speak('I am jervis, how can i help you !')
    speak('Sir ! you can get the list of commands bellow : Thanks , Ask what you need !!')

def takeCommand():
    '''It takes microphone input from user and returns output'''
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print('Listening......')
        r.pause_threshold = 1
        audio = r.listen(source)
    try:
        print("Recognizing....")
        query = r.recognize_google(audio, language='en-in')
        print(f'User said: {query}\n')
    except Exception as e:
        print('Say that again please....')
        return "None"

    return query

def takeCommand_song():
    speak('Name the song you want to listen')
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print('Listening......')
        r.pause_threshold = 1
        audio = r.listen(source)
    try:
        print("Getting song name....")
        song_name = r.recognize_google(audio, language='en-in')
        print(f'User said: {song_name}\n')

    except Exception as e:
        print('Say that again please....')
        return None
    return song_name

if __name__ == '__main__':
    wishMe()
    instruction()
    p = True
    while p:

        query = takeCommand().lower()
        if 'wikipedia' in query:
            speak('Searching Wikipedia...')
            query = query.replace('wikipedia', '')
            results = wikipedia.summary(query, sentences=2)
            speak('According to wikipedia')
            speak(results)
            print(results)

        elif 'google' in query:
            query = query.replace('in google', '')
            webbrowser.open(f'https://www.google.com/search?q={query}')

        elif 'open youtube' in query:
            webbrowser.open('youtube.com')

        elif 'open google' in query:
            webbrowser.open('google.com')

        elif 'open stack overflow' in query:
            webbrowser.open('stackoverflow.com')
    
        elif 'music' in query:
            song_name = takeCommand_song()
            time.sleep(3)
            webbrowser.open(f'https://open.spotify.com/search/{song_name}')
            time.sleep(4)
            pg.leftClick(1199, 459, 1, 1)

        elif 'favourite song'in query:
            speak('Ok sir, I am playing songs from you liked songs')
            webbrowser.open('https://open.spotify.com/collection/tracks')
            time.sleep(4)
            pg.leftClick(450, 743, 1,2 )

        elif 'stop song' in query:
            speak('Ok sir, I am pausing song !!')
            time.sleep(1)
            pg.press('space')

        elif 'play again' in query:
            speak('Ok sir !')
            pg.press('space')
        elif 'close' in query:
            speak('Ok sir , I am shutting down my self !!')
            p = False
            break

        elif 'time' in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f'Sir the time is {strTime}')

        elif 'open code' in query:
            try:
                codePath = 'C:\\Users\\bipra\\AppData\\Roaming\\Microsoft\\Windows\\Start Menu\\Programs\\Code.exe'
                os.startfile(codePath)
            except Exception as e:
                speak('Location not found !! ')
                continue

        elif 'increase volume' in query:
            pg.press('volumeup')

        elif 'decrease volume' in query:
            pg.press('volumedown')

        elif 'mute' in query:
            pg.press('volumemute')

        elif 'temperature' in query:
            search = 'Temperature in Tripura'
            url = f'https://www.google.com/search?q={search}'
            r = requests.get(url)
            data = BeautifulSoup(r.text,"html.parser")
            temp = data.find("div",class_='BNeawe').text
            speak(f'current {search} is {temp}')

        elif 'whatsapp' in query:
            webbrowser.open('https://web.whatsapp.com/')
        
