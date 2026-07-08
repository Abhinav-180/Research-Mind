# 🔬 ResearchMind

**Streamlit App**

An intelligent multi-agent research assistant that searches the web, reads source pages, writes structured reports, and critiques the final output — powered by LangChain, Tavily, and Mistral AI / OpenRouter.

🌐 **[Live Demo → research-mind-4vcvgdnejo6x6mrqnjcfuf.streamlit.app](https://research-mind-4vcvgdnejo6x6mrqnjcfuf.streamlit.app)**

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔍 Web Search Agent | Finds recent and relevant information using Tavily Search API |
| 📄 Reader Agent | Selects the most useful source and scrapes deeper page content via BeautifulSoup |
| ✍️ Research Writer | Generates a structured report with introduction, key findings, conclusion, and sources |
| 🧐 Critic Chain | Reviews the generated report and gives a quality score with improvement suggestions |
| 🎨 Streamlit UI | Beautiful dark-mode web interface with step-by-step pipeline visualization |
| 💻 CLI Pipeline | Run the same workflow from the terminal using `pipeline.py` |
| 🔄 Flexible LLM Backend | Supports Mistral AI (primary) with OpenRouter as automatic fallback |
| ⬇️ Report Download | Download the final research report as a Markdown file |

---

## 🏗️ Architecture

```text
Research Topic
      │
      ▼
┌─────────────────────┐
│  🔍 Search Agent     │  Tavily Search API → Titles, URLs, Snippets
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│  📄 Reader Agent     │  Requests + BeautifulSoup → Deep Page Content
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│  ✍️ Writer Chain      │  LangChain LCEL + Mistral/OpenRouter
│  └─ Report Builder   │  Introduction → Key Findings → Conclusion → Sources
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│  🧐 Critic Chain     │  Quality Score (X/10) + Strengths + Areas to Improve
└─────────────────────┘
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Streamlit |
| LLM Orchestration | LangChain (LCEL pipe `\|` operator) |
| LLM Providers | Mistral AI (`mistral-small-latest`) · OpenRouter (Llama 3.3 70B free) |
| Web Search | Tavily Search API |
| Web Scraping | Requests + BeautifulSoup4 |
| Language | Python 3.10+ |
| Config | python-dotenv |

---

## 📂 Project Structure

```text
ResearchMind/
│
├── app.py              # Streamlit UI (main entry point)
├── pipeline.py         # CLI entry point (terminal usage)
│
├── agents.py           # LLM setup, Search & Reader agents, Writer & Critic chains
├── tools.py            # Tavily web search & URL scraping tools
│
├── requirements.txt    # Python dependencies
├── .env.example        # Environment variable template
├── .gitignore
└── README.md
```

---

## ⚡ Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/Abhinav-180/Research-Mind.git
cd Research-Mind
```

### 2. Create and Activate a Virtual Environment

```bash
python -m venv .venv
```

```bash
# Windows
.venv\Scripts\activate

# macOS / Linux
source .venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Set Up API Keys

Create a `.env` file in the project root (or copy from `.env.example`):

```env
# Required — Tavily Search (1,000 free queries/month)
TAVILY_API_KEY=your_tavily_api_key_here

# Option A: Mistral AI (preferred)
MISTRAL_API_KEY=your_mistral_api_key_here
LLM_MODEL=mistral-small-latest

# Option B: OpenRouter (free, automatic fallback)
# OPENROUTER_API_KEY=your_openrouter_api_key_here
# LLM_MODEL=meta-llama/llama-3.3-70b-instruct:free
```

Get your free API keys from:

- **Tavily:** [tavily.com](https://tavily.com)
- **Mistral AI:** [console.mistral.ai](https://console.mistral.ai)
- **OpenRouter:** [openrouter.ai](https://openrouter.ai) *(no credit card required)*

> If `MISTRAL_API_KEY` is set, the app uses Mistral. Otherwise, it automatically falls back to OpenRouter.

### 5. Run the App

```bash
streamlit run app.py
```

The app will open at `http://localhost:8501`

---

## 💻 Run in Terminal (CLI Mode)

```bash
python pipeline.py
```

This runs the same 4-step research pipeline in CLI mode and prompts you for a topic.

---

## 🚀 How to Use

1. Open the Streamlit app
2. Enter a research topic (e.g. `Fusion energy progress`, `LLM agents 2025`, `CRISPR gene editing`)
3. Click **⚡ Run Research Pipeline**
4. Watch the 4 agents work in real-time — Search → Reader → Writer → Critic
5. Review the final report and critic feedback
6. Download the report as `.md` with one click

---

## ☁️ Deployment (Streamlit Community Cloud)

1. Push the repo to GitHub
2. Go to [share.streamlit.io](https://share.streamlit.io/)
3. Click **Create app** → Select repo `Abhinav-180/Research-Mind`, branch `main`, file `app.py`
4. In **Advanced settings**, add your secrets:

```toml
TAVILY_API_KEY = "your_tavily_api_key"
MISTRAL_API_KEY = "your_mistral_api_key"
LLM_MODEL = "mistral-small-latest"
```

Or for OpenRouter:

```toml
TAVILY_API_KEY = "your_tavily_api_key"
OPENROUTER_API_KEY = "your_openrouter_api_key"
LLM_MODEL = "meta-llama/llama-3.3-70b-instruct:free"
```

5. Click **Deploy** 🚀

---

## 🔑 Key Concepts

| Concept | Where Used | Why |
|---|---|---|
| Multi-Agent Workflow | `agents.py`, `pipeline.py`, `app.py` | Splits research into specialized steps (search, read, write, critique) for higher quality output |
| Tool Calling | `tools.py` | Lets agents autonomously search the web and scrape URLs using LangChain `@tool` |
| Prompt Chaining (LCEL) | `agents.py` | Modern chain composition using the `\|` pipe operator for clean, readable chains |
| Web Scraping | `tools.py` | Pulls deeper content from selected pages beyond search snippets (up to 3000 chars) |
| LLM Fallback Strategy | `agents.py` | Tries Mistral AI first, falls back to OpenRouter for zero-cost operation |
| Streamlit Session State | `app.py` | Tracks pipeline progress and results across re-runs for a seamless UX |


---

## 🙋 Author

Built by **[Abhinav](https://github.com/Abhinav-180)** as a portfolio project to demonstrate skills in multi-agent AI systems, LangChain orchestration, LLM integration, and full-stack Python development.
