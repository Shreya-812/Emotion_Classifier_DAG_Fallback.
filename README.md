# Emotion Classifier with Confidence-Based Fallback (LangGraph + Hugging Face)

This project implements a self-correcting, real-time **text classification pipeline** using:

- A pre-trained transformer model from Hugging Face (`distilbert-base-uncased-emotion`)
- A simplified **LangGraph DAG** with internal fallback logic
- A command-line interface (CLI) that allows user input and override of low-confidence predictions

---

## 🧠 Project Objective

To build a **resilient classification system** that doesn't blindly trust predictions. When the model isn't confident enough (below 60%), it triggers a **user-driven fallback mechanism** asking for human intervention.

---

## 🔧 Technologies Used

- `transformers` by Hugging Face
- `langgraph` (lightweight workflow graph engine)
- `langchain-core` for runnable wrapping
- Python (tested in Google Colab and locally with Python 3.10+)

---

## 💡 How It Works

1. The user enters a sentence in the CLI.
2. The `inference_node` uses a pre-trained model to predict the emotion and confidence.
3. The `handle_confidence` node checks:
   - If confidence ≥ 60%, it proceeds with the model's result.
   - If confidence < 60%, it asks the user if they want to override.
4. Final prediction is printed along with whether fallback was used.

---

## 🔁 DAG Structure

