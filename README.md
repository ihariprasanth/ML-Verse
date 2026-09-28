# MLVerse - Machine Learning Model Intelligence and Architecture Platform

MLVerse is an interactive, visual-first platform engineered to explore, diagnose, compare, and select Machine Learning and Deep Learning architectures for real-world scenarios.

Powered by high-throughput LLM reasoning (Groq) with an integrated local heuristic engine, MLVerse analyzes input problem statements in natural language or dialect (English, Tanglish, and others) and outputs tactical dataset blueprints, model benchmarks, numerical execution traces, and comparative accuracy matrices.

---

## Technical Stack

- Frontend: React 18, Vite 5, Tailwind CSS, Lucide Icons, Framer Motion, Recharts
- Design System: Tactical HUD Liquid-Glass Morphism, Coordinate Background Telemetry
- Backend: Node.js, Express, CORS, Express Rate Limit, Dotenv
- AI Inference: Groq Cloud API (openai/gpt-oss-20b / llama-3.3-70b-versatile) with strict JSON output schema and resilient local fallback heuristics

---

## Repository Structure

```
mlverse/
├── client/                     # React + Vite Frontend
│   ├── public/                 # Static assets, SVG crosshair favicon
│   ├── src/
│   │   ├── components/         # Navbar, BackgroundGraphUI, BookmarksDrawer
│   │   ├── data/
│   │   │   └── models.js       # Curated 44-model database
│   │   ├── hooks/
│   │   │   └── useAppState.jsx # Global state (navigation, compare cart, history)
│   │   ├── pages/
│   │   │   ├── LandingPage.jsx     # Scenario diagnoser, parameter cards, accuracy matrix
│   │   │   ├── CategoryPage.jsx    # Model directory with paradigm filters
│   │   │   ├── ModelDetailPage.jsx # Interactive simulator and mathematical formulas
│   │   │   ├── ComparePage.jsx     # Side-by-side radar comparison and AI verdict
│   │   │   └── RecommenderPage.jsx # AI scenario diagnoser with confidence meter
│   │   ├── utils/
│   │   │   └── api.js          # Production and local API URL resolver
│   │   ├── App.jsx             # Main layout and view router
│   │   ├── index.css           # Liquid glassmorphism classes and HUD styling
│   │   └── main.jsx            # React root entry
│   ├── package.json
│   ├── tailwind.config.js
│   └── vite.config.js
├── server/                     # Node.js Express API Server
│   ├── middleware/
│   │   └── rateLimiter.js      # Global API rate limiters
│   ├── routes/
│   │   ├── recommend.js        # POST /api/recommend (Scenario recommendation)
│   │   └── compare.js          # POST /api/compare (Comparative analysis)
│   ├── services/
│   │   └── groq.js             # Groq API integration and fallback heuristics
│   ├── .env.example            # Environment variables template
│   ├── index.js                # Express entrypoint
│   └── package.json
├── .gitignore                  # Git exclusions (node_modules, .env, build artifacts)
├── package.json                # Root scripts
└── README.md
```

---

## Local Development Setup

### 1. Prerequisites
- Node.js: v18+ (tested on Node v20/v24)
- npm: v9+

### 2. Configure Environment Variables
Create a `.env` file inside the `server/` directory:
```env
PORT=5000
GROQ_API_KEY=your_groq_api_key_here
CLIENT_ORIGIN=*
```
Note: You can obtain a free Groq API key from https://console.groq.com/keys. The backend also includes a built-in offline heuristic engine so the system remains functional even without an API key.

### 3. Install Dependencies
```bash
# Install root, client, and server dependencies
cd server && npm install && cd ..
cd client && npm install && cd ..
```

### 4. Run Locally
```bash
# Terminal 1: Start Backend API (runs on http://localhost:5000)
cd server
node index.js

# Terminal 2: Start Frontend Client (runs on http://localhost:5173)
cd client
npm run dev
```

Open http://localhost:5173 in your browser.

---

## Hosting and Deployment Guide

### Architecture Overview
- Frontend (Client): Can be hosted on GitHub Pages or Vercel for free.
- Backend API (Server): Can be hosted on Render.com or Railway for free, keeping the `GROQ_API_KEY` private and secure.

### Step 1: Deploy Backend to Render (Free Tier)
1. Go to https://render.com and sign in with GitHub.
2. Click "New +" and select "Web Service".
3. Connect your repository: `https://github.com/ihariprasanth/ML-Verse.git`.
4. Configure the settings:
   - Root Directory: `server`
   - Build Command: `npm install`
   - Start Command: `node index.js`
   - Environment Variables:
     - `GROQ_API_KEY`: your Groq API key
     - `PORT`: `5000`
     - `CLIENT_ORIGIN`: `*`
5. Click "Create Web Service".
6. Render will provide a public HTTPS URL (e.g., `https://mlverse-backend.onrender.com`).

### Step 2: Deploy Frontend to GitHub Pages
1. In the `client` directory, build the project with your backend URL:
   ```bash
   # Set the API URL environment variable
   export VITE_API_URL=https://your-backend.onrender.com
   npm --prefix client run build
   ```
2. You can deploy the `client/dist` directory to GitHub Pages using the `gh-pages` package or via GitHub Actions.

### Alternative: All-in-One Deployment on Vercel
1. Go to https://vercel.com and import `https://github.com/ihariprasanth/ML-Verse.git`.
2. Set Root Directory to `client`.
3. Under Environment Variables, add `VITE_API_URL` pointing to your deployed backend.
4. Deploy in one click.

---

## Core Features

1. Scenario Model Diagnoser:
   - Evaluates problem statements in plain English, Tanglish, or other languages.
   - Recommends the optimal algorithm, expected metric accuracy, and confidence score.

2. Dataset Columns and Parameters Blueprint:
   - Dual view mode: Comprehensive Parameter Cards and Compact Summary Table.
   - For every feature: Role, Data Type, Sample Values, Value Range/Constraints, Missing Value Imputation Strategy, and ML Preprocessing Code (StandardScaler, One-Hot Encoding, etc.).
   - Includes one-click CSV Header Copy for pandas DataFrame integration.

3. In-Depth Algorithmic Rationale:
   - Clear explanations detailing why the selected algorithm outperforms alternatives for tabular, text, image, or sequential data.

4. Step-by-Step Numerical Trace:
   - End-to-end trace showing how sample inputs propagate through model decision boundaries to produce the final prediction.

5. Accuracy and Comparison Matrix:
   - Direct benchmark comparison against 3 competing models with metric delta bars.

6. Flexible Scenario Input:
   - Direct text input with keyboard shortcut (Enter to execute).
   - `.txt` file upload button and drag-and-drop auto-diagnostic.
   - Quick-start clickable preset scenario chips.
