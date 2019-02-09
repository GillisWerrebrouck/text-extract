# Text extraction service
[Google cloud tutorial](https://cloud.google.com/functions/docs/tutorials/ocr#functions_ocr_deploy_process-node8)
## Deployment
* [Create](https://console.cloud.google.com/cloud-resource-manager) Google Cloud project
* Enable billing in your account to be able to use most Google Cloud service
* [Enable](https://console.cloud.google.com/flows/enableapi?apiid=cloudfunctions,pubsub,storage_api,translate,vision.googleapis.com) APIS for the project (Cloud Functions API, Cloud Pub/Sub API, Google Cloud Storage JSON API, Cloud Translation API and Cloud Vision API)
* [Install](https://cloud.google.com/sdk/) the gcloud SDK
* Initialize gcloud: `gcloud init`
* Update gcloud and install beta components: `gcloud components update && gcloud components install beta`
* Create an input and output bucket: `gsutil mb gs://*YOUR_BUCKET_NAME*`
* Configure the app in config.json
* Deploy image processing function: `gcloud functions deploy ocr-extract --runtime nodejs8 --trigger-bucket *YOUR_IMAGE_BUCKET_NAME* --entry-point processImage`
* Deploy text translation function: `gcloud functions deploy ocr-translate --runtime nodejs8 --trigger-topic *YOUR_TRANSLATE_TOPIC_NAME* --entry-point translateText`
* Deploy save results function: `gcloud functions deploy ocr-save --runtime nodejs8 --trigger-topic *YOUR_RESULT_TOPIC_NAME* --entry-point saveResult`
* Test the service via cmd: `gsutil cp *PATH_TO_IMAGE* gs://*YOUR_IMAGE_BUCKET_NAME*`
* Get last logs: `gcloud functions logs read --limit 100`
## Test the code
`npm test`