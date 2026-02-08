# Mastering Copilot CLI Modes: A Solo Developer's Guide

As a solo developer, understanding and leveraging the different modes in GitHub Copilot CLI can dramatically boost your productivity. This guide breaks down each mode, when to use it, and how to get the most value from it when you're working alone.

## The Three Core Modes

Copilot CLI has three primary modes that you can cycle through using **Shift+Tab**:

### 1. **Chat Mode** (Default)
**What it is:** Interactive conversation mode where Copilot responds to your prompts but waits for approval before taking action.

**When to use it:**
- Quick questions about your codebase
- Exploratory tasks where you're not sure of the approach
- Learning how something works
- When you want tight control over every action

**Solo developer advantages:**
- Low risk - you approve every step
- Great for learning as you see each action explained
- Perfect for unfamiliar codebases or technologies

**Example workflow:**
```
You: "Explain how authentication works in this app"
Copilot: [Explains the auth flow]
You: "Now add rate limiting to the login endpoint"
Copilot: [Asks permission to edit files, run tests]
```

**Pro tips:**
- Use `@filename` to bring specific files into context
- Ask for explanations before making changes
- Use `/diff` to review proposed changes before accepting

---

### 2. **Plan Mode** (Shift+Tab once)
**What it is:** Copilot creates a detailed plan before executing any changes. You review the plan, then Copilot executes it step-by-step.

**When to use it:**
- Multi-file changes or refactoring
- Feature implementation with multiple components
- When you want to understand the full scope before committing
- Tasks that might have cascading effects

**Solo developer advantages:**
- See the big picture before any code is touched
- Catch potential issues in the planning phase
- Better understanding of architectural decisions
- You can modify the plan before execution

**Example workflow:**
```
You: "Add a new user profile feature with avatar uploads"
Copilot: [Creates plan]
  1. Create ProfileController with upload method
  2. Add file validation middleware
  3. Update User model with avatar field
  4. Create migration for avatar column
  5. Add profile routes
  6. Write tests for upload functionality
You: [Review plan, approve or modify]
Copilot: [Executes each step with your approval]
```

**Pro tips:**
- Always review the plan before approving execution
- You can ask Copilot to modify the plan before starting
- Use plan mode for anything touching more than 2-3 files
- Great for learning project architecture patterns

---

### 3. **Autopilot Mode** (Shift+Tab twice, requires experimental mode)
**What it is:** Copilot works autonomously toward completing the task with minimal interruptions. It makes decisions and continues until the goal is achieved or it encounters an issue.

**When to use it:**
- Well-defined, repetitive tasks
- Boilerplate generation
- Test writing for existing code
- Tasks where the approach is straightforward

**Solo developer advantages:**
- Massive time savings on routine work
- Focus on high-level design while Copilot handles implementation
- Great for catching up on technical debt
- Lets you work on multiple things simultaneously

**Example workflow:**
```
You: "Write comprehensive unit tests for all functions in src/utils/"
Copilot: [Analyzes files, writes tests, runs them, fixes failures, continues until complete]
You: [Review final result]
```

**⚠️ Important considerations:**
- Only use for tasks where you can easily review the output
- Best for isolated changes (tests, docs, refactoring)
- Always review the complete changes afterward
- Not recommended for critical security or business logic

**Pro tips:**
- Enable experimental mode: `copilot --experimental` or `/experimental`
- Give clear, specific goals with success criteria
- Use for tasks you could do yourself but would take time
- Set up good test coverage so autopilot can validate its work

---

## Experimental Mode Features

Enable with `copilot --experimental` or `/experimental` inside a session.

**Additional capabilities:**
- **Autopilot mode** (as described above)
- **Proactive suggestions** - Copilot may suggest next steps
- **Enhanced tool usage** - More aggressive use of available tools
- **Smarter context management** - Better at maintaining long sessions

**Solo developer use cases:**
- Rapid prototyping when exploring new ideas
- Batch processing multiple similar tasks
- Weekend hackathons or time-boxed experiments
- Learning by doing - see multiple approaches quickly

---

## How to Switch Between Modes

### During a session:
- **Shift+Tab** - Cycle through Chat → Plan → Autopilot (experimental only)
- **Shift+Tab** (again) - Continue cycling
- The current mode is shown at the bottom of your terminal

