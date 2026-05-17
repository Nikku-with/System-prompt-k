# 🤖 CODING AGENT INSTRUCTIONS

## 📝 MASTER PROMPT FOR AI CODING ASSISTANT

```
TASK: Build a complete Telegram bot game with web control panel

PROJECT NAME: City Empire Bot

ARCHITECTURE: Modular, event-driven, plugin-based

===== BUILD REQUIREMENTS =====

1. FOLDER STRUCTURE:
   Create this exact structure:
   city_empire/
   ├── main.py (bot entry)
   ├── web_server.py (control panel)
   ├── requirements.txt
   ├── .env.example
   ├── core/ (framework - DON'T MODIFY)
   │   ├── database.py
   │   ├── event_bus.py
   │   ├── plugin_loader.py
   │   ├── process_manager.py
   │   └── base_feature.py
   ├── features/ (game features - ADD NEW HERE)
   │   ├── city/
   │   ├── war/
   │   ├── trade/
   │   └── missions/
   ├── ai_module/ (ShershaahXGames_ai)
   ├── web/ (frontend)
   │   ├── static/css/
   │   ├── static/js/
   │   └── templates/
   ├── utils/
   ├── migrations/
   └── logs/

2. CORE MODULES TO IMPLEMENT:

   A. Database (core/database.py):
      - SQLite with async support (aiosqlite)
      - Auto-run migrations from migrations/ folder
      - Methods: execute(), fetchone(), fetchall(), fetchval()
      - Connection pooling

   B. Event Bus (core/event_bus.py):
      - Pub/Sub pattern
      - Features communicate via events ONLY
      - Methods: on(event_name), emit(event_name, data)
      - Middleware support
      - Error isolation (one listener fails ≠ all fail)

   C. Plugin Loader (core/plugin_loader.py):
      - Auto-discover features from features/ directory
      - Load config.yaml for each feature
      - Check dependencies
      - Enable/disable features dynamically
      - Reload features without restart

   D. Process Manager (core/process_manager.py):
      - Start/stop bot as subprocess
      - Monitor CPU/RAM usage
      - Graceful shutdown
      - Status checking

3. WEB CONTROL PANEL (web_server.py):

   Tech Stack:
   - FastAPI (REST API)
   - Socket.IO (real-time updates)
   - Bootstrap 5 (UI)
   - Vanilla JavaScript (no frameworks)

   Pages Required:
   - Dashboard (bot status, stats)
   - Features (enable/disable)
   - File Editor (Monaco Editor)
   - Logs (real-time streaming)
   - Settings (.env editor)
   - AI Config (Groq setup)

   REST Endpoints:
   - GET /api/status → bot status
   - GET /api/features → list features
   - POST /api/features/{name}/toggle → enable/disable
   - GET /api/files/tree → file explorer
   - POST /api/files/write → save file
   - GET /api/env → read .env
   - POST /api/env/update → update .env
   - GET /api/logs → recent logs

   WebSocket Events:
   - start_bot → start bot process
   - stop_bot → stop bot process
   - restart_bot → restart
   - bot_status → status update broadcast
   - log → new log entry broadcast

4. AI MODULE (ai_module/ShershaahXGames_ai.py):

   Class: ShershaahXGames_AI
   
   Methods:
   - generate(prompt, system_prompt, temperature, max_tokens)
   - generate_mission(city_data) → returns mission JSON
   - analyze_trade(trade_data) → returns advice
   - generate_event(game_state) → returns event JSON
   - change_model(model_name)
   - get_available_models()

   Integration:
   - Use Groq API (free tier)
   - Support multiple models
   - Environment variables for API key
   - JSON parsing with fallbacks
   - Error handling

5. DATABASE SCHEMA (migrations/001_initial_schema.sql):

   Tables:
   - cities (id, city_name, owner_id, level, xp, resources, etc.)
   - users (user_id, username, city_id, role, etc.)
   - buildings (id, city_id, building_type, level, etc.)
   - wars (id, attacker_id, defender_id, result, etc.)
   - missions (id, city_id, mission_type, progress, etc.)
   - trades (id, from_city, to_city, status, etc.)
   - spy_missions (id, spy_city, target_city, etc.)

6. EXAMPLE FEATURE (features/city/):

   Files:
   - __init__.py → Feature class + setup()
   - handlers.py → Telegram command handlers
   - services.py → Business logic (NO telegram code)
   - models.py → Data models
   - keyboards.py → Button layouts
   - config.yaml → Feature configuration

   Pattern:
   - Handlers call Services
   - Services use Database
   - Services emit Events
   - Features listen to Events
   - Zero direct dependencies between features

7. FRONTEND (web/templates/ & web/static/):

   index.html:
   - Sidebar navigation
   - Dashboard cards (bot status, stats)
   - Real-time updates via Socket.IO
   - Responsive design

   JavaScript:
   - main.js → page navigation, UI updates
   - socket-handler.js → WebSocket events
   - file-editor.js → Monaco Editor integration
   - feature-manager.js → feature toggle logic

   CSS:
   - style.css → custom styling
   - Sidebar layout
   - Card styles
   - Animations

===== CRITICAL RULES =====

1. MODULARITY:
   - Each feature = separate folder
   - Features communicate ONLY via event_bus
   - NO direct imports between features
   - Core framework = untouchable

2. CONFIGURATION:
   - All settings in config.yaml
   - All secrets in .env
   - No hardcoded values

3. ERROR HANDLING:
   - Try-catch everywhere
   - Log all errors
   - Graceful degradation
   - User-friendly error messages

4. ASYNC/AWAIT:
   - All I/O operations async
   - Use asyncio properly
   - No blocking calls

5. SECURITY:
   - Never expose .env in web
   - Validate all inputs
   - Sanitize user data
   - Use environment variables

===== OUTPUT FORMAT =====

For each file you create, use this format:

```python
# filepath: core/database.py
"""
Module description
"""

