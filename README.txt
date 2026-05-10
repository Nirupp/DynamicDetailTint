═══════════════════════════════════════════════════════════════
  DYNAMIC DETAILING & TINT — Website Package
  Built May 2026
═══════════════════════════════════════════════════════════════

FILES INCLUDED:
───────────────────────────────────────────────────────────────

1. dynamic-detailing-v3.html  ← MAIN PUBLIC WEBSITE
   - Full public-facing website matching logo theme
   - All 7 service menus with real Urable pricing
   - Window Tinting, Ceramic, Commercial, Detailing,
     Add-Ons, Gift Cards, Maintenance
   - Hero, About, Gallery, Reviews, Contact sections
   - "Book a Service" buttons link to dynamic-booking.html

2. dynamic-booking.html  ← CUSTOMER BOOKING SYSTEM
   - 5-step booking flow (no redirect to Urable)
   - Collects: service, vehicle, contact info, date/time
   - Generates unique Booking ID (e.g. DDT-LX8K4A)
   - Sends confirmation SMS + Email to customer
   - Notifies admin via SMS + Email
   - Admin dashboard triggers "Job Complete" → customer notified
   - 1-year maintenance reminder auto-scheduled

3. dynamic-detailing.html  ← INTERNAL BUSINESS DASHBOARD
   - Staff clock in / clock out
   - Job management with status tracking
   - Inventory with low-stock alerts
   - QuickBooks, Stripe, Carfax, SMS sections
   - Reminders and quotes builder

═══════════════════════════════════════════════════════════════
  TO GO LIVE — BOOKING SYSTEM SETUP
═══════════════════════════════════════════════════════════════

Open dynamic-booking.html and find the CONFIG block:

  SENDGRID_API_KEY:    → Paste your SendGrid API key
  FROM_EMAIL:          → Your verified SendGrid sender email
  ADMIN_EMAIL:         → Where admin notifications go
  TWILIO_ACCOUNT_SID:  → Paste your Twilio Account SID
  TWILIO_AUTH_TOKEN:   → Paste your Twilio Auth Token
  TWILIO_FROM_NUMBER:  → Your Twilio phone number (+1410...)

Then uncomment the 3 fetch() blocks inside sendSMS() and sendEmail().

─────────────────────────────────────────────────────────────
  ADMIN DASHBOARD → MARK JOB DONE
─────────────────────────────────────────────────────────────

From your internal dashboard, call:

  BookingBridge.jobComplete('DDT-XXXXXX')

This will:
  ✓ Send customer an SMS: "Your car is ready for pickup!"
  ✓ Send customer a job-complete email
  ✓ Schedule a 1-year SMS + email reminder automatically

─────────────────────────────────────────────────────────────
  1-YEAR REMINDER (Production)
─────────────────────────────────────────────────────────────

For production, replace the setTimeout in _scheduleReminder()
with a server-side call:

  POST /api/schedule-reminder
  Body: { bookingId, sendAt: "2027-05-09T10:00:00Z" }

Your backend (Node.js, etc.) fires Twilio + SendGrid on that date.

═══════════════════════════════════════════════════════════════
  CONTACT
═══════════════════════════════════════════════════════════════

Dynamic Detailing & Tint
395 Mt Vernon Ave, Odenton, MD 21113
(410) 674-2430
dynamicmdetailing.com

