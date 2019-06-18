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

1. AI Services = verticals = Vision, Speech, Language, Chatbots, Forecasting, Recommendations via Serverless Rest APIs
1. ML Services = Sagemaker = notebooks, data labelling, training, optimization, reinforcement learning, deploy
1. ML Frameworks = Tensorflow/Pytorch / Keras / Docker

Services worth checking out for us:

- Rekognition https://aws.amazon.com/rekognition/:
  Activity recognition, person tracking and celebrity recognition
- Transcribe https://aws.amazon.com/transcribe/
- Comprehend https://aws.amazon.com/comprehend/
  Feed data from S3 and get Entities
- Forecast https://aws.amazon.com/forecast/
- Personalize https://aws.amazon.com/personalize/
- Checkout https://aws.amazon.com/sagemaker/neo/

## Lab 1: Lex + Lambda

### What we did

Build a chatbot to order Coffee in various types, sizes, temperature and creamer. Add backend logic to the chatbot with a lambda function. Integrate that chatbot with Slack.

### Learnings

- In Lex, you can follow the GUI to setup your chatbot with "Intents", "Slots" and "Deployment Channels"
- It basically feels like a managed https://rasa.com/

## Lab 2:
