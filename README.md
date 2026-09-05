# AI Growth & Agentic Commerce

A student-friendly, modular full-stack e-commerce platform and AI Shopping Assistant demonstrating **Agentic Commerce**, **AI Product Recommendations**, **Smart Cross-Selling**, and **Merchant Growth Analytics**.

---

## 🌟 Project Overview & Key Features

1. **AI Shopping Assistant (Gemini API):**
   - Natural language comprehension (e.g. *"I want running shoes under ₹3000"*).
   - Conversational advice with embedded interactive product cards directly in the chat feed.
   - Built-in heuristic fallback engine ensuring seamless offline/demo operation without API keys.

2. **Dynamic Product Catalog & Search:**
   - Real-time keyword search across titles, descriptions, and tags.
   - Category filtering (`Footwear`, `Accessories`, `Apparel`, `Electronics`, `Fitness`).
   - Price range slider in INR (₹).

3. **Smart Product Recommendations & Cross-Selling:**
   - Content similarity scoring algorithm based on shared tags, category, and price proximity.
   - Contextual cross-selling pairings (e.g., *Velocity Pro Running Shoes &rarr; Anti-Blister Sports Socks*).
   - Bundle discount calculation (10% OFF combo pairings) with 1-click bundle add.

4. **Session Shopping Cart:**
   - Quantity modification steppers (`-` / `+`) and item removal.
   - Visual **Free Delivery Progress Meter** (Free delivery on orders &ge; ₹999).
   - Automatic 5% GST calculation.
   - In-Cart AI Cross-Sell suggestion cards.

5. **Test Checkout & Razorpay Test Mode:**
   - Shipping address and customer info collection.
   - Razorpay Test Mode order creation & signature verification (with Simulated Gateway fallback).
   - Payment error simulation toggle (test how the app gracefully handles bank declines).
   - Instant confirmed order receipt with itemized breakdown.

6. **Merchant Analytics Dashboard:**
   - Real-time KPI cards: Total Sales (₹), Completed Orders, Average Order Value (AOV), and Abandoned Cart Opportunity.
   - Ranked Top Selling Products list.
   - Low-Stock Inventory Watchlist alerts (< 20 units).
   - Recent Customer Orders table.

7. **AI Growth Insights & Cart Recovery:**
   - Autonomous AI growth insights (Cross-Sell Affinity, Inventory Restock Alerts, Delivery Conversion Optimization).
   - Abandoned cart tracking with 1-click **AI Recovery Email & SMS Generator** featuring custom discount coupon codes (`SAVE10`, `SAVE15`).

8. **Robust Error Handling:**
   - Product not found (404)
   - Empty cart checkout rejection (400)
   - Invalid AI inputs (400)
   - AI service fallback (zero crashes)
   - Payment decline simulation (402)

---

## 🛠️ Technology Stack

| Layer | Technologies |
| :--- | :--- |
| **Frontend** | React 18, Vite 6, Custom Modern CSS, Lucide Icons |
| **Backend** | Python 3.9+, FastAPI, Uvicorn, Pydantic 2, Python-Dotenv |
| **Artificial Intelligence** | Google Gemini API (`gemini-2.5-flash` via `google-genai` SDK) + Heuristic Fallback Engine |
| **Payment Gateway** | Razorpay Test Mode (`razorpay` Python SDK) + Simulated Mock Gateway |
| **Database / Storage** | Lightweight JSON Files (`products.json`, `orders.json`, `customers.json`) |

---

## 📁 Project Structure & File Explanations

