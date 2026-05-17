# 🚀 CITY EMPIRE BOT - COMPLETE BUILD PLAN
## Full Stack Telegram Bot + Web Control Panel

---

## 📦 **TECH STACK (ALL FREE)**

```yaml
Backend:
  - Python 3.11+
  - python-telegram-bot 20.x (Async)
  - FastAPI (Web server)
  - SQLite3 (Database - file-based, free)
  - asyncpg (if PostgreSQL later)
  
Frontend:
  - HTML5 + CSS3
  - Vanilla JavaScript (No frameworks needed)
  - Bootstrap 5 (CDN - free)
  - Socket.IO (Real-time communication)
  
AI Integration:
  - ShershaahXGames_ai (Custom module)
  - Groq API (Free tier - fast inference)
  - Multiple model support
  
Real-time:
  - python-socketio (Backend)
  - socket.io-client (Frontend)
  
File Management:
  - Monaco Editor (VS Code in browser)
  - File tree viewer
  
Process Management:
  - subprocess (Python built-in)
  - psutil (Process monitoring)
```

---

## 📁 **PROJECT STRUCTURE**

```
city_empire/
│
├── README.md
├── requirements.txt
├── .env                          # Environment variables
├── .env.example                  # Example env file
├── .gitignore
│
├── main.py                       # Bot entry point
├── web_server.py                 # Web control panel server
├── start.sh                      # Unix startup script
├── start.bat                     # Windows startup script
│
├── config/
│   ├── __init__.py
│   ├── settings.py               # Global settings
│   └── constants.py              # Game constants
│
├── core/
│   ├── __init__.py
│   ├── bot.py                    # Bot initialization
│   ├── database.py               # Database connection
│   ├── event_bus.py              # Event system
│   ├── plugin_loader.py          # Feature auto-loader
│   ├── base_feature.py           # Base class for features
│   └── process_manager.py        # Bot process control
│
├── features/
│   ├── __init__.py
│   │
│   ├── city/
│   │   ├── __init__.py
│   │   ├── handlers.py
│   │   ├── services.py
│   │   ├── models.py
│   │   ├── keyboards.py
│   │   └── config.yaml
│   │
│   ├── war/
│   │   ├── __init__.py
│   │   ├── handlers.py
│   │   ├── services.py
│   │   ├── models.py
│   │   ├── keyboards.py
│   │   └── config.yaml
│   │
│   ├── trade/
│   │   └── [same structure]
│   │
│   ├── spy/
│   │   └── [same structure]
│   │
│   ├── missions/
│   │   ├── __init__.py
│   │   ├── handlers.py
│   │   ├── services.py
│   │   ├── ai_generator.py       # Uses ShershaahXGames_ai
│   │   ├── models.py
│   │   ├── keyboards.py
│   │   └── config.yaml
│   │
│   └── [more features...]
│
├── ai_module/
│   ├── __init__.py
│   ├── ShershaahXGames_ai.py     # Your AI module
│   ├── groq_client.py            # Groq API wrapper
│   └── prompts.py                # AI prompts
│
├── utils/
│   ├── __init__.py
│   ├── decorators.py
│   ├── validators.py
│   ├── formatters.py
│   ├── helpers.py
│   └── logger.py                 # Logging system
│
├── migrations/
│   ├── 001_initial_schema.sql
│   ├── 002_add_missions.sql
│   └── [auto-generated]
│
├── web/
│   ├── static/
│   │   ├── css/
│   │   │   ├── style.css
│   │   │   └── dashboard.css
│   │   ├── js/
│   │   │   ├── main.js
│   │   │   ├── socket-handler.js
│   │   │   ├── file-editor.js
│   │   │   └── feature-manager.js
│   │   └── img/
│   │       └── logo.png
│   │
│   └── templates/
│       ├── index.html            # Dashboard
│       ├── features.html         # Feature management
│       ├── file-editor.html      # Code editor
│       ├── logs.html             # Live logs
│       ├── settings.html         # Bot settings
│       ├── ai-config.html        # AI configuration
│       └── messages.html         # Send messages
│
├── data/
│   ├── bot.db                    # SQLite database
│   └── uploads/                  # File uploads
│
├── logs/
│   ├── bot.log
│   ├── web.log
│   └── errors.log
│
└── tests/
    ├── test_features.py
    └── [test files]
```

---

## 🔧 **STEP-BY-STEP BUILD INSTRUCTIONS**

### **PHASE 1: PROJECT SETUP**

```bash
# Create project directory
mkdir city_empire && cd city_empire

# Create all directories
mkdir -p {core,features,ai_module,utils,migrations,web/{static/{css,js,img},templates},data,logs,tests,config}

# Create __init__.py files
touch core/__init__.py features/__init__.py ai_module/__init__.py utils/__init__.py config/__init__.py
```

---

### **PHASE 2: REQUIREMENTS.TXT**

```txt
# requirements.txt

# Bot Framework
python-telegram-bot==20.7
python-telegram-bot[job-queue]==20.7

# Web Framework
fastapi==0.109.0
uvicorn[standard]==0.27.0
python-socketio==5.11.0
aiofiles==23.2.1

# Database
aiosqlite==0.19.0

# AI & ML
groq==0.4.2
httpx==0.26.0

# Utilities
python-dotenv==1.0.0
pyyaml==6.0.1
psutil==5.9.8
watchdog==4.0.0

# Development
pytest==8.0.0
pytest-asyncio==0.23.3
```

---

### **PHASE 3: ENVIRONMENT SETUP (.env)**

```bash
# .env.example

# Bot Configuration
BOT_TOKEN=your_telegram_bot_token_here
BOT_NAME=CityEmpireBot

# Database
DATABASE_PATH=data/bot.db

# Web Panel
WEB_HOST=0.0.0.0
WEB_PORT=8080
SECRET_KEY=your-secret-key-here

# AI Configuration
GROQ_API_KEY=your_groq_api_key_here
AI_MODEL=llama-3.1-70b-versatile
AI_TEMPERATURE=0.7
AI_MAX_TOKENS=1000

# Feature Toggles (comma-separated)
ENABLED_FEATURES=city,war,trade,spy,missions

# Logging
LOG_LEVEL=INFO
LOG_FILE=logs/bot.log

# Admin
ADMIN_USER_ID=your_telegram_user_id
```

---

### **PHASE 4: CORE MODULES**

#### **4.1: Database Module**

