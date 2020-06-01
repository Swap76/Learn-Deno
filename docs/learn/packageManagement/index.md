### Package Management

There has been a radical rethink regarding the way package management works in Deno. Rather than relying on a central repository, it is decentralized. Anyone can host a package just like anyone can host any type of file on the web.

### How Deno’s new package management works

It’s so radically simplified that it may shock you.

```ts
import { assertEquals } from "https://deno.land/std/testing/asserts.ts";
```

- There is no more centralized package manager. You import ECMAScript modules directly from the web
- There is no more “magical” Node.js module resolution. Now, the syntax is explicit, which makes things much easier to reason about
- There is no more node_modules directory. Instead, the dependencies are downloaded and hidden away on your hard drive, out of sight. If you want to refresh the cache and download them again, just add --reload to your command
