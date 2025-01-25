![[streamlit.png]]
![[Pasted image 20250124113037.png]]

---
## [Section 1: AI Assistant we will build today]

![[streamlit-assistant-demo.mp4]]

## [Section 2: What is Streamlit?]

**Streamlit is an open-source Python framework that makes it easy to build interactive web applications.**

- No need for complex front-end coding—just write Python scripts!
- It’s perfect for data apps, dashboards, and AI assistants like the one we’re building today.

### Key Features of Streamlit:

1. **Interactive UI:** Build with Python, but interact like a modern web app.
2. **Live Reload:** Update apps instantly as you code.
3. **Widgets:** Use sliders, inputs, buttons, and even chat messages with simple function calls.

---
## [Section 3: Architecture Diagram of the AI Assistant]

![[Pasted image 20250125133844.png | 700]]

---
## [Section 4: Build the AI Assistant]

Let’s walk through the code step by step.

How to Install and Run First Python application using IntelliJ
![[Pasted image 20250124151949.png]]

How to install and run Open Source Large Language Models in your local Machine using Ollama
![[Pasted image 20250124152046.png]]


```python
import streamlit as st  
from langchain_ollama import ChatOllama  
from langchain.prompts import ChatPromptTemplate, MessagesPlaceholder  
from langchain_core.messages import HumanMessage, SystemMessage  
  
# set page title  
st.title("AI Assistant")  
  
# Sidebar  
model = st.sidebar.text_input(label="Enter Ollama model", value="llama3.1:latest")  
  
# Initialize state for chat messages  
if "messages" not in st.session_state:  
    st.session_state.messages = []  
  
if model:  
    # Display existing chat history  
    for message in st.session_state.messages:  
       with st.chat_message(message["role"]):  
          st.markdown(message["content"])  
            
    # Create chat chain  
    llm = ChatOllama(model=model)  
    prompt = ChatPromptTemplate.from_messages(  
       [  
          SystemMessage(content="You are a helpful assistant."),  
          MessagesPlaceholder(variable_name="history"),  
          HumanMessage(content="{user_query}")  
       ])  
    chain = prompt.pipe(llm)  
      
    # User input  
    if prompt := st.chat_input(placeholder="How can I help you today?"):  
       st.session_state.messages.append({"role": "user", "content": prompt})  
       with st.chat_message("user"):  
          st.markdown(prompt)  
      
    # Prepare chat history  
    history = [{"role": m["role"], "content": m["content"]} for m in st.session_state.messages]  
      
    # Stream the response  
    with st.chat_message("assistant"):  
       response_stream = chain.stream({"user_query": prompt, "history": history})  
       response = st.write_stream(response_stream)  
      
    # Append full response to messages  
    st.session_state.messages.append({"role": "assistant", "content": response})  
  
else:  
    st.info("Please enter an Ollama model name in the sidebar to continue.", icon="⚠")
```
---

**In windows Machine to activate virtual environment:**
*venv\Scripts\Activate*
If there is an error saying **UnauthorizedAccess**, execute the below command
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy Unrestricted -Force

---
## [Section 6: Conclusion & Next Steps]
Congratulations! 🎉 You just built your first AI Assistant using Streamlit and Ollama.

✅ Here’s what we covered:

- Streamlit basics.
- How to integrate Ollama open source models using LangChain.
- Building a conversational AI app with contextual chat history.

📌 **Next Steps:**

- Experiment with different Ollama models.
- Customize the assistant’s personality via `SystemMessage`.

🎥 Don’t forget to like, comment, and subscribe for more tutorials. See you in the next video! 👋