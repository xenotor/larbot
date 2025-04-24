# Listen And Respond (lar)bot

## Setup

### Homebrew if not already installed
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Install Python 3.10 and ffmpeg MacOS 3.9 won't do(!)
```bash
brew install python@3.10 ffmpeg
```

### local virtual environment & dependencies
```bash
python3 .10 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### API keys
```bash
cp env.example .env # and add your credentials
```

## Running the bot
```bash
python larbot.py
```

Open `http://localhost:7860/` in your browser.


## About
THis is simple router between Deepgram (stt), OpenAI (gpt4 LLM) and Cartesia (tts). 
It uses Deepgram to transcribe audio, OpenAI to generate a response, and Cartesia to convert the response to speech. 

The bot receives audio data via WebRTC (using Google STUN server for NAT traversal), then queues dataframes into pipeline defined as:
[
    transport.input(),
    stt,
    context_aggregator.user(),
    llm,
    tts,
    ml,
    transport.output(),
    context_aggregator.assistant(),
]

The server serves the prebuild web interface and executes the bot as a background task.