```python
# core/database.py

import aiosqlite
import os
from typing import Optional, List, Dict, Any
from contextlib import asynccontextmanager

class Database:
    """SQLite database manager with async support"""
    
    def __init__(self, db_path: str = "data/bot.db"):
        self.db_path = db_path
        self._connection: Optional[aiosqlite.Connection] = None
    
    async def connect(self):
        """Initialize database connection"""
        os.makedirs(os.path.dirname(self.db_path), exist_ok=True)
        self._connection = await aiosqlite.connect(self.db_path)
        self._connection.row_factory = aiosqlite.Row
        await self._run_migrations()
    
    async def disconnect(self):
        """Close database connection"""
        if self._connection:
            await self._connection.close()
    
    async def execute(self, query: str, *args) -> aiosqlite.Cursor:
        """Execute a query"""
        cursor = await self._connection.execute(query, args)
        await self._connection.commit()
        return cursor
    
    async def fetchone(self, query: str, *args) -> Optional[Dict]:
        """Fetch single row"""
        cursor = await self._connection.execute(query, args)
        row = await cursor.fetchone()
        return dict(row) if row else None
    
    async def fetchall(self, query: str, *args) -> List[Dict]:
        """Fetch all rows"""
        cursor = await self._connection.execute(query, args)
        rows = await cursor.fetchall()
        return [dict(row) for row in rows]
    
    async def fetchval(self, query: str, *args) -> Any:
        """Fetch single value"""
        row = await self.fetchone(query, *args)
        return list(row.values())[0] if row else None
    
    async def _run_migrations(self):
        """Run SQL migrations"""
        migrations_dir = "migrations"
        if not os.path.exists(migrations_dir):
            return
        
        # Create migrations table
        await self.execute("""
            CREATE TABLE IF NOT EXISTS migrations (
                id INTEGER PRIMARY KEY,
                filename TEXT UNIQUE,
                executed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
            )
        """)
        
        # Get executed migrations
        executed = await self.fetchall("SELECT filename FROM migrations")
        executed_files = {row['filename'] for row in executed}
        
        # Run new migrations
        migration_files = sorted([
            f for f in os.listdir(migrations_dir)
            if f.endswith('.sql')
        ])
        
        for filename in migration_files:
            if filename not in executed_files:
                filepath = os.path.join(migrations_dir, filename)
                with open(filepath, 'r') as f:
                    sql = f.read()
                
                await self._connection.executescript(sql)
                await self.execute(
                    "INSERT INTO migrations (filename) VALUES (?)",
                    filename
                )
                print(f"  ✓ Migration: {filename}")

# Global database instance
db = Database()
```

#### **4.2: Event Bus**

```python
# core/event_bus.py

from typing import Callable, Dict, List, Any
import asyncio
from utils.logger import logger

class EventBus:
    """Event-driven communication between features"""
    
    def __init__(self):
        self._listeners: Dict[str, List[Callable]] = {}
        self._middleware: List[Callable] = []
    
    def on(self, event_name: str):
        """Register event listener decorator"""
        def decorator(func: Callable):
            if event_name not in self._listeners:
                self._listeners[event_name] = []
            self._listeners[event_name].append(func)
            logger.info(f"📡 Registered listener for: {event_name}")
            return func
        return decorator
    
    async def emit(self, event_name: str, data: dict):
        """Emit event to all listeners"""
        logger.debug(f"📤 Event: {event_name}")
        
        # Run middleware
        for middleware in self._middleware:
            data = await middleware(event_name, data)
            if data is None:
                return
        
        # Call listeners
        if event_name in self._listeners:
            tasks = []
            for listener in self._listeners[event_name]:
                tasks.append(self._safe_call(listener, data))
            await asyncio.gather(*tasks, return_exceptions=True)
    
    async def _safe_call(self, func: Callable, data: dict):
        """Safely call listener with error handling"""
        try:
            return await func(data)
        except Exception as e:
            logger.error(f"❌ Listener error: {e}")
    
    def add_middleware(self, middleware: Callable):
        """Add middleware for all events"""
        self._middleware.append(middleware)

# Global event bus
event_bus = EventBus()
```

#### **4.3: Plugin Loader**

```python
# core/plugin_loader.py

import os
import importlib
from pathlib import Path
from typing import List, Dict
from utils.logger import logger
import yaml

class PluginLoader:
    """Auto-load features from features/ directory"""
    
    def __init__(self, features_dir: str = "features"):
        self.features_dir = Path(features_dir)
        self.loaded_features: Dict[str, dict] = {}
        self.enabled_features: List[str] = []
    
    async def load_all_features(self, enabled_only: bool = True):
        """Discover and load all features"""
        logger.info("🔌 Loading features...")
        
        # Get enabled features from env
        from config.settings import ENABLED_FEATURES
        self.enabled_features = ENABLED_FEATURES
        
        # Scan features directory
        for feature_dir in self.features_dir.iterdir():
            if feature_dir.is_dir() and not feature_dir.name.startswith("_"):
                feature_name = feature_dir.name
                
                # Check if feature is enabled
                if enabled_only and feature_name not in self.enabled_features:
                    logger.info(f"  ⏸️  {feature_name} (disabled)")
                    continue
                
                await self.load_feature(feature_name)
        
        logger.info(f"✅ Loaded {len(self.loaded_features)} features")
    
    async def load_feature(self, feature_name: str):
        """Load a single feature"""
        try:
            # Load config
            config = self._load_config(feature_name)
            
            # Import module
            module_path = f"features.{feature_name}"
            module = importlib.import_module(module_path)
            
            # Call setup if exists
            if hasattr(module, "setup"):
                await module.setup()
            
            self.loaded_features[feature_name] = config
            logger.info(f"  ✓ {feature_name} v{config.get('version', '1.0.0')}")
            
        except Exception as e:
            logger.error(f"  ✗ {feature_name}: {e}")
    
    def _load_config(self, feature_name: str) -> dict:
        """Load feature config.yaml"""
        config_path = self.features_dir / feature_name / "config.yaml"
        if config_path.exists():
            with open(config_path) as f:
                return yaml.safe_load(f)
        return {}
    
    async def reload_feature(self, feature_name: str):
        """Reload a feature (for live updates)"""
        logger.info(f"🔄 Reloading {feature_name}...")
        
        # Unload
        if feature_name in self.loaded_features:
            del self.loaded_features[feature_name]
        
        # Reload module
        module_path = f"features.{feature_name}"
        if module_path in sys.modules:
            importlib.reload(sys.modules[module_path])
        
        # Load again
        await self.load_feature(feature_name)
    
    def get_feature_info(self, feature_name: str) -> dict:
        """Get feature configuration"""
        return self.loaded_features.get(feature_name, {})
    
    def list_all_features(self) -> List[str]:
        """List all available features (enabled + disabled)"""
        features = []
        for feature_dir in self.features_dir.iterdir():
            if feature_dir.is_dir() and not feature_dir.name.startswith("_"):
                features.append(feature_dir.name)
        return features

# Global plugin loader
plugin_loader = PluginLoader()
```

#### **4.4: Process Manager**

```python
# core/process_manager.py

import subprocess
import psutil
import os
import signal
from typing import Optional
from utils.logger import logger

class ProcessManager:
    """Manage bot process - start/stop/restart"""
    
    def __init__(self):
        self.process: Optional[subprocess.Popen] = None
        self.pid: Optional[int] = None
    
    async def start_bot(self):
        """Start the bot process"""
        if self.is_running():
            logger.warning("⚠️  Bot already running")
            return False
        
        try:
            # Start bot in separate process
            self.process = subprocess.Popen(
                ["python", "main.py"],
                stdout=subprocess.PIPE,
                stderr=subprocess.PIPE,
                text=True,
                bufsize=1
            )
            self.pid = self.process.pid
            
            logger.info(f"✅ Bot started (PID: {self.pid})")
            return True
            
        except Exception as e:
            logger.error(f"❌ Failed to start bot: {e}")
            return False
    
    async def stop_bot(self):
        """Stop the bot process"""
        if not self.is_running():
            logger.warning("⚠️  Bot not running")
            return False
        
        try:
            # Graceful shutdown
            if self.process:
                self.process.terminate()
                self.process.wait(timeout=10)
            
            # Force kill if still running
            if self.is_running():
                os.kill(self.pid, signal.SIGKILL)
            
            self.process = None
            self.pid = None
            
            logger.info("✅ Bot stopped")
            return True
            
        except Exception as e:
            logger.error(f"❌ Failed to stop bot: {e}")
            return False
    
    async def restart_bot(self):
        """Restart the bot"""
        logger.info("🔄 Restarting bot...")
        await self.stop_bot()
        await asyncio.sleep(2)
        return await self.start_bot()
    
    def is_running(self) -> bool:
        """Check if bot is running"""
        if self.pid is None:
            return False
        
        try:
            process = psutil.Process(self.pid)
            return process.is_running()
        except psutil.NoSuchProcess:
            return False
    
    def get_status(self) -> dict:
        """Get bot status info"""
        if not self.is_running():
            return {
                "running": False,
                "pid": None,
                "cpu": 0,
                "memory": 0
            }
        
        try:
            process = psutil.Process(self.pid)
            return {
                "running": True,
                "pid": self.pid,
                "cpu": process.cpu_percent(),
                "memory": process.memory_info().rss / 1024 / 1024  # MB
            }
        except:
            return {"running": False}

# Global process manager
process_manager = ProcessManager()
```

