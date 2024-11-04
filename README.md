# PayPal Payment Workflow with Node.js/Express

This project demonstrates how to create a seamless PayPal payment workflow using Node.js and Express. It covers creating a PayPal order, redirecting users to PayPal's hosted payment page, and handling post-payment actions through webhook events.

## Project Overview

### Main Features
- Create a PayPal order and redirect users to PayPal's hosted payment page for processing.
- Listen for webhook events from PayPal to handle post-payment actions.
- Verify webhook signatures for security.
- Call additional server-side logic after a successful payment. (Optional)

## Prerequisites

- **Node.js**: Ensure Node.js is installed.
- **PayPal Account**: Sign up for a PayPal Developer account if you don't have one.
- **PayPal Developer Dashboard**: Register your application to get your Client ID and Secret.

## Setup Guide

1. ### Clone Repository:
Clone this repository to your local machine:
```bash
git clone https://github.com/FabrizioMarras/PayPal_payment.git
cd PayPal_payment
```

2. ### Install Dependencies:
Run the following command to install the required dependencies:
```bash
npm install
```

3. ### Environment Variables:
Create a .env file in the project root and add your PayPal credentials:
```bash
PAYPAL_CLIENT_ID=YourClientIDHere
PAYPAL_SECRET=YourSecretHere
RETURN_URL=http://localhost:3000/success
CANCEL_URL=http://localhost:3000/cancel
```

4. ### Start the Server:
Run the server using:
```bash
node server.js
```
The server will run at http://localhost:3000.

## Project Structure

1. ### Client Pages:
- **index.html**: Main webpage containing a button to start the payment process.
- **success.html**: Success page where the user is redirected after a successful payment.
- **cancel.html**: Cancel page where the user is redirected if they decide to cancel the payment.
- **error.html**: Optional page to handle payment errors and display appropriate messages. (Not implemented).

2. ### Client Script:
- **index.js**: Script file to handle the payment button click and call the /create-order route on the server, then handle the redirect response.

3. ### Server:
- **.env**: Environment variable file to store secret keys. Add variables such as PAYPAL_CLIENT_ID, PAYPAL_SECRET, RETURN_URL, and CANCEL_URL. (File not included in the repo).
- **server.js**: Main server file that handles routes, generates access tokens, creates orders, and processes webhooks.

## Detailed Workflow

### Creating an Order
In the /create-order route, the server receives a productId from the client and creates a PayPal order using the product details. The approval URL is sent back to the client for redirection.

### Handling Webhooks for Payment Status
The /webhook route listens for webhook events sent by PayPal, such as `CHECKOUT.ORDER.APPROVED` or `PAYMENT.CAPTURE.COMPLETED`. The webhook verifies the signature and processes the event.

### Running Webhooks Locally
For local webhook testing, use tools such as ngrok to expose your local server:
```bash
ngrok http 3000
```
Update the PayPal webhook endpoint in your PayPal Developer Dashboard with the ngrok URL to receive events.

## Security Considerations

- **Verify Webhook Signatures**: Always verify webhook signatures to ensure the request is genuinely from PayPal.
- **Environment Variables**: Keep your secret keys secure and never commit them to version control.

## Customization

### Processing Post-Payment Logic
- The processSuccessfulPayment function handles additional server-side actions, such as storing payment details or updating an order status. (Not implemented in this repo).
- Modify the processSuccessfulPayment function to include any specific post-payment processing needed for your application, such as updating user accounts, sending confirmation emails, or updating a database.

### Error Page UI Redirect
- Implement logic to redirect users to an error page if the payment fails.
- Implement logic to send an email to the user if the payment fails.

### Successful Payment Optional Functionality
- Implement a notification system to notify you and the user when a payment is successful.

## Resources

<a href='https://developer.paypal.com/api/rest/'>PayPal API Reference</a>
<a href='https://developer.paypal.com/docs/checkout/'>PayPal Checkout Integration</a>
<a href='https://developer.paypal.com/api/rest/webhooks/'>PayPal Webhooks</a>
<a href='https://ngrok.com/'>ngrok</a>

##

Please mention FM Consulting when using this code for your web application. Thank you!