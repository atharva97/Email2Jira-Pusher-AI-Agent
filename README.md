# 📬 Email2Jira Pusher AI Agent

A no-code automation built with **n8n** that:

1. Scans your Gmail inbox  
2. Uses an LLM (via OpenAI, OpenRouter, or any provider) to detect requirement or scope changes  
3. Prevents duplicates by checking against Jira  
4. Automatically creates new Jira issues for valid, new change requests  

You only need to import the workflow and connect your accounts — no coding required.

---

## 💡 What Problem Does It Solve?

Many stakeholders send change requests through email. These are often informal and get lost in inboxes.

This AI Agent reads your emails and detects intent like:

> "Can you also include daily volume breakdowns in the report?"

It then:

- Identifies this as a scope change  
- Determines its priority  
- Automatically creates a Jira issue using the **email subject** as the title, e.g.:  
  `Can you also include daily volume breakdowns in the report?`

📝 Note: Issues will be created in the **Backlog** by default (not an active sprint).

No missed emails. No manual copy-pasting.

---

## ✅ What You Need

- __n8n__ (free, local or cloud instance)  
- __Gmail Account__ (OAuth2 setup via Google Cloud, free tier available)  
- __Jira Cloud__ (API access is free on basic plan)  
- __LLM Provider__:  
  - [OpenAI](https://platform.openai.com) (paid)  
  - [OpenRouter](https://openrouter.ai) (free options like DeepSeek, takes longer)  
  - Or any model that supports simple HTTP API requests

---

## 🛠️ How It Works

1. Runs every 5 minutes using n8n's schedule node (Can customize in the "Schedule Trigger" node)
2. Fetches latest 50 Gmail messages (Can customize in the "Gmail" node)
3. For each email:
   - Extracts subject and body  
   - Sends to your chosen LLM for natural language parsing  
   - Determines if it’s a requirement or scope update  
   - Searches Jira to avoid duplicates  
   - Creates a Jira issue if new  
   - Labels the email as `Processed-by-n8n`  
   - 📌 New issues land in your **Backlog** unless a sprint is explicitly set

---

## ⏱️ How to Change Email Scan Frequency

1. Open the workflow in n8n  
2. Click on the **Schedule Trigger** node  
3. Set **Trigger Interval** to your desired value (e.g., 10 minutes)  
4. Save and re-run the workflow

You can scan as often or rarely as you like.

---

## 🚀 Setup Instructions

1. Open your n8n instance  
2. Click **Import** and upload `Email2Jira_Pusher_AI_Agent.json`  
3. Create these credentials in n8n:
   - Gmail OAuth2 (using Google Cloud Console)  
   - Jira Software Cloud API (via your Atlassian account)  
   - HTTP Auth for your LLM (e.g., OpenRouter: `Authorization: Bearer YOUR-OPENROUTER-KEY`, [get a key](https://openrouter.ai)) 
4. Test manually, then click **Activate**

That's it — your workflow is now live and working.

---

## 🙋 FAQ

__Does this use GPT-4?__  
Only if you choose it. You can use any LLM provider like OpenAI or OpenRouter (e.g. DeepSeek, Mistral, Claude, etc.).

__Is it free to run?__  
Yes. You can:
- Use Gmail API with free Google Cloud setup  
- Use OpenRouter’s free LLMs (note: some are slow or imprecise)  
- Use Jira’s free-tier API access  
- Run n8n locally (For e.g. through Docker)

__Can I use Outlook instead of Gmail?__  
Not in this version — you’d need to modify the trigger node.

__Can I track more than requirement changes?__  
Yes — you can fine-tune the prompt in the OpenAI node to look for feature requests, risks, bugs, or anything else.

__Can I run n8n locally and modify this?__  
Yes! You can:
- Run n8n via Docker or CLI  
- Import this agent, edit it visually in n8n  
- Or download the `.json`, modify it manually or with ChatGPT/Claude, and re-import it  

---

## 📄 License

This project is released under the [MIT License](./LICENSE). Use it freely.

---
> ⚠️ **Disclaimer**  
> The Email2Jira Pusher AI Agent is provided on an “as is” and “as available” basis, for informational and educational purposes only.  
> The author makes no warranties, either express or implied, regarding the performance, accuracy, reliability, or suitability of this workflow for any particular purpose.  
>  
> By using this software, you acknowledge and agree that:  
> • You are solely responsible for how you configure and deploy the workflow in your environment.  
> • The author is not liable for any loss of data, missed communications, failed API interactions, or unintended automation outcomes.  
> • You are responsible for complying with the terms of service and acceptable use policies of any third-party APIs (such as Gmail, Jira, or OpenRouter) that this workflow interacts with.  
> • This software does not constitute professional, legal, or operational advice. It is your responsibility to verify all outputs and ensure safe, compliant usage, especially in regulated environments (e.g. finance, healthcare).  
>  
> This project is not affiliated with, endorsed by, or supported by Atlassian, Google, OpenAI, or any third-party vendor referenced in the workflow.  
>  
> **Use at your own risk.** You assume full responsibility for any consequences that may result from using this project.
---

Built with ❤️ using [n8n](https://n8n.io) and your preferred LLM.
