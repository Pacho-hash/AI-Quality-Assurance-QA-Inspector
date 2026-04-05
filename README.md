# 📦 AI Quality Assurance (QA) Inspector

An automated, serverless computer vision pipeline built with **n8n** that allows warehouse workers and QA inspectors to log product or package damage instantly just by snapping a photo in Telegram. 

Powered by **Google Gemini 2.5 Vision AI**, this workflow automatically analyzes the image, categorizes the damage, summarizes the issue, and logs the structured data into a Google Sheet (acting as an ERP/Database) before instantly replying to the worker.

## ✨ Features
* **Frictionless Reporting:** Workers don't need to type anything. Just send a photo to the Telegram bot.
* **Automated AI Inspection:** Uses Google Gemini Vision to accurately assess the image and output structured JSON.
* **Automated Data Entry:** Automatically logs the Report ID, Timestamp, Damage Category, and AI Summary into a Google Sheet.
* **Instant Feedback:** The bot replies to the worker in seconds with a confirmation and the AI's assessment.

## 🛠️ Architecture Flow
1. **Telegram Trigger:** Listens for incoming photos sent to your Bot.
2. **Download Image:** Pulls the high-resolution binary image data from Telegram's servers.
3. **Base64 Converter (Code Node):** Converts the binary file into a base64 string so the AI can read it.
4. **Gemini Vision Analysis:** Sends the prompt and image to Google Gemini. Gemini replies with a structured JSON assessment.
5. **Google Sheets:** Parses the AI's markdown/JSON output and appends a new row to your database.
6. **Telegram Reply:** Sends a clean, formatted success message back to the worker.

---

## 📋 Prerequisites
To run this workflow, you will need:
1. **[n8n](https://n8n.io/)** (Cloud or Self-hosted).
2. **Telegram Bot Token** (Create a free bot via [@BotFather](https://t.me/botfather) on Telegram).
3. **Google Gemini API Key** (Get one free from [Google AI Studio](https://aistudio.google.com/)).
4. **Google Sheets Account** (To store the output data).

---

## 🚀 Installation & Setup

### 1. Set up your Google Sheet
Create a new Google Sheet and add the following headers to the first row (A1 to D1):
* `Report ID`
* `Date`
* `Damage Category`
* `AI Summary`

### 2. Import the Workflow into n8n
1. Open your n8n workspace.
2. Go to **Workflows** -> **Add Workflow**.
3. Click the `...` menu in the top right and select **Import from File** (or simply copy the contents of the `workflow.json` file in this repo and paste it directly onto your n8n canvas).

### 3. Configure Credentials
You will see several nodes requiring credentials. Click on each and connect your accounts:
* **Telegram Trigger & Download Image nodes:** Add your Telegram Bot Token.
* **Save to Database (Google Sheets) node:** Connect your Google account and select the Sheet you created in Step 1.
* **Telegram Reply node:** Select the same Telegram credential you used for the trigger.

### 4. Add your Gemini API Key
1. Double-click the **Gemini Vision Analysis** HTTP Request node.
2. In the **URL** field, replace `YOUR_GEMINI_API_KEY_HERE` with your actual Google Gemini API Key.

### 5. Activate
Toggle the workflow to **Active** in the top right corner of n8n.

---

## 📱 How to Use
1. Open Telegram and start a chat with your Bot.
2. Take a photo of a box, package, or product (damaged or intact).
3. Send the photo to the bot.
4. Wait ~3 seconds. 
5. The bot will reply with the categorized damage, and the data will instantly appear in your Google Sheet!

---

## 📄 License
MIT License

Copyright (c) 2026 Pacho-hash

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software.
