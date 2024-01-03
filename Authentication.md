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
