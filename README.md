# Mailchk Zapier Integration

Connect Mailchk email validation to 5,000+ apps with Zapier.

## Overview

The Mailchk Zapier integration allows you to automatically validate email addresses from any Zapier-connected app. Validate emails from form submissions, CRM entries, spreadsheets, and more.

## Installation

1. Log in to your [Zapier account](https://zapier.com)
2. Search for "Mailchk" in the app directory
3. Connect your Mailchk account using your API key
4. Start building Zaps!

## Available Actions

### Validate Email

Validate a single email address and get detailed results.

**Input Fields:**
- `Email` (required) - The email address to validate

**Output Fields:**
- `valid` - Whether the email is valid (true/false)
- `disposable` - Whether it's a disposable email (true/false)
- `mx_valid` - Whether domain has MX records (true/false)
- `risk` - Risk level (low, medium, high, critical)
- `risk_score` - Risk score from 0-100
- `domain` - The email domain
- `reason` - Reason if invalid
- `suggestion` - Suggested correction for typos

### Check Disposable

Quick check if an email is from a disposable provider.

**Input Fields:**
- `Email` (required) - The email address to check

**Output Fields:**
- `is_disposable` - Whether the email is disposable (true/false)

## Example Zaps

### 1. Validate Form Submissions

**Trigger:** New form submission (Typeform, Google Forms, etc.)
**Action:** Mailchk - Validate Email
**Filter:** Only continue if valid = true AND disposable = false
**Action:** Add to CRM or email list

### 2. Clean Email Lists

**Trigger:** New row in Google Sheets
**Action:** Mailchk - Validate Email
**Action:** Update row with validation results

### 3. Lead Qualification

**Trigger:** New HubSpot contact
**Action:** Mailchk - Validate Email
**Filter:** Block if risk = high or risk = critical
**Action:** Update contact with risk score

### 4. E-commerce Fraud Prevention

**Trigger:** New Shopify order
**Action:** Mailchk - Validate Email
**Action:** Flag order if disposable = true

## Setup Guide

### Step 1: Get Your API Key

1. Log in to [Mailchk](https://mailchk.io)
2. Go to Settings > API Keys
3. Copy your API key

### Step 2: Connect to Zapier

1. In Zapier, search for "Mailchk"
2. Click "Connect"
3. Paste your API key
4. Click "Yes, Continue"

### Step 3: Build Your Zap

1. Choose your trigger app (e.g., Google Forms)
2. Add Mailchk as an action
3. Select "Validate Email"
4. Map the email field from your trigger
5. Add filters or additional actions based on results

## Best Practices

### Use Filters Wisely

Add a Filter step after Mailchk to route emails based on validation results:

```
Only continue if:
- valid equals true
- AND disposable equals false
- AND risk does not equal critical
```

### Store Validation Results

Save validation results back to your source for future reference:

- Update the original record with risk score
- Add tags for disposable or high-risk emails
- Create a separate log of all validations

### Handle Failures Gracefully

Add a Paths step to handle different outcomes:

- **Path A:** Valid email → Continue processing
- **Path B:** Invalid email → Send notification
- **Path C:** Disposable email → Flag for review

## Rate Limits

- Zapier polls run according to your Zapier plan
- Each validation counts against your Mailchk quota
- Consider using filters before Mailchk to reduce validations

## Troubleshooting

### "Invalid API Key" Error

1. Check that your API key is correct
2. Ensure there are no extra spaces
3. Verify your Mailchk account is active

### "Rate Limit Exceeded" Error

1. Check your Mailchk usage dashboard
2. Consider upgrading your plan
3. Add delays between Zap runs

### Validation Not Working

1. Ensure the email field is properly mapped
2. Check that the email format is valid
3. Test with a known good email address

## Support

- Mailchk Docs: https://mailchk.io/docs
- Zapier Help: https://zapier.com/help
- Contact: support@mailchk.io
