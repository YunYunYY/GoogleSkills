# Implement Sensitive Data Protection on Google Cloud: Challenge Lab
### Task 1. Redact sensitive data from text content
```bash
nano redact-request.json
```
```json
{
	"item": {
		"value": "Please update my records with the following information:\n Email address: foo@example.com,\nNational Provider Identifier: 1245319599"
	},
	"deidentifyConfig": {
		"infoTypeTransformations": {
			"transformations": [{
				"primitiveTransformation": {
					"replaceWithInfoTypeConfig": {}
				}
			}]
		}
	},
	"inspectConfig": {
		"infoTypes": [{
				"name": "EMAIL_ADDRESS"
			},
			{
				"name": "US_HEALTHCARE_NPI"
			}
		]
	}
}
```

```bash
gcloud auth print-access-token
```
```bash
export PROJECT_ID=$DEVSHELL_PROJECT_ID
export ACCESS_TOKEN=<YOUR_TOKEN>
curl -s \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  https://dlp.googleapis.com/v2/projects/$PROJECT_ID/content:deidentify \
  -d @redact-request.json -o redact-response.txt
```

```bash
gsutil cp redact-response.txt gs://<BUCKET_NAME>
```

### Task 3. Configure a job trigger to run DLP inspection
* De-identification template
```
projects/<PROJECT_NAME>/locations/us/deidentifyTemplates/unstructured_data_template
```
* Structured de-identification template
```
projects/<PROJECT_NAME>/locations/us/deidentifyTemplates/structured_data_template
```

---
<b>All tasks completed!😄🎉</b>
