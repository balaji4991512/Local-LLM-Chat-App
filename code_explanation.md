# Code Explanation for `ollama-streamlit-app.py`

Below is a detailed breakdown of how the Streamlit application works, line by line:

---

## Imports

```python
import streamlit as st
from llama_index.core.llms import ChatMessage
import logging
import time
from llama_index.llms.ollama import Ollama
```

1. **`streamlit`** – provides functions and UI components to build the interactive web app.
2. **`ChatMessage`** – a data structure that represents a single conversation message (role + content).
3. **`logging`** – Python’s logging library for info, warning, and error logs.
4. **`time`** – used for measuring response generation duration.
5. **`Ollama`** – the local LLM class from LlamaIndex, enabling real-time streaming of model outputs.

---

## Logging and Session State

```python
logging.basicConfig(level=logging.INFO)

if 'messages' not in st.session_state:
    st.session_state.messages = []
```

- **`logging.basicConfig(level=logging.INFO)`** sets the log level to INFO.
- **`st.session_state.messages`** – stores chat messages so they persist across user actions (like pressing Enter).

---

## The `stream_chat` Function

```python
def stream_chat(model, messages):
    try:
        llm = Ollama(model=model, request_timeout=120.0)
        resp = llm.stream_chat(messages)
        response = ""
        response_placeholder = st.empty()

        for r in resp:
            response += r.delta
            response_placeholder.write(response)

        logging.info(f"Model: {model}, Messages: {messages}, Response: {response}")
        return response
    except Exception as e:
        logging.error(f"Error during streaming: {str(e)}")
        raise e
```

### How It Works
1. **Initialize Ollama** – The `Ollama` instance is created with a specified `model` and a `request_timeout`.
2. **Streamed Response** – `resp = llm.stream_chat(messages)` returns chunks of text as they are generated.
3. **UI Updates** – A `response_placeholder` is used to display partial results in real time.
4. **Logging** – The final response is logged, including the user’s messages and the selected model.
5. **Error Handling** – Logs errors and re-raises them to be handled by the caller.

---

## The `main` Function

```python
def main():
    st.title("Chat with LLMs Models")
    logging.info("App started")

    model = st.sidebar.selectbox("Choose a model", ["llama3", "phi3", "mistral"])
    logging.info(f"Model selected: {model}")

    if prompt := st.chat_input("Your question"):
        st.session_state.messages.append({"role": "user", "content": prompt})
        logging.info(f"User input: {prompt}")

        for message in st.session_state.messages:
            with st.chat_message(message["role"]):
                st.write(message["content"])

        if st.session_state.messages[-1]["role"] != "assistant":
            with st.chat_message("assistant"):
                start_time = time.time()
                logging.info("Generating response")

                with st.spinner("Writing..."):
                    try:
                        messages = [ChatMessage(role=msg["role"], content=msg["content"]) for msg in st.session_state.messages]
                        response_message = stream_chat(model, messages)
                        duration = time.time() - start_time
                        response_message_with_duration = f"{response_message}\n\nDuration: {duration:.2f} seconds"

                        st.session_state.messages.append({"role": "assistant", "content": response_message_with_duration})

                        st.write(f"Duration: {duration:.2f} seconds")
                        logging.info(f"Response: {response_message}, Duration: {duration:.2f} s")

                    except Exception as e:
                        st.session_state.messages.append({"role": "assistant", "content": str(e)})
                        st.error("An error occurred while generating the response.")
                        logging.error(f"Error: {str(e)}")
```

### Step-by-Step Explanation

1. **Streamlit Title** – `st.title("Chat with LLMs Models")` sets the page title.
2. **Model Selection** – A **sidebar** dropdown lets users pick the model: `llama3`, `phi3`, or `mistral`.
3. **User Input** – `st.chat_input("Your question")` creates a chat-like input field.
   - If the user types a question, it’s appended to `st.session_state.messages` with the role `"user"`.
4. **Displaying Existing Messages** – We loop through `st.session_state.messages` and display them using `st.chat_message(...)`.
5. **Generating Assistant Response** – If the last message is from the user, we generate a response:
   - We log "Generating response".
   - Inside `st.spinner("Writing...")`, we:
     1. Convert each message to `ChatMessage` objects.
     2. Call `stream_chat(model, messages)` to get the streamed response from the chosen model.
     3. Measure how long the LLM took.
     4. Append the assistant’s answer to the session state with role `"assistant"`.
6. **Error Handling** – Any exception is logged and shown in the UI with `st.error(...)`.

---

## `if __name__ == "__main__":`

```python
if __name__ == "__main__":
    main()
```

- Ensures that `main()` is run only when this script is **executed directly**, not imported.

---

## Summary

- **Session State** keeps track of the conversation (user + assistant messages).
- **`stream_chat`** function streams partial responses from the Ollama model in real time, updating the UI.
- **Logging** is used extensively for debugging and performance monitoring.
- **Timing** calculations show how long the LLM took to produce its answer.
- **Error Handling** and UI feedback ensure users see a friendly message if something goes wrong.

This design makes for a powerful, local-first chatbot where all data and computations reside on your machine (through Ollama). Integrating it with Streamlit provides a user-friendly way to interact with different LLM models, all within a single, self-contained web interface.

