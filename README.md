# Watchtower Quant Brain

MetaTrader 5 gives you a terminal and an Expert Advisor. What it does not give you is a brain in front of that EA. You set a watchlist, then spend the session guessing which pair deserves attention while indicators disagree and risk rules live only in your head. That is the gap.

Watchtower Quant Brain is the supervised cockpit for that job: a command centre that ranks the markets you care about, gates signals before anything reaches the broker, and puts an MT5 Expert Advisor on Mac and Windows as the hands that execute what you clear. You set the watchlist and the policy. The dashboard shows rank, signal context, and system status. The EA is how a cleared signal reaches MetaTrader 5. It is not a broker, an investment adviser, or a substitute for your judgment.

Market losses and conditions are not controlled by us, but the strategies are tested and trusted by traders all around the world and used daily by them.

## Live demo

- App: [https://watch-five-lovat.vercel.app](https://watch-five-lovat.vercel.app)
- Narrated walkthrough: [https://streamable.com/2rt97r](https://streamable.com/2rt97r)

## MT5 Expert Advisor (core sell)

The MetaTrader 5 bridge is not optional. Customers run the Expert Advisor in their own terminal or VPS on **Mac and Windows**. The Go engine ranks and gates; the EA is the execution path to the broker. Auto-trade stays off until the trader turns it on. Paper mode lets you rehearse without live orders.

## SOC / IDS

Watchtower ships with an in-house security operations layer: login and attack-event logging, detection rules, alert routing, and an access-controlled review console. It is built to watch the product itself (auth abuse, injection attempts, suspicious sessions), not as a general market-data feed.

## Architecture

```mermaid
flowchart LR
  Trader[Trader] --> Web[Next.js web app\nVercel]
  Web --> Go[Go worker engine\nRender]
  Go --> EA[MT5 Expert Advisor\nMac and Windows]
  EA --> Broker[Broker / MT5]
  Go --> DB[(Supabase Postgres\nRLS)]
  Web --> DB
  SOC[SOC / IDS] --> Go
  SOC --> Web
```

More detail: [docs/architecture.md](docs/architecture.md).

## Pages

Each page below is a dedicated screenshot of the live app.

### Home

The public landing page introduces the MT5 expert advisor, the AI risk gate, and the in-house SOC/IDS, with monthly plans and a four-step setup path.

![Home](media/screenshots/home.png)

### Pricing

The pricing page lists the Starter, Pro and Scale monthly signal allowances and how to contact the operator to set a plan up.

![Pricing](media/screenshots/pricing.png)

### About

The about page describes Watch as research and alert software, and outlines the EA, the risk gate, and the trading SOC/IDS.

![About](media/screenshots/about.png)

### FAQ

The FAQ answers common questions about signals, paper versus live mode, EA install, and what the scanner status labels mean.

![FAQ](media/screenshots/faq.png)

### Contact

The contact form is how traders ask for a plan, setup help, or other support. It asks people not to send passwords or API keys.

![Contact](media/screenshots/contact.png)

### Sign in

The sign-in page is the gate to a private workspace.

![Sign in](media/screenshots/login.png)

### Create account

The create-account page starts a new Watch account. Plans are arranged after signup, not paid on this form.

![Create account](media/screenshots/signup.png)

### Privacy

The privacy notice explains what account, security, and support data the service keeps and why.

![Privacy](media/screenshots/privacy.png)

### Terms

The terms of service set out plan allowances, provider and broker responsibilities, and limits on use.

![Terms](media/screenshots/terms.png)

### Refunds

The cancellation and refunds page explains prepaid periods, unused allowances, and consumer rights.

![Refunds](media/screenshots/refunds.png)

### Cookies

The cookies page lists the first-party sign-in and device cookies the site uses, with no advertising cookies.

![Cookies](media/screenshots/cookies.png)

### Disclaimer

The risk disclosure states that trading can lose money and that software and AI analysis do not guarantee returns.

![Disclaimer](media/screenshots/disclaimer.png)

### Reset password

The reset-password page sends a reset link to the account email.

![Reset password](media/screenshots/reset-password.png)

### Verify email

The verify-email page is the confirmation step after signup, before a bridge key can be issued.

![Verify email](media/screenshots/verify-email.png)

### Dashboard

The account dashboard shows plan status, signal allowance, and the path into the web workspace or the full command centre.

![Dashboard](media/screenshots/dashboard.png)

### Omni-Scanner (web workspace)

The web Omni-Scanner ranks configured symbols and labels research-only rows that are not live signals.

![Omni-Scanner web workspace](media/screenshots/scanner.png)

### Omni-Scanner (command centre)

Omni-Scanner in the full command centre ranks public research candidates across the configured universe.

![Omni-Scanner command centre](media/screenshots/omni.png)

### Analysis

The analysis page shows a research-only chart, indicators, and a verdict for a selected symbol.

![Analysis](media/screenshots/analysis.png)

### Signals

The AI-confirmed delivery queue. Broker delivery needs fresh broker evidence.

![Signals queue](media/screenshots/signals.png)

### Backtest

The strategy backtester form, shown with default research-only settings and no run started.

![Backtest](media/screenshots/backtest.png)

### System

The system diagnostics page reports engine health, AI and MT5 bridge status, and server version.

![System](media/screenshots/system.png)

## Tech stack

| Layer | Choice |
| --- | --- |
| Web | Next.js / TypeScript on Vercel |
| Engine | Go worker on Render |
| Data | Supabase Postgres with row-level security |
| Execution | MetaTrader 5 Expert Advisor (Mac and Windows) |
| Security | In-house SOC / IDS, account hardening, AI prompt guards |

## This repository

This is a **public showcase**: README, architecture notes, and screenshots only. It is not the product source tree. The private application repository stays private. No API keys, PINs, environment files, strategy source, or EA source are published here.

## Disclaimer

Software and signals can fail. Market data may be delayed, incomplete, or wrong. Past behaviour is not a promise of future results. You trade with your own capital and your own judgment.
