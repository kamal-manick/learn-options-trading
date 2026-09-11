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

1. **Clone and assess**: Read the GitHub repo to determine current progress (using outline.md and progress.json)
2. **Load context**: Identify the next uncompleted lecture from the course outline
3. **Deliver lecture**: Generate lecture HTML based on `lecture-template.html` structure
   - Fill all required sections: header, objectives, content, quiz, preview, navigation
   - NO inline styles; use semantic HTML only
   - Follow the template structure from the cloned repo
4. **Update tracker**: Modify progress.json with newly completed lecture metadata
5. **Present outputs**: Display the lecture file and updated progress tracker for manual GitHub upload (or automated push if credentials available)

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

Each lecture is generated using the `lecture-template.html` structure with NO inline styles. The template includes:

**Required sections:**
1. **Lecture header** — title and metadata (Module & duration)
2. **Learning objectives** — 2-3 key learning goals
3. **Content sections** — main lecture material organized in H2/H3 headings
   - Content paragraphs with concrete examples
   - Key term definitions (wrapped in `<div class="key-term">`)
   - Example boxes (wrapped in `<div class="example-box">`)
   - Tables with class `table-responsive` where applicable
4. **Quiz section** — 5 collapsible Q&A pairs using `<details>` tags
5. **Next lecture preview** — 1-2 sentence teaser
6. **Navigation buttons** — Previous/Next buttons (disabled/enabled as appropriate)

**Structure template:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lecture Title - Options Trading</title>
</head>
<body>
    <div class="lecture-container">
        <!-- Header, objectives, content, quiz, preview, navigation -->
    </div>
</body>
</html>
```

**Important:** NO CSS, NO inline style attributes. All styling is handled externally via the index.html viewer.

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

When generating a lecture using `lecture-template.html`:

1. **Follow template structure exactly**: Use the sections from lecture-template.html as the blueprint
2. **No styling**: Omit all CSS and inline `style` attributes; content-only HTML
3. **Assess skill level**: Start simple in early modules, increase complexity in later ones
4. **Use concrete examples**: Every concept needs a realistic example with NSE/Nifty numbers
5. **Key terms & example boxes**: Use `<div class="key-term">` and `<div class="example-box">` divs (no styles inside)
6. **Tables for data**: Use `<div class="table-responsive"><table>` for comparative data (no inline styles)
7. **Interactive quiz**: Generate 5 collapsible `<details>` Q&A pairs testing conceptual understanding
8. **Video references**: Embed YouTube links in content when appropriate (e.g., Greeks behavior)
9. **Real India context**: Reference NSE, Nifty, Bank Nifty; mention SEBI rules where relevant
10. **Scaffold learning**: Build on prior lectures; reference earlier concepts
11. **Anticipate confusion**: Address common misconceptions in the Q&A section

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

## Lecture Generation Template

When generating each lecture, use this exact structure from `lecture-template.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>[Lecture Title] - Options Trading</title>
</head>
<body>
    <div class="lecture-container">
        <!-- Header: title + module + duration -->
        <div class="lecture-header">
            <h1>[Lecture Title]</h1>
            <p>Module [X]: [Module Name] | Duration: ~35 minutes</p>
        </div>

        <!-- Learning Objectives: 2-3 key outcomes -->
        <div class="learning-objectives">
            <h3>📚 Learning Objectives</h3>
            <ul>
                <li>[Objective 1]</li>
                <li>[Objective 2]</li>
                <li>[Objective 3]</li>
            </ul>
        </div>

        <!-- Main Content: organized sections with H2/H3, paragraphs, key terms, examples -->
        <div class="content-section">
            <h2>[Section Heading]</h2>
            <p>[Paragraph content]</p>
            <h3>[Subsection]</h3>
            <p>[Detailed content]</p>
            <div class="key-term">
                <strong>Key Term:</strong> [Definition]
            </div>
            <div class="example-box">
                <strong>Example:</strong> [Real-world Nifty/NSE example with numbers]
            </div>
        </div>

        <!-- Tables (if needed) -->
        <div class="table-responsive">
            <table>
                <tr><th>[Column 1]</th><th>[Column 2]</th></tr>
                <tr><td>[Data]</td><td>[Data]</td></tr>
            </table>
        </div>

        <!-- Quiz: 5 collapsible Q&A pairs -->
        <div class="quiz-section">
            <h3>✅ Check Your Knowledge</h3>
            <p>Click on each question to reveal the answer.</p>
            <details>
                <summary>Q1: [Question text]?</summary>
                <p>A: [Answer text]</p>
            </details>
            <!-- Q2-Q5 following same pattern -->
        </div>

        <!-- Next lecture teaser -->
        <div class="next-lecture">
            <strong>📌 Next Lecture Preview:</strong> [1-2 sentence preview]
        </div>

        <!-- Navigation buttons -->
        <div class="lecture-nav">
            <button class="btn btn-disabled" disabled>← Previous</button>
            <button class="btn btn-next">Next Lecture →</button>
        </div>
    </div>
</body>
</html>
```

**Key rules for this template:**
- NO `style=""` attributes
- NO `<style>` tags
- Use only semantic HTML + class names for styling (handled by external CSS)
- All content goes inside `<div class="lecture-container">`
- Tables always wrap in `<div class="table-responsive">`
- Key concepts go in `<div class="key-term">`
- Real examples go in `<div class="example-box">`
- Quiz questions use `<details>` tags (no hiding via JavaScript)
- Duration: always ~35 minutes estimate
- Include NSE/Nifty examples where relevant

## Notes

- Each lecture session takes ~30-45 minutes of learning time
- Weekly review sessions recommended (built into later modules)
- Course is self-paced; can stretch over weeks or months
- After Module 6 (Risk Management), student should begin paper trading to reinforce concepts
- Module 8 assumes student has paper-traded for 4+ weeks
- **Template-based generation ensures consistency**: All lectures follow the same structural pattern from `lecture-template.html`
