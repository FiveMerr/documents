# 📸 screenshot-basic

Every server comes with this already if you do not have it, download the resource from [here.](https://github.com/citizenfx/screenshot-basic)

Use the following export.

```lua
exports['screenshot-basic']:requestScreenshotUpload('https://api.fivemerr.com/v1/media/images', 'file', {
    headers = {
        Authorization = 'YOUR_API_KEY'
    },
    encoding = 'png'
}, function(data)
    local resp = json.decode(data)
    local link = (resp and resp.url) or 'invalid_url'
    print(link)
end)
```
