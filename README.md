# Mindflow Mindsdb
This repo consists of MindsDB code that I used for my Mindflow chrome extension. 

## Chat Section
<br>
For the chat section I created the following model

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
