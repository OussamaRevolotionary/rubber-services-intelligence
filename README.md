# Rubber Testing Intelligence

An interactive demo tool for rubber and tire testing services — by **Oussama Labs**.

🔗 **Live demo:** https://oussamarevolotionary.github.io/rubber-services-intelligence/

## What it does

- **Service Finder** — a guided 3-step flow: pick your material → testing need → get matching services with turnaround times, sample requirements, and standards.
- **Full Catalog** — browsable, searchable, filterable view of all 24 testing services across 5 categories, with a live category breakdown chart.
- **AI Technical Advisor** — a context-aware chatbot that answers questions on test methods, standards, equipment, turnaround times, and OE qualification.
- **Lead capture** — "Submit Your Testing Requirements" form that routes inquiries via N8N to a CRM sheet and email notification.

## Tech

Single self-contained `index.html` — no build step. Inter + JetBrains Mono, Chart.js, Lucide icons (all via CDN). Deployed on GitHub Pages.

## Backend (N8N)

Two workflows power the chatbot and the inquiry form. Importable JSON and setup instructions are in [`/n8n`](./n8n).

---

© Oussama Labs — demo build.
