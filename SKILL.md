---
name: options-trading-tutor
description: Interactive tutoring system for options trading. Teaches fundamentals, concepts, technical analysis, Greeks, strategies, and risk management. Use this skill whenever a user wants to learn options trading, take a lecture, review progress, or continue an existing course. The skill reads the GitHub repo (kamal-manick/learn-options-trading) to track progress and automatically generates the next lecture. Use at the start of each learning session to continue from where the student left off.
compatibility: Requires git CLI and ability to read/write files
---

# Options Trading Tutor Skill

## Overview

This skill enables interactive, self-paced tutoring in options trading. It manages a structured learning pathway from fundamentals to expert-level concepts, tracks progress via GitHub, and delivers daily lectures with interactive quizzes.

**Key features:**
- **Progress tracking**: GitHub-based system tracks completed lectures and modules
- **Structured curriculum**: 12-week course covering foundations → strategies → mastery
- **Interactive content**: HTML lectures with embedded quizzes (collapsible Q&A sections)
- **Web viewer**: Single-page app displays course content and progress dashboard
- **Automated delivery**: Generates next lecture based on repo state; user uploads to GitHub

## Workflow at Each Session

1. **Clone and assess**: Read the GitHub repo to determine current progress
2. **Load context**: Identify the next uncompleted lecture
3. **Deliver lecture**: Generate lecture content (HTML) with 2-5 Q&A check-your-knowledge items
4. **Update tracker**: Modify progress file with newly completed lecture
5. **Present outputs**: Show lecture file and updated progress tracker for manual GitHub upload (or automated push if credentials available)

## How to Use This Skill

### First Session
- User says: "Start teaching me options trading" or "Begin the options trading course"
- Skill clones the repo, finds it empty, and initializes:
  - `outline.md` — Full course structure
  - `progress.json` — Learning state tracker
  - `content/module-1/lecture-1.html` — First lecture
  - `index.html` — Web app for viewing course

### Subsequent Sessions
- User says: "Continue my options trading course" or "Next lecture please"
- Skill clones repo, reads progress, generates the next uncompleted lecture
- User manually commits files to GitHub (or automation via personal access token if available)

### Mid-Course Adjustments
- User can request: "Explain volatility again" → tutor re-explains that concept
- User can ask: "What's my progress?" → displays progress dashboard
- User can request: "Summarize what I've learned" → generates review

## Content Structure

```
learn-options-trading/
├── outline.md                 # Course structure (modules, lectures, topics)
├── progress.json              # Learning state (completed lectures, timestamps)
├── content/
│   ├── module-1-foundations/
│   │   ├── lecture-1.html
│   │   ├── lecture-2.html
│   │   └── lecture-3.html
│   ├── module-2-concepts/
│   │   └── lecture-4.html
│   └── ...
└── index.html                 # Web app (single-page course viewer)
```

## Lecture Format (HTML)

Each lecture includes:
- **Title & learning objectives** (2-3 key goals)
- **Main content** (text, embedded diagrams, video embeds if applicable)
- **Interactive Q&A section** with collapsible answers:
  ```html
  <details>
    <summary>Q: What is an option?</summary>
    <p>A: An option is a contract giving the buyer...</p>
  </details>
  ```
- **Knowledge check** (2-5 questions, answers hidden until clicked)
- **Preview of next lecture** (1-2 sentences)

## Web App Features

The `index.html` single-page app provides:
- **Lecture viewer**: Display current lecture with formatted content
- **Progress dashboard**: Show completed modules, total progress %
- **Lecture navigator**: Sidebar or dropdown to jump between lectures
- **Dark mode toggle**: For comfortable learning
- **Search**: Basic search within lecture titles/topics

## Progress Tracking Format

`progress.json`:
```json
{
  "current_module": 1,
  "current_lecture": 1,
  "total_modules": 12,
  "completed_lectures": [
    {"module": 1, "lecture": 1, "title": "What is an Option?", "completed_at": "2024-01-15T10:30:00Z"}
  ],
  "overall_progress_percent": 8,
  "time_invested_minutes": 45
}
```

## Course Outline Reference

The skill generates a comprehensive outline covering:

**Module 1: Foundations (Lectures 1-3)**
- What are options? Calls, puts, intrinsic/time value
- How options work: strike price, expiry, settlement
- Risk & reward payoff diagrams

**Module 2: Key Concepts (Lectures 4-6)**
- Moneyness, implied volatility, historical volatility
- Time decay and its mechanics
- Bid-ask spread, open interest, volume

**Module 3: The Greeks (Lectures 7-10)**
- Delta: directional sensitivity
- Gamma: delta's rate of change
- Theta: time decay impact
- Vega: volatility sensitivity
- Rho: interest rate impact

**Module 4: Technical Analysis for Options (Lectures 11-13)**
- Support/resistance, trends, chart patterns
- Volume analysis, moving averages
- Applying TA to options entry/exit

**Module 5: Basic Strategies (Lectures 14-17)**
- Long calls/puts: directional bets
- Spreads: bull call, bear call, straddles, strangles
- Writing covered calls, cash-secured puts
- Collar strategy, synthetic positions

**Module 6: Risk Management (Lectures 18-20)**
- Position sizing, Kelly criterion
- Stop losses, profit targets
- Portfolio Greeks, correlation risk
- Handling gap risks, assignment risk

**Module 7: Advanced Strategies (Lectures 21-24)**
- Iron condors, butterflies, calendars
- Diagonal spreads, ratio spreads
- Event-driven strategies (earnings, dividends)
- Volatility mean reversion strategies

**Module 8: Mastery & Professional Practices (Lectures 25-30)**
- Building an edge, backtesting frameworks
- Psychology and discipline
- Tax-efficient execution (India-specific)
- Reading Greeks in market conditions
- Managing tail risk
- Live trading checklist and war stories

## Tutor Instructions

When generating a lecture:

1. **Assess skill level**: Start simple in early modules, increase complexity in later ones
2. **Use examples**: Every concept needs a concrete example (with realistic numbers)
3. **Visual thinking**: Describe diagrams (payoff charts, Greeks curves) even in text; user can sketch or AI generates SVG
4. **Video references**: If a topic is better explained via video (e.g., Greeks behavior), embed YouTube links
5. **Real India context**: Use NSE index options, Nifty, Bank Nifty examples; mention SEBI rules where relevant
6. **Interactive Q&A**: Make questions test understanding, not just recall
7. **Scaffold learning**: Build on prior lectures; reference earlier concepts
8. **Anticipate confusion**: Address common misconceptions explicitly

## Initialization on First Run

On the first session, the skill auto-generates:
- Full course outline
- Empty progress.json (all lectures marked incomplete)
- Lecture 1 HTML file
- Web app HTML

User then commits all files to the GitHub repo. On subsequent sessions, skill reads current progress and generates the next lecture.

## GitHub Upload Workflow

Since the skill may not have push credentials:
1. Skill generates/updates lecture files locally
2. Displays the files in the conversation
3. User downloads and manually git add/commit/push to their repo
4. Alternatively: User provides a GitHub personal access token (PAT) for automated pushes

## Notes

- Each lecture session takes ~30-45 minutes of learning time
- Weekly review sessions recommended (built into later modules)
- Course is self-paced; can stretch over weeks or months
- After Module 6 (Risk Management), student should begin paper trading to reinforce concepts
- Module 8 assumes student has paper-traded for 4+ weeks
