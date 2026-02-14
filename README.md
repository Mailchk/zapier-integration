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
- `scam_domain` - Whether the domain is flagged as scam/phishing (true/false)
- `mx_exists` - Whether domain has MX records (true/false)
- `blacklisted_mx` - Whether MX server IPs are on a DNSBL blacklist (true/false)
- `free_email` - Whether it's a free email provider (true/false)
- `risk_score` - Risk level (low, medium, high, critical)
- `risk_factors` - List of risk factors detected
- `deliverability_score` - Deliverability likelihood score (0-100)
- `domain` - The email domain
- `email_provider` - Detected provider name (e.g. Gmail, Outlook)
- `spf` - SPF authentication result (pass, fail, none)
- `dmarc` - DMARC policy result (pass, fail, none)
- `normalized_email` - Email after provider-specific normalization
- `is_aliased` - Whether the email uses aliasing (true/false)
- `alias_type` - Type of alias (plus_addressing, dot_variation, subdomain_addressing, provider_alias)
- `did_you_mean` - Suggested correction for domain typos
- `reason` - Human-readable explanation (when applicable)

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
**Filter:** Only continue if valid = true AND disposable = false AND scam_domain = false
**Action:** Add to CRM or email list

### 2. Clean Email Lists

**Trigger:** New row in Google Sheets
**Action:** Mailchk - Validate Email
**Action:** Update row with validation results (risk_score, deliverability_score, spf, dmarc)

### 3. Lead Qualification

**Trigger:** New HubSpot contact
**Action:** Mailchk - Validate Email
**Filter:** Block if risk_score = high or risk_score = critical
**Action:** Update contact with deliverability_score and risk_score

### 4. E-commerce Fraud Prevention

**Trigger:** New Shopify order
**Action:** Mailchk - Validate Email
**Action:** Flag order if disposable = true OR scam_domain = true

### 5. Detect Email Aliasing

**Trigger:** New user signup
**Action:** Mailchk - Validate Email
**Filter:** Check if is_aliased = true
**Action:** Log the normalized_email and alias_type for duplicate detection

## Setup Guide

### Step 1: Get Your API Key

1. Log in to [Mailchk](https://mailchk.io)
2. Go to Dashboard > API Keys
3. Create and copy your API key

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
- AND scam_domain equals false
- AND risk_score does not equal critical
```

### Store Validation Results

Save validation results back to your source for future reference:

- Update the original record with risk_score and deliverability_score
- Add tags for disposable, scam, or high-risk emails
- Store SPF/DMARC results for domain reputation tracking
- Log normalized_email for alias deduplication

### Handle Failures Gracefully

Add a Paths step to handle different outcomes:

- **Path A:** Valid email → Continue processing
- **Path B:** Invalid email → Send notification
- **Path C:** Disposable or scam email → Flag for review
- **Path D:** Low deliverability_score → Route to manual review

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
