## AI/ML and Generative AI
Leveraging artificial intelligence, machine learning, and generative AI capabilities in a cost-effective manner using services like Amazon SageMaker, Amazon Bedrock, and Amazon Q.

**Artificial intelligence (AI) and machine learning (ML)** refer to the ability of computer systems to perform tasks that normally require human intelligence, such as visual perception, speech recognition, and decision-making. AWS provides a variety of services that enable developers to build AI/ML capabilities into their applications without needing advanced degrees in data science.

**Generative artificial intelligence (generative AI)** is a type of AI that can create new content and ideas, including conversations, stories, images, videos, and music. AI technologies attempt to mimic human intelligence in nontraditional computing tasks like image recognition, natural language processing (NLP), and translation. You can train it to learn human language, programming languages, art, chemistry, biology, or any complex subject matter. It reuses training data to solve new problems. For example, it can learn English vocabulary and create a poem from the words it processes. Your organization can use generative AI for various purposes, like chatbots, media creation, and product development and design.

#### AI/ML/GenAI hierarchy:
- AI: Any technique that allows computers to mimic human intelligence using logic, if-then statements, and machine learning.
- ML: A subset of AI that uses machines to search for patterns in data to build logic models automatically.
- Deep learning/DL: A subset of ML composed of deeply multi-layered neural networks that perform tasks like speech and image recognization.
- Generative AI: Powered by Large models that are pre-trained on vast corpora of data and commonly referred to as foundation models/FMs.

##### How does Generative AI work?
Like all artificial intelligence, generative AI works by using machine learning models—very large models (also known as “foundation models”) that are pretrained on vast amounts of data.
- Foundation models
- Large language models

###### Pricing Options
Generative AI offers two pricing options:
- **API-based pricing:** You pay per API call based on the number of tokens (chunks of text data) or images processed.
- **Compute-based pricing:** You pay per hour of compute instance usage. This allows you to choose the compute instance size and configuration to meet your needs. You have control over the infrastructure like instance type and deployment location.

### Amazon SageMaker
Amazon SageMaker is a cloud machine-learning platform that enables developers to create, train, and deploy machine-learning models in the cloud. SageMaker provides a complete set of tools and capabilities to streamline the machine learning workflow. SageMaker simplifies and accelerates the process of building and deploying machine learning models, making it accessible to a broader audience of developers and data scientists.

Amazon SageMaker helps data scientists and developers to prepare, build, train, and deploy high-quality machine learning (ML) models quickly by bringing together a broad set of capabilities purpose-built for ML. SageMaker supports the leading ML frameworks, toolkits, and programming languages.

With SageMaker you pay for different usage types such as notebook instances, training and processing jobs, hosting and more. In this workshop we provide information on each usage type separately according to the ML lifecycle:
- Build
- Processing
- Train & Tune
- Deploy

**Amazon SageMaker Savings Plans** help to reduce your costs by up to 64%. The plans automatically apply to eligible SageMaker ML instance usage, including SageMaker Studio notebooks, SageMaker notebook instances, SageMaker Processing, SageMaker Data Wrangler, SageMaker Training, SageMaker Real-Time Inference, and SageMaker Batch Transform regardless of instance family, size, or Region.

#### Amazon SageMaker Jumpstart
Amazon SageMaker Jumpstart is a machine learning (ML) hub that can help you accelerate your ML journey. With SageMaker JumpStart, you can evaluate, compare, and select FMs quickly based on pre-defined quality and responsibility metrics to perform tasks like article summarization and image generation. SageMaker JumpStart is charged based on the compute instance hours used for the SageMaker notebook instance that is launched. Some of the top benefits of SageMaker Jumpstart are:
- Flexibility: Deploy, fine-tune, and evaluate closed source and open source pretrained models from thousands popular models' hubs like hugging face through the JumpStart.
- Operational: Fully managed service and scalable infrastructure through instance auto-scaling.

###### Amazon SageMaker Jumpstart Pricing
- Infrastructure cost: You will be charged for the underlying Training and Inference instance hours used the same as if you had created them manually.
- Software cost: Amazon SageMaker JumpStart provides access to hundreds of publicly available and proprietary foundation models from third-party sources and partners.
```
- Publicly available models - no extra charges
- Proprietary models - you are charged for software pricing determined by the model provider. You can review each model pricing in AWS marketplace.
```
