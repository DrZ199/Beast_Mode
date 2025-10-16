# BeastMode AI Chat Browser

## 🎯 **What It Is**

BeastMode is an **autonomous AI agent platform** that lets users create intelligent agents capable of breaking down complex goals into manageable tasks and executing them step-by-step. Think of it as your personal AI workforce that can research, analyze, plan, and execute multi-step projects automatically.

---

## 🌟 **Core Concept**

Instead of chatting back-and-forth with an AI, you give BeastMode a **high-level goal** (like "Research the 2025 EV market and find the top 5 startups"), and it:

1. **Decomposes** your goal into 5 logical subtasks
2. **Executes** each task sequentially using powerful AI models
3. **Shows** you real-time progress as it works
4. **Delivers** a comprehensive result you can export

It's like having an AI assistant that doesn't need constant supervision—you set it, and it runs.

---

## 🎨 **Visual Design & Branding**

### **Theme**
- **Color Palette**: Deep black backgrounds, electric blue accents, violet glowing elements
- **Aesthetic**: Cyberpunk-inspired, futuristic, minimal yet powerful
- **Logo**: Animated pulsing Zap (⚡) icon with neon violet glow
- **Modes**: Dark mode (default) and light mode toggle

### **Layout**
```
┌─────────────────────────────────────────────────────────┐
│  ⚡ BeastMode                            🌙  ⚙️         │
├──────────────┬──────────────────────────────────────────┤
│              │                                          │
│  [New Agent] │   Main Chat/Execution Area              │
│              │                                          │
│  Agent 1     │   Selected Agent:                        │
│  Agent 2     │   "Research EV market..."                │
│  Agent 3     │                                          │
│              │   Tasks:                                 │
│  (Sidebar)   │   ✓ Task 1 - Completed                   │
│              │   ⟳ Task 2 - Running...                  │
│              │   ⏸ Task 3 - Pending                     │
│              │   ⏸ Task 4 - Pending                     │
│              │                                          │
└──────────────┴──────────────────────────────────────────┘
```

---

## 🧩 **Key Features Breakdown**

### **1. Agent Creation**
- Click **"New Agent"** button (prominent, gradient violet-to-blue)
- Modal appears asking for:
  - **Goal**: Multi-line text input (e.g., "Write a business plan for a coffee shop")
  - **Model**: Dropdown selector showing available AI models
- System automatically decomposes goal into 5 subtasks
- Agent appears in sidebar, ready to run

### **2. Agent Execution**
- Click **"Run"** button next to selected agent
- Each task executes sequentially:
  - Status changes: `pending` → `running` (animated pulse) → `completed` (green)
  - AI model processes each task (simulated 2-4 second execution)
  - Results appear below each task in a result box
- **Stop/Continue** buttons let you pause and resume anytime

### **3. Task Management**
- **Edit Tasks**: Click edit icon on pending tasks to modify their description
- **Real-time Updates**: See progress as tasks complete
- **Status Indicators**: Color-coded badges (green = done, blue = running, gray = pending, red = failed)

### **4. Sidebar**
Lists all created agents with:
- Goal title (truncated if long)
- Progress counter (e.g., "3/5 tasks")
- Status badge (idle, running, paused, completed, failed)
- Delete button (trash icon)
- Click any agent to view its details

### **5. Settings Panel**
Accessible via gear icon (⚙️) in top-right:
- **OpenRouter API Key**: Password input field (stored locally)
- **Default Model**: Dropdown with 5 models:
  - GPT-4 Turbo
  - Claude 3 Haiku
  - Mistral Medium
  - Gemini Pro (Free)
  - Llama 3 8B (Free)
- Link to OpenRouter website for key registration

### **6. Export Functionality**
- **Download** button exports agent results as Markdown
- Includes:
  - Goal description
  - Model used
  - Timestamp
  - All tasks with statuses and results
- File named: `beastmode-[agent-id].md`

---

## 🔄 **User Flow Example**

### **Scenario**: Research competing products

1. **User logs in** (sees empty state with animated Zap logo)
2. **Clicks "New Agent"**
3. **Enters goal**: "Find and analyze 5 competitors in the project management software space"
4. **Selects model**: "Claude 3 Haiku"
5. **Clicks "Create Agent"**
6. **BeastMode generates tasks**:
   - Task 1: Research project management software landscape
   - Task 2: Identify top 5 competitors
   - Task 3: Analyze each competitor's features
   - Task 4: Compare pricing and market position
   - Task 5: Generate comprehensive summary report
7. **User clicks "Run"**
8. **Task 1 starts** (status: running, blue pulsing badge)
9. **Task 1 completes** (result appears: "Researched PM software. Found 47 active companies...")
10. **Task 2 starts** automatically
11. **User can**:
    - Stop execution to review results
    - Edit remaining tasks
    - Continue execution later
12. **All tasks complete**
13. **User clicks "Export"** → downloads full report

---

## 🧠 **Agent Intelligence**

### **Goal Decomposition**
When you enter a goal, BeastMode automatically:
- Analyzes the complexity
- Breaks it into logical steps
- Creates a task pipeline
- Assigns subtasks in execution order

### **Task Execution**
Each task:
- Receives context from previous task results
- Uses selected AI model (via OpenRouter API)
- Generates detailed output
- Passes context to next task

### **Memory & Context**
- All agents stored in browser localStorage
- Full conversation history maintained
- Tasks reference previous results for continuity

---

## 🎛️ **Technical Architecture**

### **Frontend**
- **React** with TypeScript
- **Tailwind CSS** for styling
- **Lucide Icons** for UI elements
- **LocalStorage** for persistence (production uses Supabase)

### **State Management**
- React hooks (useState, useEffect)
- Real-time updates on task completion
- Persistent settings across sessions

### **Data Structure**
```typescript
Agent {
  id: string
  goal: string
  model: string
  tasks: Task[]
  status: 'idle' | 'running' | 'paused' | 'completed' | 'failed'
  createdAt: Date
}

Task {
  id: string
  title: string
  status: 'pending' | 'running' | 'completed' | 'failed'
  result?: string
}
```

---

## 🚀 **Production Features (To Be Implemented)**

### **Backend (Next.js 14)**
- **API Routes**:
  - `/api/run-agent` - Execute tasks with OpenRouter
  - `/api/models` - Fetch available models
  - `/api/user-settings` - Manage user preferences
  - `/api/get-logs` - Retrieve execution history

### **Supabase Integration**
- **Authentication**: User login/signup
- **Database**: Store agents, tasks, results
- **Real-time**: Live updates across devices
- **Storage**: File uploads for research materials

### **OpenRouter API**
- Actual AI model execution
- Streaming responses
- Rate limiting
- Error handling

### **Advanced Features**
- **Multi-agent view**: Compare outputs from multiple models side-by-side
- **Prompt templates**: Save and reuse common goals
- **Web search**: Integrate DuckDuckGo/Tavily for real-time data
- **Collaboration**: Share agents with team members

---

## 💡 **Use Cases**

1. **Market Research**: "Analyze the fintech landscape in Southeast Asia"
2. **Content Creation**: "Write a 5-article blog series on AI ethics"
3. **Business Planning**: "Create a go-to-market strategy for a B2B SaaS product"
4. **Competitive Analysis**: "Compare top 10 CRM platforms and recommend one"
5. **Learning**: "Explain quantum computing with examples and exercises"
6. **Data Analysis**: "Process this CSV and find key insights"

---

## 🎯 **What Makes BeastMode Different**

Unlike traditional chatbots:
- **Autonomous**: Set it and let it run
- **Structured**: Clear task breakdown and execution flow
- **Transparent**: See every step of the reasoning process
- **Editable**: Modify tasks on the fly
- **Exportable**: Take results with you
- **Multi-model**: Use different AI brains for different tasks

It's not a conversation—it's **delegated AI work**.

---

## 🔐 **Privacy & Security**

- API keys stored locally (encrypted in production)
- No data sent to external servers except OpenRouter
- User controls all data
- Export and delete anytime

---

This is BeastMode: **Your autonomous AI workforce in a browser.** 🚀⚡
