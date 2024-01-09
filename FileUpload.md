## This is how we can create a fileupload component in a next js ts project:

-first we install the react-dropzone:
  ``` npm install react-dropzone ```
- This is the code then to build the component:

```
"use client";

import React from "react";
import { useDropzone } from "react-dropzone";
import { Inbox } from "lucide-react";
const FileUpload = () => {
  const { getRootProps, getInputProps } = useDropzone({
    accept: { "application/pdf": [".pdf"] },
    maxFiles: 1,
    onDrop: (acceptedFiles) => {
      console.log(acceptedFiles);
    },
  });
  return (
    <div className="p-2 bg-white rounded-xl">
      <div
        {...getRootProps({
          className:
            "border-dashed border-2 rounded-xl cursor-pointer bg-gray-50 py-8 flex justify-center items-center flex-col",
        })}
      >
        <input {...getInputProps()} />
        <>
          <Inbox className="w-10 h-10 text-blue-500"></Inbox>
          <p className="mt-2 text-sm text-slate-400">Fazer upload de Arquivo</p>
        </>
      </div>
    </div>
  );
};

export default FileUpload;

```
  
## After I have setup my AWS s3 bucket and the s3.ts file that will be responsable to interact with it. I can now pass in the uploadfile function inside this s3 file to upload the files managed by this component to the s3 bucket on the amazon cloud:

```
onDrop: async (acceptedFiles) => {
      const file = acceptedFiles[0];
      if (file.size > 10 * 1024 * 1024) {
        alert("please upload a smaller file");
        return;
      }
      try {
        const data = await uploadToS3(file);
        console.log("data", data);
      } catch (error) {
        console.log(error);
      }
},

```
