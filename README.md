# 🧭 AI Learning Roadmap Generator

A Streamlit web app that uses **Google Gemini Flash** to create a personalized learning roadmap. Enter a skill, pick your level, say how much time you have, and get:

- A step-by-step learning path (3–5 stages)
- A weekly plan with a realistic timeline
- Recommended topics, tools, and resources
- A practice project for every stage
- A checklist of skills you'll have at the end
- A final capstone project
- Download as **Markdown (.md)** or **Text (.txt)**

## Project structure

```
ai-roadmap-generator/
├── app.py             # The Streamlit application
├── requirements.txt   # Python dependencies
└── README.md          # This file
```

## Requirements

- Python **3.10 or newer**
- A free Gemini API key from [Google AI Studio](https://aistudio.google.com/apikey)

## Run locally

```bash
# 1. Enter the project folder
cd ai-roadmap-generator

# 2. (Recommended) create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate          # macOS / Linux
.venv\Scripts\activate             # Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Add your API key (see next section)

# 5. Start the app
streamlit run app.py
```

The app opens at <http://localhost:8501>.

## Configure your API key

The app looks for `GEMINI_API_KEY` in **Streamlit secrets first**, then in **environment variables**. Never put the key directly in `app.py`.

### Option A: Streamlit secrets (recommended)

Create the file `.streamlit/secrets.toml` in the project folder:

```toml
GEMINI_API_KEY = "your-api-key-here"
```

### Option B: Environment variable

```bash
export GEMINI_API_KEY="your-api-key-here"        # macOS / Linux
setx GEMINI_API_KEY "your-api-key-here"          # Windows (restart terminal afterwards)
```

### Optional: choose a different model

The default model is `gemini-2.5-flash`. Google retires and releases model names over time. If you see a "model not found" error, check the [Gemini models page](https://ai.google.dev/gemini-api/docs/models) and set:

```toml
GEMINI_MODEL = "name-of-a-current-flash-model"
```

## ⚠️ Keep your key out of GitHub

Create a `.gitignore` file in the project folder with:

```
.streamlit/secrets.toml
.venv/
__pycache__/
*.pyc
.env
```

If you accidentally commit a key, **delete/revoke it in Google AI Studio and create a new one**. Removing it in a later commit is not enough.

## Upload to GitHub

1. Create a free account at <https://github.com> and click **New repository**.
2. Name it (e.g. `ai-roadmap-generator`), leave it empty (no README/.gitignore), and click **Create repository**.
3. In your project folder, run:

```bash
git init
git add app.py requirements.txt README.md .gitignore
git commit -m "Initial commit: AI Learning Roadmap Generator"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/ai-roadmap-generator.git
git push -u origin main
```

4. Refresh the GitHub page and confirm `secrets.toml` is **not** listed.

## Deploy on Streamlit Community Cloud

1. Go to <https://share.streamlit.io> and sign in with GitHub.
2. Click **Create app** → **Deploy a public app from GitHub**.
3. Choose your repository, branch `main`, and main file path `app.py`.
4. Open **Advanced settings → Secrets** and paste:

```toml
GEMINI_API_KEY = "your-api-key-here"
```

5. Click **Deploy**. The first build takes a few minutes.
6. To update the key later: app menu → **Settings → Secrets**.

Every `git push` to `main` redeploys the app automatically.

## Troubleshooting

| Problem | Fix |
|---|---|
| "No Gemini API key found" | Check the secret name is exactly `GEMINI_API_KEY`. |
| "API key looks invalid" | Create a new key in Google AI Studio. |
| "Model was not found" | Set `GEMINI_MODEL` to a current model name. |
| "Rate limit or quota reached" | Wait a minute; free tiers have request limits. |
| `ModuleNotFoundError` | Run `pip install -r requirements.txt` in your active environment. |

## Notes

- AI-generated roadmaps can contain mistakes or outdated resources. Verify before relying on them.
- The prompt asks the model not to invent URLs, but always check resource names yourself.
- Each generation uses your Gemini API quota. mudassir-khattak
