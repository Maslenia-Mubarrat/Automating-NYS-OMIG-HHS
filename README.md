# Automating NYS OMIG + HHS Exclusion Searches

A Google Colab automation project for searching exclusion databases, processing employee names from a CSV, generating PDFs of results, and saving them to Google Drive.

This project was designed to automate a repetitive compliance workflow across multiple public exclusion websites and demonstrates practical Selenium automation, browser automation in Colab, file handling, PDF generation, and validation logic.

## Overview

The script reads employee names from a CSV file, searches for each person in exclusion databases, and saves the results as PDFs to Google Drive. It supports:

- NYS OMIG exclusion search automation
- HHS OIG exclusion search automation
- Batch processing of names
- PDF generation and saving
- Error handling and retry logic
- Missing-file detection and reprocessing

This project is a strong example of web automation for compliance, document generation, and operational workflow optimization.

## Why this project matters

Many public agencies maintain exclusion databases that are used to screen workers, contractors, and vendors. Manually searching through these websites is time-consuming and repetitive. This automation reduces manual effort and helps ensure that a large list of names can be checked systematically and stored consistently.

The repository is especially relevant for roles involving:

- Python automation
- Selenium browser automation
- Data processing and CSV handling
- PDF generation and document workflows
- Google Colab / cloud-based scripting
- Operational reliability and exception handling

## Project goals

- Read employee names from a CSV file
- Search exclusion websites programmatically
- Capture results as PDFs
- Save files to organized Google Drive folders
- Handle retries and failures gracefully
- Reprocess missing PDFs automatically
- Provide a working template for similar compliance automation tasks

## Features

### 1. CSV-driven name processing
The script loads a CSV with employee names and checks for the required columns:

- Employee First Name
- Employee Last Name

It creates a combined full name field and filters out blank entries.

### 2. Selenium browser automation
The project uses Selenium to interact with exclusion websites in Chrome. It includes:

- explicit waits for page elements
- dynamic waiting for search results
- click retries
- JavaScript click fallback when normal clicks fail
- browser startup in a headless/cloud environment

### 3. Batch processing for OMIG
For the NYS OMIG flow, the script fills up to five search boxes, submits the search, waits for results, clicks the export button, waits for the PDF download, and renames the file.

### 4. PDF generation for HHS OIG
For HHS OIG, the script uses the Chrome DevTools Protocol command `Page.printToPDF` to convert the current page to a PDF and save it locally before moving it into Google Drive.

### 5. Validation and reprocessing
The script checks whether expected PDFs were created and compares them against names in the input CSV. If some results are missing, it can re-run the search for those names automatically.

### 6. Error handling
The automation includes:

- exception logging
- screenshot capture on failure
- retries for click operations
- timeout checks for downloads
- graceful continuation if some rows fail

## Technical stack

- Python
- Pandas
- Selenium
- Google Colab
- Google Drive integration
- Chrome / ChromeDriver
- PDF generation via browser print-to-PDF

## Repository structure

```text
Automating-NYS-OMIG-HHS/
├── nys_omig_+_hhs.py
├── README.md
└── (Google Drive output folders created at runtime)
```

## Input data format

The CSV must contain the following columns:

```csv
Employee First Name,Employee Last Name
John,Doe
Jane,Smith
```

The script expects the exact column names shown above.

## Google Drive setup

The script assumes that the source CSV is stored in Google Drive, for example:

```text
/content/drive/MyDrive/Medicaid Exclusions(Aug 26).csv
```

It creates output folders such as:

```text
/content/drive/MyDrive/Medicaid_Exclusion_Results
/content/drive/MyDrive/HHS OIG
```

## How to run

### In Google Colab

1. Open a new Colab notebook.
2. Upload or paste the contents of `nys_omig_+_hhs.py`.
3. Make sure your CSV is available in Google Drive.
4. Run the notebook cells in order.
5. Confirm the output PDFs are saved in the Drive folders.

### Important configuration

At the top of the script, you may need to adjust:

- `CSV_PATH`
- `OUTPUT_FOLDER`
- `NUMBER_OF_NAMES`
- `SEARCH_URL`

For testing, `NUMBER_OF_NAMES` can be set to a small number before processing the full dataset.

## Sample behavior

When the script runs, it will:

- read employee names,
- create a list of names to process,
- open the target exclusion website,
- search for each person,
- save PDFs of the results,
- validate created files,
- re-run missing searches if needed.

## Example output

The script produces files such as:

```text
medicaid_exclusion_result1.pdf
medicaid_exclusion_result2.pdf
John_Doe.pdf
Jane_Smith.pdf
```

## Challenges addressed

This project addresses common difficulties in browser automation, including:

- dynamic page loads
- inconsistent click behavior
- Chrome and browser-driver compatibility in Colab
- PDF download timing
- verifying that all expected files were generated

## Limitations

While the project is functional, there are some practical limitations:

- It is tightly customized for Google Colab.
- It relies on exact CSV column names.
- It assumes the websites continue to use their current HTML structure.
- It may need updates if the target sites change field IDs or page layouts.
- It is not yet packaged as a production-grade CLI or API service.

## Security and compliance considerations

Because the workflow involves employee names and possibly sensitive compliance screening data, it is important to:

- restrict Google Drive access appropriately
- avoid storing unnecessary copies of records
- confirm the automation complies with organizational policies and the website terms of service
- minimize exposure of personally identifiable information

## Future improvements

This project could be expanded in several directions:

- modularize the script into functions/classes
- add logging with Python's `logging` module
- create a config file for paths and browser settings
- add automatic OCR or PDF text extraction
- classify results into structured compliance records
- build a dashboard to summarize search outcomes
- create unit tests for data cleaning and filename generation
- deploy as a desktop or web app for non-Colab usage

## Why this is a good project for an AI/automation engineer profile

This repository demonstrates several skills that matter in automation and AI-focused engineering:

- data cleaning and preprocessing
- browser automation with Selenium
- handling unreliable UI interactions
- cloud-based execution in Colab
- process automation for real-world workflows
- validation and quality checks
- building resilient automation pipelines

It shows the ability to design systems that interact with real-world websites, manage operational failures, and automate repetitive business tasks.

## Conclusion

This project is a practical example of applied Python automation. It solves a real operational problem by reducing the manual burden of screening employee names against exclusion databases and saving the results as structured, reviewable PDFs.

It is an excellent example of a hands-on engineering project that combines:

- scripting
- browser automation
- file management
- reliability engineering
- cloud execution
- workflow optimization

## License

This project is currently provided as-is for educational and portfolio purposes. If you plan to share it publicly, consider adding an open-source license such as MIT.

---

If you want, I can also generate:

1. a more polished GitHub-ready version with a professional tone,
2. a concise version for a portfolio or LinkedIn project page,
3. a version with a more technical engineering focus,
4. or a version tailored specifically for an AI/ML engineering hiring profile.

I can also tweak the README to sound more like a strong job application artifact and less like a general project description.
