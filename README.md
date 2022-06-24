### What is this repo?

This repo is an example barebones Hugo site that reproduces a bug in Hugo described in this discussion thread: https://discourse.gohugo.io/t/taxonomy-list-page-takes-a-wrong-template/20189/5

### Steps used to reproduce the issue

 - Specified a taxonomy and HTML outputs for `taxonomy` and `terms` in `config.toml` with:
```
[taxonomies]
test_taxonomy = "test_taxonomy"
[outputs]
taxonomy = [ 'HTML' ]
term = [ 'HTML' ]
```
 - Defined some test content at `content/test_pages/test_1.md` with a taxonomy term specified in front matter:
```
---
test_taxonomy:
 - term1
---
```
 - Defined taxonomy templates:

`layouts/test_taxonomy/taxonomy.html`:
```
<html>
<head></head>
<body>
<div>kind: {{ .Kind }}</div>
<div>template: taxonomy.html</div>
</body>
</html>
```
`layouts/test_taxonomy/terms.html`:
```
<html>
<head></head>
<body>
<div>kind: {{ .Kind }}</div>
<div>template: terms.html</div>
</body>
</html>
```
 - Ran `hugo`

### Expected Behavior

 - A page is rendered at `public/test_taxonomy/index.html` with the content:
```
<html>
<head></head>
<body>
<div>kind: taxonomy</div>
<div>template: taxonomy.html</div>
</body>
</html>
```
 - A page is rendered at `public/test_taxonomy/term1/index.html` with the content:
```
<html>
<head></head>
<body>
<div>kind: term</div>
<div>template: terms.html</div>
</body>
</html>
```

### Actual Behavior

 - A page is rendered at `public/test_taxonomy/index.html` with the content:
```
<html>
<head></head>
<body>
<div>kind: taxonomy</div>
<div>template: terms.html</div>
</body>
</html>
```
 - A page is rendered at `public/test_taxonomy/term1/index.html` with the content:
```
<html>
<head></head>
<body>
<div>kind: term</div>
<div>template: taxonomy.html</div>
</body>
</html>
```
