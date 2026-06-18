# AI Tools & ML — Applied NLP Notebooks

> A practical collection of Jupyter notebooks for text extraction, entity recognition, and fuzzy string matching — built around real document-processing tasks (receipts, tax declarations, PDFs).

![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![spaCy](https://img.shields.io/badge/spaCy-09A3D5?style=for-the-badge&logo=spacy&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)

## Overview

This repository is a hands-on toolkit of standalone notebooks for applied Natural Language Processing and data extraction. Each notebook tackles one concrete problem encountered when turning unstructured documents into clean, structured data:

- **Reading PDFs** — pulling text out of scanned and native PDFs via OCR and direct parsing.
- **Extracting tables** — turning PDF tables into Pandas DataFrames.
- **Named-entity & field extraction** — combining spaCy NER, regex, and dependency parsing to capture specific fields from receipts and tax documents.
- **Fuzzy matching** — reconciling noisy input strings (addresses, cities) against a reference dataset.

These are practical, self-contained notebooks — not a packaged framework or library. Treat them as recipes you can read, adapt, and run cell by cell.

## Notebooks

| Notebook | What it does |
|----------|--------------|
| [`PDF-READER.ipynb`](PDF-READER.ipynb) | Extracts text from PDFs using three different approaches and compares them: Tesseract OCR (`pytesseract` + `pdf2image`), `EasyOCR`, and direct text/image/metadata extraction with PyMuPDF (`fitz`). Supports multi-language OCR (e.g. `eng+fra`). |
| [`NLP-PROCESSING.ipynb`](NLP-PROCESSING.ipynb) | Field extraction from receipt / tax text. Runs spaCy NER (`en_core_web_sm`), then layers regex patterns and dependency parsing to capture specific fields (receipt number, bill number, TIN, dates, amounts, address, operation). Collects everything into a Pandas DataFrame and writes it to CSV. |
| [`fuzzywuzy-string-matching-TF.ipynb`](fuzzywuzy-string-matching-TF.ipynb) | Fuzzy string matching for record reconciliation. Uses `fuzzywuzzy` (`fuzz.ratio`) together with a spaCy French model (`fr_core_news_md`) to match noisy postal addresses and city names against a reference spreadsheet, with an optional web-search spelling-correction step. |
| [`tableToDataFrame/extract_from_declaration.ipynb`](tableToDataFrame/extract_from_declaration.ipynb) | Walks through extracting tables from a multi-page declaration PDF with `pdfplumber`, rendering each page to an image for inspection and converting extracted tables into Pandas DataFrames. |
| [`tableToDataFrame/generalizeTheCode.ipynb`](tableToDataFrame/generalizeTheCode.ipynb) | The reusable version of the table-extraction logic. Wraps the workflow into helper functions (`open_pdf`, `extract_tables_from_page`, `process_tables`) that handle single- and multiple-table pages and return a list of DataFrames. |
| [`word-matching.ipynb`](word-matching.ipynb) | Placeholder / scratch notebook (currently empty). |

## Tech Stack

Libraries actually imported across the notebooks:

- **NLP** — [spaCy](https://spacy.io/) (`en_core_web_sm`, `fr_core_news_md` models), Python `re` (regex)
- **Fuzzy matching** — [fuzzywuzzy](https://github.com/seatgeek/fuzzywuzzy)
- **PDF & OCR** — [PyMuPDF (`fitz`)](https://pymupdf.readthedocs.io/), [pdfplumber](https://github.com/jsvine/pdfplumber), [pdf2image](https://github.com/Belval/pdf2image), [pytesseract](https://github.com/madmaze/pytesseract), [EasyOCR](https://github.com/JaidedAI/EasyOCR)
- **Imaging** — [OpenCV (`cv2`)](https://opencv.org/), [Pillow (`PIL`)](https://python-pillow.org/), [Matplotlib](https://matplotlib.org/), [NumPy](https://numpy.org/)
- **Data** — [pandas](https://pandas.pydata.org/), `openpyxl` (Excel I/O via `pd.read_excel`)
- **Web** — `requests`, `serpapi` (optional spelling-correction lookup)

## Getting Started

### 1. Clone and create an environment

```bash
git clone https://github.com/MohamedKhattat/AI-tools-ml.git
cd AI-tools-ml
python -m venv .venv
# Windows:  .venv\Scripts\activate
# macOS/Linux:  source .venv/bin/activate
```

### 2. Install the Python libraries

```bash
pip install jupyter pandas numpy openpyxl requests \
            spacy fuzzywuzzy python-Levenshtein \
            pdfplumber pymupdf pdf2image pytesseract easyocr \
            opencv-python pillow matplotlib
```

Download the spaCy language models used by the notebooks:

```bash
python -m spacy download en_core_web_sm
python -m spacy download fr_core_news_md
```

### 3. Install system OCR dependencies

Some notebooks rely on external binaries:

- **Tesseract OCR** — required by `pytesseract` (`PDF-READER.ipynb`).
- **Poppler** — required by `pdf2image` for converting PDF pages to images.

Install these via your OS package manager (e.g. `apt`, `brew`, or the official Windows builds) before running the OCR cells.

### 4. Launch Jupyter

```bash
jupyter notebook
```

Open any notebook and run the cells top to bottom. Update the local file paths (PDFs, Excel files) at the top of each notebook to point at your own inputs.

## Notes

- **Self-contained & exploratory.** Each notebook is independent and meant to be read and run interactively. There is no shared package, CLI, or installable module.
- **Bring your own inputs.** The notebooks reference local file paths (PDFs, spreadsheets) that are not committed to the repo. Point them at your own documents.
- **Provide your own API keys.** Any third-party service (e.g. the SerpAPI spelling-correction lookup) requires your own credentials — supply them via an environment variable or your own configuration, and never commit keys to the repo.
- **Domain focus.** The example documents are fiscal / administrative (receipts, tax declarations), reflecting an applied focus on document understanding in fiscal-tech contexts.

---
<p align="center">Built by <b>Mohamed Habib Khattat</b> — <a href="https://github.com/MohamedKhattat">GitHub</a> · <a href="https://www.linkedin.com/in/mohamed-habib-khattat-2b206a173">LinkedIn</a></p>
