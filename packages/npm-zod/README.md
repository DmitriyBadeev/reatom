This utility helps to deserialize a plain (JSON) data structure to a reactive data model.

## Installation

```sh
npm i @reatom/npm-zod
```

## Usage

You can find an example here: https://github.com/artalar/reatom/tree/v3/examples/react-table-atomization

```ts
import { parseAtoms } from '@reatom/framework'
import { reatomZod } from '@reatom/npm-zod'
import * as z from 'zod'

export const User = z.object({
  id: z.string().readonly(),
  email: z.string().readonly(),
  name: z.string(),
  age: z.number().optional(),
})

const KEY = 'user-data'
export const model = reatomZod(User, {
  sync(ctx) {
    localStorage.setItem(KEY, JSON.stringify(parseAtoms(ctx, model)))
  },
  initState: JSON.parse(localStorage.getItem(KEY) || '{}'),
})
```
