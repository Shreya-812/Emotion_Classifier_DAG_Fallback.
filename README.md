# Emotion Classifier with Confidence-Based Fallback (LangGraph + Hugging Face)

This project implements a self-correcting, real-time **text classification pipeline** using:

- A pre-trained transformer model from Hugging Face (`distilbert-base-uncased-emotion`)
- A simplified **LangGraph DAG** with internal fallback logic
- A command-line interface (CLI) that allows user input and override of low-confidence predictions

---

##  Project Objective

To build a **resilient classification system** that doesn't blindly trust predictions. When the model isn't confident enough (below 60%), it triggers a **user-driven fallback mechanism** asking for human intervention.

---

##  Technologies Used

- `transformers` by Hugging Face
- `langgraph` (lightweight workflow graph engine)
- `langchain-core` for runnable wrapping
- Python (tested in Google Colab and locally with Python 3.10+)

---

##  How It Works

1. The user enters a sentence in the CLI.
2. The `inference_node` uses a pre-trained model to predict the emotion and confidence.
3. The `handle_confidence` node checks:
   - If confidence ≥ 60%, it proceeds with the model's result.
   - If confidence < 60%, it asks the user if they want to override.
4. Final prediction is printed along with whether fallback was used.

---

## DAG Structure

[input] → [inference_node] → [handle_confidence] → [END]

This avoids complex routing logic and uses a **self-contained fallback system** inside a single node.

---

## How to Run

### 1. Install Dependencies

```bash
pip install transformers datasets langchain langgraph
2. Run the Script / Notebook
You can run the .ipynb file in Google Colab or Jupyter

OR convert to .py and run locally

3. Sample CLI Output
vbnet
Copy
Edit
Enter input (or 'exit'): I feel terrible about everything today.
[INFER] 'I feel terrible about everything today.' → sadness (0.57)
[CHECK] Low confidence: 0.57
[FALLBACK] Prediction: sadness
Do you want to override it? (y/n): y
Enter correct label: fear
[RESULT] Final Label: fear | Fallback used: True
Customization
You can fine-tune the emotion model or replace it with any text-classification model

Confidence threshold is customizable in handle_confidence node

Logs can be expanded to persist prediction history

Files Included
Emotion_Classifier_Fallback_Simplified.ipynb — core notebook with CLI and DAG

README.md — project overview and usage instructions

(Optional) Exported .py modules for packaging

Credits
Developed by Shreya Singh with support from Hugging Face and LangGraph libraries.

