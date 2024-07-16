---
description: To upload an audio to the Audio API, send a POST request to the API endpoint.
---

# 🔊 Audio

## API Endpoint

URL: [https://api.fivemerr.com/v1/media/audios](https://api.fivemerr.com/v1/media/audios)

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
    "uuid": "54812bad-eb9a-4ad0-bf90-412185a27e74",
    "filename": "54812bad-eb9a-4ad0-bf90-412185a27e74.mp3",
    "original_filename": "joe_japanese.mp3",
    "mime_type": "audio/mpeg",
    "size": 307722,
    "hash": "4dfdfa634076d6f6abf3b84486c7c2940c1a8d86e60535c4aaca2692fbb6d650",
    "url": "https://fivemerr.com/files/audios/54812bad-eb9a-4ad0-bf90-412185a27e74.mp3",
    "created_at": "2024-07-04T01:04:27.772178312+05:30",
    "updated_at": "2024-07-04T01:04:27.772178364+05:30"
}
```

### Example with Node.js (with Axios)

```javascript
const axios = require('axios');
const fs = require('fs');
const FormData = require('form-data');

// Load the image file
const filePath = '/path/to/your/audio.mp3'; // Replace with your file path
const file = fs.createReadStream(filePath);

// Create a form data object
const form = new FormData();
form.append('file', file);

// Make the POST request
axios.post('https://api.fivemerr.com/v1/media/audios', form, {
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
file_path = '/mnt/data/image.mp3' # Replace with your file path
files = {'file': open(file_path, 'rb')}

# Set the headers
headers = {
    'Authorization': 'YOUR_API_KEY', # Replace with your API key
    'Content-Type': 'multipart/form-data'
}

# Make the POST request
response = requests.post('https://api.fivemerr.com/v1/media/audios', files=files, headers=headers)

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
  url: 'https://api.fivemerr.com/v1/media/audios',
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
  url: 'https://api.fivemerr.com/v1/media/audios',
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

## Supported Audio Types

If you need any other added, let us know.

* **MPEG** - `.mpeg`\
  Files with the extension .mp1, .mp2, .mp3 must use audio/mpeg mimetype. audio/mp3 doesn't exist as such, it is a common mime type but it's official approach is to use the audio/mpeg.
  * **MP4**- `.mp3`
  * **MP3**- `.mp4`
* **WAV** - `.wav`
* **OGG** - `.ogg`
* **AAC** - `.aac`
* **FLAC** - `.flac`
* **WMA** - `.wma`
* **AIFF** - `.aiff` or `.aif`
* **PCM** - `.pcm`
* **AMR** - `.amr`
