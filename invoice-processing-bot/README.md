# Invoice Processing Bot

## What This Project Does

This workflow automatically detects invoice emails in Gmail, uses AI to extract the key financial details, and logs everything into both a Notion database and Google Sheets — sending budget alerts when invoices exceed a set threshold. No manual data entry, no missed invoices, no spreadsheet updating by hand.

## The Problem It Solves

Most small businesses and freelancers receive invoices by email and then manually copy the vendor name, amount, date, and category into a spreadsheet or accounting tool. This is slow, error-prone, and easy to forget. This bot watches your inbox and handles all of that automatically the moment an invoice arrives.

## How It Works

Make.com watches your Gmail inbox every 15 minutes for any unread email with the word Invoice in the subject line. When it finds one, it sends the email subject and body to Google Gemini AI and asks it to extract four key fields: the vendor name, the invoice amount, the invoice date, and the expense category. Gemini returns these details as a structured JSON object. Make.com then parses that JSON and simultaneously creates a new entry in the Notion Invoice Tracker database and adds a row to a Google Sheet. A Router module then checks the amount. If it is over $200 a budget alert email is sent immediately. If it is $200 or under a simple confirmation email is sent instead so there is always a record of what was processed.

## Tools Used

All tools in this project use free tiers only.

- **Make.com** (free tier) - the automation platform that orchestrates the entire workflow
- **Gmail** (free) - the email account being monitored for invoices
- **Google Gemini API** (free tier) - the AI that reads and extracts data from invoice emails
- **Notion** (free tier) - the visual invoice tracker database
- **Google Sheets** (free) - the backup spreadsheet log of all invoices
- **Make.com Router** (built-in) - handles conditional logic for budget alerts

## Workflow Structure

The scenario runs in this order. The Gmail Watch Emails module triggers when a new unread email with Invoice in the subject arrives. The HTTP module sends the email content to Gemini AI with a prompt asking for structured extraction. The JSON Parse module converts Gemini's text response into usable data fields. The Notion Create Database Item module writes a new row to the Invoice Tracker. The Google Sheets Add a Row module logs the same data as a backup. The Router module checks the amount and routes to either the Budget Alert email for amounts over $200 or the Confirmation email for amounts at or below $200.

## Screenshot
![Workflow Screenshot](https://github.com/user-attachments/assets/ff64316f-d27e-4a1c-9ada-e7ba61c020cc)

## How to Set It Up

To run this workflow yourself you will need a Make.com account, a Gmail account connected to Make.com via Google OAuth, a Google Gemini API key from Google AI Studio, a Notion account with an internal integration token and a database called Invoice Tracker with columns for Invoice, Date, Vendor, Amount, Category, and Status, and a Google Sheet with matching column headers.

Import the blueprint JSON into Make.com, connect your credentials to each module, update the Notion database ID and Google Sheet ID with your own values, and activate the scenario.
