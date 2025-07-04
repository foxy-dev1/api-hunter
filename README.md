# 🕵️‍♂️ API Hunter

**API Hunter** is a lightweight Python tool that scans staged Git files for sensitive credentials like API keys, access tokens, and private keys before you commit them.

> 🔒 Catch secrets before they leak. Simple, fast, and configurable.

---

## 🚀 Features

- ✅ Scans only files added via `git add` (i.e., staged files)
- 🔍 Detects:
  - AWS, GitHub, Google, Slack tokens
  - API keys, auth tokens, secret keys
  - Private keys and database URLs
- ⚡️ Async scanning for fast performance
- 🛠️ Custom regex patterns (add/remove/display)
- 🤖 Gemini integration for automatic regex generation (with API key anonymization)

---

## 📦 Installation

### From PyPI

```bash
pip install api-hunter

```

---

## 🛠️ CLI Commands

- **Scan all staged files in git repo:**
  ```bash
  hunt
  ```
- **Scan a specific file:**
  ```bash
  hunt -n path/to/file.py
  ```
- **Add a custom pattern:**
  ```bash
  hunt -a "my_service" "my_service_[a-zA-Z0-9]{32}"
  ```
- **Remove a custom pattern:**
  ```bash
  hunt -r "my_service"
  ```
- **Display all custom patterns:**
  ```bash
  hunt -d
  ```
- **Configure Gemini API key:**
  ```bash
  hunt -c "your-gemini-api-key"
  ```
- **Generate and add a regex for a new API key using Gemini:**
  ```bash
  hunt -re "my_service" "sk-abc123..."
  ```
  > **Note:** The tool randomizes the digits in your API key before sending it to Gemini, so your actual key is never exposed.

---

## 💡 Example Usage

```bash
# Scan all staged files in your git repo
hunt

# Scan a specific file
hunt -n path/to/file.py

# Add a custom pattern
hunt -a "my_service" "my_service_[a-zA-Z0-9]{32}"

# Remove a custom pattern
hunt -r "my_service"

# Display all custom patterns
hunt -d

# Configure Gemini API key
hunt -c "your-gemini-api-key"

# Generate and add a regex for a new API key using Gemini
hunt -re "my_service" "sk-abc123..."
```

---

## 📝 Notes

- Custom patterns and Gemini API key are stored in `~/api_hunt_envs/`.
- Only files with common code/config extensions are scanned (see `api_hunt/patterns.py`).
- For Gemini integration, you need a valid Google Gemini API key.
- **Privacy:** When generating a regex for your API key using Gemini, API Hunter randomizes the digits in your key before sending it to the LLM. This ensures your actual API key is never exposed to any third party.
