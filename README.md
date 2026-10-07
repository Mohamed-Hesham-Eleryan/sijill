<div align="center">

# Sijill · سجل

**A bilingual document workspace that turns PDFs, spreadsheets, Word and PowerPoint files, and photos into clean tables, charts and summaries.**

Runs entirely in the browser as a single HTML file. Your documents never leave your device.

[**Live demo**](https://mohamed-hesham-eleryan.github.io/sijill/)

![Single file](https://img.shields.io/badge/single-HTML%20file-0B7A6B)
![No backend](https://img.shields.io/badge/backend-none-0B7A6B)
![Languages](https://img.shields.io/badge/UI-English%20%7C%20Arabic%20(RTL)-0B7A6B)
![Build](https://img.shields.io/badge/build%20step-none-0B7A6B)

</div>

---

## Overview

Sijill is a document workspace for financial and business files. Drop in a file and it extracts the tables, flags anything that needs a human check, and lets you view the result as a table, a chart, a summary, or a short presentation. Everything is stored locally in your browser.

It is built as one self-contained `index.html`: no server, no build tooling, no account.

## Features

### Import
- **Formats:** XLSX, CSV/TSV, PDF, DOCX, PPTX, TXT and images (JPG, PNG, WebP, GIF, BMP)
- **Real type detection:** the file type is read from the file's bytes, not its extension
- **PDF table extraction:** rebuilds tables from positioned text, including right-to-left layouts
- **Built-in OCR (English + Arabic)** for scanned PDFs and photos, with a confidence score
- **Camera capture** on mobile, **drag and drop** anywhere on the page, and **multi-file upload** with per-file progress
- **Paste text or a chat export** and read it as a document
- **Manual entry** with an empty editable table
- **Duplicate detection** using SHA-256, so the same file is not imported twice

### Review
- Documents read from PDFs or images are marked **Needs review** until you confirm them
- **Inline table editing**, add rows, save changes
- Automatic or manual choice of the **key figure** for each document
- Per-document **info panel** (pages, OCR pages, confidence, currency detected), **re-read with OCR**, and **download the original file**

### Analyse
- **Charts:** bar and line, powered by Chart.js
- **Auto-generated summary** of the key numbers
- **Presentation mode** with keyboard navigation (title, chart, summary)
- **Search** across document names and every table row, filtered by category
- **Compare several documents together** in a combined summary, chart or merged table
- **Categories:** Financial, Real estate, General

### Currency
- Totals can be shown in **SAR, USD, AED, TRY, EGP or EUR**
- **Live exchange rates** with an offline reference fallback
- **Manual rate overrides** are clearly marked, logged, and ask for confirmation if they deviate sharply from the live rate

### Export
| Format | Notes |
|---|---|
| **XLSX** | One sheet per table plus an Info sheet, frozen header, RTL-aware |
| **PDF** | Paginated report with logo, summary, chart and tables |
| **PPTX** | Title, summary, chart and table slides |
| **CSV** | UTF-8 with BOM for Excel, protected against formula injection |

### Interface
- Full **Arabic (RTL) and English** UI, switchable at any time
- **Light and dark** themes
- Responsive layout with a sidebar on desktop and a drawer plus bottom dock on mobile
- Respects `prefers-reduced-motion`; keyboard and screen-reader friendly controls
- **Installable as an app** when served over HTTPS (icon is generated at runtime)

## Privacy and security

- **No backend.** Documents and extracted data are stored in the browser's **IndexedDB**; settings in `localStorage`.
- The only network requests are for open-source libraries (loaded on demand from cdnjs), Google Fonts, and the exchange-rate API.
- All imported text is HTML-escaped before rendering.
- PDF parsing runs with `isEvalSupported: false` to mitigate pdf.js CVE-2024-4367.
- Office files are size-checked after decompression to guard against zip bombs, and spreadsheet row/column indexes are bounded.
- CSV exports neutralise cells that start with `=`, `+`, `-` or `@`.
- A Content Security Policy blocks plugins, `<base>` tags and form submission.

> Data is stored **unencrypted** on the device. Use the clear-workspace button (trash icon in the sidebar) on shared computers.

## Limits

| Item | Limit |
|---|---|
| File size | 40 MB |
| PDF pages read | 60 |
| OCR pages per PDF | 12 |
| Rows per table | 3,000 |
| Unpacked Office file | 200 MB |

Legacy Office formats (`.xls`, `.doc`, `.ppt`) and HEIC photos are not supported. Save them as `.xlsx` / `.docx` / `.pptx` or JPG first.

## Getting started

**Use it online:** open the [live demo](https://mohamed-hesham-eleryan.github.io/sijill/).

**Run it locally:** download `index.html` and open it in a modern browser. An internet connection is needed the first time a feature loads its library (PDF, OCR, export).

**Host it yourself:**
1. Put `index.html` in a repository.
2. Go to **Settings → Pages**, choose **Deploy from branch**, select `main` and `/ (root)`.
3. Open `https://<username>.github.io/<repository>/`.

On a first run with no documents, use **Load sample data** to explore the interface.

## Tech stack

Vanilla JavaScript, HTML and CSS, with these libraries loaded on demand:

| Purpose | Library |
|---|---|
| Charts | [Chart.js](https://www.chartjs.org/) 4.4 |
| PDF reading | [pdf.js](https://mozilla.github.io/pdf.js/) 3.11 |
| OCR | [Tesseract.js](https://tesseract.projectnaptha.com/) 5.1 |
| Office files and XLSX export | [JSZip](https://stuk.github.io/jszip/) 3.10 |
| PDF export | [html2canvas](https://html2canvas.hertzen.com/) + [jsPDF](https://github.com/parallax/jsPDF) |
| PPTX export | [PptxGenJS](https://gitbrent.github.io/PptxGenJS/) 3.12 |
| Font | IBM Plex Sans Arabic |
| Exchange rates | [open.er-api.com](https://www.exchangerate-api.com/docs/free) |

## Project status

Working prototype. Sample data is clearly labelled as simulated.

## Author

**Mohamed Hesham Eleryan**
Biomedical engineer · [GitHub](https://github.com/Mohamed-Hesham-Eleryan)

## License

Copyright © 2026 Mohamed Hesham Eleryan. All rights reserved.

---

<div dir="rtl" align="right">

## نبذة بالعربي

**سجل** مساحة عمل للمستندات المالية والتجارية تعمل بالكامل داخل المتصفح في ملف HTML واحد. ارفع ملفات Excel أو CSV أو PDF أو Word أو PowerPoint أو صور، وسيستخرج الجداول، وينبّهك لما يحتاج مراجعة، ويعرضها كجداول ورسوم بيانية وملخصات وعرض تقديمي، مع تصدير إلى XLSX وPDF وPPTX وCSV. يدعم العربية (من اليمين لليسار) والإنجليزية، والوضع الفاتح والداكن، وتحويل العملات بأسعار مباشرة. لا يوجد خادم، وجميع بياناتك تبقى على جهازك.

</div>
