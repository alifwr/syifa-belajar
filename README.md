Berikut adalah draf perencanaan proyek (*Project Planning*) komprehensif untuk ketiga tema proyek LLM yang diusulkan. Format ini dirancang menggunakan Markdown agar terstruktur dan siap digunakan di repositori GitHub atau portofolio proyek Syifa.

---

# Multi-Project Blueprint: Production-Grade LLM Fine-Tuning, Optimization, and Deployment

Dokumen ini memuat draf perencanaan taktis untuk tiga proyek implementasi *Large Language Model* (LLM) tingkat lanjut, yang berfokus pada spesialisasi domain, integrasi sistem (*agentic workflows*), dan efisiensi komputasi *edge*.

---

## PROJECT 1: Specialized Biomedical LLM Assistant via Parameter-Efficient Fine-Tuning (PEFT)

### 1. Project Overview & Objectives

Proyek ini bertujuan untuk melakukan *fine-tuning* pada *Open-Source* LLM berskala menengah agar memiliki spesialisasi tinggi dalam domain biomedis dan medis. Model dilatih untuk memahami istilah klinis, merangkum literatur biomedis, dan menjawab pertanyaan berbasis bukti (*evidence-based QA*) dengan meminimalkan halusinasi.

### 2. Technical Stack & Tools

* **Base Model:** `Llama-3-8B-Instruct` atau `Gemma-2-9B-It`.


* **Training & Optimization:** PyTorch, Hugging Face (Transformers, TRL, PEFT), **Unsloth** (untuk akselerasi QLoRA 4-bit).


* **Dataset:** `PubMedQA` & `MedQA (USMLE)`.


* **Experiment Tracking:** Weights & Biases (WandB).


* **Inference & Deployment:** vLLM, FastAPI, Docker.



### 3. Project Roadmap (4-Week Timeline)

* **Week 1 (Data Engineering):** Mengunduh dataset `PubMedQA` dan `MedQA`, melakukan *data cleaning*, dan memformatnya ke dalam instruksi terstruktur (*Instruction Tuning*). membagi data menjadi *Train* (80%), *Validation* (10%), dan *Test* (10%).


* **Week 2 (Environment Setup & Config):** Mengonfigurasi Docker dengan CUDA toolkit. Menentukan konfigurasi hyperparameter LoRA (`r=16`, `lora_alpha=32`, menargetkan seluruh modul atensi dan MLP).


* **Week 3 (Training & Quantitative Evaluation):** Menjalankan *Supervised Fine-Tuning* (SFT) dengan *tracking* via WandB. Mengevaluasi model akhir pada *Test Set* menggunakan framework **Ragas** untuk mengukur *faithfulness* dan *context recall*.


* **Week 4 (Merging & Production Deployment):** Menggabungkan bobot LoRA kembali ke model dasar. Membangun *inference service* dengan **vLLM** dan **FastAPI** di dalam kontainer Docker untuk mendukung *token streaming* berkecepatan tinggi.



---

## PROJECT 2: LLM Fine-Tuning for Enterprise Function Calling & Structured Tool Use

### 1. Project Overview & Objectives

Proyek ini berfokus pada pelatihan model bahasa berukuran kecil hingga menengah agar mampu bertindak sebagai *Controller* dalam arsitektur AI Agent. Model dilatih secara intensif untuk mengubah instruksi teks natural manusia menjadi sintaks pemanggilan fungsi/API (*Function Calling*) atau query database secara konsisten dalam format JSON yang valid tanpa *catastrophic forgetting*.

### 2. Technical Stack & Tools

* **Base Model:** `Mistral-7B-Instruct-v0.3` atau `Phi-3-medium-instruct`.


* **Training & Alignment:** Hugging Face (PEFT/LoRA), TRL (Transformer Reinforcement Learning), Axolotl.


* **Dataset:** `ToolBench` & `Spider (Text-to-SQL subset)`.


* **Validation & Serving:** JSON Schema Validation, FastAPI, Qdrant/Elasticsearch.



### 3. Project Roadmap (4-Week Timeline)

* **Week 1 (Schema & Data Synthesis):** Menyusun skema API tiruan dan memformat dataset `ToolBench` ke dalam pola interaksi: `User Query` -> `Available Tools` -> `Target JSON Output`.


* **Week 2 (LoRA Training Setup):** Mengonfigurasi skrip pelatihan LoRA dengan fokus parameter yang ketat untuk menjaga kepatuhan sintaksis JSON tanpa merusak kemampuan bahasa umum model.


* **Week 3 (Training & Robustness Testing):** Melatih model dan melacak metrik kegagalan format (*parsing errors*). Melakukan pengujian penetrasi dengan input yang ambigu untuk menguji ketahanan logika penalaran model.


* **Week 4 (Agent Integration):** Mengintegrasikan model yang telah di-*fine-tune* ke dalam arsitektur multi-agent menggunakan **LangGraph** atau **LangChain**, menggantikan ketergantungan pada API eksternal komersial.



---

## PROJECT 3: TinyLLM Fine-Tuning, Quantization, and Deployment for Edge Devices

### 1. Project Overview & Objectives

Proyek ini menjembatani kapabilitas AI modern dengan keterbatasan *hardware* lokal (*On-device AI*). Fokus utamanya adalah melakukan *fine-tuning* pada *Small Language Model* (SLM) untuk tugas spesifik, kemudian menerapkan teknik *Post-Training Quantization* ekstrem agar model dapat berjalan secara luring (*offline*) dengan *latency* rendah pada perangkat dengan spesifikasi terbatas.

### 2. Technical Stack & Tools

* **Base Model:** `Llama-3.2-3B-Instruct` atau `Phi-3.5-mini-instruct`.


* **Fine-Tuning:** PyTorch, Hugging Face PEFT (LoRA/QLoRA).


* **Quantization & Edge Runtime:** `Llama.cpp`, GGUF Format, Ollama.


* **Dataset:** `SlimOrca` (High-quality general reasoning) & `Alpaca`.


* **Benchmarking:** Custom Python profiling scripts untuk monitoring VRAM/RAM, CPU/GPU utilization, dan *Tokens Per Second* (TPS).



### 3. Project Roadmap (4-Week Timeline)

* **Week 1 (Dataset Filtering):** Memilih subset berkualitas tinggi dari `SlimOrca` dan `Alpaca` untuk memastikan model kecil mendapatkan sinyal pelatihan yang padat informasi.


* **Week 2 (Downsized SFT Training):** Melakukan *Supervised Fine-Tuning* (SFT) pada model dasar 3B parameter. Mengoptimalkan *learning rate* dan *batch size* agar pas dengan batasan komputasi *hardware*.


* **Week 3 (Compilation & Quantization):** Mengompilasi bobot model akhir menggunakan `llama.cpp`. Melakukan kuantisasi bobot menjadi format **GGUF 4-bit (Q4_K_M)** dan **5-bit (Q5_K_M)**, lalu mengevaluasi penurunan *perplexity* pasca-kuantisasi.


* **Week 4 (Local Benchmarking & Deployment):** Menjalankan model secara lokal via **Ollama**. Membuat skrip *benchmark* untuk mengukur performa *real-time*: menargetkan penghematan memori hingga **>70%** dan memantau stabilitas metrik *Time to First Token* (TTFT).



---

Ketiga cetak biru proyek di atas sangat selaras dengan latar belakang akademis dan rekam jejak profesional Syifa di bidang rekayasa perangkat lunak serta komputasi performa tinggi.

Dari ketiga draf perencanaan di atas, proyek mana yang ingin dieksekusi atau didokumentasikan terlebih dahulu ke dalam portofolionya, Alif-sama?