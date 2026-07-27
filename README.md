# 🚀 [Tips Hindawi](https://www.tipshindawi.com/) Challenge (June–July) 2026

> 🏆 This repository is my official submission for the [ **Tips Hindawi** ](https://www.tipshindawi.com/) **Challenge (June–July) 2026**.

## 👤 Participant

| Field            | Value                                |
| ---------------- | ------------------------------------ |
| Full Name        | Mariam Khaled Hassan                 |
| Project Name     | Novellm                              |
| GitHub Username  | mariamkh204                          |
| Challenge Batch  | June–July 2026                       |
| Training Program | Large Language Models (LLMs) Program |
| Organization     | [**Edrak for Ai**](https://edrak4ai.com/en)                         |

---

# 📖 Project Overview

Novellm is an AI powered reading companion that lets you upload any book as a PDF and get deep, interactive insight into it. Once uploaded, it analyzes the full text (falling back to OCR for scanned or Arabic language PDFs) and lets you ask questions or do Q&A about any part of the book. It supports "catch up" summaries too so if you're on chapter 5, you can ask it to recap everything from chapters 1–5.

It also includes an analytics dashboard showing stats like word count and estimated reading time, plus a full character map built using a flexible output parser to reliably extract characters, their roles, and relationships from the model's responses and an interactive relationship graph showing how characters connect to one another. Beyond that, there's a dedicated summarization tool for condensing whole sections, a quiz generator for comprehension checks, an explanation mode that breaks down difficult or dense passages into plain language, and a recommendation feature tell it your mood or what you're in the mood to read, and it suggests real books that fit.

it's built on Mistral-7B, quantized to 4-bit for efficient GPU use, orchestrated with LangChain and a FAISS vector store for retrieval. PDF parsing runs through PyMuPDF with an EasyOCR fallback for Arabic and scanned text, and the whole experience is served through a custom animated Gradio dashboard, with an interactive vis network graph for character relationships all running in a Kaggle GPU notebook.

---

# ✨ Features

* Full book PDF upload & indexing (with automatic Arabic OCR fallback for scanned/degraded text)
* Full book Q&A ask questions about any part of the book
* Spoiler free "Catch Up" summaries 
* Character Network analysis auto extracted character cards (name, role, mentions, summary)
* Interactive character relationship graph 
* Book analytics dashboard (word count, estimated reading time, chunk count, character count, mention frequency chart)
* Excerpt summarizer 
* Comprehension quiz generator 
* "Explain This" mode simplifies dense or difficult passages into plain language
* Personalized book recommender (based on mood, pacing, ending type, protagonist archetype, length, and genre)

---

# 🛠️ Technologies Used

* **Mistral-7B-Instruct-v0.2** ➜ core LLM, quantized to 4-bit (NF4) with BitsAndBytes for efficient GPU inference
* **Transformers** ➜ (Hugging Face)  model loading, tokenizer, and text-generation pipeline
* **LangChain** ➜ (core, community, text splitters) orchestration layer, chunking (`RecursiveCharacterTextSplitter`), LLM pipeline wrapper
* **FAISS** ➜ vector store for semantic search / retrieval (RAG)
* **Custom output parser** ➜ reliably extracts structured JSON (characters, relationships, quizzes, recommendations) from raw LLM text output
* **PyMuPDF (fitz)** **EasyOCR** ➜ for PDF text extraction
* **Gradio** ➜ interactive web dashboard (tabs, sidebar, progress bars, custom CSS/animations)
* **pyngrok** ➜  tunneling for public share links

---

# ⚙️ Installation

## Setup Steps

1. Enable the GPU accelerator

2. Add your Hugging Face token and load model  

3. **Run the setup cell**
   This installs all required dependencies:
```bash
   pip install -q -U torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
   pip install -q -U transformers accelerate bitsandbytes
   pip install -q -U langchain langchain-community langchain-core langchain-text-splitters
   pip install -q -U sentence-transformers faiss-gpu pypdf pyvis pydantic pymupdf
   pip install -q -U pyngrok matplotlib gradio easyocr
```

4. **Run all cells in order**
   - 1) Installs dependencies and authenticates with Hugging Face using the Kaggle Secret
   - 2) Loads and quantizes Mistral-7B-Instruct-v0.2 (4-bit)
   - 3) Sets up EasyOCR, parses PDFs, and builds the RAG index (chunking + FAISS vector store)
   - 4) Defines the analysis, summarization, quiz, and recommendation functions
   - 5) Launches the Gradio dashboard (wires up RAG-based Q&A and all other features to the UI)

