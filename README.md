# ResearchMind - Multi-Agent Research System

ResearchMind is a Streamlit-based AI research assistant that uses a multi-agent workflow to search the web, read useful sources, write a structured research report, and review the final output.

The app is built with LangChain, Tavily Search, BeautifulSoup, and OpenAI-compatible LLM APIs such as Mistral AI or OpenRouter.

## Features

- Web-based Streamlit interface
- Multi-agent research pipeline
- Recent web search using Tavily
- URL scraping for deeper source reading
- AI-generated structured research reports
- Critic chain that scores and reviews the report
- Optional command-line pipeline through `pipeline.py`
- Supports Mistral AI and OpenRouter models

## Tech Stack

- Python
- Streamlit
- LangChain
- LangChain OpenAI
- Tavily Search API
- BeautifulSoup
- Requests
- python-dotenv

## Project Structure

```text
.
├── app.py              # Streamlit web app
├── agents.py           # LLM, agents, writer chain, critic chain
├── tools.py            # Tavily search and URL scraping tools
├── pipeline.py         # CLI version of the research pipeline
├── requirements.txt    # Python dependencies
├── .env.example        # Environment variable template
└── .gitignore
```

## How It Works

1. Search Agent finds recent and reliable web information using Tavily.
2. Reader Agent selects a useful URL and scrapes deeper content from it.
3. Writer Chain creates a structured research report from the gathered data.
4. Critic Chain reviews the report and gives feedback with a score.

## Setup Locally

### 1. Clone the repository

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it:

```bash
# Windows
.venv\Scripts\activate

# macOS/Linux
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Add environment variables

Copy the example file:

```bash
copy .env.example .env
```

On macOS/Linux:

```bash
cp .env.example .env
```

Then add your API keys inside `.env`:

```env
TAVILY_API_KEY=your_tavily_api_key

# Use either Mistral:
MISTRAL_API_KEY=your_mistral_api_key
LLM_MODEL=mistral-small-latest

# Or OpenRouter:
OPENROUTER_API_KEY=your_openrouter_api_key
LLM_MODEL=meta-llama/llama-3.3-70b-instruct:free
```

If `MISTRAL_API_KEY` is present, the app uses Mistral first. If it is not present, it falls back to OpenRouter.

Do not upload your `.env` file to GitHub.

## Run the App

```bash
streamlit run app.py
```

Then open:

```text
http://localhost:8501
```

## Run the CLI Pipeline

You can also run the research pipeline from the terminal:

```bash
python pipeline.py
```

Enter a topic when prompted.

## Deployment

### Option 1: Deploy on Streamlit Community Cloud

This is the easiest option for this project.

1. Push this project to GitHub.
2. Go to [Streamlit Community Cloud](https://share.streamlit.io/).
3. Click `New app`.
4. Select your GitHub repository.
5. Set the main file path as:

```text
app.py
```

6. Add secrets in Streamlit Cloud:

```toml
TAVILY_API_KEY = "your_tavily_api_key"
MISTRAL_API_KEY = "your_mistral_api_key"
LLM_MODEL = "mistral-small-latest"
```

Or, if using OpenRouter:

```toml
TAVILY_API_KEY = "your_tavily_api_key"
OPENROUTER_API_KEY = "your_openrouter_api_key"
LLM_MODEL = "meta-llama/llama-3.3-70b-instruct:free"
```

7. Deploy the app.

### Option 2: Deploy on Render

1. Push the project to GitHub.
2. Create a new `Web Service` on [Render](https://render.com/).
3. Connect your GitHub repository.
4. Use these settings:

```text
Build Command: pip install -r requirements.txt
Start Command: streamlit run app.py --server.port $PORT --server.address 0.0.0.0
```

5. Add environment variables in Render dashboard:

```text
TAVILY_API_KEY
MISTRAL_API_KEY or OPENROUTER_API_KEY
LLM_MODEL
```

6. Deploy.

## GitHub Repository Description

Use this as the GitHub repo description:

```text
A Streamlit multi-agent AI research assistant that searches the web, scrapes sources, writes structured reports, and reviews them using LangChain, Tavily, and OpenAI-compatible LLMs.
```

Short version:

```text
Multi-agent AI research assistant built with Streamlit, LangChain, Tavily, and LLM APIs.
```

## Suggested GitHub Topics

```text
streamlit
langchain
multi-agent
ai-agents
research-assistant
tavily
mistral-ai
openrouter
python
llm
```

## Important Notes

- Keep `.env` private.
- Add API keys only through environment variables or deployment secrets.
- Tavily is required for web search.
- Mistral or OpenRouter is required for LLM responses.
- If you get an API connection error locally, check your internet connection, API keys, firewall, or deployment secrets.

## License

This project is open for learning and experimentation. Add a license file if you want to publish it as an open-source project.
