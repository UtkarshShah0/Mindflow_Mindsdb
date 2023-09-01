# Mindflow Mindsdb
[MindFlow](https://github.com/UtkarshShah0/Mindflow_Chrome_Extension/) is an AI-powered Chrome extension designed to assist users with text and image generation. MindsDB is a key component that enhances MindFlow's text generation capabilities.

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
<br>
For the context section I created the following model <br>

```
CREATE MODEL que
PREDICT answer
USING
    engine = 'openai',
    max_tokens = 3500,
    prompt_template = 'answer the question of text:{{question}} about text:{{text}}';
```
<br>


## Image Section
<br>
For the image section, I created the following model <br>

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