---

### **PHASE 5: AI MODULE**

```python
# ai_module/ShershaahXGames_ai.py

import os
from typing import Optional, Dict, Any
from groq import Groq
from utils.logger import logger

class ShershaahXGames_AI:
    """AI Module using Groq API"""
    
    def __init__(self):
        self.api_key = os.getenv("GROQ_API_KEY")
        self.model = os.getenv("AI_MODEL", "llama-3.1-70b-versatile")
        self.client = None
        
        if self.api_key:
            self.client = Groq(api_key=self.api_key)
    
    async def generate(
        self, 
        prompt: str, 
        system_prompt: Optional[str] = None,
        temperature: float = 0.7,
        max_tokens: int = 1000
    ) -> str:
        """Generate AI response"""
        
        if not self.client:
            logger.error("❌ Groq API key not configured")
            return "AI not configured"
        
        try:
            messages = []
            
            if system_prompt:
                messages.append({
                    "role": "system",
                    "content": system_prompt
                })
            
            messages.append({
                "role": "user",
                "content": prompt
            })
            
            # Call Groq API
            response = self.client.chat.completions.create(
                model=self.model,
                messages=messages,
                temperature=temperature,
                max_tokens=max_tokens
            )
            
            return response.choices[0].message.content
            
        except Exception as e:
            logger.error(f"❌ AI generation failed: {e}")
            return f"Error: {e}"
    
    async def generate_mission(self, city_data: Dict[str, Any]) -> Dict:
        """Generate daily mission for city"""
        
        system_prompt = """You are a game designer for City Empire.
Generate a challenging but achievable daily mission for the city.
Return ONLY valid JSON with this structure:
{
    "title": "Mission title with emoji",
    "description": "What player needs to do",
    "type": "build/war/trade/spy",
    "required_progress": 1,
    "rewards": {"gold": 1000, "xp": 500},
    "penalties": {"morale": -10},
    "mandatory": true/false,
    "expires_hours": 24
}"""
        
        prompt = f"""Generate mission for this city:
Level: {city_data.get('level', 1)}
Type: {city_data.get('type', 'military')}
Recent activity: {city_data.get('recent_actions', [])}
Weak points: {city_data.get('weaknesses', [])}

Make it contextual and engaging!"""
        
        response = await self.generate(
            prompt, 
            system_prompt=system_prompt,
            temperature=0.8
        )
        
        # Parse JSON
        import json
        try:
            return json.loads(response)
        except:
            # Fallback mission
            return {
                "title": "🏗️ Build Something",
                "description": "Construct or upgrade any building",
                "type": "build",
                "required_progress": 1,
                "rewards": {"gold": 1000, "xp": 500},
                "penalties": {"morale": -5},
                "mandatory": True,
                "expires_hours": 24
            }
    
    async def analyze_trade(self, trade_data: Dict) -> str:
        """Analyze if trade is fair"""
        
        prompt = f"""Analyze this trade deal:
Giving: {trade_data['giving']}
Receiving: {trade_data['receiving']}

Is this fair? What's the value difference?
Give brief advice in 2-3 sentences."""
        
        return await self.generate(prompt, temperature=0.5)
    
    async def generate_event(self, game_state: Dict) -> Dict:
        """Generate random world event"""
        
        system_prompt = """Generate a unique random game event.
Return ONLY valid JSON with:
{
    "name": "Event name with emoji",
    "description": "What's happening",
    "effects": {"morale": 10, "production": 1.5},
    "duration_hours": 6,
    "probability": 0.05
}"""
        
        prompt = f"""Current game state:
Total cities: {game_state.get('total_cities', 0)}
Average level: {game_state.get('avg_level', 5)}

Create an interesting event!"""
        
        response = await self.generate(
            prompt,
            system_prompt=system_prompt,
            temperature=0.9
        )
        
        import json
        try:
            return json.loads(response)
        except:
            return {}
    
    def change_model(self, model_name: str):
        """Change AI model"""
        self.model = model_name
        logger.info(f"🤖 AI model changed to: {model_name}")
    
    def get_available_models(self) -> list:
        """List available Groq models"""
        return [
            "llama-3.1-70b-versatile",
            "llama-3.1-8b-instant",
            "llama-3.2-90b-text-preview",
            "mixtral-8x7b-32768",
            "gemma2-9b-it"
        ]

# Global AI instance
ai = ShershaahXGames_AI()
```

---

### **PHASE 6: WEB SERVER (FastAPI + SocketIO)**

