# 📈 AI Stock Analysis System

[![GitHub stars](https://img.shields.io/github/stars/ZhuLinsen/daily_stock_analysis?style=social)](https://github.com/ZhuLinsen/daily_stock_analysis/stargazers)
[![CI](https://github.com/ZhuLinsen/daily_stock_analysis/actions/workflows/ci.yml/badge.svg)](https://github.com/ZhuLinsen/daily_stock_analysis/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-Ready-2088FF?logo=github-actions&logoColor=white)](https://github.com/features/actions)

> 🤖 AI-powered stock analysis system for A-shares, Hong Kong stocks, and US stocks. Automatically analyzes your watchlist daily and sends "Decision Dashboard" to WeChat Work/Feishu/Telegram/Email

English | [简体中文](../README.md)

![Demo](./sources/all_2026-01-13_221547.gif)

## ✨ Key Features

### 🎯 Core Capabilities
- **AI Decision Dashboard** - One-sentence core conclusion + precise entry/exit points + checklist
- **Multi-dimensional Analysis** - Technical analysis + chip distribution + sentiment intelligence + real-time quotes
- **Market Review** - Daily market overview, sector performance, northbound capital flow
- **Multi-channel Push** - Support WeChat Work, Feishu, Telegram, Email (auto-detection)
- **Zero-cost Deployment** - Free to run on GitHub Actions, no server required
- **💰 Free AI Models** - NVIDIA NIM free models + Google Gemini free quota, no cost for personal use
- **🔄 Multi-model Support** - Priority: NVIDIA NIM > Gemini > OpenAI-compatible API

### 📊 Data Sources
- **Market Data**: AkShare (free), Tushare, Baostock, YFinance
- **News Search**: Tavily, SerpAPI, Bocha
- **AI Analysis**:
  - Primary: NVIDIA NIM free models (Llama 3.1 8B, etc.) — [Get it free](https://build.nvidia.com)
  - Secondary: Google Gemini (gemini-3-flash-preview) — [Get it free](https://aistudio.google.com/)
  - Backup: OpenAI-compatible API (DeepSeek, Qwen, Moonshot, etc.)

### 🌍 Supported Markets
- **A-shares** - Shanghai & Shenzhen Stock Exchanges
- **Hong Kong Stocks** - HKEX
- **US Stocks** - NYSE, NASDAQ

### 🛡️ Built-in Trading Philosophy
- ❌ **No Chasing Highs** - Auto mark "Danger" when price deviation > 5%
- ✅ **Trend Trading** - Only trade in bull alignment (MA5 > MA10 > MA20)
- 📍 **Precise Levels** - Entry price, stop loss, target price
- 📋 **Checklist** - Every condition marked with ✅⚠️❌

## 🚀 Quick Start

### Option 1: GitHub Actions (Recommended, Zero Cost)

**No server needed, runs automatically every day!**

#### 1. Fork this repository (⭐ Star it too!)

Click the `Fork` button in the upper right corner

#### 2. Configure Secrets

Go to your forked repo → `Settings` → `Secrets and variables` → `Actions` → `New repository secret`

**AI Model Configuration (Choose one, priority: NIM > Gemini > OpenAI)**

| Secret Name | Description | Required |
|------------|------|:----:|
| `NIM_API_KEY` | Get free API key from [NVIDIA NIM](https://build.nvidia.com) (recommended) | ✅* |
| `NIM_MODEL` | Model name (default: `meta/llama-3.1-8b-instruct`) | Optional |
| `GEMINI_API_KEY` | Get free API key from [Google AI Studio](https://aistudio.google.com/) | ✅* |
| `OPENAI_API_KEY` | OpenAI-compatible API Key (supports DeepSeek, Qwen, etc.) | Optional |
| `OPENAI_BASE_URL` | OpenAI-compatible API endpoint (e.g., `https://api.deepseek.com/v1`) | Optional |
| `OPENAI_MODEL` | Model name (e.g., `deepseek-chat`) | Optional |

> *Note: Configure at least one of `NIM_API_KEY`, `GEMINI_API_KEY` or `OPENAI_API_KEY`

**Notification Channel Configuration (Can configure multiple, all will receive notifications)**

| Secret Name | Description | Required |
|------------|------|:----:|
| `WECHAT_WEBHOOK_URL` | WeChat Work Webhook URL | Optional |
| `FEISHU_WEBHOOK_URL` | Feishu Webhook URL | Optional |
| `TELEGRAM_BOT_TOKEN` | Telegram Bot Token (Get from @BotFather) | Optional |
| `TELEGRAM_CHAT_ID` | Telegram Chat ID | Optional |
| `EMAIL_SENDER` | Sender email (e.g., `xxx@qq.com`) | Optional |
| `EMAIL_PASSWORD` | Email authorization code (not login password) | Optional |
| `EMAIL_RECEIVERS` | Receiver emails (comma-separated, leave empty to send to yourself) | Optional |
| `PUSHPLUS_TOKEN` | PushPlus Token ([Get it here](https://www.pushplus.plus), Chinese push service) | Optional |
| `CUSTOM_WEBHOOK_URLS` | Custom Webhook URLs (supports DingTalk, etc., comma-separated) | Optional |

> *Note: Configure at least one channel, multiple channels will all receive notifications

**Stock List Configuration**

| Secret Name | Description | Required |
|------------|------|:----:|
| `STOCK_LIST` | Watchlist codes, e.g., `600519,AAPL,hk00700` | ✅ |
| `TAVILY_API_KEYS` | [Tavily](https://tavily.com/) Search API (for news) | Recommended |
| `SERPAPI_API_KEYS` | [SerpAPI](https://serpapi.com/) Backup search | Optional |
| `TUSHARE_TOKEN` | [Tushare Pro](https://tushare.pro/) Token | Optional |

**Stock Code Format**

| Market | Format | Examples |
|--------|--------|----------|
| A-shares | 6-digit number | `600519`, `000001`, `300750` |
| HK Stocks | hk + 5-digit number | `hk00700`, `hk09988` |
| US Stocks | 1-5 uppercase letters | `AAPL`, `TSLA`, `GOOGL` |

#### 3. Enable Actions

Go to `Actions` tab → Click `I understand my workflows, go ahead and enable them`

#### 4. Manual Test

`Actions` → `Daily Stock Analysis` → `Run workflow` → Select mode → `Run workflow`

#### 5. Done!

The system will:
- Run automatically at scheduled time (default: 18:00 Beijing Time)
- Send analysis reports to all configured channels
- Save reports locally

---

### Option 2: Local Deployment

#### 1. Clone Repository

```bash
git clone https://github.com/ZhuLinsen/daily_stock_analysis.git
cd daily_stock_analysis
```

#### 2. Install Dependencies

```bash
# Create virtual environment (recommended)
python3 -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

#### 3. Configure Environment Variables

```bash
# Copy configuration template
cp .env.example .env

# Edit .env file
nano .env  # or use any editor
```

Configure the following:

```bash
# AI Model (Choose one)
NIM_API_KEY=your_nim_api_key_here
# GEMINI_API_KEY=your_gemini_api_key_here

# Stock Watchlist (Mixed markets supported)
STOCK_LIST=600519,AAPL,hk00700

# Notification Channel (Choose at least one)
TELEGRAM_BOT_TOKEN=your_bot_token
TELEGRAM_CHAT_ID=your_chat_id

# News Search (Optional)
TAVILY_API_KEYS=your_tavily_key
```

#### 4. Run

```bash
# One-time analysis
python main.py

# Scheduled mode (runs daily at 18:00)
python main.py --schedule

# Analyze specific stocks
python main.py --stocks AAPL,TSLA,GOOGL

# Market review only
python main.py --market-review
```

---

## 📱 Supported Notification Channels

### 1️⃣ Telegram (Recommended for international users)

1. Talk to [@BotFather](https://t.me/BotFather) → `/newbot` → Get Bot Token
2. Get Chat ID: Send message to [@userinfobot](https://t.me/userinfobot)
3. Configure:
   ```bash
   TELEGRAM_BOT_TOKEN=123456789:ABCdefGHIjklMNOpqrsTUVwxyz
   TELEGRAM_CHAT_ID=123456789
   ```

### 2️⃣ Email (Universal)

1. Get authorization code (e.g., Gmail App Password)
2. Configure:
   ```bash
   EMAIL_SENDER=your_email@gmail.com
   EMAIL_PASSWORD=your_app_password
   EMAIL_RECEIVERS=receiver@example.com  # Optional
   ```

### 3️⃣ WeChat Work / Feishu (For Chinese users)

WeChat Work:
```bash
WECHAT_WEBHOOK_URL=https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=xxx
```

Feishu:
```bash
FEISHU_WEBHOOK_URL=https://open.feishu.cn/open-apis/bot/v2/hook/xxx
```

### 4️⃣ PushPlus (Chinese mobile push)

```bash
PUSHPLUS_TOKEN=your_token_here
```

---

## 🎨 Sample Output

### Decision Dashboard Format

```markdown
# 🎯 2026-01-24 Decision Dashboard

> Total **3** stocks analyzed | 🟢Buy:1 🟡Hold:1 🔴Sell:1

## 📊 Analysis Summary

🟢 **AAPL(Apple Inc.)**: Buy | Score 85 | Strong Bullish
🟡 **600519(Kweichow Moutai)**: Hold | Score 65 | Bullish
🔴 **TSLA(Tesla)**: Sell | Score 35 | Bearish

---

## 🟢 AAPL (Apple Inc.)

### 📰 Key Information
**💭 Sentiment**: Positive news on iPhone 16 sales
**📊 Earnings**: Q1 2024 earnings beat expectations

### 📌 Core Conclusion

**🟢 Buy** | Strong Bullish

> **One-sentence Decision**: Strong technical setup with positive catalyst, ideal entry point

⏰ **Time Sensitivity**: Within this week

| Position | Action |
|----------|--------|
| 🆕 **No Position** | Buy at pullback |
| 💼 **With Position** | Continue holding |

### 📊 Data Perspective

**MA Alignment**: MA5>MA10>MA20 | Bull Trend: ✅ Yes | Trend Strength: 85/100

| Price Metrics | Value |
|--------------|-------|
| Current | $185.50 |
| MA5 | $183.20 |
| MA10 | $180.50 |
| MA20 | $177.80 |
| Bias (MA5) | +1.26% ✅ Safe |
| Support | $183.20 |
| Resistance | $190.00 |

**Volume**: Ratio 1.8 (Moderate increase) | Turnover 2.3%
💡 *Volume confirms bullish momentum*

### 🎯 Action Plan

**📍 Sniper Points**

| Level Type | Price |
|-----------|-------|
| 🎯 Ideal Entry | $183-184 |
| 🔵 Secondary Entry | $180-181 |
| 🛑 Stop Loss | $177 |
| 🎊 Target | $195 |

**💰 Position Sizing**: 20-30% of portfolio
- Entry Plan: Enter in 2-3 batches
- Risk Control: Strict stop loss at $177

**✅ Checklist**

- ✅ Bull trend confirmed
- ✅ Price near MA5 support
- ✅ Volume confirms trend
- ⚠️ Monitor market volatility

---
```

---

## 🔧 Advanced Configuration

### Environment Variables

```bash
# === Analysis Behavior ===
ANALYSIS_DELAY=10              # Delay between analysis (seconds) to avoid API rate limit
REPORT_TYPE=full               # Report type: simple/full
SINGLE_STOCK_NOTIFY=true       # Push immediately after each stock analysis

# === Schedule ===
SCHEDULE_ENABLED=true          # Enable scheduled task
SCHEDULE_TIME=18:00            # Daily run time (HH:MM, 24-hour format)
MARKET_REVIEW_ENABLED=true     # Enable market review

# === Data Source ===
TUSHARE_TOKEN=your_token       # Tushare Pro (priority data source if configured)

# === System ===
MAX_WORKERS=3                  # Concurrent threads (3 recommended to avoid blocking)
DEBUG=false                    # Enable debug logging
```

---

## 📖 Documentation

- [Complete Configuration Guide](full-guide.md)
- [Bot Command Reference](bot-command.md)
- [Feishu Bot Setup](bot/feishu-bot-config.md)
- [DingTalk Bot Setup](bot/dingding-bot-config.md)

---

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork this repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## ⚠️ Disclaimer

This tool is for **informational and educational purposes only**. The analysis results are generated by AI and should not be considered as investment advice. Stock market investments carry risk, and you should:

- Do your own research before making investment decisions
- Understand that past performance does not guarantee future results
- Only invest money you can afford to lose
- Consult with a licensed financial advisor for personalized advice

The developers of this tool are not liable for any financial losses resulting from the use of this software.

---

## 🙏 Acknowledgments

- [AkShare](https://github.com/akfamily/akshare) - Stock data source
- [NVIDIA NIM](https://build.nvidia.com) - Free AI models (Llama 3.1, Mistral, etc.)
- [Google Gemini](https://ai.google.dev/) - AI analysis engine
- [Tavily](https://tavily.com/) - News search API
- All contributors who helped improve this project

---

## 📞 Contact

- GitHub Issues: [Report bugs or request features](https://github.com/ZhuLinsen/daily_stock_analysis/issues)
- Discussions: [Join discussions](https://github.com/ZhuLinsen/daily_stock_analysis/discussions)

---

**Made with ❤️ by AI enthusiasts | Star ⭐ this repo if you find it useful!**
