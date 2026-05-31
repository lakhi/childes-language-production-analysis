# Comparative Analysis of Language Production in Late- vs. Typical-Talking Toddlers

A data science project exploring differences in language production between late-talking toddlers (with language impairment) and typically-developing toddlers, using the Ellis Weismer longitudinal corpus from the CHILDES database.

### View the notebook

If GitHub's renderer doesn't load, open it directly in nbviewer:
[**Open in nbviewer →**](https://nbviewer.org/github/lakhi/childes-language-production-analysis/blob/main/lg_production_comparative_analysis_with_outputs_with_classifier.ipynb)

> **Note:** Read `final_project_document_akshay_lakhi.pdf` before the notebook — it provides the full theoretical background and methodology rationale. The notebook contains the code, inline comments, and all output tables/figures.

---

## Background

Child language acquisition follows a species-specific biological progression (Gleitman & Newport, 1995). This project investigates that progression by comparing language production in two groups across a 5-year longitudinal study:

- **Late Talkers (LT):** Children with language impairment
- **Typically Developing (TD):** Age-matched controls

The goal is to identify whether differences in language production are measurable and significant, and to shed light on the developmental trajectory of typical language acquisition.

---

## Dataset

**Ellis Weismer Corpus** — sourced from [CHILDES](https://childes.talkbank.org/access/Clinical-Eng/EllisWeismer.html) (Weismer, 2013)

- **N = 112** (56 late talkers, 56 TD controls), matched on age, nonverbal cognition, and SES
- **Longitudinal:** Language samples collected at ages **2;6, 3;6, 4;6, and 5;6**
- **Session formats:** Examiner-Child (EC), Parent-Child (PC), Structured Interview (INT), Conversation (CON)
- Raw data in CHAT format (`.cha`) and XML format (`.xml`) — both included as zips

---

## Methods

Two Python libraries were used and compared for processing the CHAT corpus data:

| Library | Strengths | Weaknesses |
|---|---|---|
| **PyLangAcq** | Specialised for CHILDES; intuitive Python objects; more out-of-the-box developmental measures (TTR, IPSyn) | MLU-morpheme values trend high |
| **NLTK** | More functions for raw/utterance-level text analysis | More cumbersome for CHILDES; no folder-level corpus object |

An ancillary outcome is a methods comparison between the two libraries for child language data analysis.

### Developmental Measures Analysed

- **MLU (Mean Length of Utterance)** — in both morphemes and words; primary measure used for conclusions
- **TTR (Type-Token Ratio)** — excluded from final conclusions (sensitive to text length differences between groups)
- **IPSyn (Index of Productive Syntax)** — excluded (measures structural comprehension, not production)

---

## Key Findings

MLU (words and morphemes) reliably distinguishes the two groups:

- TD children's mean MLU **consistently exceeds** LT children's across most conversation formats and age points (2;6 → 5;6)
- The one exception is the 4;6 examiner-child format, where scores converge (reason unexplained)
- NLTK MLU-morpheme scores align more closely with published norms than PyLangAcq scores

This supports Rice et al. (2010), who validated MLU as a reliable index of normative language acquisition and a marker of language impairment.

The notebook also includes a **supervised classifier** trained on developmental measures at 2;6 to predict late-talker status at later ages.

---

## Repository Contents

```
.
├── lg_production_comparative_analysis_with_outputs_with_classifier.ipynb  # Main analysis notebook
├── EllisWeismer.zip          # CHAT (.cha) corpus — used by PyLangAcq
├── corpora_for_nltk.zip      # XML corpus — used by NLTK
├── final_project_document_akshay_lakhi.pdf  # Full project write-up
└── README.md
```

---

## How to Run

1. **Clone the repo and extract the data:**
   ```bash
   git clone <repo-url>
   cd <repo-name>
   unzip EllisWeismer.zip
   unzip corpora_for_nltk.zip
   ```

2. **Install dependencies:**
   ```bash
   pip install pylangacq nltk pandas matplotlib seaborn scikit-learn jupyter
   ```
   Then in Python, download the NLTK tokenizer:
   ```python
   import nltk; nltk.download('punkt')
   ```

3. **Open the notebook:**
   ```bash
   jupyter notebook lg_production_comparative_analysis_with_outputs_with_classifier.ipynb
   ```

---

## References

- Ellis Weismer, S., Venker, C., Evans, J. L., & Moyle, M. (2013). Fast mapping in late-talking toddlers. *Applied Psycholinguistics, 34*, 69–89.
- Gleitman, L., & Newport, E. (1995). The invention of language by children. In *Language: An invitation to cognitive science* (2nd ed.). MIT Press.
- Lee, J. L., et al. (2016). Working with CHAT transcripts in Python. Technical report TR-2016-02, University of Chicago.
- MacWhinney, B. (2000). *The CHILDES Project: Tools for analyzing talk* (3rd ed.). Lawrence Erlbaum.
- Rice, M. L., et al. (2010). Mean length of utterance levels in 6-month intervals for children 3 to 9 years with and without language impairments. *JSLHR, 53*(2), 333–349.
- Sanchez, A., et al. (2019). childes-db: a flexible and reproducible interface to CHILDES. *Behavior Research Methods, 51*(4), 1928–1941.
- Scarborough, H. S. (1990). Index of Productive Syntax. *Applied Psycholinguistics, 11*(1), 1–22.
