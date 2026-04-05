# Using the Google Cloud Speech API: Challenge Lab
### Task 1 - Create an API key
After creating the API key, run the following command.
```bash
export API_KEY=<API_KEY>
```

### Task 2 - Transcribe speech to English text
```bash
touch speech_request.json
nano speech_request.json
```
```json
{
  "config": {
      "encoding":"LINEAR16",
      "languageCode": "en-US",
      "audioChannelCount": 2,
      "enableSeparateRecognitionPerChannel": true
  },
  "audio": {
      "uri":"gs://spls/arc131/question_en.wav"
  }
}
```
```bash
curl -s -X POST -H "Content-Type: application/json" --data-binary @speech_request.json \
"https://speech.googleapis.com/v1/speech:recognize?key=${API_KEY}" > response.json
```
The output of **response.json** is as follows.
```json
{
  "results": [
    {
      "alternatives": [
        {
          "transcript": "hi how far is it to the next train station",
          "confidence": 0.993858
        }
      ],
      "channelTag": 1,
      "resultEndTime": "2.490s",
      "languageCode": "en-us"
    },
    {
      "alternatives": [
        {
          "transcript": "hi how far is it to the next train station",
          "confidence": 0.9941575
        }
      ],
      "channelTag": 2,
      "resultEndTime": "2.490s",
      "languageCode": "en-us"
    }
  ],
  "totalBilledTime": "6s",
  "requestId": "766558323086353787"
}
```

### Task 3 - Transcribe speech to Spanish text
```bash
touch request_sp.json
nano request_sp.json
```
```json
{
  "config": {
      "encoding":"FLAC",
      "languageCode": "es-ES"
  },
  "audio": {
      "uri":"gs://spls/arc131/multi_es.flac"
  }
}
```
```bash
curl -s -X POST -H "Content-Type: application/json" --data-binary @request_sp.json \
"https://speech.googleapis.com/v1/speech:recognize?key=${API_KEY}" > response_sp.json
```
The output of **response_sp.json** is as follows.
```json
{
  "results": [
    {
      "alternatives": [
        {
          "transcript": "estoy bien y tú",
          "confidence": 0.8978097
        }
      ],
      "resultEndTime": "1.500s",
      "languageCode": "es-es"
    }
  ],
  "totalBilledTime": "2s",
  "requestId": "5082328754920989484"
}
```
---
<b>All tasks completed!😄🎉</b>
