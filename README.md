# NetHorizon

## NetHorizon – Redefining Internet Access 

### With transparent pricing, customer-first bundles, and a long-term mission to move toward free internet access, we’re not just another ISP—we’re a movement.

## Technology Stack

### Frontend (Port 5000)
- **Framework**: React 18+ with Hooks
- **UI Library**: Material-UI / Tailwind CSS
- **Charts**: Recharts, D3.js for real-time bandwidth visualization
- **State Management**: React Context API / Redux Toolkit
- **Real-time**: Socket.io-client
- **HTTP Client**: Axios
- **Routing**: React Router v6

### Backend (Port 3000)
- **Framework**: FastAPI (Python 3.10+)
- **Database**: PostgreSQL 14+
- **ORM**: SQLAlchemy 2.0
- **Authentication**: JWT (PyJWT)
- **Real-time**: Socket.io (python-socketio)
- **Task Queue**: Celery with Redis
- **Caching**: Redis
- **API Documentation**: Swagger/OpenAPI (built-in FastAPI)

### Payment Integration
- **Stripe**: For international cards
- **WHISH**: For local and international cards and online payments
- **OMT**: Lebanon mobile money
- **Suyool**: Middle East payment gateway
- **PayPal**: Global payments
- **Cash**: Manual verification system

### AI Assistant
- **LLM**: OpenAI GPT-4 / Anthropic Claude API
- **Vector DB**: Pinecone / Chroma for knowledge base
- **Framework**: LangChain for RAG implementation
- **Memory**: Redis for conversation state

### Monitoring & Network Tools
- **Bandwidth Monitoring**: Python scapy, psutil
- **Network Scanning**: nmap (via python-nmap)
- **Packet Analysis**: tcpdump, tshark (via pyshark)
- **Metrics**: Prometheus + Grafana integration
- **Logging**: ELK Stack (Elasticsearch, Logstash, Kibana)

### Communication
- **Telegram Bot**: python-telegram-bot
- **WhatsApp**: Twilio API / WhatsApp Business API
- **Email**: SendGrid / AWS SES
- **SMS**: Twilio

### Security
- **Encryption**: AES-256 for data at rest
- **HTTPS**: Let's Encrypt SSL certificates
- **Rate Limiting**: slowapi
- **CORS**: Configured for secure cross-origin requests
- **Firewall**: UFW configuration
- **Master Access**: Encrypted SSH tunnel with 2FA

## Database Schema

### Core Tables
```sql
- users (id, email, password_hash, role, created_at)
- clients (id, user_id, subscription_id, status, activation_date)
- subscriptions (id, plan_name, speed, price, features)
- billing (id, client_id, amount, due_date, status, invoice_url)
- payments (id, billing_id, method, transaction_id, amount, timestamp)
- tickets (id, client_id, subject, status, priority, created_at)
- ticket_messages (id, ticket_id, user_id, message, timestamp)
- bandwidth_logs (id, client_id, download, upload, timestamp)
- network_logs (id, type, severity, message, timestamp)
- chat_sessions (id, client_id, ai_session_id, started_at)
- chat_messages (id, session_id, sender, message, timestamp)
- referrals (id, referrer_id, referee_id, status, reward_amount)
- loyalty_points (id, client_id, points, earned_date)
```

## Environment Variables (.env)

```env
# Backend
DATABASE_URL=postgresql://user:pass@localhost:5432/nethorizon
SECRET_KEY=your-super-secret-key-change-this
JWT_SECRET=your-jwt-secret-key
API_KEY=your-api-key-for-external-access
REDIS_URL=redis://localhost:6379

# Founder Access
FOUNDER_EMAIL=felipeeloco@pm.me
FOUNDER_BACKDOOR_KEY=encrypted-key-here
FOUNDER_SSH_PORT=2222

# AI Assistant
OPENAI_API_KEY=your-openai-key
ANTHROPIC_API_KEY=your-anthropic-key
PINECONE_API_KEY=your-pinecone-key

# Payment Gateways
STRIPE_SECRET_KEY=sk_live_xxx
STRIPE_PUBLISHABLE_KEY=pk_live_xxx
OMT_API_KEY=your-omt-key
SUYOOL_API_KEY=your-suyool-key
PAYPAL_CLIENT_ID=your-paypal-client
PAYPAL_SECRET=your-paypal-secret

# Communication
TELEGRAM_BOT_TOKEN=your-telegram-token
WHATSAPP_API_KEY=your-whatsapp-key
TWILIO_ACCOUNT_SID=your-twilio-sid
TWILIO_AUTH_TOKEN=your-twilio-token
SENDGRID_API_KEY=your-sendgrid-key

# Monitoring
PROMETHEUS_PORT=9090
GRAFANA_PORT=3001

# Frontend
REACT_APP_API_URL=http://localhost:3000
REACT_APP_WS_URL=ws://localhost:3000
```

