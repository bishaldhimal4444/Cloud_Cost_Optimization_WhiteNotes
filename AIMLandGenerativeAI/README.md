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

### 1. Amazon SageMaker
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


## 2. Amazon Bedrock
Amazon Bedrock is a fully managed service that offers a choice of high-performing foundation models (FMs) via a single API.

Some of the top benefits of Bedrock are:
- Flexibility: Choice of FMs from Amazon, AI21 Labs, Anthropic, Cohere, Stability AI, Meta and more.
- Security: Comprehensive AWS security controls and services
- Using API calls: No need to manage infrastructure.
- Customization: You can customize your model with Knowledge Bases, which are large datasets of structured information that can be used to enhance the capabilities of foundation models.

In Amazon Bedrock, you will be charged for model inference and/or customization. Inference refers to the ability of foundation models to make predictions or generate content based on what they have learned from their training data. Model customization refers to the ability to take a pre-trained foundation model and customize it for your specific use case. This allows you to enhance the model's capabilities for your domain without extensive retraining.

###### Amazon Bedrock pricing

You have a choice of two pricing plans for inference:
- On-Demand: This mode allows you to use FMs on a pay-as-you-go basis without having to make any time-based term commitments for real-time and batch invocations.
- Provisioned Throughput: This mode allows you to provision sufficient throughput to meet your application's performance requirements in exchange for a one/six months time-based term commitment.

##### Model Customization

- Retrieval-Augmented Generation (RAG)
```
Called knowledge bases in Bedrock
Specialized knowledge through prompt augmentation
No change to the foundational model
Can help make model smarter which could result in less prompt/responses/tokens
More flexible when referenced data is dynamic
```
- Fine-Tuning
```
Continued Pre-Training
Embed specialized knowledge into a model for specific taks
Requires labeled data
Resulting fine tuned model requires provisioned throughput (unless using Nova models)
Fine tuned model can provide higher quality and more contextually relevant answers which could result in less prompt/response/tokens
Best when data is mostly fixed because data changes will require re-training
```
- Continued Pre-Training
```
Generalized and specialized knowledge for your domain
Supports unlabled, unstructured data
Resulting model requires provisioned throughput (unless using Nova models)
Supports frequently changing data
```

###### Model Distallation
Distallation uses a larger teacher model to train a smaller student model. The result is a customized model that is up to 500% faster, 75% less expensive than the original models with less than 2% accuracy loss for use cases like RAG. Customize a model with distallation in Amazon Bedrock.

###### Prompt Caching
When a prompt is sent to a model within 5 minutes of the same prompt being sent, it will be responded to from the cache instead of the model having the process the prompt. A successful prompt hit refreshes the 5 minute TTL on the cache. Prompt caching reduces costs by up to 90% and latency by up to 85% for supported models. Prompt Caching for faster model inference.

###### Intelligent Prompt Routing (IPR)
IPR automatically route prompts to different foundation models to optimize response quality and lower costs. It provides a single endpoint to efficiently route prompts and uses advanced prompt matching techniques to meet cost and latency thresholds. It reduces costs by up to 30%. Understanding Intelligent Prompt Routing.

## 3. Amazon Q
- **Amazon Q:** Amazon Q generates code, tests, debugs, and has multistep planning and reasoning capabilities that can transform and implement new code generated from developer requests. Amazon Q also makes it easier for employees to get answers to questions across business data—such as company policies, product information, business results, code base, employees, and many other topics—by connecting to enterprise data repositories to summarize the data logically, analyze trends, and engage in dialogue about the data.

- **Amazon Q Business:** Amazon Q Business is a generative AI–powered assistant that can answer questions, provide summaries, generate content, and securely complete tasks based on data and information in your enterprise systems. It empowers employees to be more creative, data-driven, efficient, prepared, and productive.

Amazon Q Business Lite - $3 per user/mo. The Amazon Q Business Lite subscription provides users access to basic functionality such as asking questions and receiving permission-aware responses.

Amazon Q Business Pro - $20 per user/mo. The Amazon Q Business Pro subscription provides users access to the full suite of Amazon Q Business capabilities, including access to Amazon Q Apps, and Amazon Q in QuickSight (Reader Pro).

To effectively manage Amazon Q Business license costs, conduct regular audits of user accounts to remove access for departed employees and reassess whether existing users need their current license type. Start all new users with the Lite license as the default option and only upgrade to Pro when the additional features are truly necessary. Since pricing is per-user, maintaining tight control over user provisioning and license allocation is essential for cost optimization.

- **Amazon Q Developer:** Amazon Q Developer (AI Coding Assistant) assists developers and IT professionals with all their tasks—from coding, testing, and upgrading applications, to diagnosing errors, performing security scanning and fixes, and optimizing AWS resources. Amazon Q has advanced, multistep planning and reasoning capabilities that can transform (for example, perform Java version upgrades) and implement new features generated from developer requests.

Amazon Q Developer Free Tier – Free. Individual developers can sign up and sign in using an email address with an AWS Builder ID to start using Amazon Q Developer within minutes. The Individual Tier provides code suggestions, reference tracking, security scans, and includes Amazon Q conversational coding.

Amazon Q Developer Pro Tier - $19/mo. per user. Offers administrative capabilities to organizations that want to provide their developers with access to Amazon Q Developer. Administrators get organizational license management to centrally manage which developers in the organization should have access to Amazon Q Developer. They also get organizational policy management to set service policies at the organizational level, such as whether developers are allowed to receive code suggestions that might be similar to particular open-source training data.


###### Amazon QuickSight

Amazon Q brings its advanced generative AI technology to Amazon QuickSight, the AWS unified business intelligence (BI) service built for the cloud. With Amazon Q in QuickSight, customers get a Generative BI assistant that allows business analysts to use natural language to build BI dashboards in minutes and easily build visualizations and complex calculations. Additionally, business users can go beyond dashboard-delivered insights with multi-visual Q&A responses, get AI-driven executive summaries of dashboards, and create detailed and customizable data stories highlighting key insights, trends, and drivers.

###### Amazon Connect

In Amazon Connect, our contact center service, Amazon Q helps your customer service agents provide better customer service. Amazon Q in Connect uses the real-time conversation with the customer along with relevant company content to automatically recommend what to say or what actions an agent should take to better assist customers.

## Note's:
**1. A company wants to create a text summarization application, without provisioning infrastructure. They are missing ML OPs knowledge in the company. Which AWS service they should use?**
- Amazon Bedrock

**2. You want to create a customized model on Amazon Bedrock, that will include internal company datasets, which option will be the best fit for building this solution?**
- Fine-tune a model (FM) on Amazon Bedrock

**3. Bedrock pricing model is:**
- Based on tokens and/or images

**4. Your company is getting ready to launch a generative AI application build with Meta's Llama 2 chat 13B foundation model. You're now about to go into production and expect heavy user traffic. What is the most cost-effective way to ensure your users can access the application?**
- Move to 6-month commitment for Provisioned Throughput

**5. Your company has been using Amazon Q as an internal chat assistant for a few weeks with positive results. There are a set number of users that does not change but you notice the daily charges are increasing steadily. What is the most likely cause?**
-  Users are adding documents to Amazon Q to create context for the Assistant

**6. Your company is developing AI/ML products and will be increasing their Amazon SageMaker usage consistently for the next few years. What is the least effort solution to reduce SageMaker cost?**
- Purchase SageMaker Savings Plans

