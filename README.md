 AI-FAO-Assistant
An AI-powered agricultural assistant designed to help farmers and agricultural users access useful information about crops, farming practices, irrigation, soil management, pests, diseases, weather, and agricultural knowledge.

The project combines:

FastAPI

Python

MongoDB

Large Language Models (LLMs)

Retrieval-Augmented Generation (RAG)

Agricultural knowledge

External APIs

Future image-based crop/disease analysis

Multilingual support

📌 Project Status
Current status: Development / MVP

Implemented
FastAPI backend

MongoDB configuration

Farmer management

Crop data architecture

Conversation storage

Chat API

LLM integration structure

RAG architecture

Environment configuration

Docker development environment

API documentation through Swagger

Planned
Authentication

Production RAG

Vector search

FAO document ingestion

Weather integration

Market-price integration

Crop disease image analysis

Multilingual voice assistant

Mobile application

Notifications

Production deployment

🎯 Project Objectives
The main goal of AI-FAO-Assistant is to provide an accessible agricultural information assistant.

The system should allow a user to ask questions such as:

How should I manage my rice crop?

What type of irrigation is suitable for my crop?

Why are my tomato leaves turning yellow?

How can I improve soil management?

What should I consider before applying a pesticide?

What agricultural practices are suitable for this crop?

The assistant uses the user's question together with available agricultural knowledge and application context to generate a response.

🏗️ System Architecture
                         USER
                           |
              +------------+------------+
              |                         |
           Web App                  Mobile App
              |                         |
              +------------+------------+
                           |
                           v
                     FastAPI API
                           |
                    AI Orchestrator
                           |
          +----------------+----------------+
          |                |                |
          v                v                v
         LLM              RAG          External Tools
          |                |                |
          |                v                |
          |         Agricultural KB         |
          |                                 |
          |                    +------------+
          |                    |
          |                 Weather
          |                 Market
          |                 GIS
          |                 etc.
          |
          +----------------+
                   |
                   v
                MongoDB
                   |
        +----------+----------+
        |          |          |
     Farmers     Crops    Conversations
                              |
                           Messages

🧰 Technology Stack
Component	Technology
Programming Language	Python
Backend	FastAPI
Database	MongoDB
Database Driver	PyMongo
AI	LLM API
RAG	Embeddings + Vector Search
API Documentation	Swagger / OpenAPI
Containerization	Docker
Testing	Pytest
HTTP Client	HTTPX
Configuration	Environment Variables

📁 Project Structure
AI-FAO-Assistant/
│
├── backend/
│   │
│   ├── app/
│   │   ├── main.py
│   │   │
│   │   ├── api/
│   │   │   └── routes/
│   │   │       ├── chat.py
│   │   │       ├── farmers.py
│   │   │       ├── crops.py
│   │   │       └── health.py
│   │   │
│   │   ├── ai/
│   │   │   ├── llm.py
│   │   │   ├── rag.py
│   │   │   └── orchestrator.py
│   │   │
│   │   ├── core/
│   │   │   └── config.py
│   │   │
│   │   ├── db/
│   │   │   ├── mongodb.py
│   │   │   ├── collections.py
│   │   │   └── indexes.py
│   │   │
│   │   └── services/
│   │       ├── farmer_service.py
│   │       ├── conversation_service.py
│   │       └── document_service.py
│   │
│   ├── data/
│   │   └── documents/
│   │
│   ├── tests/
│   │
│   ├── .env
│   ├── .env.example
│   ├── requirements.txt
│   ├── Dockerfile
│   └── docker-compose.yml
│
├── frontend/
│
├── DEVELOPMENT.md
├── MONGODB_SETUP.md
├── README.md
└── .gitignore

🚀 Getting Started
1. Clone the Project
git clone <repository-url>
cd AI-FAO-Assistant

If the project is not yet hosted in Git, simply download or create the project directory locally.

2. Create Python Environment
Move into the backend:

cd backend

Create a virtual environment:

python -m venv venv

Windows
venv\Scripts\activate

Linux/macOS
source venv/bin/activate

3. Install Dependencies
pip install -r requirements.txt

4. Configure Environment Variables
Create:

.env

Example:

APP_NAME=AI-FAO-Assistant

MONGODB_URL=mongodb://admin:change_this_password@localhost:27017

MONGODB_DATABASE=aifao

OPENAI_API_KEY=YOUR_API_KEY

OPENAI_MODEL=gpt-4o-mini

Never commit .env to Git.

🗄️ MongoDB Setup
Option 1 — Docker
Start MongoDB:

docker compose up -d mongodb

Check:

docker ps

