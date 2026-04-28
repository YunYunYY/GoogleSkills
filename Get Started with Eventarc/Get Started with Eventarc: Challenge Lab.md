# Get Started with Eventarc: Challenge Lab
### Set up
```
gcloud config set project <PROJECT_NAME>
gcloud config set run/region "<REGION>"
gcloud config set run/platform managed
gcloud config set eventarc/location "<REGION>"
```

### Task 1. Create a Pub/Sub topic
```bash
gcloud pubsub topics create qwiklabs-gcp-01-6f922f1de918-topic
gcloud  pubsub subscriptions create --topic qwiklabs-gcp-01-6f922f1de918-topic qwiklabs-gcp-01-6f922f1de918-topic-sub
```

### Task 2. Create a Cloud Run sink
* Enable service account
```bash
export PROJECT_NUMBER="$(gcloud projects list \
  --filter=$(gcloud config get-value project) \
  --format='value(PROJECT_NUMBER)')"

gcloud projects add-iam-policy-binding $(gcloud config get-value project) \
  --member=serviceAccount:${PROJECT_NUMBER}-compute@developer.gserviceaccount.com \
  --role='roles/eventarc.admin'
  ```
  * Create a Cloud Run sink
  ```bash
  export SERVICE_NAME=pubsub-events
export IMAGE_NAME="gcr.io/cloudrun/hello"
gcloud run deploy ${SERVICE_NAME} \
  --image ${IMAGE_NAME} \
  --allow-unauthenticated 
  ```

  ### Task 3. Create and test a Pub/Sub event trigger using Eventarc
* Create Trigger
```bash
gcloud eventarc triggers create pubsub-events-trigger \
  --destination-run-service=pubsub-events \
  --transport-topic=$DEVSHELL_PROJECT_ID-topic \
  --event-filters="type=google.cloud.pubsub.topic.v1.messagePublished"
```
* Test Trigger
```bash
gcloud pubsub topics publish $DEVSHELL_PROJECT_ID-topic --message="Test"
```
---
**All tasks completed!😄🎉**
