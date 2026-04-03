# Deep Research Agent

An autonomous multi-agent research system powered by OpenAI that takes a user query, plans and executes web searches, synthesizes a detailed markdown report, and delivers it via email — all through a clean Gradio UI.

---

## Demo


> **Screen Recording**
>
> [![Deep Research Demo](https://via.placeholder.com/800x450?text=Click+to+Watch+Demo)](https://github.com/user-attachments/assets/b67b5dd0-6a72-4742-81fe-a9fdee7fad91)
>




---

## How It Works

The system is orchestrated by the `ResearchManager` which coordinates four specialized agents in a pipeline:

```
User Query
    │
    ▼
┌─────────────────┐
│  Planner Agent  │  ──► Generates 5 targeted web search queries
└─────────────────┘
    │
    ▼
┌─────────────────┐
│  Search Agent   │  ──► Executes searches concurrently & summarizes results
└─────────────────┘
    │
    ▼
┌─────────────────┐
│  Writer Agent   │  ──► Synthesizes a detailed 1000+ word markdown report
└─────────────────┘
    │
    ▼
┌─────────────────┐
│  Email Agent    │  ──► Sends the formatted report as an HTML email via SendGrid
└─────────────────┘
```

---

## Project Structure

```
deep_research/
├── deep_research.py       # Gradio UI entry point
├── research_manager.py    # Orchestrates the full research pipeline
├── planner_agent.py       # Plans web searches from the user query
├── search_agent.py        # Executes individual web searches
├── writer_agent.py        # Writes the final structured report
└── email_agent.py         # Sends the report via SendGrid email
```

---

## Agents

| Agent             | Model       | Role                                                      |
| ----------------- | ----------- | --------------------------------------------------------- |
| **Planner Agent** | gpt-4o-mini | Breaks the query into 5 focused web search terms          |
| **Search Agent**  | gpt-4o-mini | Searches the web and summarizes results (≤300 words each) |
| **Writer Agent**  | gpt-4o-mini | Produces a cohesive 1000+ word markdown report            |
| **Email Agent**   | gpt-4o-mini | Converts the report to HTML and sends it via SendGrid     |

---

## Prerequisites

- Python 3.11+
- An [OpenAI API key](https://platform.openai.com/api-keys)
- A [SendGrid API key](https://sendgrid.com/) with a verified sender email

---

## Installation

```bash
# Clone the repository
git clone <your-repo-url>
cd deep_research

# Create and activate a virtual environment
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # macOS/Linux

# Install dependencies
pip install openai-agents gradio python-dotenv sendgrid
```

---

## Configuration

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=your_openai_api_key_here
SENDGRID_API_KEY=your_sendgrid_api_key_here
```

Update the sender and recipient email addresses in `email_agent.py`:

```python
from_email = Email("your-verified-sender@example.com")
to_email   = To("your-recipient@example.com")
```

---

## Usage

```bash
python deep_research.py
```

The Gradio UI will open in your browser. Enter any research topic and click **Run**. The app will:

1. Display real-time status updates as each stage completes
2. Render the final markdown report in the UI
3. Send the full HTML report to the configured email address
4. Print an OpenAI trace URL to the terminal for debugging

---

## Tracing

Every run generates an OpenAI trace. The trace URL is printed to the terminal and yielded as the first status message in the UI:

```
View trace: https://platform.openai.com/traces/trace?trace_id=<id>
```

---

## License

This project is for educational purposes as part of the **AI Engineer Agentic Track — The Complete Agent & MCP Course**.
