# Deep Research Agent

An autonomous multi-agent research system powered by the **OpenAI Agents SDK**. Given any topic or query, it plans web searches, gathers information from the internet, synthesizes a detailed markdown report, and delivers it to your inbox — all automatically.

---

## Demo

<!-- Replace the block below with your screen recording video (e.g., a GIF, YouTube embed, or video file link) -->

> 📹 **Screen Recording coming soon...**
>
> <!-- To embed a YouTube video, use: -->
> <!-- [![Deep Research Demo](https://img.youtube.com/vi/YOUR_VIDEO_ID/0.jpg)](https://www.youtube.com/watch?v=YOUR_VIDEO_ID) -->
>
> <!-- To embed a GIF or local video file, use: -->
> <!-- ![Demo](assets/demo.gif) -->

---

## How It Works

The system orchestrates **4 specialized AI agents** in a pipeline:

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
│  Search Agent   │  ──► Executes all searches in parallel & summarizes results
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

Each step streams a status update to the Gradio UI in real time.

---

## Project Structure

```
deep_research/
├── deep_research.py       # Gradio UI entry point
├── research_manager.py    # Orchestrates the full research pipeline
├── planner_agent.py       # Plans web search queries from the user's topic
├── search_agent.py        # Searches the web and summarizes results
├── writer_agent.py        # Writes the final detailed markdown report
└── email_agent.py         # Formats and sends the report via SendGrid
```

---

## Prerequisites

- Python 3.11+
- An [OpenAI API key](https://platform.openai.com/api-keys)
- A [SendGrid API key](https://sendgrid.com/) with a verified sender email

---

## Setup

1. **Clone the repository**

   ```bash
   git clone <your-repo-url>
   cd deep_research
   ```

2. **Install dependencies**

   ```bash
   pip install openai-agents gradio python-dotenv sendgrid
   ```

3. **Configure environment variables**

   Create a `.env` file in the project root:

   ```env
   OPENAI_API_KEY=your_openai_api_key_here
   SENDGRID_API_KEY=your_sendgrid_api_key_here
   ```

4. **Update email addresses** in `email_agent.py`

   ```python
   from_email = Email("your_verified_sender@example.com")
   to_email   = To("your_recipient@example.com")
   ```

---

## Usage

```bash
python deep_research.py
```

The Gradio UI will open in your browser automatically. Enter any research topic and click **Run**.

---

## Features

- **Parallel search execution** — all web searches run concurrently for speed
- **OpenAI Traces** — every run is linked to a trace on the [OpenAI platform](https://platform.openai.com/traces)
- **Structured outputs** — agents use Pydantic models for reliable, typed responses
- **Email delivery** — the finished report lands in your inbox as clean HTML
- **Streaming UI** — live status updates via Gradio while the pipeline runs

---

## Models Used

| Agent         | Model       |
| ------------- | ----------- |
| Planner Agent | gpt-4o-mini |
| Search Agent  | gpt-4o-mini |
| Writer Agent  | gpt-4o-mini |
| Email Agent   | gpt-4o-mini |

---

## License

This project is for educational purposes as part of the **AI Engineer Agentic Track** course.
