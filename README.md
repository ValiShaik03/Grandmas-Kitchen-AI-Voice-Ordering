# Grandma's Kitchen — AI Voice Ordering & Payment Automation

A Telugu-first AI voice ordering system that allows customers to place food orders through a natural conversational voice agent and automates order validation, Razorpay payment-link generation, Google Sheets order tracking, payment-status updates, and Telegram notifications.

## 🚀 Project Overview

Grandma's Kitchen is an AI-powered ordering workflow designed for a small food business.

The system combines conversational AI with workflow automation and payment APIs to create an end-to-end digital ordering experience.

### Customer Flow

Customer speaks with the AI agent → selects products → provides quantity → provides customer details → confirms the order → receives a Razorpay payment link.

### Business Flow

Order received → validated by n8n → payment link generated → order stored in Google Sheets → payment completed → Razorpay webhook received → order marked as PAID → Telegram notification sent to the business owner.

---

## 🏗️ System Architecture

```text
                    ┌──────────────────────┐
                    │      Customer        │
                    │   Telugu Voice Call  │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ ElevenLabs AI Agent  │
                    │ Telugu Conversation  │
                    └──────────┬───────────┘
                               │
                        Confirmed Order
                               │
                               ▼
                    ┌──────────────────────┐
                    │     n8n Webhook      │
                    │   Order Processing   │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │    Order Validation  │
                    │ Name / Phone / Order │
                    │ Location / Amount    │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │       Razorpay       │
                    │   Payment Link API   │
                    └──────────┬───────────┘
                               │
                         Payment Link
                               │
                 ┌─────────────┴─────────────┐
                 ▼                           ▼
       ┌─────────────────┐         ┌─────────────────┐
       │  Google Sheets  │         │ ElevenLabs Agent│
       │ Order Tracking  │         │ Customer Reply  │
       └─────────────────┘         └─────────────────┘

                    Customer completes payment
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Razorpay Webhook     │
                    │ payment_link.paid    │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Update Google      │
                    │   Sheets → PAID      │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Telegram Notification│
                    │ Business Owner Alert │
                    └──────────────────────┘
