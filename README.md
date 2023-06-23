## Instructions

1. Clone repo and setup: `npm i && npm run dev`
2. Open the browser
3. Upload the images found in `src/routes/test_files`
4. Check the console logs.

---

## The error

This is the log: a comparison between the error that `zod` throws and the one reported by `superforms`.

```
------- Superforms error -------
{0: {…}, 1: {…}}
    0: arrayBuffer: undefined
        lastModified: undefined
        name: undefined
        size: undefined
        slice: ƒ slice()stream: undefined
        text: undefined
        type: undefined
        webkitRelativePath: undefined
        [[Prototype]]: Object
    1:
        arrayBuffer:
        undefined
        lastModified: undefined
        name: undefined
        size: undefined
        slice: undefined
        stream: undefined
        text: undefined
        type: undefined
        webkitRelativePath: undefined
        [[Prototype]]: Object
    [[Prototype]]: Object


------- Zod error -------
ZodError: [
  {
    "code": "custom",
    "message": "FILE_TYPE_NOT_ALLOWED",
    "path": [
      0
    ]
  }
]
    at get error [as error] (index.mjs:537:31)
    at ZodArray.parse (index.mjs:636:22)
    at $$self.$$.update (+page.svelte:45:16)
    at update (index.mjs:1343:12)
    at flush (index.mjs:1307:17)
```
