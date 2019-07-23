# 2019-06-18 - AWS Machine Learning Immersion Day

What we did was a mixture of

- https://aws.amazon.com/blogs/machine-learning/building-better-bots-part-2/

## Agenda

https://mlimmersiondayberlin.splashthat.com/

- Intro
- Chatbot
- SageMaker
- Tensorflow

## Intro

There are 3 tiers of AI related services in AWS

1. **AI Services** = verticals = Vision, Speech, Language, Chatbots, Forecasting, Recommendations via Serverless Rest APIs
1. **ML Services** = Sagemaker = notebooks, data labelling, training, optimization, reinforcement learning, deploy
1. **ML Frameworks** = Tensorflow / Pytorch / Keras / Docker

Services worth checking out for us:

- Rekognition https://aws.amazon.com/rekognition/:
  Activity recognition, person tracking and celebrity recognition
- Transcribe https://aws.amazon.com/transcribe/
- Comprehend https://aws.amazon.com/comprehend/
  Feed data from S3 and get Entities
- Forecast https://aws.amazon.com/forecast/
- Personalize https://aws.amazon.com/personalize/

### Learnings

- https://aws.amazon.com/blogs/machine-learning/build-a-social-media-dashboard-using-machine-learning-and-bi-services/
- cf BlazingText https://docs.aws.amazon.com/sagemaker/latest/dg/blazingtext.html
  - unsupervised pretrained https://github.com/awslabs/amazon-sagemaker-examples/blob/master/introduction_to_amazon_algorithms/blazingtext_hosting_pretrained_fasttext/blazingtext_hosting_pretrained_fasttext.ipynb
  - unsupervised trained from scratch
  - supervised 10 classes https://github.com/awslabs/amazon-sagemaker-examples/tree/master/introduction_to_amazon_algorithms/blazingtext_text_classification_dbpedia

## Lab 1: Lex + Lambda

### What we did

Build a chatbot to order Coffee in various types, sizes, temperature and creamer. Add backend logic to the chatbot with a lambda function. Integrate that chatbot with Slack.

### Learnings

- In Lex, you can follow the GUI to setup your chatbot with "Intents", "Slots" and "Deployment Channels"
- It basically feels like a managed https://rasa.com/

## Lab 2: Sagemaker - built-in and custom models

### What we did

1. Predict if a video game will be a sales hit based on genre, publisher and ratings using a AWS optimised XGBoost.
2. Predict telco user churn based on usage features.
3. Classify images using a pretrained image classifier fine tuned on a small dataset.
4. Do the same but this time we use auto-tuning to improve prediction accuracy and deploy it on Elastic Inference
5. IMDB reviews sentiment analysis with a custom keras-tensorflow model

### Learnings

- Notebook instance is launched
  - we bing a sagemaker to a git repo with the notebooks
  - we used the `import sagemaker` python library
- Algorithms are built-in and optimised
  - you use `sagemaker.amazon.amazon_estimator.get_image_uri` to get the built-in XGBoost image
  - you can use pipe mode to stream training data in
- Training and Deployment

  - you use `sagemaker.estimator.Estimator` to get a sklearn like object
  - then "Estimator.fit" creates a Sagemaker training job
  - then "Estimator.deploy" creates an inference endpoint and gives back a `sagemaker.predictor.Predictor`
  - then "Predictor.predict"
  - using the Predictor object, classifying telco users or pictures is really similar, except `classifier.content_type = 'application/x-image'` vs `classifier.content_type = 'text/x-libsvm'`

- Custom models

  - `sagemaker.tensorflow.TensorFlow` is the object to train a custom tensorflow model

- Misc
  - `from sklearn.datasets import dump_svmlight_file` is cool, getting rid of boilerplate and using the `.libsvm` data format
  - sagemaker integrated with airflow
