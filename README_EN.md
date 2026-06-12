# RunYay MCP

> Connect your AI assistant to RunYay via MCP — read your running data, generate training plans, and push them straight to your watch.

**[中文](./README.md) · English**

---

### Download RunYay

Available on both iOS and Android. Scan the QR code below or search **"RunYay"** in the App Store / Google Play:

<img src="./imgs/download_qcode.jpg" width="480" alt="Download RunYay"/>

> Android users who cannot access the app store: add our support WeChat **yayarunya** or **yayarun02** to get the APK directly.

---

### Join the Community

Add WeChat **yayarunya** or **yayarun02** to connect with other runners and share tips on using AI + MCP for training.

---

### What is MCP?

MCP (Model Context Protocol) is an open standard by Anthropic that lets AI assistants securely connect to external data sources and tools.

Without MCP, you'd copy running data manually to the AI and paste AI-generated plans back into your app.  
With RunYay MCP, your AI can:

- **Directly read** your running records — pace, heart rate, cadence, stride, power, and more
- **Directly write** training plans into RunYay and sync them to your watch
- No manual data transfer needed on your end

---

### MCP Server URL

```
https://yayarun.cn/mcp
```

---

### Quick Start

#### Step 1: Enable a connection in RunYay

Open RunYay → **Settings** → **Connections & Authorization**, then choose one of the methods below.

#### Method 1: OAuth Web Authorization (Recommended)

Best for **Claude, ChatGPT**, and other AI tools that can open a browser for authorization.

1. Copy the MCP server URL: `https://yayarun.cn/mcp`
2. Paste it into your AI tool's MCP settings
3. Follow the prompts to complete web login — the connection is established automatically

#### Method 2: Manual API Key

Best for tools that **cannot open a browser** (e.g., local agents, CLI tools).

1. In RunYay, go to Connections & Authorization and tap **Generate Key**
2. Enter a name, choose permissions, and set an expiration period
3. Copy the generated key (**shown only once — save it immediately**)
4. Configure your AI tool with the server URL and key:

```json
{
  "mcpServers": {
    "runyay": {
      "url": "https://yayarun.cn/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_ACCESS_KEY"
      }
    }
  }
}
```

> Each account supports up to 5 manual API keys. Revoke any key at any time in the app.

📖 **[Full Configuration Guide →](https://z18f18tjyu.feishu.cn/wiki/WImVwzwvVi0S5lkqvAocP1t6ned)**

---

### Supported AI Tools

| AI Tool | Recommended Method |
|---------|-------------------|
| Claude Desktop / claude.ai | Method 1 (OAuth) |
| ChatGPT (MCP-enabled) | Method 1 (OAuth) |
| Cursor, Windsurf, etc. | Either method |
| Local agents / CLI tools | Method 2 (API Key) |
| Any MCP-compatible client | Depends on tool support |

---

### Available Tools

Once connected, your AI can call the following tools:

#### 📊 Running Data

**Get Latest Run Summary**  
Fetches your most recent run in full detail: distance, duration, pace, heart rate, cadence, stride length, power, VO2 max, vertical oscillation ratio, temperature, humidity, and more.

Notably, RunYay MCP supports **per-split data** — pace, heart rate, cadence, and more broken down by each kilometer (or mile). This lets your AI analyze pacing strategy, late-race fade, or effort distribution within a single run.

> The COROS official MCP does not currently support split-level data. RunYay MCP provides finer-grained analysis at this level.

> Example prompt: "Analyze the splits from my latest run — did I go out too fast and fade at the end?"

**Get Run History**  
Queries multiple runs within a date range (up to 90 days per request). Filter by activity type: outdoor / indoor / trail. Great for monthly mileage totals and long-term trend analysis.

> Example prompts: "What was my total mileage this month?" · "Compare my training load this month vs last month."

---

#### 🗓️ Training Plans

**Get Training Plans**  
Lists your existing plans, filterable by date range and completion status.

> Example prompt: "Which training sessions this week haven't I finished yet?"

**Push Training Plan**  
Generates structured training plans and writes them directly into RunYay. Supports warmup / main workout / cooldown blocks, interval runs, aerobic runs, and more. Up to 30 plans per push — enough to schedule a full week or month at once.

Once written to RunYay, plans can be synced to your watch with a single tap. **Garmin, COROS, and Apple Watch are currently supported, with more brands coming soon.**

> Example prompts:  
> "Based on my recent data, build a training plan for next week and push it to RunYay."  
> "I'm targeting a half marathon — create a 4-week training block and push it to my Garmin."

**Delete Training Plan**  
Removes a specific plan by ID.

> Example prompt: "Delete tomorrow's training session — I need to rest."

---

### Example Prompts

Copy and send any of these directly to your AI:

```
Analyze my running data from last month. What's improved and what needs work?
```

```
Estimate my VDOT from recent runs and create a training plan for next week. Push it to RunYay.
```

```
I'm racing a half marathon in 3 months. Build a systematic training plan and push it to RunYay week by week.
```

```
Look at my heart rate data across my last 10 runs and identify trends in my aerobic base.
```

---

### Managing Connections & Usage

In RunYay → **Settings → Connections & Authorization**, you can:

- View all connected AI tools
- Edit permission scopes per connection
- Check today's and this month's API call counts against your quota
- Revoke any connection instantly

---

### FAQ

**Q: Is my data safe? Will the AI store my running data?**  
A: RunYay MCP uses standard OAuth2 authorization. Data flows directly between the AI tool and RunYay's official servers — no third parties involved. Revoke access at any time in the app; the AI tool loses access immediately. Whether the AI tool retains conversation history depends on that product's own privacy policy.

**Q: Will plans sync to my watch after being pushed?**  
A: Plans are written to RunYay first, then synced to your watch from within the app. **Garmin, COROS, and Apple Watch are currently supported, with more brands on the way.**

**Q: What if I lose my API key?**  
A: Keys are shown only once at creation. If lost, revoke it in the app under Connections & Authorization and generate a new one.

**Q: Can I edit a plan that was already pushed?**  
A: Yes. Tell the AI what you'd like to change — it can look up the plan ID and overwrite it with the updated version.
