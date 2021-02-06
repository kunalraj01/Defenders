# Defenders
import pyttsx3
import speech_recognition as sr
import datetime
import wikipedia
import webbrowser
import os
import smtplib
import time
import cv2
import numpy as np
import pyzbar.pyzbar as pyzbar
import base64
import sys
import time
import datetime
import xlwt

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
#print(voices[0].id)
engine.setProperty('voice',voices[0].id)


def speak(audio):

    engine.say(audio)
    engine.runAndWait()

    



def wishMe():

    speak(" starting all system and application ....... All system have been started , i am eva 0.2 version. your artifical intelligence ")  
    
    hour = int(datetime.datetime.now().hour) 
    if hour>= 0 and hour<12: 
         speak("Good Morning kunal ! , how may i help you ") 
   
    elif hour>= 12 and hour<18: 
         speak("Good Afternoon kunal ! , how may i help you")    
   
    else: 
         speak("Good Evening kunal ! , how may i help  you ") 

    

     
    
              

def takecommand():
    #it takes microphone input from the user and returns strings output

    r = sr.Recognizer()
    with sr.Microphone() as source:
         print("listening....")
         r.pause_threshold = 1
         audio = r.listen(source)

    try:
         print("recognizing....")
         query = r.recognize_google(audio, language = 'en-in')
         print(f"user said: {query}\n")
 

    except Exception as e:

         #print(e)
 
         print("say that again please.....")
    
         return "None" 

    return query

def sendEmail(to, content):
     server = smtplib.SMTP('smtp.gmail.com', 587)
     server.ehlo()
     server.starttls()
     server.login('kunalworkshop0106@gmail.com','***************')
     server.sendmail('kunalworkshop0106@gmail.com', to, content)
     server.close()





if __name__ == "__main__":
    wishMe()
       
    while True:
    
    #if 1 :
       
          
        query = takecommand().lower() 
          
        # All the commands said by user will be  
        # stored here in 'query' and will be 
        # converted to lower case for easily  
        # recognition of command
        if 'wikipedia' in query: 
             speak('Searching Wikipedia...') 
             query = query.replace("wikipedia","")
             results = wikipedia.summary(query, sentences = 3) 
             speak("According to Wikipedia")  
             print(results) 
             speak(results) 

        
        elif 'open youtube' in query: 
             speak("Here you go to Youtube\n") 
             webbrowser.open("youtube.com") 
  
        elif 'open google' in query:  
             speak("Here you go to Google\n") 
             webbrowser.open("google.com") 
        
       

        elif 'open D '  in query:
             Dpath = " D:\\ "
             os.startfile(Dpath)

        elif 'open E ' in query :
             Epath = ' E:\\'
             os.startfile(Epath) 

        elif 'open C ' in query :
             Cpath = 'C:\\'
             os.startfile(Cpath)    

       


        elif 'play music' in query or "play song" in query: 
             speak("Here you go with songs") 
             music_dir = 'D:\\songs'
             songs = os.listdir(music_dir) 
             print(songs) 
             random = os.startfile(os.path.join(music_dir, songs[1])) 

        
        elif 'the time' in query: 
             strTime = datetime.datetime.now().strftime("%H:%M:%S")     
             speak(f"Sir, the time is {strTime}")

        elif 'open visual studio code' in query  or 'open code ' in query :
             codepath = "C:\\Microsoft VS Code\\Code.exe" 
             os.startfile(codepath)


        elif 'send mail to shivam' in query :
            try:
                speak("what should i say")
                content = takecommand()
                to = "royshivam5612@gmail.com"

                sendEmail(to, content)
                speak("Email has been sent !")

            except Exception as e:
                print(e)
                speak("sorry my friend . i am not able to snd this email") 

        elif 'send email' in query:
            try: 
                speak("What should I say?") 
                content = takecommand() 
                speak("whome should i send") 
                to = input()     
                sendEmail(to, content) 
                speak("Email has been sent !") 
            except Exception as e: 
                print(e) 
                speak("I am not able to send this email") 

        elif 'Telegram Desktop' in query or 'open telegram' in query:
             Telegrampath = "C:\\Telegram Desktop\\Telegram.exe"
             os.startfile(Telegrampath) 

        #elif "camera" in query or "take a photo" in query: 
           # ec.capture(0, "eva Camera ", "img.jpg")     

          
        elif "tell me the time" in query or "what is the time"  in query: 
             telltime()
             continue
          
        # this will exit and terminate the program 
        elif "bye" in query or "eva bye" in query or " talk u later " in query or "offline" in query: 
             speak("Bye  !  sir ") 
             exit()


        elif "tell me your name" in query: 
             speak("I am eva. Your deskstop Assistant") 


        elif "who made you" in query or "who create you" in query or "who is your father" in query:
             speak("in short i call him KR, DO YOU WANT TO KNOW, how is? FIND YOUR SELF! ha ha ha  !!!")

        elif "hello eva" in query or "hello" in query or "namaste" in query or "hye" in query or "hii" in query :
             speak("hello sir !")
             print("kunal sir")

        

        elif "good moring eva" in query or " good morning" in query :
             speak ("good morning sir !")

        elif "good evening eva" in query or "good evening" in query:
             speak("good evening sir !")

        elif " good afternoon eva" in query or " good afternoon" in query:
             speak (" good afternoon sir !") 

        elif "good night eva" in query or "good night" in query:
             speak("good night sir , have a good sleep dude !")
             exit()


       


        elif "shutdown the computer" in query or "switch off the computer" in query or "shutdown" in query:
             speak("DO you want to shutdown your computer sir ?")
             while True:
                  command = takecommand()
                  if "no" in command:
                       speak("thank you sir i will not shutdown the system ") 
                       break

                  if "yes" in command:
                       # shutting down
                       command.speak("shutting the computer")
                       os.system("shutdown /s /t 30")
                       speak("ok sir ! i shutdown the computer")
                       break

        elif "open qr scanner" in query:
            # starting the webcam using opencv 
cap = cv2.VideoCapture(0)

fob=open('attendence.txt','w+')

names=[]

#function for writing the data into text file
def enterData(z):
    if z in names:
        pass
    else:
        names.append(z)
        z=''.join(str(z))
        fob.write(z+'\n')
    return names

print('Reading...')
#function for check the data is present or not
def checkData(data):
    data=str(data)    
    if data in names:
        print('Already Present')
    else:
        print('\n'+str(len(names)+1)+'\n'+data)
        enterData(data)
  
while True:
    _, frame = cap.read() 
    decodedObjects = pyzbar.decode(frame)
    for obj in decodedObjects:
        checkData(obj.data)
        time.sleep(1)
       
    cv2.imshow("Frame", frame)

    #closing the program when s is pressed
    if cv2.waitKey(1)& 0xFF == ord('s'):
        cv2.destroyAllWindows()
        break
    
fob.close()





    
  

                       

          

                    
                      
          
             

     








                           


                                    



               



        


                     


                

          
            

        

             

      









    


