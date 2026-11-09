# AI Invoice Data Extractor & Chatbot

An AI-powered invoice processing application built using **Python, Streamlit, LangChain, and Azure OpenAI**. The application extracts structured information from multiple PDF invoices, stores the extracted records in a consolidated CSV file, and provides an AI-powered chatbot to answer natural-language questions about invoice data.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Key Features](#key-features)
- [Application Workflow](#application-workflow)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Extracted Invoice Information](#extracted-invoice-information)
- [Installation and Setup](#installation-and-setup)
- [Azure OpenAI Configuration](#azure-openai-configuration)
- [Run the Application](#run-the-application)
- [Application Modules](#application-modules)
- [Evaluation Metrics](#evaluation-metrics)
- [Sample Invoice Dataset](#sample-invoice-dataset)
- [Data Storage](#data-storage)
- [Limitations](#limitations)
- [Future Improvements](#future-improvements)
- [Author](#author)

---

## Project Overview

Manually extracting information from invoices can be repetitive and time-consuming, especially when dealing with multiple PDF documents.

This project automates the invoice extraction process using **Large Language Models (LLMs)** and **Agentic AI**.

The application uses Azure OpenAI and LangChain to read PDF invoices, extract relevant information, and convert unstructured invoice text into structured JSON data.

The extracted information is stored in a universal invoice table, allowing users to manage and query invoice records efficiently.

The application also includes an AI-powered conversational chatbot that uses vector-based retrieval to answer questions about previously processed invoices.

The project consists of three main modules:

1. **AI Invoice Extractor:** Extracts structured information from multiple PDF invoices.
2. **Invoice Chatbot:** Answers natural-language questions about stored invoice records.
3. **Evaluation Metrics:** Evaluates extraction performance through field-level comparison and classification metrics.

---

## Key Features

- **Multiple PDF Upload:** Upload and process multiple invoice PDF files simultaneously.
- **Automated PDF Reading:** Extract textual content from PDF invoices using PyPDFLoader.
- **LLM-Based Information Extraction:** Utilize Azure OpenAI to extract structured information from unstructured invoice documents.
- **Structured JSON Generation:** Convert invoice information into a predefined JSON format.
- **Duplicate Invoice Detection:** Prevent duplicate records using Invoice ID validation.
- **Universal Invoice Table:** Consolidate extracted invoice information into a single Pandas DataFrame.
- **CSV Export:** Download all extracted invoice records in CSV format.
- **Individual JSON Export:** Download structured JSON output for individual invoices.
- **AI-Powered Invoice Chatbot:** Ask questions about stored invoice information using natural language.
- **Vector-Based Retrieval:** Utilize Azure OpenAI embeddings and ChromaDB for semantic retrieval.
- **LangChain Agent:** Implement a tool-calling agent capable of selecting appropriate tools for invoice-related tasks.
- **Evaluation Dashboard:** Compare extracted invoice information and calculate Accuracy, Precision, Recall, and F1-score.

---

## Application Workflow

The overall workflow of the application is illustrated below:

```text
                  PDF Invoice Upload
                          |
                          v
                 Multiple PDF Processing
                          |
                          v
                  PDF Text Extraction
                    (PyPDFLoader)
                          |
                          v
                   Extract Invoice Text
                          |
                          v
                  Azure OpenAI LLM
                          |
                          v
                Structured JSON Extraction
                          |
                          v
                   JSON Parsing
                          |
                          v
                Duplicate Invoice Check
                          |
                  +-------+-------+
                  |               |
              Duplicate        New Invoice
                  |               |
                  v               v
                 Skip       Pandas DataFrame
                                  |
                                  v
                         Universal Invoice Table
                                  |
                                  v
                            CSV Storage
                                  |
                  +---------------+---------------+
                  |               |               |
                  v               v               v
             JSON Export     CSV Export      Invoice Chatbot
                                                  |
                                                  v
                                          Text Chunking
                                                  |
                                                  v
                                         Azure Embeddings
                                                  |
                                                  v
                                             ChromaDB
                                                  |
                                                  v
                                           Semantic Search
                                                  |
                                                  v
                                           RetrievalQA
                                                  |
                                                  v
                                          AI-Generated Answer
```

---

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Streamlit | Interactive web application interface |
| Azure OpenAI | LLM-based invoice extraction and question answering |
| LangChain | Agent development, tool integration, and retrieval pipelines |
| Azure OpenAI Embeddings | Generate vector embeddings |
| PyPDFLoader | Extract text from PDF documents |
| ChromaDB | Vector database for semantic retrieval |
| Pandas | Data manipulation and invoice table management |
| Scikit-learn | Evaluation metrics |
| RecursiveCharacterTextSplitter | Text chunking |
| Python-dotenv | Environment variable management |
| JSON | Structured invoice data representation |

---

## Project Structure

```text
InvoiceDataExtractor/
│
├── InvoiceDataExtractorAgent.py
│
├── requirment.txt
│
├── .env
│
├── .gitignore
│
├── invoice_table.csv
│
├── invoice_chroma_index/
│
├── sample_invoices/
│   ├── invoice_1.pdf
│   ├── invoice_2.pdf
│   └── ...
│
└── README.md
```

**File Descriptions:**

- `InvoiceDataExtractorAgent.py`: Main Python application containing the Streamlit interface, LangChain tools, agent configuration, extraction logic, chatbot, and evaluation module.
- `requirment.txt`: Contains the Python dependencies required to execute the application.
- `.env`: Stores Azure OpenAI configuration and API credentials.
- `invoice_table.csv`: Stores consolidated invoice records generated during application execution.
- `invoice_chroma_index/`: Directory used for Chroma vector-store persistence.
- `sample_invoices/`: Optional directory for storing sample PDF invoices.
- `README.md`: Project documentation.

---

## Extracted Invoice Information

The application extracts the following information from each invoice.

### 1. Invoice-Level Information

| Field | Description |
|---|---|
| Customer Name | Name of the customer |
| Ship To | Shipping destination |
| Vendor | Invoice-issuing organization |
| Invoice_ID | Unique invoice number |
| Date | Invoice date in YYYY-MM-DD format |
| Ship Mode | Shipping method |
| Balance Due | Outstanding invoice balance |
| Amount | Invoice amount |
| Discount | Discount applied to the invoice |
| Shipping | Shipping charges |
| Currency | Currency used in the invoice |
| Items | List of purchased products |
| Order ID | Unique order reference |

### 2. Item-Level Information

For every purchased item, the application extracts:

- Item Name
- Description
- Category
- Item Code
- Quantity
- Unit_Price
- Total

The extracted information is returned in JSON format to maintain a structured representation of the invoice data.

---

## Installation and Setup

### Step 1: Clone the Repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
```

Navigate to the project directory:

```bash
cd InvoiceDataExtractor
```

### Step 2: Create a Virtual Environment

```bash
python -m venv venv
```

Activate the virtual environment.

**Windows:**

```bash
venv\Scripts\activate
```

**Linux / macOS:**

```bash
source venv/bin/activate
```

### Step 3: Install Dependencies

If the dependency file is named `requirment.txt`:

```bash
pip install -r requirment.txt
```

Alternatively, rename it to `requirements.txt` and execute:

```bash
pip install -r requirements.txt
```

---

## Azure OpenAI Configuration

This project requires an Azure OpenAI resource with:

1. A deployed chat model.
2. A deployed embedding model.

Create a `.env` file in the project root directory.

Add the following environment variables:

```env
AZURE_OPENAI_ENDPOINT=your_azure_openai_endpoint

AZURE_OPENAI_DEPLOYMENT_NAME=your_chat_deployment_name

AZURE_OPENAI_API_KEY=your_azure_openai_api_key

AZURE_OPENAI_API_VERSION=your_azure_openai_api_version

AZURE_OPENAI_MODEL_NAME=your_chat_model_name

AZURE_OPENAI_EMBEDDING_MODEL_NAME=your_embedding_model_name

AZURE_OPENAI_EMBEDDING_MODEL_DEPLOYMENT=your_embedding_deployment_name
```

Replace the placeholder values with your actual Azure OpenAI configuration.

The application uses:

**AzureChatOpenAI**

For:
- Invoice information extraction.
- Natural-language question answering.
- AI agent operations.

**AzureOpenAIEmbeddings**

For:
- Generating embeddings.
- Semantic search.
- Vector-based invoice retrieval.

**Important:** Never upload your `.env` file or expose your Azure OpenAI API key on GitHub.

Add the following to `.gitignore`:

```gitignore
.env
venv/
__pycache__/
*.pyc
invoice_table.csv
invoice_chroma_index/
```

---

## Run the Application

After installing the dependencies and configuring Azure OpenAI, execute:

```bash
streamlit run InvoiceDataExtractorAgent.py
```

The application will start locally.

Open the following URL in your browser:

```text
http://localhost:8501
```

---

## Application Modules

The Streamlit application contains three main tabs.

### 1. AI Invoice Extractor

This module allows users to upload and process multiple PDF invoices.

**Working Process:**

1. Upload one or more invoice PDF files.
2. Click the Process Invoices button.
3. Extract text from uploaded PDFs using PyPDFLoader.
4. Send the extracted text to Azure OpenAI.
5. Generate structured JSON containing invoice information.
6. Parse the JSON response.
7. Check whether the Invoice ID already exists in the universal invoice table.
8. Add new invoice records to the Pandas DataFrame.
9. Save the consolidated records into `invoice_table.csv`.

**Available Functionalities:**

- Multiple invoice uploads.
- Automated information extraction.
- Structured JSON output.
- Duplicate invoice detection.
- Universal invoice table visualization.
- Individual invoice JSON download.
- Complete invoice CSV download.
- Reset universal invoice table.

### 2. Invoice Chatbot

This module provides a conversational interface for interacting with previously extracted invoice records.

The chatbot is implemented using LangChain and a tool-calling agent.

**Working Process:**

1. Load the existing invoice records from `invoice_table.csv`.
2. Convert invoice records into textual representations.
3. Split the text using RecursiveCharacterTextSplitter.
4. Generate vector embeddings using Azure OpenAI Embeddings.
5. Store and retrieve embedded text using ChromaDB.
6. Retrieve relevant information based on the user's query.
7. Generate an answer using Azure OpenAI.

**Example Questions:**

```text
1. What is the total balance due for all available invoices?

2. Which customer has the highest invoice amount?

3. List all invoices shipped using Standard Class.

4. Which products belong to the Technology category?

5. What is the shipping charge for invoice 25881?

6. Find all invoices associated with Tracy Blumstein.

7. Which invoice has the highest balance due?

8. What are the details of invoice 20584?
```

The chatbot uses semantic retrieval to identify relevant invoice information and generate conversational responses.

### 3. Evaluation Metrics

This module evaluates the extraction results by comparing the extracted invoice information against the corresponding record in the universal invoice table.

**Working Process:**

1. Upload a PDF invoice for evaluation.
2. Extract invoice information using Azure OpenAI.
3. Retrieve the corresponding record using Invoice ID.
4. Compare the extracted fields with the stored invoice information.
5. Identify matching and non-matching fields.
6. Calculate evaluation metrics.

The application displays a field-by-field comparison containing:

- Field Name
- Ground Truth
- Predicted Value
- Match Result

It also calculates:

- Accuracy
- Precision
- Recall
- F1-score

---

## Evaluation Metrics

The project uses Scikit-learn to calculate the following evaluation metrics.

### Accuracy

Measures the proportion of correctly matched fields among all compared fields.

\[
Accuracy = \frac{Correct\ Matches}{Total\ Fields}
\]

### Precision

Measures the proportion of predicted matches that are correct.

\[
Precision = \frac{TP}{TP+FP}
\]

### Recall

Measures the proportion of actual matches correctly identified.

\[
Recall = \frac{TP}{TP+FN}
\]

### F1-score

Represents the harmonic mean of Precision and Recall.

\[
F1 = 2 \times \frac{Precision \times Recall}{Precision+Recall}
\]

**Evaluation Approach:**

In the current implementation:

- Every compared field is assigned a ground-truth label of 1.
- A matching field receives a predicted label of 1.
- A non-matching field receives a predicted label of 0.
- Numeric values are compared after removing commas and dollar signs.
- Other values are compared using stripped string equality.

These metrics represent field-level exact-match performance rather than conventional document-level extraction accuracy.

---

## Sample Invoice Dataset

The project includes eight sample SuperStore invoices.

| Invoice ID | Customer Name | Invoice Date | Ship Mode | Balance Due |
|---|---|---|---|---:|
| 25881 | Tony Molinari | 2012-11-17 | First Class | $4,368.45 |
| 20584 | Tracy Blumstein | 2012-10-25 | Standard Class | $1,551.57 |
| 28215 | Tracy Blumstein | 2012-06-23 | Second Class | $3,365.06 |
| 21272 | Tracy Hopkins | 2012-07-19 | First Class | $580.92 |
| 13856 | Tracy Poddar | 2012-06-13 | Standard Class | $2,631.48 |
| 18864 | Troy Blackwell | 2012-11-21 | Standard Class | $1,356.49 |
| 25750 | Troy Staebel | 2012-12-07 | Standard Class | $4,229.80 |
| 30584 | Troy Staebel | 2012-01-31 | Standard Class | $10,413.48 |

These sample documents contain customer information, invoice numbers, shipping details, product information, quantities, discounts, shipping charges, and order IDs.

The sample invoices are provided to demonstrate the application's document extraction capabilities.

---

## Data Storage

The application uses local file-based storage.

### 1. Universal Invoice Table

**File:** `invoice_table.csv`

Stores all successfully extracted invoice records.

Each row represents an invoice, and the Items field is stored as a JSON string.

### 2. Chroma Vector Database

**Directory:** `invoice_chroma_index/`

Used as the persistence directory for the Chroma vector store.

It supports semantic retrieval of invoice information for the chatbot.

---

## Limitations

The current implementation has the following limitations:

1. **Scanned PDF Support:** The application uses PyPDFLoader for text extraction. OCR functionality for scanned or image-only invoices is not implemented.

2. **JSON Validation:** The application uses Python's `json.loads()` to parse the LLM response. Invalid JSON responses may cause extraction failures.

3. **Local Data Storage:** Invoice records are stored in a local CSV file rather than a centralized database.

4. **Vector Index Management:** The Chroma vector store is created from the invoice records during querying. Incremental indexing is not implemented.

5. **Evaluation Methodology:** The evaluation module uses field-level exact matching and does not use a separately maintained, manually verified ground-truth dataset.

6. **Agent PDF Input:** The PDF-reading tool accepts PDF bytes, while the agent tool interface is text-based. Agent-driven PDF reading may require an additional file-input mechanism.

7. **Data Security:** Additional authentication and access-control mechanisms are required before deploying the application for handling sensitive business invoices.

---

## Future Improvements

Potential enhancements include:

- Implement OCR support for scanned PDF invoices.
- Introduce structured JSON output validation.
- Improve error handling and API retry mechanisms.
- Implement incremental vector database indexing.
- Integrate a centralized database for invoice storage.
- Add invoice-level and item-level evaluation.
- Introduce more robust duplicate detection.
- Add interactive visualizations for invoice analytics.
- Implement authentication and authorization.
- Deploy the application using Streamlit Community Cloud or another hosting platform.
- Improve invoice chatbot retrieval accuracy using metadata filtering and optimized retrieval strategies.

---

## Author

**Satyabrata Nayak**

Interested in Artificial Intelligence, Generative AI, Agentic AI, Machine Learning, and Python-based applications.

---

If you find this project useful, feel free to ⭐ the repository!
