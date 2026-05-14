# AuthoAI

AI-assisted auto-filler for the **Massachusetts Standard Form for Medication Prior Authorization Requests**.

Physicians enter a Member ID and a few clinical details; AuthoAI pulls the patient record, then uses a local LLM (via [Ollama](https://ollama.com)) to generate ICD-10 codes, dosing schedules, clinical justifications, and medical necessity statements — all mapped to the official MA form sections A–F.

> **Disclaimer:** AI-generated clinical content is for drafting assistance only. All fields must be reviewed and verified by a licensed clinician before submission.

## Features

- **Patient lookup** from a local dataset by Member ID
- **LLM-powered auto-fill** of clinical fields (ICD-10, dosing, justification, medical necessity)
- **Live form preview** mirroring the MA Standard Prior Auth layout (Sections A–F)
- **Form completeness score** showing how many required fields are filled
- **Copy letter** — one-click copy of a medical necessity letter to clipboard
- **Download PDF** — print-ready version via browser print dialog
- **Fully offline** — no data leaves your machine

## Prerequisites

- [Node.js](https://nodejs.org/) >= 18
- [Ollama](https://ollama.com) installed and running

## Quick Start

```bash
# 1. Clone the repo
git clone https://github.com/<your-username>/authoai.git
cd authoai

# 2. Install dependencies
npm install

# 3. Copy the env file and adjust if needed
cp .env.example .env

# 4. Pull the model and start Ollama
ollama pull adrienbrault/biomistral-7b:Q5_K_M
ollama serve

# 5. Start the app
npm start
```

The app opens at [http://localhost:3000](http://localhost:3000).

## Regenerating the Patient Dataset

The synthetic patient dataset (`src/patient_dataset.json`) can be regenerated with:

```bash
cd src
python generate_dataset.py
```

Requires Python >= 3.8 (standard library only, no pip dependencies).

## Project Structure

```
authoai/
├── public/             # Static assets
├── src/
│   ├── App.js          # Main application (UI + Ollama integration)
│   ├── patient_dataset.json  # 500 synthetic patient records
│   └── generate_dataset.py   # Script to regenerate the dataset
├── .env.example        # Environment variable template
├── .gitignore
├── package.json
└── README.md
```

## Tech Stack

- React 19 (Create React App)
- Ollama + BioMistral 7B (local LLM inference)
- Inline styles (single-file component)

## License

MIT
