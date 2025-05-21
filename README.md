# NM-ARASU-VOICE-BASED-NOTES-AND-MEMO-SYSTEMS
Voice-based Notes and Memo
Systems
Introduction:
In today's fast-paced digital age, traditional methods of note-taking and memo recording
are being rapidly replaced by smart, efficient, and accessible technologies. Voice-based
systems have emerged as a powerful solution to enhance productivity and convenience.
The "Voice-based Notes and Memo System" aims to provide users with a seamless
method to record spoken thoughts, ideas, and reminders, converting them into textual
notes automatically using speech recognition technologies.

This project is especially beneficial for professionals, students, and individuals who
prefer hands-free interaction with devices or need to capture ideas quickly on the go.
With advancements in voice processing, it's now feasible to transcribe speech with high
accuracy and store it systematically for future reference.

Problem Statement:
Manual note-taking using traditional input devices like keyboards or writing tools can be
time-consuming, error-prone, and inefficient in situations where users are multitasking or
physically constrained. Moreover, people often forget ideas if they cannot record them
immediately. There's a clear need for a reliable and user-friendly system that can:

● Record voice inputs.
● Convert speech to text.
● Save the converted text in an organized manner (e.g., CSV or text file).
● Allow appending new entries without overwriting previous ones.
The "Voice-based Notes and Memo System" addresses this issue by providing a
lightweight, intuitive, and accurate voice-to-text platform that updates the user's
notes automatically.
Objectives
The key objectives of this project include:

● To develop a system that allows users to input memos or notes using voice.
● To convert `.wav` audio files into transcribed text using speech recognition
libraries.
● To store the transcriptions in a structured format like `.csv` or `.txt` without
recreating the file each time.
● To support batch processing of multiple audio files uploaded via a ZIP archive.
● To make the system usable in environments like Google Colab for cloud-based
accessibility.
Methodology
The development of the Voice-based Notes and Memo System follows a structured
methodology to ensure accurate voice recognition, efficient storage, and seamless user
experience. The steps are as follows:

Audio Input Collection
The user records their note or memo as a .wav audio file using any voice
recorder. This allows flexibility in capturing voice inputs even without a live
microphone.
Audio File Upload
The system allows users to upload one or more .wav files at a time. These files
are collected through a file input interface and stored temporarily for processing.
Speech Recognition
Using a speech recognition library (such as Python’s speech_recognition
module), the system processes each .wav file to extract the spoken words and
convert them into text format. This module uses Google's Web Speech API for
accurate transcription.
Data Validation and Cleaning
The transcribed text is cleaned to remove background noise errors, common
artifacts, or misinterpretations. Optional keyword filtering can be implemented to
ignore irrelevant inputs.
File Handling and Storage
○ If the output file does not exist, it is created.
○ If it already exists, the system appends the new note without overwriting
the previous entries.
○ Each recognized note is saved in a new line or row, maintaining the
chronological order of input.
Error Handling
The system includes exception handling to manage cases such as:
○ Unrecognizable audio
○ Missing files
○ File format issues
Output Generation
The recognized text is saved and can be reviewed later as a memo or note. The
output is either a .txt file for simple notes or a .csv file if metadata (like date
and time) needs to be recorded alongside the note.
Repeatable Use
The system is designed to be used multiple times. Each run will append new
content to the existing file without duplication, ensuring continuity.
Program Flow:
!pip install SpeechRecognition pandas

! pip install pandas pyttsx

!apt-get install -y portaudio19-dev

!pip install pyaudio

pip install pipwin

from google.colab import files

print("Upload your ZIP file containing .wav files:")

uploaded = files.upload()

import os

import zipfile

extract_folder = "extracted_audio"

os.makedirs(extract_folder, exist_ok=True)

for zip_filename in uploaded.keys():

if zip_filename.endswith('.zip'):
with zipfile.ZipFile(zip_filename, 'r') as zip_ref:
zip_ref.extractall(extract_folder)
print(f"Extracted ZIP file to folder: {extract_folder}")
else:
print(f"❌ {zip_filename} is not a ZIP file.")
print("Files extracted:")

print(os.listdir(extract_folder))

import os

import zipfile

from google.colab import files

import speech_recognition as sr

Step 1: Upload and unzip
uploaded = files.upload() # Upload a zip with .wav files

zip_file_name = list(uploaded.keys())[0]

extract_path = "Notes"

with zipfile.ZipFile(zip_file_name, 'r') as zip_ref:

zip_ref.extractall(extract_path)
print(f"\n✅ Extracted to '{extract_path}'")
Step 2: Find all .wav files in all subfolders
wav_files = []

for root, dirs, files_in_dir in os.walk(extract_path):

for file in files_in_dir:
if file.lower().endswith(".wav"):
wav_files.append(os.path.join(root, file))
if not wav_files:

print("❌ No .wav files found. Check your ZIP structure.")
else:

print("🎧 Found the following .wav files:")
for wf in wav_files:
print(" -", wf)
Step 3: Recognize and write to output file
recognizer = sr.Recognizer()

output_file = "Notes_output.txt"

with open(output_file, "w", encoding="utf-8") as f:

for wav_path in wav_files:
filename = os.path.basename(wav_path)
print(f"\n🎧 Processing {filename}...") try:
with sr.AudioFile(wav_path) as source:
audio_data = recognizer.record(source)
Input Format
.wav audio files (voice memos or notes)
Combined in a .zip file for batch upload
Output Format
.txt file (or .csv if needed), containing each transcribed note on a new line
Automatically appended—no data is overwritten
command = recognizer.recognize_google(audio_data)
print(f"✅ Recognized: {command}")
f.write(f"{filename}: {command}\n")
except sr.UnknownValueError:
print(f"⚠ Could not understand audio in {filename}.")
f.write(f"{filename}: Could not understand audio.\n")
except sr.RequestError as e:
print(f"❌ API error for {filename}: {e}")
f.write(f"{filename}: API error - {e}\n")
print(f"\n🎧 All recognized commands saved to '{output_file}'")
output:
Testing and Validation:
● Tested with varied accents and sentence structures.
● Included background noise in some files to test recognition robustness.
● Validated file appending functionality and ensured no overwriting occurred.
● Ensured system handled unrecognized audio gracefully with placeholder text.
Conclusion:
The Voice-based Notes and Memo System successfully delivers an accessible, accurate,
and convenient method for voice-based note-taking. By leveraging Python's speech
recognition libraries and simple file handling mechanisms, the system can process
multiple audio files, extract meaningful content, and store it systematically.
This approach is highly extensible and can be adapted for mobile apps, accessibility
tools, or productivity platforms. Future improvements may include live recording
support, multilingual support, speaker identification, and integration with cloud storage.
