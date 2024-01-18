# Using stripe api to handle payment for us

```
npm install stripe
```
## Create a stripe connection, inside a lib/stripe.ts file:
```
import Stripe from "stripe";

export const stripe = new Stripe(process.env.STRIPE_API_KEY as string, {
    apiVersion:'2023-10-16'
    typescript: true,
});

```
## to get the API_KEY I can go to stripe and "criar conta", then "desenvolvedores" and api keys.(get the secret key)
