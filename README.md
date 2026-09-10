# 🤖 AI Auto Reply Bot

An AI-powered desktop automation bot that reads a WhatsApp chat, analyzes the conversation using OpenAI, generates an intelligent reply, and automatically sends the response through the WhatsApp web interface.

The project combines **Python, OpenAI API, PyAutoGUI, and clipboard automation** to create an automated AI reply workflow.

---

## 🚀 Features

- 🤖 AI-generated chat responses using OpenAI
- 💬 Reads chat history directly from the desktop interface
- 🖱️ Automates mouse and keyboard actions with PyAutoGUI
- 📋 Uses clipboard operations to read and send messages
- 🔍 Detects whether the latest message was sent by a specific person
- 🌐 Supports Hindi + English conversational responses
- 🔄 Continuously monitors the chat for new messages
- 😂 Can generate casual and humorous responses based on the configured AI personality

---

## 🧠 How It Works

The bot follows this basic workflow:

```text
WhatsApp Web
     │
     ▼
Select Chat History
     │
     ▼
Copy Text to Clipboard
     │
     ▼
Python Reads Clipboard
     │
     ▼
Check Latest Sender
     │
     ▼
Send Chat History to OpenAI
     │
     ▼
Generate AI Response
     │
     ▼
Copy AI Response
     │
     ▼
Paste into WhatsApp
     │
     ▼
Send Message
```

The main automation is implemented in `bot.py`. It uses PyAutoGUI to interact with the browser, Pyperclip to access clipboard contents, and the OpenAI client to generate the response. citeturn0view1

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| **Python** | Main programming language |
| **OpenAI API** | AI-powered response generation |
| **PyAutoGUI** | Mouse and keyboard automation |
| **Pyperclip** | Clipboard access |
| **Google Chrome** | Browser interface for WhatsApp |
| **WhatsApp Web** | Messaging interface |

---

## 📁 Project Structure

```text
AI_Autoreply_Bot/
│
├── bot.py
├── get_cursor.py
├── openai.py
└── README.md
```

### `bot.py`

The main application.

It:

1. Opens/interacts with the browser.
2. Selects the visible chat history.
3. Copies the conversation.
4. Reads the copied text.
5. Checks whether the latest message is from the configured sender.
6. Sends the conversation to OpenAI.
7. Generates a response.
8. Pastes the response into the chat.
9. Sends the message automatically. citeturn0view1

### `get_cursor.py`

A small utility used to identify mouse coordinates on the screen.

This is useful when configuring the PyAutoGUI coordinates required by the automation script. citeturn0view2

### `openai.py`

A separate OpenAI API testing/example script.

It demonstrates sending a predefined WhatsApp-style conversation to OpenAI and printing the generated response. citeturn1view0

---

## ⚙️ Requirements

Before running the project, make sure you have:

- Python 3.x
- Google Chrome
- WhatsApp Web
- An OpenAI API key
- An internet connection
- A Windows desktop environment recommended for the current coordinate-based setup

---

## 📦 Installation

### 1. Clone the repository

```bash
git clone https://github.com/pp80768241-alt/AI_Autoreply_Bot.git
```

### 2. Enter the project directory

```bash
cd AI_Autoreply_Bot
```

### 3. Install required Python packages

```bash
pip install pyautogui pyperclip openai
```

---

## 🔑 OpenAI API Key

The bot requires an OpenAI API key to generate responses.

The current source code initializes the OpenAI client with an API-key placeholder. citeturn0view1turn1view0

For security, **do not commit your real API key to GitHub**.

A recommended approach is to store the key in an environment variable.

### Windows PowerShell

```powershell
$env:OPENAI_API_KEY="your_api_key_here"
```

Then configure the OpenAI client to read the environment variable rather than placing the key directly inside the Python file.

> ⚠️ If you have ever accidentally committed a real API key to a public repository, revoke/rotate that key immediately.

---

## ▶️ Running the Bot

### Step 1 — Open WhatsApp Web

Open WhatsApp Web in Google Chrome and log in to your account.

### Step 2 — Open the required chat

Navigate to the conversation that the bot should monitor.

### Step 3 — Configure the screen coordinates

The current implementation uses fixed screen coordinates for mouse operations.

For example, the script contains coordinates for:

- Browser interaction
- Selecting chat history
- Message input
- Sending the message

These coordinates are specific to the screen layout used when the script was created. citeturn0view1

If the coordinates don't work on your computer, use:

```bash
python get_cursor.py
```

Move your mouse to the required UI elements and use the displayed coordinates to update `bot.py`.

### Step 4 — Start the bot

```bash
python bot.py
```

The bot will continuously monitor the configured chat and generate a reply when the configured sender is detected.

---

## 🧩 AI Personality

The current bot uses a custom system prompt to define the AI's personality.

The configured personality is designed to:

