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

4. Deploy the container into the Cloud run with `gcloud run deploy nextwords-app --image gcr.io/<project-id>/nextwords-app --platform managed --memory 1Gi`
> replace the <project-id> with your project id. Changes the memory to 1GB because the default memory (512 MiB is not enough)

## Google Cloud Infrastructure
[![Infrastucture Image](Infrastucture/Lokal.ind%20Diagram.png)
](https://github.com/C241-PS127/Cloud-Computing-API/blob/main/Infrastucture/Lokal.ind%20Diagram.png)

## API Documentation
- Predict Next Word
  - method: POST
  Send a POST request to <Cloud_Run_Endpoint>/predict with JSON data containing the seed_text and optionally next_words:
  > replace <Your_Cloud_Run_Endpoint> with endpoint that you got from deploy the container to the cloud run
  -body request:
    {
    "seed_text": "kaos",
    "next_words": 2
    }
    *seed_text: The starting text from which the prediction will start.
    *next_words: (Optional) Number of words to predict following the seed_text. Defaults to 1 if not specified.
  -body response:
  {
    "predicted_text": "kaos eiger shirt"
  }
