# Architecture (showcase)

High-level shape of Watchtower Quant Brain. This document describes boundaries, not implementation details or strategy rules.

## Layers

1. **Web app (Next.js on Vercel)**  
   Accounts, plan requests, authenticated dashboard, and the public marketing surface. The browser talks to the web app; the web app proxies to the engine with shared edge signing. Customers do not get raw engine credentials in the page.

2. **Go worker engine (Render)**  
   Ranking, risk gates, paper vs live mode, bridge commands, and SOC event handling. Analysis can use public research candles without a broker connection; execution still needs the MT5 bridge and fresh broker evidence.

3. **MetaTrader 5 Expert Advisor**  
   Runs inside the customer’s MT5 terminal on Mac or Windows (or a VPS). It reports account and market state to the engine and carries out cleared commands. Auto-trade defaults off. The cloud UI alone does not place broker orders.

4. **Supabase Postgres**  
   Tenants, subscriptions, and encrypted account state under row-level security. Subscription delivery quotas are enforced in the database, separate from request rate limits.

5. **SOC / IDS**  
   Sits beside auth and the engine: records security-relevant events (for example suspicious sign-ins and attack patterns), applies detection rules, and routes alerts into an owner-facing review console.

## Trust boundaries

- Public research data is for analysis and ranking. It is not treated as an executable broker fill.
- Broker prices, positions, and order lifecycle require the EA bridge.
- AI copilots and analysers are optional second opinions. Malformed or low-quality model output cannot by itself approve a live delivery.
- Secrets stay in host environment configuration and encrypted stores. They are never shipped in this showcase repo.

## What this showcase deliberately omits

- Strategy and risk source code  
- Expert Advisor `.mq5` source  
- Environment templates that list production secret names in operational detail  
- Any claim of profit, return, or win rate  

For the live product, open [https://watch-five-lovat.vercel.app](https://watch-five-lovat.vercel.app).
