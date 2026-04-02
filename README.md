# jarvis-virtual-voice-assistant
Jarvis is a voice-controlled virtual assistant that uses speech recognition and text-to-speech to interact with users. It can perform tasks like opening applications, searching the web, providing real-time information, and executing basic system commands. 
import speech_recognition as sr
import webbrowser
import pyttsx3
import musiclibrary

recognizer = sr.Recognizer()
engine = pyttsx3.init()

def speak (text):
    engine.say(text)
    engine.runAndWait()

def ProcessCommand(c):
    if "open google" in c.lower():
        webbrowser.open("https://google.com")
    elif "open you tube" in c.lower():
        webbrowser.open("https://youtube.com")
    elif "open facebook" in c.lower():
        webbrowser.open("https://facebook.com")
    elif c.lower().startswith("play"):
        song = c.lower().split(" ")[1]
        link =musiclibrary.music[song]
        webbrowser.open(link)
 

if __name__ == "__main__":
    speak("initializing jarvis...")


    while True:
        #listen for make the word "jarvis"
        # obtain audio form microphone
        r = sr.Recognizer()


        print("recognizing..")
        # recognize speech using sphinx
        try:
            with sr.Microphone() as source:
                print("listening...")
                audio = r.listen(source, timeout=2, phrase_time_limit=2)
            word = r.recognize_google(audio)
            if "jarvis" in word.lower():
                speak("Ya")

                with sr.Microphone() as source:
                    print("jarvis active...")
                    audio = r.listen(source)
                    command = r.recognize_google(audio)

                    ProcessCommand(command)
        except Exception as e:
            print("Error;{0}".format(e))
