# Docling OCR Task

## Table of Contents

- [What is Docling OCR?](#what-is-docling-ocr)
- [What is OCR?](#what-is-ocr)
- [Repo Structure](#repo-structure)
- [Python package manager](#python-package-manager)
- [Setup](#setup)
- [## Parsing documents using OCR-engines](#Parsing-documents-using-OCR-engines)
  - [EasyOCR](#1-easyocr)
  - [RapidOCR](#2-rapidocr)
  - [Tesseract](#3-tesseract)
  - [TesserOCR](#4-tesserocr)
- [Supported Language Codes](#supported-language-codes)
- [Let's analyse these different OCR-engines.](Let's-analyse-these-different-OCR-engines.)
- 

---

## What is Docling OCR?

Docling OCR is an open-source document processing library developed by IBM Research. It is designed to parse and convert complex, multilingual documents — including scanned PDFs — into structured formats like Markdown or JSON, making them ready for translation or further processing.

---

## What is OCR?

**OCR** (Optical Character Recognition) is the technology that extracts text from:

- Images
- Scanned PDFs
- Multilingual documents

---

## Repo Structure

```
├── original_scanned_pdfs/
|   ├── arabic_scanned.pdf
|   ├── french_scanned_pdf.pdf
|   ├── hindu_scanned.pdf     
├── outputs/                      
│   ├── easyocr_outputs 
|       ├── arabic_scanned.md
|       ├── french_scanned.md
|       ├── hindu_scanned.md
│   ├── rapidocr_outputs
|       ├── arabic_scanned.md
|       ├── french_scanned.md
|       ├── hindu_scanned.md
│   ├── tesseract_outputs
|       ├── arabic_scanned.md
│   └── tesserocr_outputs
|       ├── arabic_scanned.md
├── Screenshots/
|       ├── screenshots(windows)
|           ├── 1. creating_folder_and_venv.jpeg
|           ├── 2. installing_docling.jpeg
|           ├── 3. installing_easyocr.jpeg
|           ├── 4. installing_easyocr_separately.jpeg
|           ├── 5. checking_versions.jpeg
|       ├── screenshots(fedora linux)/
|           ├── 1. creating_folder_pyversion.jpeg
|           ├── 2. installing_docling.jpeg
|           ├── 3. easyocr_install.jpeg
|           ├── 4. docling_easyocr_versions.jpeg
|           ├── 5. easyocr_output.jpeg
|           ├── 6. rapidocr_install.jpeg
|           ├── 7. onnxruntime_rapidocr_install.jpeg
|           ├── 8. rapidocr_output.jpeg
|           ├── 9. tesseract_install.jpeg
|           ├── 10. tesseract_output.jpeg
|           ├── 11.tesserocr_install_version.jpeg
├── .gitignore   
└── README.md
```

---

## Python package manager

- Python 3.8+
- pip

For scanned multilingual PDFs to use as test documents, [this site here](https://archive.org/) create an account, search for documents in your target language, and download as PDF.

---

## Setup

**1. Create a project folder and navigate into it:**

```bash
mkdir docling_ocr_project
cd docling_ocr_project
```

**2. Create and activate a virtual environment:**

```bash
python -m venv venv
source venv/bin/activate       # Linux / macOS
source venv\Scripts\activate          # Windows
```

**3. Install Docling** (this may take a few minutes):

```bash
pip install docling
```

**4. Create an output folder:**

```bash
mkdir outputs
cd outputs
mkdir easyocr_outputs
mkdir rapidocr_outputs
mkdir tesseractocr_outputs
mkdir tesserocr_outputs
```

---

## Parsing documents using OCR-engines

The general pattern for running Docling CLI is:

```bash
docling <path/to/your.pdf> \
  --ocr \
  --force-ocr \
  --ocr-engine <engine> \
  --ocr-lang <lang-code> \
  --to md \
  --output ./outputs/
```

### 1. EasyOCR

Install:

```bash
pip install easyocr
```

Run:

```bash
docling original_scanned_pdfs/french-document.pdf \
  --ocr \
  --ocr-engine easyocr \
  --ocr-lang fr \
  --to md \
  --output ./outputs/
```

---

### 2. RapidOCR

Install:

```bash
pip install rapidocr
pip install onnxruntime    # required dependency
```

Run:

```bash
docling original_scanned_pdfs/arabic-document.pdf \
  --ocr \
  --force-ocr \
  --ocr-engine rapidocr \
  --to md \
  --output ./outputs/
```

---

### 3. Tesseract

Install:

```bash
pip install tesseract
```

Tesseract requires a separate language data file for each language. For example, to download Arabic:

```bash
curl -L https://github.com/tesseract-ocr/tessdata/raw/main/ara.traineddata \
  -o ~/tessdata/ara.traineddata
```

Run:

```bash
docling original_scanned_pdfs/arabic-document.pdf \
  --ocr \
  --force-ocr \
  --ocr-engine tesseract \
  --to md \
  --output ./outputs/
```

---

### 4. TesserOCR

TesserOCR uses Tesseract internally and provides a Python binding.

Install:

```bash
pip install tesserocr
```

Run:

```bash
docling original_scanned_pdfs/arabic-document.pdf \
  --ocr \
  --force-ocr \
  --ocr-engine tesserocr \
  --to md \
  --output ./outputs/
```


---

## Supported Language Codes

Use these codes with the `--ocr-lang` flag:

| Language | Code | Language | Code |
|---|---|---|---|
| English | `en` | Arabic | `ar` |
| Hindi | `hi` | Chinese (Simplified) | `ch_sim` |
| French | `fr` | Chinese (Traditional) | `ch_tra` |
| German | `de` | Japanese | `ja` |
| Spanish | `es` | Korean | `ko` |
| Portuguese | `pt` | Russian | `ru` |
| Italian | `it` | Dutch | `nl` |
| Telugu | `te` | | |

---


### Let's analyse these different OCR-engines.
#### 1. Easyocr
- It is easy to use you just install easyocr then input your parsing code and that's it.
- However, it takes a lot of time to parse your document, it is realy slow.
- Doesn't give the best results. Gave a completely different and poor french output compared to other ocr-engines

#### 2. Rapidocr
- You have to install onnxruntime.
- As the word itself says it is really fast and installation is not complex at all.

#### 3. Tesseract
- You have to install a lot more packages hence the installation is really complex.
- For every language you must upload it's own package. 
- Give really good results.

#### 4. Tesserocr
- Uses tesseract internally.
- A bit complex when installing.
