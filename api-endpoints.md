# To create an api route in next js I can simply:
- Create a folder called api inside the app folder
- Inside this api folder create the name of the api end-point I want
- Inside the end-point I create a file called route.ts and inside of it I write the end-point function and export it.
- Bellow is an example of code of an api-endpoint:
obs: need to install this library to make the queries to my endpoint:

 npm install @tanstack/react-query

 Then we'll also need to wrap our entire app in the react-query provider like so:
 - create a Provider.tsx inside the components folder
 - put this code inside of it:
```
   "use client";
import React from "react";
import { QueryClientProvider, QueryClient } from "@tanstack/react-query";

type Props = {
  children: React.ReactNode;
};

const queryClient = new QueryClient();

const Provider = ({ children }: Props) => {
  return (
    <QueryClientProvider client={queryClient}>{children}</QueryClientProvider>
  );
};

export default Provider;

```
Then we wrap our code up on this Provider so that the data fetched from the server will be cached and available for use in all our pages:


```
import type { Metadata } from "next";
import { Inter } from "next/font/google";
import "./globals.css";
import { ClerkProvider } from "@clerk/nextjs";
import Provider from "@/components/Provider";

const inter = Inter({ subsets: ["latin"] });

export const metadata: Metadata = {
  title: "GemPDF",
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <ClerkProvider>
      <Provider>
        <html lang="en">
          <body className={inter.className}>{children}</body>
        </html>
      </Provider>
    </ClerkProvider>
  );
}

```


## Now in order for us to be able to "hit" these endpoints we have created and put in the cache convention we need to use the useMutation from @tanstack/react-query";
I will leave an example on just how to do this in the fileUpload code.