```python
# web_server.py

from fastapi import FastAPI, WebSocket, Request, HTTPException
from fastapi.responses import HTMLResponse, JSONResponse, FileResponse
from fastapi.staticfiles import StaticFiles
from fastapi.templating import Jinja2Templates
import socketio
import os
from typing import Dict
from core.process_manager import process_manager
from core.plugin_loader import plugin_loader
from utils.logger import logger
import asyncio
import json

# Create FastAPI app
app = FastAPI(title="City Empire Control Panel")

# Socket.IO server
sio = socketio.AsyncServer(async_mode='asgi', cors_allowed_origins='*')
socket_app = socketio.ASGIApp(sio, app)

# Mount static files
app.mount("/static", StaticFiles(directory="web/static"), name="static")

# Templates
templates = Jinja2Templates(directory="web/templates")

# Connected clients
connected_clients = set()

# ============= SOCKET.IO EVENTS =============

@sio.event
async def connect(sid, environ):
    """Client connected"""
    connected_clients.add(sid)
    logger.info(f"🔌 Client connected: {sid}")
    
    # Send current bot status
    status = process_manager.get_status()
    await sio.emit('bot_status', status, room=sid)

@sio.event
async def disconnect(sid):
    """Client disconnected"""
    connected_clients.discard(sid)
    logger.info(f"🔌 Client disconnected: {sid}")

@sio.event
async def start_bot(sid):
    """Start bot command"""
    success = await process_manager.start_bot()
    await sio.emit('bot_status', process_manager.get_status())
    await broadcast_log(f"Bot {'started' if success else 'failed to start'}")

@sio.event
async def stop_bot(sid):
    """Stop bot command"""
    success = await process_manager.stop_bot()
    await sio.emit('bot_status', process_manager.get_status())
    await broadcast_log(f"Bot {'stopped' if success else 'failed to stop'}")

@sio.event
async def restart_bot(sid):
    """Restart bot command"""
    await process_manager.restart_bot()
    await sio.emit('bot_status', process_manager.get_status())
    await broadcast_log("Bot restarted")

async def broadcast_log(message: str):
    """Broadcast log message to all clients"""
    await sio.emit('log', {
        'message': message,
        'timestamp': datetime.now().isoformat()
    })

# ============= REST API ENDPOINTS =============

@app.get("/", response_class=HTMLResponse)
async def dashboard(request: Request):
    """Main dashboard"""
    return templates.TemplateResponse("index.html", {"request": request})

@app.get("/api/status")
async def get_status():
    """Get bot status"""
    return process_manager.get_status()

@app.get("/api/features")
async def get_features():
    """Get all features"""
    all_features = plugin_loader.list_all_features()
    loaded_features = plugin_loader.loaded_features
    
    features_data = []
    for feature_name in all_features:
        info = plugin_loader.get_feature_info(feature_name)
        features_data.append({
            "name": feature_name,
            "enabled": feature_name in loaded_features,
            "version": info.get("version", "1.0.0"),
            "description": info.get("description", "")
        })
    
    return features_data

@app.post("/api/features/{feature_name}/toggle")
async def toggle_feature(feature_name: str):
    """Enable/disable feature"""
    try:
        # Update .env
        from config.settings import update_enabled_features
        current = plugin_loader.enabled_features
        
        if feature_name in current:
            current.remove(feature_name)
            # Unload feature
        else:
            current.append(feature_name)
            # Load feature
            await plugin_loader.load_feature(feature_name)
        
        update_enabled_features(current)
        
        await broadcast_log(f"Feature {feature_name} toggled")
        
        return {"success": True}
    except Exception as e:
        raise HTTPException(status_code=500, detail=str(e))

@app.get("/api/files/tree")
async def get_file_tree():
    """Get project file tree"""
    def build_tree(path: str, prefix: str = ""):
        items = []
        try:
            for item in sorted(os.listdir(path)):
                if item.startswith('.') or item == '__pycache__':
                    continue
                
                item_path = os.path.join(path, item)
                if os.path.isdir(item_path):
                    items.append({
                        "name": item,
                        "type": "folder",
                        "path": item_path,
                        "children": build_tree(item_path, prefix + item + "/")
                    })
                else:
                    items.append({
                        "name": item,
                        "type": "file",
                        "path": item_path
                    })
        except PermissionError:
            pass
        
        return items
    
    return build_tree(".")

@app.get("/api/files/read")
async def read_file(filepath: str):
    """Read file content"""
    try:
        with open(filepath, 'r') as f:
            content = f.read()
        return {"content": content}
    except Exception as e:
        raise HTTPException(status_code=400, detail=str(e))

@app.post("/api/files/write")
async def write_file(data: dict):
    """Write file content"""
    try:
        filepath = data['filepath']
        content = data['content']
        
        with open(filepath, 'w') as f:
            f.write(content)
        
        await broadcast_log(f"File saved: {filepath}")
        return {"success": True}
    except Exception as e:
        raise HTTPException(status_code=400, detail=str(e))

@app.get("/api/env")
async def get_env():
    """Get .env variables"""
    env_vars = {}
    if os.path.exists('.env'):
        with open('.env', 'r') as f:
            for line in f:
                line = line.strip()
                if line and not line.startswith('#'):
                    key, value = line.split('=', 1)
                    env_vars[key] = value
    return env_vars

@app.post("/api/env/update")
async def update_env(data: dict):
    """Update .env variables"""
    try:
        env_vars = data.get('env_vars', {})
        
        lines = []
        if os.path.exists('.env'):
            with open('.env', 'r') as f:
                for line in f:
                    if line.strip() and not line.startswith('#'):
                        key = line.split('=')[0]
                        if key in env_vars:
                            lines.append(f"{key}={env_vars[key]}\n")
                            del env_vars[key]
                        else:
                            lines.append(line)
                    else:
                        lines.append(line)
        
        # Add new vars
        for key, value in env_vars.items():
            lines.append(f"{key}={value}\n")
        
        with open('.env', 'w') as f:
            f.writelines(lines)
        
        await broadcast_log(".env updated")
        return {"success": True}
    except Exception as e:
        raise HTTPException(status_code=400, detail=str(e))

@app.get("/api/logs")
async def get_logs(lines: int = 100):
    """Get recent logs"""
    try:
        with open('logs/bot.log', 'r') as f:
            all_lines = f.readlines()
            return {"logs": all_lines[-lines:]}
    except:
        return {"logs": []}

@app.post("/api/ai/config")
async def update_ai_config(data: dict):
    """Update AI configuration"""
    from ai_module.ShershaahXGames_ai import ai
    
    if 'model' in data:
        ai.change_model(data['model'])
    
    # Update .env
    env_updates = {}
    if 'api_key' in data:
        env_updates['GROQ_API_KEY'] = data['api_key']
    if 'model' in data:
        env_updates['AI_MODEL'] = data['model']
    
    if env_updates:
        await update_env({"env_vars": env_updates})
    
    return {"success": True}

@app.get("/api/ai/models")
async def get_ai_models():
    """Get available AI models"""
    from ai_module.ShershaahXGames_ai import ai
    return {"models": ai.get_available_models()}

# ============= START SERVER =============

if __name__ == "__main__":
    import uvicorn
    
    port = int(os.getenv("WEB_PORT", 8080))
    
    print(f"""
╔════════════════════════════════════════╗
║   🎮 CITY EMPIRE CONTROL PANEL        ║
╠════════════════════════════════════════╣
║                                        ║
║   📡 Server: http://localhost:{port}     ║
║   🔧 Admin Panel Ready                 ║
║                                        ║
╚════════════════════════════════════════╝
    """)
    
    uvicorn.run(
        socket_app,
        host="0.0.0.0",
        port=port,
        log_level="info"
    )
```

---

### **PHASE 7: FRONTEND (HTML/CSS/JS)**

#### **7.1: Main Dashboard**

