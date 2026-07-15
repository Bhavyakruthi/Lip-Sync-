# Lip Sync Voice Clone Pipeline for Indic Languages

A real-time lip-syncing voice clone model that translates English video content to multiple Indic languages with voice cloning and lip synchronization.

## Features

- **Speech Recognition**: Whisper (large-v3) for accurate English transcription
- **Translation**: IndicTrans2 supporting 22+ Indic languages
- **Voice Cloning**: XTTS-v2 for zero-shot voice cloning (only 3-6 seconds needed)
- **Lip Sync**: Wav2Lip for realistic lip synchronization

## Supported Languages

| Language | Code | 
|----------|------|
| Hindi | hi |
| Tamil | ta |
| Telugu | te |
| Bengali | bn |
| Marathi | mr |
| Gujarati | gu |
| Kannada | kn |
| Malayalam | ml |
| Punjabi | pa |

## Installation

```bash
# Create virtual environment
python -m venv venv
venv\Scripts\activate  # Windows
# source venv/bin/activate  # Linux/Mac

# Install dependencies
pip install -r requirements.txt

# Install ffmpeg (required for video processing)
# Windows: Download from https://ffmpeg.org/download.html
# Or use: winget install ffmpeg
```

## Usage

### 1. Configure the pipeline

Edit `config.yaml`:

```yaml
input:
  video_path: "samples/input_video.mp4"
  voice_sample_path: "samples/voice_sample.wav"

settings:
  target_language: "hi"  # Hindi

output:
  output_path: "output/result.mp4"
```

### 2. Run the pipeline

```bash
python run.py --config config.yaml
```

Or with command-line overrides:

```bash
python run.py -c config.yaml \
    --video samples/input.mp4 \
    --voice samples/voice.wav \
    --language ta \
    --output output/tamil_video.mp4
```

### 3. List supported languages

```bash
python run.py --list-languages
```

## Pipeline Architecture

```
Input Video (English) → Whisper (STT) → IndicTrans2 (Translation)
                                              ↓
Output Video (Lip-synced) ← Wav2Lip ← XTTS-v2 (Voice Clone)
```

## Project Structure

```
project-2/
├── config.yaml           # Configuration file
├── run.py               # Entry point
├── pipeline.py          # Main pipeline orchestrator
├── requirements.txt     # Dependencies
├── modules/
│   ├── transcriber.py   # Whisper-based STT
│   ├── translator.py    # IndicTrans2 translation
│   ├── voice_cloner.py  # XTTS-v2 voice cloning
│   └── lip_sync.py      # Wav2Lip lip synchronization
├── samples/             # Input samples
├── output/              # Generated outputs
└── temp/                # Temporary files
```

## Hardware Requirements

- **GPU**: NVIDIA GPU with 8GB+ VRAM (recommended)
- **RAM**: 16GB+ recommended
- **Storage**: ~10GB for models

## License

MIT License
