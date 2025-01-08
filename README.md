- 👋 Hi, I’m @Hamidgharah
- 👀 I’m interested in rap

- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Hamidgharah/Hamidgharah is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

import cv2
import speech_recognition as sr
import pyttsx3
from geopy.geocoders import Nominatim

engine = pyttsx3.init()

def speak(text):
    engine.say(text)
    engine.runAndWait()

def recognize_speech():
    recognizer = sr.Recognizer()
    with sr.Microphone() as source:
        print("لطفاً صحبت کنید...")
        audio = recognizer.listen(source)
        try:
            text = recognizer.recognize_google(audio, language='fa-IR')
            print(f"شما گفتید: {text}")
            return text
        except sr.UnknownValueError:
            print("متوجه نشدم، لطفاً دوباره تکرار کنید.")
            return None

def get_location():
    geolocator = Nominatim(user_agent="geoapiExercises")
    location = geolocator.geocode("Tehran, Iran")
    return location.address

def access_camera():
    cap = cv2.VideoCapture(0)
    while True:
        ret, frame = cap.read()
        cv2.imshow('Camera', frame)
        if cv2.waitKey(1) & 0xFF == ord('q'):
            break
    cap.release()
    cv2.destroyAllWindows()

while True:
    text = recognize_speech()
    if text:
        if "سلام" in text:
            speak("سلام! چطور می‌تونم کمکتون کنم؟")
        elif "خداحافظ" in text:
            speak("خداحافظ! روز خوبی داشته باشید.")
            break
        elif "مکان" in text:
            location = get_location()
            speak(f"مکان شما: {location}")
        elif "دوربین" in text:
            speak("دسترسی به دوربین")
            access_camera()
        else:
            speak("متوجه نشدم، لطفاً دوباره بگید.")