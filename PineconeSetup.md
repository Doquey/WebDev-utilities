# First we have to create a pinecone account for our project

## Pinecone terms

- Index = Database
- namespace = segment pdf vector embeddings(much like a table)

## Installing pinecone:

```
npm install @pinecone-database/pinecone
```


## Then we go to create index and follow these steps:

- Choose the dimensions for the vectors(it goes up to 1500) so we should try to choose the maximum number if we do not know how long our vectors are going to be.
- choose the similarity we want to use, availables are: cosine,dotproduct,euclidean
- Go to api key section, create a new api key copy it and the enviroment and place it on my .env file.

## Now we have pinecone index setup, we need to create the file that will contain the functions for pinecone in our application, to do that we do the following:


- Go to lib, create a file called pinecone.ts
- Write the code that will be bellow

  
