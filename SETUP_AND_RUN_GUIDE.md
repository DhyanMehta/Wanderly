# 🌍 AI Trip Planner - Setup & Run Guide

## Project Overview
This is a **Travel Planning Agentic Application** that uses AI agents with LLM (Large Language Models) to create detailed travel plans. The system is built with:
- **Backend**: FastAPI server running agents
- **Frontend**: Streamlit web interface
- **LLM Providers**: Groq or OpenAI
- **Tools**: Weather, Places, Currency Conversion, Expense Calculator

---

## ✅ Code Analysis Results

### No Syntax Errors Found ✓
All Python files are syntactically correct and ready to run.

### Fixed Issues
✅ **Filename Typo Fixed**: `exception/exceptiohandling.py` → `exception/exceptionhandling.py`

---

## 📋 Required API Keys & Where to Get Them

### 1. **Groq API Key** (Recommended - Free, Fast)
   - **Purpose**: LLM for main agent reasoning
   - **Get it**: https://console.groq.com/keys
   - **Sign Up**: Free account at groq.com
   - **Steps**:
     1. Go to https://console.groq.com/
     2. Sign up with email
     3. Click "API Keys" in the sidebar
     4. Create new API key
     5. Copy and save in `.env` as `GROQ_API_KEY`
   - **Status**: ⭐ **PRIMARY (Required)**

### 2. **OpenAI API Key** (Optional Alternative)
   - **Purpose**: Alternative LLM provider
   - **Get it**: https://platform.openai.com/api-keys
   - **Sign Up**: https://platform.openai.com/signup
   - **Steps**:
     1. Create/login to OpenAI account
     2. Go to API Keys section
     3. Create new secret key
     4. Copy and save in `.env` as `OPENAI_API_KEY`
   - **Cost**: Pay-as-you-go (Charges apply)
   - **Status**: 🔵 **Optional (Alternative)**

### 3. **OpenWeather Map API Key** (Weather Information)
   - **Purpose**: Get weather data for destinations
   - **Get it**: https://openweathermap.org/api
   - **Sign Up**: Free account at openweathermap.org
   - **Steps**:
     1. Sign up at https://openweathermap.org/
     2. Go to API Keys section
     3. You'll get a default key "Default"
     4. Copy and save in `.env` as `OPENWEATHERMAP_API_KEY`
   - **Status**: ⭐ **Required**

### 4. **Google Places API Key** (Places & Attractions)
   - **Purpose**: Search attractions, restaurants, activities, transportation
   - **Get it**: https://console.cloud.google.com/
   - **Steps**:
     1. Go to Google Cloud Console: https://console.cloud.google.com/
     2. Create a new project
     3. Enable these APIs:
        - Maps JavaScript API
        - Places API
     4. Create an API key (Credentials → Create Credentials → API Key)
     5. Copy and save in `.env` as `GPLACES_API_KEY`
   - **Cost**: Pay-per-request ($7 per 1000 requests for Places search)
   - **Status**: ⭐ **Required**

### 5. **Exchange Rate API Key** (Currency Conversion)
   - **Purpose**: Convert currencies in travel plans
   - **Get it**: https://www.exchangerate-api.com/
   - **Sign Up**: Free account available
   - **Steps**:
     1. Go to https://www.exchangerate-api.com/
     2. Sign up (free plan: 1500 requests/month)
     3. Check your email for API key
     4. Copy and save in `.env` as `EXCHANGE_RATE_API_KEY`
   - **Status**: ⭐ **Required**

### 6. **Tavily Search API Key** (Fallback Search)
   - **Purpose**: Fallback search when Google Places fails
   - **Get it**: https://tavily.com/
   - **Sign Up**: Free account
   - **Steps**:
     1. Go to https://tavily.com/
     2. Sign up
     3. Get your API key from dashboard
     4. Copy and save in `.env` as `TAVILY_API_KEY`
   - **Status**: 🟢 **Recommended (Fallback)**

### 7. **Alpha Vantage API Key** (Optional)
   - **Purpose**: Additional currency conversion option
   - **Get it**: https://www.alphavantage.co/
   - **Status**: 🔵 **Optional**

---

## 🚀 Project Setup & Running

### Step 1: Install Dependencies
```bash
# Navigate to project directory
cd c:\Users\hp\Desktop\AI_Trip_Planner

# Install required packages
pip install -r requirements.txt
```

### Step 2: Create .env File
```bash
# Copy the example file
copy .env.example .env

# Edit .env file with your actual API keys
# Open .env in your editor and fill in all the API keys
```

**Important**: Never commit `.env` to git (already in .gitignore ✓)

### Step 3: Run the FastAPI Backend Server
```bash
# Start the FastAPI server on localhost:8000
uvicorn main:app --reload --host localhost --port 8000
```

