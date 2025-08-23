# PDF-QnA with Amazon Bedrock \& Streamlit

This project is a PDF Question-Answering (QA) system leveraging **Amazon Bedrock** embeddings and large language models. Using **Streamlit** for interactive UI, it processes PDF documents, indexes them with vector embeddings (Titan), and allows users to ask questions that are answered using LLMs (Llama2, Jurassic2) via Bedrock.

## Features

- Loads and processes PDF documents from a local directory.
- Splits PDFs into text chunks for efficient embedding.
- Uses Amazon Titan for text embeddings via Bedrock.
- Stores vector embeddings locally with FAISS.
- Retrieves and answers questions against the ingested documents using Bedrock LLMs (Llama2, Jurassic2).
- Interactive querying and results via Streamlit web interface.


## Directory Structure

```
.
├── data/                 # Place your PDF files here
├── faiss_index/          # Vectorstore location (auto-created)
├── app.py                # Main Streamlit app (rename pdf-_chat.py if necessary)
├── requirements.txt      # Python dependencies
└── README.md
```


## Dependencies

- Python 3.8+
- boto3 (for AWS Bedrock/FAISS)
- awscli (for configuring AWS credentials)
- streamlit
- langchain
- numpy

Install with:

```bash
pip install -r requirements.txt
```

Additionally, you may need to install extra dependencies for LangChain and Streamlit support:

```bash
pip install langchain streamlit numpy faiss-cpu
```


## Setup

1. **AWS Setup**

Make sure your environment is configured to access Amazon Bedrock via boto3. You may need to set AWS credentials:

```bash
aws configure
```

Ensure your AWS user has permission to use Bedrock and associated models.
2. **Prepare Data**

Place your PDF files inside the `data/` folder.
3. **Run the Application**

Rename `pdf-_chat.py` to `app.py` if needed.

```bash
streamlit run app.py
```


## How It Works

1. **Data Ingestion**: PDF files are loaded and chunked into manageable text fragments.
2. **Embedding \& Vector Store**: Each chunk is converted to a vector embedding using Amazon Titan, then stored in a FAISS vector index.
3. **Question Answering**: User questions are matched to relevant document chunks via vector similarity, and the gathered context is sent to Bedrock LLMs for detailed answers.
4. **Prompt Template**: The system asks the LLM to provide detailed, summarized answers (~250 words) or admit when the answer is unknown.

## Customization

- **PDF Directory**: Change the path in `data_ingestion()` if your PDFs are elsewhere.
- **LLMs**: You may switch LLM backends (Llama2, Jurassic2) by modifying `get_llama2_llm()` or `get_claude_llm()`.
- **Chunk Size**: Tune `chunk_size` and `chunk_overlap` in the text splitter for optimal results.


## Notes

- Make sure you have access to Amazon Bedrock models used (`amazon.titan-embed-text-v1`, `meta.llama2-70b-chat-v1`, `ai21.j2-mid-v1`).
- For large PDF sets, initial indexing could take some time.


## License

This project is licensed under the MIT License.

***

Feel free to edit and expand as needed for your particular workflow or organization!

<div style="text-align: center">⁂</div>

[^1]: pdf-_chat.py

[^2]: requirements.txt

