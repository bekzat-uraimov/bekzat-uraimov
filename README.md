## Hi, I'm Bekzat

Software engineer in Seattle. I work mostly on backends in Python.
CS student at Bellevue College. Before software I spent four years making commercial videos, so I am used to clients, feedback and deadlines.

### What I am building

**ONER** (private for now) is an online course platform for Russian speaking Central Asia.
I built the backend with FastAPI, PostgreSQL, SQLModel and Alembic. The part that took the longest was the payment flow with FreedomPay, because a mistake there means someone gets charged twice, or gets a course they never paid for.
The rule of the whole product is simple: you watch a lesson only if you own it. Access is decided on the server, only after the payment webhook is verified. Clicking "buy" twice returns the same order, not a second charge. Video is DRM protected with Kinescope, and files are stored on Cloudflare R2.

```mermaid
sequenceDiagram
    participant S as Student
    participant API as ONER API (FastAPI)
    participant DB as PostgreSQL
    participant FP as FreedomPay
    S->>API: Buy course
    API->>DB: Create order (or return the open one)
    API-->>S: Redirect to payment page
    S->>FP: Pay
    FP->>API: Webhook with payment result
    API->>API: Verify webhook
    API->>DB: Mark order paid, grant entitlement
    S->>API: Open lesson
    API->>DB: Check entitlement
    API-->>S: Kinescope DRM video
```

**ThinkCoder** at [akyldoo.ai](https://akyldoo.ai), an AI coding assistant. I built the Python AI orchestration layer.
LangGraph runs each problem as its own session with state, instead of one long prompt. LiteLLM sends easy requests to a local Qwen2.5-Coder model through Ollama, and the harder ones go to Gemini. This keeps the cost down.

```mermaid
flowchart LR
    P[Student problem] --> G[LangGraph session<br/>state per problem]
    G --> R{LiteLLM router}
    R -->|easy| L[Qwen2.5-Coder 7B<br/>local, Ollama]
    R -->|hard or fallback| M[Gemini]
```

### Hackathons

- **[Poly Predictor Kit](https://github.com/bekzat-uraimov/Poly_Predictor_Kit)**: won the Polymarket track at QuackHacks (Nov 2025). Chrome extension that analyzes Polymarket events with Gemini and a TF-IDF emotion classifier.
- **[AI Visual Novel Creator](https://github.com/bekzat-uraimov/AI_Visual_Novel_Creator)**: hackathon win. Generates a playable Ren'Py visual novel from one prompt.

### Other projects

- **[focusn't](https://github.com/bekzat-uraimov/Focusn-t)**: focus timer that uses your webcam to notice when you look away. All ML runs in the browser with MediaPipe, video never leaves the device.
- **[HabitTrackerBot](https://github.com/bekzat-uraimov/HabitTrackerBot)**: stateless Telegram bot for habit tracking with the Pixela API.
- **[portfolio](https://github.com/bekzat-uraimov/portfolio)**: my site, [bekzat.dev](https://bekzat.dev). Flask, one page, projects load live from the GitHub API.

### Working with

Python, FastAPI, PostgreSQL, SQLModel, Alembic, LangGraph, LiteLLM, Docker, Next.js, C++

This fall I am taking Data Structures in C++ and Python for Data Science at Bellevue College.

### Contact

[bekzat.dev](https://bekzat.dev) · [LinkedIn](https://www.linkedin.com/in/bekzat-uraimov/) · bkzturaimov@gmail.com
