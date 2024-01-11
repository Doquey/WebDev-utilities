# Lagchain can be used for a lot of things that make our life easiear when dealing with LLM's. One of those things is converting pdfs to text streams. Lets take a look at how to do that bellow.
```
npm install langchain

npm install pdf-parser

npm install @pinecone-database/doc-splitter

```


```

import {PDFLoader} from "langchain/document_loaders/fs/pdf";
import {
  Document,
  RecursiveCharacterTextSplitter,
} from "@pinecone-database/doc-splitter";

type PDFPage ={
pageContent:string;
metadata:{
loc:{pageNumber:number}
}
}

export async function loadPDF(file_path:string){
const loader = new PDFLoader(file_path);
const pages = (await loader.load()) as PDFPage[];
}




```


