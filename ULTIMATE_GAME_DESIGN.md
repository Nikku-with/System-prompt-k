# 🏙️ CITY EMPIRE - ULTIMATE GAME DESIGN DOCUMENT
## *Complete Breakdown: Features, Boards, Commands, Social Systems, Competition*

---

# 📑 TABLE OF CONTENTS

1. [CORE SYSTEMS](#core-systems)
2. [SOCIAL FEATURES](#social-features)
3. [CITIZEN ROLES & PROGRESSION](#citizen-roles--progression)
4. [COMPLETE COMMAND LIST](#complete-command-list)
5. [BOARD LAYOUTS](#board-layouts)
6. [LEVEL & XP SYSTEM](#level--xp-system)
7. [MONEY & ECONOMY](#money--economy)
8. [PLACES & LOCATIONS](#places--locations)
9. [COMPETITION SYSTEMS](#competition-systems)
10. [BUFFS & ITEMS](#buffs--items)
11. [RELATIONSHIPS & SOCIAL](#relationships--social)
12. [SPECIAL EVENTS](#special-events)
13. [FORMULAS & CALCULATIONS](#formulas--calculations)

---

# 🎯 CORE SYSTEMS

## 🏙️ **CITY HIERARCHY**

```
                    👑 MAYOR (Host)
                          |
        ┌─────────────────┼─────────────────┐
        |                 |                 |
    ⚔️ GENERAL        💼 FINANCE       🏗️ ARCHITECT
    (Military)        MINISTER         (Buildings)
        |              (Economy)            |
        |                 |                 |
    ┌───┴───┐         ┌───┴───┐         ┌──┴──┐
    |       |         |       |         |     |
 Soldiers  Guards  Traders  Bankers  Builders Workers
    |       |         |       |         |     |
    └───┬───┘         └───┬───┘         └──┬──┘
        |                 |                 |
    NORMAL CITIZENS (Can be promoted based on contribution)
```

### **PROMOTION PATHS:**

```
👤 CITIZEN (Starting)
    ↓ (50 Contribution Points)
🎖️ ACTIVE MEMBER
    ↓ (150 Contribution Points + Mayor Approval)
┌────────┬────────┬────────┐
|        |        |        |
⚔️ SOLDIER 💼 TRADER 🔧 BUILDER
    ↓        ↓        ↓
    (500 CP) (500 CP) (500 CP)
    ↓        ↓        ↓
🎖️ VETERAN 💰 MERCHANT 🏗️ ARCHITECT
    ↓        ↓        ↓
    (1500 CP)(1500 CP)(1500 CP)
    ↓        ↓        ↓
⚔️ GENERAL 💼 MINISTER 🏛️ CHIEF ARCHITECT
```

---

# 👥 SOCIAL FEATURES

## 💑 **COUPLES IN CITY**

### **How to Become a Couple:**

```
User A: /propose @UserB
Bot: 💍 @UserA has proposed to @UserB!
     
     @UserB, respond:
     [💕 Accept] [💔 Reject] [⏳ Think About It]

If Accept:
Bot: 🎊 @UserA & @UserB are now a couple!
     Relationship Status: Dating
     Couple Benefits Unlocked!
```

### **Couple Benefits:**

| Benefit | Description | Bonus |
|---------|-------------|-------|
| 💕 **Joint Income** | Pool resources together | +20% combined income |
| 🏠 **Shared House** | Live together (cost split) | -50% housing cost |
| 🎁 **Gift Exchange** | Give items tax-free | 0% tax on gifts |
| ⚔️ **Duo Attacks** | Fight together in wars | +30% attack power |
| 🛡️ **Couple Shield** | Protect each other | One takes 50% damage for other |
| 🎉 **Anniversary Bonus** | Every 30 days | 💰 10,000 + 💎 50 gems |

### **Couple Progression:**

```
Level 1: Dating (0-7 days)
  → Unlock: Joint missions

Level 2: Serious (8-30 days)
  → Unlock: Shared house

Level 3: Engaged (31-90 days)
  → Unlock: Couple business

Level 4: Married (91+ days)
  → Unlock: Family system, kids (cosmetic)
```

### **Couple Commands:**

```
/propose @user          - Propose to someone
/breakup                - End relationship (mutual or 7-day cooldown)
/couplemissions         - View couple-only missions
/gift @partner [item]   - Give gift to partner
/anniversary            - View relationship stats
/couplehouse            - Manage shared living
/teamattack [city]      - Attack as couple (+30% power)
```

---

## 🎂 **BIRTHDAY SYSTEM**

### **Setting Birthday:**

```
/setbirthday DD/MM/YYYY

Bot: 🎂 Birthday set to [Date]!
     You'll receive special rewards on your birthday!
```

### **Birthday Benefits:**

When it's your birthday (00:00 to 23:59 that day):

```
╔═══════════════════════════════════════════╗
║     🎂 HAPPY BIRTHDAY, @USERNAME! 🎉      ║
╠═══════════════════════════════════════════╣
║                                           ║
║  🎁 BIRTHDAY REWARDS:                     ║
║  ├─ 💰 10,000 Gold                       ║
║  ├─ 💎 100 Gems                          ║
║  ├─ 🎫 Birthday Buff (24h)               ║
║  ├─ 🏆 2x XP for today                   ║
║  └─ 🎊 Special Birthday Title            ║
║                                           ║
║  🎉 CITY CELEBRATION:                     ║
║  ├─ City throws party for you            ║
║  ├─ All citizens get +10% income today   ║
║  └─ Mayor can give special gift          ║
║                                           ║
║  [🎁 Claim Rewards] [🎊 Thank Everyone]  ║
╚═══════════════════════════════════════════╝
```

### **City Birthday List:**

```
/birthdays

📅 UPCOMING BIRTHDAYS:
┌────────────────────────────────────┐
│ Today (Feb 12):                    │
│  🎂 @Alice - 25 years old          │
│     [🎁 Send Gift]                 │
│                                    │
│ Tomorrow (Feb 13):                 │
│  🎂 @Bob - 30 years old            │
│     [⏰ Set Reminder]              │
│                                    │
│ This Week:                         │
│  Feb 15: @Charlie (22)             │
│  Feb 18: @Diana (28)               │
└────────────────────────────────────┘
```

---

## 😠 **JEALOUSY & RIVALRY SYSTEM**

### **How Jealousy Works:**

Jealousy increases when:
- Someone gets promoted (you don't): +10 jealousy
- Couple forms (you're single): +5 jealousy
- Someone earns more than you: +3 jealousy/day
- Someone has higher rank: +2 jealousy/day
- Someone gets birthday celebration: +8 jealousy

### **Jealousy Effects:**

```
Jealousy Level: 0-100

0-20:   😊 Content
        No effects

21-40:  😐 Slightly Jealous
        -5% Work efficiency

41-60:  😠 Jealous
        -10% Work efficiency
        Chance to gossip (spreads rumors)

61-80:  😡 Very Jealous
        -20% Work efficiency
        May sabotage others' work
        Can start rivalry

81-100: 🤬 Extremely Jealous
        -30% Work efficiency
        May betray city
        Can defect to enemy city
```

### **Managing Jealousy:**

```
REDUCE JEALOUSY:
✅ Get promoted           → -20 jealousy
✅ Earn achievement       → -15 jealousy
✅ Receive recognition    → -10 jealousy
✅ Win competition        → -25 jealousy
✅ Find partner           → -30 jealousy
✅ Get gift from mayor    → -20 jealousy
```

### **Rivalry System:**

```
/challenge @user

Creates a RIVALRY:
┌─────────────────────────────────────┐
│  ⚔️ RIVALRY: You vs @Opponent       │
├─────────────────────────────────────┤
│  Duration: 7 days                   │
│  Competition Type: [Choose]         │
│   • 💰 Most Money Earned            │
│   • ⚔️ Most Battles Won             │
│   • 🏗️ Most Buildings Built         │
│   • 🏆 Most XP Gained               │
│                                     │
│  Winner Gets:                       │
│   • 💰 5,000 Gold                  │
│   • 🏆 Rival Victor Title          │
│   • 🎖️ Respect from city           │
│   • 📈 +50 Contribution            │
│                                     │
│  Loser Gets:                        │
│   • 😢 Temporary shame             │
│   • -25 Contribution                │
│                                     │
│  [⚔️ Accept] [❌ Decline]          │
└─────────────────────────────────────┘
```

---

## 💬 **RELATIONSHIPS & REPUTATION**

### **Relationship Types:**

```
❤️ LOVED    (+80 to +100) - Best friends, trusted allies
💚 FRIEND   (+50 to +79)  - Good relationship
😊 FRIENDLY (+20 to +49)  - Positive acquaintance
😐 NEUTRAL  (-19 to +19)  - No strong feelings
😠 DISLIKE  (-49 to -20)  - Negative relationship
😡 ENEMY    (-79 to -50)  - Active hostility
💀 HATED    (-100 to -80) - Deep hatred, rivalry
```

### **Relationship Actions:**

```
INCREASE RELATIONSHIP (+):
✅ /gift @user [item]        → +5 to +20
✅ /compliment @user          → +3
✅ /helpmission @user         → +10
✅ Fight together in war      → +15
✅ Trade fairly               → +5
✅ Defend their honor         → +20
✅ Vote for them              → +8

DECREASE RELATIONSHIP (-):
❌ /insult @user              → -10
❌ Attack their friends       → -15
❌ Steal from them            → -30
❌ Sabotage their work        → -20
❌ Spread rumors              → -12
❌ Vote against them          → -8
❌ Break promise/deal         → -25
```

### **Reputation Board:**

```
/reputation

╔══════════════════════════════════════════╗
║        YOUR REPUTATION IN CITY           ║
╠══════════════════════════════════════════╣
║                                          ║
║  Overall Score: ⭐ 850 (Respected)       ║
║  City Rank: #5 of 50 citizens           ║
║                                          ║
║  REPUTATION BREAKDOWN:                   ║
║  ├─ Work Ethic:      ████████░░ 85/100  ║
║  ├─ Loyalty:         ██████████ 100/100 ║
║  ├─ Trustworthy:     ███████░░░ 72/100  ║
║  ├─ Combat Skill:    ██████░░░░ 65/100  ║
║  ├─ Trading:         ████████░░ 78/100  ║
║  └─ Social:          ███████░░░ 68/100  ║
║                                          ║
║  RELATIONSHIPS:                          ║
║  ❤️ Loved by:     5 citizens            ║
║  💚 Friends:      12 citizens            ║
║  😊 Friendly:     18 citizens            ║
║  😐 Neutral:      10 citizens            ║
║  😠 Dislike:      3 citizens             ║
║  😡 Enemies:      2 citizens             ║
║                                          ║
║  [📊 Detailed View] [📈 Improve]         ║
╚══════════════════════════════════════════╝
```

---

# 🎖️ CITIZEN ROLES & PROGRESSION

## 👤 **NORMAL USER ACTIVITIES**

### **Daily Work System (Earn Contribution):**

```
/work

╔══════════════════════════════════════════╗
║          💼 DAILY WORK BOARD             ║
╠══════════════════════════════════════════╣
║                                          ║
║  Choose your task:                       ║
║                                          ║
║  🏗️ CONSTRUCTION WORK                    ║
║  ├─ Help build city structures           ║
║  ├─ Duration: 2 hours                    ║
║  ├─ Reward: 💰 500 + 🎖️ 10 CP          ║
║  └─ [Start Work]                         ║
║                                          ║
║  🛡️ GUARD DUTY                           ║
║  ├─ Patrol city walls                    ║
║  ├─ Duration: 3 hours                    ║
║  ├─ Reward: 💰 600 + 🎖️ 12 CP          ║
║  └─ [Start Patrol]                       ║
║                                          ║
║  💼 MARKET ASSISTANCE                    ║
║  ├─ Help in city market                  ║
║  ├─ Duration: 1 hour                     ║
║  ├─ Reward: 💰 300 + 🎖️ 8 CP           ║
║  └─ [Help Market]                        ║
║                                          ║
║  🎯 MINI-GAME CHALLENGE                  ║
║  ├─ Complete quiz/puzzle                 ║
║  ├─ Duration: 15 minutes                 ║
║  ├─ Reward: 💰 200 + 🎖️ 5 CP           ║
║  └─ [Play Game]                          ║
║                                          ║
║  Work Cooldown: ⏰ 20h 15m remaining     ║
║                                          ║
║  Today's Stats:                          ║
║  ├─ Work Streak: 🔥 7 days              ║
║  ├─ Total Earned Today: 💰 1,500        ║
║  └─ Contribution Gained: 🎖️ 35 CP      ║
╚══════════════════════════════════════════╝
```

### **Contribution Point (CP) System:**

```
CONTRIBUTION ACTIVITIES:

WORK & TASKS:
✅ Complete daily work        → 8-15 CP
✅ 7-day work streak          → 50 CP bonus
✅ 30-day work streak         → 300 CP bonus
✅ Help build city building   → 20 CP per building
✅ Donate to city treasury    → 1 CP per 100 gold

COMBAT:
✅ Win battle                 → 25 CP
✅ Defend city successfully   → 40 CP
✅ Participate in war         → 15 CP (win or lose)
✅ Kill enemy spy             → 30 CP

ECONOMIC:
✅ Complete trade deal        → 10 CP
✅ Successful auction         → 15 CP
✅ Pay taxes on time          → 5 CP/week
✅ Donate resources           → varies

SOCIAL:
✅ Recruit new citizen        → 30 CP
✅ Help citizen mission       → 10 CP
✅ Win rivalry competition    → 50 CP
✅ City event participation   → 20 CP

PENALTIES:
❌ Miss daily work           → -5 CP
❌ Betray city               → -100 CP
❌ Lose battle badly         → -10 CP
❌ Get caught stealing       → -50 CP
```

### **Promotion Request System:**

```
/requestpromotion

╔══════════════════════════════════════════╗
║       🎖️ PROMOTION REQUEST               ║
╠══════════════════════════════════════════╣
║                                          ║
║  Your Stats:                             ║
║  ├─ Contribution: 🎖️ 165 CP             ║
║  ├─ Time in City: 15 days               ║
║  ├─ Reputation: ⭐ 850                   ║
║  └─ Work Streak: 🔥 12 days             ║
║                                          ║
║  AVAILABLE PROMOTIONS:                   ║
║                                          ║
║  🎖️ ACTIVE MEMBER                        ║
║  ├─ Required: 150 CP ✅                  ║
║  ├─ Time: 7 days ✅                      ║
║  ├─ Mayor Approval: Pending              ║
║  └─ [Request Now]                        ║
║                                          ║
║  ⚔️ SOLDIER                              ║
║  ├─ Required: 500 CP ❌ (Need 335 more) ║
║  ├─ Time: 14 days ✅                     ║
║  ├─ Battles Won: 5 ❌ (Need 5 more)     ║
║  └─ [Locked]                             ║
║                                          ║
║  💼 TRADER                               ║
║  ├─ Required: 500 CP ❌                  ║
║  ├─ Trades: 20 ❌ (Need 15 more)        ║
║  └─ [Locked]                             ║
║                                          ║
║  Progress to Next Rank:                  ║
║  ████████░░░░░░ 55% (165/300 CP)        ║
║                                          ║
║  [📊 View All Ranks] [💬 Message Mayor] ║
╚══════════════════════════════════════════╝
```

---

## 👑 **MAYOR/HOST POWERS**

### **Mayor Dashboard:**

```
/mayordashboard

╔══════════════════════════════════════════╗
║      👑 MAYOR COMMAND CENTER             ║
╠══════════════════════════════════════════╣
║                                          ║
║  🏙️ CITY: Neo Mumbai | Level 12         ║
║  👥 Population: 45/80 citizens           ║
║  💰 Treasury: 156,000 gold               ║
║                                          ║
║  ━━━━━━━━ QUICK ACTIONS ━━━━━━━━         ║
║                                          ║
║  [📋 Pending Requests (7)]               ║
║   ├─ Join Requests: 5                    ║
║   ├─ Promotion Requests: 2               ║
║   └─ Appeal Requests: 0                  ║
║                                          ║
║  [👥 Citizen Management]                 ║
║   ├─ View all citizens                   ║
║   ├─ Promote/demote                      ║
║   ├─ Kick/ban                            ║
║   └─ Send city-wide message              ║
║                                          ║
║  [💰 Treasury Management]                ║
║   ├─ View transactions                   ║
║   ├─ Set tax rate (current: 12%)         ║
║   ├─ Distribute bonuses                  ║
║   └─ Emergency funds                     ║
║                                          ║
║  [⚔️ Military Control]                   ║
║   ├─ Declare war                         ║
║   ├─ Form alliances                      ║
║   ├─ Deploy troops                       ║
║   └─ Defense strategy                    ║
║                                          ║
║  [🏗️ City Development]                   ║
║   ├─ Build structures                    ║
║   ├─ Upgrade buildings                   ║
║   ├─ Urban planning                      ║
║   └─ Special projects                    ║
║                                          ║
║  [🎉 Events & Celebrations]              ║
║   ├─ Organize city event                 ║
║   ├─ Birthday celebrations               ║
║   ├─ Festival planning                   ║
║   └─ Competitions                        ║
║                                          ║
║  [⚖️ Justice System]                     ║
║   ├─ Handle disputes                     ║
║   ├─ Punish criminals                    ║
║   ├─ Reward contributors                 ║
║   └─ Pardon citizens                     ║
╚══════════════════════════════════════════╝
```

### **Promotion Approval System:**

```
/approvepromotion @user

╔══════════════════════════════════════════╗
║     🎖️ PROMOTION APPROVAL REQUEST        ║
╠══════════════════════════════════════════╣
║                                          ║
║  Citizen: @Alice                         ║
║  Current Rank: 👤 Citizen                ║
║  Requested Rank: 🎖️ Active Member        ║
║                                          ║
║  ━━━━━━━━ QUALIFICATION CHECK ━━━━━━━━   ║
║                                          ║
║  Requirements:                           ║
║  ✅ Contribution: 165 CP (≥150 required) ║
║  ✅ Time in City: 15 days (≥7 required)  ║
║  ✅ Reputation: 850 (≥500 required)      ║
║  ✅ Active: Last seen 2h ago             ║
║  ✅ No violations                         ║
║                                          ║
║  ━━━━━━━━ CITIZEN FEEDBACK ━━━━━━━━      ║
║                                          ║
║  Officer Recommendations:                ║
║  ⚔️ General: "Good soldier, approve"     ║
║  💼 Finance Minister: "Reliable trader"  ║
║                                          ║
║  Citizen Votes:                          ║
║  👍 Support: 12 citizens (80%)           ║
║  👎 Oppose: 3 citizens (20%)             ║
║                                          ║
║  Recent Activity:                        ║
║  ├─ Work streak: 12 days                 ║
║  ├─ Battles won: 3 (0 lost)              ║
║  ├─ Trades completed: 8                  ║
║  └─ Missions done: 15                    ║
║                                          ║
║  Decision:                               ║
║  [✅ APPROVE & PROMOTE]                   ║
║  [⏳ REQUEST MORE INFO]                   ║
║  [❌ DENY WITH REASON]                    ║
║                                          ║
║  If Approved, @Alice will receive:       ║
║  • 🎖️ Active Member rank                 ║
║  • 💰 500 gold promotion bonus           ║
║  • 🏆 Promotion achievement              ║
║  • 📢 City-wide announcement             ║
╚══════════════════════════════════════════╝
```

---

# 📜 COMPLETE COMMAND LIST

## 🎮 **CITIZEN COMMANDS (Everyone)**

### **Profile & Stats:**
```
/start                  - Start bot, main menu
/profile                - View your profile
/stats                  - Detailed statistics
/inventory              - Your items & weapons
/balance                - Check gold balance
/achievements           - View achievements
/reputation             - See reputation score
/relationships          - View all relationships
```

### **City Actions:**
```
/mycity                 - View your city dashboard
/citizens               - List all city members
/cityinfo               - City statistics
/cityrankings           - Top citizens by contribution
/leavecity              - Leave current city
```

### **Work & Economy:**
```
/work                   - Daily work tasks
/collect                - Collect passive income
/shop                   - City marketplace
/trade @user            - Trade with citizen
/gift @user [item]      - Give gift
/auction                - Browse/create auctions
/business               - Manage personal business
```

### **Social:**
```
/propose @user          - Propose relationship
/breakup                - End relationship
/birthday               - View birthday info
/setbirthday DD/MM      - Set your birthday
/compliment @user       - Give compliment
/challenge @user        - Start rivalry
/relationships          - View all relationships
```

### **Combat:**
```
/attack [cityID]        - Attack enemy city
/defend                 - View defense status
/troops                 - Manage your troops
/heal                   - Heal wounded troops
/buyweapon              - Purchase weapons
/upgrade [weapon]       - Upgrade equipment
```

### **Missions & Quests:**
```
/daily                  - Daily missions
/missions               - Active missions
/quest                  - Story quests
/couplemissions         - Couple-only missions
/complete [missionID]   - Complete mission
```

### **Exploration:**
```
/explore                - Explore city
/places                 - Visit locations
/travel [place]         - Travel to location
/discover               - Find secrets
```

---

## 👑 **MAYOR/HOST COMMANDS**

### **Management:**
```
/mayordashboard         - Mayor control panel
/approve @user          - Approve join request
/reject @user [reason]  - Reject application
/promote @user [role]   - Promote citizen
/demote @user           - Demote citizen
/kick @user [reason]    - Remove citizen
/ban @user [reason]     - Ban from city
/pardon @user           - Forgive citizen
```

### **Economy:**
```
/settax [1-30]          - Set tax rate
/treasury               - View city funds
/distribute [amount]    - Give bonuses
/salary @user [amount]  - Set citizen salary
/bonus @user [amount]   - Give one-time bonus
```

### **City Development:**
```
/build [building]       - Construct building
/upgrade [building]     - Upgrade structure
/demolish [building]    - Remove building
/rename [newname]       - Rename city
/setdescription [text]  - City description
```

### **Military:**
```
/declarewar [cityID]    - Declare war
/makepeace [cityID]     - Negotiate peace
/formalliance [cityID]  - Create alliance
/deploytroops [number]  - Deploy forces
/defensestrategy        - Set defense plan
```

### **Events:**
```
/createevent [name]     - Organize event
/startcompetition       - Begin competition
/birthday @user         - Celebrate birthday
/announcement [text]    - City-wide message
/vote [topic]           - Create poll
```

---

## 🎖️ **OFFICER COMMANDS (Generals, Ministers, etc.)**

### **General (Military Officer):**
```
/warroom                - Military dashboard
/trainsoliders          - Train troops
/scout [cityID]         - Spy on enemy
/fortify                - Strengthen defense
/strategize             - Plan attack
```

### **Finance Minister:**
```
/economydashboard       - Economy overview
/audit                  - Financial audit
/investments            - Manage investments
/grants @user [amount]  - Give financial aid
/tradedeal [cityID]     - Negotiate trade
```

### **Architect (Building Officer):**
```
/buildingplan           - Construction queue
/blueprint              - View building plans
/optimize               - Optimize buildings
/expansion              - City expansion plan
```

---

# 🎨 BOARD LAYOUTS

## 📱 **MAIN MENU BOARD**

```
╔══════════════════════════════════════════════════════╗
║              🏙️ CITY EMPIRE - MAIN MENU             ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  Welcome back, @Username! 👋                        ║
║  Rank: 🎖️ Active Member | Level: 8                  ║
║                                                      ║
║  ━━━━━━━━━━━━━ QUICK INFO ━━━━━━━━━━━━━             ║
║                                                      ║
║  💰 Gold: 5,420  |  💎 Gems: 150  |  ⚡ Energy: 85% ║
║  🏙️ City: Neo Mumbai  |  👥 Citizens: 45            ║
║  🎖️ Contribution: 165 CP  |  🏆 Rank: #12           ║
║                                                      ║
║  ━━━━━━━━━━━━━━ MAIN MENU ━━━━━━━━━━━━━             ║
║                                                      ║
║  ┌──────────────┬──────────────┬──────────────┐     ║
║  │   🏙️ MY      │   ⚔️ WAR     │   💼 WORK    │     ║
║  │   CITY       │   ROOM       │   & EARN     │     ║
║  └──────────────┴──────────────┴──────────────┘     ║
║                                                      ║
║  ┌──────────────┬──────────────┬──────────────┐     ║
║  │   🏪 SHOP    │   👥 SOCIAL  │   🎯 MISSIONS│     ║
║  │   & TRADE    │   & COUPLES  │   & QUESTS   │     ║
║  └──────────────┴──────────────┴──────────────┘     ║
║                                                      ║
║  ┌──────────────┬──────────────┬──────────────┐     ║
║  │   🗺️ EXPLORE │   🏆 COMPETE │   📊 STATS   │     ║
║  │   PLACES     │   & RANKINGS │   & PROFILE  │     ║
║  └──────────────┴──────────────┴──────────────┘     ║
║                                                      ║
║  ━━━━━━━━━━━ NOTIFICATIONS (3) ━━━━━━━━━━━          ║
║                                                      ║
║  🔔 New promotion request approved!                  ║
║  🎂 It's @Alice's birthday today!                   ║
║  ⚔️ Enemy city spotted nearby - prepare defense!    ║
║                                                      ║
║  [📨 View All] [⚙️ Settings] [❓ Help]              ║
╚══════════════════════════════════════════════════════╝
```

---

## 🏙️ **CITY DASHBOARD BOARD**

```
╔══════════════════════════════════════════════════════╗
║         🏙️ NEO MUMBAI - CITY DASHBOARD              ║
║         Level 12 ⭐⭐⭐ | Rank: #45 Global           ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  👑 Mayor: @RajKing | Type: 🏰 Military City        ║
║  📍 Location: South Region | Founded: 45 days ago   ║
║                                                      ║
║  ━━━━━━━━━━━━ CITY STATS ━━━━━━━━━━━━               ║
║                                                      ║
║  👥 POPULATION                                       ║
║  ├─ Total: 45/80 (56% full)                        ║
║  ├─ Active (24h): 38 citizens                       ║
║  ├─ Officers: 5 | Citizens: 40                      ║
║  └─ Couples: 3 💑                                    ║
║                                                      ║
║  💰 ECONOMY                                          ║
║  ├─ Treasury: 156,000 💰                            ║
║  ├─ Income: +8,500/day                              ║
║  ├─ Tax Rate: 12%                                   ║
║  └─ Trade Volume: 45,000/week                       ║
║                                                      ║
║  ⚔️ MILITARY                                         ║
║  ├─ Attack Power: 3,200 ⚔️                          ║
║  ├─ Defense Power: 2,800 🛡️                         ║
║  ├─ Active Troops: 145                              ║
║  ├─ Wars: 12W - 3L (80% win rate)                   ║
║  └─ Shield Status: None [💰 Buy 24h - 5,000]        ║
║                                                      ║
║  🏗️ BUILDINGS (8/12 slots)                          ║
║  ├─ 🏛️ City Hall: Level 12                          ║
║  ├─ 💰 Gold Mine: Level 5 (+350/hr)                 ║
║  ├─ 🪵 Lumber Mill: Level 4 (+200/hr)               ║
║  ├─ ⚔️ Barracks: Level 8 (150 troop capacity)       ║
║  ├─ 🏰 Wall: Level 6 (2,800 defense)                ║
║  ├─ 🏦 Bank: Level 5 (+2% interest)                 ║
║  ├─ 🔬 Lab: Level 3 (3 techs unlocked)              ║
║  └─ 🏪 Market: Level 7 (active trading)             ║
║                                                      ║
║  🎯 CITY MORALE: 85% 😊 (Excellent)                 ║
║  ├─ Recent victories: +10%                          ║
║  ├─ Good economy: +5%                               ║
║  ├─ Birthday celebrations: +3%                      ║
║  └─ Couple bonuses: +2%                             ║
║                                                      ║
║  ━━━━━━━━━ QUICK ACTIONS ━━━━━━━━━                  ║
║                                                      ║
║  [🏗️ Build] [⬆️ Upgrade] [📦 Collect Resources]     ║
║  [👥 Citizens] [⚔️ War Room] [💼 Economy]           ║
║  [📋 Requests (5)] [🎉 Events] [⚙️ Settings]        ║
╚══════════════════════════════════════════════════════╝
```

---

## 💼 **WORK BOARD (Detailed)**

```
╔══════════════════════════════════════════════════════╗
║              💼 DAILY WORK & TASKS                   ║
║              @Username | Level 8                     ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  Work Streak: 🔥 12 days | Next Bonus: 18 days      ║
║  Today's Earnings: 💰 1,500 | CP Gained: 🎖️ 35      ║
║  Energy: ⚡ 85/100 | Work Cooldown: ⏰ 20h 15m       ║
║                                                      ║
║  ━━━━━━━━━━ AVAILABLE JOBS ━━━━━━━━━━               ║
║                                                      ║
║  ┌────────────────────────────────────────────┐     ║
║  │ 🏗️ CONSTRUCTION WORKER                     │     ║
║  ├────────────────────────────────────────────┤     ║
║  │ Help build city wall upgrade               │     ║
║  │                                            │     ║
║  │ Duration: ⏱️ 2 hours                       │     ║
║  │ Energy Cost: ⚡ -20                        │     ║
║  │                                            │     ║
║  │ Rewards:                                   │     ║
║  │ ├─ 💰 Gold: 500                           │     ║
║  │ ├─ 🎖️ CP: +10                             │     ║
║  │ ├─ 🏗️ Building XP: +50                    │     ║
║  │ └─ Chance: 🎁 Blueprint (15%)             │     ║
║  │                                            │     ║
║  │ [⚡ START WORK] [⏭️ Skip (-100💰)]        │     ║
║  └────────────────────────────────────────────┘     ║
║                                                      ║
║  ┌────────────────────────────────────────────┐     ║
║  │ 🛡️ GUARD DUTY                              │     ║
║  ├────────────────────────────────────────────┤     ║
║  │ Patrol city walls and watch for threats    │     ║
║  │                                            │     ║
║  │ Duration: ⏱️ 3 hours                       │     ║
║  │ Energy Cost: ⚡ -30                        │     ║
║  │                                            │     ║
║  │ Rewards:                                   │     ║
║  │ ├─ 💰 Gold: 600                           │     ║
║  │ ├─ 🎖️ CP: +12                             │     ║
║  │ ├─ ⚔️ Combat XP: +30                      │     ║
║  │ └─ Chance: ⚔️ Weapon (10%)                │     ║
║  │                                            │     ║
║  │ Random Events:                             │     ║
║  │ • Spot enemy spy (30% chance) → +50💰     │     ║
║  │ • Prevent theft (20% chance) → +100💰     │     ║
║  │                                            │     ║
║  │ [🛡️ START PATROL] [⏭️ Skip]               │     ║
║  └────────────────────────────────────────────┘     ║
║                                                      ║
║  ┌────────────────────────────────────────────┐     ║
║  │ 💼 MARKET ASSISTANT                        │     ║
║  ├────────────────────────────────────────────┤     ║
║  │ Help manage city marketplace               │     ║
║  │                                            │     ║
║  │ Duration: ⏱️ 1 hour                        │     ║
║  │ Energy Cost: ⚡ -10                        │     ║
║  │                                            │     ║
║  │ Rewards:                                   │     ║
║  │ ├─ 💰 Gold: 300                           │     ║
║  │ ├─ 🎖️ CP: +8                              │     ║
║  │ ├─ 💼 Trade XP: +25                       │     ║
║  │ └─ Chance: 🎫 Discount Coupon (25%)       │     ║
║  │                                            │     ║
║  │ [💼 START WORK] [⏭️ Skip]                  │     ║
║  └────────────────────────────────────────────┘     ║
║                                                      ║
║  ┌────────────────────────────────────────────┐     ║
║  │ 🎯 MINI-GAME: Quiz Master                  │     ║
║  ├────────────────────────────────────────────┤     ║
║  │ Answer 5 questions correctly               │     ║
║  │                                            │     ║
║  │ Duration: ⏱️ 15 minutes                    │     ║
║  │ Energy Cost: ⚡ -5                         │     ║
║  │                                            │     ║
║  │ Rewards (5/5 correct):                     │     ║
║  │ ├─ 💰 Gold: 500                           │     ║
║  │ ├─ 🎖️ CP: +15                             │     ║
║  │ ├─ 🧠 Intelligence: +10                   │     ║
║  │ └─ 🏆 Quiz Master Badge                   │     ║
║  │                                            │     ║
║  │ Difficulty: ⭐⭐⭐ Medium                   │     ║
║  │                                            │     ║
║  │ [🎮 PLAY NOW] [⏭️ Skip]                    │     ║
║  └────────────────────────────────────────────┘     ║
║                                                      ║
║  ━━━━━━━━━━ WORK BONUSES ━━━━━━━━━━                 ║
║                                                      ║
║  Current Bonuses:                                    ║
║  ✨ Work Streak (12 days): +10% gold rewards        ║
║  💑 Couple Bonus: +5% all rewards                   ║
║  🎂 Birthday Month: +15% XP                         ║
║  🏆 Top Worker Title: +8% CP gains                  ║
║                                                      ║
║  Next Milestone:                                     ║
║  18-day streak: 💎 50 gems + 🎖️ 100 CP bonus       ║
║                                                      ║
║  [📊 Work History] [🏆 Work Achievements] [◀️ Back] ║
╚══════════════════════════════════════════════════════╝
```

---

## 💑 **COUPLES BOARD**

```
╔══════════════════════════════════════════════════════╗
║            💑 COUPLES & RELATIONSHIPS                ║
║            @Username & @Partner                      ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  Relationship Status: 💕 Dating                     ║
║  Together Since: Jan 15, 2026 (28 days)             ║
║  Relationship Level: 2 (Serious)                     ║
║  Next Level: 62 days (Engaged)                       ║
║                                                      ║
║  ━━━━━━━━━━ COUPLE STATS ━━━━━━━━━━                 ║
║                                                      ║
║  💖 Love Points: 850/1000                           ║
║  ├─ Daily interactions: +5/day                      ║
║  ├─ Gifts exchanged: 12 (+120)                      ║
║  ├─ Missions together: 8 (+80)                      ║
║  ├─ Wars fought together: 3 (+90)                   ║
║  └─ Time spent: 28 days (+28)                       ║
║                                                      ║
║  🏠 Shared House: Level 2 Apartment                 ║
║  ├─ Rent: 400💰/week (200💰 each)                   ║
║  ├─ Capacity: 2 residents                           ║
║  ├─ Decorations: 5 items                            ║
║  └─ [🏠 Manage House]                                ║
║                                                      ║
║  💰 Joint Account:                                   ║
║  ├─ Balance: 12,500 💰                              ║
║  ├─ Your contribution: 8,000 (64%)                  ║
║  ├─ Partner contribution: 4,500 (36%)               ║
║  └─ [💰 Manage Finances]                             ║
║                                                      ║
║  ━━━━━━━━━ COUPLE BONUSES ━━━━━━━━━                 ║
║                                                      ║
║  Active Bonuses:                                     ║
║  ✅ +20% Combined Income                             ║
║  ✅ +30% Attack Power (when fighting together)       ║
║  ✅ 0% Tax on Gifts                                  ║
║  ✅ Shared Experience (+10% XP each)                 ║
║  ✅ Emotional Support (Morale +15%)                  ║
║                                                      ║
║  Upcoming Bonuses (Level 3 - Engaged):               ║
║  🔒 Couple Business (+50% profit)                    ║
║  🔒 Wedding Planning (unlock marriage)               ║
║  🔒 Family System (cosmetic kids)                    ║
║                                                      ║
║  ━━━━━━━━ COUPLE MISSIONS ━━━━━━━━                  ║
║                                                      ║
║  🎯 Daily Couple Mission:                            ║
║  "Win a battle together"                             ║
║  Progress: ▓▓▓▓▓░░░░░ 50% (1/2 completed)           ║
║  Reward: 💰 2,000 + 💎 25 gems + 💖 50 Love Points  ║
║  [⚔️ Continue Mission]                               ║
║                                                      ║
║  Weekly Challenge:                                   ║
║  "Earn 10,000 gold together"                         ║
║  Progress: ▓▓▓▓▓▓░░░░ 65% (6,500/10,000)            ║
║  Reward: 🏠 House Upgrade + 🏆 Power Couple Badge   ║
║                                                      ║
║  ━━━━━━━ QUICK ACTIONS ━━━━━━━                      ║
║                                                      ║
║  [🎁 Gift Partner] [💬 Send Message] [📸 Photo]     ║
║  [⚔️ Team Attack] [🏠 Visit Home] [📊 Stats]        ║
║  [🎊 Plan Date] [💔 Breakup] [◀️ Back]              ║
║                                                      ║
║  ━━━━━━━ RELATIONSHIP MILESTONES ━━━━━━━            ║
║                                                      ║
║  ✅ First Date (Day 1)                               ║
║  ✅ First Gift (Day 3)                               ║
║  ✅ First Battle Together (Day 7)                    ║
║  ✅ Moved in Together (Day 14)                       ║
║  ✅ First Anniversary (Day 30) - IN 2 DAYS! 🎉      ║
║  🔒 Engagement (Day 90)                              ║
║  🔒 Marriage (Day 180)                               ║
╚══════════════════════════════════════════════════════╝
```

---

## 🎂 **BIRTHDAY CELEBRATION BOARD**

```
╔══════════════════════════════════════════════════════╗
║        🎂 HAPPY BIRTHDAY, @ALICE! 🎉                 ║
║        Turning 25 Today - Feb 12, 2026               ║
╠══════════════════════════════════════════════════════╝
║                                                      ║
║  🎊 CITY-WIDE CELEBRATION IN PROGRESS! 🎊            ║
║                                                      ║
║  ━━━━━━━━━ BIRTHDAY GIFTS ━━━━━━━━━                 ║
║                                                      ║
║  🎁 FROM THE CITY:                                   ║
║  ├─ 💰 10,000 Gold                                  ║
║  ├─ 💎 100 Gems                                     ║
║  ├─ 🎫 Birthday Buff (24 hours)                     ║
║  │   • 2x XP for all activities                     ║
║  │   • 2x Work rewards                              ║
║  │   • Free shop items (up to 1,000💰)              ║
║  ├─ 🏆 "Birthday Star" Title (7 days)               ║
║  └─ 🎊 Party Decorations for profile                ║
║                                                      ║
║  [🎁 CLAIM ALL REWARDS]                              ║
║                                                      ║
║  ━━━━━━━━ CITIZEN GIFTS ━━━━━━━━                    ║
║                                                      ║
║  From @Mayor:                                        ║
║  🎁 "Leadership Guide Book" + 💰 5,000              ║
║  💬 "Happy birthday! You're a great citizen!"       ║
║                                                      ║
║  From @Bob (Partner):                                ║
║  💝 "Diamond Ring" + 💎 50 gems                     ║
║  💬 "Love you! Best birthday together! 💕"          ║
║                                                      ║
║  From @Charlie (Best Friend):                        ║
║  🎁 "Legendary Sword" + ⚔️ +100 Attack              ║
║  💬 "You deserve the best! Have fun! 🎉"            ║
║                                                      ║
║  From @City Treasury:                                ║
║  💰 Automatic 2,500 gold bonus                      ║
║                                                      ║
║  Total Gifts Received: 12 gifts from 12 citizens    ║
║  [📨 View All] [💬 Thank Everyone]                   ║
║                                                      ║
║  ━━━━━━━━━ CITY PARTY ━━━━━━━━━                     ║
║                                                      ║
║  🎉 Party Status: ACTIVE (24 hours)                  ║
║                                                      ║
║  All Citizens Get Today:                             ║
║  ✨ +10% Income (celebrating Alice!)                 ║
║  ✨ +5% XP Gain                                       ║
║  ✨ Free cake item (consumable, +20 morale)          ║
║  ✨ Party mood boost (+15% productivity)             ║
║                                                      ║
║  Party Activities:                                   ║
║  🎮 Birthday Quiz Game (+500💰 if win)               ║
║  🎰 Birthday Raffle (1 free ticket)                  ║
║  🎵 Music & Dance (+10 morale)                       ║
║  🍰 Cake Cutting Ceremony (2 PM)                     ║
║                                                      ║
║  ━━━━━━━━ BIRTHDAY STATS ━━━━━━━━                   ║
║                                                      ║
║  🎂 Age: 25 years old                                ║
║  📅 Birthdays Celebrated in City: 1                  ║
║  🎁 Total Gifts Received (lifetime): 12              ║
║  💰 Total Birthday Earnings: 17,500 gold             ║
║  🏆 Birthday Achievement: "Quarter Century"          ║
║                                                      ║
║  ━━━━━━━━ MESSAGES (45) ━━━━━━━━                    ║
║                                                      ║
║  @David: "Happy birthday Alice! 🎂"                  ║
║  @Emma: "Have an amazing day! 🎉"                    ║
║  @Frank: "Wishing you the best year yet! 🎊"        ║
║  ... 42 more messages                                ║
║                                                      ║
║  [📨 View All Messages] [💬 Reply All]               ║
║                                                      ║
║  ━━━━━━━ SPECIAL BIRTHDAY BUFF ━━━━━━━              ║
║                                                      ║
║  🎫 BIRTHDAY STAR BUFF (Active: 24h)                 ║
║  ├─ 2x XP on all activities                         ║
║  ├─ 2x Gold from work                               ║
║  ├─ 2x Contribution Points                          ║
║  ├─ Free items up to 1,000💰 value                  ║
║  ├─ Priority in all queues                          ║
║  ├─ Special birthday emoji next to name: 🎂         ║
║  └─ Cannot be attacked today (birthday protection)   ║
║                                                      ║
║  Expires in: 23h 45m                                 ║
║                                                      ║
║  [🎊 CELEBRATE] [📸 Take Photo] [🎁 Open Gifts]     ║
╚══════════════════════════════════════════════════════╝
```

---

## ⚔️ **COMPETITION BOARD**

```
╔══════════════════════════════════════════════════════╗
║           🏆 CITY COMPETITIONS & RANKINGS            ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  ━━━━━━━━ ACTIVE COMPETITIONS ━━━━━━━━              ║
║                                                      ║
║  🔥 WEEKLY BUILDER CHALLENGE                         ║
║  ├─ Goal: Build the most structures                 ║
║  ├─ Time Remaining: 3 days 12 hours                 ║
║  ├─ Your Progress: 5 buildings built                ║
║  ├─ Current Rank: #3 of 45 participants             ║
║  │                                                   ║
║  │  TOP 3 LEADERS:                                  ║
║  │  🥇 @BuilderBob - 12 buildings                   ║
║  │  🥈 @ConstructorCarl - 8 buildings               ║
║  │  🥉 @YouAreHere - 5 buildings                    ║
║  │                                                   ║
║  ├─ Prizes:                                         ║
║  │  🥇 1st: 💰 10,000 + 🏗️ Master Builder Title    ║
║  │  🥈 2nd: 💰 5,000 + 🎖️ 200 CP                   ║
║  │  🥉 3rd: 💰 2,500 + 🎖️ 100 CP                   ║
║  │  Top 10: 💰 500 each                             ║
║  └─ [🏗️ Build Now] [📊 View Leaderboard]           ║
║                                                      ║
║  ⚔️ WARRIOR TOURNAMENT (Daily)                       ║
║  ├─ Goal: Win the most battles today                ║
║  ├─ Resets in: 8 hours                              ║
║  ├─ Your Score: 3 wins, 0 losses                    ║
║  ├─ Current Rank: #7 of 30 fighters                 ║
║  │                                                   ║
║  │  TOP 3:                                          ║
║  │  🥇 @WarriorX - 8 wins                           ║
║  │  🥈 @BattleMaster - 6 wins                       ║
║  │  🥉 @Gladiator99 - 5 wins                        ║
║  │                                                   ║
║  ├─ Daily Prizes:                                   ║
║  │  🥇 1st: 💰 3,000 + ⚔️ Legendary Weapon          ║
║  │  🥈 2nd: 💰 1,500 + ⚔️ Epic Weapon               ║
║  │  🥉 3rd: 💰 750 + ⚔️ Rare Weapon                 ║
║  └─ [⚔️ Battle Now] [📊 Rankings]                   ║
║                                                      ║
║  💼 TRADER OF THE MONTH                              ║
║  ├─ Goal: Highest trade volume                      ║
║  ├─ Month Progress: 18/30 days                      ║
║  ├─ Your Volume: 💰 45,000 traded                   ║
║  ├─ Rank: #5 of 28 traders                          ║
║  │                                                   ║
║  │  LEADERS:                                        ║
║  │  🥇 @MerchantKing - 💰 250,000                   ║
║  │  🥈 @TradeQueen - 💰 180,000                     ║
║  │  🥉 @DealMaker - 💰 120,000                      ║
║  │                                                   ║
║  ├─ Monthly Prizes:                                 ║
║  │  🥇 1st: 💰 25,000 + 💼 Trade Master Title      ║
║  │  🥈 2nd: 💰 15,000 + 🎖️ 500 CP                  ║
║  │  🥉 3rd: 💰 10,000 + 🎖️ 300 CP                  ║
║  └─ [💼 Trade Now] [📈 Statistics]                  ║
║                                                      ║
║  ━━━━━━━━ RIVALRY BATTLES ━━━━━━━━                  ║
║                                                      ║
║  Your Active Rivalries (2):                          ║
║                                                      ║
║  ⚔️ VS @EnemyPerson                                  ║
║  ├─ Challenge: Most XP in 7 days                    ║
║  ├─ Time Left: 4 days 8 hours                       ║
║  ├─ Your XP: 12,500                                 ║
║  ├─ Their XP: 15,200                                ║
║  ├─ Status: 🔴 You're losing by 2,700 XP            ║
║  └─ [📊 Details] [💪 Catch Up]                      ║
║                                                      ║
║  ⚔️ VS @CompetitorX                                  ║
║  ├─ Challenge: Most battles won (7 days)            ║
║  ├─ Time Left: 2 days 15 hours                      ║
║  ├─ Your Wins: 8                                    ║
║  ├─ Their Wins: 6                                   ║
║  ├─ Status: 🟢 You're winning by 2 battles          ║
║  └─ [📊 Details] [⚔️ Maintain Lead]                 ║
║                                                      ║
║  ━━━━━━━ OVERALL RANKINGS ━━━━━━━                   ║
║                                                      ║
║  🏆 CITY LEADERBOARDS:                               ║
║                                                      ║
║  📊 Contribution Points:                             ║
║     You: #12 (165 CP) | Leader: @TopCitizen (2,500) ║
║                                                      ║
║  💰 Wealth:                                          ║
║     You: #18 (5,420💰) | Leader: @RichGuy (250K)    ║
║                                                      ║
║  ⚔️ Combat Power:                                    ║
║     You: #9 (850 ATK) | Leader: @Warrior (3,200)    ║
║                                                      ║
║  🎖️ Overall Rank:                                    ║
║     You: #15 (Balanced Performance)                  ║
║                                                      ║
║  [🏆 Full Rankings] [📊 Detailed Stats] [◀️ Back]   ║
╚══════════════════════════════════════════════════════╝
```

---

# 📊 LEVEL & XP SYSTEM

## 🎯 **COMPLETE XP TABLE**

```
╔═══════╦═════════════╦══════════════╦══════════════════════════════╗
║ Level ║ XP Required ║ Total XP     ║ Unlocks                      ║
╠═══════╬═════════════╬══════════════╬══════════════════════════════╣
║   1   ║      —      ║       0      ║ Starting level               ║
║   2   ║   1,000     ║   1,000      ║ Basic trading                ║
║   3   ║   2,500     ║   3,500      ║ Join alliances               ║
║   4   ║   5,000     ║   8,500      ║ Personal business            ║
║   5   ║   8,500     ║  17,000      ║ Advanced weapons             ║
║   6   ║  13,000     ║  30,000      ║ Couple system                ║
║   7   ║  18,500     ║  48,500      ║ Rivalry challenges           ║
║   8   ║  25,000     ║  73,500      ║ Elite missions               ║
║   9   ║  33,000     ║ 106,500      ║ Advanced buildings           ║
║  10   ║  42,000     ║ 148,500      ║ Specialization choice        ║
║  15   ║ 100,000     ║ 500,000      ║ Black market access          ║
║  20   ║ 200,000     ║ 1,500,000    ║ Leadership positions         ║
║  25   ║ 350,000     ║ 3,500,000    ║ Legendary status             ║
║  30   ║ 550,000     ║ 7,000,000    ║ Master rank                  ║
║  40   ║ 1,200,000   ║ 18,000,000   ║ Elite commander              ║
║  50   ║ 2,500,000   ║ 40,000,000   ║ God tier                     ║
╚═══════╩═════════════╩══════════════╩══════════════════════════════╝
```

## 📈 **XP GAIN SOURCES (Complete List)**

### **Work & Tasks:**
```
Daily Work (Varies by job):
├─ Construction Worker:     50-100 XP
├─ Guard Duty:              75-125 XP
├─ Market Assistant:        40-80 XP
├─ Mini-game Success:       100-200 XP
└─ Streak Bonus (7 days):   +500 XP

Special Tasks:
├─ Build structure:         200 XP
├─ Upgrade building:        150 XP per level
├─ Donate resources:        10 XP per 100💰 donated
└─ Help citizen:            50 XP
```

### **Combat:**
```
Battle Victories:
├─ Win attack:              300 XP
├─ Perfect victory (0 casualties): +200 XP bonus
├─ Win defense:             400 XP
├─ Defeat major enemy:      500 XP
└─ War participation:       150 XP (win or lose)

Combat Skills:
├─ Kill enemy troop:        5 XP each
├─ Destroy building:        250 XP
├─ Capture spy:             150 XP
└─ Defend ally:             200 XP
```

### **Economic:**
```
Trading:
├─ Complete trade:          100 XP
├─ Fair trade bonus:        +50 XP
├─ Large trade (10K+):      200 XP
└─ Auction win:             150 XP

Business:
├─ Daily profit:            1 XP per 10💰 earned
├─ Business milestone:      500 XP
└─ Trade route established: 300 XP
```

### **Social:**
```
Relationships:
├─ Make new friend:         50 XP
├─ Form couple:             500 XP
├─ Anniversary (30 days):   300 XP
├─ Win rivalry:             400 XP
└─ Get promoted:            1,000 XP

Community:
├─ Help citizen mission:    100 XP
├─ City event participation: 200 XP
├─ Vote in city poll:       10 XP
└─ Birthday gift given:     25 XP
```

### **Achievements:**
```
Milestones:
├─ First battle won:        200 XP
├─ 10 battles won:          500 XP
├─ 50 battles won:          2,000 XP
├─ 100 battles won:         5,000 XP
└─ 500 battles won:         25,000 XP

Specialization:
├─ Master Builder:          3,000 XP
├─ War Hero:                3,000 XP
├─ Trade Mogul:             3,000 XP
└─ Legendary Citizen:       10,000 XP
```

### **Special Events:**
```
Events:
├─ Seasonal event:          500-2,000 XP
├─ City festival:           300 XP
├─ Competition top 3:       1,000-3,000 XP
└─ Secret achievement:      5,000 XP
```

## 🔥 **XP MULTIPLIERS**

```
Base XP × Multipliers:

TIME-BASED:
├─ Birthday (24h):          2x XP
├─ Weekend bonus:           1.5x XP
├─ City festival:           1.3x XP
└─ Event period:            1.5x-3x XP

RELATIONSHIP:
├─ Couple bonus:            1.1x XP
├─ Best friend nearby:      1.05x XP
└─ City morale >80%:        1.2x XP

RANK/STATUS:
├─ VIP member:              1.25x XP
├─ Officer rank:            1.15x XP
├─ Top contributor:         1.1x XP
└─ Legendary status:        1.5x XP

ITEMS/BUFFS:
├─ XP Boost potion:         2x XP (1 hour)
├─ Mentor present:          1.2x XP
├─ Training facility:       1.15x XP
└─ Wisdom scroll:           1.3x XP (24h)

STREAK BONUSES:
├─ 7-day active streak:     1.1x XP
├─ 30-day streak:           1.25x XP
├─ 100-day streak:          1.5x XP
└─ 365-day streak:          2x XP
```

---

# 💰 MONEY & ECONOMY

## 💵 **INCOME SOURCES (Complete)**

### **Passive Income:**
```
City Buildings (Per Hour):
├─ Gold Mine Level 1:       +50 💰/hr
├─ Gold Mine Level 5:       +250 💰/hr
├─ Gold Mine Level 10:      +500 💰/hr
├─ Lumber Mill (sell wood): +30-150 💰/hr
├─ Quarry (sell stone):     +20-100 💰/hr
├─ Farm (sell food):        +40-200 💰/hr
└─ Factory (production):    +100-500 💰/hr

Personal Business:
├─ Shop (daily profit):     200-2,000 💰/day
├─ Inn (passive):           100-500 💰/day
├─ Casino (house edge):     500-5,000 💰/day
├─ Bank (interest):         5% of loans/day
└─ Factory (crafting):      varies by product

Interest & Investments:
├─ Bank savings:            1-2% daily
├─ City bonds:              5% weekly
├─ Stock market:            varies (-50% to +200%)
└─ Real estate:             10% monthly
```

### **Active Income:**
```
Work (24h cooldown):
├─ Construction:            300-500 💰
├─ Guard duty:              400-600 💰
├─ Market help:             200-400 💰
├─ Mini-game win:           200-500 💰
└─ Streak bonus (7d):       +50% rewards

Combat:
├─ Attack victory:          Loot 30% of enemy treasury
├─ Defense win:             Keep all + 1,000 💰 bonus
├─ Bounty hunting:          Varies by target
├─ Tournament prizes:       1,000-50,000 💰
└─ War spoils:              Shared among participants

Trading:
├─ Sell resources:          Market price (varies)
├─ Trade margins:           10-30% profit
├─ Auction sales:           Your pricing
├─ Export deals:            Bulk bonuses
└─ Broker fees:             5% of deal value

Couple Income:
├─ Joint work:              +20% combined
├─ Duo attacks:             +30% loot
├─ Shared business:         +50% profit
└─ Anniversary gift:        10,000 💰 (monthly)
```

### **Special Income:**
```
Achievements:
├─ First city:              1,000 💰
├─ Level milestones:        500-10,000 💰
├─ Competition wins:        1,000-25,000 💰
└─ Legendary status:        100,000 💰

Events:
├─ Birthday:                10,000 💰
├─ City festival:           2,000 💰
├─ Random events:           500-5,000 💰
└─ Mayor gifts:             Varies

Contributions:
├─ Recruit citizen:         500 💰
├─ City growth bonus:       1,000 💰/level
├─ Promotion rewards:       500-5,000 💰
└─ Mayor salary (officers): 1,000-5,000 💰/week
```

## 💸 **EXPENSES**

### **Fixed Costs:**
```
Living Expenses:
├─ Housing (rent):          200-1,000 💰/week
├─ Food:                    50-100 💰/day
├─ Healthcare:              100 💰/week
└─ Insurance:               200 💰/week

Taxes:
├─ Income tax:              1-30% (set by mayor)
├─ Trade tax:               5-10% per transaction
├─ Business tax:            10% of profits
└─ Property tax:            500 💰/month
```

### **Variable Costs:**
```
Combat:
├─ Troop training:          100-500 💰 per unit
├─ Weapons:                 500-50,000 💰
├─ Armor:                   300-30,000 💰
├─ Healing:                 50-200 💰 per soldier
└─ Attack launch:           200 💰 minimum

Building:
├─ Construct building:      1,000-100,000 💰
├─ Upgrade building:        Level × 500 💰
├─ Repair damage:           Varies
└─ Decorations:             100-10,000 💰

Social:
├─ Gifts:                   100-10,000 💰
├─ Proposals:               1,000 💰
├─ Wedding:                 5,000 💰
├─ Date expenses:           500 💰
└─ Rivalry stake:           1,000 💰 minimum
```

## 📊 **WEALTH TIERS**

```
Poverty:        0 - 5,000 💰
  └─ Struggling, need work

Lower Class:    5,001 - 25,000 💰
  └─ Stable, basic needs met

Middle Class:   25,001 - 100,000 💰
  └─ Comfortable, some luxuries

Upper Class:    100,001 - 500,000 💰
  └─ Wealthy, multiple businesses

Elite:          500,001 - 2,000,000 💰
  └─ Very rich, influential

Millionaire:    2,000,001 - 10,000,000 💰
  └─ Extremely wealthy, city leader

Billionaire:    10,000,001+ 💰
  └─ Legendary wealth, game mastery
```

---

# 🗺️ PLACES & LOCATIONS

## 🏛️ **CITY LOCATIONS**

```
╔══════════════════════════════════════════════════════╗
║              🗺️ CITY MAP - NEO MUMBAI               ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║     🏛️ CITY HALL (CENTER)                           ║
║     ├─ Mayor's Office                               ║
║     ├─ Council Chamber                              ║
║     ├─ Registry Office                              ║
║     └─ Public Notice Board                          ║
║                                                      ║
║     🏪 MARKET DISTRICT (East)                        ║
║     ├─ General Store                                ║
║     ├─ Weapon Shop                                  ║
║     ├─ Armor Shop                                   ║
║     ├─ Potion Shop                                  ║
║     ├─ Black Market (Lv 15+, Night only)            ║
║     └─ Auction House                                ║
║                                                      ║
║     ⚔️ MILITARY QUARTER (North)                      ║
║     ├─ Barracks                                     ║
║     ├─ Training Grounds                             ║
║     ├─ Armory                                       ║
║     ├─ War Room                                     ║
║     └─ Hospital                                     ║
║                                                      ║
║     🏘️ RESIDENTIAL AREA (West)                       ║
║     ├─ Basic Housing                                ║
║     ├─ Apartments                                   ║
║     ├─ Luxury Homes                                 ║
║     ├─ Couple Houses                                ║
║     └─ Communal Garden                              ║
║                                                      ║
║     🏭 INDUSTRIAL ZONE (South)                       ║
║     ├─ Factories                                    ║
║     ├─ Workshops                                    ║
║     ├─ Mines                                        ║
║     ├─ Lumber Mills                                 ║
║     └─ Quarries                                     ║
║                                                      ║
║     🎪 ENTERTAINMENT DISTRICT                        ║
║     ├─ Casino                                       ║
║     ├─ Theater                                      ║
║     ├─ Arena (PvP fights)                           ║
║     ├─ Restaurant                                   ║
║     └─ Park                                         ║
║                                                      ║
║     🔬 RESEARCH CENTER                               ║
║     ├─ Laboratory                                   ║
║     ├─ Library                                      ║
║     ├─ Tech Workshop                                ║
║     └─ Innovation Hub                               ║
║                                                      ║
║     🕵️ SECRET AREAS (Hidden)                         ║
║     ├─ Underground Vault                            ║
║     ├─ Secret Tunnels                               ║
║     ├─ Ancient Ruins                                ║
║     └─ Forgotten Temple                             ║
╚══════════════════════════════════════════════════════╝
```

## 📍 **LOCATION INTERACTIONS**

### **Market District:**
```
/visit market

╔══════════════════════════════════════════════════════╗
║         🏪 MARKET DISTRICT - NEO MUMBAI              ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  Bustling marketplace filled with traders...        ║
║                                                      ║
║  Available Shops:                                    ║
║                                                      ║
║  🛒 GENERAL STORE                                    ║
║  ├─ Food supplies                                   ║
║  ├─ Basic tools                                     ║
║  └─ Daily necessities                               ║
║  [🚪 Enter]                                          ║
║                                                      ║
║  ⚔️ WEAPON SHOP                                      ║
║  ├─ Swords, axes, bows                              ║
║  ├─ Upgrades available                              ║
║  └─ Special orders                                  ║
║  [🚪 Enter]                                          ║
║                                                      ║
║  🛡️ ARMOR SHOP                                       ║
║  ├─ Light, medium, heavy armor                      ║
║  ├─ Shields & helmets                               ║
║  └─ Custom fitting                                  ║
║  [🚪 Enter]                                          ║
║                                                      ║
║  💊 POTION SHOP                                      ║
║  ├─ Health potions                                  ║
║  ├─ Buff potions                                    ║
║  └─ Rare elixirs                                    ║
║  [🚪 Enter]                                          ║
║                                                      ║
║  🏺 AUCTION HOUSE                                    ║
║  ├─ Live auctions                                   ║
║  ├─ Rare items                                      ║
║  └─ Player listings                                 ║
║  [🚪 Enter]                                          ║
║                                                      ║
║  Random Events:                                      ║
║  • Traveling merchant (rare items) - 15% chance     ║
║  • Pickpocket attempt - 5% chance                   ║
║  • Price discount day - 10% chance                  ║
║  • Special promotion - 8% chance                    ║
║                                                      ║
║  Citizens here (12):                                 ║
║  @Alice, @Bob, @Charlie, ... [View All]             ║
║                                                      ║
║  [💬 Chat] [🔍 Search] [🗺️ Map] [◀️ Leave]          ║
╚══════════════════════════════════════════════════════╝
```

### **Training Grounds:**
```
/visit training

╔══════════════════════════════════════════════════════╗
║      ⚔️ TRAINING GROUNDS - MILITARY QUARTER          ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  Soldiers train here daily...                        ║
║                                                      ║
║  Available Training:                                 ║
║                                                      ║
║  💪 STRENGTH TRAINING                                ║
║  ├─ Duration: 1 hour                                ║
║  ├─ Cost: 500 💰                                    ║
║  ├─ Result: +10 Attack permanently                  ║
║  └─ Cooldown: 24h                                   ║
║  [💪 Train]                                          ║
║                                                      ║
║  🏃 SPEED TRAINING                                   ║
║  ├─ Duration: 45 min                                ║
║  ├─ Cost: 400 💰                                    ║
║  ├─ Result: +5% Attack speed                        ║
║  └─ Cooldown: 24h                                   ║
║  [🏃 Train]                                          ║
║                                                      ║
║  🎯 ACCURACY TRAINING                                ║
║  ├─ Duration: 1.5 hours                             ║
║  ├─ Cost: 600 💰                                    ║
║  ├─ Result: +15% Critical hit chance                ║
║  └─ Cooldown: 24h                                   ║
║  [🎯 Train]                                          ║
║                                                      ║
║  ⚔️ SPARRING MATCH                                   ║
║  ├─ Fight another citizen                           ║
║  ├─ No real damage, practice only                   ║
║  ├─ Winner gets: 200 💰 + 50 XP                     ║
║  └─ [⚔️ Find Opponent]                               ║
║                                                      ║
║  Your Training Progress Today:                       ║
║  ├─ Strength: 2/3 sessions                          ║
║  ├─ Speed: 1/3 sessions                             ║
║  ├─ Accuracy: 0/3 sessions                          ║
║  └─ Total Training XP: 250                          ║
║                                                      ║
║  [📊 Training History] [🗺️ Map] [◀️ Leave]          ║
╚══════════════════════════════════════════════════════╝
```

### **Secret Location: Underground Vault**
```
/discover vault
(Only appears if you found the secret map)

╔══════════════════════════════════════════════════════╗
║         🔐 UNDERGROUND VAULT (SECRET)                ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  You've discovered a hidden vault beneath the city!  ║
║                                                      ║
║  ⚠️ This location is secret - only you can access   ║
║     unless you share the coordinates.                ║
║                                                      ║
║  🗝️ VAULT FEATURES:                                  ║
║                                                      ║
║  💎 TREASURE STORAGE                                 ║
║  ├─ Store unlimited gold (raid-proof!)              ║
║  ├─ Hide valuable items                             ║
║  ├─ Current stored: 25,000 💰                       ║
║  └─ [💰 Deposit] [💰 Withdraw]                       ║
║                                                      ║
║  📦 RARE ITEM CACHE                                  ║
║  ├─ Random rare items spawn here weekly             ║
║  ├─ Next spawn: 2 days 5 hours                      ║
║  ├─ Available now: Legendary Sword ⚔️               ║
║  └─ [🎁 Claim Items]                                 ║
║                                                      ║
║  🗺️ SECRET MAP                                       ║
║  ├─ Shows hidden locations                          ║
║  ├─ Treasure hunt markers                           ║
║  └─ [🗺️ View Map]                                   ║
║                                                      ║
║  🤝 INVITE SYSTEM                                    ║
║  ├─ Share vault with trusted friends                ║
║  ├─ Current members: Only you                       ║
║  ├─ Max members: 5                                  ║
║  └─ [📨 Invite Friend]                               ║
║                                                      ║
║  ⚠️ WARNING: If discovered by enemies, they may     ║
║     try to raid this vault!                          ║
║                                                      ║
║  [🔐 Lock Vault] [📊 Vault Stats] [◀️ Leave]        ║
╚══════════════════════════════════════════════════════╝
```

---

# 🎁 BUFFS & ITEMS

## ⚡ **BUFF SYSTEM**

### **Attack Buffs:**
```
⚔️ ATTACK BOOST (30 min)
├─ Cost: 1,000 💰
├─ Effect: +30% Attack Power
├─ Stackable: No
└─ Cooldown: 2 hours

⚔️ RAGE MODE (1 hour)
├─ Cost: 2,500 💰
├─ Effect: +50% Attack, -10% Defense
├─ Stackable: No
└─ Cooldown: 6 hours

⚔️ CRITICAL STRIKE (2 hours)
├─ Cost: 3,000 💰
├─ Effect: +25% Critical hit chance
├─ Stackable: Yes (max 2)
└─ Cooldown: 4 hours
```

### **Defense Buffs:**
```
🛡️ IRON SKIN (1 hour)
├─ Cost: 800 💰
├─ Effect: +20% Defense
├─ Stackable: No
└─ Cooldown: 2 hours

🛡️ FORTIFICATION (2 hours)
├─ Cost: 2,000 💰
├─ Effect: +40% Defense, -20% Speed
├─ Stackable: No
└─ Cooldown: 6 hours

🛡️ SHIELD WALL (30 min)
├─ Cost: 1,500 💰
├─ Effect: +60% Defense (cannot attack)
├─ Stackable: No
└─ Cooldown: 8 hours
```

### **Economic Buffs:**
```
💰 MIDAS TOUCH (24 hours)
├─ Cost: 5,000 💰
├─ Effect: +50% Gold from all sources
├─ Stackable: No
└─ Cooldown: 48 hours

💰 MERCHANT'S BLESSING (12 hours)
├─ Cost: 3,000 💰
├─ Effect: -20% Shop prices, +10% Sell prices
├─ Stackable: No
└─ Cooldown: 24 hours

💰 DOUBLE INCOME (6 hours)
├─ Cost: 4,000 💰
├─ Effect: 2x Passive income
├─ Stackable: No
└─ Cooldown: 24 hours
```

### **XP Buffs:**
```
📈 XP BOOST (1 hour)
├─ Cost: 1,000 💰 or 50 💎
├─ Effect: 2x XP gain
├─ Stackable: No
└─ Cooldown: 6 hours

📈 WISDOM (24 hours)
├─ Cost: 5,000 💰
├─ Effect: +30% XP gain
├─ Stackable: Yes (max 2)
└─ Cooldown: None

📈 LEARNING SPREE (48 hours)
├─ Cost: 10,000 💰
├─ Effect: +50% XP, +25% Skill gains
├─ Stackable: No
└─ Cooldown: 72 hours
```

### **Special Buffs:**
```
🎂 BIRTHDAY BUFF (24 hours)
├─ Cost: Free (birthday only)
├─ Effect: 2x XP, 2x Gold, 2x CP, Cannot be attacked
├─ Stackable: With other buffs
└─ Cooldown: 365 days

💑 COUPLE BUFF (Permanent while coupled)
├─ Cost: Free
├─ Effect: +20% Joint income, +30% Duo attack
├─ Stackable: Yes
└─ Cooldown: None

🏆 CHAMPION BUFF (7 days)
├─ Cost: Win competition
├─ Effect: +15% All stats, Special title
├─ Stackable: Yes
└─ Cooldown: None (must win again)

🌟 VIP BUFF (30 days)
├─ Cost: 💎 500 gems or $4.99
├─ Effect: +25% XP, +10% Income, Priority queue
├─ Stackable: With other buffs
└─ Cooldown: None (subscription)
```

## 🎒 **ITEMS & EQUIPMENT**

### **Weapons (Attack):**
```
⚔️ MELEE WEAPONS:
├─ Rusty Sword:        +50 ATK  | 💰 500
├─ Iron Sword:         +120 ATK | 💰 2,000
├─ Steel Blade:        +250 ATK | 💰 8,000
├─ Katana:             +400 ATK | 💰 20,000
├─ Legendary Sword:    +800 ATK | 💰 100,000
└─ Excalibur (Mythic): +1,500 ATK | 💰 500,000

🏹 RANGED WEAPONS:
├─ Basic Bow:          +40 ATK  | 💰 400
├─ Crossbow:           +100 ATK | 💰 1,800
├─ Longbow:            +220 ATK | 💰 7,000
├─ Compound Bow:       +380 ATK | 💰 18,000
├─ Magic Bow:          +750 ATK | 💰 90,000
└─ Phoenix Bow:        +1,400 ATK | 💰 450,000

💣 EXPLOSIVES:
├─ Grenade:            +80 ATK  | 💰 600 (consumable)
├─ Bomb:               +200 ATK | 💰 2,500 (consumable)
├─ C4:                 +500 ATK | 💰 10,000 (consumable)
└─ Nuke (Rare):        +2,000 ATK | 💰 1,000,000 (1-use)
```

### **Armor (Defense):**
```
🛡️ ARMOR SETS:
├─ Leather Armor:      +30 DEF  | 💰 300
├─ Iron Armor:         +80 DEF  | 💰 1,500
├─ Steel Armor:        +180 DEF | 💰 6,000
├─ Knight Armor:       +350 DEF | 💰 15,000
├─ Legendary Plate:    +700 DEF | 💰 80,000
└─ Dragon Scale:       +1,300 DEF | 💰 400,000

🛡️ SHIELDS:
├─ Wooden Shield:      +20 DEF  | 💰 200
├─ Iron Shield:        +60 DEF  | 💰 1,000
├─ Tower Shield:       +150 DEF | 💰 5,000
├─ Magic Shield:       +300 DEF | 💰 25,000
└─ Aegis (Mythic):     +800 DEF | 💰 300,000
```

### **Consumables:**
```
💊 POTIONS:
├─ Health Potion (S):  Heal 100 HP | 💰 100
├─ Health Potion (M):  Heal 300 HP | 💰 300
├─ Health Potion (L):  Heal 1000 HP | 💰 1,000
├─ Full Restore:       100% HP | 💰 5,000
└─ Phoenix Down:       Revive from death | 💰 50,000

⚡ ENERGY:
├─ Energy Drink:       +20 Energy | 💰 150
├─ Coffee:             +10 Energy | 💰 50
├─ Power Bar:          +30 Energy | 💰 250
└─ Full Energy:        +100 Energy | 💰 2,000

🎁 BOOST ITEMS:
├─ Lucky Charm:        +10% Luck (24h) | 💰 500
├─ Speed Boots:        +20% Speed (1h) | 💰 800
├─ Strength Potion:    +15% ATK (30m) | 💰 600
└─ Intelligence Book:  +25% XP (2h) | 💰 1,200
```

---

# 🎲 FORMULAS & CALCULATIONS

## ⚔️ **COMBAT FORMULAS**

### **Battle Power Calculation:**
```javascript
Total Attack Power = 
    (Base Attack × Level Multiplier) +
    (Weapon Attack) +
    (Troop Count × Troop Power) +
    (Active Buffs %) +
    (City Type Bonus %) +
    (Couple Bonus if applicable)

Total Defense Power = 
    (Wall Level × 100) +
    (Tower Count × 50) +
    (Defending Troops × Troop Power) +
    (Armor Defense) +
    (Active Buffs %) +
    (City Type Bonus %)

Level Multiplier = 1 + (Level × 0.05)
// Level 1 = 1.05x
// Level 10 = 1.5x
// Level 50 = 3.5x

Example:
User Level 10:
- Base Attack: 100
- Weapon: +250 (Steel Blade)
- Troops: 30 × 10 power = 300
- Buff: +30% (Attack Boost active)
- City Bonus: +10% (Military City)
- Couple: +30% (Fighting with partner)

Calculation:
Base = (100 × 1.5) + 250 + 300 = 700
With buffs: 700 × 1.30 × 1.10 × 1.30 = 1,301 Attack Power
```

### **Battle Outcome:**
```javascript
Win Probability = 
    Attack Power / (Attack Power + Defense Power)

Random Variance = ±10%

Final Win Chance = Win Probability ± Random Variance

Loot Calculation (if win):
Loot = Enemy Treasury × (0.20 to 0.40)
// 20-40% of enemy's total gold

Casualties (if lose):
Lost Troops = Your Troops × (0.30 to 0.60)
// Lose 30-60% of troops

Building Damage (if win):
Target random enemy building
Damage = -1 to -3 levels
// Building loses 1-3 levels
```

## 💰 **ECONOMIC FORMULAS**

### **Income Calculation:**
```javascript
Hourly Passive Income = 
    Σ(Building Production × Building Level) +
    (Business Daily Profit / 24) +
    (Investment Returns / 24) +
    (Rental Income / 24)

Daily Active Income =
    (Work Rewards × Work Count) +
    (Battle Loot) +
    (Trade Profits) +
    (Mission Rewards) +
    (Competition Prizes)

Tax Deduction = 
    (Total Income × City Tax Rate)

Net Income = 
    Total Income - Tax Deduction - Expenses

Example:
Passive (24h):
- Gold Mine L5: 250/hr × 24 = 6,000
- Shop Profit: 1,500/day
- Bank Interest: 500/day
Total Passive: 8,000/day

Active (24h):
- Work: 1,500
- Battles: 3,000
- Trades: 2,000
Total Active: 6,500/day

Grand Total: 14,500/day
Tax (12%): -1,740
Net: 12,760/day
```

### **Price Fluctuation:**
```javascript
Market Price = 
    Base Price × Supply/Demand Ratio × Event Multiplier

Supply/Demand Ratio =
    (Total Supply / Total Demand)
    // Ranges from 0.5x to 2.0x

Event Multiplier:
- Normal day: 1.0x
- Trade Festival: 0.8x (discount)
- War time: 1.3x (expensive)
- Shortage: 2.0x (very expensive)

Example:
Steel Sword Base Price: 8,000
Current Supply: Low (0.7x multiplier)
Event: War (1.3x multiplier)

Market Price = 8,000 × 0.7 × 1.3 = 7,280
```

## 📈 **XP & LEVEL FORMULAS**

### **XP Required for Next Level:**
```javascript
XP_Required(Level) = 
    Base_XP × (Level ^ Exponent) × Multiplier

Where:
- Level 1-10: Base = 1000, Exponent = 1.5
- Level 11-25: Base = 5000, Exponent = 1.8
- Level 26-50: Base = 20000, Exponent = 2.0

Example Calculations:
Level 5 → 6:
1000 × (5 ^ 1.5) = 1000 × 11.18 = 11,180 XP

Level 20 → 21:
5000 × (20 ^ 1.8) = 5000 × 80 = 400,000 XP
```

### **XP Gain with Multipliers:**
```javascript
Final_XP = 
    Base_XP × 
    Birthday_Mult × 
    Couple_Mult × 
    Buff_Mult × 
    VIP_Mult × 
    Streak_Mult

Example:
Base XP from work: 100

Active Multipliers:
- Birthday (2x)
- Couple (1.1x)
- XP Boost Buff (2x)
- 7-day Streak (1.1x)

Final XP = 100 × 2 × 1.1 × 2 × 1.1
         = 100 × 4.84
         = 484 XP
```

## 💑 **RELATIONSHIP FORMULAS**

### **Relationship Points:**
```javascript
Relationship_Change = 
    Base_Action_Points × 
    Frequency_Penalty × 
    Mutual_Interest_Bonus

Frequency Penalty:
- First time today: 1.0x
- 2nd time today: 0.8x
- 3rd time today: 0.5x
- 4+ times today: 0.2x

Mutual Interest:
- Both online: 1.2x
- One online: 1.0x
- Both offline: 0.8x

Example:
@User gives gift to @Friend
- Base Points: +10
- 1st gift today: 1.0x
- Both online: 1.2x

Final = 10 × 1.0 × 1.2 = +12 relationship points
```

### **Love Points (Couples):**
```javascript
Daily_Love_Points = 
    (Time_Together × 0.5) +
    (Gifts_Exchanged × 10) +
    (Missions_Together × 15) +
    (Battles_Won_Together × 20) +
    Base_Daily_Gain

Base_Daily_Gain = 5 points/day

Decay (if no interaction):
- 1 day no interaction: -2 points
- 3 days: -10 points/day
- 7 days: -20 points/day
- 14 days: Auto breakup

Example:
Day Activity:
- Spent 2 hours together: +1 point
- Exchanged 2 gifts: +20 points
- Won 1 battle together: +20 points
- Base gain: +5 points

Total: +46 love points today
```

## 🎖️ **CONTRIBUTION POINTS (CP) Formula:**
```javascript
CP_Gain = 
    Base_CP × 
    Activity_Quality_Mult × 
    Streak_Mult × 
    City_Rank_Mult

Activity Quality:
- Perfect work: 1.5x
- Normal work: 1.0x
- Failed work: 0.5x

Streak Multiplier:
- 7-day: 1.1x
- 30-day: 1.25x
- 100-day: 1.5x

City Rank Multiplier:
- Top 10 city: 1.2x
- Top 50 city: 1.1x
- Others: 1.0x

Example:
Work task completed perfectly
- Base CP: 10
- Perfect quality: 1.5x
- 7-day streak: 1.1x
- Top 10 city: 1.2x

Final = 10 × 1.5 × 1.1 × 1.2 = 19.8 ≈ 20 CP
```

---

# 🎉 SPECIAL FEATURES

## 🎰 **RANDOM EVENTS SYSTEM**

### **Daily Random Events (5% chance each):**

```
1. 💰 GOLD RUSH (6 hours)
   - All income sources × 2
   - City-wide effect
   - Notification to all citizens

2. 🌧️ STORM (-20% productivity)
   - All work slower
   - Attack power -15%
   - Lasts 3 hours

3. 🎊 SURPRISE FESTIVAL
   - Free items for everyone
   - +50% morale
   - 💰 1,000 bonus to all
   - Lasts 12 hours

4. 🏴‍☠️ BANDIT RAID
   - Random NPC attack
   - Must defend or lose gold
   - Rewards if defeated

5. 🔮 MYSTICAL PORTAL
   - Appears for 30 minutes
   - Transport to secret area
   - Rare loot available

6. 👽 ALIEN ENCOUNTER
   - Choice event:
     • Trade (tech boost)
     • Fight (big loot risk)
     • Ignore (safe)

7. 🎁 TREASURE HUNT
   - Hidden treasure in city
   - First to find wins
   - Prize: 💰 5,000 + rare item

8. 🌟 LUCKY DAY
   - All RNG chances +50%
   - Double rewards
   - Lasts 4 hours
```

## 🏆 **ACHIEVEMENT SYSTEM (100+ Achievements)**

### **Categories:**

```
COMBAT (25 achievements):
├─ First Blood (Win 1 battle)
├─ Warrior (Win 10 battles)
├─ Gladiator (Win 50 battles)
├─ War Hero (Win 100 battles)
├─ Legendary Fighter (Win 500 battles)
├─ Undefeated (Win 20 without loss)
├─ Perfect Victory (0 casualties)
├─ Giant Slayer (Beat city 2x your size)
└─ ... +17 more

ECONOMIC (25 achievements):
├─ First Sale (Complete 1 trade)
├─ Merchant (Complete 50 trades)
├─ Tycoon (Earn 100K total gold)
├─ Millionaire (Own 1M gold at once)
├─ Business Mogul (Own 5 businesses)
├─ Stock Expert (100 investments)
├─ Philanthropist (Donate 50K total)
└─ ... +18 more

SOCIAL (25 achievements):
├─ Popular (10 friends)
├─ Social Butterfly (50 friends)
├─ True Love (30-day relationship)
├─ Power Couple (Max love points)
├─ Matchmaker (Help 5 couples form)
├─ Party Animal (Host 10 events)
├─ Gift Giver (Give 100 gifts)
└─ ... +18 more

PROGRESSION (25 achievements):
├─ Level milestones (5, 10, 25, 50)
├─ XP milestones (100K, 1M, 10M)
├─ Contribution (100, 500, 1000 CP)
├─ Work Streak (7, 30, 100 days)
├─ Perfect Attendance (365 days)
└─ ... +20 more

SPECIAL (Hidden):
├─ Time Traveler (Play on leap day)
├─ Night Owl (Active at 3 AM)
├─ Lucky Charm (Win 10 lotteries)
├─ Hacker (Find all secrets)
└─ Immortal (Never die in battle 1 year)
```

---

# 🎮 **MINI-GAMES**

## 🎯 **Quiz Game:**
```
/playgame quiz

╔══════════════════════════════════════════════════════╗
║            🎯 QUIZ MASTER CHALLENGE                  ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  Question 1/5:                                       ║
║                                                      ║
║  What is the maximum level in City Empire?           ║
║                                                      ║
║  A) 50                                               ║
║  B) 100                                              ║
║  C) 200                                              ║
║  D) Unlimited                                        ║
║                                                      ║
║  Time Remaining: ⏰ 00:25                            ║
║                                                      ║
║  [A] [B] [C] [D]                                     ║
║                                                      ║
║  Prizes:                                             ║
║  5/5 Correct: 💰 500 + 🎖️ 15 CP + 🧠 +10 INT       ║
║  3-4 Correct: 💰 300 + 🎖️ 10 CP                    ║
║  1-2 Correct: 💰 100 + 🎖️ 5 CP                     ║
║  0 Correct: Better luck next time!                   ║
╚══════════════════════════════════════════════════════╝
```

## 🎰 **Casino Games:**
```
/visit casino

Available Games:
├─ 🎰 Slot Machine (100-10,000 💰 bet)
├─ 🃏 Blackjack (500-50,000 💰 bet)
├─ 🎲 Dice Roll (100-100,000 💰 bet)
├─ 🎡 Wheel of Fortune (1,000 💰 spin)
└─ 🏇 Virtual Horse Racing (Bet on races)

House Edge: 5%
Max Win: 1,000,000 💰
VIP Perks: Better odds
```

---

Bhai yeh **COMPLETE MEGA FILE** hai! 📄🔥

**Is file mein hai:**
✅ Har board ki detailed design
✅ Complete command list (100+ commands)
✅ Couples, birthdays, jealousy system
✅ Normal user se officer tak promotion
✅ Level/XP/Money formulas
✅ Places & locations
✅ Competition systems
✅ Relationships & reputation
✅ 100+ achievements
✅ Random events
✅ Mini-games
✅ Har buff ka breakdown
✅ Complete economy system

**FILE SIZE:** 50KB+ of pure game design! 🎮

Kuch aur add karna hai? Koi specific feature detail mein chahiye? 🚀
