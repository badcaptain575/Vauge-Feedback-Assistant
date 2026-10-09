# Vague Feedback Assistant 

**Technical Note:** The n8n execution engine for this pipeline is hosted locally to protect client data and eliminate API waste. While the workflow itself is not publicly live, the Live Project Link provided in the submission directs to the real-time Google Sheets dashboard tracking the system's live outputs.

## The Problem
In creative agencies, design review cycles are frequently bottlenecked by vague client feedback (e.g., "make it pop", "make it more premium"). Translating these subjective comments into actionable design tasks requires multiple manual clarification cycles, draining hours of project management and design time.

## The Solution
The Vague Feedback Assistant is a deterministic control graph built in n8n. It intercepts unstructured client feedback in Slack, analyzes the design draft using GPT-4o Vision, and instantly replies in the thread with structured, actionable multiple-choice visual questions. 

## System Architecture
1. **Trigger & Polling:** A Schedule Trigger polls the centralized Slack channel every 60 seconds, using Unix timestamp filtering to isolate only net-new replies without relying on fragile webhooks.
2. **Context Aggregation:** The system checks if the message is a threaded reply. If true, it extracts the full conversation history to ensure the AI retains multi-turn context without hallucinating past design choices.
3. **AI Vision Analysis:** OpenAI's GPT-4o evaluates the specific attached image against the thread transcript. Using strict Chain-of-Thought prompting, the LLM outputs exactly three targeted multiple-choice questions regarding specific visual elements (colors, typography, layout).
4. **Data Logging:** A Google Sheets OAuth integration appends the interaction—capturing the timestamp, client name, draft image URL, raw feedback, and the generated AI questions—into a live centralized dashboard to track time saved and ROI.

## Repository Contents
* "Vauge Feedback Assistant.json" : The complete n8n workflow export. 

## How to View the Workflow
1. Download the "Vauge Feedback Assistant.json" file.
2. Open your local or cloud instance of n8n.
3. Go to your workflows dashboard, click **Import from File**, and select the JSON.
4. Update the OAuth credentials for Slack, OpenAI, and Google Sheets to run the pipeline.
