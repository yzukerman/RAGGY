# RAG Example
## Overview
**Retrieval-Augmented Generation (RAG)** is now the mainstream Generative AI technique. It allows you to use your private content with a public LLM to answer questions about your documents. The idea is to send 'context', or a snippet of your overall document collection, to the LLM - helping it answer your query.
This works in the following fashion:
1. Prep
   1. Collect the documents you want to search through for answers.
   2. Break the documents apart into chunks. You need to do that to ensure you do not exceed the LLM's input capacity.
   3. Create vector embeddings - a numeric representation of the text - for each chunk. You create these vector using dedicated models known as 'embedding models'. These models convert text into number vectors.
   4. Load these vector embeddings into a vector database.
2. Search the vector database for the information you want. (Vector databases are used because they are really great for searching)
3. The vector database will either return you the text chunks that are relevant to your question or point at the documents you will want to use. 
   1. This will be the text/documents you send to the LLM with your question to help it compose an answer for you.
4. Send a prompt containing the question and the context (search results) to the LLM.
5. The LLM will return an answer that is relevant to your question.

## Sources
This tutorial is based on a conglomeration of content from the following sources
* ChatGPT (Chapters 1 and 2)
* [Weaviate's documentation](https://weaviate.io/developers/academy/py/starter_text_data/text_rag)
* Pixegami's [YouTube tutorial](https://www.youtube.com/watch?v=2TJxpyO3ei4&t=202s)
* [Ollama's blog post about local embedding](https://ollama.com/blog/embedding-models)

## Making that happen: what do you need?
This tutorial ran using Python 3.12.7.

* A collection of documents - PDFs are good
* Install
  * FAISS - an in-memory vector database from Meta (use faiss-cpu or faiss-gpu based on your hardware)
  * Docker
  * Weaviate (depends on Docker)
  * Ollama (for running a local embedding model)
  * Jupyter Lab (for running my Python examples)
* An OpenAI API (not ChatGPT) account with a funding source. I spent $2 in total on this demo.
   * Set up an environment variable for your OpenAI API key under the name ```OPENAI_API_KEY```

I created the demo on Fedora Linux and installing all of these was very simple. What the world is coming to?

## Getting up and running
1. Use pip to install
   1. jupyter or jupyter-ai
   2. FAISS
   3. weaviate-client
   4. ollama
   5. mercury
   6. transformers
   7. tqdm
   8. openai
   9. langchain
   10. beautifulsoup4
3. Install Docker (on Linux, this is as complex as ```sudo dnf install docker``` [for other OSes](https://docs.docker.com/desktop/)
   1. Our setup requires you to use a minimally customized Weaviate Docker container. For that reason you need to be sure Docker Compose is installed.
   2. Installing this on Fedora with ```dnf``` was not working but [installing Compose as a plugin](https://docs.docker.com/compose/install/standalone/) did.
4. With Docker ready, you will need to use the ```docker-compose.yml``` file I have in the project, which enables the use of OpenAI seamlessly with Weaviate.
   1. This can save you time and get you up and running muuuuuuch faster.
   2. You can use another LLM provider but your milage will vary.
5. From the command line, run ```jupyter lab```.
6. For the sections that discuss local execution (chapters 4 and 5):
   1. [Install Ollama](https://ollama.com/download).
   2. Download and install the [Nomic embedding model](https://ollama.com/library/nomic-embed-text) using the Ollama command-line tool.

Follow the tutorial from rag1 onward! I hope you enjoy!

