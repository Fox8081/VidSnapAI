# VidSnapAI
This project is a Flask-based web application that lets users upload images and a description, then automatically generates a vertical “reel” video by combining uploaded images with speech audio synthesized from the description text. The finished reels are showcased in a gallery for easy viewing by all users.

Features
Image and text upload: Users can upload images and submit a text description.

Automatic text-to-speech: Description is converted to lifelike narration using ElevenLabs API.

Reel creation: Images and narration are combined into a 1080x1920 vertical-format video using ffmpeg.

Gallery page: Completed reels are displayed for convenient playback in the browser.

Automated backend: Background script processes uploads and manages reel generation automatically.

Demonstration
Navigate to the home page.

Create a new reel by uploading images and entering a description.

Wait for processing; visit the gallery to view your finished reels.

Project Structure:

 main.py             -  Flask web server: uploads, routing, gallery
 
 generate_process.py -  Background worker: processes new uploads to reels
 
 text_to_audio.py    -  Converts text to speech with ElevenLabs API
 
 config.py           -  Stores API key(s) (not shown)
 
 user_uploads/       -  Uploaded user files (created at runtime)
 
 static/reels/       -  Outputted reel videos
 
 templates/          -  HTML templates (index.html, create.html, gallery.html)
 
Installation and Setup
Clone the repository:

bash
git clone https://github.com/Fox8081/VidSnapAI.git

cd VidSnapAI

Install dependencies:

bash
pip install flask elevenlabs
Install ffmpeg:

On Ubuntu/Linux: sudo apt-get install ffmpeg

On Mac: brew install ffmpeg

On Windows: Download from FFmpeg site.

Configure ElevenLabs API key:

Edit config.py and add:

python
ELEVENLABS_API_KEY = 'your_api_key_here'
Run the Flask app:

bash
python main.py
Start the background processor:

bash
python generate_process.py
Usage
Go to http://127.0.0.1:5000/ in a web browser.

Use the “Create” page to upload up to several images (jpg/png/jpeg).

Enter a description for narration.

Submit; allow a few seconds for video generation.

Visit the “Gallery” page to view all reels created so far.

How it Works

main.py: Handles image uploads, saves description and input file list, and serves UI pages.

generate_process.py: Loops through uploads, converts description text to audio.mp3 using ElevenLabs, then calls ffmpeg to generate a vertical reel video; writes to static/reels.

text_to_audio.py: Calls ElevenLabs API as per settings to create narration.

Gallery: Lists all .mp4 reels for playback.

Requirements
Python 3.8+

Flask

ffmpeg (system dependency)

elevenlabs

File Explanations
File	Role

main.py:	            Web server, routes for upload and gallery

generate_process.py:	Watches for new uploads, processes them to create reels

text_to_audio.py:	   Text-to-speech conversion using ElevenLabs API

config.py:	          API key configuration (must add ELEVENLABS_API_KEY)

Notes and Troubleshooting
Ensure ffmpeg is correctly installed and available in your system PATH.

The ElevenLabs API key is required and usage may have daily limits or costs.

Input and output folders (user_uploads, static/reels) are auto-created if missing.

For development/debug, Flask runs in debug=True mode by default.

Future Improvements
User authentication and personalized reel management

Improved error handling for failed conversions

Video customization (timings, transitions, audio options)

Deployment instructions for public hosting
