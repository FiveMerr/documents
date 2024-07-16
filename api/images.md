---
description: To upload an image to the Image API, send a POST request to the API endpoint.
---

# 🖼️ Images

## API Endpoint

URL: [https://api.fivemerr.com/v1/media/images](https://api.fivemerr.com/v1/media/images)

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
    "id": 3,
    "uuid": "f1ce38a5-4e05-456e-9e86-33c2f269fcdf",
    "filename": "f1ce38a5-4e05-456e-9e86-33c2f269fcdf.jpg",
    "original_filename": "xjss8mp8il3b1.jpg",
    "mime_type": "image/jpeg",
    "size": 180585, // in bytes
    "hash": "63b89ee6f0b2e368d9823c5c0fc42b4ad080b42548c8d692516ea6a942ab612f",
    "url": "https://fivermerr/files/images/f1ce38a5-4e05-456e-9e86-33c2f269fcdf.jpg",
    "created_at": "2024-07-04T00:53:53.569154676+05:30",
    "updated_at": "2024-07-04T00:53:53.569154745+05:30"
}
```

### Example with Node.js (with Axios)

```javascript
const axios = require('axios');
const fs = require('fs');
const FormData = require('form-data');

// Load the image file
const filePath = '/path/to/your/image.png'; // Replace with your file path
const file = fs.createReadStream(filePath);

// Create a form data object
const form = new FormData();
form.append('file', file);

// Make the POST request
axios.post('https://api.fivemerr.com/v1/media/images', form, {
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
file_path = '/mnt/data/image.png' # Replace with your file path
files = {'file': open(file_path, 'rb')}

# Set the headers
headers = {
    'Authorization': 'YOUR_API_KEY', # Replace with your API key
    'Content-Type': 'multipart/form-data'
}

# Make the POST request
response = requests.post('https://api.fivemerr.com/v1/media/images', files=files, headers=headers)

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
  url: 'https://api.fivemerr.com/v1/media/images',
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
  url: 'https://api.fivemerr.com/v1/media/images',
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

## Supported Image Extensions&#x20;

If you need any other added, let us know.

* **JPEG** - `.jpeg`
* **PNG** - `.png`
* **WEBP**- `.webp`
* **GIF** - `.gif`
* **BMP** - `.bmp`
* **TIFF** - `.tif` or `.tiff`
* **HEIC** - `.heic`
* **SVG** - `.svg`
* **ICO** - `.ico`

## FiveM Integration&#x20;

