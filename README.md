# CallCare Portal

React + Vite call-centre app with an admin portal, a customer portal and **real voice calling**.

## Setup
Requires Node 18+ and **Chrome or Edge** (speech features).
```bash
npm install
cp .env.example .env     # Windows PowerShell: copy .env.example .env
# open .env and add ONE key: GEMINI_API_KEY (free from Google AI Studio), ANTHROPIC_API_KEY or OPENAI_API_KEY
npm run dev              # web on http://localhost:5173, AI server on :3001
```
Demo logins: admin `admin@demo.com` / `admin123`, customer `customer@demo.com` / `user123`.

## Calling (no mocks)
1. **Human to human:** WebRTC audio through PeerJS. Open the customer portal in a second window (or device) to see a call ID. In the admin **Calls** tab, enter the ID and click *Call (human to human)*. The customer's portal rings; after *Answer*, both sides talk live.
2. **AI to human:** click *Call with AI agent*. The customer portal rings; after *Answer*, the AI agent greets the customer and holds a live voice conversation (browser speech-to-text, then the LLM through `server/index.js`, then text-to-speech). The admin sees the live transcript.

Notes: calls are browser to browser, not over the phone network (a Twilio integration would be the next step). The API key stays on the server in `.env`, which is git-ignored. For two separate devices, host the app over HTTPS because browsers require it for the microphone.

## Other features
Admin dashboard (complaints by type, resolve), Caller Guide (Yes/No flowchart and final call report saved to localStorage), customer FAQ and FAQ chat assistant.

## Structure
`src/pages/` (Login, Admin, CallerGuide, CallCenter, Customer, CallPanel), `src/aiCall.js` (AI voice loop), `server/index.js` (LLM proxy), `src/data.js`, `src/store.js`.

## AI tools used
- Claude (Anthropic): used to help generate the code. The AI agent in the demo uses [Anthropic / OpenAI, edit to match your key]. Add any other tools you used.
