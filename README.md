# EDECS-case-study
# Automated RFI Processing Agent

**Problem**: Manual RFI processing in construction delays projects and risks errors. Project managers, engineers, and site supervisors lose time reviewing and responding to RFIs, impacting EDECS’ efficiency.

**Solution**: This agent parses RFI PDFs, extracts details (question, project ID, urgency) using a local LLM, queries project PDFs for context, and generates responses, saving time and reducing errors.

## Setup
1. Clone: `git clone <repo_url>`
2. Create virtual environment: `python -m venv venv && source venv/bin/activate`
3. Install: `pip install -r requirements.txt`
4. Place `sample_rfi1.pdf` and `project_docs/*.pdf` in project directory (use `generate_pdfs.py` to create).
5. Ensure ~8GB RAM and ~2GB disk space for `facebook/bart-large` model.

## Usage
Run: `python rfi_agent.py`  
Output: `rfi_response.txt` with response.

## Example
**Input** (`sample_rfi1.pdf`):  
```
RFI: Request for Information
Project ID: PRJ-001
Question: What is the concrete specification for the foundation of Building A?
Urgency: Medium
```  
**Output** (`rfi_response.txt`): Response citing Grade 30 concrete from project docs.

## Design Choices
- **pdfplumber**: Reliable PDF text extraction for RFIs and project docs.
- **HuggingFacePipeline**: Local `facebook/bart-large` for text2text-generation, avoiding API rate limits.
- **Chroma**: Lightweight vector DB for project document search.
- **Modular Functions**: Ensures reproducibility and extensibility.

## Limitations
- Requires significant memory for local LLM inference.
- Basic PDF parsing; tables/images unsupported.
- Dummy data used; real project docs may vary.
- No UI; file-based I/O.

## Extensibility
- Add email integration (`smtplib`).
- Parse PDF tables/images.
- Connect to EDECS’ knowledge graph.
- Support multi-language RFIs.

**Word Count**: 218  
**Notes**: Built in ~10 hours for 24-hour deadline. Tested with dummy PDFs.