```html
<!-- web/templates/index.html -->

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>City Empire - Control Panel</title>
    
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Custom CSS -->
    <link rel="stylesheet" href="/static/css/style.css">
</head>
<body>
    <!-- Sidebar -->
    <div class="sidebar">
        <div class="sidebar-header">
            <h3><i class="fas fa-city"></i> City Empire</h3>
        </div>
        <ul class="sidebar-menu">
            <li class="active"><a href="#" data-page="dashboard"><i class="fas fa-home"></i> Dashboard</a></li>
            <li><a href="#" data-page="features"><i class="fas fa-puzzle-piece"></i> Features</a></li>
            <li><a href="#" data-page="editor"><i class="fas fa-code"></i> File Editor</a></li>
            <li><a href="#" data-page="logs"><i class="fas fa-terminal"></i> Live Logs</a></li>
            <li><a href="#" data-page="settings"><i class="fas fa-cog"></i> Settings</a></li>
            <li><a href="#" data-page="ai"><i class="fas fa-robot"></i> AI Config</a></li>
        </ul>
    </div>
    
    <!-- Main Content -->
    <div class="main-content">
        <!-- Top Bar -->
        <nav class="navbar navbar-light bg-white border-bottom">
            <div class="container-fluid">
                <span class="navbar-brand mb-0 h1">Control Panel</span>
                <div>
                    <span id="bot-status-badge" class="badge bg-secondary">Checking...</span>
                    <span id="cpu-usage" class="badge bg-info ms-2">CPU: 0%</span>
                    <span id="memory-usage" class="badge bg-warning ms-2">RAM: 0MB</span>
                </div>
            </div>
        </nav>
        
        <!-- Content Area -->
        <div class="content-area p-4">
            <!-- Dashboard Page -->
            <div id="dashboard-page" class="page-content active">
                <div class="row">
                    <!-- Bot Control Card -->
                    <div class="col-md-4">
                        <div class="card">
                            <div class="card-header bg-primary text-white">
                                <h5><i class="fas fa-robot"></i> Bot Control</h5>
                            </div>
                            <div class="card-body text-center">
                                <div id="bot-status-display" class="mb-3">
                                    <h2 class="text-secondary">●</h2>
                                    <p class="text-muted">Status: <span id="status-text">Unknown</span></p>
                                    <p class="small">PID: <span id="bot-pid">-</span></p>
                                </div>
                                <div class="btn-group d-flex" role="group">
                                    <button class="btn btn-success" id="btn-start">
                                        <i class="fas fa-play"></i> Start
                                    </button>
                                    <button class="btn btn-danger" id="btn-stop">
                                        <i class="fas fa-stop"></i> Stop
                                    </button>
                                    <button class="btn btn-warning" id="btn-restart">
                                        <i class="fas fa-redo"></i> Restart
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Quick Stats -->
                    <div class="col-md-8">
                        <div class="card">
                            <div class="card-header bg-info text-white">
                                <h5><i class="fas fa-chart-line"></i> System Stats</h5>
                            </div>
                            <div class="card-body">
                                <div class="row text-center">
                                    <div class="col-md-3">
                                        <div class="stat-box">
                                            <i class="fas fa-users fa-2x text-primary"></i>
                                            <h4 id="total-users">-</h4>
                                            <p class="text-muted">Total Users</p>
                                        </div>
                                    </div>
                                    <div class="col-md-3">
                                        <div class="stat-box">
                                            <i class="fas fa-city fa-2x text-success"></i>
                                            <h4 id="total-cities">-</h4>
                                            <p class="text-muted">Active Cities</p>
                                        </div>
                                    </div>
                                    <div class="col-md-3">
                                        <div class="stat-box">
                                            <i class="fas fa-fire fa-2x text-danger"></i>
                                            <h4 id="active-wars">-</h4>
                                            <p class="text-muted">Active Wars</p>
                                        </div>
                                    </div>
                                    <div class="col-md-3">
                                        <div class="stat-box">
                                            <i class="fas fa-handshake fa-2x text-warning"></i>
                                            <h4 id="active-trades">-</h4>
                                            <p class="text-muted">Active Trades</p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                
                <!-- Recent Activity -->
                <div class="row mt-4">
                    <div class="col-12">
                        <div class="card">
                            <div class="card-header bg-dark text-white">
                                <h5><i class="fas fa-history"></i> Recent Activity</h5>
                            </div>
                            <div class="card-body">
                                <div id="activity-log" style="max-height: 300px; overflow-y: auto;">
                                    <!-- Activity items will be populated here -->
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- Other pages will be loaded here -->
            <div id="features-page" class="page-content"></div>
            <div id="editor-page" class="page-content"></div>
            <div id="logs-page" class="page-content"></div>
            <div id="settings-page" class="page-content"></div>
            <div id="ai-page" class="page-content"></div>
        </div>
    </div>
    
    <!-- Socket.IO -->
    <script src="https://cdn.socket.io/4.5.4/socket.io.min.js"></script>
    
    <!-- Bootstrap JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    
    <!-- Custom JS -->
    <script src="/static/js/main.js"></script>
    <script src="/static/js/socket-handler.js"></script>
</body>
</html>
```

#### **7.2: Main JavaScript**

