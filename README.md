# 🧠 LangChain + Astra DB: Interactive Q&A with Vector Search

This project demonstrates an interactive command-line chatbot that leverages LangChain's integration with DataStax Astra DB for vector-based semantic search. Users can input natural language questions, and the system retrieves relevant information from a vector store to provide accurate answers.

---

## 📌 Features

- **Interactive Q&A Loop**: Continuously prompts the user for questions until 'quit' is entered.
- **Semantic Search**: Utilizes Astra DB's vector capabilities to find contextually relevant documents.
- **Similarity Scoring**: Displays the top matching documents along with their similarity scores.

---

## 🛠️ Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/ssarthak0/LangChain-Astra-DB-Interactive-Q-A-with-Vector-Search
cd LangChain-Astra-DB-Interactive-Q-A-with-Vector-Search
```

### 2. Create and Activate a Virtual Environment

```bash
python -m venv env
source env/bin/activate  # On Windows: env\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Set Environment Variables

Create a `.env` file in the root directory and add your Astra DB credentials:

```env
ASTRA_DB_API_ENDPOINT=your_astra_db_api_endpoint
ASTRA_DB_APPLICATION_TOKEN=your_astra_db_application_token
```

---

## 🧪 Usage

Run the chatbot script:

```bash
python chatbot.py
```

You'll be prompted to enter your question:

```
Enter your question (or type 'quit' to exit):
```

Type your question and press Enter. The system will display the answer and the top matching documents with their similarity scores.

---

## 📄 Code Overview

Here's a snippet of the main interactive loop:

```python
first_question = True
while True:
    if first_question:
        query_text = input("\nEnter your question (or type 'quit' to exit): ").strip()
    else:
        query_text = input("\nWhat's your next question (or type 'quit' to exit): ").strip()

    if query_text.lower() == "quit":
        break

    if query_text == "":
        continue

    first_question = False

    print("\nQUESTION: \"%s\"" % query_text)
    answer = astra_vector_index.query(query_text, llm=llm).strip()
    print("ANSWER: \"%s\"\n" % answer)

    print("FIRST DOCUMENTS BY RELEVANCE:")
    for doc, score in astra_vector_store.similarity_search_with_score(query_text, k=4):
        print("    [%0.4f] \"%s ...\"" % (score, doc.page_content[:84]))
```

---

---

## 🔗 Resources

- [LangChain Documentation](https://python.langchain.com/)
- [DataStax Astra DB Documentation](https://docs.datastax.com/en/astra-db/)
- [LangChain Astra DB Integration Guide](https://python.langchain.com/docs/integrations/vectorstores/astradb/)

---

## 📄 License

This project is licensed under the MIT License.

---

## 🙏 Acknowledgements

- [LangChain](https://www.langchain.com/)
- [DataStax Astra DB](https://www.datastax.com/astra)
