# 🤖 AI-Powered HR Onboarding Buddy
<img width="1068" height="672" alt="image" src="https://github.com/user-attachments/assets/26b1b77a-b926-4ed8-88af-122e3c197700" />

Sistem tanya jawab otomatis (Chatbot) berbasis kecerdasan buatan yang dirancang khusus untuk menjadi **"Onboarding Buddy"** bagi karyawan baru. Proyek ini dibangun menggunakan **Langflow** dengan arsitektur *Retrieval-Augmented Generation* (RAG) untuk membaca dan menjawab pertanyaan berdasarkan dokumen internal perusahaan (SOP/Panduan HR).

## 💡 Latar Belakang
Proses orientasi (onboarding) karyawan baru seringkali memakan waktu lama karena tim HR harus menjawab pertanyaan-pertanyaan repetitif terkait kebijakan, prosedur, dan langkah-langkah awal di perusahaan. Sistem ini hadir untuk mengatasi masalah tersebut dengan menyediakan asisten virtual yang **proaktif, suportif, dan profesional** 24/7.

## 🚀 Fitur Utama
- **Pemrosesan Dokumen Dinamis:** Mampu membaca file PDF (seperti `Onboarding_SOP.pdf`) dan mengekstrak teksnya.
- **Pencarian Konteks Akurat:** Menggunakan Vector Database untuk menemukan bagian dokumen yang paling relevan dengan pertanyaan pengguna.
- **Persona Khusus:** Menggunakan teknik *Prompt Engineering* agar AI bertindak selayaknya seorang mentor/buddy perusahaan yang ramah dan suportif.
- **Arsitektur Tanpa Kode (Low-Code):** Dibangun sepenuhnya menggunakan antarmuka visual Langflow.

## 🛠️ Teknologi yang Digunakan (Tech Stack)
- **Visual Framework:** [Langflow](https://www.langflow.org/) (v1.12.2)
- **LLM (Language Model):** Google Generative AI (Gemini 3.8 Flash / Gemini Flash Latest)
- **Embeddings Model:** Google Generative AI Embeddings (`models/gemini-embedding-001`)
- **Vector Database:** [DataStax Astra DB](https://astra.datastax.com/) (Serverless Vector DB)

## 🏗️ Arsitektur Sistem (Alur Kerja)

Proyek ini terbagi menjadi dua alur (flow) utama di dalam Langflow:

### 1. Data Ingestion Pipeline (Penyimpanan Pengetahuan)
Alur ini bertugas untuk membaca dokumen HR dan menyimpannya ke dalam memori AI (Vector Database).
*   **File Loader:** Membaca dokumen referensi yang diunggah.
*   **Text Splitter:** Memecah teks dokumen menjadi potongan kecil (*chunk size*: 1000, *overlap*: 200) agar tidak kehilangan konteks.
*   **Embeddings & Astra DB:** Mengubah potongan teks menjadi vektor dan menyimpannya ke dalam koleksi `hr_document` di Astra DB.

### 2. Retrieval & Generation Pipeline (Sistem Tanya Jawab)
Alur ini bertugas menerima pertanyaan pengguna dan meracik jawaban.
*   **Chat Input:** Menerima pertanyaan dari karyawan baru.
*   **Vector Search:** Sistem mencari potongan informasi yang relevan di Astra DB berdasarkan pertanyaan pengguna.
*   **Context Parser:** Menggabungkan hasil pencarian menjadi satu teks konteks yang utuh.
*   **Prompt Template:** Memberikan instruksi ketat kepada AI untuk menjawab berdasarkan konteks, memberikan arahan yang jelas, dan menggunakan bahasa yang ramah layaknya seorang rekan kerja.
*   **Language Model & Chat Output:** LLM Gemini memproses prompt tersebut dan menghasilkan jawaban akhir.

## 🧠 Contoh Prompt Engineering yang Digunakan
Sistem ini menggunakan *system prompt* khusus untuk memastikan kualitas jawaban:
> "Anda berperan sebagai Onboarding Buddy bagi karyawan baru di perusahaan... Berdasarkan konteks di atas, jawab pertanyaan sebagai Buddy yang suportif, proaktif, dan profesional. Berikan arahan yang jelas dan praktis, jelaskan langkah yang harus dilakukan karyawan baru, tawarkan bantuan atau dukungan lanjutan, dan gunakan bahasa yang ramah namun tetap profesional."

## 📸 Tampilan Alur Kerja (Screenshot)
<img width="1747" height="581" alt="image" src="https://github.com/user-attachments/assets/fa06b999-68fd-48aa-90ac-fa8098ea6b3e" />

## ⚙️ Cara Menjalankan Proyek Ini
Jika Anda ingin mencoba menjalankan alur ini di lingkungan lokal atau cloud Anda:
1. Pastikan Anda telah menginstal **Langflow**.
2. Clone repository ini atau unduh file `Onboarding Buddy System (Starter Project) (1).json`.
3. Buka antarmuka pengguna Langflow.
4. Klik tombol **"Import"** dan unggah file JSON tersebut.
5. Masukkan kunci API (API Keys) Anda pada komponen yang membutuhkan:
   - **Astra DB:** Masukkan `Database Endpoint` dan `Application Token`.
   - **Google Generative AI:** Masukkan `Google API Key` Anda pada komponen LLM dan Embeddings.
6. Unggah file dokumen SOP PDF Anda pada komponen **File**, lalu jalankan alur pertama (Ingestion).
7. Mulai obrolan melalui komponen **Chat**.