```javascript
// web/static/js/main.js

// Page Navigation
document.querySelectorAll('.sidebar-menu a').forEach(link => {
    link.addEventListener('click', (e) => {
        e.preventDefault();
        
        // Update active menu item
        document.querySelectorAll('.sidebar-menu li').forEach(li => li.classList.remove('active'));
        e.target.closest('li').classList.add('active');
        
        // Show corresponding page
        const pageName = e.target.getAttribute('data-page');
        document.querySelectorAll('.page-content').forEach(page => page.classList.remove('active'));
        document.getElementById(`${pageName}-page`).classList.add('active');
        
        // Load page content
        loadPage(pageName);
    });
});

// Load page content
async function loadPage(pageName) {
    switch(pageName) {
        case 'features':
            await loadFeatures();
            break;
        case 'editor':
            await loadEditor();
            break;
        case 'logs':
            await loadLogs();
            break;
        case 'settings':
            await loadSettings();
            break;
        case 'ai':
            await loadAIConfig();
            break;
    }
}

// Bot Control Functions
document.getElementById('btn-start').addEventListener('click', () => {
    socket.emit('start_bot');
});

document.getElementById('btn-stop').addEventListener('click', () => {
    socket.emit('stop_bot');
});

document.getElementById('btn-restart').addEventListener('click', () => {
    socket.emit('restart_bot');
});

// Update bot status UI
function updateBotStatus(status) {
    const statusBadge = document.getElementById('bot-status-badge');
    const statusDisplay = document.getElementById('bot-status-display');
    const statusText = document.getElementById('status-text');
    const pidText = document.getElementById('bot-pid');
    const cpuUsage = document.getElementById('cpu-usage');
    const memoryUsage = document.getElementById('memory-usage');
    
    if (status.running) {
        statusBadge.className = 'badge bg-success';
        statusBadge.textContent = 'Running';
        statusDisplay.querySelector('h2').className = 'text-success';
        statusText.textContent = 'Running';
        pidText.textContent = status.pid;
        cpuUsage.textContent = `CPU: ${status.cpu.toFixed(1)}%`;
        memoryUsage.textContent = `RAM: ${status.memory.toFixed(0)}MB`;
    } else {
        statusBadge.className = 'badge bg-danger';
        statusBadge.textContent = 'Stopped';
        statusDisplay.querySelector('h2').className = 'text-danger';
        statusText.textContent = 'Stopped';
        pidText.textContent = '-';
        cpuUsage.textContent = 'CPU: 0%';
        memoryUsage.textContent = 'RAM: 0MB';
    }
}

// Load Features Page
async function loadFeatures() {
    const response = await fetch('/api/features');
    const features = await response.json();
    
    let html = `
        <div class="card">
            <div class="card-header bg-primary text-white">
                <h5><i class="fas fa-puzzle-piece"></i> Feature Management</h5>
            </div>
            <div class="card-body">
                <table class="table table-hover">
                    <thead>
                        <tr>
                            <th>Feature</th>
                            <th>Version</th>
                            <th>Status</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody>
    `;
    
    features.forEach(feature => {
        html += `
            <tr>
                <td><strong>${feature.name}</strong></td>
                <td>${feature.version}</td>
                <td>
                    ${feature.enabled 
                        ? '<span class="badge bg-success">Enabled</span>' 
                        : '<span class="badge bg-secondary">Disabled</span>'}
                </td>
                <td>
                    <button class="btn btn-sm ${feature.enabled ? 'btn-danger' : 'btn-success'}" 
                            onclick="toggleFeature('${feature.name}')">
                        ${feature.enabled ? 'Disable' : 'Enable'}
                    </button>
                </td>
            </tr>
        `;
    });
    
    html += `
                    </tbody>
                </table>
            </div>
        </div>
    `;
    
    document.getElementById('features-page').innerHTML = html;
}

// Toggle Feature
async function toggleFeature(featureName) {
    const response = await fetch(`/api/features/${featureName}/toggle`, {
        method: 'POST'
    });
    
    if (response.ok) {
        await loadFeatures(); // Reload features list
    }
}

// Load Settings Page
async function loadSettings() {
    const response = await fetch('/api/env');
    const envVars = await response.json();
    
    let html = `
        <div class="card">
            <div class="card-header bg-warning text-dark">
                <h5><i class="fas fa-cog"></i> Environment Settings</h5>
            </div>
            <div class="card-body">
                <form id="env-form">
    `;
    
    for (const [key, value] of Object.entries(envVars)) {
        const isSensitive = key.includes('KEY') || key.includes('TOKEN');
        html += `
            <div class="mb-3">
                <label class="form-label"><strong>${key}</strong></label>
                <input type="${isSensitive ? 'password' : 'text'}" 
                       class="form-control" 
                       name="${key}" 
                       value="${value}">
            </div>
        `;
    }
    
    html += `
                    <button type="submit" class="btn btn-primary">
                        <i class="fas fa-save"></i> Save Settings
                    </button>
                </form>
            </div>
        </div>
    `;
    
    document.getElementById('settings-page').innerHTML = html;
    
    // Handle form submission
    document.getElementById('env-form').addEventListener('submit', async (e) => {
        e.preventDefault();
        
        const formData = new FormData(e.target);
        const envVars = Object.fromEntries(formData);
        
        const response = await fetch('/api/env/update', {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({env_vars: envVars})
        });
        
        if (response.ok) {
            alert('Settings saved! Restart bot to apply changes.');
        }
    });
}

// Load AI Config Page
async function loadAIConfig() {
    const modelsResponse = await fetch('/api/ai/models');
    const {models} = await modelsResponse.json();
    
    const envResponse = await fetch('/api/env');
    const envVars = await envResponse.json();
    
    let html = `
        <div class="card">
            <div class="card-header bg-info text-white">
                <h5><i class="fas fa-robot"></i> AI Configuration</h5>
            </div>
            <div class="card-body">
                <form id="ai-form">
                    <div class="mb-3">
                        <label class="form-label"><strong>Groq API Key</strong></label>
                        <input type="password" class="form-control" name="api_key" 
                               value="${envVars.GROQ_API_KEY || ''}" 
                               placeholder="Enter your Groq API key">
                        <small class="text-muted">Get free API key from <a href="https://console.groq.com" target="_blank">console.groq.com</a></small>
                    </div>
                    
                    <div class="mb-3">
                        <label class="form-label"><strong>AI Model</strong></label>
                        <select class="form-select" name="model">
    `;
    
    models.forEach(model => {
        const selected = model === envVars.AI_MODEL ? 'selected' : '';
        html += `<option value="${model}" ${selected}>${model}</option>`;
    });
    
    html += `
                        </select>
                    </div>
                    
                    <button type="submit" class="btn btn-primary">
                        <i class="fas fa-save"></i> Save AI Config
                    </button>
                </form>
            </div>
        </div>
    `;
    
    document.getElementById('ai-page').innerHTML = html;
    
    // Handle form submission
    document.getElementById('ai-form').addEventListener('submit', async (e) => {
        e.preventDefault();
        
        const formData = new FormData(e.target);
        const data = Object.fromEntries(formData);
        
        const response = await fetch('/api/ai/config', {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify(data)
        });
        
        if (response.ok) {
            alert('AI configuration saved!');
        }
    });
}

// Load Logs Page
async function loadLogs() {
    const response = await fetch('/api/logs');
    const {logs} = await response.json();
    
    let html = `
        <div class="card">
            <div class="card-header bg-dark text-white">
                <h5><i class="fas fa-terminal"></i> Live Logs</h5>
            </div>
            <div class="card-body">
                <div id="log-display" style="background: #1e1e1e; color: #d4d4d4; padding: 15px; border-radius: 5px; max-height: 600px; overflow-y: auto; font-family: 'Courier New', monospace;">
    `;
    
    logs.forEach(log => {
        html += `<div>${log}</div>`;
    });
    
    html += `
                </div>
            </div>
        </div>
    `;
    
    document.getElementById('logs-page').innerHTML = html;
}

// Initial load
async function init() {
    // Fetch initial stats
    const response = await fetch('/api/status');
    const status = await response.json();
    updateBotStatus(status);
}

init();
```

#### **7.3: Socket Handler**

```javascript
// web/static/js/socket-handler.js

// Connect to Socket.IO server
const socket = io();

// Connection events
socket.on('connect', () => {
    console.log('✅ Connected to server');
    addActivityLog('Connected to control panel');
});

socket.on('disconnect', () => {
    console.log('❌ Disconnected from server');
    addActivityLog('Disconnected from control panel');
});

// Bot status updates
socket.on('bot_status', (status) => {
    updateBotStatus(status);
});

// Log messages
socket.on('log', (data) => {
    addActivityLog(data.message, data.timestamp);
    
    // Update log display if on logs page
    const logDisplay = document.getElementById('log-display');
    if (logDisplay) {
        const logEntry = document.createElement('div');
        logEntry.textContent = `[${new Date(data.timestamp).toLocaleTimeString()}] ${data.message}`;
        logDisplay.appendChild(logEntry);
        logDisplay.scrollTop = logDisplay.scrollHeight;
    }
});

// Add activity to log
function addActivityLog(message, timestamp = new Date().toISOString()) {
    const activityLog = document.getElementById('activity-log');
    if (!activityLog) return;
    
    const item = document.createElement('div');
    item.className = 'activity-item p-2 border-bottom';
    item.innerHTML = `
        <small class="text-muted">${new Date(timestamp).toLocaleTimeString()}</small>
        <p class="mb-0">${message}</p>
    `;
    
    activityLog.insertBefore(item, activityLog.firstChild);
    
    // Keep only last 20 items
    while (activityLog.children.length > 20) {
        activityLog.removeChild(activityLog.lastChild);
    }
}

// Request periodic status updates
setInterval(() => {
    if (socket.connected) {
        fetch('/api/status')
            .then(r => r.json())
            .then(status => updateBotStatus(status));
    }
}, 5000); // Every 5 seconds
```

#### **7.4: Custom CSS**

