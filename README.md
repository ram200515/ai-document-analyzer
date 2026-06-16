# AI Document Analyzer
### SAP UI5 + Python Flask + LLaMA API (Groq) + MySQL

**Developer:** Adithyaram Gude

---

## Screenshots

### Application UI
| Home — Upload Page | Result — Analysis Output |
|---|---|
| ![Home Page](screenshots/home.png) | ![Result Page](screenshots/result.png) |

### Database — MySQL Workbench
| EER Diagram | Documents Table |
|---|---|
| ![EER Diagram](screenshots/eer_diagram.png) | ![Documents Table](screenshots/documents_table.png) |

### Backend Terminal
![Backend Running](screenshots/terminal.png)

---

## What It Does
Upload any business document (.txt or .pdf) and get instant AI-powered analysis with results saved permanently to MySQL database:
- 📄 Document Summarization
- 🔑 Key Points Extraction
- 💬 Sentiment Analysis
- ✅ Action Items Extraction
- ⚠️ Risk Identification

---

## Tech Stack

| Layer      | Technology                        |
|------------|-----------------------------------|
| Frontend   | SAP UI5 (XMLViews, MVC, Routing)  |
| Backend    | Python Flask + REST API           |
| AI Model   | LLaMA 3 via Groq API              |
| Database   | MySQL + MySQL Workbench           |
| PDF Parse  | PyPDF2                            |
| Styling    | SAP Horizon Theme (sap_horizon)   |

---

## Database Schema

```
ai_doc_analyzer_db
├── users            (id, name, email, created_at)
├── documents        (id, user_id FK, file_name, file_type, word_count, upload_date)
├── analysis_results (id, document_id FK, analysis_type, confidence, processing_time, created_at)
└── insights         (id, result_id FK, category, insight, state)
```

---

## Project Structure

```
ai-doc-analyzer/
├── webapp/                      # SAP UI5 Frontend
│   ├── index.html               # Bootstrap entry point
│   ├── Component.js             # UI5 Component definition
│   ├── manifest.json            # App config + routing
│   ├── view/
│   │   ├── App.view.xml         # Root nav container
│   │   ├── Home.view.xml        # Upload page
│   │   └── Result.view.xml      # Results page
│   └── controller/
│       ├── App.controller.js
│       ├── Home.controller.js   # File upload + API call
│       └── Result.controller.js # Display + export
├── backend/
│   ├── app.py                   # Flask server + LLaMA + MySQL
│   └── requirements.txt
├── database/
│   └── schema.sql               # MySQL schema setup script
└── screenshots/                 # Project screenshots
```

---

## Setup & Run

### Step 1 — Get Free Groq API Key
1. Go to https://console.groq.com
2. Sign up (free) → Create API Key
3. Copy your key

### Step 2 — MySQL Database Setup
1. Install MySQL Community Server from https://mysql.com
2. Open MySQL Workbench
3. Run the schema file:
```bash
mysql -u root -p < database/schema.sql
```
Or open `database/schema.sql` in MySQL Workbench and execute it.

### Step 3 — Backend Setup
```bash
cd backend
pip install -r requirements.txt
export GROQ_API_KEY="your_groq_api_key_here"
python app.py
```
Backend runs on: http://localhost:5000

### Step 4 — Frontend Setup
```bash
cd webapp
# Option A: VS Code Live Server (easiest)
# Right-click index.html → Open with Live Server

# Option B: Python simple server
python -m http.server 8080
# Open: http://localhost:8080
```

### Step 5 — Test it!
1. Open http://localhost:8080 in browser
2. Upload a .txt or .pdf file
3. Choose analysis type
4. Click "Analyze Document with AI"
5. View results on the Result page
6. Check MySQL Workbench — data saved automatically!

---

## API Endpoints

| Method | Endpoint  | Description           |
|--------|-----------|-----------------------|
| GET    | /health   | Check backend status  |
| POST   | /analyze  | Analyze document text |

### POST /analyze — JSON Body
```json
{
  "text": "Your document text here...",
  "analysis_type": "summarize",
  "file_name": "report.txt"
}
```

### Analysis Types
| Key          | Description             |
|--------------|-------------------------|
| summarize    | Document summary        |
| keypoints    | Key points extraction   |
| sentiment    | Sentiment analysis      |
| action_items | Action items extraction |
| risks        | Risk identification     |

---
