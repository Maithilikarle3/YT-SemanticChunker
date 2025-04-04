#  YT-Semantic Chunker

An LLM-enhanced YouTube audio analyzer that semantically chunks video transcripts, enriches each chunk with AI-generated titles, summaries, topics, Hindi translations, and provides a final overall summary.

> 🎯 Built to demonstrate the power of LLMs in audio understanding, chunk-level summarization, and multilingual accessibility.

---

## 🚀 Features

- 🔗 Input any **YouTube video URL**
- 🧠 Extracts and **transcribes audio**
- 🧩 **Semantically chunks** transcript by dynamically chosen time intervals
- 🏷️ **LLM-based enrichment**: title, summary, topic tags, Q&A
- 🌐 **Translates** each chunk to **Hindi**
- 📚 **Generates a final summary** of the whole video
- 🖼️ Simple **Gradio-based UI**

---

## 🛠️ Technologies Used & Their Roles

| Technology        | Purpose                                                                 |
|------------------|-------------------------------------------------------------------------|
| `yt-dlp`          | Downloads audio from YouTube URLs in high quality                       |
| `FFmpeg`          | Used to extract and convert audio (e.g., MP3) from downloaded videos     |
| `librosa` / `pydub`| Calculates total duration of audio to decide dynamic chunk time         |
| `Voice Activity Detection (VAD)` | Removes silence to improve transcription and chunk accuracy |
| `Speech Recognition Model` (like `Whisper`) | Transcribes audio to text                             |
| `Transformers` (Hugging Face) | Used for LLM-based title/summary/topic generation              |
| `facebook/m2m100_418M` | Translates English chunks to Hindi                             |
| `Gradio`          | Provides a clean and interactive user interface                         |

---

## 🔄 Project Workflow

1. **YouTube Audio Download**
   - The video URL is passed to `yt-dlp` to extract high-quality audio.

2. **Voice Activity Detection (VAD)**
   - Removes silent parts using `webrtcvad` or `librosa` to get more accurate chunking and transcription.

3. **Audio Transcription**
   - A speech-to-text model (e.g., OpenAI Whisper or Wav2Vec2) converts the audio to English transcript.

4. **Audio Duration Measurement**
   - `librosa.get_duration` or `pydub.utils.mediainfo` is used to dynamically determine how long each chunk should be (e.g., 30s, 45s, 60s).

5. **Semantic Chunking**
   - The transcript is segmented into chunks of max duration (e.g., 30 seconds), and aligned with time markers.

6. **LLM-Based Enrichment**
   - Each chunk is passed through:
     - `generate_title(text)`
     - `summarize(text)`
     - `tag_topic(text)`
     - `translator(text)`  
   - This enriches every chunk with metadata.

7. **Hindi Translation**
   - Each chunk’s transcript is translated into Hindi using facebook/m2m100_418M.




---

## 🧪 Example Chunk Output

```json
{
  "chunk_id": 4,
  "chunk_length": 29.6,
  "text": " ",
  "start_time": 88.58,
  "end_time": 120.38,
  "title": " ",
  "summary": " ",
  "topic": " ",
  "translated_text_hi": " "
}