The MongoDB container should be running.

Option 2 — Local MongoDB
Start your local MongoDB service and verify the connection:

mongosh

Then:

show dbs

▶️ Start the Backend
From the backend directory:

uvicorn app.main:app --reload

The backend will be available at:

http://localhost:8000

📚 API Documentation
FastAPI automatically provides Swagger documentation.

Open:

http://localhost:8000/docs

Alternative OpenAPI interface:

http://localhost:8000/redoc

❤️ Health Check
Request:

GET /health

Example:

curl http://localhost:8000/health

Expected response:

{
  "status": "healthy",
  "mongodb": true
}

👨‍🌾 Farmer API
Create Farmer
POST /api/v1/farmers

Example:

{
  "name": "Test Farmer",
  "phone": "+910000000000",
  "language": "en"
}

Example response:

{
  "_id": "68db00000000000000000000",
  "name": "Test Farmer",
  "phone": "+910000000000",
  "language": "en"
}

Get Farmer
GET /api/v1/farmers/{farmer_id}

Example:

curl http://localhost:8000/api/v1/farmers/FARMER_ID

🤖 AI Chat API
Endpoint:

POST /api/v1/chat

Request:

{
  "farmer_id": "FARMER_ID",
  "question": "How should I manage my rice crop?",
  "language": "en"
}

Response:

{
  "conversation_id": "CONVERSATION_ID",
  "answer": "Rice crop management depends on...",
  "sources": []
}

🧠 AI Processing Flow
When a user sends a question:

User Question
      |
      v
FastAPI
      |
      v
AI Orchestrator
      |
      +--------> Farmer Context
      |
      +--------> Crop Context
      |
      +--------> RAG Search
      |
      +--------> External Tools
      |
      v
LLM
      |
      v
Response Validation
      |
      v
MongoDB
      |
      v
User

📚 RAG
RAG means:

Retrieval-Augmented Generation

Instead of relying only on the language model, the assistant retrieves relevant agricultural information and supplies it as context.

Agricultural Documents
        |
        v
Document Processing
        |
        v
Chunking
        |
        v
Embeddings
        |
        v
Vector Search
        |
        v
Relevant Information
        |
        v
LLM
        |
        v
Answer

This architecture allows the knowledge base to be updated without retraining the entire language model.

📖 Knowledge Base
The future knowledge base can contain:

FAO documents
Agricultural manuals
Crop management information
Pest information
Disease information
Soil information
Irrigation information
Agricultural statistics
Local agricultural guidance

Documents should contain metadata such as:

{
  "title": "Rice Water Management",
  "source": "Agricultural Knowledge Base",
  "language": "en",
  "crop": "rice",
  "content": "..."
}

🍚 Crop Management
The system can maintain information about:

Crop
 |
 +-- Variety
 |
 +-- Planting Date
 |
 +-- Growth Stage
 |
 +-- Soil
 |
 +-- Irrigation
 |
 +-- Fertilization
 |
 +-- Pest Observations
 |
 +-- Disease Observations
 |
 +-- Harvest

Example MongoDB document:

{
  "name": "Rice",
  "variety": "Example Variety",
  "planting_date": "2026-07-15",
  "status": "growing"
}

🌦️ Future Weather Integration
Weather services can be integrated through an external API.

Flow:

Farmer Location
      |
      v
Weather API
      |
      v
Current Conditions
      |
      v
Forecast
      |
      v
AI Orchestrator
      |
      v
Agricultural Explanation

For example, the assistant could combine weather information with crop context to explain weather-related agricultural considerations.

🐛 Future Disease Detection
A future version can support crop images.

Camera
  |
  v
Crop Image
  |
  v
Image Upload API
  |
  v
Vision Model
  |
  v
Possible Disease / Issue
  |
  v
Agricultural Knowledge
  |
  v
LLM
  |
  v
Explanation

Image classification should be treated as an aid rather than automatically presenting an uncertain result as a confirmed diagnosis.

🌍 Multilingual Support
The architecture is designed to support multiple languages.

Potential languages include:

English
Tamil
Hindi
Telugu
Kannada
Malayalam
Bengali
Marathi

Example:

{
  "question": "நெல் பயிரை எப்படி பராமரிப்பது?",
  "language": "ta"
}

The AI service can return the answer in Tamil.

🗃️ MongoDB Collections
The primary MongoDB database is:

aifao

Collections:

farmers
farms
crops
observations
conversations
messages
diseases
weather
market_prices
documents
ai_logs

🔐 Security
Security requirements include:

Keep API keys on the backend.

Never expose database credentials to the frontend.

Use authentication for protected endpoints.

