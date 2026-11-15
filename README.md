# AI-Powered Group Ordering System

**結合自然語言處理之群組式智慧點餐系統**  
A group ordering application integrating a web interface, LINE Bot, AI-assisted menu/order processing, and browser-based ordering assistance.

> University capstone project developed by an Information Management student team. This repository is a portfolio/code sample. External services require the repository user to provide their own credentials and configuration.

## Project Highlights

- **Group ordering:** supports shared ordering workflows and order/session handling.
- **LINE integration:** provides a LINE Bot interface for interacting with the ordering workflow.
- **AI-assisted processing:** integrates Gemini/OpenAI-compatible services for menu or order-related language/image processing, depending on local configuration.
- **Web interface:** provides the browser-based front end in `front/`.
- **Ordering assistance:** `foodpanda_order.py` uses Playwright to assist with browser-based cart operations. Login and any final confirmation/payment remain user-controlled; do not share browser profiles or account session data.
- **Cloud data integration:** the LINE Bot code uses Firebase Admin / Firestore when valid local service-account credentials are configured.

## Technology Stack

- Python, Flask
- LINE Messaging API (`line-bot-sdk`)
- Google Gemini API (`google-genai`)
- OpenAI API (`openai`)
- Firebase Admin SDK / Cloud Firestore
- Playwright
- HTML, CSS, JavaScript
- Ngrok (for local webhook development, if needed)

## Repository Structure

```text
AI-Group-Ordering-System/
├── front/
│   └── index.html             # Web front end
├── linebot/
│   ├── app.py                 # Main Flask / LINE Bot application
│   ├── app_backup.py          # Earlier backup version
│   ├── ai_agent.py            # AI menu and voice/order processing helpers
│   └── .env.example           # Environment-variable template (copy to .env)
├── foodpanda_order.py         # Playwright-based ordering assistance script
├── requirements.txt           # Python dependencies
├── .gitignore                 # Excludes local secrets and generated files
└── README.md
```

## Requirements

- Python 3.10+ recommended
- A LINE Messaging API channel (for LINE Bot features)
- Gemini and/or OpenAI API credentials for the corresponding AI features
- Firebase project and service-account JSON for Firestore-backed features
- A supported browser for Playwright (Chromium can be installed as a fallback)

## Setup

1. Clone this repository and open the project directory.
2. Create and activate a virtual environment (recommended):

   ```bash
   python -m venv .venv
   ```

   Windows PowerShell:

   ```powershell
   .\.venv\Scripts\Activate.ps1
   ```

   macOS / Linux:

   ```bash
   source .venv/bin/activate
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Copy `linebot/.env.example` to `linebot/.env` and fill in your own credentials. Never commit `linebot/.env`.

   Windows PowerShell:

   ```powershell
   Copy-Item linebot/.env.example linebot/.env
   ```

5. If using Firebase/Firestore, place your own service-account JSON in the local `linebot/` directory (for example, `linebot/serviceAccountKey.json`) and set `FIREBASE_CREDENTIALS_PATH=serviceAccountKey.json` in `linebot/.env`. The JSON credential file is excluded from Git.

6. If using Playwright's bundled Chromium:

   ```bash
   playwright install chromium
   ```

## Environment Variables

See `linebot/.env.example` for the complete template. Common settings include:

- `LINE_CHANNEL_ACCESS_TOKEN`
- `LINE_CHANNEL_SECRET`
- `GEMINI_API_KEY`
- `GEMINI_VOICE_API_KEY`
- `OPENAI_API_KEY`
- `LIFF_ID`
- `LIFF_URL_BASE`
- `FIREBASE_CREDENTIALS_PATH`

Only add credentials that you own and are authorized to use. Keep all real keys, service-account JSON files, cookies, and browser profiles on your local machine.

## Run the LINE Bot / Web Application

From the repository root, run:

```bash
python linebot/app.py
```

Configure your LINE webhook URL and LIFF settings in your own LINE Developers Console and local environment. For local webhook testing, a tunneling service such as Ngrok may be used.

## Run the Foodpanda Browser-Assistance Script

`foodpanda_order.py` is a local browser automation helper. It may use a local Playwright browser profile to preserve the user's sign-in state. That profile is stored outside the repository by default and must never be uploaded or shared.

For available command-line options, run:

```bash
python foodpanda_order.py --help
```

If the script requires OpenAI assistance, configure `OPENAI_API_KEY` in `linebot/.env` or in your local environment. Review all cart contents yourself. Any final order confirmation and payment should remain under the account holder's direct control and comply with the service's terms.

## Security Notes

- Never commit `.env`, API keys, LINE channel secrets/tokens, Firebase service-account JSON, real user/order data, browser cookies, or Playwright profiles.
- The repository's `.gitignore` excludes common secret, credential, cache, and generated-data paths. Always review the **Changes** tab in GitHub Desktop before committing.
- If a credential was ever committed, deleting the file in a later commit is not enough: revoke/rotate that credential immediately and remove it from Git history before making the repository public.
- This repository does not include production credentials. Each user must configure their own services.

## Project Context

This project was created as an Information Management capstone project to explore how AI, natural-language interaction, messaging platforms, and database services can support collaborative food ordering.
