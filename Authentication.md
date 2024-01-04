# The best tool I have come by so far for this is Clerk:

-Website : https://clerk.com/
-Its free and can be used for any kind of application and just need to be easily configured into the next js app.

## To setup and use the clerk authentication I can just go to their documentation and follow it:

- https://clerk.com/docs/quickstarts/nextjs?_gl=1*1atubvg*_ga*MTE1ODE0MDkyNS4xNzA0MjgzNDc3*_ga_1WMF5X234K*MTcwNDI4MzQ3Ni4xLjEuMTcwNDI4Mzk5MS4wLjAuMA..*_gcl_au*MTQ3MTc3MTQyOS4xNzA0MjgzNDc3

## Following the setup and running code at the clerk documentation the middleware.ts file will protect all of our routes, meaning all of the routes will be protected by authentication by default. To have some route, say the home page of the app, that is not protected we can do the following on the middleware.ts file:

export default authMiddleware({
  publicRoutes:['/'],
});

export const config = {
  matcher: ["/((?!.+\\.[\\w]+$|_next).*)", "/", "/(api|trpc)(.*)"],
};


## Can use a the UserButton to let the user logout easily and manage their account as well.

import { UserButton } from "@clerk/nextjs";

<UserButton afterSignOutUrl="/"> 


## After this we have almost everything setup, now we just need some more information to place on the .env file so that our clerk api knows where to look for our login page and the for the logout page. In summary we need to define in which route our login and logout pages are going to be set.


```
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_ZmFzdC1tYW50aXMtNzUuY2xlcmsuYWNjb3VudHMuZGV2JA
CLERK_SECRET_KEY=sk_test_hnYnuVNgMUmt6oEYR6AjExYpOAT2bCBel0FE8hH2Ku
NEXT_PUBLIC_CLERK_SIGN_IN_URL =/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL =/sign-up
NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL =/
NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL =/

```



## Verifying if a user is signed in:


```
import { auth } from '@clerk/nextjs';
 
export default function Page() {
const { userId } : { userId: string | null } = auth();
```

