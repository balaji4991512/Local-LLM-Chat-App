**Chat with Local AI Models using Streamlit, Ollama, and LlamaIndex
**
This project is a real-time chatbot built with:

- Streamlit — for the interactive web UI
- Ollama — to run local LLMs like Llama3, Mistral, or Phi3
- LlamaIndex — to abstract prompts and enhance LLM interaction

100% local and offline — No API keys required. Your data stays on your machine.



⸻

🚀 Features
	•	🔁 Real-time chat with response streaming
	•	🧠 Choose between multiple LLMs: Llama3, Phi3, Mistral7B
	•	🎛 Sidebar model selector
	•	🐛 Logging built-in for monitoring/debugging
	•	🔌 Easily extendable with document loaders, vector search, or RAG

⸻

📸 Screenshot

(Optional: Replace with your real screenshot image)


⸻

📦 Requirements
	•	Python 3.9 or higher
	•	Ollama installed and running (ollama serve)
	•	Supported model pulled (e.g., ollama pull llama3)
	•	macOS users: llama-index-llms-ollama is required

⸻

🛠️ Installation & Setup

1. Clone the Repository

git clone https://github.com/your-username/llm-chat-app.git
cd llm-chat-app

2. Create a Virtual Environment

python3 -m venv venv_llm_chatapp
source venv_llm_chatapp/bin/activate

3. Install Python Dependencies

pip install -r requirements.txt

Or manually:

pip install streamlit llama-index llama-index-llms-ollama

4. Pull a Model with Ollama

Make sure Ollama is installed and running. Then:

ollama pull llama3  # or mistral, phi3, etc.



⸻

▶️ Running the App

streamlit run ollama-streamlit-app.py

Then open http://localhost:8501 in your browser.

⸻

💬 Usage Guide
	1.	Choose a model from the sidebar (e.g., Llama3, Phi3, Mistral)
	2.	Type your question in the chat box
	3.	View the real-time streamed response from the selected model

⸻

🧠 How It Works
	•	ollama-streamlit-app.py handles the full UI + backend
	•	Uses llama_index.llms.ollama.Ollama for connecting to local LLMs
	•	Chat history is tracked using st.session_state
	•	Supports streaming responses and error logging

⸻

🧪 Example Interaction
	1.	User selects Llama3
	2.	User asks: “What is the capital of France?”
	3.	Response: “The capital of France is Paris.”

⸻

📁 Project Structure

llm-chat-app/
├── ollama-streamlit-app.py       # Main app file
├── requirements.txt              # Python dependencies
├── README.md                     # You're here!
├── chat-interface-app.png        # (Optional) UI screenshot
└── venv_llm_chatapp/             # Your virtual environment (excluded in .gitignore)



⸻

🤝 Contributing

Contributions are welcome!
Feel free to open issues, submit PRs, or suggest features.

⸻

📃 License

This project is open-source and available under the MIT License.

⸻

🙏 Acknowledgements
	•	Streamlit
	•	Ollama
	•	LlamaIndex
