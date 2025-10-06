# Study-AI Qwen Code Extension

## Overview
The extension helps students prepare for exams by processing lecture PDF slides in a two-stage pipeline:
1. **Preprocessing**: Clean and extract content from PDFs
2. **Analysis**: Generate structured study notes with key topics and explanations

## Setup Instructions

### 1. Install Required Packages

```bash
sudo apt-get update
sudo apt-get install -y npm nodejs uv git
```

### 2. Install an AI CLI (Choose One)

#### Option A: Qwen Code

```bash
npm install -g @qwen-code/qwen-code@latest
qwen --version
```

#### Option B: Gemini CLI

```bash
npm install -g @google/gemini-cli@latest
gemini --version
```

### 3. Set Up the Study-AI Extension

Your `<workspace>` is the folder where you keep your lecture slides (for example, `~/Documents/COMP417`).

```bash
mkdir -p <workspace>/.qwen/extensions
cd <workspace>/.qwen/extensions
git clone https://github.com/planetis-m/study-ai.git
cd <workspace>
```

### 4. Run Your Chosen CLI

#### If using Qwen Code:

```bash
qwen
```

#### If using Gemini CLI:

```bash
gemini
```

Then run `/help` to confirm that the `study-ai` commands are available.

## Usage Examples

```bash
# Clean a single PDF
/study-ai:clean lecture1.pdf

# Clean specific pages
/study-ai:clean lecture1.pdf --start-page 5 --end-page 15

# Analyze already-cleaned text content
/study-ai:analyze "Paste your cleaned slide content here..."

# Complete pipeline (extract, clean, analyze)
/study-ai:study-notes lecture1.pdf

# Redirect output to a file
/study-ai:study-notes lecture1.pdf > notes-lecture1.md

# Process multiple PDFs
/study-ai:batch-process "lecture1.pdf
lecture2.pdf
lecture3.pdf"

# Use OCR for scanned PDFs
/study-ai:study-notes scanned-lecture.pdf --use-ocr yes
```

## Extension Directory Structure

```
study-ai/
├── AGENTS.md            # Context file with assistant behavior
├── qwen-extension.json  # Extension config
└── commands/
    └── study-ai/
        ├── clean.toml           # Preprocessing command
        ├── analyze.toml         # Analysis command
        ├── study-notes.toml     # Complete pipeline command
        └── batch-process.toml   # Batch processing command
```

## Key Design Decisions

1. **Separation of Concerns**: Commands are separated into discrete stages (clean, analyze) while also providing a convenient combined command (study-notes)
2. **Flexible Input**: Users can either pipe PDF files directly or paste pre-extracted text for analysis
3. **Context-Driven Behavior**: The AGENTS.md file establishes the assistant's role and behavior patterns, which commands reinforce through their specific prompts
4. **Integration with pdf-reader**: Commands leverage the existing PDF tools (`read_pdf_text`, `read_by_ocr`) without reimplementing PDF parsing
5. **Exam-Focused**: All prompts emphasize exam preparation, key topics, and deep understanding rather than general summarization

