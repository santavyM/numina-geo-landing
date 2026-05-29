# Část B — Popis zkušeností s tvorbou webů

Jsem web developer zaměřený hlavně na WordPress, frontend a technickou správu klientských webů. Nejvíc zkušeností mám s praktickými webovými projekty, kde nejde jen o nakódování vzhledu, ale také o editovatelný obsah, formuláře, výkon, SEO, e-commerce logiku, importy dat nebo napojení na externí systémy.

## Zkušenosti s WordPressem

WordPress používám především pro klientské weby, kde je důležité, aby si klient mohl obsah dlouhodobě spravovat sám. Nejčastěji pracuji s custom šablonami v PHP, ACF poli, repeater sekcemi, vlastními post types, taxonomiemi a `WP_Query`. Snažím se stavět administraci tak, aby byla pro klienta srozumitelná, ale zároveň aby frontend zůstal čistý, rychlý a dobře udržovatelný.

Mám zkušenosti také s WooCommerce. Řešil jsem úpravy checkoutu, objednávkového procesu, chyby v objednávkách, subscription scénáře a menší úpravy e-shopové logiky podle potřeb klienta. Kromě klasických webů jsem pracoval i na importech dat do WordPressu, generování XML feedů, napojení na reklamní nebo srovnávací systémy a na technických úpravách kolem SEO, výkonu a analytiky.

Moje silnější stránka ve WordPressu je kombinace frontendu, ACF/PHP šablon, praktických integrací a debuggingu produkčních problémů. Baví mě hledat konkrétní příčinu chyby, ať už jde o plugin konflikt, cache, formulář, e-mailovou doručitelnost, výkon, datový import nebo problém v objednávkovém procesu.

## Další nástroje

Se Shoptetem mám zkušenosti hlavně z pohledu frontendových úprav, úprav šablon, drobných skriptů a řešení vizuálních nebo UX detailů v e-shopu. Mám také základní zkušenost s Upgates.

Shopify, Webflow a Framer zatím nemám jako hlavní každodenní praxi, ale rozumím jejich účelu a workflow. Shopify vnímám jako silnou e-commerce platformu, Webflow a Framer jako nástroje vhodné pro rychlou tvorbu vizuálně kvalitních webů bez nutnosti stavět celé CMS ručně. Pokud bych na nich měl pracovat, začal bych pochopením šablony, datového modelu, možností editoru a hranic vlastního kódu.

Z frontendových technologií běžně používám HTML, CSS, JavaScript, Tailwind CSS, Bootstrap, jQuery a knihovny jako Splide.js. Řeším responzivní layouty podle grafických návrhů, technické SEO, strukturovaná data, výkon, Lighthouse, LCP, CLS, WebP, lazy loading a měření konverzí přes dataLayer nebo analytické nástroje.

## Jak postupuji při stavbě webu

Na začátku se snažím pochopit účel webu: pro koho je, co má návštěvník udělat, jaký je hlavní konverzní cíl a jak bude klient s obsahem dál pracovat. Potom si projekt rozdělím na strukturu stránek, obsahové bloky, technické požadavky, integrace a riziková místa.

U WordPress webů přemýšlím hlavně nad tím, které části mají být editovatelné přes ACF, kde dává smysl použít custom post type, kde stačí běžná stránka a jak nastavit šablony tak, aby klient nemusel řešit technické detaily. U e-commerce projektů se víc soustředím na katalog, objednávkový proces, feedy, měření konverzí a napojení na externí systémy.

Po implementaci testuji responzivitu, formuláře, e-mailovou doručitelnost, rychlost, základní SEO, analytiku a chování v produkčním prostředí. U klientských webů beru jako důležitou část práce i následnou správu: aktualizace, opravy chyb, optimalizace výkonu a řešení reálných provozních problémů.

## Jak bych k této landing page přistoupil ve WordPressu

Tuto konkrétní landing page jsem kvůli rychlosti a zadání postavil jako statický frontend s n8n automatizací. Pokud bych ji měl stavět přímo ve WordPressu, zvolil bych pravděpodobně custom šablonu s ACF bloky, případně lehký builder podle potřeb klienta.

Strukturu bych rozdělil na editovatelné sekce:
- hero sekce s hlavním claimem a CTA,
- vysvětlení služby GEO,
- proces spolupráce,
- ceník,
- kontaktní formulář,
- blok s AI chatem nebo embedded chat komponentou.

Pro formulář bych použil buď vlastní AJAX endpoint, nebo osvědčený formulářový plugin s webhook podporou. Odeslání by opět směřovalo do n8n, kde by běžel stejný princip automatizace: persistence konverzací, AI odpověď, Telegram notifikace a instrukce majitele. Hosting bych u WordPress varianty volil podle rozsahu projektu, například kvalitní managed WordPress hosting s dobrou cache a stagingem. Pro jednodušší statickou variantu mi dává větší smysl Cloudflare Pages, protože backendovou logiku už řeší n8n.

## Co mě na tvorbě webů baví

Baví mě kombinace vizuální práce a technického řešení. Mám rád, když je výsledek vidět, ale zároveň pod ním běží promyšlená logika: dobře připravená administrace, čistá data, rychlý frontend, funkční formuláře, správné měření a stabilní integrace.

Baví mě také debugging a technické integrace. Často je potřeba spojit více částí dohromady: API, importy, XML feedy, cron úlohy, analytiku nebo automatizace. Právě tyto praktické úlohy mě posouvají, protože člověk musí pochopit nejen kód, ale i celý proces okolo.

## Co mě baví méně a kde se chci posouvat

Méně mě baví nejasná zadání bez rozhodnutí, kdy není jasné, co má být výstupem nebo kdo za co odpovídá. Zároveň vím, že schopnost doptat se, rozdělit problém a navrhnout rozumné řešení je důležitá součást práce developera.

Mezi moje rozvojové oblasti patří hlubší práce s Reactem/Next.js, TypeScriptem, modernějšími PHP frameworky jako Symfony nebo Nette a každodenní používání Dockeru. OOP v PHP znám základně a chci se v něm dál zlepšovat. Angličtinu zvládám hlavně pro čtení technické dokumentace a postupně zlepšuji mluvení.

Kariérně mě nejvíc zajímá směr WordPress/WooCommerce vývoje, frontend s WordPress přesahem, e-commerce, technické integrace, API, importy a XML feedy. Do budoucna mě láká také postupný přesah do React/Next.js, PHP frameworků nebo analytického návrhu technických řešení.
