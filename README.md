Medical NER & Specialist Recommendation System
A clinical NLP pipeline using medspaCy to extract medical problems from clinical text and recommend appropriate specialists based on detected conditions.

🏥 Overview
This system processes clinical narratives (discharge summaries, patient notes, symptoms) to:

Identify medical problems using rule-based named entity recognition

Filter out negated/uncertain findings using ConText algorithm

Map detected problems to appropriate medical specialties

Recommend specific specialists from a curated directory

Built with medspaCy - a clinical NLP library extending spaCy for healthcare text processing.

✨ Features
Rule-based NER: TargetMatcher with 100+ clinical problem patterns

Negation detection: ConText algorithm to identify negated/uncertain findings

Synonym normalization: Maps variations to canonical terms

Intelligent specialty mapping: Pattern-based problem-to-specialty matching

Fallback extraction: Regex pattern matching for symptom extraction when NER fails

Duplicate removal: Deduplicates detected problems

Comprehensive specialist directory: 20+ specialists across 18+ specialties

🛠️ Installation
bash
pip install medspacy
pip install spacy
python -m spacy download en_core_web_sm
🚀 Quick Start
python
import medspacy
from medspacy.ner import TargetRule

# Load medspaCy with clinical components
nlp = medspacy.load(
    medspacy_enable=["medspacy_pyrush", "medspacy_target_matcher", "medspacy_context"]
)

# Define problem patterns
problem_rules = [
    TargetRule("stroke", "PROBLEM"),
    TargetRule("diabetes", "PROBLEM"),
    TargetRule("abdominal pain", "PROBLEM"),
    # ... add more rules
]

# Add rules to pipeline
target_matcher = nlp.get_pipe("medspacy_target_matcher")
target_matcher.add(problem_rules)

# Process clinical text
text = "Patient presents with abdominal pain. No history of stroke."
doc = nlp(text)

# Extract active problems (skip negated)
problems = []
for ent in doc.ents:
    if ent.label_ == "PROBLEM" and not ent._.is_negated:
        problems.append(ent.text.lower())

print(problems)  # ['abdominal pain']
📋 Clinical Problem Coverage
The system recognizes 100+ medical conditions across these categories:

Category	Examples
🧠 Neurological	stroke, migraine, epilepsy, Parkinson's, dementia
🩸 Endocrine	diabetes, thyroid disorders, PCOS, obesity
🫀 Cardiovascular	hypertension, heart attack, arrhythmia, CAD
🫁 Respiratory	asthma, COPD, pneumonia, tuberculosis
🫂 Gastrointestinal	colon cancer, GERD, IBS, Crohn's, hepatitis
🧬 Oncology	metastasis, leukemia, lymphoma, melanoma
🦴 Musculoskeletal	arthritis, back pain, osteoporosis, gout
🩻 Renal	kidney failure, UTIs, nephrolithiasis
🩺 Other	depression, anxiety, anemia, allergies, etc.
🩻 Specialty Mapping
Problems are intelligently mapped to medical specialties:

python
# Example mapping logic
if "stroke" in problem_text or "cva" in problem_text:
    return ["Neurologist"]
elif "diabetes" in problem_text:
    return ["Endocrinologist", "General Physician"]
elif "cancer" in problem_text and "colon" in problem_text:
    return ["Oncologist", "Gastroenterologist"]
# ... and more
👨‍⚕️ Specialist Directory
Includes 20+ specialists across India:

Specialty	Sample Doctor	Location
Neurologist	Dr. Alafiya Meditour	Gurugram, Haryana
Cardiologist	Dr. Priya Mehta	Mumbai, Maharashtra
Oncologist	Dr. Amit Choraria	Kolkata, West Bengal
Pulmonologist	Dr. Sameer Bansal	Jaipur, Rajasthan
... and 15+ more	...	...
📊 Example Output
Input:

text
Patient presents with abdominal pain and history of type 2 diabetes. 
Imaging shows no metastasis.
Output:

text
🔍 Detected 2 problem(s): Abdominal Pain, Type 2 Diabetes

👨‍⚕️ Recommended specialists:

🩺 Specialty: Gastroenterologist
📛 Doctor: Dr. Bhartia Mithun
📞 Contact: +91-9012345678
📍 Location: Kamrup Metropolitan, Assam
🎯 Specialization: Digestive Disorders, Endoscopy

🩺 Specialty: Endocrinologist
📛 Doctor: Dr. Anshul Kumar
📞 Contact: +91-9123456780
📍 Location: West Delhi, Delhi
🎯 Specialization: Diabetes, Thyroid Disorders, Hormonal Issues
🔧 Key Components
1. TargetMatcher
Rule-based entity recognizer that matches literal strings or token patterns.

python
TargetRule("atrial fibrillation", "PROBLEM", 
          pattern=[{"LOWER": "afib"}])  # Matches "afib" as synonym
2. ConText Component
Detects negation, uncertainty, and temporal status of clinical entities.

python
if ent._.is_negated:
    continue  # Skip "no evidence of metastasis"
3. PyRuSH Sentencizer
Clinical sentence splitter optimized for medical narratives.

🎯 Use Cases
Clinical Decision Support: Suggest appropriate specialist referrals

Patient Triage: Automatically route patients based on symptoms

Medical Record Analysis: Extract active problems from discharge summaries

Telemedicine: Match patient-reported symptoms to specialists

📁 Project Structure
text
├── NER.ipynb              # Main notebook with complete pipeline
├── README.md              # This file
└── discharge_summary.txt  # Sample clinical text (optional)
⚙️ Configuration
Modify the specialist directory to add/update doctors:

python
specialist_directory["Neurologist"] = {
    "name": "Dr. Name",
    "contact": "+91-XXXXXXXXXX",
    "location": "City, State",
    "specialization": "Neurology, Stroke"
}
📈 Future Enhancements
Add UMLS integration for broader concept coverage

Implement machine learning-based NER as fallback

Add temporal detection (acute vs. chronic)

Create web API endpoint

Add confidence scores for recommendations

Expand to multilingual support

🤝 Contributing
Contributions welcome! Areas for improvement:

Add more medical problem patterns

Expand specialist directory

Improve specialty mapping logic

Add unit tests

Optimize performance for large documents

📚 Dependencies
Python 3.7+

medspaCy ≥ 1.0.0

spaCy ≥ 3.0.0

en_core_web_sm

📄 License
MIT

🙏 Acknowledgments
medspaCy team for the clinical NLP library

spaCy for the core NLP framework

MIMIC-III dataset for clinical text examples
