# NUMINA GEO Landing Page + AI Agent

## 1. Záměr a koncept

Cílem projektu bylo vytvořit jednoduchou, funkční a vizuálně výraznou landing page pro službu GEO (Generative Engine Optimization) z pohledu marketingové agentury. GEO chápu jako návaznost na SEO v prostředí AI vyhledávání: nejde pouze o pozice ve výsledcích Google, ale o to, jestli značku doporučí AI nástroje jako ChatGPT, Perplexity, Gemini, Google AI Overviews, Claude nebo Copilot.

Landing page je postavená pro B2B značky, e-commerce, služby a firmy, jejichž zákazníci začínají hledat odpovědi přes AI asistenty. Tón komunikace je sebevědomý, ale praktický: vysvětluje, proč GEO dává smysl, co klient získá, jak probíhá proces a kolik služba stojí.

Vizuálně jsem zvolil prémiovější agenturní styl: světlé krémové pozadí, tmavě modrý kontrast, výrazná typografie, jednoduché karty a interaktivní prvek ve formě animovaného AI editoru. Cílem bylo, aby stránka nepůsobila jako generická SaaS šablona, ale jako prezentace služby od AI-first agentury.

## 2. Použité technologie a nástroje

Frontend:
- HTML5
- Tailwind CSS přes CDN
- vlastní CSS pro animace, chat, scrollbar a responzivní úpravy
- vanilla JavaScript pro chat, formulář, animace a komunikaci s webhookem

Hosting:
- Cloudflare Pages
- statický deploy z GitHub repozitáře
- entry point: `index.html`

Repozitář:
- GitHub: `https://github.com/santavyM/numina-geo-landing`

Automatizace:
- n8n Cloud
- webhook endpoint pro příjem zpráv z webu
- Google Sheets jako jednoduchá persistence konverzací
- Telegram skupina pro notifikace majiteli webu

LLM:
- Google Gemini přes n8n node
- model v n8n lze přepnout podle aktuální dostupnosti/quota limitů

Persistence:
- Google Sheets list `Konverzace`
- sloupce: `conversationId`, `role`, `text`, `name`, `email`, `timestamp`
- `conversationId` se generuje ve frontendu a ukládá do `localStorage`, aby navazující zprávy zůstaly ve stejném vlákně

Šablona / výchozí návrh:
- Vycházel jsem z dodaného statického HTML návrhu z Claude exportu pro značku VISER.
- Návrh jsem upravil na značku NUMINA, přepsal texty a napojil formulář/chat na n8n automatizaci.
- Dále jsem upravoval UX detailů chatu, čitelnost inputu, scrollbar a zpracování eskalačního tokenu.

## 3. Architektura řešení

Tok dat:

```text
Uživatel vyplní formulář nebo napíše do chatu
        ↓
Frontend odešle POST request na n8n webhook
        ↓
n8n načte historii konverzace z Google Sheets podle conversationId
        ↓
n8n uloží novou zprávu uživatele do Google Sheets
        ↓
Gemini dostane prompt + historii konverzace + novou zprávu
        ↓
n8n zpracuje odpověď, odstraní interní token [ESKALACE]
        ↓
n8n uloží odpověď AI do Google Sheets
        ↓
n8n pošle notifikaci do Telegram skupiny
        ↓
n8n vrátí JSON odpověď zpět na web
        ↓
Uživatel vidí odpověď v chatu
```

Frontend posílá na webhook tento payload:

```json
{
  "conversationId": "uuid-konverzace",
  "name": "Jméno uživatele",
  "email": "email@example.com",
  "message": "Text zprávy"
}
```

n8n vrací odpověď ve tvaru:

```json
{
  "reply": "Text odpovědi AI asistenta"
}
```

## 4. AI agent a eskalace

Agent má za úkol odpovídat česky, stručně a v kontextu předchozí komunikace. Pokud si není jistý, uživatel chce individuální nabídku, slevu, smlouvu nebo něco mimo jasně popsaný rozsah služby, použije interní token `[ESKALACE]`.

Tento token není určený pro uživatele. Workflow ho detekuje, odstraní z odpovědi a do Telegram skupiny přidá upozornění, že je potřeba zásah člověka. Uživatel mezitím dostane přirozenou odpověď, že dotaz předáváme kolegovi z týmu.