## Setup Instructions

### 1. Clone Repository
```bash
git clone https://github.com/develoc/NetHorizon.git
cd NetHorizon
```

### 2. Backend Setup
```bash
cd backend
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
alembic upgrade head
python app/main.py
```

### 3. Frontend Setup
```bash
cd frontend
npm install
npm start
```

### 4. Database Setup
```bash
psql -U postgres
CREATE DATABASE nethorizon;
\q
python scripts/init_db.py
```

### 5. Start Services
```bash
# Terminal 1: Backend
cd backend && source venv/bin/activate && uvicorn app.main:app --host 0.0.0.0 --port 3000

# Terminal 2: Frontend
cd frontend && npm start

# Terminal 3: Redis
redis-server

# Terminal 4: Celery Worker
cd backend && celery -A app.worker worker --loglevel=info

# Terminal 5: Telegram Bot
cd bots/telegram_bot && python bot.py

# Terminal 6: Monitoring
cd monitoring && python scripts/bandwidth_collector.py
```

## Next Steps

1. Backend API with all endpoints
2. Frontend React application
3. Admin dashboard
4. Client portal with real-time bandwidth monitoring
5. Payment integration
6. AI chat assistant
7. Monitoring tools
8. Bot integrations

# NetHorizon - Complete Project Structure