```css
/* web/static/css/style.css */

:root {
    --sidebar-width: 250px;
    --primary-color: #4e73df;
    --secondary-color: #858796;
    --success-color: #1cc88a;
    --danger-color: #e74a3b;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: #f8f9fc;
}

/* Sidebar */
.sidebar {
    position: fixed;
    left: 0;
    top: 0;
    width: var(--sidebar-width);
    height: 100vh;
    background: #2c3e50;
    color: white;
    overflow-y: auto;
    transition: 0.3s;
}

.sidebar-header {
    padding: 20px;
    background: #34495e;
    border-bottom: 1px solid rgba(255,255,255,0.1);
}

.sidebar-header h3 {
    margin: 0;
    font-size: 1.3rem;
}

.sidebar-menu {
    list-style: none;
    padding: 0;
    margin: 0;
}

.sidebar-menu li {
    border-bottom: 1px solid rgba(255,255,255,0.1);
}

.sidebar-menu a {
    display: block;
    padding: 15px 20px;
    color: #ecf0f1;
    text-decoration: none;
    transition: 0.3s;
}

.sidebar-menu a:hover,
.sidebar-menu li.active a {
    background: rgba(255,255,255,0.1);
    padding-left: 25px;
}

.sidebar-menu i {
    margin-right: 10px;
    width: 20px;
}

/* Main Content */
.main-content {
    margin-left: var(--sidebar-width);
    min-height: 100vh;
}

.content-area {
    padding: 20px;
}

/* Page Content */
.page-content {
    display: none;
}

.page-content.active {
    display: block;
}

/* Cards */
.card {
    border: none;
    border-radius: 10px;
    box-shadow: 0 0.15rem 1.75rem 0 rgba(58, 59, 69, 0.15);
    margin-bottom: 20px;
}

.card-header {
    border-radius: 10px 10px 0 0 !important;
}

/* Stat Box */
.stat-box {
    padding: 20px;
    text-align: center;
}

.stat-box i {
    margin-bottom: 10px;
}

.stat-box h4 {
    margin: 10px 0 5px 0;
    font-size: 2rem;
    font-weight: bold;
}

/* Activity Log */
.activity-item {
    animation: slideIn 0.3s ease;
}

@keyframes slideIn {
    from {
        opacity: 0;
        transform: translateX(-20px);
    }
    to {
        opacity: 1;
        transform: translateX(0);
    }
}

/* Responsive */
@media (max-width: 768px) {
    .sidebar {
        width: 70px;
    }
    
    .sidebar-header h3,
    .sidebar-menu a span {
        display: none;
    }
    
    .main-content {
        margin-left: 70px;
    }
}
```

---

### **PHASE 8: INITIAL DATABASE SCHEMA**

```sql
-- migrations/001_initial_schema.sql

-- Cities Table
CREATE TABLE IF NOT EXISTS cities (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    city_name TEXT NOT NULL,
    owner_id INTEGER NOT NULL,
    city_type TEXT DEFAULT 'military',
    level INTEGER DEFAULT 1,
    xp INTEGER DEFAULT 0,
    gold INTEGER DEFAULT 1000,
    wood INTEGER DEFAULT 500,
    stone INTEGER DEFAULT 300,
    food INTEGER DEFAULT 200,
    population INTEGER DEFAULT 10,
    max_population INTEGER DEFAULT 100,
    defense_power INTEGER DEFAULT 0,
    attack_power INTEGER DEFAULT 0,
    morale INTEGER DEFAULT 100,
    invite_code TEXT UNIQUE,
    peace_shield TIMESTAMP,
    last_collected TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Users Table
CREATE TABLE IF NOT EXISTS users (
    user_id INTEGER PRIMARY KEY,
    username TEXT,
    city_id INTEGER,
    role TEXT DEFAULT 'citizen',
    personal_gold INTEGER DEFAULT 0,
    contribution INTEGER DEFAULT 0,
    work_cooldown TIMESTAMP,
    last_active TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    joined_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (city_id) REFERENCES cities(id)
);

-- Buildings Table
CREATE TABLE IF NOT EXISTS buildings (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    city_id INTEGER NOT NULL,
    building_type TEXT NOT NULL,
    level INTEGER DEFAULT 1,
    position INTEGER,
    upgrade_started TIMESTAMP,
    upgrade_complete TIMESTAMP,
    built_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (city_id) REFERENCES cities(id)
);

-- Wars Table
CREATE TABLE IF NOT EXISTS wars (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    attacker_id INTEGER NOT NULL,
    defender_id INTEGER NOT NULL,
    attack_power INTEGER,
    defense_power INTEGER,
    loot_gold INTEGER DEFAULT 0,
    loot_wood INTEGER DEFAULT 0,
    loot_stone INTEGER DEFAULT 0,
    status TEXT DEFAULT 'pending',
    result TEXT,
    travel_ends TIMESTAMP,
    ended_at TIMESTAMP,
    started_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (attacker_id) REFERENCES cities(id),
    FOREIGN KEY (defender_id) REFERENCES cities(id)
);

-- Missions Table
CREATE TABLE IF NOT EXISTS missions (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    city_id INTEGER NOT NULL,
    mission_type TEXT,
    title TEXT,
    description TEXT,
    required_progress INTEGER DEFAULT 1,
    current_progress INTEGER DEFAULT 0,
    rewards TEXT, -- JSON
    penalties TEXT, -- JSON
    mandatory BOOLEAN DEFAULT 0,
    expires_at TIMESTAMP,
    completed BOOLEAN DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (city_id) REFERENCES cities(id)
);

-- Create indexes
CREATE INDEX IF NOT EXISTS idx_users_city ON users(city_id);
CREATE INDEX IF NOT EXISTS idx_buildings_city ON buildings(city_id);
CREATE INDEX IF NOT EXISTS idx_wars_attacker ON wars(attacker_id);
CREATE INDEX IF NOT EXISTS idx_wars_defender ON wars(defender_id);
CREATE INDEX IF NOT EXISTS idx_missions_city ON missions(city_id);
```

---

### **PHASE 9: EXAMPLE FEATURE (CITY)**

```python
# features/city/__init__.py

from core.base_feature import BaseFeature
from telegram.ext import CommandHandler, CallbackQueryHandler
from .handlers import (
    create_city_handler,
    my_city_handler,
    collect_resources_handler
)

class CityFeature(BaseFeature):
    @property
    def name(self) -> str:
        return "city"
    
    async def setup(self):
        self.app.add_handler(CommandHandler("createcity", create_city_handler))
        self.app.add_handler(CommandHandler("mycity", my_city_handler))
        self.app.add_handler(CallbackQueryHandler(
            collect_resources_handler,
            pattern="^collect_"
        ))

async def setup():
    """Auto-called by plugin loader"""
    from telegram.ext import Application
    import os
    
    app = Application.builder().token(os.getenv("BOT_TOKEN")).build()
    feature = CityFeature(app)
    await feature.setup()
```

```python
# features/city/handlers.py

from telegram import Update, InlineKeyboardButton, InlineKeyboardMarkup
from telegram.ext import ContextTypes
from .services import CityService
from core.event_bus import event_bus

city_service = CityService()

async def create_city_handler(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user_id = update.effective_user.id
    
    if await city_service.has_city(user_id):
        await update.message.reply_text("❌ You already have a city!")
        return
    
    # Simple city creation (can be expanded)
    city_name = " ".join(context.args) if context.args else f"City_{user_id}"
    
    city = await city_service.create_city(user_id, city_name, "military")
    
    await event_bus.emit("city.created", {
        "user_id": user_id,
        "city_id": city["id"],
        "city_name": city_name
    })
    
    await update.message.reply_text(
        f"🏙️ {city_name} has been founded!\n\n"
        f"💰 Gold: {city['gold']}\n"
        f"🪵 Wood: {city['wood']}\n"
        f"⛏️ Stone: {city['stone']}\n\n"
        f"Use /mycity to manage your city!"
    )

async def my_city_handler(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user_id = update.effective_user.id
    
    city = await city_service.get_user_city(user_id)
    
    if not city:
        await update.message.reply_text("❌ You don't have a city! Use /createcity")
        return
    
    keyboard = InlineKeyboardMarkup([
        [
            InlineKeyboardButton("📦 Collect All", callback_data="collect_all"),
            InlineKeyboardButton("🏗️ Build", callback_data="build_menu")
        ],
        [
            InlineKeyboardButton("⬆️ Upgrade", callback_data="upgrade_menu"),
            InlineKeyboardButton("📊 Stats", callback_data="city_stats")
        ]
    ])
    
    text = f"""
🏙️ **{city['city_name']}** | Level {city['level']}

**Resources:**
💰 Gold: {city['gold']:,}
🪵 Wood: {city['wood']:,}
⛏️ Stone: {city['stone']:,}
🌾 Food: {city['food']:,}

**Population:** {city['population']}/{city['max_population']}
**Morale:** {city['morale']}%
    """
    
    await update.message.reply_text(text, reply_markup=keyboard)

async def collect_resources_handler(update: Update, context: ContextTypes.DEFAULT_TYPE):
    query = update.callback_query
    await query.answer()
    
    user_id = update.effective_user.id
    
    collected = await city_service.collect_all_resources(user_id)
    
    await event_bus.emit("city.resources_collected", {
        "user_id": user_id,
        "resources": collected
    })
    
    await query.answer(
        f"✅ Collected: {collected['gold']}💰 {collected['wood']}🪵",
        show_alert=True
    )
```