Validate all incoming data.

Use authorization to protect farmer records.

Use rate limiting for public APIs.

Protect uploaded images and documents.

Use encrypted connections in production.

Keep secrets outside source control.

Maintain appropriate audit logs.

Define data retention and deletion policies.

Example .gitignore:

.env
venv/
__pycache__/
*.pyc
.pytest_cache/

🧪 Testing
Run tests:

pytest

Example test:

from fastapi.testclient import TestClient

from app.main import app


client = TestClient(app)


def test_health():

    response = client.get("/health")

    assert response.status_code == 200

    assert response.json()["status"] == "healthy"

🐳 Docker
The development environment can use Docker:

Docker
 |
 +-- FastAPI
 |
 +-- MongoDB

Start services:

docker compose up --build

Stop services:

docker compose down

Stop and remove database volume:

docker compose down -v

Warning: Removing the volume deletes the local MongoDB data.

📊 Development Roadmap
Phase 1 — Foundation
[x] FastAPI
[x] MongoDB
[x] Configuration
[x] Farmer API
[x] Basic Chat API
[x] LLM integration structure

Phase 2 — Knowledge
[ ] FAO document ingestion
[ ] Document processing
[ ] Chunking
[ ] Embeddings
[ ] Vector search
[ ] Source citations

Phase 3 — Agriculture Services
[ ] Weather API
[ ] Market data
[ ] Crop management
[ ] Pest information
[ ] Disease information

Phase 4 — AI Features
[ ] Image analysis
[ ] Voice input
[ ] Voice output
[ ] Multilingual AI
[ ] Personalized recommendations

Phase 5 — Production
[ ] Authentication
[ ] Authorization
[ ] Monitoring
[ ] Logging
[ ] Backups
[ ] CI/CD
[ ] Cloud deployment
[ ] Security testing

🧩 Recommended Production Architecture
                       USER
                         |
               +---------+---------+
               |                   |
             Web                 Mobile
               |                   |
               +---------+---------+
                         |
                         v
                   API Gateway
                         |
                         v
                   FastAPI Backend
                         |
                 AI Orchestrator
                         |
       +-----------------+----------------+
       |                 |                |
       v                 v                v
      LLM               RAG             Tools
       |                 |                |
       |                 v        +-------+-------+
       |            Vector DB     |       |       |
       |                          Weather Market GIS
       |
       +------------------+
                          |
                          v
                       MongoDB
                          |
              +-----------+-----------+
              |           |           |
           Farmers      Crops    Conversations
                                      |
                                   Messages

📝 Development Principles
The project should follow these principles:

1. AI is not the database
The LLM should not be treated as the authoritative storage system.

Use:

MongoDB
+
Knowledge Base
+
RAG
+
External Data
+
LLM

2. Use retrieved information
Agricultural answers should use the appropriate knowledge sources whenever available.

3. Keep source information
Where appropriate, responses should include the source documents or references used by the RAG system.

4. Separate services
Keep:

API
AI
Database
RAG
External APIs

as separate logical components.

5. Design for scale
The MVP can be a single FastAPI application.

As usage increases, individual services can be separated.

🤝 Contribution
A typical contribution workflow:

git checkout -b feature/my-feature

git add .

git commit -m "Add my feature"

git push origin feature/my-feature

Then create a pull request.

Before submitting:

pytest

and verify the API manually through:

http://localhost:8000/docs

⚠️ Agricultural Safety
AI-FAO-Assistant is an information and decision-support system.

AI-generated agricultural information should not automatically be treated as a professional diagnosis or a substitute for qualified agricultural, veterinary, pesticide-safety, food-safety, or other professional advice.

Particular care should be taken with:

Pesticide application

Chemical handling

Livestock health

Food safety

Plant disease diagnosis

Human health

Environmental hazards

The system should communicate uncertainty when information is incomplete.

📄 Documentation
Project documentation:

README.md
DEVELOPMENT.md
MONGODB_SETUP.md

Recommended additional documentation:

API.md
ARCHITECTURE.md
SECURITY.md
DEPLOYMENT.md
CONTRIBUTING.md

🌾 Project Vision
AI-FAO-Assistant aims to provide a modular platform where agricultural knowledge, AI, farmer information, and external agricultural services can work together.

The long-term architecture is:

             Agricultural Knowledge
                      +
                Farmer Data
                      +
                 AI / LLM
                      +
                    RAG
                      +
              Weather / Market
                      +
              Image Analysis
                      +
               Multilingual AI
                      |
                      v
             AI-FAO-Assistant

License
Add the project's chosen license here.

Example:

MIT License
