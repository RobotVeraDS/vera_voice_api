# Vera Voice API

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
* `speaker` - Speaker, now available only Archer
* `text` - The text you want to synthesize, e. g. "привет". 300 characters limitation. If you're going to add stress to the word, use "+" before the stressed vowel, e. g. "пр+ивет". The numbers need to be written as words, e. g. “10” - “десять”.
* `get_samples` - boolean, default `false`, return array of samples of audio in headers, 1000 samples per second. You can get it like this: `req.headers["samples"]`
