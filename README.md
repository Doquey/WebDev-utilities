# WebDev-utilities
Will be updating this file whenever I get a front-end/web-developing tip or come by a new usefull tool

Some GRADIENTS : https://hypercolor.dev/

How to use the .env file:

We can acess variables that are inside the .env file in any file that is inside the src folder like this:

process.env.variable_name


however if the file we are acessing the .env file from is outside the src, we can install the dotenv package and do the following:

```
import * as dotenv from "dotenv";
dotenv.config({ path: ".env" });

```
