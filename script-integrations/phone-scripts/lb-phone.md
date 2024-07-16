# 📳 LB Phone

## Set your config to "Custom".

located: lb-phone/config/config.lua

![image](https://github.com/FiveMerr/documents/assets/112778590/5084d36d-f9c2-4d86-bad1-1a8ccb580327)

## Create a MEDIA API key and add it below to all 3

Located: lb-phone/server/apiKeys.lua

![image](https://github.com/FiveMerr/documents/assets/112778590/b8eac3e8-287e-495d-aeac-7f338d48ba66)

## On UploadMethods at Custom. Replace for this

Located: lb-phone/shared/upload.lua

```lua
    Custom = {
        Video = {
            url = "https://api.fivemerr.com/v1/media/videos",
            field = "file", -- The field name (formData)
            headers = { -- headers to send when uploading
                ["Authorization"] = "API_KEY"
            },
            error = {
                path = "success", -- The path to the error value (res.success)
                value = false -- If the path is equal to this value, it's an error
            },
            success = {
                path = "url" -- The path to the video file (res.url)
            },
        },
        Image = {
            url = "https://api.fivemerr.com/v1/media/images",
            field = "file", -- The field name (formData)
            headers = { -- headers to send when uploading
                ["Authorization"] = "API_KEY"
            },
            error = {
                path = "success", -- The path to the error value (res.success)
                value = false -- If the path is equal to this value, it's an error
            },
            success = {
                path = "url" -- The path to the image file (res.url)
            },
        },
        Audio = {
            url = "https://api.fivemerr.com/v1/media/audios",
            field = "file", -- The field name (formData)
            headers = { -- headers to send when uploading
                ["Authorization"] = "API_KEY"
            },
            error = {
                path = "success", -- The path to the error value (res.success)
                value = false -- If the path is equal to this value, it's an error
            },
            success = {
                path = "url" -- The path to the audio file (res.url)
            },
        },
    },
```

Should look like this now:&#x20;

![image](https://github.com/FiveMerr/documents/assets/112778590/93a3ba7c-f742-4fbc-bb66-99a00da6233a)

Restart your phone script and you're all set!
