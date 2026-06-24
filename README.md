⚠️ This is the local development version. The production backend with fine-tuned models is deployed on Hugging Face: amarre/speakease-models

# ⚙️ SpeakEase Backend – FastAPI AI Server

FastAPI backend powering the SpeakEase speech analysis platform.
Handles transcription, quality scoring, age classification, 
conversational AI, and text-to-speech.

> ⚠️ **This is the local development version.**
> Production backend with hosted models is deployed on Hugging Face:
> 👉 [huggingface.co/spaces/amarre/speakease-models](https://huggingface.co/amarre)

## 🔗 Related Repositories
- **Flutter App:** [SpeakEase_App](https://github.com/Amar-77/SpeakEase_App)
- **Models on HuggingFace:** [amarre/speakease-models](https://huggingface.co/amarre/speakease-models)

## 🧠 AI Models Used
| Model | Purpose | Source |
|-------|---------|--------|
| Whisper (Svarah fine-tuned) | Speech-to-text transcription | Custom trained |
| Wav2Vec2 MultiScore | Fluency + Pronunciation + Clarity scoring | Custom trained |
| Wav2Vec2 Age Classifier | Speaker age group detection | Custom trained |
| LLaMA 3.1 8B (via Groq) | Conversational AI tutor (Speaky) | Groq API |
| LLaMA 3.3 70B (via Groq) | Practice content generation | Groq API |
| Edge TTS – NeerjaExpressive | Teacher voice generation | Microsoft |

## 🔌 API Endpoints
| Method | Endpoint | Description |
|--------|---------|-------------|
| POST | `/analyze/` | Full speech analysis (transcription + scores + word analysis) |
| POST | `/generate-teacher-voice/` | Generate TTS audio response |
| POST | `/chat-batch/` | Speaky conversational chat mode |
| GET | `/end-session-score/{id}` | Session analytics + cleanup |
| POST | `/generate-practice/` | AI-generated practice paragraphs |
| POST | `/speaky-chat/` | Text-based Speaky chatbot |
| GET | `/` | Health check |

## 🛠️ Tech Stack
- **Framework:** FastAPI + Uvicorn
- **ML:** PyTorch, HuggingFace Transformers
- **Audio:** Librosa, PyDub, SoundFile
- **LLM:** Groq SDK
- **TTS:** edge-tts
- **Deployment:** Hugging Face Spaces (port 7860)

## 🚀 Local Setup

```bash
git clone https://github.com/Amar-77/SpeakEase_2.0.git
cd SpeakEase_2.0
pip install -r requirements.txt
```

Create a `.env` file:
GROQ_API_KEY=your_groq_api_key_here

Run the server:
```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

Server will be available at `http://localhost:8000`

## 📊 Scoring Formula
Overall Score = (WER Accuracy × 0.4) + (Fluency × 0.3) + (Pronunciation × 0.3)

Session Score = (Avg Fluency × 0.4) + (Avg Pronunciation × 0.4) + (Avg Clarity × 0.2)
