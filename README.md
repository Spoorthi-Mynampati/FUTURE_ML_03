# Resume Screening & Ranking System

An NLP-based system that reads resumes, extracts skills, compares them against
a job description, and ranks candidates by role fit — with clear explanations
of why each candidate scored the way they did and which skills they're missing.

Built as part of the **Future Interns – Machine Learning Task 3 (2026)**.

## What it does

Given a job description and a dataset of resumes, the system:
1. Cleans and preprocesses raw resume text
2. Extracts relevant skills from both resumes and the job description
3. Converts text into numerical vectors (TF-IDF) and measures similarity
4. Ranks all candidates by how closely they match the job
5. Shows exactly which required skills each candidate has — and which they're missing
6. Visualizes the top candidates in a simple bar chart

## How it works

| Step | What happens |
|---|---|
| 1. Load data | Resumes loaded from a CSV (`ID`, `Resume_str`, `Category`) |
| 2. Clean text | Lowercase, remove punctuation/extra whitespace |
| 3. Tokenize | Split text into words, remove stopwords ("the", "and", etc.) |
| 4. Extract skills | Match cleaned text against a defined list of skill keywords |
| 5. Parse job description | Same cleaning + skill extraction applied to the job posting |
| 6. Score candidates | TF-IDF vectorization + cosine similarity between each resume and the job description |
| 7. Rank & explain | Sort by similarity score; show matched vs. missing skills per candidate |
| 8. Visualize | Bar chart of the top 10 candidates by score |

### Why cosine similarity?
Both the job description and each resume are turned into vectors of word
importance (TF-IDF). Cosine similarity measures the angle between two vectors
— a score close to 1 means the resume and job description share similar,
important words; a score close to 0 means they don't overlap much. This
mirrors how many real resume-screening tools rank candidates.

## Example output

```
Top candidate: ID 23456789 (INFORMATION-TECHNOLOGY)
Match score: 0.42
Matched skills: python, sql, data analysis, communication
Missing skills: aws, cloud computing, project management
```

## Dataset

[Resume Dataset (Kaggle)](https://www.kaggle.com/datasets/snehaanbhawal/resume-dataset)
— 2,484 resumes across 24 job categories (IT, Finance, HR, Engineering, etc.)

## Tools & libraries

- **Python**
- **pandas** – data loading and handling
- **NLTK** – tokenization, stopword removal
- **scikit-learn** – TF-IDF vectorization, cosine similarity
- **matplotlib** – candidate score visualization

## Project structure

```
resume-screening-nlp/
├── resume_screening.ipynb   # Main notebook (all steps, in order)
├── README.md                # This file
```

## Limitations

- Skill extraction relies on a manually defined keyword list — skills not in
  the list won't be detected, and synonyms (e.g. "JS" vs "JavaScript") aren't
  automatically matched.
- Similarity scoring is based on word overlap (TF-IDF), not deep semantic
  understanding — it won't recognize that "led a team" implies "leadership"
  unless that phrase itself appears.
- Built for learning and demonstration purposes on a beginner-friendly scale,
  not production hiring use.

## Possible improvements

- Use spaCy's `PhraseMatcher` or NER for more flexible skill extraction
- Weight critical skills more heavily in the final score
- Use word embeddings (e.g. spaCy vectors, sentence-transformers) for
  semantic similarity instead of pure keyword overlap

## Author

Built by [Spoorthi Mynampati] as part of the Future Interns Machine Learning internship track.
