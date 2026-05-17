# 🚀 CITY EMPIRE - QUICK REFERENCE

## 📁 PROJECT STRUCTURE (30-SECOND OVERVIEW)

```
city_empire/
├── main.py              ← Bot entry point
├── web_server.py        ← Control panel server
├── requirements.txt     ← Dependencies
├── .env                 ← Configuration (SECRET!)
│
├── core/                ← Framework (DON'T TOUCH)
│   ├── database.py         → SQLite manager
│   ├── event_bus.py        → Events system
│   ├── plugin_loader.py    → Auto-load features
│   ├── process_manager.py  → Start/stop bot
│   └── base_feature.py     → Feature base class
│
├── features/            ← Game features (ADD NEW HERE)
│   ├── city/              → City management
│   ├── war/               → War system
│   ├── trade/             → Trading
│   └── missions/          → AI missions
│
├── ai_module/           ← AI Integration
│   └── ShershaahXGames_ai.py → Groq API wrapper
│
├── web/                 ← Control Panel UI
│   ├── static/css/
│   ├── static/js/
│   └── templates/
│
├── migrations/          ← Database schemas
├── utils/               ← Helpers
└── logs/                ← Log files
```

---

## ⚡ QUICK START (3 COMMANDS)

```bash
# 1. Install
git clone [your-repo]
cd city_empire
pip install -r requirements.txt

# 2. Configure
cp .env.example .env
# Edit .env with your tokens

# 3. Run
./start.sh
# Open http://localhost:8080
```

---

## 🔑 KEY CONCEPTS (MUST KNOW)

### 1️⃣ **Event Bus** (Features Talk Via Events)

```python
# Feature A emits event
await event_bus.emit("city.created", {"city_id": 123})

# Feature B listens (in __init__.py)
@self.listen_to_event("city.created")
async def on_city_created(data):
    # Do something
    pass
```

### 2️⃣ **Plugin Loader** (Auto-Discovers Features)

```
Just create folder in features/
├── new_feature/
│   ├── __init__.py    ← Has setup() function
│   ├── handlers.py
│   ├── services.py
│   └── config.yaml

Auto-loads on startup! 🎉
```

### 3️⃣ **Process Manager** (Control Bot from Web)

```python
# Start bot
await process_manager.start_bot()

# Stop bot
await process_manager.stop_bot()

# Check status
status = process_manager.get_status()
```

### 4️⃣ **Database** (SQLite Async)

```python
# Insert
await db.execute("INSERT INTO cities ...")

# Select one
city = await db.fetchone("SELECT * FROM cities WHERE id = ?", city_id)

# Select many
cities = await db.fetchall("SELECT * FROM cities")
```

---

## 🎮 ADDING NEW FEATURE (5 MINUTES)

```bash
# 1. Create folder
mkdir features/new_feature
cd features/new_feature

# 2. Create files
touch __init__.py handlers.py services.py config.yaml

# 3. Write __init__.py
```

```python
from core.base_feature import BaseFeature
from telegram.ext import CommandHandler

class NewFeature(BaseFeature):
    @property
    def name(self):
        return "new_feature"
    
    async def setup(self):
        # Register handlers
        self.app.add_handler(CommandHandler("cmd", handler))
        
        # Listen to events
        @self.listen_to_event("city.created")
        async def on_city_created(data):
            # React to city creation
            pass

async def setup():
    # Auto-called by plugin loader
    pass
```

Done! Feature auto-loads on next restart! ✅

---

## 🌐 WEB API ENDPOINTS

```
GET  /api/status              → Bot status
GET  /api/features            → List features
POST /api/features/{id}/toggle → Enable/disable
GET  /api/files/tree          → File explorer
POST /api/files/write         → Save file
GET  /api/env                 → Read .env
POST /api/env/update          → Update .env
GET  /api/logs                → Recent logs
GET  /api/ai/models           → Available AI models
POST /api/ai/config           → Update AI config
```

---

## 🔌 WEBSOCKET EVENTS

```javascript
// Frontend sends:
socket.emit('start_bot')
socket.emit('stop_bot')
socket.emit('restart_bot')

// Server broadcasts:
socket.on('bot_status', (status) => {})
socket.on('log', (data) => {})
```

---

## 🤖 AI MODULE (ShershaahXGames_ai)

```python
from ai_module.ShershaahXGames_ai import ai

# Generate text
response = await ai.generate("Your prompt here")

# Generate mission
mission = await ai.generate_mission({
    "level": 5,
    "type": "military",
    "weaknesses": ["low defense"]
})

# Change model
ai.change_model("llama-3.1-8b-instant")

# Get models
models = ai.get_available_models()
```

---

## 📊 DATABASE SCHEMA (CORE TABLES)

```sql
cities
├── id, city_name, owner_id
├── level, xp, gold, wood, stone, food
├── defense_power, attack_power, morale
└── created_at, last_collected

users
├── user_id, username, city_id
├── role, personal_gold, contribution
└── joined_at, last_active

buildings
├── id, city_id, building_type
├── level, upgrade_started, built_at

missions
├── id, city_id, mission_type
├── title, description, progress
├── rewards, penalties, expires_at

wars
├── id, attacker_id, defender_id
├── attack_power, defense_power
├── result, loot, started_at
```

---

## 🎯 COMMON TASKS

### Start Bot from Code:
```python
await process_manager.start_bot()
```

### Toggle Feature:
```python
await plugin_loader.reload_feature("feature_name")
```

### Emit Event:
```python
await event_bus.emit("event.name", {"data": "value"})
```

