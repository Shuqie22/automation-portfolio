# Sales Lead Automation Pipeline

## What This Project Does

This workflow automatically captures, scores, and manages sales leads without any manual work. When a potential client fills out a contact form, the entire process of recording their details, scoring their inquiry with AI, adding them to a CRM, and notifying the sales team happens in under 10 seconds — completely automatically.

## The Problem It Solves

Without automation, a sales team has to manually read every inquiry, decide how urgent it is, add the contact to their CRM, update their tracking spreadsheet, and notify the right person. This takes time, introduces human error, and means hot leads sometimes get missed. This pipeline eliminates all of that.

## How It Works

A potential client submits a Google Form with their name, email, company name, and what they need help with. The moment they submit, n8n receives the data instantly through a webhook trigger. n8n then sends the lead details to Google Gemini AI, which reads the inquiry and returns a structured score from 1 to 10, a category of Hot, Warm, or Cold, a reason for the score, and a suggested next action. That AI response is parsed and passed simultaneously to three destinations. First, a contact is created in HubSpot CRM with the lead status set automatically based on the AI score. Second, all the lead details and AI analysis are logged into a Google Sheet for record keeping and reporting. Third, a formatted HTML email is sent to the sales team with the full lead profile and AI recommendation.

## Tools Used

All tools in this project use free tiers only, making it accessible to any business without upfront cost.

- **n8n** (self-hosted, free) : the automation engine that connects everything together
- **Google Forms** (free) : the lead capture form that triggers the pipeline
- **Google Gemini API** (free tier) : the AI that scores and categorises each lead
- **HubSpot CRM** (free tier) : where contacts are stored and managed
- **Google Sheets** (free) : the master log of all leads and their scores
- **Gmail** (free) : sends the notification email to the sales team

## Workflow Structure

The workflow runs in this exact order. The Webhook node listens for Google Form submissions and receives the lead data. The HTTP Request node sends the lead details to Gemini AI for scoring. The Code node parses the AI response and extracts the structured fields. The HubSpot node creates or updates the contact in the CRM. The Google Sheets node logs everything to the spreadsheet. The Gmail node sends the notification email. The Respond to Webhook node sends a success response back to the form so the submitter sees a confirmation.

## Screenshot
![Workflow Screenshot](https://github.com/user-attachments/assets/fa5752f4-a349-431f-8ddc-f898bf399431)

## How to Set It Up

To run this workflow yourself you will need an n8n instance running locally or on a server, a Google Cloud project with the Gemini API enabled, a HubSpot free account with a private app token, a Google Sheet with the headers Date, Name, Email, Company, Inquiry, Score, Category, Reason, Suggested Action, and a Gmail account connected to n8n via OAuth2.

Import the workflow JSON file into n8n, replace the API keys and Sheet ID with your own values, activate the webhook, and connect your Google Form to the webhook URL using Google Apps Script.
