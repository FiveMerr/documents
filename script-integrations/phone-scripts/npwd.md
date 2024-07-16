# 📳 NPWD

Resource can be located [here.](https://github.com/project-error/npwd)\
\
Travel to [config.default.json](https://github.com/project-error/npwd/blob/master/config.default.json#L32).

Edit the following code block to look as below:

```json
"images": {
    "url": "https://api.fivemerr.com/v1/media/images",
    "type": "file",
    "imageEncoding": "webp",
    "contentType": "multipart/form-data",
    "useContentType": false,
    "authorizationHeader": "Authorization",
    "authorizationPrefix": "",
    "useAuthorization": true,
    "returnedDataIndexes": ["url"]
  },
```

Add the following to the lines to [`imageSafety`](https://github.com/project-error/npwd/blob/43fea82c1f838ad5e5e258fa9184fe43ffba571c/config.default.json#L43)

```json
files.fivemerr.com
api.fivemerr.com
```
