# RAG PDF Chatbot

Ask questions of a PDF and get answers grounded in its text rather than in the
model's memory. A single-file Streamlit app: upload a document, it is chunked and
embedded, and each question is answered from the chunks that actually match it.

## How it works

```
PDF  ->  extract text (PyPDF2)
     ->  chunk
     ->  embed
     ->  retrieve the chunks nearest the question
     ->  answer from those chunks only (OpenAI)
```

Retrieval-augmented generation exists to solve one problem: a language model
asked about a document it has not seen will produce a confident, fluent, wrong
answer. Grounding the answer in retrieved passages makes it checkable.

## Running it

```bash
pip install -r requirements.txt
export OPENAI_API_KEY="sk-..."     # or put it in .env
streamlit run RAG_PDF_chatbot.py
```

The key is read from the environment via `python-dotenv`. Nothing secret belongs
in source.

## Known limitations

- One PDF at a time, held in memory; no persistent vector store
- Naive fixed-size chunking, so a passage split across a boundary can be missed
- Scanned PDFs need OCR first — PyPDF2 only reads embedded text
- No citation of which chunk produced the answer, which is the first thing worth
  adding

## License

MIT
