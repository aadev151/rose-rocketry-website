# EmailJS Setup Guide

This guide will help you set up EmailJS to automatically send contact form emails to `hello@example.com` (or your preferred email).

## Step 1: Create EmailJS Account

1. Go to [https://www.emailjs.com/](https://www.emailjs.com/)
2. Sign up for a free account
3. Verify your email address

## Step 2: Add Email Service

1. In your EmailJS dashboard, go to **Email Services**
2. Click **Add New Service**
3. Choose your email provider (Gmail, Outlook, etc.)
4. Follow the setup instructions for your provider
5. Note down your **Service ID** (e.g., `service_abc123`)

## Step 3: Create Email Template

1. Go to **Email Templates** in your dashboard
2. Click **Create New Template**
3. Use this template content:

```
Subject: New Contact Form Submission - {{subject}}

From: {{from_name}} ({{from_email}})
Subject: {{subject}}

Message:
{{message}}

---
This email was sent from the Rose Rocketry website contact form.
```

4. Save the template and note down your **Template ID** (e.g., `template_xyz789`)

## Step 4: Get Your Public Key

1. Go to **Account** → **General**
2. Find your **Public Key** (e.g., `user_abc123def456`)

## Step 5: Update the Website Code

Replace the placeholder values in `script.js`:

```javascript
// Line 67: Replace YOUR_PUBLIC_KEY
emailjs.init("YOUR_PUBLIC_KEY"); // Replace with your actual public key

// Line 100: Replace YOUR_SERVICE_ID and YOUR_TEMPLATE_ID
emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', {
    from_name: data.name,
    from_email: data.email,
    subject: data.subject,
    message: data.message,
    to_email: 'hello@example.com' // Change this to your actual email
})
```

## Step 6: Test the Form

1. Open your website
2. Fill out the contact form
3. Submit it
4. Check your email inbox for the message

## Example Configuration

Here's what your updated code should look like:

```javascript
// Initialize EmailJS
(function() {
    emailjs.init("user_abc123def456"); // Your actual public key
})();

// In the form submission:
emailjs.send('service_gmail123', 'template_contact456', {
    from_name: data.name,
    from_email: data.email,
    subject: data.subject,
    message: data.message,
    to_email: 'rose.rocketry@rose-hulman.edu' // Your actual email
})
```

## Free Tier Limits

- **200 emails per month** (free tier)
- **2 email services**
- **2 email templates**

This should be more than enough for a club website!

## Troubleshooting

- **"EmailJS is not defined"**: Make sure the EmailJS script is loaded before your JavaScript
- **"Service not found"**: Double-check your Service ID
- **"Template not found"**: Double-check your Template ID
- **Emails not received**: Check spam folder and verify email service setup

## Alternative: Simple Form Backend

If you prefer not to use EmailJS, you could also:

1. Use a service like Formspree, Netlify Forms, or FormSubmit
2. Set up a simple backend with Node.js and Nodemailer
3. Use a serverless function (Vercel, Netlify Functions)

EmailJS is the easiest option for a static website with no backend!
