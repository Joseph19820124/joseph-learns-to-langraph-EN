# Quick Start Guide

## 🚀 Start Experimenting Immediately

### Step 1: Environment Preparation

#### 1. Clone the Original Project
```bash
# In your working directory
git clone https://github.com/google-gemini/gemini-fullstack-langgraph-quickstart.git
cd gemini-fullstack-langgraph-quickstart
```

#### 2. Set Up API Keys
```bash
# Enter backend directory
cd backend

# Copy environment variable template
cp .env.example .env

# Edit .env file, add your Gemini API key
echo 'GEMINI_API_KEY="your_actual_api_key_here"' > .env
```

#### 3. Install Dependencies
```bash
# Backend dependencies
cd backend
pip install .

# Frontend dependencies
cd ../frontend
npm install
```

### Step 2: Run the Project

#### Method 1: Using Makefile (Recommended)
```bash
# In project root directory
make dev
```

#### Method 2: Start Separately
```bash
# Terminal 1 - Start backend
cd backend
langgraph dev

# Terminal 2 - Start frontend
cd frontend
npm run dev
```

### Step 3: Test Functionality
- Open browser and visit `http://localhost:5173/app`
- Try asking a research question like: "What are the latest developments in quantum computing?"
- Observe the Agent's working process

## 🔬 Practice Exercises

### Exercise 1: Understanding the Workflow (30 minutes)

#### Goal
Observe and understand the complete workflow of the Agent

#### Steps
1. Start the application and open LangGraph UI (`http://127.0.0.1:2024`)
2. Ask a question in the frontend interface: "What are the recent major breakthroughs in artificial intelligence?"
3. Observe the execution trace in LangGraph UI
4. Record the input and output of each node

#### Observation Points
- [ ] What search queries were generated?
- [ ] How was the quality of search results?
- [ ] How many iterations did the Agent perform?
- [ ] Are the citation sources in the final answer accurate?

### Exercise 2: Modifying Prompts (45 minutes)

#### Goal
Change Agent behavior by modifying prompts

#### Steps
1. Open `backend/src/agent/prompts.py`
2. Find `QUERY_GENERATION_PROMPT`
3. Modify the prompt to make the Agent generate more diverse queries
4. Restart backend service and test the effect

#### Experimental Direction
```python
# Example modification of original prompt
QUERY_GENERATION_PROMPT = """
You are a professional search query generation expert.
Based on the user's question, generate 5-7 search queries from different angles.

Requirements:
1. Cover the core concepts of the question
2. Include relevant academic terminology
3. Consider time factors (latest, recent, trends)
4. Include different perspectives (technical, business, social impact)

User question: {question}

Please generate a list of search queries:
"""
```

### Exercise 3: Adding New Search Tools (60 minutes)

#### Goal
Integrate additional search sources, such as academic paper search

#### Steps
1. Add new tools in `backend/src/agent/tools_and_schemas.py`
2. Modify the search node in `graph.py`
3. Update state definition to support multi-source search

#### Implementation Example
```python
# Add in tools_and_schemas.py
def search_academic_papers(query: str) -> List[dict]:
    """Mock implementation for academic paper search"""
    # Here you can integrate arXiv API or other academic search services
    return [
        {
            "title": f"Academic paper about {query}",
            "url": "https://arxiv.org/example",
            "snippet": f"This paper discusses {query}...",
            "source": "arXiv"
        }
    ]
```

### Exercise 4: Frontend Interface Customization (45 minutes)

#### Goal
Optimize the user interface and add better visualization

#### Steps
1. Open `frontend/src/App.tsx`
2. Add search progress display
3. Improve citation source presentation
4. Add conversation history functionality

#### Improvement Directions
- Display search rounds and status
- Beautify citation link presentation
- Add copy answer functionality
- Implement dark theme toggle

## 🐛 Common Problem Solutions

### Problem 1: API Key Error
```
Error: Authentication failed
Solution: Check if GEMINI_API_KEY in .env file is correct
```

### Problem 2: Port Conflict
```
Error: Port 2024 is already in use
Solution: Close other programs using the port, or modify port in configuration file
```

### Problem 3: Dependency Installation Failed
```
Error: Package installation failed
Solution:
- Python: Ensure using Python 3.8+
- Node.js: Ensure using Node.js 18+
- Consider using virtual environment: python -m venv venv
```

### Problem 4: Search Function Not Working
```
Error: Search results empty
Solution:
- Check network connection
- Verify Google Search API configuration
- Check backend logs for detailed error information
```

## 📊 Performance Testing

### Test Script
Create a simple performance test:

```python
# test_performance.py
import time
import asyncio
from agent.app import graph

async def test_question(question: str):
    start_time = time.time()
    
    result = await graph.ainvoke({
        "messages": [{"role": "user", "content": question}]
    })
    
    end_time = time.time()
    return {
        "question": question,
        "duration": end_time - start_time,
        "iterations": result.get("reflection_count", 0),
        "answer_length": len(result.get("final_answer", ""))
    }

# Test questions of different complexity
test_questions = [
    "What is Python?",  # Simple
    "Latest trends in machine learning",  # Medium
    "Comprehensive analysis of quantum computing impact on cryptography"  # Complex
]
```

## 🎯 Learning Checkpoints

### Basic Understanding ✅
- [ ] Successfully run the original project
- [ ] Understand the Agent's workflow
- [ ] Can explain the role of each node

### Code Modification ✅
- [ ] Successfully modify prompts and see effects
- [ ] Understand state passing between nodes
- [ ] Can add simple log output

### Feature Extension ✅
- [ ] Try integrating new tools or APIs
- [ ] Modify frontend interface and improve user experience
- [ ] Understand frontend-backend communication mechanisms

### Deployment & Operations ✅
- [ ] Successfully deploy using Docker
- [ ] Understand the role of configuration files
- [ ] Can troubleshoot common problems

## 🔗 Useful Links

- [Original Project Repository](https://github.com/google-gemini/gemini-fullstack-langgraph-quickstart)
- [LangGraph Official Documentation](https://langchain-ai.github.io/langgraph/)
- [Google Gemini API](https://ai.google.dev/)
- [React Documentation](https://react.dev/)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)

---

**Remember: Learn by doing, problems are great learning opportunities!** 🎉
