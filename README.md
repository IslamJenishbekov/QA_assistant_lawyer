# Creating a QA assistant for consultation on the laws of the Kyrgyz Republic.
This project aimed to test the possibility of creating a chatbot based on RAG for providing consultations to citizens on the laws of the Kyrgyz Republic in the Russian language.

## Technologies and Libraries Used
- Python
- Embedding Model ("deepvk/USER-bge-m3")
- Numpy 
- Faiss
- Json
- CrossEncoder ("DiTy/cross-encoder-russian-msmarco")
- Groq, LLM ("llama3-70b-8192")

## Algorithm
- Data Preprocessing

a) Splitting each book into short chunks by extracting each clause into a separate chunk, saving it in `chunks.json` ([chunk1, chunk2...]), while also saving in `metadata.json` ({chunk_id: {"book": book, "article_num": article_num, "link": book_link}) the name of the code, the article number from which the clause is taken, and a link to the book. And after this we need do separate processing of chunks longer than 2000 characters.

b) Vectorizing each chunk

c) Creating an index with these vectors

d) Saving index.index, chunks.json, metadata.json


- Main
  
a) Downloading index.index, chunks.json, metadata.json

b) Receiving a question as input 

c) Vectorizing question

d) Selecting 200 vectors from index based on cosine similarity

e) Using CrossEncoder

f) Creating context from the 5 most likely answer chunks for question, adding information from the metadata

g) Creating system prompt and query wrapper

h) Passing system prompt and query wrapper with question + context to LLM and receiving answer


## Result 
We tested our chatbot using 50 questions prepared by professional lawyers. The model achieved an average answer correctness of 0.603 and an average answer similarity of 0.924. These results are promising and indicate that developing a chatbot for providing consultations to civilians is indeed feasible.
