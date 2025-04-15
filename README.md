# 🧾 Complaint Classifier for Au Pair Agency

This repo contains a lightweight tool that helps an au pair agency identify and categorize customer complaints, so they can report them properly to the government.

## 🧩 What's the Problem?

The agency receives tons of messages from customers (host families and au pairs). But complaints aren't labeled or categorized, and the government needs them to be reported properly.

We needed a way to:
1. Figure out which cases count as a *real complaint*
2. Assign the correct complaint reason from a government list
3. Identify who reported it (host family or au pair)
4. Do all this with minimal cost

## ✅ What This Project Does

Given an Excel file with **Subject** and **Description** columns, this script:

- Tells you if it’s a complaint (yes/no)
- If yes, it adds:
  - The complaint category
  - Who reported it (Host Family or Au Pair)

It only makes the detailed follow-up API calls for cases flagged as actual complaints to save tokens and stay cost-efficient.

## 🛠️ How It Works

- Python script using OpenAI's `gpt-4o` model
- Runs through each row in the spreadsheet
- Prompts GPT to classify and categorize
- Adds new columns with results
- Saves everything to a new Excel file

🚦 What Could Be Improved
- Prompts could be tuned for better accuracy
- Might be classifying too many things as complaints right now
- Would be fun to try this on GPT-4.1 to see if we get better results
- Add a web-based UI later (e.g., Streamlit)

💬 Notes on API Usage
- I initially thought we’d hit OpenAI's token-per-minute limits on the real file that had more than 9700 rows
- Each row (subject + description + prompt) is ~625 tokens. At 60 requests/min, we’re using only ~37,500 tokens/min — below the GPT-4o limit of 30000 TPM.
- Also, we only ask for complaint reason and reporter if the case is actually flagged as a complaint, which saves extra requests.


⚙️ Requirements:
- Python 3.10+
- OpenAI API key
- `openai`, `pandas`, `openpyxl`, `presidio-analyzer`, and `presidio-anonymizer`
