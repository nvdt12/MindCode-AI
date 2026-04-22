# 🤖 MindCode-AI: Your AI-Powered Code Reviewer

MindCode-AI is a full-stack web application that leverages the Google Gemini API to provide intelligent, on-demand code reviews. Built with a modern FastAPI backend and an interactive Streamlit frontend, this tool helps developers improve code quality, document standards, and analyze algorithm complexity.

---

## ✨ Features

* **Secure User Authentication:** JWT-based login and registration system.
* **Persistent User Data:** User profiles are securely stored in a database.
* **Multi-Type Code Analysis:**
    * **General Review:** Checks for best practices, potential bugs, and logic improvements.
    * **Documentation Review:** Analyzes docstrings and comments for clarity and completeness.
    * **Competitive Programming:** Provides Time and Space Complexity analysis (e.g., O(n log n)) and explains the user's algorithm.
* **Interactive AI Chatbot:** A popover chat assistant for any coding-related questions.
* **Modern UI:** A clean, responsive interface built with Streamlit, including an ACE code editor with syntax highlighting.
* **Scalable Backend:** A robust API built with FastAPI, ready to handle concurrent requests.

---

## 🚀 Tech Stack

* **Frontend:** [Streamlit](https://codesense-ai-your-ai-powered-code-reviewer.streamlit.app/)
* **Backend:** [FastAPI](https://mindcode-ai.onrender.com)
* **AI Model:** [Google Gemini](https://ai.google.dev/)
* **Database:** [SQLite](https://www.sqlite.org/index.html)
* **Authentication:** [JWT (python-jose)](https://python-jose.readthedocs.io/en/latest/)
* **Password Hashing:** [Argon2 (passlib)](https://passlib.readthedocs.io/en/stable/)
* **Deployment:** [Render](https://render.com/)

---

## 📁 File Structure

```

ai-code-reviewer-app/
│
├── backend/
│   ├── .env.example        \# Environment variable template
│   ├── code\_reviewer.db    \# Local SQLite database
│   ├── database.py         \# DB logic, user management, hashing
│   ├── gemini\_client.py    \# All Gemini API logic and prompts
│   ├── main.py             \# FastAPI application
│   ├── models.py           \# Pydantic models for API
│   └── requirements.txt    \# Backend Python packages
│
└── frontend/
├── pages/
│   ├── 2\_Login.py      \# Login & Register page
│   └── 3\_Code\_Reviewer.py \# Main app page
│
├── 1\_Home.py           \# Streamlit landing page
├── requirements.txt    \# Frontend Python packages
└── style.css           \# Custom CSS for styling

````

---

## ⚙️ Local Setup

### Prerequisites

* Python 3.10+
* A Google Gemini API Key.
* A separate terminal for the backend and frontend.

### 1. Backend Setup

1.  **Navigate to the backend folder:**
    ```bash
    cd backend
    ```

2.  **Create and activate a virtual environment:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # (or .\venv\Scripts\activate on Windows)
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Set up environment variables:**
    * Copy `.env.example` to a new file named `.env`.
    * Edit `.env` and add your `GEMINI_API_KEY`.
    * Generate a `SECRET_KEY` using:
        ```bash
        python -c "import secrets; print(secrets.token_hex(32))"
        ```
    * Paste the generated key into your `.env` file.

5.  **Run the backend server:**
    ```bash
    uvicorn main:app --reload
    ```
    The API will be running at `http://127.0.0.1:8000`.

### 2. Frontend Setup

1.  **Open a *new* terminal** and navigate to the frontend folder:
    ```bash
    cd frontend
    ```

2.  **Create and activate a virtual environment:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # (or .\venv\Scripts\activate on Windows)
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Run the frontend app:**
    ```bash
    streamlit run 1_Home.py
    ```
    The app will open in your browser at `http://localhost:8501`.

---

## ☁️ Deployment

This application is configured for deployment on [Render](https://render.com/) as two separate "Web Services" using a monorepo structure.

* **Backend Service:**
    * **Root Directory:** `backend`
    * **Start Command:** `uvicorn main:app --host 0.0.0.0 --port $PORT`
    * A **Persistent Disk** is required to store the SQLite database.
    * **Env Vars:** `GEMINI_API_KEY`, `SECRET_KEY`, `DB_DIR` (e.g., `/var/data`).

* **Frontend Service:**
    * **Root Directory:** `frontend`
    * **Start Command:** `streamlit run 1_Home.py --server.port $PORT --server.address 0.0.0.0`
    * **Env Vars:** `API_URL` (set to the URL of the deployed backend service).

---

## License

This project is licensed under the MIT License.
