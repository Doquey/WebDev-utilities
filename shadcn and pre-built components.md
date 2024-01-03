# This is a very cool tool that lets us get pré-built cool looking components very easily.

## Its build upon the radix-ui library and upon the tailwind css library so it has very good compatibility with both.

## how to get started:

Go to terminal and type:

```
npx shadcn-ui@latest init
```
Respond : yes, default,slate, yes to using css variables, the rest is all yes.

Then go to src/app/globals.css and get ride of the file. After that tell shadcn that this globals.css exist in there still, shadcn will see that there is nothing there and will
replace the file with their own css configuration.

## Whenever I want to use a new component from shadcn I need to do:

- Type this on terminal:
```
npx shadcn-ui@latest add component_name(button for example)
```
- Import the component in the page we want to use it.
