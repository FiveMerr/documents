---
description: To upload a video to the Video API, send a POST request to the API endpoint.
---

# 🎥 Video

## API Endpoint

URL: [https://api.fivemerr.com/v1/media/videos](https://api.fivemerr.com/v1/media/videos)

## Authorization

You can access the API using one of the following methods:

* Include the `Authorization` header with your API key.
* Include the `apiKey` as a query parameter in the URL.

## Supported Request Formats

The API supports the following request formats:

* form-data
* json
* x-www-form-urlencoded

Each request must include the appropriate header to be accepted.

## Form Data Requests

### Body

The request body should be a form-data object containing a file named `file` or `data`.&#x20;

### Response

The response JSON body takes the following shape:

```json
{
    "id": 1,
    "uuid": "acdde24a-1a46-4880-9744-8b26b49f0460",
    "filename": "acdde24a-1a46-4880-9744-8b26b49f0460.mp4",
    "original_filename": "input.mp4",
    "mime_type": "video/mp4",
    "size": 137489,
    "hash": "ee828a888bf2c429b878306f8fc35bf9a7daff097b48a5cb7909a033f53274ed",
    "url": "https://fivemerr.com/files/videos/acdde24a-1a46-4880-9744-8b26b49f0460.mp4",
    "created_at": "2024-07-04T01:06:59.245622227+05:30",
    "updated_at": "2024-07-04T01:06:59.245622285+05:30"
}
```

### Example with Node.js (with Axios)

```javascript
const axios = require('axios');
const fs = require('fs');
const FormData = require('form-data');

// Load the image file
const filePath = '/path/to/your/video.mp4'; // Replace with your file path
const file = fs.createReadStream(filePath);

// Create a form data object
const form = new FormData();
form.append('file', file);

// Make the POST request
axios.post('https://api.fivemerr.com/v1/media/videos', form, {
  headers: {
    ...form.getHeaders(),
    'Authorization': 'YOUR_API_KEY' // Replace with your API key
  }
})
.then(response => {
  console.log(response.data.url);
})
.catch(error => {
  console.error(error);
});

```

### Example with Python

```python
import requests

# Load the image file
file_path = '/mnt/data/video.mp4' # Replace with your file path
files = {'file': open(file_path, 'rb')}

# Set the headers
headers = {
    'Authorization': 'YOUR_API_KEY', # Replace with your API key
    'Content-Type': 'multipart/form-data'
}

# Make the POST request
response = requests.post('https://api.fivemerr.com/v1/media/videos', files=files, headers=headers)

# Print the response
print(response.json())
```

## JSON Requests

### Body

The request body should be a JSON string containing a key named `file` or `data`.  Data should be encoded as base64 in the following format.

```
data:[<mediatype>][;base64],<data>
```

### Example with Node.js (with Axios)

<pre class="language-javascript"><code class="lang-javascript"><strong>const axios = require('axios');
</strong>
let data = JSON.stringify({
  "file": "data:image/png;base64,iVBORw0KGgoAAA=="
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://api.fivemerr.com/v1/media/videos',
  headers: { 
    'Content-Type': 'application/json', 
    'Authorization': '••••••'
  },
  data : data
};

axios.request(config)
.then((response) => {
  console.log(JSON.stringify(response.data));
})
.catch((error) => {
  console.log(error);
});
</code></pre>

## x-www-form-urlencoded Requests

### Body

The request body should be x-www-form-urlencoded containing a key named `file` or `data`.  Data should be encoded as base64 in the following format.

```
data:[<mediatype>][;base64],<data>
```

### Example with Node.js (with Axios)

```javascript
const axios = require('axios');
const qs = require('qs');
let data = qs.stringify({
  'file': 'data:image/png;base64,iVBORw0kJggg==' 
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://api.fivemerr.com/v1/media/videos',
  headers: { 
    'Content-Type': 'application/x-www-form-urlencoded', 
    'Authorization': '••••••'
  },
  data : data
};

axios.request(config)
.then((response) => {
  console.log(JSON.stringify(response.data));
})
.catch((error) => {
  console.log(error);
});
```

## Supported Video Type

If you need any other added, let us know.

* **MP4** - `.mp4`
* **OGG** - `.ogg`
* **WEBM** - `.webm`
* **AVI** - `.avi`
* **MKV** - `.mkv`
* **MOV** - `.mov`
* **WMV** - `.wmv`
* **FLV** - `.flv`
* **M4V** - `.m4v`
