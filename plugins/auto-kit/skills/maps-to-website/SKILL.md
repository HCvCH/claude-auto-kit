---
name: maps-to-website
description: Builds a complete website for a local business from a Google Maps link or business name — collects name, address, hours, services, photos and review themes, then runs project-pipeline and prepares a free deploy (Netlify, Vercel or a home server). Use when the user pastes a Maps link or asks for a site for a café, shop, salon, workshop or similar.
---

# Maps to Website

## 1. Collect the facts

From the link or name, use web search and the business's own pages (website, social profiles) to collect:

- name, category, address, phone, opening hours, map embed link
- services or menu with prices if public
- 3–5 recurring themes from public reviews (paraphrased, no copied review text, no reviewer names)
- existing logo and colors if the business has a brand

Don't scrape Google Maps pages directly; use what search results and the business's own sites show. Mark anything uncertain as "to confirm with the owner".

## 2. Plan

Write a one-screen brief: audience, main goal (calls, bookings, visits), pages (usually one page with sections: hero, about, services/menu, reviews summary, hours + map, contact), call to action.

## 3. Build

Run `project-pipeline` with project type WEB and this brief. Use real facts everywhere; placeholders only where data is missing, clearly marked.

## 4. Legal basics (Germany/EU)

Add an Impressum and Datenschutzerklärung page (placeholders for the owner's data), embed the map only after consent or as a static image with a link, and no tracking without consent.

## 5. Deploy (free)

- Netlify or Vercel free tier for a demo link (`vercel` CLI or Netlify).
- Or the user's own home server.
Give the user the demo link and a short list of what the owner must confirm.

## Rules

- Demo sites for businesses that haven't asked for one stay private or clearly marked as a demo; never publish under the business's name as if it were official.
- No fake reviews, no invented awards or prices.

---
Written for this repo; no third-party text copied.
License: CC-BY-NC-SA-4.0 — © HCvCH, https://github.com/HCvCH/claude-auto-kit (see NOTICE.md)
