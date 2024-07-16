# 🤳 ShareX

This will allow you to utilize ShareX to automatically upload your screenshots from ShareX to Fivemerr. This will also copy the URL to your clipboard to automatically paste where you choose.

## Configuration

* Open ShareX main application
* Open Destinations > Custom Uploader Settings
* Create New Uploader
* Set name Fivemerr
* Request URL https://api.fivemerr.com/v1/media/images (Must be typed in)
* Header Name: Authorization
* Value: Your\_Api\_Key (Add your API Key here)
* File Form Name file
* URL {json:url}
* Change destination to Custom Image Uploader

**Please see attached images to see a detailed outline of how it should look**

<figure><img src="https://files.fivemerr.com/images/0b9b20b6-f2d4-412c-b119-ca459ac3feb7.png" alt=""><figcaption><p>Custom Uploader Settings</p></figcaption></figure>

<figure><img src="https://files.fivemerr.com/images/7fa3ba9e-a0fb-4294-a7ba-148ad22aa24b.png" alt=""><figcaption><p>Correct Setting Examples</p></figcaption></figure>

<figure><img src="https://files.fivemerr.com/images/8cafafde-ef3f-458c-bff9-0996f3469d8c.png" alt=""><figcaption><p>Image Uploader Settings</p></figcaption></figure>
