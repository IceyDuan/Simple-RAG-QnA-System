# Simple-RAG-QnA-System
## Introduction
A simple Retrieval-Augmented Generation (RAG) system using Python, LangChain, and OpenAI's GPT-4/DeepSeek. We created Q&amp;A tool for recommending meal combinations based on nutritional requirements and cuisine preferences. Users can use our RAG to generate recipes corresponding to their specific requirements and fulfill their needs.
## Dataset
We use the dataset All_Diets.csv containing recipes and their nutritional information including protein, carbs, and fats. In this way we can use the data in this table to inform the LLM model, meaning to be able to answer the user's questions more accurately.

![image](https://github.com/user-attachments/assets/fd0c1ee9-5e47-4b79-bf4d-a79d5b93879b)
## Embedding
We deployed Ollama locally in this program and used LLaMA3 for embedding and storing inside the FAISS vector database. We transformed the dataset into a high-dimensional vector and implemented a semantic mapping. When a user asks a question, the question is embedded into a vector, and then a similarity computation (we use cosine similarity) is used to match relevant fragments.
## QnA System
We chose FAISSRetriever to perform a search in the knowledge base. Then we built RetrievalQA chain to combine Retriever with LLM (you can use your own API to call ChatGPT or Deepseek). In this step, our system gets the relevant documents from Retriever, then adds the documents and user questions to Prompt and passes them to LLM for it to answer based on those documents.

We then define the QA Tool as the tool responsible for the Q&A task. You can think of it as a Q&amp;A button with a name and description, and the Agent decides when to click it". With this tool, the system receives the user's query, calls qa_chain to get the answer, and uses the answer as the return value of this Tool for the Agent to refer to or use.

Finally, we have our Agent, which is the brain of LangChain. Through it, the system can understand the user's question, determine whether it is necessary to use and which Tool to call, and integrate the results to finally generate the answer Compared with the simplest RAG system, Agent is more free than simple input and output. It can make multi-step decisions, such as looking up data before summarizing, or even calling multiple Tools.
