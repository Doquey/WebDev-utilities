# This is basically a tecnique that we use to give context to AI models. 

## Its defined by storing the embedding vectors of our context content and then using a similarity search with the query(user question) to see what context we should give to the model for that question.

## In summary what I can do is:

- Get some pdf or book as context
- Break it down as multiple sub-documents
- Feed these paragraphs/sub-documents to openai embedder
- Save the embeddings into pineconedb(a database host specialized in storing vectors)
- Then do a similarity search with any question the use may pass in and retrieve the most embedding with the most similar semantic.
- Use this embedding as context for the prompt to the LLM.
