# Cricket Score WhatsApp Bot

A small Python script that requests cricket match data and sends a score summary to a configured WhatsApp recipient through Twilio.

## What the code does

1. Requests a match list from the CricAPI endpoint configured in the script.
2. Looks for a started match dated today using the current team filter.
3. Requests that match's score, or returns a no-match message.
4. Sends one WhatsApp message when the script is executed.

This is a one-shot sender, not an interactive chatbot, webhook server, or continuously scheduled service. The implemented filter checks `team-1 == "Auckland"` or `team-2 == "India"`; update it for the teams you actually want to follow.

## Setup

```bash
git clone https://github.com/CaptainVish/Cric-Score-Whatsapp-Bot.git
cd Cric-Score-Whatsapp-Bot
python3 -m venv .venv
source .venv/bin/activate
python -m pip install requests twilio
```

On Windows, activate the environment with `.venv\Scripts\activate` instead. Dependency versions are not pinned in this repository.

Before running [whatsapp-bot-live-cricket-score.py](whatsapp-bot-live-cricket-score.py):

- Check the configured legacy CricAPI endpoints and response fields against your provider account. Their current availability has not been verified.
- Supply your own cricket API credentials and Twilio account configuration in a local working copy.
- Configure a WhatsApp-capable sender and an authorized recipient; if using a sandbox, complete its recipient setup first.
- Review the match filter and the computer's date/timezone.

```bash
python whatsapp-bot-live-cricket-score.py
```

Running this command contacts external services and attempts to send a real WhatsApp message. Provider charges or account limits may apply. No message was sent as part of this README update.

## Credentials and reliability

The source contains a hardcoded cricket API credential. Treat any published credential as exposed: revoke/rotate it with the provider and use private configuration for replacements. Do not reuse or republish the committed value. The current script does **not** automatically read environment variables or a `.env` file; that requires a code change.

Before relying on this project, add request timeouts, HTTP/error handling, response validation, configurable team matching, and tests with mocked API responses. Neither current provider compatibility nor end-to-end delivery has been validated in this documentation pass.
