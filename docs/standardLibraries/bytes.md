# bytes

bytes module is made to provide helpers to manipulation of bytes slice.

## findIndex

Find first index of binary pattern from given binary array.

```typescript
import { findIndex } from "https://deno.land/std/bytes/mod.ts";

findIndex(
  new Uint8Array([1, 2, 0, 1, 2, 0, 1, 2, 0, 1, 3]),
  new Uint8Array([0, 1, 2])
);

// => returns 2
```

## findLastIndex

Find last index of binary pattern from given binary array.

```typescript
import { findLastIndex } from "https://deno.land/std/bytes/mod.ts";

findLastIndex(
  new Uint8Array([0, 1, 2, 0, 1, 2, 0, 1, 3]),
  new Uint8Array([0, 1, 2])
);

// => returns 3
```

## equal

Check whether given binary arrays are equal to each other.

```typescript
import { equal } from "https://deno.land/std/bytes/mod.ts";

equal(new Uint8Array([0, 1, 2, 3]), new Uint8Array([0, 1, 2, 3])); // returns true
equal(new Uint8Array([0, 1, 2, 3]), new Uint8Array([0, 1, 2, 4])); // returns false
```

## hasPrefix

Check whether binary array has binary prefix.

```typescript
import { hasPrefix } from "https://deno.land/std/bytes/mod.ts";

hasPrefix(new Uint8Array([0, 1, 2]), new Uint8Array([0, 1])); // returns true
hasPrefix(new Uint8Array([0, 1, 2]), new Uint8Array([1, 2])); // returns false
```

## repeat

Repeat bytes of given binary array and return new one.

```typescript
import { repeat } from "https://deno.land/std/bytes/mod.ts";

repeat(new Uint8Array([1]), 3); // returns Uint8Array(3) [ 1, 1, 1 ]
```

## concat

Concatenate two binary arrays and return new one.

```typescript
import { concat } from "https://deno.land/std/bytes/mod.ts";

concat(new Uint8Array([1, 2]), new Uint8Array([3, 4])); // returns Uint8Array(4) [ 1, 2, 3, 4 ]
```