[CODE HERE]
```

Start with core modules, then features, then web interface.

Test each component as you build it.

===== QUALITY STANDARDS =====

✅ Code must be production-ready
✅ Include docstrings
✅ Add type hints where possible
✅ Handle edge cases
✅ Log important actions
✅ Follow PEP 8
✅ Add comments for complex logic
✅ Make it extensible

===== DELIVERABLES =====

Phase 1: Core Framework
- database.py ✅
- event_bus.py ✅
- plugin_loader.py ✅
- process_manager.py ✅
- base_feature.py ✅

Phase 2: AI Module
- ShershaahXGames_ai.py ✅
- Integration with Groq ✅

Phase 3: Database
- Initial schema SQL ✅
- Migration system ✅

Phase 4: Example Feature
- City feature complete ✅
- War feature basic ✅

Phase 5: Web Server
- FastAPI setup ✅
- Socket.IO integration ✅
- All API endpoints ✅

Phase 6: Frontend
- All HTML templates ✅
- JavaScript files ✅
- CSS styling ✅
- Real-time updates ✅

Phase 7: Integration
- Everything working together ✅
- Bot starts from web ✅
- Features load/unload ✅
- Logs stream live ✅

Phase 8: Polish
- Error handling ✅
- Documentation ✅
- Startup scripts ✅
- .env.example ✅

===== TESTING CHECKLIST =====

Before marking complete, test:
□ Bot starts from web panel
□ Features can be toggled
□ Files can be edited
□ Logs update in real-time
□ .env can be updated
□ AI configuration works
□ Database migrations run
□ Events fire correctly
□ Features load on startup
□ Bot commands work

===== START BUILDING NOW! =====

Build in order:
1. Create project structure
2. Implement core modules
3. Add database + migrations
4. Create AI module
5. Build example features
6. Implement web server
7. Create frontend
8. Integration testing
9. Polish and document

GO! 🚀
```

---

## 🎯 QUICK PROMPTS FOR SPECIFIC TASKS

### Prompt 1: Create Core Framework

```
Create the core framework for City Empire bot:

1. core/database.py - SQLite async wrapper with migration support
2. core/event_bus.py - Event pub/sub system
3. core/plugin_loader.py - Auto-load features from features/
4. core/process_manager.py - Start/stop bot subprocess
5. core/base_feature.py - Base class for all features

Requirements:
- Full async/await
- Error handling
- Logging
- Type hints
- Docstrings

Make it production-ready!
```

### Prompt 2: Create Web Server

```
Create web_server.py with:

1. FastAPI app with static files + templates
2. Socket.IO integration for real-time updates
3. REST API endpoints for:
   - Bot status
   - Feature management
   - File operations
   - Env management
   - Logs
   - AI config
4. WebSocket handlers for bot control

Include:
- CORS setup
- Error handling
- Security headers
- Request validation

Make it scalable and secure!
```

### Prompt 3: Create Frontend

```
Create complete web interface:

Templates (web/templates/):
1. index.html - Dashboard with sidebar
2. Features page included
3. File editor with Monaco
4. Live logs viewer
5. Settings page
6. AI config page

JavaScript (web/static/js/):
1. main.js - Navigation + UI logic
2. socket-handler.js - WebSocket events
3. feature-manager.js - Toggle features
4. file-editor.js - Code editing

CSS (web/static/css/):
1. style.css - Custom styling
2. Responsive design
3. Dark theme for logs
4. Animations

Use Bootstrap 5 CDN. Make it beautiful!
```

