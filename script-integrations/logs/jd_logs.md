---
description: >-
  Stripped apart from JD_Logsv3 Discord and converted to Fivemerr API log
  support.
---

# ℹ️ fm-logs

Download the resource from our GitHub: [https://github.com/FiveMerr/fm-logs](https://github.com/FiveMerr/fm-logs)

Example of a `createLog` function

```
        Logger.CreateLog({
            LogType = "Player", -- The log type, must be defined in the config
            Message = "Player action here", -- The message of the log
            Level = "info", -- The level of the log (can be filtered on Fivemerr)
            Resource = "script-name", -- Resource where the log is coming from
            Source = 1, -- Server id for player (Required for Player Attributes to be pulled)
            Metadata = {} -- Custom attributes to be added
        })
```

