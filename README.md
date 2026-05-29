# NUMINA GEO Landing + AI Agent

Landing page pro sluzbu GEO s AI agentem za kontaktnim formularem.

## Co je soucasti

- `index.html` - hlavni staticka landing page
- `numina-landing.html` - stejna landing page pod pracovnim nazvem
- `numina-workflow.json` - n8n workflow pro webhook, Google Sheets persistenci, Gemini odpoved a Telegram notifikaci
- `DOCUMENTATION.md` - projektova dokumentace k praktickemu zadani
- `CAST_B_ZKUSENOSTI.md` - kratky popis zkusenosti s tvorbou webu
- `uploads/` - assety pouzite landing page

## Architektura

Uzivatel odesle formular na webu. Frontend posle `conversationId`, jmeno, e-mail a zpravu do n8n webhooku. n8n nacte historii z Google Sheets, ulozi novou zpravu, vygeneruje odpoved pres Gemini, ulozi odpoved do Sheets, posle notifikaci do Telegram skupiny a vrati odpoved zpet do weboveho chatu.

## Nasazeni

Web je staticky, proto staci Cloudflare Pages, Vercel nebo Netlify. Jako entry point pouzijte `index.html`.

V n8n je potreba doplnit:

- Google Sheets credentials a sheet `Konverzace`
- Gemini API credential
- Telegram bot token
- Telegram Chat ID skupiny
