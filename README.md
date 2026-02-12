Clinical Named Entity Recognition using medSpaCy

This project implements Clinical Named Entity Recognition (NER) using medSpaCy on de-identified hospital discharge summaries. The system processes raw clinical text and extracts structured medical entities such as:

Diseases

Symptoms

Medications

Procedures

Diagnoses

It uses PyRuSH for clinical sentence segmentation and spaCy-based pipelines for entity extraction.

📌 Project Overview

Clinical notes are often unstructured and difficult to analyze. This project demonstrates how to:

Perform sentence segmentation using PyRuSH

Process discharge summaries

Extract medical entities

Convert raw clinical text into structured outputs

Analyze patient-level medical information programmatically

🛠️ Technologies Used

Python

medSpaCy

spaCy

PyRuSH

Jupyter Notebook

📂 Project Structure
├── NER.ipynb              # Main notebook for running clinical NER
├── README.md              # Project documentation

⚙️ Installation
1️⃣ Clone the Repository
git clone https://github.com/yourusername/your-repo-name.git
cd your-repo-name

2️⃣ Create Virtual Environment (Recommended)
python -m venv venv
source venv/bin/activate   # Mac/Linux
venv\Scripts\activate      # Windows

3️⃣ Install Dependencies
pip install medspacy spacy
pip install PyRuSH

🚀 How to Run

Open the notebook:

jupyter notebook


Run NER.ipynb

Provide clinical text input (example: discharge summary)

The system will output:

Sentence segmentation logs

Extracted named entities

Structured medical concepts

📊 Example Input
Chief Complaint:
Abdominal pain

History of Present Illness:
74y female with type 2 dm and recent stroke...

📈 Example Output

Extracted Entities:

Hydrochlorothiazide
Abdominal pain
Stroke
Colon cancer
Hemicolectomy
Pancreatitis
HTN

🧠 How It Works

Sentence Segmentation

PyRuSH detects clinical sentence boundaries.

Tokenization

spaCy tokenizes the text.

Entity Recognition

medSpaCy extracts clinical entities.

Structured Output

Entities are returned as structured tuples.

🎯 Use Cases

Clinical decision support systems

Medical research analysis

Hospital record structuring

Healthcare NLP research

EHR data mining

🔐 Data Privacy

This project uses de-identified medical text.
All patient-identifying information is masked.

📌 Future Improvements

Add entity classification labels

Convert output to structured JSON

Integrate with FHIR format

Build a Streamlit UI

Deploy as an API

👨‍💻 Author

Hari Haran.C
AI/ML Enthusiast | Clinical NLP | LangChain | Healthcare AI
