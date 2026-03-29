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
- [why these OCR engines](why-these-ocr-engines)
- [Let's analyse these different OCR-engines.](Let's-analyse-these-different-OCR-engines.)
- [Evaluating the findings](evaluating-the-findings)

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
Fedora
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/p0dd2jyt5tohbfvdfvxy.jpeg)

Windows

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5hj3pb47r0hyvqaaifh7.jpeg)

**3. Install Docling and easy ocr** (this may take a few minutes):

```bash
pip install docling
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bs97icmg6rxw3fw38g2k.png)

easy ocr install

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qvmcogez8rvu9nd8g27d.png)

Windows

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5f45c9xjk6zi6hbhk4px.jpeg)

#### Check for the versions of both docling and easyocr.
Fedora

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/j2yid78jnbkjjvbyid7c.png)

Windows

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zks7nbt169d9kmumufez.jpeg)

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
Easy OCR output
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4ueh79wx2zgw1no3lc2s.png)
 
---

### 2. RapidOCR

Install:

```bash
pip install rapidocr
pip install onnxruntime    # required dependency
```
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/yyg3jn3ibr1r4mo9tle6.jpeg)
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xd5xjlo1v9es8p50q5qr.png)
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
Rapidocr output
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0xbxfve1pibaqqylmzoi.png)

 
### 3. Tesseract

Install:

```bash
pip install tesseract
```
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ecj1l6pfot1c0j5z5kdf.png)

Tesseract requires a separate language data file for each language. For example, to download Arabic:

```bash
curl -L https://github.com/tesseract-ocr/tessdata/raw/main/ara.traineddata \
  -o ~/tessdata/ara.traineddata
```
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/oitfh2zzqi90stuwa0mo.png)
Run:

```bash
docling original_scanned_pdfs/arabic-document.pdf \
  --ocr \
  --force-ocr \
  --ocr-engine tesseract \
  --to md \
  --output ./outputs/
```
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/msm9ixunr2rkap1hq0f0.png)

---

### 4. TesserOCR

TesserOCR uses Tesseract internally and provides a Python binding.

Install:

```bash
pip install tesserocr
```
- install the ocr and check the version.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/r22tesedex591hi9sihn.png)
- Requires one to install each language package

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/254ccx6x0ijcsnuwaf5j.png)


Run:

```bash
docling original_scanned_pdfs/arabic-document.pdf \
  --ocr \
  --force-ocr \
  --ocr-engine tesserocr \
  --to md \
  --output ./outputs/
```
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3k69j6f7e37mwcpnotmm.png)


---

## Supported Language Codes easyocr
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

## Supported Language Codes — Tesseract OCR, Tesserocr and Rapidocr
Use these codes with the `--ocr-lang` flag:

| Language | Code | Language | Code |
|---|---|---|---|
| English | `eng` | Arabic | `ara` |
| Hindi | `hin` | Chinese (Simplified) | `chi_sim` |
| French | `fra` | Chinese (Traditional) | `chi_tra` |
| German | `deu` | Japanese | `jpn` |
| Spanish | `spa` | Korean | `kor` |
| Portuguese | `por` | Russian | `rus` |
| Italian | `ita` | Dutch | `nld` |
| Telugu | `tel` | | |


### Why these OCR engines
- I used easy OCR as it is really easy to use
- The Rapid OCR is really fast.
- the tesseract and tesserocr give good results.

### Let's analyse these different OCR-engines.
#### 1. Easyocr
- It is easy to use you just install easyocr then input your parsing code and that's it.
- However, it takes a lot of time to parse your document, it is realy slow.
- Doesn't give the best results. Gave a poor french output compared to other ocr-engines
- I also noticed easyocr uses different language codes for different languages compared to the other ocr engines.

#### 2. Rapidocr
- You have to install onnxruntime.
- As the word itself says it is really fast and installation is not complex at all.

#### 3. Tesseract
- You have to install a lot more language packages hence the installation is really complex.
- For every language you must upload it's own package. 
- Give really good results.

#### 4. Tesserocr
- Uses tesseract internally.
- A bit complex when installing.

#### 5 Ocrmac
- Requires mac to install.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ej4afzq4pwd21m77q915.png)


## Result Findimgs
- Other than differing character changes in the french document outputs, the ocr-engines gave almost similar results for the scanned pdfs.
- I used markdown format and it was pretty good.
- Easyocr only combines specific languages , well, I used a multilingual arabic and french scanned document but easyocr could not parse it because of the language combination. The rest of the documents parsed the scanned arabic and french pdf really well and gave good results.
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5asizbb2sd6d5te84bpg.png)

## Using of AI
- I used claude to correct some of the errors I got.




  
