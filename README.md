# Next Word Prediction API Deployment

This Flask-based API predicts the next word(s) in a given text sequence using a pre-trained Keras model. This API was used to provide AI-generated next word at the user's search bar. Using Dockerfile to build this code into Container Registry for deployment requirements to the Cloud Run. The model was saved on the root of the registry.

## Features

- Predict the next word(s) based on a seed text
- Customizable number of words to predict
- RESTful API endpoint for easy integration

## Get Started (Cloud Run Deployment)

1. Clone repository with command `git clone <repo_url>`
2. Move to directory `cd Cloud-Computing-API`

3. Build Container Registry with command `gcloud builds submit --tag gcr.io/<project-id>/nextwords-app`
> replace the <project-id> with your project id

4. Deploy the container into the Cloud run with
```
gcloud run deploy nextwords-app --image gcr.io/<project-id>/nextwords-app --platform managed --memory 1Gi
```
> replace the <project-id> with your project id. Changes the memory to 1GB because the default memory (512 MiB is not enough)

## Google Cloud Infrastructure
![Infrastucture Image](https://github.com/C241-PS127/Cloud-Computing-API/blob/main/Infrastucture/Lokal.ind%20Diagram.png)

## API Documentation

### Predict Next Word

- **Method**: POST
- **Endpoint**: `<Cloud_Run_Endpoint>/predict`
> replace <Cloud_Run_Endpoint> with endpoint that you got from deploy the container to the cloud run

#### Request Body
```json
{
  "seed_text": "kaos",
  "next_words": 2
}
```
* seed_text: The starting text from which the prediction will start.
* next_words: (Optional) Number of words to predict following the seed_text. Defaults to 1 if not specified.

#### Response Body
```json
{
    "predicted_text": "kaos eiger shirt"
}
```
Model Details
* The model (model_predict_next_words.h5) used in this API is pre-trained for predicting the next words in a sequence.
* It utilizes a tokenizer trained on data from API_DS.csv to preprocess text inputs and outputs.
> Notes
> * Adjust max_sequence_len in app.py according to your model's maximum sequence length.
> * Ensure that model_predict_next_words.h5 and API_DS.csv are accessible to the application when deployed.