### At launch:
```bash
# Start in experimental mode (enables autopilot)
copilot --experimental

# Start with a specific prompt
copilot --prompt "Add error handling to the API"

# Continue last session
copilot --continue
```

---

## Mode Selection Decision Tree

Use this flowchart to pick the right mode:

```
Is the task well-defined and low-risk?
├─ Yes → Is it repetitive or boilerplate?
│         ├─ Yes → Use AUTOPILOT MODE
│         └─ No → Use PLAN MODE
└─ No → Is it exploratory or learning-focused?
          ├─ Yes → Use CHAT MODE
          └─ No → Use PLAN MODE
```

---

## Real-World Solo Developer Scenarios

### Scenario 1: Bug Fix (Unknown Cause)
**Mode:** Chat Mode
**Why:** You need to explore, ask questions, and understand the issue before fixing.
```
1. "Why is the login form failing on mobile?"
2. Review explanation
3. "Show me the relevant CSS and JS files"
4. Identify issue
5. "Fix the viewport meta tag issue"
```

### Scenario 2: New Feature Implementation
**Mode:** Plan Mode
**Why:** Multi-step process with dependencies between components.
```
1. "Add a search feature to the blog with filtering by tags"
2. Review the 7-step plan
3. Approve execution
4. Review each step as it completes
5. Run final tests
```

### Scenario 3: Writing Tests
**Mode:** Autopilot Mode
**Why:** Well-defined task, easy to validate output.
```
1. Enable experimental mode
2. "Write unit tests for all API endpoints in src/api/"
3. Let autopilot work
4. Review generated tests
5. Run test suite to verify
```

### Scenario 4: Refactoring
**Mode:** Plan Mode
**Why:** Need to see impact across files and dependencies.
```
1. "Refactor the database queries to use async/await instead of callbacks"
2. Review plan showing all affected files
3. Approve step-by-step execution
4. Verify tests still pass
```

### Scenario 5: Learning a New Framework
**Mode:** Chat Mode
**Why:** Exploratory, lots of questions, learning-focused.
```
1. "Explain how routing works in this Next.js app"
2. "Show me an example of adding a new route"
3. "What's the difference between getServerSideProps and getStaticProps?"
4. "Create a new page using getStaticProps"
```

---

## Advanced Mode Tips for Solo Developers

### Combining Modes in a Workflow
You don't have to stick to one mode per session:

1. **Start with Chat** - Understand the problem
2. **Switch to Plan** - Map out the solution
3. **Execute the plan** - Implement with approvals
4. **Switch to Autopilot** - Let it write the tests
5. **Back to Chat** - Debug any issues

### Mode-Specific Slash Commands

**In any mode:**
- `/context` - Check what's in context
- `/diff` - See pending changes
- `/review` - Get a code review
- `/model` - Switch AI models
- `/usage` - Check token usage

**Plan mode specific:**
- Ask to modify the plan: "Add error handling to step 3"
- Request plan details: "Explain why you chose this approach"
- Break it down: "Create a more detailed plan for step 5"

**Autopilot tips:**
- Give it clear success criteria: "All tests must pass"
- Provide boundaries: "Only modify files in src/components/"
- Set constraints: "Keep the same API interface"

---

## Delegation Mode (Advanced)

For tasks that need the full power of Copilot coding agent in the cloud:

```bash
/delegate implement OAuth2 authentication with Google and GitHub providers
```

Or prefix with `&`:
```bash
& implement OAuth2 authentication with Google and GitHub providers
```

**When to delegate:**
- Complex tasks requiring deep research
- Multi-step implementations with many edge cases
- Tasks that would take hours of your time
- When you want to work on something else while it runs

**Solo developer advantage:**
- Offload time-consuming work
- Get a complete implementation to review and refine
- Learn patterns from the implementation
- Better work-life balance - delegate before end of day, review next morning

---

## Managing Context Across Modes

All modes share the same context in a session:

### Keep context clean:
```bash
/compact        # Compress context to save tokens
/clear          # Clear context and start fresh
/context        # See what's currently in context
```

### Add context strategically:
```bash
@src/auth.js    # Include specific file
@src/**/*.test.js  # Include all test files
!git log -5     # Include recent commits
```