**Expected output**:
```
INFO:     Started server process [xxxx]
INFO:     Waiting for application startup
INFO:     Application startup complete
INFO:     Uvicorn running on http://localhost:8000
INFO:     Press CTRL+C to quit
```

### Step 4: Run the Streamlit Frontend (In Another Terminal)
```bash
# Open a new terminal/PowerShell window
cd c:\Users\hp\Desktop\AI_Trip_Planner

# Run Streamlit app
streamlit run streamlit_app.py
```

**Expected output**:
```
  You can now view your Streamlit app in your browser.

  Local URL: http://localhost:8501
```

### Step 5: Use the Application
1. Open your browser: `http://localhost:8501`
2. Enter your travel query (e.g., "Plan a trip to Goa for 5 days")
3. Click "Send"
4. Wait for the AI agent to generate your travel plan
5. View the comprehensive travel plan with day-by-day itinerary, costs, weather, etc.

---

## 📁 Project Structure

```
AI_Trip_Planner/
├── main.py                 # FastAPI backend server
├── streamlit_app.py        # Streamlit web interface
├── requirements.txt        # Python dependencies
├── .env.example           # Template for API keys
├── config/
│   └── config.yaml        # LLM configuration
├── agent/
│   └── agentic_workflow.py # Main agent logic
├── tools/                 # Agent tools
│   ├── weather_info_tool.py
│   ├── place_search_tool.py
│   ├── currency_conversion_tool.py
│   └── expense_calculator_tool.py
├── utils/                 # Utility functions
│   ├── model_loader.py
│   ├── config_loader.py
│   ├── weather_info.py
│   ├── place_info_search.py
│   └── currency_converter.py
├── prompt_library/
│   └── prompt.py          # System prompt for agent
└── exception/
    └── exceptionhandling.py
```

---

## 🔧 Configuration

### LLM Selection
Edit `config/config.yaml` to switch between providers:

```yaml
llm:
  groq:
    provider: "groq"
    model_name: "deepseek-r1-distill-llama-70b"  # or other Groq models
  openai:
    provider: "openai"
    model_name: "gpt-4-mini"
```

### Run with Groq (Default - Recommended)
```bash
# In main.py, the default is already set to Groq
graph = GraphBuilder(model_provider="groq")
```

### Run with OpenAI
```python
# Modify in main.py if you want to use OpenAI
graph = GraphBuilder(model_provider="openai")
```

---

## ⚙️ LM Studio Models Support

The project is configured to use cloud-based LLMs (Groq/OpenAI) by default. To use **local LLMs with LM Studio**:

1. Download LM Studio from https://lmstudio.ai/
2. Import a model (e.g., DeepSeek, Llama)
3. Start the local server (typically on port 1234)
4. Modify `utils/model_loader.py` to connect to local server

---

## 🛠️ Troubleshooting

### Issue: "API Key not found"
- **Solution**: Make sure `.env` file exists in project root with all required keys

### Issue: "Connection refused on localhost:8000"
- **Solution**: Make sure FastAPI server is running in another terminal

### Issue: "Google Places API not working"
- **Solution**: Verify API is enabled in Google Cloud Console and API key has correct permissions

### Issue: "Streamlit app not loading"
- **Solution**: Check if fastapi backend is running and accessible

### Issue: "ModuleNotFoundError"
- **Solution**: Ensure all dependencies are installed: `pip install -r requirements.txt`

---

## 📊 Agent Capabilities

The AI agent can:
✅ Create detailed day-by-day itineraries
✅ Find attractions and tourist spots
✅ Recommend restaurants with prices
✅ Suggest activities and experiences
✅ Provide transportation information
✅ Calculate trip expenses and budgets
✅ Show weather forecasts
✅ Convert currencies
✅ Offer both mainstream and off-beat destination suggestions

---

## 📝 Summary

| Component | Status | Notes |
|-----------|--------|-------|
| Code Syntax | ✅ No errors | All files clean |
| Filename Typo | ✅ Fixed | exceptiohandling.py renamed |
| API Keys Needed | 7 total | 5 required, 2 optional/fallback |
| Backend Server | Ready | FastAPI on port 8000 |
| Frontend | Ready | Streamlit on port 8501 |
| Configuration | Ready | config.yaml pre-configured |

---

## 🎯 Next Steps

1. ✅ Get all API keys from links provided above
2. ✅ Create `.env` file with your API keys
3. ✅ Run: `pip install -r requirements.txt`
4. ✅ Run: `uvicorn main:app --reload`
5. ✅ Run: `streamlit run streamlit_app.py` (in new terminal)
6. ✅ Open http://localhost:8501 and start planning trips!

---

**Happy Travel Planning! 🌍✈️**
