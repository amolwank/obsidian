RAG = Retrieval-Augmented Generation
Its a technique in AI that combines:
1. Retrieval ->Searching a knowledge base (like documents, databases or APIs) for relevant information.
2. Generation -> Using a language model (like GPT) to generate a natural language answer based on both the retrieved info + its own knowledge.

In Short: RAG helps AI give accurate, up-to-date answers by looking things up first, instead of only relying on what it was trained on.

##### Why Do We Need RAG?
- Normal AI models are trained on data up to a certain point (they can be outdated).
- They might "hallucinate" (make up answers ).
- With RAG, the model fetches the latest and most relevant data before responding.
###### How RAG Works (Simple flow):
1. User asks a questions.
2. AI agent retrieves relevant documents from  a knowledge base
3. AI reads + summarizes those documents
4. AI generates the final response.