### Query Database:
```python
result = await db.fetchone("SELECT * FROM cities WHERE id = ?", city_id)
```

### Update .env:
```python
# Use web panel /api/env/update
# Or edit directly and restart
```

---

## 🔧 TROUBLESHOOTING

### Bot Won't Start:
```bash
# Check logs
tail -f logs/bot.log

# Check .env
cat .env | grep BOT_TOKEN

# Test database
sqlite3 data/bot.db ".tables"

# Verify features
ls features/
```

### Web Panel 404:
```bash
# Check server running
ps aux | grep web_server

# Check port
lsof -i :8080

# Restart
pkill -f web_server
python web_server.py
```

### Feature Not Loading:
```bash
# Check structure
ls features/feature_name/

# Check __init__.py
cat features/feature_name/__init__.py

# Check logs
grep "feature_name" logs/bot.log
```

---

## 📝 .ENV VARIABLES (REQUIRED)

```bash
# Bot
BOT_TOKEN=123456:ABC...        # From @BotFather
BOT_NAME=CityEmpireBot

# Database
DATABASE_PATH=data/bot.db

# Web
WEB_HOST=0.0.0.0
WEB_PORT=8080
SECRET_KEY=random-string-here

# AI
GROQ_API_KEY=gsk_...           # From console.groq.com
AI_MODEL=llama-3.1-70b-versatile
AI_TEMPERATURE=0.7
AI_MAX_TOKENS=1000

# Features (comma-separated)
ENABLED_FEATURES=city,war,trade,spy,missions

# Logging
LOG_LEVEL=INFO
LOG_FILE=logs/bot.log

# Admin
ADMIN_USER_ID=your_telegram_id
```

---

## 🎨 FEATURE STRUCTURE (STANDARD)

```python
# features/example/__init__.py
from core.base_feature import BaseFeature

class ExampleFeature(BaseFeature):
    @property
    def name(self):
        return "example"
    
    async def setup(self):
        # Register handlers
        # Setup event listeners
        pass

async def setup():
    # Auto-called by loader
    pass
```

```python
# features/example/handlers.py
from telegram import Update
from telegram.ext import ContextTypes

async def command_handler(update: Update, context: ContextTypes.DEFAULT_TYPE):
    # Handle command
    pass
```

```python
# features/example/services.py
from core.database import db

class ExampleService:
    async def do_something(self):
        # Business logic
        # NO Telegram code here!
        pass
```

```yaml
# features/example/config.yaml
name: example
version: 1.0.0
enabled: true
description: Example feature

settings:
  option1: value1
  option2: value2

commands:
  - /command1
  - /command2

events:
  emits:
    - example.event1
  listens_to:
    - city.created
```

---

## 📚 USEFUL COMMANDS

```bash
# Development
python main.py                 # Run bot directly
python web_server.py           # Run web panel

# Logs
tail -f logs/bot.log          # Watch bot logs
tail -f logs/web.log          # Watch web logs

# Database
sqlite3 data/bot.db           # Open database
.tables                       # List tables
SELECT * FROM cities;         # Query

# Process
ps aux | grep main.py         # Find bot process
kill -9 [PID]                 # Force stop
pkill -f main.py              # Kill by name

# Features
ls features/                  # List features
cat features/city/config.yaml # View config

# Dependencies
pip freeze > requirements.txt # Update deps
pip install -r requirements.txt # Install deps
```

---

## 🎯 TESTING CHECKLIST

```bash
# ✅ Core
□ Database connects
□ Migrations run
□ Events fire
□ Features load

# ✅ Web
□ Panel loads
□ Bot starts
□ Features toggle
□ Files edit
□ Logs stream

# ✅ Bot
□ Commands work
□ Buttons respond
□ Database updates
□ AI generates

# ✅ Integration
□ Event propagation
□ Feature independence
□ Error handling
□ Logging works
```

---

## 🚨 CRITICAL RULES

1. ❌ **DON'T** modify core/ files
2. ✅ **DO** use event_bus for communication
3. ❌ **DON'T** import features directly
4. ✅ **DO** put settings in config.yaml
5. ❌ **DON'T** hardcode values
6. ✅ **DO** use .env for secrets
7. ❌ **DON'T** block async functions
8. ✅ **DO** handle errors gracefully
9. ❌ **DON'T** skip logging
10. ✅ **DO** test features independently

---

## 💾 BACKUP COMMANDS

```bash
# Backup database
cp data/bot.db data/bot.db.backup

# Backup .env
cp .env .env.backup

# Full backup
tar -czf backup.tar.gz city_empire/

# Restore
tar -xzf backup.tar.gz
```

---

## 🎉 SUCCESS METRICS

✅ Bot responds to commands
✅ Web panel controls bot
✅ Features can toggle
✅ Files editable from web
✅ Logs stream in real-time
✅ AI generates missions
✅ Database persists data
✅ Events propagate correctly
✅ No errors in logs
✅ Production-ready!

---

## 📞 NEED HELP?

- Check logs: `logs/bot.log`
- Test feature: Create test file in `tests/`
- Debug event: Add `print()` in event_bus.py
- View database: Use `sqlite3 data/bot.db`
- Reload feature: Use web panel or restart

---

## 🚀 DEPLOYMENT

```bash
# Production checklist:
□ Configure .env
□ Set strong SECRET_KEY
□ Use production database
□ Enable HTTPS (nginx)
□ Set up monitoring
□ Configure backups
□ Add rate limiting
□ Secure API endpoints
□ Test everything!
```

---

Bhai yeh **quick reference** hai! Har cheez ka short summary! 📋🔥