### Prompt 4: Create Example Features

```
Create these game features:

1. features/city/ - City management
   - Create city
   - View dashboard
   - Collect resources
   - Build structures

2. features/war/ - War system (basic)
   - Attack cities
   - Defend
   - Battle calculator

3. features/missions/ - AI missions
   - Daily mission generation
   - Progress tracking
   - Rewards/penalties

Each feature needs:
- __init__.py (setup)
- handlers.py (Telegram)
- services.py (logic)
- config.yaml (settings)

Follow event-driven pattern!
```

---

## 🔧 DEBUGGING PROMPTS

### If Bot Won't Start:

```
Debug bot startup issue:

1. Check .env file exists and has BOT_TOKEN
2. Verify database migrations ran successfully
3. Check if features are loading (check logs)
4. Ensure requirements.txt packages installed
5. Look for errors in logs/bot.log

Fix the issue and make bot start properly!
```

### If Web Panel Won't Connect:

```
Debug web panel connection:

1. Check if web_server.py is running
2. Verify port 8080 is not in use
3. Test Socket.IO connection in browser console
4. Check CORS settings in FastAPI
5. Verify static files are served correctly

Fix and make web panel accessible!
```

### If Features Won't Load:

```
Debug feature loading:

1. Check features/ directory structure
2. Verify __init__.py exists in each feature
3. Check config.yaml syntax
4. Look for errors in plugin_loader logs
5. Test feature setup() function

Fix feature loading and reload features!
```

---

## 📋 COMPLETION CHECKLIST

### Core Framework ✅
- [ ] database.py works
- [ ] event_bus.py works
- [ ] plugin_loader.py works
- [ ] process_manager.py works
- [ ] base_feature.py works

### Web Interface ✅
- [ ] Dashboard loads
- [ ] Features page works
- [ ] File editor works
- [ ] Logs stream live
- [ ] Settings update
- [ ] AI config works

### Bot Features ✅
- [ ] City feature works
- [ ] War feature basic
- [ ] Missions generate
- [ ] Events fire correctly

### Integration ✅
- [ ] Bot starts from web
- [ ] Features toggle
- [ ] Database migrations
- [ ] Logs appear live
- [ ] .env updates work

### Testing ✅
- [ ] Create city command
- [ ] View city command
- [ ] Start/stop bot
- [ ] Enable/disable features
- [ ] Edit files
- [ ] View logs

---

## 🚀 DEPLOYMENT CHECKLIST

### Pre-Production:
- [ ] All features tested
- [ ] Error handling added
- [ ] Logging configured
- [ ] Security reviewed
- [ ] Documentation complete

### Production:
- [ ] .env configured
- [ ] Database backed up
- [ ] Monitoring setup
- [ ] SSL certificate (if public)
- [ ] Reverse proxy (nginx)

---

## 💡 TIPS FOR CODING AGENT

1. **Build incrementally** - Test each module before moving on
2. **Follow the structure exactly** - Don't deviate from file layout
3. **Use type hints** - Makes code clearer and catches errors
4. **Add docstrings** - Explain what each function does
5. **Handle errors gracefully** - Try-catch everywhere
6. **Log important actions** - Helps with debugging
7. **Test event bus** - Make sure events fire correctly
8. **Keep features independent** - No direct imports between features
9. **Use async properly** - Don't block the event loop
10. **Make it extensible** - Easy to add new features later

---

## 📞 SUPPORT QUERIES

If coding agent gets stuck, try these prompts:

**"I'm getting [ERROR] when [ACTION]. How do I fix it?"**

**"How should I structure [FEATURE] to work with the event bus?"**

**"What's the best way to implement [FUNCTIONALITY]?"**

**"Show me an example of [PATTERN] in this architecture."**

**"How do I test [COMPONENT] independently?"**

---

## 🎉 FINAL VERIFICATION

Before considering the project complete, run:

```bash
# Start the bot
./start.sh

# Open web panel
http://localhost:8080

# Verify:
✅ Web panel loads
✅ Bot status shows
✅ Features listed
✅ Can start bot
✅ Logs appear
✅ Can edit .env
✅ Files editable
✅ AI config works

# Test bot:
✅ /start command works
✅ /createcity works
✅ /mycity works
✅ Buttons respond
✅ Resources collect

SUCCESS! 🎊
```

---

Bhai yeh sab instructions hai coding agent ke liye! Detailed aur step-by-step! 🔥