## 5. Klíčový prompt agenta

Zkrácená verze hlavního promptu v n8n:

```text
Jsi přátelský a profesionální AI asistent marketingové agentury NUMINA,
která nabízí službu GEO (Generative Engine Optimization).

ZDROJ PRAVDY O NUMINA:
- NUMINA pomáhá značkám být viditelné v odpovědích AI vyhledávačů.
- GEO Audit stojí 39 000 Kč jednorázově.
- GEO Růst stojí 59 000 Kč měsíčně bez dlouhodobého závazku.
- První pohyb ve viditelnosti lze typicky očekávat do 14 dní.
- Stabilní růst se buduje v horizontu 2–3 měsíců.
- Kontakt: projekty@numina.cz, +420 737 499 315.

TVŮJ ÚKOL:
- Odpovídej česky, vstřícně, lidsky a stručně.
- Reaguj konkrétně na to, co uživatel napsal.
- Nikdy neuváděj jiné ceny než 39 000 Kč za GEO Audit a 59 000 Kč/měsíc za GEO Růst.
- Pokud si nejsi jistý nebo je potřeba člověk, napiš do odpovědi token [ESKALACE].

KONTEXT KONVERZACE:
{{ historie z Google Sheets }}

NOVÁ ZPRÁVA UŽIVATELE:
{{ nová zpráva z webhooku }}
```

## 6. Práce s AI nástroji

AI nástroje jsem použil hlavně pro:
- rychlé vytvoření vizuálního návrhu landing page
- návrh textů a struktury pro GEO službu
- iteraci nad UX chatovacího rozhraní
- návrh n8n workflow a promptu agenta
- ladění chyb v automatizaci, zejména persistence, Gemini quota, mapování Google Sheets a Telegram Chat ID
- přípravu dokumentace

Ručně jsem řešil zejména:
- napojení frontendu na webhook
- práci s `conversationId` a `localStorage`
- testování reálného toku dat mezi webem, n8n, Sheets, Gemini a Telegramem
- úpravy konkrétních chyb v n8n nodech
- sjednocení cen a faktických informací mezi webem a promptem

## 7. Časový rozpis

Orientační čas:
- Analýza zadání a rešerše GEO: 30–45 minut
- Landing page a vizuální úpravy: 2 hodiny
- Napojení formuláře a chat UI na webhook: 45 minut
- n8n automatizace, Google Sheets persistence, Gemini, Telegram: 2–3 hodiny
- Testování a ladění chyb: 1–1,5 hodiny
- Dokumentace a část B: 1 hodina

Celkově se projekt pohyboval kolem zadaného rámce přibližně 6 hodin čisté práce, s dodatečným časem na ladění reálných integračních detailů.

## 8. Testování

Testoval jsem:
- odeslání formuláře z webu do n8n webhooku
- předání `conversationId`, jména, e-mailu a zprávy
- zápis zprávy uživatele do Google Sheets
- načtení historie konverzace
- odpověď Gemini v kontextu vlákna
- zápis odpovědi AI do Google Sheets
- notifikaci do Telegram skupiny
- odpověď zpět na webový chat
- eskalační scénář přes interní token `[ESKALACE]`

## 9. Co bych udělal v další fázi

V další fázi bych řešení posunul hlavně v těchto oblastech:
- nahradil Google Sheets robustnější databází, například Supabase nebo PostgreSQL
- přidal jednoduchý admin přehled konverzací
- doplnil možnost, aby majitel webu odpověděl v Telegramu a agent tuto instrukci použil v další odpovědi
- přidal server-side proxy pro webhook, aby URL nebyla přímo ve frontendu
- doplnil analytiku, například Cloudflare Web Analytics nebo Plausible
- přidal reálné měření konverzí a událostí formuláře
- lépe oddělil prompt, znalostní bázi a obchodní data, aby se ceny daly měnit bez zásahu do workflow

## 10. Odkazy

- Landing page: doplnit finální Cloudflare Pages URL
- GitHub repo: https://github.com/santavyM/numina-geo-landing
- n8n workflow: export v souboru `numina-workflow.json`
- AI konverzace: doplnit sdílený odkaz, pokud bude součástí odevzdání

