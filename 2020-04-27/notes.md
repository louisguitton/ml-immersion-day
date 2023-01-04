# Notes

## AI Services
### Polly and Rekognition

- The Polly part is really straight forward: you provide the sentence and the voice you want
  and you get the result as an MP3

- Facial recognition: gender, age bracket, bounding box

- Celebrity recognition: does not work out of the box for Messi. For our domain specific use case,
  we should [search faces in a collection](https://docs.aws.amazon.com/rekognition/latest/dg/collections.html)

  - create collection [doc](https://docs.aws.amazon.com/rekognition/latest/dg/API_CreateCollection.html) [boto](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/rekognition.html#Rekognition.Client.create_collection)
  - index imgaes [doc](https://docs.aws.amazon.com/rekognition/latest/dg/API_IndexFaces.html) [boto](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/rekognition.html#Rekognition.Client.index_faces)
  - search faces by image [doc](https://docs.aws.amazon.com/rekognition/latest/dg/API_SearchFacesByImage.html) [boto](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/rekognition.html#Rekognition.Client.search_faces_by_image)

- Face comparison: you can check if a reference face is in the image

- Text in image: you can read what's on T-shirts

you can get the confidence proba for each item

- didn't get the feeling you can use it straightforward for understanding of it's a fixture piece or not

- [Rekognition SDK](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/rekognition.html)
  - `rekognition.detect_labels`, `rekognition.detect_faces`, `rekognition.detect_text`
  - `rekognition.compare_faces`
  - `rekognition.recognize_celebrities`

### Chatbot with Lex

- https://github.com/jeremywarrick/amazon-ai-building-better-bots

## AI Sagemaker ML Platform

- GroundTruth = prodigy > doccano (due to active learning)
- Sagemaker examples https://github.com/awslabs/amazon-sagemaker-examples

- use cases

  - manage notebooks (lifecycle policy: shut down the notebook after 30 min not used)
  - training models (the more complex the model e.g. DL, the more clients build it inside Sagemaker)
    due to spot instance training
  - deploy (e.g. when you have a kubernetes cluster policy, customers don't use Sagemaker,
    they package it as an image and then deploy it in k8s).
    Smaller teams should use endpoints.

- Object2Vec is Sagemaker's Starspace basically

  - [multilabel classification](https://github.com/awslabs/amazon-sagemaker-examples/tree/master/introduction_to_amazon_algorithms/object2vec_multilabel_genre_classification)
  - [embeddings](https://github.com/awslabs/amazon-sagemaker-examples/tree/master/introduction_to_applying_machine_learning/object2vec_document_embedding)

- for k8s <-> sagemaker interaction, there now are operators for k8s [blog post](https://towardsdatascience.com/kubernetes-and-amazon-sagemaker-for-machine-learning-best-of-both-worlds-part-1-37580689a92f)

- you can pull Sagemaker docker images locally, or set sagemaker as `local-mode`

```sh
$(aws ecr get-login --no-include-email --registry-ids 438346466558 --region eu-west-1)
docker pull 438346466558.dkr.ecr.eu-west-1.amazonaws.com/object2vec:1
```

- to get a model out of Sagemaker: you can try to get S3 artifacts of models and package them myself

- orchestrate with lambda function or with airflow. There is a 4h MLOps workshop at AWS. 
Ask the solution architect or the account manager.
