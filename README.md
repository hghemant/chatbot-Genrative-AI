document_chatbot
Lot of enterprise clients want to understand how they could utilize Generative AI (LLLMs) with their own enterprise data but are concerned about data privacy concerns. This bot provides you a quick way to understand how to utilize LLMs securely for your enterprise data.

Please note that this is just a quick demo and there are better ways of implementing this with Retrieval Augemented Generation. https://aws.amazon.com/blogs/machine-learning/question-answering-using-retrieval-augmented-generation-with-foundation-models-in-amazon-sagemaker-jumpstart/

![image](https://github.com/hghemant/document_chatbot/assets/35923032/31210eaa-d605-4dd3-9421-88dc761a1916)


To understand this chatbot in detail, basic knowledge of following components would help:

Streamlit- A faster way to build and share data apps. Streamlit turns data scripts into shareable web apps in minutes. All in pure Python. No front‑end experience required. www.streamlit.io
Langchain- LangChain is a framework for developing applications powered by language models. It enables applications to connect a language model to other sources of data (for e.g. get data from Google Search results and then answer user's questions in a better way). https://python.langchain.com/docs/get_started/introduction
LLM Model- Foundational models from HuggingFace model hub. https://huggingface.co/models
Architecture diagram for SageMaker implementation


![image](https://github.com/hghemant/document_chatbot/assets/35923032/c49bf914-44bc-4891-837b-d19ce708c610)

The key advantage with this implementation is that no data ever leaves your AWS account. The model is hosted in a SageMaker endpoint in your account and all inference requests will be sent to that endpoint. 

How to run the application with a SageMaker Endpoint

1. Go to the SageMaker folder
2. Install the required packages for this application with pip install -r requirements.txt. To avoid conflicts with existing python dependencies, it is best to do so in a virtual environment:
  $python3 -m venv .venv
  $source .venv/bin/activate
  $pip3 install -r requirements.txt
3. You will need a SageMaker endpoint deployed in your account. If you don't have, one you can use this notebook to deploy the AI21 Jurassic-2 Jumbo Instruct model in your account. Before doing that, you need to go to SageMaker Foundational Model Hub (eg. https://us-west-2.console.aws.amazon.com/sagemaker/home?region=us-west-2#/foundation-models), select the model to be deployed in your SageMaker Notebook above and click "Subscribe". You only need to do it once. Otherwise, you will get an error message during SageMaker notebook execution: "ClientError: An error occurred (ValidationException) when calling the CreateModel operation: Caller is not subscribed to the marketplace offering.". (Caution: This will spin up an ml.p4d.24xlarge instance in your account to host the model, which costs ~$30 per hour!). Alternatively you can deploy a different, smaller model into a SageMaker endpoint or use a ml.g5.48xlarge.
4. Amend the app.py file so that it points to your endpoint (variable endpoint_name) and that it loads your AWS credentials correctly (i.e. set credentials_profile_name when calling the SagemakerEndpoint class)
5. Run the app with streamlit run app.py
6. Upload a text file
7. Start chatting 🤗
   
Running Streamlit apps in SageMaker Studio

If you want to run Streamlit apps directly in SM Studio, you can do so with command streamlit run <app>.py --server.port 6006. Once the app has started you can go to https://<YOUR_STUDIO_ID>.studio.<YOUR_REGION>.sagemaker.aws/jupyter/default/proxy/6006/ to launch the app.
