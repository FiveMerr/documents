# R14 Evidence

This will allow you to upload evidence photos directly to Fivemerr. This will also copy the URL to your clipboard to automatically paste into MDT reports or wherever you need it.

## Prerequisites
* [Fivemerr API Key](https://docs.fivemerr.com/introduction-to-api/readme)
**Note:** I suggest creating a dedicated image only API key for this script.
## Optional
* [Fivemerr Webhook](https://docs.fivemerr.com/features/webhooks)
**Note:** This is not required for this script, but it is a nice feature to have. This needs to be setup in your Fivemerr server under the _webhooks_ section.


## Config File Change
* Navigate to `r14-evidence/config.lua`
* On line _17_, paste the below code:
```
-- Set this to true if you wish to use Fivemerr (https://fivemerr.com/) for media uploads. 
Config.Fivemerr = true
Config.FivemerrKey = '' --Your Fivemerr API key
```

## Client File Change
* Navigate to `r14-evidence/client/main.lua`
 * On line _263_ place the following code (It should be go right above the _TakePhoto()_ function):
 ```
 RegisterNetEvent('fivmerr:takeScreenshot')
AddEventHandler('fivmerr:takeScreenshot', function()
    if Config.Fivemerr then
        print('Fivemerr is enabled, attempting to upload to Fivemerr...')
        exports['screenshot-basic']:requestScreenshotUpload('https://api.fivemerr.com/v1/media/images', 'file', {
            headers = {
                Authorization = Config.FivemerrKey
            },
            encoding = 'jpg'
            },
            function(data)
                TriggerServerEvent('fivmerr:screenshotResult', data)
            end)
    else
        TakePhoto()
    end
end)

RegisterNetEvent('fivmerr:copyToClipboard')
AddEventHandler('fivmerr:copyToClipboard', function(link)
    SendNUIMessage({
        action = 'copyToClipboard',
        text = link
    })
end)
```

## Server File Change
* Navigate to `r14-evidence/server/main.lua`
* On line _23_ place the following code:
```
RegisterNetEvent('fivmerr:screenshotResult')
AddEventHandler('fivmerr:screenshotResult', function(imageData)
    local src = source
    local image = json.decode(imageData)
    local link = (image and image.url) or 'invalid_url'
    print('Fivemerr upload successful, image link: ' .. link)

    -- Ensure the link is valid
    if link ~= 'invalid_url' then
        -- Notify the client
        TriggerClientEvent('QBCore:Notify', src, 'URL Copied to clipboard', 'success', 3000)
        -- Optionally, send the link to the client for clipboard copying
        TriggerClientEvent('fivmerr:copyToClipboard', src, link)
    else
        print('Invalid URL received from Fivemerr')
    end
end)
```

## HTML File Change(s)

* Navigate to `r14-evidence/html/evidence.html`
* Replace it with the following code:
```
<!DOCTYPE html>
<html>
    <body>
        <script src="main.js" type="text/javascript"></script>
        <script>
            document.addEventListener('DOMContentLoaded', () => {
                const input = document.createElement('input');
                document.body.appendChild(input);
                input.select();
                document.execCommand('copy');
                document.body.removeChild(input);
            });
        </script>
    </body>
</html>
```

* Navigate to `r14-evidence/html/main.js`
* Replace it with the following code:
```
const open = (data) => {
  $('#corner1').show();
  $('#corner2').show();
  $('#corner3').show();
  $('#corner4').show();
  $('#battery').show();
  $('#dot').show();
  $('#date').text(data.date);
  $('#record').text("REC");
}

const close = () => {
  $('#corner1').hide();
  $('#corner2').hide();
  $('#corner3').hide();
  $('#corner4').hide();
  $('#battery').hide();
  $('#dot').hide();
  $('#date').text('');
  $('#rec').text('');
}

window.addEventListener('message', function(event) {
    if (event.data.action === 'copyToClipboard') {
        const text = event.data.text;

        // Create a temporary textarea element to hold the text
        const textarea = document.createElement('textarea');
        textarea.value = text;
        document.body.appendChild(textarea);
        textarea.select();
        
        try {
            const successful = document.execCommand('copy');
            const msg = successful ? 'successful' : 'unsuccessful';
        } catch (err) {
            console.error('Unable to copy to clipboard', err);
        }

        // Remove the temporary textarea
        document.body.removeChild(textarea);
    }
});
```


