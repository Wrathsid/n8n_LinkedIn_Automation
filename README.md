Automated LinkedIn Content Publisher with n8n
This project provides a powerful n8n workflow that automates the entire process of creating and publishing content on LinkedIn. It uses a Google Sheet as a content queue, leverages the Google Gemini API to intelligently generate post copy, publishes it to your LinkedIn profile, and updates the sheet to track your posts.

## ✨ Features

Dynamic Content Queue: Fetches post topics directly from a Google Sheet.

AI-Powered Content Generation: Uses the Google Gemini API to write insightful and human-like posts based on your topics.

Automated Publishing: Posts the generated content directly to your personal LinkedIn profile.

Status Tracking: Updates the Google Sheet to mark topics as "Posted" and adds a timestamp, preventing duplicate posts.

Scalable & Customizable: Easily modify the AI prompt, add more steps, or change the trigger to a schedule.

⚙️ How It Works
The workflow follows a simple but effective logic:

Trigger: The process starts manually when you execute the workflow.

Fetch Topic: It connects to a specified Google Sheet and finds the first row where the Status column is marked as "Not Posted".

Generate Content: The topic from that row is sent to the Google Gemini Chat Model. An AI Agent node uses a detailed prompt to craft a high-quality LinkedIn post.

Publish to LinkedIn: The AI-generated text is then published as a new post on your connected LinkedIn account.

Update Sheet: Finally, the workflow goes back to the Google Sheet, changes the Status of the topic to "Posted", and logs the current date and time in the Posted At column.

📋 Prerequisites
Before you begin, ensure you have the following:

A running n8n instance (either on n8n.cloud or self-hosted).

A Google Account with access to Google Sheets.

A Google Gemini API Key. You can get one from Google AI Studio.

A LinkedIn Account.

🚀 Setup Instructions
Follow these steps to get your automation up and running.

Step 1: Set Up Your Google Sheet
Create a new Google Sheet.

Name the first three columns exactly as follows: Topic, Status, and Posted At.

Add some post ideas under the Topic column.

For each topic you want to post, set the Status column to Not Posted.

Topic	Status	Posted At
The future of Web Dev	Not Posted	
My favorite VSCode extension	Not Posted	
Why I use n8n for automation	Posted	9/20/2025

Export to Sheets
Step 2: Import the n8n Workflow
Download the My workflow 4.json file you provided.

In your n8n instance, click Import from File and select the JSON file to add the workflow to your canvas.

Step 3: Configure Node Credentials
You will need to connect your accounts to n8n.

Google Sheets Node (Get row(s) in sheet):

In the Credentials section, select your Google Account or create a new credential by authenticating with Google (using OAuth2).

Google Gemini Chat Model Node:

In the Credentials section, create a new "Google PaLM API" credential and paste in your Gemini API key.

LinkedIn Node (Create a post):

In the Credentials section, create a new credential by authenticating with your LinkedIn account (using OAuth2).

Google Sheets Node (Update row in sheet):

Select the same Google Sheets credential you created in the first step.

Step 4: Configure Node Parameters
Get row(s) in sheet:

Select your credential.

In the Document ID field, choose your Google Sheet from the list.

In the Sheet Name field, select the correct sheet.

Ensure the filter is set to find rows where Status is Not Posted.

Update row in sheet:

Select the same Google Sheet and sheet name as above.

Under Columns, ensure the mapping is set to update the Status field to Posted and the Posted At field to {{ $now }}.

Make sure Topic is set as the Matching Column to identify the correct row to update.

🏃‍♀️ Usage
Add new ideas to your Google Sheet with the status Not Posted.

Open your workflow in n8n and click Execute Workflow.

Watch as your post is written and published automatically!

Pro Tip: To make this a fully "set-it-and-forget-it" system, replace the When clicking ‘Execute workflow’ node with a Cron node to run it on a schedule (e.g., once every day).
