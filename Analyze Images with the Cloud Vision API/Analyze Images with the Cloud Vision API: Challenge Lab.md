# Analyze Images with the Cloud Vision API: Challenge Lab
### Task 1 - Verify your resources
After creating the API key, run the following command.
```bash
export API_KEY=<API_KEY>
```

### Task 2 - Create Request.json file
```bash
touch request.json
nano request.json
```
```json
{
  "requests": [
      {
        "image": {
          "source": {
              "gcsImageUri":
          }
        },
        "features": [
          {
            "type":
            "maxResults": 10
          }
        ]
      }
  ]
}
```

### Task 3 - Update the json file
* **TEXT_DETECTION**<br>
Update the json file(request.json) as follows
```json
{
  "requests": [
      {
        "image": {
          "source": {
              "gcsImageUri":"gs://<PROJECT_NAME>-bucket/manif-des-sans-papiers.jpg"
          }
        },
        "features": [
          {
            "type":"TEXT_DETECTION",
            "maxResults": 10
          }
        ]
      }
  ]
}
```
Run the following commands.
```
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json  https://vision.googleapis.com/v1/images:annotate?key=${API_KEY}

curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json  https://vision.googleapis.com/v1/images:annotate?key=${API_KEY} -o text-response.json

gsutil cp text-response.json gs://<PROJECT_NAME>-bucket
```

* **LANDMARK_DETECTION**<br>
Update the json file(request.json) as follows
```json
{
  "requests": [
      {
        "image": {
          "source": {
              "gcsImageUri":"gs://qwiklabs-gcp-02-83f2ae23f73f-bucket/manif-des-sans-papiers.jpg"
          }
        },
        "features": [
          {
            "type":"LANDMARK_DETECTION",
            "maxResults": 10
          }
        ]
      }
  ]
}
```
Run the following commands.
```bash
curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json https://vision.googleapis.com/v1/images:annotate?key=${API_KEY} -o landmark-response.json
gsutil cp landmark-response.json gs://<PROJECT_NAME>-bucket
```
---
**All tasks completed!😄🎉**
