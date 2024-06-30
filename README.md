# RESUME FILTERING

import os
import fitz  # PyMuPDF

def extract_text_from_pdf(file_path):
    doc = fitz.open(file_path)
    full_text = []
    for page_num in range(len(doc)):
        page = doc.load_page(page_num)
        full_text.append(page.get_text())
    return '\n'.join(full_text)

def resume_contains_keywords(resume_text, keywords):
    return any(keyword.lower() in resume_text.lower() for keyword in keywords)

def get_matching_resumes(resume_folder, keywords):
    matching_resumes = []
    for resume_file in os.listdir(resume_folder):
        if resume_file.endswith('.pdf'):
            resume_path = os.path.join(resume_folder, resume_file)
            resume_text = extract_text_from_pdf(resume_path)
            if resume_contains_keywords(resume_text, keywords):
                matching_resumes.append(resume_file)
    return matching_resumes

def main():
    resume_folder = 'C:\\Users\\simar\\OneDrive\\Desktop'  # Folder containing the resumes
    keywords = ['Python', 'Data Analysis', 'DSA']  # Keywords to match

    matching_resumes = get_matching_resumes(resume_folder, keywords)
    
    if matching_resumes:
        print('Matching Resumes:')
        for resume in matching_resumes:
            print(resume)
    else:
        print('No matching resumes found.')

if __name__ == "__main__":
    main()








# AI-DRIVEN VOICE ASSISTANT

import pyttsx3
import speech_recognition as sr
import datetime
import wikipedia
import webbrowser
import pywhatkit as wk
import os
import pyjokes
import pyautogui 
import sys

engine=pyttsx3.init('sapi5')
voices=engine.getProperty('voices')
engine.setProperty('voice',voices[0].id)
engine.setProperty('rate', 200)

def speak(audio):
    engine.say(audio)
    engine.runAndWait()

def wishMe():
    hour=int(datetime.datetime.now().hour)
    if hour>=0 and hour<12:
        speak("Good Morning Simar")
    elif hour>=12 and hour<18:
        speak("Good Afternoon Simar")
    else:
        speak("Good evening Simar")
    speak("Ready to go. How can i help you")

def takeCommand():
    r=sr.Recognizer()
    with sr.Microphone()as source:
      print("Listening...")
      r.pause_threshold=1
      audio=r.listen(source)

    try:
        print("Recognizing...")
        query=r.recognize_google(audio,language='en-in')
        print(f"User said: {query}\n")

    except Exception as e:
        print("Say that again please...")
        return "None"

    return query

if __name__=="__main__":
    wishMe()
    while True:
        query=takeCommand().lower()
        if 'jarvis' in query:
            print("Yes ,Simar")
            speak("Yes Simar")

        elif "who are you" in query:
            print("Namaste, i am jarvis , a personal voice assistant for Simar. She is my best friend")
            speak("Namaste, i am jarvis , a personal voice assistant for Simar. She is my best friend")

        elif 'what is' in query:
            speak("Searching wikipedia...")
            query=query.replace("what is","")
            results=wikipedia.summary(query,sentences=4)
            speak("according to wikipedia")
            print (results)
            speak(results)

        elif 'just open youtube' in query:
            webbrowser.open('youtube.com')

        elif 'open youtube' in query:
            speak("what will you like to watch ?")
            qrry=takeCommand().lower()
            wk.playonyt(f"{qrry}")

        elif 'just open google' in query:
            webbrowser.open('google.com')

        elif 'open google' in query:
            speak("What should i search")
            qry=takeCommand().lower()
            webbrowser.open(f"{qry}")
            results=wikipedia.summary(qry,sentences=4)
            speak(results)

        elif 'crack a joke' in query:
            speak(pyjokes.get_joke())

        elif 'close browser' in query:
            os.system("taskkill /f /iim msedge.exe")

        elif 'close google' in query:
            os.system("taskkill /f /im chrome.exe")
        elif 'type' in query:
            query=query.replace("type","")
            pyautogui.typewrite(f"{query}",0.1)
        elif 'open chrome' in query:
            os.startfile('C:\Program Files\Google\Chrome\Application\chrome.exe')
        elif 'maximize this window' in query:
            pyautogui.hotkey('alt','space')
            time.sleep(1)
            pyautogui.press('x')
        elif'google search' in query:
            query=query.replace("google search","")
            pyautogui.hotkey('alt','d')
            puautogui.write(f"{query}",0.1)
            pyautogui.press('enter')
        elif 'youtube search' in query:
            query=query.replace("youtube search","")
            pyautogui.hotkey('alt','d')
            time.sleep(1)
            pyautogui.press('tab')
            pyautogui.press('tab')
            pyautogui.press('tab')
            pyautogui.press('tab')
            time.sleep(1)
            pyautogui.wwrite(f"{query}",0.1)
            pyautogui.press('enter')
        elif 'open new window' in query:
            pyautogui.hotkey('ctrl','n')
        elif 'minimize this window' in query:
            pyautogui.hotkey('alt','space')
            time.sleep(1)
        elif 'open history' in query:
            pyautogui.hotkey('ctrl','h')
        elif 'open downloads'in query:
            pyautogui.hotkey('ctrl','j')
        elif 'previous tab in query':
            pyautogui.hotkey('ctrl','shift','tab')
        elif 'next tab' in query:
            pyautogui.hotkey('ctrl','tab')
        elif 'close tab in query':
            pyautogui.hotkey('ctrl','w')
        elif 'clodse window' in query:
            pyautogui.hotkey('ctrl','shift','w')
        elif 'clear browsing history' in query:
            pyautogui.hotkey('ctrl','shift','delete')
        elif 'close chrome' in query:
            os.system("taskill /f /im chrome.exe")
        elif 'go to sleep' in query:
            speak("Alright the, i am switching off")
            sys.exit()
        elif 'take screenshot' in query:
            speak("Tell me the name of file")
            time.sleep(3)
            img=pyautogui.screenshot()
            img.save(f"{name}.png")
            speak("screenshot saved")
        elif 'shut dowm the system' in query:
            os.system("shutdown /r /t 5")
        elif 'restart the system' in query:
            os.system("shutdown /r /t 5")
            
            
            