- Speak Hindi and English
- Act as a coder from India
- Analyze the conversation
- Respond casually
- Use humorous/roasting-style responses

The personality can be customized by modifying the system prompt inside `bot.py`. citeturn0view1

For example:

```python
{
    "role": "system",
    "content": "Your custom AI personality here"
}
```

---

## 🎯 Sender Detection

The bot contains a function that checks whether the latest portion of the copied chat history contains a configured sender name.

The current sender is:

```text
Rohan Das
```

This can be changed in:

```python
is_last_message_from_sender(chat_history, sender_name="Rohan Das")
```

For example:

```python
is_last_message_from_sender(
    chat_history,
    sender_name="Your Contact Name"
)
```

---

## 🔄 Continuous Automation

The main bot runs inside a continuous loop:

```python
while True:
```

It periodically:

1. Selects the chat.
2. Copies the conversation.
3. Reads the clipboard.
4. Checks the sender.
5. Generates an AI response when appropriate.
6. Sends the response.

A delay is included between iterations to avoid performing the actions continuously. citeturn0view1

---

## ⚠️ Current Limitations

This project is currently a **desktop GUI automation prototype**, so there are several limitations.

### 1. Hard-coded screen coordinates

The bot relies on fixed coordinates such as:

```python
pyautogui.click(...)
pyautogui.moveTo(...)
pyautogui.dragTo(...)
```

Changing the screen resolution, browser size, zoom level, or WhatsApp layout may cause the automation to fail.

### 2. Browser/UI dependency

The bot depends on the current visual layout of WhatsApp Web.

Changes to the website interface may require changes to the automation coordinates.

### 3. Sender detection

The current implementation uses text matching to determine whether the configured person sent the latest message.

This is not a full WhatsApp message parser.

### 4. No persistent conversation memory

The bot sends the copied chat history to the AI but does not implement its own database or long-term memory system.

### 5. No error recovery system

The current prototype does not have comprehensive handling for situations such as:

- Browser not being open
- WhatsApp Web being logged out
- Clipboard failures
- API failures
- Network interruptions
- Incorrect screen coordinates

---

## 🔐 Security

**Never expose your OpenAI API key publicly.**

Do not commit secrets such as:

```text
OPENAI_API_KEY
```

to GitHub.

A `.env` file or operating-system environment variable should be used for local development.

If using `.env`, add it to `.gitignore`:

```gitignore
.env
.env.local
__pycache__/
*.pyc
```

---

## 🧪 Example Use Case

Imagine a WhatsApp conversation:

```text
Rohan: Bro, what are you doing?

Bot: Just coding.

Rohan: Again? 😂

Bot: Someone has to keep the bugs employed.
```

The bot can read the conversation, send it to the AI, generate a context-aware response, and automatically send the generated message.

---

## 💡 Future Improvements

Several improvements could make this project more reliable and production-ready.

### 🔹 Better WhatsApp automation

Replace hard-coded coordinates with more reliable UI detection or browser automation.

Possible approaches:

- Selenium
- Playwright
- Browser automation APIs
- Image/template recognition

### 🔹 Environment-based configuration

Move configuration values such as:

- API key
- Sender name
- AI model
- Response style

into environment variables or a configuration file.

### 🔹 Better message detection

Instead of repeatedly copying the entire chat, detect only newly received messages.

### 🔹 Conversation memory

Add a database such as:

- SQLite
- MongoDB
- PostgreSQL

to maintain conversation history.

### 🔹 Web dashboard

Create a dashboard where users can configure:

- Contact
- AI personality
- Reply style
- Enable/disable auto-reply
- Response delay

### 🔹 Improved error handling

Add proper handling for:

```text
API errors
Network errors
Browser errors
Clipboard errors
UI changes
Authentication issues
```

### 🔹 Multiple contacts

Allow the bot to manage different reply settings for different contacts.

---

## 📚 What I Learned From This Project

This project provides practical experience with:

- Python automation
- Working with external APIs
- OpenAI API integration
- GUI automation
- Clipboard management
- Conditional logic
- Infinite loops
- Function creation
- Prompt engineering
- Browser-based automation
- Automating repetitive tasks

---

## ⚠️ Disclaimer

This project is intended for **educational and personal automation purposes**.

Use automation responsibly and make sure your use complies with the terms and policies of the messaging platform, OpenAI, and any other services involved.

The project is not affiliated with or officially supported by WhatsApp or OpenAI.

---

## 👨‍💻 Author

**Prince Panwar**

B.Tech Computer Science & Engineering — Data Science

GitHub:  
https://github.com/pp80768241-alt

---

## ⭐ Support

If you found this project useful or interesting, consider giving the repository a ⭐ on GitHub.

---

## 📄 License

This project currently does not include a license.

If you plan to make the project open source for others to use, consider adding an appropriate license such as the MIT License.
