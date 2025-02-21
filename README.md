# SAJE Scraper

## Overview

This project is designed to scrape the *South African Journal of Economics* (SAJE) website to collect DOIs for all articles, download the corresponding PDFs, extract metadata, and perform text mining. The end goal is to set up a structured pipeline to automate this process efficiently.

## Project Structure

The project consists of four main scripts, each handling a specific step in the workflow:

1. **`01-get-DOIs.py`** - Scrapes the SAJE website to collect the DOIs for each article.
2. **`02-get-PDFs.py`** - Downloads the PDFs for each article using the DOI.
3. **`03-get-metadata.py`** - Extracts and stores metadata associated with each article.
4. **`04-textmine.py`** - Performs text mining on the downloaded PDFs to extract meaningful insights.

Once these scripts are functional, they will be refactored into a more structured pipeline using:

* A **Makefile** to automate the workflow.
* A **utils module** to store shared functions.
* A **main script** to orchestrate the entire process.

---

## Setup

To run this scraper, follow these steps:

### **1. Create a virtual environment**

It is recommended to run the scripts in a virtual environment to manage dependencies cleanly. Run the following commands in your terminal:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

If you prefer using `uv` as the package manager, install it with:

```bash
pip install uv
```

### **2. Install dependencies**

Once the virtual environment is activated, install the necessary packages:

```bash
uv pip install selenium requests undetected_chromedriver
```

---

## How the Scraper Works

### **Step 1: Collecting DOIs**

* The script navigates the SAJE landing page and collects all issue links.
* For each issue, it extracts article links and retrieves the DOI from each article page.
* The DOIs are stored in a structured format for further use.
* **Important:** DOIs follow the format `10.1111/j.1813-6982.1933.tb02985.x` and will be used to construct download URLs.

### **Step 2: Downloading PDFs**

* Once the DOIs are collected, the PDFs can be downloaded using:
  ```
  https://onlinelibrary.wiley.com/doi/pdfdirect/{doi}?download=true
  ```
* The PDFs will be stored in an organized directory structure.

### **Step 3: Extracting Metadata**

* Metadata such as title, authors, publication year, and abstract will be collected from the SAJE website and stored in a structured format (e.g., JSON or CSV).

### **Step 4: Text Mining**

* The downloaded PDFs will be processed to extract text for analysis.
* NLP techniques can be applied to extract key terms, perform sentiment analysis, or summarize articles.

---

## Notes

* **Avoiding Bot Detection** : The scraper uses `undetected_chromedriver` to bypass Cloudflare protection that requires CAPTCHA verification.
* **Headless Mode** : The script is currently set to **visible mode** for debugging. To run in headless mode, uncomment the `--headless` flag in the Chrome options.
* **Browser Requirement** : Google Chrome must be installed on your system to run Selenium. See the [ChromeDriver documentation](https://developer.chrome.com/docs/chromedriver/get-started) for setup instructions.

---

## Next Steps

* Complete the DOI collection script (`01-get-DOIs.py`).
* Do the PDF downloader (`02-get-PDFs.py`).
* Dothe metadata extraction script (`03-get-metadata.py`).
* Set up the text mining workflow (`04-textmine.py`).
* Refactor the scripts into a modular Python package with a Makefile.