```
AI-Growth-Agent/
│
├── backend/
│   ├── main.py              # FastAPI application entry, CORS config, and router registration
│   ├── products.py          # Catalog loader, search, recommendations & cross-selling endpoints
│   ├── ai_agent.py          # Gemini AI Assistant reasoning, intent parser & heuristic fallback
│   ├── cart.py              # Session cart state, GST calculation & in-cart cross-sell detection
│   ├── payment.py           # Razorpay Test Mode order creation, verification & order recording
│   ├── dashboard.py         # Merchant analytics, sales KPIs, top products & inventory alerts
│   └── growth.py            # AI Growth strategies & Abandoned Cart recovery message generator
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Chat.jsx            # Interactive AI Assistant chat with embedded product cards
│   │   │   ├── ProductCard.jsx     # Reusable product card with rating, tags, price & cross-sell
│   │   │   ├── CrossSellModal.jsx  # AI cross-selling modal (Shoes -> Socks) with bundle discount
│   │   │   ├── Cart.jsx            # Full shopping cart with quantity steppers & free delivery meter
│   │   │   ├── Checkout.jsx        # Test Mode checkout form, decline simulator & receipt view
│   │   │   └── Dashboard.jsx       # Merchant analytics, AI growth insights & cart recovery center
│   │   ├── App.jsx          # Root component managing navigation tabs, cart state & notifications
│   │   ├── main.jsx         # React 18 DOM mount point
│   │   └── index.css        # Clean, modern CSS styling and responsive layouts
│   ├── index.html           # HTML entry point
│   ├── vite.config.js       # Vite React server configuration (port 5173)
│   └── package.json         # React 18, Vite, and Lucide icon dependencies
│
├── data/
│   ├── products.json        # 10 realistic products in INR across 5 categories
│   ├── customers.json       # Customer profiles, purchase histories & abandoned carts
│   └── orders.json          # Completed test orders with line items & payment IDs
│
├── tests/
│   ├── test_products.py     # Tests for catalog retrieval, keyword search & price filters
│   ├── test_ai_agent.py     # Tests for AI Shopping Assistant query parsing & budget constraints
│   ├── test_recommendations.py # Tests for recommendation scoring & cross-sell pairings
│   ├── test_cart.py         # Tests for cart additions, quantity steppers, taxes & shipping
│   ├── test_payment.py      # Tests for test order creation, verification & failure simulation
│   ├── test_dashboard.py    # Tests for merchant analytics and sales KPIs
│   ├── test_growth.py       # Tests for AI growth insights and recovery copy generation
│   └── test_all_phases.py   # Master E2E test runner executing all phases & error scenarios
│
├── .env.example             # Template for API keys (Gemini, Razorpay)
├── .env                     # Local environment configuration file
├── requirements.txt         # Python dependencies
└── README.md                # Project documentation & run guide
```

---

## 🚀 Step-by-Step Installation & Run Guide

### 1. Prerequisites
- **Python 3.9+**
- **Node.js 18+ and npm**

---

### 2. Configure Environment Variables (Optional)

Copy `.env.example` to `.env` in the root directory:

```bash
# On Windows (PowerShell):
Copy-Item .env.example .env

# On macOS/Linux:
cp .env.example .env
```

Edit `.env` to configure your keys (optional — the application includes full heuristic and mock fallbacks so you can run it without any keys!):

```env
# Google Gemini API Key (from https://aistudio.google.com/)
GEMINI_API_KEY=your_gemini_key_here

# Razorpay Test Credentials (from https://dashboard.razorpay.com/)
RAZORPAY_KEY_ID=your_razorpay_key_id_here
RAZORPAY_KEY_SECRET=your_razorpay_key_secret_here

BACKEND_PORT=8000
```

---

### 3. Start the Backend (FastAPI)

Open a terminal in the root `AI-Growth-Agent` directory:

```bash
# 1. Install Python dependencies
pip install -r requirements.txt

# 2. Start the FastAPI development server
uvicorn backend.main:app --reload --port 8000
```

- **Backend API:** [http://127.0.0.1:8000](http://127.0.0.1:8000)
- **Interactive Swagger Documentation:** [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
- **System Health Check:** [http://127.0.0.1:8000/api/health](http://127.0.0.1:8000/api/health)

---

### 4. Start the Frontend (React + Vite)

Open a second terminal in the `frontend` folder:

```bash
cd frontend

# 1. Install npm packages
npm install

# 2. Start the Vite React dev server
npm run dev
```

- **Web Application:** [http://localhost:5173](http://localhost:5173)

---

## 🧪 Running Automated Tests

A comprehensive suite of automated tests verifies all 10 features:

```bash
# Run the Master E2E Test Suite (All Phases + Error Handling)
python tests/test_all_phases.py

# Or run individual phase test suites:
python tests/test_products.py         # Phase 2
python tests/test_ai_agent.py         # Phase 4
python tests/test_recommendations.py  # Phase 5
python tests/test_cart.py             # Phase 6
python tests/test_payment.py          # Phase 7
python tests/test_dashboard.py        # Phase 8
python tests/test_growth.py           # Phase 9



