# 📄 Comprehensive ATS-Friendly Resume Engineering Guide & AI Prompt Blueprint

> **Purpose**: This document provides the complete, end-to-end framework, technical rules, regex considerations, and prompt instructions used to create a **top 3% tier (95%+ score)** ATS-friendly, single-page technical resume from a Master CV.
> 
> You can pass this entire file (or copy the Master Prompt at the bottom) to **any AI (ChatGPT, Claude, Gemini, DeepSeek)** to produce or update resumes following this exact standard.

---

## 📑 Table of Contents
1. [Core Principles of ATS-Friendly Engineering](#1-core-principles-of-ats-friendly-engineering)
2. [Layout & LaTeX Geometry Specifications](#2-layout--latex-geometry-specifications)
3. [Header & Contact Info (Regex-Safe Formatting)](#3-header--contact-info-regex-safe-formatting)
4. [Standard Section Architecture](#4-standard-section-architecture)
5. [Chronological Sorting & Date Formatting Rules](#5-chronological-sorting--date-formatting-rules)
6. [Bullet Point Engineering (Google XYZ Formula)](#6-bullet-point-engineering-google-xyz-formula)
7. [Forbidden Buzzwords & Cliche Blacklist](#7-forbidden-buzzwords--cliche-blacklist)
8. [Project Header & Live Demo Linking Architecture](#8-project-header--live-demo-linking-architecture)
9. [Pre-Flight Terminal Verification Checklist](#9-pre-flight-terminal-verification-checklist)
10. [Master Prompt for Other AIs (Copy-Paste Ready)](#10-master-prompt-for-other-ais-copy-paste-ready)

---

## 1. Core Principles of ATS-Friendly Engineering

Applicant Tracking Systems (Workday, Taleo, Greenhouse, Lever, iCIMS) parse PDF files into plain text before matching candidates against job criteria. To guarantee a 95%+ parse rate:

- **Single-Column Linear Layout ONLY**: Never use two-column layouts, tables for positioning, sidebars, or floating boxes. Modern ATS parsers read horizontally across columns, scrambling the text into unreadable gibberish.
- **Searchable Text (Type-1 Fonts)**: Resumes must be compiled via LaTeX (`pdflatex`) using standard scalable vector fonts (Computer Modern or TeX Gyre). Never flatten text into images or use canvas-based designs.
- **No Graphics, Icons, or Rating Bars**: Progress bars (e.g. 80% Python) and star icons (⭐⭐⭐) cannot be read by ATS parsers and trigger parsing errors.
- **Strict 1-Page Constraint**: For early-career or undergraduate engineers, the resume must fit **strictly on 1 page (A4 or Letter)**. An accidental 2nd page with 2–3 trailing lines drops recruiter impression significantly.

---

## 2. Layout & LaTeX Geometry Specifications

To fit comprehensive technical substance on exactly one page without looking crowded, use these exact parameters in LaTeX:

```latex
\documentclass[10pt,a4paper]{article}

% Margin: 0.42in top/bottom, 0.48in left/right maximizes printable area while remaining within safe printer margins
\usepackage[a4paper,top=0.42in,bottom=0.42in,left=0.48in,right=0.48in]{geometry}
\usepackage{enumitem}
\usepackage{hyperref}
\usepackage{titlesec}
\usepackage{xcolor}

% Itemize spacing: Zero margin padding, compact bullet indentation
\setlist[itemize]{noitemsep, topsep=1pt, parsep=0pt, partopsep=0pt, leftmargin=1.15em}
\setlength{\parindent}{0pt}
\setlength{\parskip}{0pt}

% Section titles: Tight spacing with horizontal divider rule
\titleformat{\section}{\large\bfseries}{}{0em}{}[\vspace{-2pt}\titlerule]
\titlespacing*{\section}{0pt}{3pt plus 1pt minus 1pt}{2pt plus 1pt minus 1pt}

\hypersetup{
    colorlinks=true,
    linkcolor=black,
    urlcolor=blue
}
```

---

## 3. Header & Contact Info (Regex-Safe Formatting)

ATS parsers (especially Jobscan and Taleo) use strict regular expressions to validate candidate location, phone, and email. Failing these regexes causes "Contact Info Not Found" errors.

### Safe Formatting Rules:
1. **Location**: Use `City, Country` format (e.g. `Dhaka, Bangladesh`). Do not use 3-tier municipal names like `Gazipur, Dhaka, Bangladesh` which fail city-lookup databases.
2. **Phone Number**: Always format with country code, space, and local grouping (e.g. `+880 1740-071118`). Avoid unspaced strings like `+8801740071118`.
3. **Email**: Use standard university or professional domain. Use `\enspace$|$\enspace` or standard pipe delimiters so regex tokenizers do not concatenate fields.
4. **Professional Headline**: Place target engineering title immediately below your name (e.g. `Embedded Systems & Edge AI Engineer`).

### Verified LaTeX Implementation:
```latex
\begin{center}
    {\LARGE \textbf{Full Name}} \\
    \vspace{2pt}
    \textbf{Embedded Systems \& Edge AI Engineer} \\
    \vspace{2pt}
    \small
    Dhaka, Bangladesh \enspace$|$\enspace +880 1740-071118 \enspace$|$\enspace \href{mailto:email@domain.com}{email@domain.com} \\
    \href{https://linkedin.com/in/username}{linkedin.com/in/username} \enspace$|$\enspace \href{https://github.com/username}{github.com/username}
\end{center}
\vspace{-4pt}
```

---

## 4. Standard Section Architecture

Do **NOT** invent creative section titles (like "Things I Built" or "Core Passions"). Always use universal ATS-recognized standard headers:

| Section Header | ATS Recognition | Purpose |
|---|:---:|---|
| **`Professional Summary`** | 100% | 3–4 line high-density elevator pitch. |
| **`Technical Skills`** | 100% | Hard skills categorized into 5–6 ATS keyword buckets. |
| **`Experience`** | 100% | Industry, research, or published open-source developer roles. |
| **`Technical Projects`** | 100% | Top 3 high-impact engineering projects. |
| **`Education`** | 100% | Running degree, university, major, and graduation year. |
| **`Leadership & Activities`** | 100% | Extracurricular leadership, competition segment leads, club executive roles. |

> [!IMPORTANT]
> **Avoid Hybrid Headers**: Do NOT use `Experience & Open Source` or `Projects & Works`. Legacy ATS parsers fail to categorize hybrid headers and dump them into "Uncategorized". Simply use `Experience` and `Technical Projects`.

---

## 5. Chronological Sorting & Date Formatting Rules

ATS algorithms (e.g. Resume Worded) penalize inconsistent date formats and out-of-order timelines.

### The Rules:
1. **Strict Reverse Chronological Order**:
   - Ongoing roles (`Present`) must be listed at the top.
   - Finished roles/projects must be sorted by **end date**, newest first:
     - `May 2026 – Sep 2026` (Ended Sep 2026) $\rightarrow$ 1st
     - `Jan 2026 – Sep 2026` (Ended Sep 2026) $\rightarrow$ 2nd
     - `Jun 2026 – Aug 2026` (Ended Aug 2026) $\rightarrow$ 3rd
2. **Uniform 3-Letter Month Abbreviations**:
   - Always use 3 letters for every month: `Jan`, `Feb`, `Mar`, `Apr`, `May`, `Jun`, `Jul`, `Aug`, `Sep`, `Oct`, `Nov`, `Dec`.
   - **Common Pitfall**: Never write `Sept 2026`. Always write `Sep 2026`. Mixing 4-letter and 3-letter months triggers ATS consistency penalties.

---

## 6. Bullet Point Engineering (Google XYZ Formula)

Every single bullet point must follow the **Google XYZ Formula**:
$$\text{Accomplished [X] as measured by [Y] by doing [Z]}$$

### Anatomy of an Elite Bullet Point:
1. **Lead with a Heavyweight Action Verb**: *Architected, Engineered, Designed, Deployed, Implemented, Automated, Formulated.*
2. **State Specific Hardware / Protocols / Algorithms**: *ESP32, FreeRTOS, TreeSHAP, NVS boot counters, HTTPS, LoRa, MQTT.*
3. **Include Quantified Metrics (Mandatory)**:
   - *Verified across **15+ physical ESP32 nodes** with **0% bricking rate**.*
   - *Achieved **sub-100ms local inference** across **5 atmospheric parameters**.*
   - *Reduced provisioning time from **minutes to under 30 seconds**.*
   - *Eliminated manual flashing across **100% of device deployments**.*

---

## 7. Forbidden Buzzwords & Cliche Blacklist

Resume Worded, Jobscan, and technical recruiters deduct points for subjective claims that add no technical value.

### 🚫 Words to Ban & Replaced With Action:
| Vague Buzzword | Why It Fails | Replacement Technical Phrasing |
|---|---|---|
| *"Specializes in"* | Subjective claim | *"Experienced in C/C++ firmware development and FreeRTOS multitasking..."* |
| *"Robust firmware"* | Overused filler adjective | State the mechanism: *"Dual-partition OTA with automated rollback"* |
| *"Dependable / Field-ready"* | Unsubstantiated buzzword | State the test metric: *"Verified under simulated power and network drops"* |
| *"Commercial IoT"* | Buzzword | *"Production-grade microcontroller deployments"* |
| *"Intelligent system"* | Generic filler | State the exact algorithm: *"Risk-aware quantile forecasting model"* |
| *"Hardworking / Passionate"* | 0 technical value | Eliminate completely. Let project metrics prove capability. |

---

## 8. Project Header & Live Demo Linking Architecture

For technical projects, recruiters want to see three things immediately: Title, Source/Live Link, and Tech Stack.

### 3-Line Project Architecture:
```latex
\textbf{RespiGuard --- Explainable Edge AI Respiratory Risk Monitoring} \hfill \textit{May 2026 -- Sep 2026} \\
\href{https://github.com/Masud744/RespiGuard}{github.com/Masud744/RespiGuard} \,|\, \href{https://respiguard-fvh9.onrender.com/}{Live: respiguard-fvh9.onrender.com} \\
\textit{ESP32, PMS5003, MQ-135, DHT22, FreeRTOS, FastAPI, TreeSHAP, React, Vite, Supabase, Groq LLaMA 3.3, Render}
\begin{itemize}
    \item Designed an ESP32 edge sensing node (PMS5003 laser particulate counter, MQ-135, DHT22) running FreeRTOS firmware to collect localized air quality telemetry across 5 atmospheric parameters.
    \item Deployed a hierarchical ML model with dynamic TreeSHAP explainability for asthma triage, achieving sub-100ms local inference; built real-time React 18 dashboard on Render with geospatial risk maps and Groq LLaMA-3.3 copilot.
\end{itemize}
```

- **Line 1**: Clear product-style title with right-aligned date range.
- **Line 2**: Clickable GitHub repository link followed by clickable Live Demo URL (if deployed).
- **Line 3**: Exhaustive, italicized tech stack containing microcontrollers, sensors, ML libraries, and cloud hosts.
- **Lines 4–5**: Exactly 2 metric-rich bullet points.

---

## 9. Pre-Flight Terminal Verification Checklist

Before uploading a compiled PDF to any ATS platform, run these terminal commands locally:

### 1. Test Text Extractability & Parsing
```bash
pdftotext resume.pdf - | head -n 30
```
*Verification*: Ensure output contains clean text with zero scrambled characters or broken ligatures.

### 2. Verify Page Count is Exactly 1
```bash
pdfinfo resume.pdf | grep "Pages:"
```
*Verification*: Must output `Pages: 1`.

### 3. Verify Contact Info Extraction Regex
```bash
python3 -c "
import subprocess, re
text = subprocess.check_output(['pdftotext', 'resume.pdf', '-']).decode('utf-8')
print('Phone match:', bool(re.search(r'\+?\d{1,3}[\s-]\d{3,4}[\s-]\d{4,6}', text)))
print('Email match:', bool(re.search(r'[\w\.-]+@[\w\.-]+', text)))
print('Location match:', 'Dhaka, Bangladesh' in text)
"
```
*Verification*: All three assertions must return `True`.

### 4. Verify 3-Letter Month Uniformity
```bash
python3 -c "
import subprocess, re
text = subprocess.check_output(['pdftotext', 'resume.pdf', '-']).decode('utf-8')
assert 'Sept' not in text, 'Error: Found Sept instead of Sep'
print('Date check passed: All months are valid 3-letter abbreviations.')
"
```

---

## 10. Master Prompt for Other AIs (Copy-Paste Ready)

Copy and paste the entire block below into ChatGPT, Claude, Gemini, or DeepSeek whenever you want it to build, update, or tailor your resume:

```text
Act as a Principal Embedded Systems Engineer and Tier-1 ATS Resume Specialist.
Your task is to generate or update a 1-page, ATS-optimized LaTeX resume for Shahriar Alom Masud.

You MUST strictly comply with these technical rules:
1. LAYOUT & LENGTH:
   - Single-column linear layout ONLY. Absolutely NO tables, minipages, icons, or floating boxes.
   - Use LaTeX article class with geometry: [a4paper, top=0.42in, bottom=0.42in, left=0.48in, right=0.48in].
   - Must fit EXACTLY on 1 single page (0 overflow onto page 2).
   - Use \titlespacing*{\section}{0pt}{3pt plus 1pt minus 1pt}{2pt plus 1pt minus 1pt} and compact \setlist[itemize].

2. HEADER & CONTACT:
   - Title: Embedded Systems & Edge AI Engineer
   - Location: Dhaka, Bangladesh
   - Phone: +880 1740-071118 (Must include space and hyphen for regex compatibility)
   - Email: shahriar0002@std.uftb.ac.bd
   - Links: linkedin.com/in/shahriar-alom-masud and github.com/Masud744 separated by \enspace$|$\enspace

3. SECTION HEADERS:
   - Use ONLY standard headers: Professional Summary, Technical Skills, Experience, Technical Projects, Education, Leadership & Activities.
   - Do NOT use hybrid headers like "Experience & Open Source". Use "Experience".

4. CHRONOLOGY & DATES:
   - Strict reverse-chronological order: ongoing/present roles first, then newest end dates to oldest.
   - Use standard 3-letter month abbreviations ONLY (Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec). Never write "Sept".

5. BULLET POINTS & BUZZWORDS:
   - Every bullet must follow the Google XYZ Formula: [Action Verb] + [Specific Hardware/Stack] + [Quantified Metric].
   - Must include verifiable numbers (e.g., "15+ physical ESP32 nodes", "0% bricking rate", "sub-100ms inference", "under 30 seconds").
   - Strictly BAN subjective buzzwords: "specializes in", "robust", "dependable", "field-ready", "commercial", "intelligent", "passionate".

6. PROJECTS SELECTION:
   - Feature SmartProv (v2.1.3 on Arduino Library Manager) under Experience.
   - Feature 3 flagship projects under Technical Projects:
     a) RespiGuard (May 2026 – Sep 2026) with Live Demo link
     b) Solar-Aware HEMS (Jan 2026 – Sep 2026) with Live Demo link
     c) ESP32 SmartProv GitHub OTA System (Jun 2026 – Aug 2026)
   - Include complete tech stacks in italics under project links.

Provide valid, compilation-ready LaTeX source code that compiles with pdflatex without warnings or overfull hboxes.
```
