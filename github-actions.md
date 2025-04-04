# 💡 What is GitHub Actions?

**GitHub Actions** is a tool built into GitHub that helps you **automate tasks** like:
- Testing your code
- Building your application
- Deploying to servers or the cloud  
➡️ Every time someone **pushes code**, **opens a pull request**, or even on a **schedule**, you can run actions automatically.

It’s like giving your project a robot that listens and takes care of tasks for you 🤖.

---

# 📂 Where does it live?

In your GitHub repository, GitHub Actions lives inside:
```
.github/workflows/
```

Inside that folder, you add `.yml` files. These files define your **workflows**.

---

# 🔄 What is a Workflow?

A **workflow** is a set of instructions that tells GitHub what to do and when.

Example:  
> "When someone pushes code, run tests, then deploy."

Each workflow file is written in **YAML** (easy-to-read text format).

---

# 🧱 Structure of a Workflow

Here’s how a simple GitHub Actions workflow looks:

```yaml
name: My First Workflow

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Run a script
        run: echo "Hello, world!"
```

Let’s break it down:

| Part | What it means |
|------|----------------|
| `name` | Name of the workflow |
| `on` | When to run this (e.g., `push`, `pull_request`, `schedule`) |
| `jobs` | A set of tasks to run |
| `runs-on` | What kind of machine to run on (e.g., `ubuntu-latest`) |
| `steps` | The actual commands to run |
| `uses` | Reuse someone else's action (like checking out code) |
| `run` | Write your own command |

---

# ⚙️ Triggers (`on:`)

Here are common triggers to run a workflow:

| Trigger | What it does |
|--------|---------------|
| `push` | Runs when code is pushed |
| `pull_request` | Runs when a pull request is opened/updated |
| `schedule` | Runs at specific times (like a cron job) |
| `workflow_dispatch` | Runs manually (button click) |

---

# 🧪 Example: Run Tests on Code Push

```yaml
name: Run Tests

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run Unit Tests
        run: npm test
```

This runs `npm test` every time someone pushes code to GitHub.

---

# 🔐 Secrets and Environment Variables

You can use **secrets** (like passwords or API keys) securely:

```yaml
env:
  MY_API_KEY: ${{ secrets.MY_API_KEY }}
```

You define secrets in your repo settings:  
**Settings → Secrets and variables → Actions**

---

# 🧩 Popular Built-in Actions

You don’t have to write everything from scratch. Some useful pre-made actions:

| Action | What it does |
|--------|--------------|
| `actions/checkout` | Checks out your code |
| `actions/setup-node` | Sets up Node.js |
| `actions/upload-artifact` | Uploads build files |
| `actions/download-artifact` | Downloads files from earlier jobs |

---

# 🤝 Matrix Strategy (Optional)

You can test on **multiple environments** like this:

```yaml
strategy:
  matrix:
    node-version: [14, 16, 18]

steps:
  - uses: actions/setup-node@v3
    with:
      node-version: ${{ matrix.node-version }}
```

This will run the job **3 times**, once for each Node.js version.

---

# 🧪 Common Use Cases

| Task | GitHub Actions Can Help |
|------|--------------------------|
| Test your code | Run unit/integration tests automatically |
| Linting | Check for coding style errors |
| Build | Compile your code (Java, Node, etc.) |
| Deploy | Deploy to AWS, Azure, Netlify, Vercel, etc. |
| Notifications | Send Slack/Discord/email alerts |

---

# ✅ Practice Task (You can try)

Create this file in your repo:  
`.github/workflows/hello-world.yml`

```yaml
name: Hello World

on: [push]

jobs:
  say-hello:
    runs-on: ubuntu-latest
    steps:
      - name: Print Message
        run: echo "Hello from GitHub Actions!"
```

Then push the code — and watch the magic happen 💫

---

# 📌 Summary

| Topic | Summary |
|-------|---------|
| What is it? | Automation tool inside GitHub |
| File type | `.yml` files in `.github/workflows/` |
| Key parts | Triggers, Jobs, Steps |
| Benefits | Saves time, avoids manual tasks, improves code quality |

---