```
NetHorizon/
├── frontend/                          # React Frontend (Port 5000)
│   ├── public/
│   │   ├── index.html
│   │   └── favicon.ico
│   ├── src/
│   │   ├── components/
│   │   │   ├── landing/
│   │   │   │   ├── Hero.jsx
│   │   │   │   ├── Mission.jsx
│   │   │   │   ├── Services.jsx
│   │   │   │   ├── Pricing.jsx
│   │   │   │   ├── Features.jsx
│   │   │   │   └── Contact.jsx
│   │   │   ├── admin/
│   │   │   │   ├── Dashboard.jsx
│   │   │   │   ├── UserManagement.jsx
│   │   │   │   ├── NetworkMonitoring.jsx
│   │   │   │   ├── BillingManagement.jsx
│   │   │   │   ├── TicketSystem.jsx
│   │   │   │   ├── Analytics.jsx
│   │   │   │   └── Settings.jsx
│   │   │   ├── client/
│   │   │   │   ├── ClientDashboard.jsx
│   │   │   │   ├── BandwidthMonitor.jsx
│   │   │   │   ├── BillingHistory.jsx
│   │   │   │   ├── SupportTickets.jsx
│   │   │   │   ├── ProfileSettings.jsx
│   │   │   │   └── PaymentPortal.jsx
│   │   │   ├── shared/
│   │   │   │   ├── Navbar.jsx
│   │   │   │   ├── Sidebar.jsx
│   │   │   │   ├── ChatWidget.jsx
│   │   │   │   ├── NotificationCenter.jsx
│   │   │   │   └── LoadingSpinner.jsx
│   │   │   └── charts/
│   │   │       ├── BandwidthChart.jsx
│   │   │       ├── UsageChart.jsx
│   │   │       └── RevenueChart.jsx
│   │   ├── pages/
│   │   │   ├── Landing.jsx
│   │   │   ├── AdminPortal.jsx
│   │   │   ├── ClientPortal.jsx
│   │   │   ├── Login.jsx
│   │   │   └── Register.jsx
│   │   ├── services/
│   │   │   ├── api.js
│   │   │   ├── auth.js
│   │   │   ├── websocket.js
│   │   │   └── payments.js
│   │   ├── utils/
│   │   │   ├── constants.js
│   │   │   ├── helpers.js
│   │   │   └── validators.js
│   │   ├── App.jsx
│   │   └── index.js
│   ├── package.json
│   └── .env
│
├── backend/                           # Python FastAPI Backend (Port 3000)
│   ├── app/
│   │   ├── api/
│   │   │   ├── v1/
│   │   │   │   ├── endpoints/
│   │   │   │   │   ├── auth.py
│   │   │   │   │   ├── users.py
│   │   │   │   │   ├── admin.py
│   │   │   │   │   ├── clients.py
│   │   │   │   │   ├── billing.py
│   │   │   │   │   ├── tickets.py
│   │   │   │   │   ├── payments.py
│   │   │   │   │   ├── monitoring.py
│   │   │   │   │   ├── chat.py
│   │   │   │   │   └── analytics.py
│   │   │   │   └── api.py
│   │   │   └── deps.py
│   │   ├── core/
│   │   │   ├── config.py
│   │   │   ├── security.py
│   │   │   ├── database.py
│   │   │   └── logging.py
│   │   ├── models/
│   │   │   ├── user.py
│   │   │   ├── client.py
│   │   │   ├── subscription.py
│   │   │   ├── billing.py
│   │   │   ├── ticket.py
│   │   │   ├── payment.py
│   │   │   └── network_log.py
│   │   ├── schemas/
│   │   │   ├── user.py
│   │   │   ├── client.py
│   │   │   ├── billing.py
│   │   │   └── ticket.py
│   │   ├── services/
│   │   │   ├── auth_service.py
│   │   │   ├── user_service.py
│   │   │   ├── billing_service.py
│   │   │   ├── payment_service.py
│   │   │   ├── ticket_service.py
│   │   │   ├── monitoring_service.py
│   │   │   ├── ai_assistant.py
│   │   │   ├── telegram_bot.py
│   │   │   ├── whatsapp_service.py
│   │   │   └── email_service.py
│   │   ├── utils/
│   │   │   ├── bandwidth_monitor.py
│   │   │   ├── network_tools.py
│   │   │   ├── nmap_scanner.py
│   │   │   ├── tcpdump_analyzer.py
│   │   │   └── helpers.py
│   │   ├── websockets/
│   │   │   ├── chat.py
│   │   │   ├── monitoring.py
│   │   │   └── notifications.py
│   │   └── main.py
│   ├── alembic/                       # Database migrations
│   │   ├── versions/
│   │   └── env.py
│   ├── tests/
│   │   ├── test_auth.py
│   │   ├── test_users.py
│   │   └── test_billing.py
│   ├── requirements.txt
│   ├── .env
│   └── Makefile
│
├── ai_assistant/                      # AI Assistant with Knowledge Base
│   ├── knowledge_base/
│   │   ├── company_info.json
│   │   ├── services.json
│   │   ├── pricing.json
│   │   ├── faqs.json
│   │   └── troubleshooting.json
│   ├── models/
│   │   └── fine_tuned_model/
│   ├── assistant.py
│   ├── training.py
│   └── requirements.txt
│
├── monitoring/                        # Network Monitoring Tools
│   ├── scripts/
│   │   ├── bandwidth_collector.py
│   │   ├── network_scanner.py
│   │   ├── traffic_analyzer.py
│   │   └── alert_manager.py
│   ├── config/
│   │   └── monitoring_config.yaml
│   └── requirements.txt
│
├── bots/                             # Telegram & WhatsApp Bots
│   ├── telegram_bot/
│   │   ├── bot.py
│   │   ├── handlers.py
│   │   └── requirements.txt
│   └── whatsapp_bot/
│       ├── bot.py
│       ├── handlers.py
│       └── requirements.txt
│
├── database/
│   ├── init.sql
│   └── seed.sql
│
├── docker/                           # Optional (you mentioned no Docker, but keeping for reference)
│   ├── Dockerfile.frontend
│   └── Dockerfile.backend
│
├── scripts/
│   ├── setup_venv.sh
│   ├── start_backend.sh
│   ├── start_frontend.sh
│   └── deploy.sh
│
├── docs/
│   ├── API.md
│   ├── SETUP.md
│   ├── DEPLOYMENT.md
│   └── USER_GUIDE.md
│
├── .github/
│   └── workflows/
│       ├── ci.yml
│       └── deploy.yml
│
├── .gitignore
├── README.md
└── LICENSE
```
