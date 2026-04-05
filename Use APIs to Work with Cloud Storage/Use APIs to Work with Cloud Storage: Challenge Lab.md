# Use APIs to Work with Cloud Storage: Challenge Lab
### Task1 - Create two Cloud Storage buckets
```bash
export OAUTH2_TOKEN=<ACCESS_TOKEN>
export PROJECT_ID=<PROJECT_ID>
```
* Bucket1
```bash
nano values.json
```

```json
{  
   "name": "<PROJECT_NAME>-bucket-1",
   "location": "us",
   "storageClass": "multi_regional"
}
```


```bash
curl -X POST --data-binary @values.json \
    -H "Authorization: Bearer $OAUTH2_TOKEN" \
    -H "Content-Type: application/json" \
    "https://www.googleapis.com/storage/v1/b?project=$PROJECT_ID"
```

* Bucket2
```bash
nano values.json
```

```json
{  
   "name": "<PROJECT_NAME>-bucket-2",
   "location": "us",
   "storageClass": "multi_regional"
}
```


```bash
curl -X POST --data-binary @values.json \
    -H "Authorization: Bearer $OAUTH2_TOKEN" \
    -H "Content-Type: application/json" \
    "https://www.googleapis.com/storage/v1/b?project=$PROJECT_ID"
```


### Task2 - Upload an image file to a Cloud Storage Bucket
* After upload the image (demo0.jfif)
```bash
export OBJECT=/home/<STUDENT>/demo0.jfif # Use the output of the 'realpath' command.

export BUCKET_NAME=<PROJECT_NAME>-bucket-1
```

```bash
curl -X POST --data-binary @$OBJECT \
    -H "Authorization: Bearer $OAUTH2_TOKEN" \
    -H "Content-Type: image/png" \
    "https://www.googleapis.com/upload/storage/v1/b/$BUCKET_NAME/o?uploadType=media&name=demo1.png"
```


### Task3 - Copy a file to another bucket
```bash
curl -X POST \
  -H "Authorization: Bearer $OAUTH2_TOKEN" \
  -H "Content-Length: 0" \
  "https://storage.googleapis.com/storage/v1/b/$BUCKET_NAME/o/demo1.png/rewriteTo/b/<SECOND_BUCKET_NAME>/o/demo2.png"
```


### Task4 - Make an object (file) publicly accessible
```bash
nano pp.json
```
```json
{
  "entity": "allUsers",
  "role": "READER"
}
```
```bash
curl -X POST "https://storage.googleapis.com/storage/v1/b/$BUCKET_NAME/o/demo1.png/acl" \
  -H "Authorization: Bearer $OAUTH2_TOKEN" \
  -H "Content-Type: application/json" \
  --data-binary @pp.json
```

### Task5 - Delete the object file and a Cloud Storage bucket (Bucket 1)
```bash
curl -X DELETE \
  -H "Authorization: Bearer $OAUTH2_TOKEN" \
  "https://storage.googleapis.com/storage/v1/b/$BUCKET_NAME/o/demo1.png"
```
```bash
curl -X DELETE -H "Authorization: Bearer $OAUTH2_TOKEN" \
  "https://storage.googleapis.com/storage/v1/b/$BUCKET_NAME"
```
---
<b>All tasks completed!😄🎉</b>
