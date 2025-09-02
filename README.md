PDF Question-Answering with RAG
This is a from-scratch implementation of a Retrieval-Augmented Generation (RAG) pipeline in a Python notebook. It is designed to answer questions about a specific PDF document by finding the most relevant text and using a large language model to generate a precise answer.

Pipeline Overview
This project follows a five-step process to intelligently answer questions.

Extract: The pipeline begins by loading the source PDF. Using the PyMuPDF library, it systematically extracts all raw text from every page of the document.

Chunk: The extracted text is then cleaned to remove formatting issues. It's broken down into smaller, overlapping chunks using a sliding window approach. This ensures that the semantic context is preserved across chunk boundaries.

Embed: Each text chunk is converted into a high-dimensional vector, known as an embedding, using the all-MiniLM-L6-v2 sentence transformer model. These embeddings numerically represent the meaning and context of the text.

Retrieve: To find relevant information, the user's question is also converted into an embedding. The system then uses Cosine Similarity to compare the question's vector against all chunk vectors, retrieving the top 5 chunks that are most semantically similar.

Generate: The retrieved chunks are compiled into a context block and fed into the gpt-4o-mini model through a carefully engineered prompt. This prompt instructs the model to formulate its answer based only on the provided text, ensuring the response is accurate and grounded in the source document.

Requirements
The following libraries are required to run the code. You can install them via pip:

pip install PyMuPDF sentence-transformers transformers scikit-learn openai

How to Run This Code (in Google Colab)
Upload Files:

In the Colab file explorer, upload this notebook (.ipynb) and the source PDF (Human-Nutrition-2020.pdf).

Set Up API Key:

For security, add your OpenAI key to Colab's Secrets manager (the 🔑 icon).

Name: OPENAI_API_KEY

Value: Your sk-... key.

Ensure "Notebook access" is enabled.

Run the Notebook:

Execute the first cell to install the required libraries.

Run the remaining cells in order. The script will process the PDF, create the embeddings, and then prompt you to enter your question.