```python
# features/city/services.py

from core.database import db
from typing import Optional, Dict
from datetime import datetime, timedelta

class CityService:
    async def has_city(self, user_id: int) -> bool:
        result = await db.fetchval(
            "SELECT COUNT(*) FROM cities WHERE owner_id = ?",
            user_id
        )
        return result > 0
    
    async def create_city(self, user_id: int, city_name: str, city_type: str) -> Dict:
        result = await db.fetchone("""
            INSERT INTO cities (
                city_name, owner_id, city_type,
                gold, wood, stone, food
            ) VALUES (?, ?, ?, 1000, 500, 300, 200)
            RETURNING *
        """, city_name, user_id, city_type)
        
        return result
    
    async def get_user_city(self, user_id: int) -> Optional[Dict]:
        return await db.fetchone(
            "SELECT * FROM cities WHERE owner_id = ?",
            user_id
        )
    
    async def collect_all_resources(self, user_id: int) -> Dict:
        city = await self.get_user_city(user_id)
        
        # Calculate time passed
        last_collected = datetime.fromisoformat(city['last_collected'])
        time_passed = (datetime.now() - last_collected).total_seconds() / 3600
        
        # Calculate production
        production = {
            "gold": int(50 * city['level'] * time_passed),
            "wood": int(30 * city['level'] * time_passed),
            "stone": int(20 * city['level'] * time_passed),
            "food": int(40 * city['level'] * time_passed)
        }
        
        # Update database
        await db.execute("""
            UPDATE cities 
            SET 
                gold = gold + ?,
                wood = wood + ?,
                stone = stone + ?,
                food = food + ?,
                last_collected = CURRENT_TIMESTAMP
            WHERE owner_id = ?
        """, production['gold'], production['wood'], production['stone'], production['food'], user_id)
        
        return production
```

```yaml
# features/city/config.yaml

name: city
version: 1.0.0
enabled: true
description: Core city management feature
dependencies: []

settings:
  starting_resources:
    gold: 1000
    wood: 500
    stone: 300
    food: 200
  
  production_rates:
    gold_per_hour: 50
    wood_per_hour: 30
    stone_per_hour: 20
    food_per_hour: 40

commands:
  - /createcity
  - /mycity

events:
  emits:
    - city.created
    - city.resources_collected
    - city.level_up
  
  listens_to: []
```

---

### **PHASE 10: STARTUP SCRIPTS**

```bash
#!/bin/bash
# start.sh

echo "🚀 Starting City Empire Bot..."

# Create virtual environment if not exists
if [ ! -d "venv" ]; then
    echo "📦 Creating virtual environment..."
    python3 -m venv venv
fi

# Activate virtual environment
source venv/bin/activate

# Install requirements
echo "📦 Installing dependencies..."
pip install -r requirements.txt

# Create directories
mkdir -p data logs

# Copy .env if not exists
if [ ! -f ".env" ]; then
    cp .env.example .env
    echo "⚠️  Please configure .env file before running!"
    exit 1
fi

# Start web server
echo "🌐 Starting web control panel..."
python web_server.py &

echo "✅ Control panel started!"
echo "📡 Access: http://localhost:8080"
```

```batch
@echo off
REM start.bat

echo Starting City Empire Bot...

REM Create virtual environment
if not exist "venv" (
    echo Creating virtual environment...
    python -m venv venv
)

REM Activate virtual environment
call venv\Scripts\activate

REM Install requirements
echo Installing dependencies...
pip install -r requirements.txt

REM Create directories
if not exist "data" mkdir data
if not exist "logs" mkdir logs

REM Copy .env
if not exist ".env" (
    copy .env.example .env
    echo Please configure .env file!
    pause
    exit
)

REM Start web server
echo Starting web control panel...
start python web_server.py

echo Control panel started!
echo Access: http://localhost:8080
pause
```

---

## 🎯 CODING AGENT PROMPT

```
Create a complete Telegram bot with web control panel using this plan:

PROJECT: City Empire - Multiplayer city building game bot

REQUIREMENTS:
1. Follow the exact file structure provided
2. Implement all PHASE modules (1-10)
3. Use SQLite for database (free)
4. Implement Socket.IO for real-time updates
5. Create responsive web UI with Bootstrap
6. Add file editor with Monaco Editor
7. Implement feature toggle system
8. Add .env management from web
9. Include AI configuration panel
10. Add live log streaming

TECH STACK:
- Backend: Python + FastAPI + python-telegram-bot
- Frontend: HTML/CSS/JS + Bootstrap + Socket.IO
- Database: SQLite
- AI: Groq API (free tier)

DELIVERABLES:
✅ All Python modules working
✅ Complete web interface
✅ Database migrations
✅ Event bus system
✅ Plugin loader for features
✅ Process manager
✅ Real-time logging
✅ File editor
✅ Settings manager

Make it production-ready with:
- Error handling
- Logging
- Security (env vars)
- Modular architecture
- Event-driven design

START CODING NOW!
```

---

## 📝 USAGE INSTRUCTIONS

### **Step 1: Initial Setup**

```bash
# Clone or create project
mkdir city_empire && cd city_empire

# Run startup script
chmod +x start.sh
./start.sh

# Or on Windows
start.bat
```

### **Step 2: Configure**

1. Open http://localhost:8080
2. Go to Settings page
3. Add your Telegram Bot Token
4. Add Groq API key (free from console.groq.com)
5. Click Save

### **Step 3: Start Bot**

1. Go to Dashboard
2. Click "Start" button
3. Bot is now running!

### **Step 4: Manage**

- Enable/disable features from Features page
- Edit code from File Editor page
- View logs in real-time
- Update AI settings
- Send messages from bot

---

## 🎉 FEATURES CHECKLIST

✅ Start/Stop bot from web
✅ Enable/disable features
✅ Edit files in browser (Monaco Editor)
✅ View live logs
✅ Update .env from web
✅ Configure AI (Groq + models)
✅ Real-time status updates
✅ Feature auto-loading
✅ Event-driven architecture
✅ SQLite database (free)
✅ Modular design
✅ No API costs (uses Groq free tier)
✅ Responsive web UI
✅ Process management
✅ File tree viewer

---

## 🚀 READY TO BUILD!

Bhai yeh **complete blueprint** hai! Coding agent ko yeh file de do aur bol:

**"Build this entire project exactly as specified. Create all files, implement all features, and make it working end-to-end."**

Sab kuch detail mein hai - structure, code, database, frontend, backend, everything! 🔥

Kuch aur chahiye? 🎯
