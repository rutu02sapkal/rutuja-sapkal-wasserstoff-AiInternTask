**PDF Processing and Summarization Pipeline**

This project is a PDF ingestion, summarization, and keyword extraction pipeline. It processes multiple PDFs, extracts text, generates summaries and keywords, and stores document metadata, summaries, and keywords in MongoDB. The pipeline supports concurrent processing of multiple PDFs for efficient document handling.

**Table of Contents**

1) Project Overview
2)System Requirements
3)Setup Instructions
4) Usage
5)Solution Explanation
6) Error Handling
7)License

## Project Overview

This project performs the following tasks:
1. Downloads PDFs from URLs stored in a JSON dataset.
2. Extracts text from each PDF using PyMuPDF.
3. Generates summaries and extracts keywords from the text.
4. Stores the PDF metadata, summary, and keywords in MongoDB.
5. Processes multiple PDFs concurrently to improve performance.

## System Requirements

- **Python 3.7+**
- **MongoDB** installed locally or in the cloud.
- Required Python libraries:
  - `pymongo`
  - `requests`
  - `PyMuPDF` (via `fitz`)
  - `nltk`

You can install the required libraries using:
pip install pymongo requests PyMuPDF nltk
Additionally, ensure NLTK resources are downloaded:
import nltk
nltk.download('punkt')
nltk.download('stopwords')
Setup Instructions
Clone the repository:
git clone https://github.com/yourusername/pdf-processing-mongodb.git
Install dependencies:
pip install -r requirements.txt
Set up MongoDB: Ensure that MongoDB is running locally or is accessible via a cloud service. Start MongoDB with:
mongod
Prepare the dataset: The Dataset.json file should be updated with the URLs of the PDFs you want to download and process.

Run the project: After MongoDB and Python dependencies are set up, run the main Python script:
python main.py
Usage
JSON Dataset: Place the Dataset.json file in the project directory or update the path to it in the script. The JSON should have this structure:

json
Copy code
{
   "pdf1": "https://example.com/sample1.pdf",
   "pdf2": "https://example.com/sample2.pdf"
}
Folder Path: Ensure the folder where downloaded PDFs are stored is correctly updated in the script. Update the folder_path variable in the main function.

Running the Pipeline: The script will:

Download PDFs from URLs in the Dataset.json file.
Extract text from the PDFs.
Generate summaries based on text frequencies and extract keywords.
Store metadata, summaries, and keywords in MongoDB.
Solution Explanation
1. PDF Ingestion:
The pipeline ingests PDFs from URLs specified in a JSON dataset. If a file already exists, it skips downloading that file.

2. Text Extraction:
Text from the PDFs is extracted using PyMuPDF (fitz). The extracted text is then used for summarization and keyword extraction.

3. Summarization:
A frequency-based summarization technique is used. Sentences are ranked based on the frequency of important words, and the top sentences are included in the summary.

4. Keyword Extraction:
Keywords are extracted based on word frequencies, excluding common stopwords, using NLTK.

5. MongoDB Integration:
Metadata about the PDFs (such as name, path, and file size), along with the summaries and extracted keywords, are stored in MongoDB.

6. Concurrency:
The project uses ThreadPoolExecutor to process multiple PDFs concurrently, improving the speed and efficiency of the pipeline.

Error Handling
File Not Found: If a PDF file or URL is invalid, the error is logged, and the script moves to the next file.
Empty PDFs: If no text is extracted from a PDF, the issue is logged, and the script continues processing.
Corrupted PDFs: Corrupted files are handled, and the error is logged without breaking the pipeline.
