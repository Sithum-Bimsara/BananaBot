# 📘 Table of Contents

- [🚀 Project Overview](#project-overview)
- [🛠️ 01 - How to Create and Set Up a Telegram Bot Locally](#01_how_to_create_and_set_up_a_telegram_bot_locally)
- [🧠 02 - Python Code Review](#02_python_code_review)
- [🌐 03 - Host the Bot](#03_host_the_bot)
- [📄 License](#license)

# Project Overview
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

# 01_How_to_Create_and_Set_Up_a_Telegram_Bot_locally

---

### 🤖 Step-by-Step Guide to Create a Telegram Bot using BotFather

1. **Start a Chat with BotFather**

   * Open Telegram and search for **BotFather** or visit 👉 [https://t.me/BotFather](https://t.me/BotFather)
   * Type `/start` to begin interacting.

2. **Create a New Bot**

   * Command: `/newbot`
   * BotFather will ask for:

     * **Bot Name**: Any friendly name. (e.g., `Banana Bot` 🍌)
     * **Username**: Must end with `bot`. (e.g., `sithum_banana_bot`)
   * ✅ BotFather will confirm creation and give you your **Bot Token** (Keep this safe!)

     ```
     Example Token:
     7846752505:AAhjbgu_KfQcLYghNGEUiBgUDqx76l7nVvQ
     ```

3. **Customize Your Bot**

   * `/setdescription` ➡️ Adds a description shown on bot chat startup.

     * `I can respond as a banana`
   * `/setabouttext` ➡️ Adds short info in profile view.

     * `I am a banana bot. I like bananas`
   * `/setuserpic` ➡️ Add a profile picture 🍌
   * `/setname` ➡️ Change bot name if needed
   * `/setcommands` ➡️ Define bot commands:

     ```
     start - Starts the bot
     help - Provides help for Banana Bot
     custom - This is a custom command
     ```

---

### 🐍 Integrating Telegram Bot with Python

#### ✅ Requirements



### 1. Clone the Repository or make a python file(bot.py) and add the following code in there.

```bash
git clone https://github.com/Sithum-Bimsara/BananaBot.git
cd BananaBot
```

### 2. Create and Activate a Virtual Environment (optional but recommended)

```bash
python -m venv venv


# Activate Virtual Environment in Windows:
venv\Scripts\activate

# Activate Virtual Environment in macOS/Linux:
source venv/bin/activate
```

### 2. Install Dependencies

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



#### 🧠 Sample Python Code to Start the Bot:

```python
from typing import Final
from telegram import Update 
from telegram.ext import Application, CommandHandler, MessageHandler,filters, ContextTypes

TOKEN: Final = '7844852505:AAGzbgu_KfQcLYghNGERNBgUDqx76l9mVvQ'
BOT_USERNAME: Final = '@sithum_banana_bot'

# Commands
async def start_command(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "Hello! Thanks for chatting with me. I'm a banana!"
    )

async def help_command(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        " I'm a banana!. Please type something so I can respond!"
    )   

async def custom_command(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "This is a custom command!"
    )  


# Responses
def handle_response(text: str) -> str:
    processed: str = text.lower()
    
    if 'hello' in processed:
        return 'Hey there!'
    if 'how are you' in processed:
        return 'I am fine, thank you!'
    if 'i love you' in processed:
        return 'Remember to subscribe!'
    return 'I do not understand what you wrote...'

async def handle_message(update: Update, context: ContextTypes.DEFAULT_TYPE):
    message_type: str = update.message.chat.type
    text: str = update.message.text    

    print(f'User ({update.message.chat.id}) in {message_type}: "{text}"')


    # Use the commented code if you only want to respond bot only if tag in a group
    # if message_type == 'group':
    #     if BOT_USERNAME in text:
    #         new_text: str = text.replace(BOT_USERNAME, '').strip()
    #         response: str = handle_response(new_text)
    #     else:
    #         return
    # else:
    #     response: str = handle_response(text) 

    response: str = handle_response(text) 

    print(f'Bot: "{response}"') 
    await update.message.reply_text(response)   


async def error(update: Update, context: ContextTypes.DEFAULT_TYPE):
    print(f'Update "{update}" caused error "{context.error}"')


if __name__ == '__main__':
    print('Starting the bot...')
    app = Application.builder().token(TOKEN).build()

    # Commands
    app.add_handler(CommandHandler('start', start_command))
    app.add_handler(CommandHandler('help', help_command))
    app.add_handler(CommandHandler('custom', custom_command))

    # Messages
    app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))

    # Errors
    app.add_error_handler(error)

    print('Polling...')
    app.run_polling(poll_interval=3)
```

#### 🔍 What the Code Does:

* Initializes the bot using the **token** you received
* Defines handlers for `/start`, `/help`, and `/custom`
* Uses **polling** to listen for incoming messages (alternatively, you can use webhooks)

---


#### 

### ⚠️ Tips and Security

* Keep your **Bot Token** private and safe. Anyone with it can control your bot!
* You can regenerate it anytime using `/token` in BotFather.
* If deploying publicly, consider setting up webhook with SSL and a secret path.

---

### 🎉 Your Bot is Now Live!

Try chatting with it here: [@sithum\_banana\_bot](https://t.me/sithum_banana_bot)

---

Need more help? Check the [Telegram Bot API docs](https://core.telegram.org/bots/api) 📖

---
# 02_Python_Code_Review

---

## 📌 Overview:

This bot uses the `python-telegram-bot` library to interact with users via Telegram.
It supports commands like `/start`, `/help`, and `/custom`, and responds to text messages using simple keyword-based logic.

---

## 🧱 Key Components:

### 📥 Imports and Constants:

```python
from typing import Final
from telegram import Update
from telegram.ext import Application, CommandHandler, MessageHandler, filters, ContextTypes

TOKEN: Final = '...'
BOT_USERNAME: Final = '@sithum_banana_bot'
```

* Sets up necessary modules and constants.
* `TOKEN` is used to authenticate the bot.

---

### 💬 Command Handlers:

These are triggered by Telegram commands:

* **`/start`** → `start_command()`: Greets the user.
* **`/help`** → `help_command()`: Informs users what to do.
* **`/custom`** → `custom_command()`: Placeholder for a custom action.

---

### 🧠 Message Response Logic:

```python
def handle_response(text: str) -> str:
```

* Processes plain text messages.
* Responds to keywords like:

  * "hello" → "Hey there!"
  * "how are you" → "I am fine, thank you!"
  * "i love you" → "Remember to subscribe!"
  * Else → "I do not understand what you wrote..."

---

### 📩 Message Handler:

```python
async def handle_message(update: Update, context: ContextTypes.DEFAULT_TYPE):
```

* Listens for **non-command text** messages.
* Optionally checks if bot is tagged in a **group chat**.
* Calls `handle_response()` and replies with a suitable message.

---

### ⚠️ Error Handler:

```python
async def error(update: Update, context: ContextTypes.DEFAULT_TYPE):
```

* Logs any **runtime errors** that occur while handling updates.

---

### 🚀 Main Bot Execution:

```python
if __name__ == '__main__':
```

* Initializes the bot application.
* Registers command and message handlers.
* Starts **polling** every 3 seconds to check for new messages.

---


```python
# Import necessary modules
from typing import Final  # Final type hint used to denote constants
from telegram import Update  # Represents an incoming update (message, command, etc.)
from telegram.ext import (
    Application,  # Main application class to manage the bot
    CommandHandler,  # Used to handle commands like /start, /help
    MessageHandler,  # Used to handle non-command messages (like texts)
    filters,  # For filtering messages (text, command, etc.)
    ContextTypes  # Context object passed to handlers
)

# Define bot token and username
TOKEN: Final = 'your_bot_token_here'  # Replace with your actual bot token
BOT_USERNAME: Final = '@your_bot_username_here'

# Command Handlers
aSync def start_command(update: Update, context: ContextTypes.DEFAULT_TYPE):
    # Respond to /start command
    await update.message.reply_text(
        "Hello! Thanks for chatting with me. I'm a banana!"
    )

async def help_command(update: Update, context: ContextTypes.DEFAULT_TYPE):
    # Respond to /help command
    await update.message.reply_text(
        " I'm a banana!. Please type something so I can respond!"
    )

async def custom_command(update: Update, context: ContextTypes.DEFAULT_TYPE):
    # Respond to /custom command
    await update.message.reply_text(
        "This is a custom command!"
    )

# Function to generate a response based on user's message
def handle_response(text: str) -> str:
    processed: str = text.lower()  # Convert input to lowercase for comparison

    # Basic text matching
    if 'hello' in processed:
        return 'Hey there!'
    if 'how are you' in processed:
        return 'I am fine, thank you!'
    if 'i love you' in processed:
        return 'Remember to subscribe!'
    return 'I do not understand what you wrote...'

# Handler for any text messages
aSync def handle_message(update: Update, context: ContextTypes.DEFAULT_TYPE):
    message_type: str = update.message.chat.type  # Get type of chat (private, group)
    text: str = update.message.text  # Get message text

    print(f'User ({update.message.chat.id}) in {message_type}: "{text}"')

    # Optional: respond only if mentioned in a group
    # if message_type == 'group':
    #     if BOT_USERNAME in text:
    #         new_text: str = text.replace(BOT_USERNAME, '').strip()
    #         response: str = handle_response(new_text)
    #     else:
    #         return
    # else:
    #     response: str = handle_response(text)

    response: str = handle_response(text)  # Generate a response

    print(f'Bot: "{response}"')
    await update.message.reply_text(response)  # Send the response to user

# Error handler
aSync def error(update: Update, context: ContextTypes.DEFAULT_TYPE):
    print(f'Update "{update}" caused error "{context.error}"')

# Main entry point to start the bot
if __name__ == '__main__':
    print('Starting the bot...')

    # Build the bot application using the token
    app = Application.builder().token(TOKEN).build()

    # Register command handlers
    app.add_handler(CommandHandler('start', start_command))
    app.add_handler(CommandHandler('help', help_command))
    app.add_handler(CommandHandler('custom', custom_command))

    # Register message handler for non-command text
    app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))

    # Register error handler
    app.add_error_handler(error)

    print('Polling...')
    # Start polling for updates (messages)
    app.run_polling(poll_interval=3)
```
---

# 03_Host_the_Bot 

Tired of keeping your PC on 24/7 just to keep your Telegram bot running? 🤖 Here's a **step-by-step guide** to host your bot online for free using **PythonAnywhere**!

---

### 🧠 Why Host Your Bot Online?

* Local script needs your PC to stay ON 🖥️
* Hosting online ensures your bot runs **24/7** ⏰
* No need to spend on another computer 💸

---

### 🌐 Step 1: Go to PythonAnywhere

1. Visit [pythonanywhere.com](https://www.pythonanywhere.com) 🌐
2. Sign up for a **free account** ✅
3. Log into your dashboard 🧑‍💻

---

### 📁 Step 2: Create Your Bot File

1. Click on **Files** in the dashboard 🗂️
2. Tap on **"New File"** ➕
3. Name your file, e.g., `telegram_bot.py` 📝
4. Paste your Telegram bot Python code into this file 💻

> Make sure your bot runs fine locally before proceeding!

---

### 📦 Step 3: Install Required Packages

1. Go to **Consoles** ➜ Open a **Bash Console** 🖥️
2. Install necessary packages using pip:

   ```bash
   pip install python-telegram-bot
   ```

   ✅ This will install the Telegram Bot API wrapper

> If your bot has more dependencies, install them here!

---

### ▶️ Step 4: Run the Bot

1. Go back to your bot file in **Files** 📂
2. Click **Run** ▶️
3. The console will show `Bot is polling...` 📡
4. Your bot is now **LIVE & listening**! 🎉

---

### 📲 Step 5: Test Your Bot

* Open Telegram & message your bot 🤖
* Try commands like:

  * `hello` ➜ replies "Hey there!"
  * `I love Python` ➜ replies "Remember to subscribe!"

> ✅ If the bot replies, you’re all set!

---

### 💤 Step 6: Close & Relax 😎

* Even if you **shut down your PC**, the bot will keep running! ✅
* PythonAnywhere handles the server part 📡

---

### ⚠️ Limitations of Free Plan

* Daily CPU limit: \~100 seconds of CPU time per day 🧠
* For light bots, it's enough 💡
* For more traffic: consider upgrading 🔼

---

### 🏁 Conclusion

✅ You now have a **Telegram bot** running 24/7 **for FREE**!

---

# License

This project is for learning purposes and is licensed under the MIT License.

---

Happy chatting with BananaBot! 🍌
