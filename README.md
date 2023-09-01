# Mindsdb
[MindFlow](https://github.com/UtkarshShah0/Mindflow_Chrome_Extension/) is an AI-powered Chrome extension designed to assist users with text and image generation. __MindsDB__ is a key component that enhances MindFlow's text generation capabilities.<br>

[MindsDB](https://mindsdb.com/) empowers organizations to harness the power of AI by abstracting `AI models` as `Generative AI Tables`. These tables are capable of learning from the input data and generating predictions from the underlying model upon being queried. This abstraction makes AI highly accessible, enabling development teams to use their existing SQL skills to build applications powered by AI.<br>
MindsDB bridges the gap between AI and data by integrating data sources and ML engines.<br>

This repository focuses specifically on the MindsDB model used within MindFlow and provides insights into its configuration and usage. <br>
<br>

## Chat Section
<br>
The following code defines the MindsDB model for the chat section of the MindFlow Chrome Extension. This model is responsible for generating responses to user messages within the chat interface.
<br>
<br>

```
CREATE MODEL mindsdb.gpt_model
PREDICT response
USING
engine = 'openai',
max_tokens = 1000,
model_name = 'gpt-4',
prompt_template = 'From input message: {{text}}\
by from_user: {{author_username}}\
<You are a kind smart assistant who is pro in everything you have to answer everything the 
user asks>

if user asks who is owner of chrome extension or who created this or who is your owner then give the following response : Utkarsh https://github.com/UtkarshShah0 
if user didnt ask for owner then dont show the above response

<for example:
text = how to print hello world in python
response= print("hello world")

text = owner or who created you
response = Utkarsh https://github.com/UtkarshShah0>

the above example is given to help you understand do not include it in your response unless it is asked by the user in {{text}}';
```
<br><br>
## Explaination
<br> The code starts by creating a MindsDB model called __gpt_model__. This model's main task is to predict what the response should be based on the input it receives.<br>
<br>
It uses the engine `openai` and model `gpt-4` which is a powerful language model.<br>

The code also sets some limitations. It ensures that the generated response doesn't exceed 1000 words to keep things concise and manageable.<br>

The `prompt_template` part is like an introduction for the model. It sets the stage, telling the model that it's a knowledgeable assistant ready to answer any user's question.

Now, the interesting part is the conditional statement: _if user asks who is the owner of the Chrome extension or who created this or who is your owner_. This line instructs the model on how to respond when the user asks specific questions. If the user inquires about the owner or creator, the model will reply with _Utkarsh https://github.com/UtkarshShah0._

For example, if a user asks, "Who is the owner?" or "Who created you?" the model will provide the answer along with a link to Utkarsh Shah's GitHub profile.

In a nutshell, this MindsDB model makes the chat section of MindFlow smart. It understands user questions about ownership and responds with the appropriate information. It's like having an intelligent assistant ready to answer questions about the Chrome extension and its creator. <br>
<br>

## Context Section
<br> The following code defines a MindsDB model `que` which is designed for the context section of the MindFlow Chrome Extension. This model is built to provide specific answers within a given context, and it does so by understanding both the question and the context it's asked in. <br>

```
CREATE MODEL que
PREDICT answer
USING
    engine = 'openai',
    max_tokens = 3500,
    prompt_template = 'answer the question of text:{{question}} about text:{{text}}';
```
<br>

## Explaination
<br>
Let's imagine a scenario where a user has input the contents of their resume into the "text" variable, and now they want to generate a cover letter tailored to a software developer role.

- **Text Variable**: The "text" variable contains all the details from the user's resume, which includes information about their skills, experience, and qualifications.

- **Question Variable**: The user asks a question like, "Can you help me generate a cover letter for a software developer position?"

Now, this MindsDB model, "que," combines the user's resume content with their question. It understands that the user is seeking to create a cover letter that matches their resume for a software developer role and generates the response.

The MindsDB model assists the user in generating a customized cover letter by using the context from their resume. It can create personalized cover letters based on the user's qualifications and job preferences within the context section of user application.<br>
<br>
## Image Section
<br> The _image_ section is a feature that allows users to request the generation of images based on specific descriptions or prompts they provide. The model named `mindsdb.gpt_image_3` is designed to assist with generating the images using the power of the OpenAI GPT-4 engine. <br>
<br>
```
CREATE MODEL mindsdb.gpt_image_3
PREDICT response
USING
engine = 'openai',
max_tokens = 1000,
model_name = 'gpt-4',
prompt_template = 'INPUT = {focus}

OUTPUT = {description} \n https://image.pollinations.ai/prompt/{description}

{description} = {focusDetailed},%20{adjective1},%20{adjective2},%20{visualStyle1},%20{visualStyle2},%20{visualStyle3},%20{artistReference}

INPUT = a photo of a cat

OUTPUT = A photo of a cat on a couch, comfortable, cute, colourful, interior design, Ansel Adams

https://image.pollinations.ai/prompt/a%20photo%20of%20a%20cat%20on%20a%20couch,%20comfortable,%20cute,%20colourful,%20interior%20photograph,%20interior design,%20Ansel Adams

INPUT = Fox with a cloak

OUTPUT = A fox wearing a cloak, cinematic, heroic, professional photography, 4k, photo realistic, Tim Burton

https://image.pollinations.ai/prompt/A%20fox%20wearing%20a%20cloak,%20cinematic,%20heroic,%20professional%20photography,%204k,%20photo%20realistic,%20Tim%20Burton

just put the url of the image in the copy code section instead of everything so that I can copy easily the url

remove the quotes from the above urls

Only give url in response

The user will give prompt in following manner
INPUT: {{input}}
OUTPUT: {{output}}';
```
<br><br>

## Explaination
