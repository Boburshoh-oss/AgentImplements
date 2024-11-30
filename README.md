# Task Maistro - Intelligent Task Management Assistant

An AI-powered task management system that combines natural language processing with sophisticated memory management to create an intuitive and intelligent task tracking experience.

## 🌟 Key Features

### Task Management
- **Natural Language Input**: Create and manage tasks using everyday language
  ```python
  "Schedule a team meeting for next Tuesday at 2 PM"
  "Remind me to follow up with Sarah about the project proposal"
  ```

- **Smart Deadline Handling**: Automatically interprets and sets deadlines
  ```python
  "I need to finish the report by end of day Friday"
  # Automatically sets deadline to Friday 23:59:59
  ```

- **Task Prioritization**: Intelligent sorting and prioritization of tasks
  ```python
  "What are my highest priority tasks for this week?"
  "Show me overdue items"
  ```

### Memory System
- **User Profile Management**: Maintains detailed user information
  ```python
  class Profile(BaseModel):
      name: Optional[str]
      location: Optional[str]
      job: Optional[str]
      connections: list[str]
      interests: list[str]
  ```

- **Context-Aware Responses**: Personalizes interactions based on user history
  ```python
  # System remembers user preferences and past interactions
  "What's my next task related to the website redesign project?"
  ```

### Task Schema
python
class ToDo(BaseModel):
task: str
time_to_complete: Optional[int] # in minutes
deadline: Optional[datetime]
solutions: list[str]
status: Literal["not started", "in progress", "done", "archived"]


## 🚀 Getting Started

### Prerequisites
- Python 3.11+
- Docker (for deployment)
- OpenAI API key
- LangChain API key

### Local Development Setup

1. **Clone and Setup**
   ```bash
   git clone <repository-url>
   cd task-maistro
   python -m venv venv
   source venv/bin/activate  # On Windows: .\venv\Scripts\activate
   ```

2. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Environment Configuration**
   Create a `.env` file:
   ```env
   OPENAI_API_KEY=your_openai_key
   LANGCHAIN_API_KEY=your_langchain_key
   LANGCHAIN_TRACING_V2=true
   LANGCHAIN_PROJECT=task-maistro
   ```

4. **Run Development Server**
   ```bash
   langgraph serve
   ```

### Docker Deployment

1. **Build the Image**
   ```bash
   cd deployment
   docker build -t task-maistro .
   ```

2. **Configure Docker Compose**
   ```yaml
   services:
     langgraph-api:
       image: "task-maistro"
       ports:
         - "8123:8000"
       environment:
         OPENAI_API_KEY: ${OPENAI_API_KEY}
         LANGCHAIN_API_KEY: ${LANGCHAIN_API_KEY}
   ```

3. **Run the Stack**
   ```bash
   docker compose up
   ```

## 💡 Usage Examples

### Task Creation
python
Simple task
"Create a task to review the quarterly report"
Task with deadline and estimated time
"I need to prepare the presentation by next Thursday, it should take about 2 hours"
Task with multiple steps
"Set up a new project with the following steps:
1. Initial team meeting
2. Requirements gathering
3. Project timeline creation"


### Task Management
python
"Mark the task as done"
"What is the status of the project timeline creation task?"


# Add solutions to a task
"Add a solution to the task of creating the project timeline"
"What are the solutions to the task of creating the project timeline?"


1. Use Material UI components

2. Implement responsive design

3. Optimize for mobile


# Query tasks

"Show me all tasks due this week"
"Show me all tasks overdue"

### Memory Integration
The system remembers user context
User: "I work in marketing"
Assistant: stores information in profile
Later...
User: "Show me my tasks"
Assistant: prioritizes marketing-related tasks in response


## 🔧 Advanced Configuration

### Custom Memory Store

python
from langgraph.store.base import BaseStore
class CustomStore(BaseStore):
def init(self):
self.store = {}
async def get(self, key: str) -> dict:
return self.store.get(key, {})
async def set(self, key: str, value: dict) -> None:
self.store[key] = value


### Deployment Configuration
json
{
"dockerfile_lines": [],
"graphs": {
"task_maistro": "./task_maistro.py:graph"
},
"python_version": "3.11",
"dependencies": [
"."
]
}


## 🔍 Monitoring and Debugging

### LangSmith Integration
- Access traces at: https://smith.langchain.com/
- Monitor API calls and performance
- Debug conversation flows

### Local Logging

python
import logging
logging.basicConfig(
level=logging.INFO,
format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)

## 🤝 Contributing

### Development Workflow
1. Fork the repository
2. Create a feature branch
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. Implement changes
4. Run tests
   ```bash
   pytest tests/
   ```
5. Submit PR

### Code Style
- Follow PEP 8
- Use type hints
- Document functions and classes
- Add tests for new features

## 📚 API Documentation

### Task Management Endpoints
- `POST /tasks/create` - Create new task
- `PUT /tasks/{task_id}` - Update task
- `GET /tasks/list` - List all tasks
- `DELETE /tasks/{task_id}` - Delete task

### Memory Management Endpoints
- `GET /memory/{user_id}` - Get user memory
- `POST /memory/{user_id}` - Update user memory

## 🔐 Security

- API Authentication required
- Rate limiting implemented
- Data encryption in transit and at rest
- Regular security audits

## 📄 License

[Add your license information here]

## 🙏 Acknowledgments

- LangGraph Team
- LangChain Community
- OpenAI