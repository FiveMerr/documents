# 📳 QBCore Phone

Every standard QB-Core server comes with `screenshot-basic` and `qb-phone` out of the box. This at present is configured to use Discord as a CDN.

To _upgrade_ to Fivemerr, follow these simple instructions below:

## Server File Change

* Navigate to `qb-phone/main/server/main.lua`
* Update `WebHook` to the Fivemerr API url based on your token type.
  * Missed the Fivemerr setup? You can find it [here](https://docs.fivemerr.com/introduction-to-api/readme)

```lua
local WebHook = 'https://api.fivemerr.com/v1/media/images' -- Enter the API URL here
local WebHookKey = 'WEBHOOKKEY' -- Add this new var containing your API Key
```

* On line 585/586 locate and find the following callback registration event

```lua
QBCore.Functions.CreateCallback('qb-phone:server:GetWebhook', function(_, cb)
    if WebHook ~= '' then
        cb(WebHook)
    else
        print('Set your webhook to ensure that your camera will work!!!!!! Set this on line 10 of the server sided script!!!!!')
        cb(nil)
    end
end)
```

Found it? Great!

Now replace it to this:

```lua
QBCore.Functions.CreateCallback('qb-phone:server:GetWebhook', function(_, cb)
    if WebHook ~= '' then
        cb(WebHook, WebHookKey)
    else
        print('Set your webhook to ensure that your camera will work!!!!!! Set this on line 10 of the server sided script!!!!!')
        cb(nil)
    end
end)
```

## Client File Change

* Navigate to `qb-phone/main/client/main.lua`
* Search for `exports['screenshot-basic']:requestScreenshotUpload` within this file
* You should find something _similar_ to this:

```lua
QBCore.Functions.TriggerCallback('qb-phone:server:GetWebhook', function(hook)
    if not hook then
        QBCore.Functions.Notify('Camera not setup', 'error')
        return
    end
    exports['screenshot-basic']:requestScreenshotUpload(tostring(hook), 'files[]', function(data)
        SaveToInternalGallery()
        local image = json.decode(data)
        DestroyMobilePhone()
        CellCamActivate(false, false)
        TriggerServerEvent('qb-phone:server:addImageToGallery', image.attachments[1].proxy_url)
        Wait(400)
        TriggerServerEvent('qb-phone:server:getImageFromGallery')
        cb(json.encode(image.attachments[1].proxy_url))
        takePhoto = false
    end)
end)
```

Found it? Great!

Now update it to this:

```lua
QBCore.Functions.TriggerCallback('qb-phone:server:GetWebhook', function(hook, key)
    if not hook or not key then
        QBCore.Functions.Notify('Camera not setup', 'error')
        return
    end
    exports['screenshot-basic']:requestScreenshotUpload(tostring(hook), 'file', {
        headers = {
            Authorization = key
        } 
    }, function(data)
            SaveToInternalGallery()
            local image = json.decode(data)
            local link = (image and image.url) or 'invalid_url'
            DestroyMobilePhone()
            CellCamActivate(false, false)
            TriggerServerEvent('qb-phone:server:addImageToGallery', link)
            Wait(400)
            TriggerServerEvent('qb-phone:server:getImageFromGallery')
            cb(json.encode(link))
            takePhoto = false
    end)
end)
```

Restart your `qb-phone` **or** server and you're done 🎉!
