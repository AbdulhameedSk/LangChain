# LangChain – From Zero to Project (Absolute Beginner’s Guide)



## What Is LangChain?

**LangChain** is a tool (Python/JS library) that helps you build applications using language models like ChatGPT, Llama, etc.  
You use it to:
- Connect with different LLMs (OpenAI, Anthropic, local models…)
- Chain together steps (ask, remember, call API, answer)
- Add memory (so your bot remembers the conversation)
- Easily plug in tools (search, calculator, database, etc.)

## Prerequisites

- **Basic Python installed** ([get it here](https://python.org), if not already)
- **OpenAI API key** (or other LLM provider)—get from [platform.openai.com](https://platform.openai.com)

No experience with AI or coding? Copy the code snippets exactly; explanations are included.

## Step 1: Set Up Your Project

### 1.1. Make a New Folder
Open your terminal/command prompt and run:
```bash
mkdir langchain-demo
cd langchain-demo
```

### 1.2. Install Dependencies
Install the needed Python libraries:
```bash
pip install langchain openai python-dotenv
```

### 1.3. Save Your API Key Securely
Create a file named `.env` in your project folder, and put your OpenAI key in it:

```
OPENAI_API_KEY=your_actual_key_here
```

This is safer than hardcoding your key!

## Step 2: Build Your First Chatbot

Create a new file called `chatbot.py` and paste in this code (each line is explained below!):

```python
from langchain.llms import OpenAI
from langchain.memory import ConversationBufferMemory
from langchain.prompts import PromptTemplate
from dotenv import load_dotenv
import os

# Load environment variables (your API key)
load_dotenv()
api_key = os.getenv("OPENAI_API_KEY")

# Make an LLM (the AI "brain") using your OpenAI key
llm = OpenAI(openai_api_key=api_key)

# Keep conversation memory, so the bot remembers context
memory = ConversationBufferMemory()

# Set up how the prompt is presented to the LLM
prompt = PromptTemplate.from_template("You are a helpful assistant. {history} User: {input}")

while True:
    user_input = input("You: ")
    # Pass in user input & chat history to the AI
    response = llm(prompt.format(input=user_input, history=memory.buffer))
    memory.save_context({"input": user_input}, {"output": response})
    print("Bot:", response)
```

### Explanation:
- **Load API Key:** Securely pulls your OpenAI key from the `.env` file.
- **Create LLM object:** This is the interface to chat with GPT-3/4.
- **Set up Memory:** Saves the conversation so your bot *remembers* what you said before.
- **PromptTemplate:** Tells the LLM how to format things—here, it’s a simple Q&A style.
- **Main loop:** Asks for your input, sends it (and context) to OpenAI, prints the answer.

## Step 3: Run Your Bot

In your terminal:
```bash
python chatbot.py
```
Type things! Your bot should answer and remember your previous messages.

## What’s Next?

You’ve just built a **stateful, real LLM chatbot** using LangChain!

### Next Steps:
- **Customize prompt:** Make the assistant more chatty, or specialized (math tutor, travel agent, etc.).
- **Add tools:** Connect with web search, Wikipedia, or a calculator.
- **Retrieval-Augmented Generation (RAG):** Feed the model documents or files, so it can answer with your info.
- **Move to web/app:** Make it into a web service, Telegram bot, etc.

## Troubleshooting

- If something errors, check your API key and your internet.
- If you run out of OpenAI free credits, use another key/provider.

## Summary

- **LangChain** gives you “cheat codes” for building powerful AI apps, quickly.
- **Scales from very simple (like this chatbot) to super advanced (multi-step, multi-tool apps).**
- You don’t need deep AI knowledge—just curiosity and willingness to try!

Use this as your beginner README for LangChain. When you’re ready, check out the official docs for **chains, agents, tools, and memory** to level up your AI building even more!

Refer to RAG + LangChain in Chat_with_PDF repo