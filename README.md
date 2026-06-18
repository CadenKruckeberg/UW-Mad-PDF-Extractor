# UW–Madison PDF Extractor

## Overview

This tool is used to extract data from UW–Madison's Department Instructional Reports (DIR) and Grade-Distribution Reports. It is built with Python and pdfplumber with a goal of maximum accuracy and data usability. Simply provide a valid PDF, and the tool will output a Tab-Separated Values (TSV) file of the contents.

## Why

I asked UW for the data in a better format than PDF but was denied, so I decided to look into extraction. This tool is similar to the popular [Madgrades' extractor](https://github.com/Madgrades/madgrades-extractor), and I initially solely wanted to help with that project. My main concern was with extractor accuracy because I had discovered a mistake the first time I used it. I realized that because there are so many reports, each with so many records, it would be unrealistic to manually check whether each record was correct or not; instead, I wanted a completely independent extractor to compare results with, and so I started working on this project. I figured that all discrepancies between the two extractors' results **could** be manually reviewed, and both extractors could be improved this way. Things worked out as planned, and I first used the discrepancies to improve a small bug in this tool. I was then able to identify 32,822 records that Madgrades incorrectly extracted (or didn't extract at all) and submit PRs to fix them. I was also able to identify another bug that I roughly estimate to cause >100 records to be incorrectly extracted by Madgrades (at the time of writing, this has yet to be resolved). Finally, I discovered a limitation of pdfplumber that makes my extractor so slightly incorrect that it could even be argued that it is for the better. In the end, these two extractors agree on (a conservative estimate of) 99.9% of the 1,272,761 records that currently exist in the report PDFs. Though these extractors are similar, they are not the same. Madgrades' extractor, built with Java and Tabula, is much faster. Actually, my extractor supports parallel processing and Madgrades' does not, so actual speed depends on your processor, but Madgrades' extractor is easily faster per PDF extracted. I hope that I or someone else will give Madgrades' extractor parallel processing soon, too. There is also the whole Madgrades "suite" of tooling to use with the relational output its extractor produces as a benefit. On the other hand, my extractor is technically (I would say insignificantly) more accurate, but more importantly, I think its output is more approachable and less opinionated. It directly transforms records in the PDF reports to rows of a TSV, where Madgrades transforms and fragments the data while introducing many UUIDs. I also hope I or someone else will add the ability to output raw extracted rows to Madgrades' extractor, though. If my tool ends up as nothing more than a means to the end of pushing Madgrades toward perfection, I will content still.

## How to Use

1. Ensure you have a Python interpreter

2. Clone this repo

3. Change directory into this repo

4. (Optional) Create a virtual environment `python3 -m venv venv` and source it (platform dependant)

5. Install requirements: `pip install -r requirements.txt`

6. Use the tool (`python3 src/uw_mad_pdf_extractor/main.py`) with the usage provided below

## Usage

```
usage: main.py [-h] [-p N] [-s] [-j N] [-o DIR] PATH [PATH ...]

Extract data from PDF files or directories of PDFs.

positional arguments:
  PATH                  One or more PDF files or directories containing PDFs.

options:
  -h, --help            show this help message and exit
  -p, --debug-page N    Generate debug images for the specified page number. Can be used multiple times (e.g. -p 1 -p 3).
  -s, --output-skipped  Write skipped rows to a separate TSV output file.
  -j, --jobs N          Number of PDFs to process in parallel.
  -o, --output-dir DIR  Directory to write output files (default: current directory).
```

## Getting the PDFs

I recommend using [Madgrades' archive](https://github.com/Madgrades/madgrades-data) to download the PDF reports.

## Known Issues

If you want to read about the known issues with the parser or PDFs, read [docs.md](./docs.md).

*This project is unaffiliated with UW–Madison*
