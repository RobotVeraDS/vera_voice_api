# Vera Voice API (Beta)

Here is API documentation for TTS service from [veravoice.ai](https://veravoice.ai/).
First of all, you need to pass registration. It's not open for everybody, so you need to write an email to apirequest@veravoice.ai and describe your use case.

After you receive username and password, you need to get auth-token:
```python
import requests
login_url = "https://api.veravoice.ai/api-token-auth/"
req = requests.post(login_url, data={"username": "you_username", "password": "your_password"})
token = req.json()["token"]
```

Then you can call TTS API like this:
```python
headers={"Authorization": "Token " + token}
data = {"speaker": "archer", "text": "Ваш текст"}
req = requests.post("https://api.veravoice.ai/api/tts", data=data, headers=headers)
```

API endpoint: `https://api.veravoice.ai/api/tts`
Method: `POST`

### Parameters
* `speaker` - Speaker, you can get a list of all available speakers at the link: `https://api.veravoice.ai/api/speakers/`
* `text` - The text you want to synthesize, e. g. "привет". 1500 characters limitation. If you're going to add stress to the word, use "+" before the stressed vowel, e. g. "прив+ет". The numbers need to be written as words, e. g. “10” - “десять”.
* `frame_rate` - integer, valid values are from 0 to 1000, if you pass this parameter, it returns the array of samples of audio (passed value of samples per second) and audio in base64 in JSON-response. You can get it like this: `req.json()["array_of_samples"]`, and get audio bytes like this:
```python
import base64
audio_bytes = base64.b64decode(req.json()["audio"])

```

Your requests' statistics available at this https://api.veravoice.ai/api/requests/.
