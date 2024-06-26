# Poe-API-Server
 An API server that lets you interact with Poe.com, using Selenium. It's just a test project and should not be used for any productive purposes.

It can simulate an OpenAI Proxy and be used with SillyTavern.

### Installation guide

~~Docker:~~
~~1. Install it with 'docker compose up'~~
~~2. Wait until it's running and listening (by default to 0.0.0.0:5000)~~

Python:
1. Install python 3.11
2. Install requirements.txt
3. Start app.py
4. Wait until it's running and listening (by default to 0.0.0.0:5000)

~~For Windows you can alternatively also use the [release version](https://github.com/vfnm/Poe-API-Server/releases/latest), just extract it and open the executable file.~~

### Use with SillyTavern
1. Select Chat Completion API
2. Open the settings and enter 'http://IP:Port/v2/driver/sage' in 'Alternative server URL'. Replace IP and port with the real value
3. Enter your 'p_b_cookie' and 'bot_name' in 'Proxy Password', using this format: p_b_cookie|bot_name
5. Set the 'Context Size (tokens)' to '2048' unless you use Claude-100K, ChatGPT-16K or GPT-4-32K
6. Empty all prompt fields expect for main prompt, where you need to add [Character=={{char}}] [User=={{user}}]
7. If you want to use the Claude Jailbreak, you also need to add this: [ClaudeJB]
8. Activate streaming
9. Close the settings and click connect
10. For GPT-3.5/4 based bots, you can get better results by modifying 'instruction' in config.json. The file will be created after the first launch, it can be changed to something like this: `"instruction": "Read the instructions in here"`
11. If you have a problem with the message being sent as a file, you can disable this by modifying 'send-as-text-limit' in config.json, for example to `"send-as-text-limit": 99999`, this solves the issue with the bot keep asking for a prompt, which can sometimes happen with OpenAI based bots

It can also run on Termux.


### Main API Endpoints

    GET /latest-message
    Returns the bot's latest message, message generation status, and suggestions if they exist

    POST /send-message
    Sends a message. Requires 'message', can optionally clear the context with 'clear_context' = true

    POST /clear-context
    Clears the bot's context

    POST /start-driver
    Starts the driver. Requires 'p_b_cookie' and 'bot_name'

    POST /kill-driver
    Kills the driver

    POST /abort-message
    Aborts the current message generation

    GET /is-generating
    Returns the current message generation status
