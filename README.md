# DoppleChat-The-AI-Chat-Persona-System
An innovative approach to understanding

## Project Overview

DoppleChat is an advanced AI-based intelligent agent system that creates personalized AI personas from WhatsApp chat exports. The system analyzes conversation patterns, writing styles, and personality traits to generate AI personas that can chat in the style of specific individuals.

## AI Agent Semester Project - Requirements Compliance

### Core Features Implemented

#### 1. Data Source & Dataset
- **WhatsApp Chat Parser**: Supports uploading exported WhatsApp chat files (.txt format)
- **Multiple Query Types**:
  - Search and extract messages by person name
  - Filter and clean messages (remove media, deleted messages)
  - Categorize messages by sender

#### 2. AI Reasoning & Analytics Features (4+ Required)

##### Mandatory: Agent Memory
- **Conversation History**: Stores all user-AI interactions in database
- **Long-term Memory**: Maintains persona context across sessions
- **Context-Aware Responses**: Uses conversation history for coherent dialogue

##### Feature 2: Summarization
- **Persona Summary Generation**: Creates comprehensive summaries of communication styles
- **Writing Style Analysis**: Generates detailed behavioral profiles

##### Feature 3: Classification & Categorization
- **Message Intent Classification**: Classifies messages into categories (greeting, question, statement, etc.)
- **Sender Classification**: Separates messages by different participants

##### Feature 4: Pattern Detection
- **Writing Pattern Analysis**: Detects emoji usage patterns, message length patterns
- **Communication Style Detection**: Identifies formal/informal patterns, question/exclamation usage

##### Bonus: Trend Analysis
- **Message Statistics**: Analyzes message frequency and characteristics
- **Behavioral Trends**: Tracks communication patterns over time

##### Bonus: Rule-based Decision-making
- **Validation Rules**: Pydantic models enforce data quality rules
- **Error Handling**: Comprehensive rule-based error detection

##### Bonus: LLM-based Explanation & Analysis
- **Gemini 2.5 Flash Integration**: Advanced AI analysis and response generation
- **Persona Profiling**: Deep personality and style analysis

#### 3. Database & Storage (SQLite3)
- **ChatInfo Table**: Stores persona profiles and chat data
- **SelectedChat Table**: Manages active chat selection
- **ConversationHistory Table**: Logs all conversations
- **SystemLog Table**: Records system events and errors

#### 4. Pydantic Validation Models (2+ Required)
- **ChatUploadValidator**: Validates file uploads and person names
- **PersonaSummaryValidator**: Ensures quality of generated personas
- **ConversationValidator**: Validates chat messages

#### 5. User Interface
- **Modern Web UI**: Built with Django templates and Tailwind CSS
- **WhatsApp-like Design**: Familiar chat interface
- **Responsive Layout**: Works on different screen sizes
- **Real-time Messaging**: AJAX-based chat functionality

## Technical Architecture

### Backend
- **Framework**: Django 6.0
- **Database**: SQLite3
- **AI Model**: Google Gemini 2.5 Flash
- **Validation**: Pydantic 2.12.5
- **Logging**: Python logging + Database logging

### Frontend
- **Templates**: Django Templates
- **Styling**: Tailwind CSS 3.x
- **JavaScript**: Vanilla JS (minimal, as requested)
- **Animations**: CSS animations with Tailwind

### Project Structure
```
double/
├── chatapp/
│   ├── models.py              # Django ORM models
│   ├── views.py               # Views with error handling
│   ├── admin.py               # Admin interface configuration
│   ├── urls.py                # URL routing
│   ├── utils/
│   │   ├── validators.py      # Pydantic validation models
│   │   ├── whatsapp_parser.py # WhatsApp chat parser
│   │   ├── gemini_service.py  # Gemini AI integration
│   │   └── logger.py          # Logging utilities
│   ├── templates/
│   │   └── chatapp/
│   │       ├── base.html      # Base template
│   │       └── home.html      # Main chat interface
│   └── static/
│       ├── css/
│       └── js/
├── dopplechat/
│   ├── settings.py            # Django settings
│   ├── urls.py                # Main URL configuration
│   └── wsgi.py
├── manage.py
├── requirements.txt
├── .env                       # Environment variables
├── .gitignore
└── README.md
```

## Installation & Setup

### Prerequisites
- Python 3.10 or higher
- Google Gemini API key

### Step 1: Clone and Setup Virtual Environment
```bash
cd double
python -m venv venv

# Windows
.\venv\Scripts\activate

# Linux/Mac
source venv/bin/activate
```

### Step 2: Install Dependencies
```bash
pip install -r requirements.txt
```

### Step 3: Configure Environment Variables
Edit the `.env` file:
```
GEMINI_API_KEY=your_actual_gemini_api_key
SECRET_KEY=your_django_secret_key
DEBUG=True
```

**Get Gemini API Key**: https://makersuite.google.com/app/apikey

### Step 4: Run Migrations
```bash
python manage.py makemigrations
python manage.py migrate
```

### Step 5: Create Superuser (Optional)
```bash
python manage.py createsuperuser
```

### Step 6: Run the Server
```bash
python manage.py runserver
```

Access the application at: `http://127.0.0.1:8000/`

## Usage Guide

### 1. Export WhatsApp Chat
- Open WhatsApp on your phone
- Go to the chat you want to export
- Tap the 3 dots menu → **More** → **Export chat**
- Choose **Without Media**
- Send the .txt file to your computer

