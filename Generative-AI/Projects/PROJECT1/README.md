#                                           PROJECT: LANGCHAIN MATH SOLVER AGENT 
# LangChain
## Definition 
---
> "Framework for developing applications powered by large language models (LLMs)."
## Process in LangChain
### 1. Development
*   Build your applications using its own open-source components
*  Allows third-party integrations.
### 2. Productionization
- Optimize your application for scalability, reliability, and robustness.
### 3. Deployment
- Launch and deploy your application to make it accessible to end-users

# LangGraph 
LangGraph is a tool used to build **stateful agents** with:
- First-class streaming support.
- Human-in-the-loop capabilities, enabling interactive workflows.

# Prerequisites
1. **Colab Signup**: Ensure Python 3.9+ is installed.
2. **LangChain Installed**: Install LangChain via pip:
```python
 pip install langchain
```
4. **Gemini Flash API Key**: Obtain an API key for the Google Gemini Flash model.
5. **OpenAI Client for Gemini Flash**: Install the Gemini Flash client or SDK:
```python
 pip install google-generativeai
```

## Step 1: Setup Environment 
Install Required Libraries
First, install the langchain_google_genai library:
```python
!pip install -qU langchain_google_genai
```
### Step 2: Import Required Modules
```python
from langchain_google_genai import ChatGoogleGenerativeAI
from google.colab import userdata
import os
```
### Step 3: Configure API Key and Gemini Flash Model 2.0
Use the Google API Key to authenticate and configure the ChatGoogleGenerativeAI model to answer user questions:
```python
api_key = userdata.get('GOOGLE_API_KEY')
model = ChatGoogleGenerativeAI(api_key=api_key, model="gemini-2.0-flash-exp")
```
### Step 4: Create a Prompt Template
Define a prompt template to restrict responses to math-related questions:
```python
from langchain.prompts import PromptTemplate
prompt_template = PromptTemplate(
    input_variables=["question"],
    template="I want you to answer only math related question and don't respond if question is from other subject:\n\n{question}"
)
```
### Step 5: Build the LangChain Pipeline
Combine the model and the prompt template into an LLM chain:
```python
from langchain.chains import LLMChain
chain = LLMChain(llm=model, prompt=prompt_template)
```
### Step 6: Run the Math Solver Agent 
Pass sample questions to chain to test its functionality:
#### Example 1: Math Question
```python
chain.invoke("tell me factorization of this equation: x^2+5x+6?")
```
#### Output
---
> {'question': 'tell me factorization of this equation: x^2+5x+6?',
 'text': '(x + 2)(x + 3)\n'}

#### Example 2: Non-Math Question/ Control System Question
```python
chain.invoke("What is Open Loop System?")
```
#### Output:
---
> {'question': 'What is Open Loop System?',
 'text': 'I cannot answer this question as it is not related to mathematics.\n'}
