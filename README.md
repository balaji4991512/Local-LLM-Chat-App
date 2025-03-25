# Chat with AI Models Using Streamlit, Ollama, and LlamaIndex (macOS)


<img width="1491" alt="Screenshot 2025-03-25 at 7 25 58 AM" src="https://github.com/user-attachments/assets/87bc04db-3860-432d-8a52-f33f04297b98" />


This repository contains the code for a chat application specifically designed for **macOS**, leveraging **Streamlit**, **Ollama**, and **LlamaIndex** to interact with users in real time. The app allows users to select from multiple local AI models and receive streaming responses instantly — all while keeping your data local and private. The application is optimized to run smoothly in **VS Code**.

## Features

- Real-time chat interface using Streamlit.
- Integration with Ollama LLMs via LlamaIndex.
- Sidebar model selection (supports Llama3, Phi3, and Mistral7B).
- Local-first: No API keys or cloud dependency.
- Streaming responses and session-managed chat history.
- Logging for debugging and monitoring.

## Requirements

- macOS operating system.
- Python 3.9 or higher.
- Ollama installed and running ([Ollama Website](https://ollama.com)).
- Streamlit.
- LlamaIndex with Ollama integration (`llama-index-llms-ollama`).
- VS Code (recommended IDE).

## Installation & Setup

### 1. Clone the Repository

Open VS Code terminal:

```bash
git clone https://github.com/balaji4991512/Local-LLM-Chat-App
cd Local-LLM-Chat-App
code .
```

### 2. Create a Virtual Environment

In the VS Code terminal, run:

```bash
python3 -m venv venv_llm_chatapp
```

### 3. Activate the Virtual Environment

In the VS Code terminal, activate your virtual environment:

```bash
source venv_llm_chatapp/bin/activate
```

### 4. Install Python Dependencies

Install from `requirements.txt` in VS Code terminal:

```bash
pip install -r requirements.txt
```

*Or install manually:*

```bash
pip install streamlit llama-index llama-index-llms-ollama
```

### 5. Pull a Model Using Ollama

Make sure Ollama is installed and running, then pull the desired model from the VS Code terminal:

```bash
ollama pull llama3
```

*You can also pull other models like `mistral` or `phi3` if needed.*

### 6. Run the Application

In VS Code terminal, run:

```bash
streamlit run ollama-streamlit-app.py
```

This will direct the browser to open the app.

## Usage

1. Open your web browser and navigate to the redirected link.
2. Select a model from the sidebar (e.g., Llama3, Phi3, or Mistral7B).
3. Enter your question in the chat input box and press Enter.
4. The app streams the selected model's response back to you in real time.

## Code Overview

- **Initialization:** Sets up logging and initializes chat history in `st.session_state`.
- **Model Selection:** Sidebar allows users to choose from supported LLMs (Llama3, Phi3, Mistral7B).
- **Chat Input:** Captures user messages and appends them to the chat state.
- **Streaming Responses:** Uses `llama_index.llms.ollama.Ollama` for connecting to local LLMs and streaming responses.
- **Error Handling:** Catches exceptions and logs errors, displaying user-friendly messages in the UI.

## Example Interaction

1. **User selects:** `"Llama3"` from the sidebar.
2. **User asks:** "What is the PM of India?"
3. **Response:** "TAs of my knowledge cutoff, the Prime Minister of India is Narendra Modi. He has been serving as the 15th and current Prime Minister of India since May 26, 2014."

## Project Structure

```
llm-chat-app/
├── ollama-streamlit-app.py       # Main app file
├── requirements.txt              # Python dependencies
├── README.md                     # This file
├── code_explanation.md           # Explanation of the main code
├── chat-interface-app.png        # (Optional) UI screenshot
```

## Contributing

Contributions are welcome! Feel free to open issues, suggest improvements, or submit a pull request.

## License

This project is open-sourced.

## Acknowledgements

This project uses the following libraries:

- [Streamlit](https://streamlit.io/)
- [Ollama](https://ollama.com/)
- [LlamaIndex](https://www.llamaindex.ai/)

Feel free to reach out if you have any questions or need further assistance. Happy coding!

