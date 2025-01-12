# Langchain Function Tool Calling

This project demonstrates the integration of LangChain with Google Gemini's Generative AI model for building tool-based interactions, including custom mathematical operations.

## Features

- **Integration with Google Gemini API**: Utilizes the `gemini-2.0-flash-exp` model with LangChain.
- **Custom Tools**: Includes examples of custom tools for mathematical operations:
  - Annual Return Calculation
  - Addition
  - Multiplication
- **Dynamic Tool Binding**: Illustrates how to bind tools dynamically and use them in conversational AI.

## Prerequisites

1. Python 3.8 or higher.
2. Required libraries:
   - `langchain-google-genai`
   - `langchain-core`


# Setup
 + Ensure your GEMINI_API_KEY is securely stored in the environment and accessible using:
```python
from google.colab import userdata
GEMINI_API_KEY = userdata.get('GEMINI_API_KEY')
```
# Usage
 + Import and initialize the Google Gemini model:
```python
from langchain_google_genai import ChatGoogleGenerativeAI
llm = ChatGoogleGenerativeAI(
    api_key=GEMINI_API_KEY,
    model="gemini-2.0-flash-exp",
)
```
+ Define and use custom tools:
```python
@tool
def annual_return(a: int):
    return (a + 15) / 5 + 3
```
+ Bind tools and invoke them with questions:
```python
llm_with_tools = llm.bind_tools([annual_return, add, multiply])
question = "What is the annual return of 10?"
ai_msg = llm_with_tools.invoke([HumanMessage(content=question)])
print(ai_msg)
```
# Examples
### Example 1: Annual Return Calculation
```python
@tool
def annual_return(a: int):
    return (a + 15) / 5 + 3
```
```
Input: 10
Output: Annual return = 8.0
```

### Example 2: Tool Binding
```python
tools = [annual_return, add, multiply]
llm_with_tools = llm.bind_tools(tools)
```

### Example 3: Full Interaction
```python
messages = [HumanMessage(content="What is the annual return of 10?")]
ai_msg = llm_with_tools.invoke(messages)
print(ai_msg.tool_calls)
```
## `Contribution`
`Feel free to contribute by forking the repository, making updates, and creating pull requests.`