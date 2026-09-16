# WanderPlan

WanderPlan is a travel-planning assistant I built with LangGraph, MCP, and FastAPI. It uses multiple agents, a supervisor, input guardrails, and a human approval step to turn a travel request into a plan that can be reviewed before it is finalized.

I created this project to explore how agent workflows can be organized into clear, safe, and reviewable steps instead of relying on a single agent to handle everything.

What this project demonstrates:
- Coordinating multiple agents with LangGraph and MCP
- Using a supervisor agent to manage the workflow
- Validating incoming requests with guardrails
- Reviewing and approving generated travel plans with a human-in-the-loop step

Project structure
- `app.py`: FastAPI web frontend and API endpoints
- `backend.py`: agent orchestration and travel-planning logic
- `mcp_client.py`: client helpers to interact with the MCP server
- `custom_weather_mcp_server.py`: example MCP server for checking weather
- `templates/` and `static/`: frontend files (HTML, JavaScript, and CSS)

Features
- Interactive web UI for sending travel planning prompts
- Endpoint for drafting travel plans and a separate approval endpoint
- Example MCP server demonstrating domain adapters such as weather and checkpoints

Requirements
- Python 3.10+ (recommended)
- Git
- A virtual environment such as `venv`

Getting started on Windows

1. Create and activate a virtual environment:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1    # PowerShell
```

2. Install the dependencies:

```powershell
pip install -r requirements.txt
```

3. Start the FastAPI app in development mode:

```powershell
# option A (run module)
python app.py

# option B (uvicorn)
uvicorn app:app --reload --host 127.0.0.1 --port 8000
```

4. Open the web UI:

Visit http://127.0.0.1:8000 in your browser to use the WanderPlan frontend.

Running the example MCP server

The project includes `custom_weather_mcp_server.py` as an example MCP server. Run it in a separate terminal when experimenting with the custom adapters used by the application.

```powershell
# start example MCP server (if needed)
python custom_weather_mcp_server.py
```

API endpoints
- `POST /api/travel` — create or resume a travel planning thread. JSON: `{ "message": "<user prompt>", "thread_id": "optional-thread-id" }`
- `POST /api/travel/approve` — approve or request revisions for a draft. JSON: `{ "thread_id": "<id>", "approved": true|false, "feedback": "optional" }`
- `GET /health` — basic health check and features list

Configuration and environment

Secrets and API keys are not included in this repository. Set any required keys through environment variables or a `.env` file for LangGraph, LangChain, or other adapters.

Development notes
- I keep synchronous convenience wrappers in `backend.py` while the FastAPI server runs asynchronously. `nest_asyncio` is applied in `app.py` so the synchronous helpers can call the asynchronous MCP helpers.
- Automated tests are not included yet. For now, the easiest way to try the project is to use the web UI or call the API endpoints directly.

Contributing

Suggestions and improvements are welcome. Feel free to open an issue or pull request with bug fixes, documentation updates, or new adapter examples.

License

This repository follows the license in the `LICENSE` file.

Acknowledgements

This project was built while learning and experimenting with LangGraph, MCP, supervisor workflows, guardrails, and human-in-the-loop patterns.

Contact

For questions or suggestions, open an issue in this repository.
