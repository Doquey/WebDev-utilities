## To only show something if a condition is met we can do this in ts:


```
<div className="flex mt-1">
 {isAuth && <Button>Ir para Chats</Button>}
</div>
```

## If I want to have a conditional and a counter-conditional like an if else I can do this:

```
<div className="something">
{isAuth ? (<h1>show something</h1>):(do something else)

</div>
```

## To use the next router I can do :

```
import { useRouter } from "next/navigation";

const router = useRouter();

router.push("my_route/my_app")

```
