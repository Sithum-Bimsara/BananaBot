# 🍌 BananaBot

A fun and simple Telegram chatbot built with Python that responds to user messages and commands. This is my first Telegram bot project, created to explore and learn the basics of chatbot development using the `python-telegram-bot` library.

GitHub Repository: [BananaBot](https://github.com/Sithum-Bimsara/BananaBot.git)

---

## 🛠 Features

* Responds to basic greetings and phrases
* Supports `/start`, `/help`, and `/custom` commands
* Handles messages differently in private chats and group chats
* Built using `python-telegram-bot` (v20+)

---

## 🧑‍💻 How to Run This Bot

### 1. Clone the Repository

```bash
git clone https://github.com/Sithum-Bimsara/BananaBot.git
cd BananaBot
```

### 2. Create and Activate a Virtual Environment (optional but recommended)

```bash
python -m venv venv

# Windows:
venv\Scripts\activate

# macOS/Linux:
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

> If `requirements.txt` doesn't exist, manually install:

```bash
pip install python-telegram-bot
```

### 4. Set Your Bot Token

Open the `bot.py` file and replace the `TOKEN` value with your actual Telegram Bot Token provided by [BotFather](https://t.me/BotFather).

```python
TOKEN: Final = 'YOUR_BOT_TOKEN_HERE'
```

### 5. Run the Bot

```bash
python bot.py
```

You should see:

```
Starting the bot...
Polling...
```

Your bot is now running and listening for messages!

---

## 🤖 Bot Behavior and Code Breakdown

### Main Components:

#### 1. **Commands**

* `/start` — Sends a welcome message.
* `/help` — Explains the bot's purpose.
* `/custom` — Responds with a custom message.

Each command is defined as an asynchronous function and registered with the `Application` object using `CommandHandler`.

#### 2. **Message Handling**

* Responds to text messages (not commands) with predefined replies.
* In group chats, it only responds if mentioned using its `BOT_USERNAME`.

#### 3. **Error Handling**

* Logs any errors that occur during polling or message processing.

#### 4. **Custom Response Logic**

Located in the `handle_response(text: str)` function:

```python
if 'hello' in processed:
    return 'Hey there!'
elif 'how are you' in processed:
    return 'I am fine, thank you!'
```

You can expand this logic to add more intelligent or funny responses.

---

## ✅ To-Do / Improvements

* Hide the bot token using environment variables
* Add more commands and message handling cases
* Add emoji reactions or media support

---

## 📄 License

This project is for learning purposes and is licensed under the MIT License.

---

Happy chatting with BananaBot! 🍌
