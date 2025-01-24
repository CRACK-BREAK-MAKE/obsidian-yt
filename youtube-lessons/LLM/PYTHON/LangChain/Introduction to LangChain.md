  ![[Pasted image 20250124113037.png]]

---

### **Why LangChain?**

💡 _"LangChain simplifies how we use AI models by organizing all the pieces needed to create intelligent applications. It’s like a toolbox that helps you combine AI, memory, and tools seamlessly."_

---

### **Architecture**

🏗️ _"LangChain organizes its ecosystem into different packages like chat models, tools, memory, and retrievers. Each package focuses on solving a specific problem, and they all work together to power your app."_

The LangChain framework consists of multiple open-source libraries like -
**langchain-core:** Base abstractions for chat models and other components.

**langchain:** Chains, agents, and retrieval strategies that make up an application's cognitive architecture.

**langchain-community:** Third-party integrations that are community maintained.

**langgraph:** Orchestration framework for combining LangChain components into production-ready applications with persistence, streaming, and other key features.

---

### **Chat Models**

🗨️ _"These are AI models that work like chatbots. They take a series of messages as input and give you a response as a message."_

---

### **Messages**

✉️ _"Messages are the building blocks of communication in LangChain – like sending texts back and forth. They represent both what you say to the AI and what the AI responds with."_

---

### **Chat History**

🕰️ _"Chat history is just a record of your conversation, stored as a sequence of messages. It helps the AI understand the context of what you’re talking about."_

---

### **Structured Output**

📋 _"Sometimes, you want the AI to respond in a specific format, like JSON. LangChain makes it easy to create these structured outputs so the data is well-organized."_

---

### **Memory**

🧠 _"Memory lets the AI remember things you’ve said before so it can use that knowledge later. This makes conversations feel more natural and connected."_

---

### **Runnable Interface**

🚀 _"This is the backbone of LangChain – it connects all the parts together so you can build workflows like plugging in LEGO blocks."_

---

### **Streaming**

🌊 _"Streaming allows LangChain to show responses in real-time, piece by piece, instead of waiting for the entire answer to be ready."_

---

### **LangChain Expression Language (LCEL)**

📜 _"LCEL is a simple syntax for chaining LangChain components together. Think of it as writing recipes for AI workflows."_

---
And many more like ...
### **Document Loaders**, **Text Splitters**, **Embedding Models**, **Vector Stores**, **Retriever** etc.

---


**[Example Setup]**

  ```mermaid 
graph TD
A[Start Program] --> B[Initialize LLM]
B --> C[Define Prompt Template]
C --> E[Combine Prompt and LLM into Base Chain]
E --> F[Wait for User Input]
F --> G{User Input?}
G -->|Yes| H[Invoke Base Chain with User Input]
G -->|No Exit| I[End Program]
H --> J[Generate Response from LLM]
J --> F[Wait for Next Input]
```

How to Install and Run First Python application using IntelliJ
![[Pasted image 20250124151949.png]]

How to install and run Open Source Large Language Models in your local Machine using Ollama
![[Pasted image 20250124152046.png]]

```python

from langchain.prompts import ChatPromptTemplate, SystemMessagePromptTemplate, HumanMessagePromptTemplate, MessagesPlaceholder  
from langchain_ollama import ChatOllama  
  
FORMAT_MARKDOWN_PROMPT = """You are a helpful assistant. Please respond to the user's query in Markdown format."""  
  
def main():  
    # Step 1: Initialize the LLM  
    llm = ChatOllama(model="llama3.1:latest")  
      
    # Step 2: Create the prompt template  
    prompt = ChatPromptTemplate.from_messages([  
       SystemMessagePromptTemplate.from_template(FORMAT_MARKDOWN_PROMPT),  
       HumanMessagePromptTemplate.from_template("{user_query}")  
    ])  
      
    # Step 3: Combine the prompt with the LLM into a base chain  
    base_chain = prompt.pipe(llm)  
      
    while True:  
       # Step 4: Take user input  
       user_query = input("You: ")  
         
       if user_query.lower() in ['exit', 'quit', 'bye']:  
          print("Exiting. Goodbye!")  
          break  
       # Step 5: Invoke the chain with user input  
       response = base_chain.invoke({"user_query": user_query})  
         
       # Step 6: Print the response  
       print(f"Assistant: {response.content}")  
  
if __name__ == "__main__":  
    main()

```
