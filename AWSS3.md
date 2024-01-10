# How to use AWS S3 to store files

- Login to aws and go to the console home
- search for s3 (simple storage service)
- Click upon it
- Create a new bucket
     ACLs desabilitadas
     uncheck block all public acess
     versionamento de bucket desabilitado
     
- choose sao paulo (as-east-1)
- Now we need to modify the permission for the objects, because so far all of them can be public:
- Click on the new bucket
- Go to permissions
- Edit the permission policy and place this json file in there:

Permission Policy
  ```

  {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::gempdf/*"
        }
    ]
}
  ```
- Ok now we go to the CORS Object(This policy will be responsable to let us upload files from our localhost as well as from the vercel url when in production).

this is the json file to make sure we can upload files from our computer and use the allowed methods:


CORS :
[
    {
        "AllowedHeaders":["*"],
        "AllowedMethods":[
            "PUT","POST","DELETE","GET"
            ],
        "AllowedOrigins":["*"],
        "ExposeHeaders":[]
    }
    
]


## Now we have S3 setup, and can start sending files upthere:

- go to lib and create a s3.ts file
- This s3.ts file will have the code to actually look in the s3 configuration.
- Install s3 package : npm install aws-sdk
- We then need to get the secret acess key and the acesskeyid from the AIM in the aws console
- go to the console and search for AIM, then we need to add a new user to our bucket
- in the AIM page go to usuarios, click create new user and then name it ADM or something.
- go to next, then mark : put in policies manually(the last option)
- Then search for s3 and give it the amazons3fullacess policy.
- then we can create the user.
- Now that we have the user we click on him and go to permissions.
- Then we create an acess key.
- Choose local code
- Now we have what is needed for our app to interact with the s3.

Inside the .env file create two variables:

NEXT_PUBLIC_S3_ACESS_KEY_ID 
NEXT_PUBLIC_S3_SECRET_ACCESS_KEY

Get the two keys in the user acess keys and place them in these variables in order. (we put the NEXT_PUBLIC prefix because we'll be acessing these enviromental variables
from the client(when the user clicks to upload a pdf file)).

We also need the name of our bucket to create the s3 object that we'll be using to acess the bucket, we can store this name inside this variable:

NEXT_PUBLIC_S3_BUCKET_NAME

## How to download and read a file from S3:

- Create a file under lib(it seems all of our utils goes under the lib folder) with following code:


```
import AWS from "aws-sdk";

import fs from "fs";

export async function downloadFromS3(file_key: string) {
  try {
    AWS.config.update({
      accessKeyId: process.env.NEXT_PUBLIC_S3_ACESS_KEY_ID!,
      secretAccessKey: process.env.NEXT_PUBLIC_S3_SECRET_ACCESS_KEY!,
    });
    const s3 = new AWS.S3({
      params: {
        Bucket: process.env.NEXT_PUBLIC_S3_BUCKET_NAME,
      },
      region: "as-east-1",
    });
    const params = {
      Bucket: process.env.NEXT_PUBLIC_S3_BUCKET_NAME!,
      Key: file_key,
    };

    const object = await s3.getObject(params).promise();
    const file_name = `tmp/pdf-${Date.now()}.pdf`;

    fs.writeFileSync(file_name, object.Body as Buffer);

    return file_name;
  } catch (error) {
    console.log("There has been an error downloading the file from aws");
    return null;
  }
}

```





