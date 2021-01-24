Generate from OpenAPI 3.0's resolved json with:

```
widdershins --search false --language_tabs 'shell' 'python' 'javascript' --summary kiri-ai-Kiri_Model_API-1.0.0-resolved.json --resolve --httpsnippet -o source/index.html.md
```

Ensure that the updated `index.html.md` is in the source folder.

Push changes to main and they should be up in a few minutes on [docs.kiri.ai](http://docs.kiri.ai).
