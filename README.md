from pathlib import Path
import json, zipfile, textwrap

base = Path("/mnt/data/aj-detailers-github")
base.mkdir(exist_ok=True)

prompt = """You are the voice assistant for AJ Detailers. Your job is to answer phone calls in a friendly, professional, and helpful way. Start with: 'Hey, you have reached AJ Detailers. How can I help you today?' Help customers with services such as interior detailing, exterior detailing, full detailing, seat shampoo, stain removal, polishing, paint correction, ceramic coating, and general car cleaning questions. Keep answers clear and natural. Ask follow-up questions when needed, such as vehicle type, preferred date, and the service they want. If pricing is not confirmed, give general guidance and let the customer know final pricing depends on vehicle size and condition. If a customer wants to book, collect their name, phone number, vehicle type, requested service, and preferred date/time. If the request is outside your scope, offer to take their details and pass them to the team. Stay polite, concise, and customer-focused. Do not make up business policies, exact prices, or availability if they are not provided."""
(base / "prompt.txt").write_text(prompt, encoding="utf-8")

config = {
    "business_name": "AJ Detailers",
    "agent_name": "AJ Detailers Voice Agent",
    "agent_id": "agent_af37bfc92c54d60fa25abab657",
    "language": "en-US",
    "voice_id": "minimax-Cimo",
    "initial_message": "Hey, you have reached AJ Detailers. How can I help you today?",
    "tone": "friendly",
    "style": "conversational",
    "services_supported": [
        "interior detailing",
        "exterior detailing",
        "full detailing",
        "seat shampoo",
        "stain removal",
        "polishing",
        "paint correction",
        "ceramic coating",
        "general car cleaning"
    ],
    "transfer_call": {
        "enabled": True,
        "type": "cold_transfer",
        "when_to_transfer": "When the caller ask to speak to human",
        "number": "+16723386143"
    },
    "end_call": {
        "enabled": True,
        "when_to_end": "When the conversation is complete",
        "max_duration_minutes": 60,
        "silence_timeout_seconds": 10,
        "voicemail_action": "hangup"
    },
    "notes": [
        "Retell hosts the live voice agent.",
        "GitHub can store documentation, prompts, and config files for backup and collaboration.",
        "Phone number deployment happens in Retell, not GitHub."
    ]
}
(base / "agent-config.json").write_text(json.dumps(config, indent=2), encoding="utf-8")

readme = f"""# AJ Detailers Voice Agent

This repository stores the configuration and prompt for the **AJ Detailers Voice Agent**.

## Agent details

- **Business:** AJ Detailers
- **Agent name:** AJ Detailers Voice Agent
- **Agent ID:** agent_af37bfc92c54d60fa25abab657
- **Language:** en-US
- **Voice:** minimax-Cimo

## Files in this repo

- `agent-config.json` — main configuration details
- `prompt.txt` — system prompt used by the voice agent

## Important

The live voice agent and phone number are hosted in **Retell AI**, not on GitHub.  
GitHub is useful for:
- saving the prompt
- keeping a backup of settings
- sharing setup files with a team
- tracking changes over time

## How to upload this folder to GitHub

### Option 1: GitHub website
1. Create a new repository on GitHub.
2. Click **Add file** → **Upload files**.
3. Upload `agent-config.json`, `prompt.txt`, and this `README.md`.
4. Commit the files.

### Option 2: Git commands
```bash
git init
git add .
git commit -m "Add AJ Detailers voice agent files"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git push -u origin main