5. **Access the app**
   - Once the final cell runs, Gradio will print a local URL (`http://127.0.0.1:7860`) and a temporary public URL (`https://xxxx.gradio.live`) open either links to access the website

---

# 🚀 Usage

1. **Index your book** Go to the "📖 Reader Hub" tab, upload a PDF using the file picker, and click "⚡ Index Book". The app will extract the text (falling back to OCR automatically if the PDF is scanned or in Arabic) and show an indexing status with page count, word count, and number of chunks.

2. **Ask questions about the book** Still in the "Reader Hub" tab, type a question into the "Question about the book" box and click "🔍 Answer Question" to get a retrieval based answer grounded in the book's text.

3. **Get a spoiler free catch up** Use the slider to set the chapter/section you stopped at, then click "📜 Generate Catch Up Summary" to get a recap of everything up to that point without spoilers.

4. **Explore characters** Go to the "👥 Character Network" tab and click "🔍 Analyze Full Book Characters". This generates clickable character cards (name, role, mention count, summary) and an interactive relationship graph showing how characters connect.

5. **Summarize or quiz yourself** — In the "📝 Summaries & Quizzes" tab, paste any excerpt (or leave it blank to use the whole book) and click "📋 Summarize Excerpt" for a bulleted summary, or "🎯 Generate Quiz" for auto generated multiple choice comprehension questions.

6. **Simplify a difficult passage**  In the "💡 Explain This" tab, paste a dense or confusing paragraph and click "💡 Simplify Paragraph" to get a plain language explanation.

7. **Get book recommendations**  In the "📚 Book Recommender" tab, fill in your desired vibe, pacing, ending type, protagonist archetype, length, and genre, then click "✨ Discover Books" for personalized suggestions.

8. **Check analytics anytime** The sidebar shows live stats (total words, estimated reading time, chunk count, character count) plus a chart of the most mentioned characters. Click "🔄 Refresh Stats" to update it.
---

# 📸 Demo

🎥 [Watch the demo video](https://drive.google.com/file/d/1CWieKmdfUm64axqgL3ZrGAVRGaEl8z2z/view?usp=sharing)
---

# 📈 Results

* Successfully built and ran a fully local, GPU-efficient RAG pipeline on a quantized 4-bit Mistral-7B model, keeping VRAM usage under ~2GB
* Enabled full-book question answering grounded in the actual source text rather than the model's general knowledge
* Added bilingual support (Arabic + English) with automatic OCR fallback, extending usability beyond digitally-native English PDFs — a gap most similar tools don't address
* Delivered five distinct reading-assistant features (Q&A, catch-up summaries, character network analysis, quizzes/summarization, recommendations) in a single unified dashboard
* Automated character and relationship extraction from raw book text using a custom output parser, turning unstructured LLM output into structured, visualized data
* Packaged the entire system into an interactive, shareable Gradio dashboard usable without any local setup beyond a browser link

---

# 🔮 Future Improvements

* Package the app as a **mobile app** (iOS/Android) for on the go reading companionship
* **Fine tune the model** on book focused/literary datasets to improve domain knowledge and reduce generic responses
* Add support for more file formats beyond PDF (EPUB, plain text, DOCX)
* Introduce user accounts with reading progress tracking synced across devices
* Add audio/text-to-speech support so users can listen to summaries or explanations

---

# 📚 About the Challenge

This project was developed as part of the [**Tips Hindawi**](https://www.tipshindawi.com/) **Challenge (June–July) 2026**.

[Tips Hindawi](https://www.tipshindawi.com/) is the internships department of [**Edrak for Ai**](https://edrak4ai.com/en), and the challenge encourages participants to build real-world projects, apply practical skills, and showcase their work through GitHub.

For more information about the challenge, training programs, and upcoming batches, visit the official [Tips Hindawi](https://www.tipshindawi.com/) website.

---

# 📄 License

This project is shared for educational and portfolio purposes.