### For solo developers:
- Start fresh for unrelated tasks to avoid confusion
- Use `/compact` when approaching token limits
- Include relevant docs or examples in context
- Save sessions worth resuming: they remember context

---

## Session Management for Solo Work

### Resume valuable sessions:
```bash
copilot --resume        # Pick from recent sessions
copilot --continue      # Jump back into last session
```

### Start fresh:
```bash
copilot                 # New session
```

### Save and name important sessions:
Within the CLI, your sessions are auto-saved. Use descriptive initial prompts so you can find them later:
```
"Implement payment processing feature" (easy to find)
vs
"help me with this" (hard to find later)
```

---

## Common Pitfalls and How to Avoid Them

### ❌ Using autopilot for critical logic
**Problem:** Autopilot might make assumptions about business rules.
**Solution:** Use plan mode for anything business-critical; review carefully.

### ❌ Staying in chat mode for large tasks
**Problem:** Lose track of progress, too many manual approvals.
**Solution:** Switch to plan mode for multi-step tasks.

### ❌ Not reviewing autopilot output
**Problem:** Bugs or security issues slip through.
**Solution:** Always review code, run tests, and use `/review`.

### ❌ Fighting the mode instead of switching
**Problem:** Frustrated when chat mode needs 20 approvals.
**Solution:** Recognize when to switch modes (Shift+Tab is quick!).

### ❌ Letting context get stale
**Problem:** Copilot uses outdated information from earlier in session.
**Solution:** Use `/compact` or start fresh for new tasks.

---

## Productivity Hacks for Solo Developers

### 1. **Morning Mode Routine**
```bash
copilot --experimental
# Use autopilot to:
# - Update dependencies
# - Fix linter warnings
# - Generate missing tests
# - Update documentation
```

### 2. **Deep Work Mode**
```bash
copilot --experimental=false  # Disable autopilot
# Use plan mode for focused feature work
# More intentional, less distraction
```

### 3. **Learning Mode**
```bash
# Stay in chat mode
# Ask questions before implementing
# Request explanations for suggestions
# Build understanding, not just code
```

### 4. **Cleanup Mode**
```bash
copilot --experimental
# Use autopilot for:
# - Removing dead code
# - Standardizing formatting
# - Adding missing types
# - Writing documentation
```

### 5. **Friday Afternoon Mode**
```bash
# Use chat or plan mode only
# Avoid autopilot when tired
# More review, less trust
# Safer mode when context-switching is harder
```

---

## Measuring Mode Effectiveness

Track which modes work best for which tasks in your workflow:

### Ask yourself:
- **Speed:** Did this mode save time?
- **Quality:** Is the output what I wanted?
- **Learning:** Did I understand what happened?
- **Stress:** Was it pleasant to use?

### Adjust accordingly:
- If autopilot produces code you don't understand → use plan mode
- If chat mode feels tedious → switch to plan mode
- If plan mode feels like overkill → try chat mode
- If you're not learning → spend more time in chat mode

---

## Final Thoughts for Solo Developers

The best mode is the one that fits **your current task and energy level**:

- **Tired or unfocused?** Use chat mode for safety and learning.
- **Deep work time?** Use plan mode for focused feature development.
- **Batch processing?** Use autopilot for repetitive, well-defined tasks.
- **Complex problem?** Start in chat, plan the solution, execute the plan.

**Remember:**
- Shift+Tab is your friend - don't be afraid to switch modes mid-task
- Every mode is a tool; master when to use each one
- As a solo dev, you're both the decision-maker and the reviewer
- The goal is to amplify your abilities, not replace your judgment

Start with chat mode until you're comfortable, then gradually experiment with plan and autopilot. Within a few weeks, you'll develop an intuition for which mode fits each situation.

Happy coding! 🚀

---

**Quick Reference Card:**

| Mode | Activation | Best For | Risk Level |
|------|-----------|----------|------------|
| Chat | Default | Exploration, learning, questions | Low |
| Plan | Shift+Tab | Multi-file changes, features | Medium |
| Autopilot | Shift+Tab×2 + experimental | Boilerplate, tests, repetitive tasks | Medium-High |
| Delegate | `/delegate` or `&` | Complex cloud-based tasks | Medium |

**Mode switching:** Shift+Tab cycles through available modes
**Experimental mode:** Required for autopilot - enable with `--experimental` or `/experimental`
