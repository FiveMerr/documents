# 📷 Spy Bodycam

This feature is available from version 2.5.0 or higher.

## Steps:

1. Set the `Upload.ServiceUsed` to 'fivemerr' in `server/upload_config.lua`:
    ```lua
    Upload.ServiceUsed = 'fivemerr'
    ```
   
2. Create a video-only token and place it in the `Upload.Token` field in `server/upload_config.lua`:
    ```lua
    Upload.Token = 'YOUR_TOKEN'
    ```

Once you have completed these steps, the configuration is finished.
