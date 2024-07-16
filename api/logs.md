---
description: To create a log using the Logs API, send a POST request to the API endpoint.
---

# ℹ️ Logs

## API Endpoint

URL: [https://api.fivemerr.com/v1/logs](https://api.fivemerr.com/v1/logs)

## Authorization

You can access the API using one of the following methods:

* Include the `Authorization` header with your API key.
* Include the `apiKey` as a query parameter in the URL.

## Body

The request body should be a JSON object containing the following keys:

* **level** (required): A string. Recommended values include:
  * `info`
  * `warn`
  * `error`
  * `fatal`
  * `debug`
* **message** (required): A string.
* **resource** (optional): A string.
* **metadata** (optional): A JSON object of any shape.

### **Example**

```json5
{
    "level": "fatal",
    "message": "Something went wrong in the server",
    "resource": "core",
    "metadata": {
        "server": "Primary",
        "team": "unknown"
    }
}
```



## Example with Node.js (with Axios)

```javascript
const axios = require('axios');

const data = {
    "level": "fatal",
    "message": "Something went wrong in the server",
    "resource": "core", // optional
    "metadata": { // optional
        "server": "Primary",
        "team": "unknown"
    }
}

const config = {
  method: 'post',
  url: 'https://api.fivemerr.com/v1/logs',
  headers: { 
    'Content-Type': 'application/json', 
    'Authorization': '••••••'
  },
  data : data
};

axios.request(config)
.then((response) => {
  console.log(response.data);
})
.catch((error) => {
  console.log(error);
});

```