### 2. Upload Chat to DoppleChat
- Click **Upload Chat** button
- Enter the exact name as it appears in the chat
- Select the exported .txt file
- Click **Upload**

### 3. Chat with AI Persona
- Select the uploaded chat from the sidebar
- Type messages in the input box
- The AI will respond in the persona's style

### 4. Delete Chat
- Click the trash icon next to any chat in the sidebar
- Confirm deletion

## Features & Functionality

### WhatsApp Chat Parser
- Supports multiple WhatsApp export formats
- Extracts messages by specific person
- Cleans and filters messages
- Analyzes writing style patterns

### AI Persona Generation
- Creates detailed personality profiles
- Analyzes communication style
- Detects emoji usage patterns
- Identifies tone and mood

### Conversation System
- Context-aware responses
- Maintains conversation history
- Mimics original person's style
- Natural dialogue flow

### Error Handling
- Comprehensive try-catch blocks
- User-friendly error messages
- Detailed logging system
- Input validation at every step

### Logging System
- File-based logging (logs/dopplechat.log)
- Database logging (SystemLog table)
- Multiple log levels (INFO, WARNING, ERROR)
- Detailed error tracking

## Database Schema

### ChatInfo
- `chat_id` (PK): Auto-generated chat identifier
- `person_name`: Name of the persona
- `cleaned_chat`: JSON array of messages
- `persona_summary`: AI-generated personality profile
- `raw_file_name`: Original filename
- `created_at`: Creation timestamp
- `updated_at`: Last update timestamp

### SelectedChat
- `id` (PK): Selection identifier
- `chat_id` (FK): Reference to ChatInfo
- `active`: Boolean flag for active chat
- `selected_at`: Selection timestamp

### ConversationHistory
- `id` (PK): Message identifier
- `chat_id` (FK): Reference to ChatInfo
- `user_message`: User's input
- `ai_response`: AI's reply
- `timestamp`: Message timestamp

### SystemLog
- `id` (PK): Log identifier
- `level`: Log level (INFO, WARNING, ERROR)
- `message`: Log message
- `module`: Source module name
- `timestamp`: Log timestamp
- `extra_data`: JSON metadata

## AI Features Breakdown

### 1. Agent Memory
- Stores last 10 messages in context
- Maintains persona consistency
- Cross-session memory persistence

### 2. Summarization
- Analyzes 50+ messages for persona
- Creates 200+ word summaries
- Includes style, tone, and patterns

### 3. Classification
- Message intent classification
- Sender categorization
- Content type filtering

### 4. Pattern Detection
- Emoji usage patterns
- Message length analysis
- Question/exclamation frequency
- Communication style patterns

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Home page with chat interface |
| `/upload/` | POST | Upload WhatsApp chat file |
| `/select/<chat_id>/` | POST | Select active chat |
| `/delete/<chat_id>/` | POST | Delete chat persona |
| `/send-message/` | POST | Send message to AI |
| `/messages/<chat_id>/` | GET | Retrieve conversation history |

## Testing & Evaluation

### Manual Testing Checklist
- Upload valid WhatsApp chat
- Upload invalid file (error handling)
- Upload with wrong person name (error handling)
- Send messages to AI persona
- Switch between multiple personas
- Delete chat
- View conversation history
- Check database logging

### Validation Tests
- Pydantic model validation
- WhatsApp format detection
- Empty file handling
- Invalid encoding handling

## Challenges & Solutions

### Challenge 1: WhatsApp Format Variations
**Solution**: Multiple regex patterns to handle different export formats

### Challenge 2: Persona Quality
**Solution**: Comprehensive Pydantic validation with quality checks

### Challenge 3: Context Management
**Solution**: Database-backed conversation history with sliding window

### Challenge 4: Error Handling
**Solution**: Try-catch at every level with user-friendly messages

## Future Enhancements

- Multi-language support
- Voice message analysis
- Emotion detection in responses
- Advanced analytics dashboard
- Export conversation history
- Multiple active chats
- Chat search functionality
- Persona customization options

## Code Quality

### Clean Code Principles
- Meaningful variable and function names
- Single responsibility principle
- DRY (Don't Repeat Yourself)
- Comprehensive error handling
- Extensive logging
- Type hints and validation

### Best Practices
- Virtual environment isolation
- Environment variable configuration
- Git version control
- Comprehensive documentation
- Modular architecture
- Separation of concerns

## Troubleshooting

### Issue: Gemini API Error
- Check if API key is set correctly in `.env`
- Verify API key is valid
- Check internet connection

### Issue: Chat Upload Fails
- Ensure file is .txt format
- Check person name matches exactly
- Verify file encoding (UTF-8 or UTF-16)

### Issue: No Messages Loading
- Check browser console for JavaScript errors
- Verify chat is selected (highlighted in sidebar)
- Check database migrations are applied

## Credits

**Developed by**: [Arsal , Abdul Rehman , Samama , Ali]
**Course**: Artificial Intelligence
**Instructor**: Dr. Irfana Bibi
**Institution**: [Your Institution]
**Semester**: Fall 2025

## Contact & Support

For queries and support:
- Mr. Fazeel: bsef23m043@pucit.edu.pk
- Ms Adan: bsef23m025@pucit.edu.pk
- Ms Momina: bsef23m024@pucit.edu.pk

## License

This project is created for educational purposes as part of the AI semester project.

---

**Note**: This project demonstrates AI reasoning, data processing, automation, logging, and evaluation as required by the semester project guidelines.

