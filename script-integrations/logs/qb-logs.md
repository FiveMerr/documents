# ℹ️ qb-logs

logs.lua

replace ```RegisterNetEvent('qb-log:server:CreateLog'``` in ```qb-smallresources/server/logs.lua```

With Below Code Here

```lua
RegisterNetEvent('qb-log:server:CreateLog', function(name, title, color, message, tagEveryone, imageUrl)
    local postData = {}
    local tag = tagEveryone or false
    
    if Config.Logging == "fivemerr" then
        local embedData = {
                level = tagEveryone and 'warn' or 'info',
                message = title .. " - " .. message,
                resource = "qb-logs",
                metadata = {
                    image = imageUrl,
                    playerId = source,
                }
        }

        local apiKey = GetConvar('FIVEMERR_API_KEY', 'false')
        if apiKey == 'false' then
            print('You need to set the Fivemerr API key in your server.cfg')
            return
        end

        PerformHttpRequest('https://api.fivemerr.com/v1/logs', function(statusCode, response, headers)
        end, 'POST', json.encode(embedData), {
            ['Authorization'] = apiKey,
            ['Content-Type'] = 'application/json',
        })
    end
end)
```

Server.cfg

```
set FIVEMERR_API_KEY "API KEY HERE"
```

config.lua

```
Config.Logging = 'fivemerr'
```
