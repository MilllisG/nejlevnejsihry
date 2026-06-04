# NejlevnejsiHry.link v0.1.0

Hotový startovací Next.js e-shop pro PC herní klíče. Připraveno pro GitHub + Netlify + doménu `nejlevnejsihry.link`.

## Co je hotové

- Next.js App Router projekt v TypeScriptu.
- Temný responzivní herní design bez Tailwind závislosti.
- Homepage, katalog, detail hry, demo checkout, právní stránky.
- Stripe checkout route: `app/api/checkout/route.ts`.
- Stripe webhook route: `app/api/webhook/stripe/route.ts`.
- Distributor/Kinguin klient: `lib/kinguin.ts`.
- Mock režim pro bezpečné nasazení bez API klíčů.
- Product JSON-LD, sitemap a robots.
- Netlify konfigurace: `netlify.toml`.
- Windows launcher: `start.bat`.

## Lokální spuštění

```bash
npm install
npm run dev
```

Nebo na Windows spusť `start.bat`.

## Nasazení na Netlify

1. Nahraj celý obsah ZIPu do GitHub repozitáře.
2. V Netlify zvol **Add new site → Import an existing project**.
3. Vyber GitHub repozitář.
4. Build settings:
   - Build command: `npm run build`
   - Publish directory: `.next`
5. Přidej vlastní doménu `nejlevnejsihry.link`.

## Environment variables na Netlify

V Netlify nastav proměnné v UI, necommituj reálný `.env` do GitHubu.

```env
NEXT_PUBLIC_SITE_URL=https://nejlevnejsihry.link
STRIPE_MOCK_MODE=true
STRIPE_SECRET_KEY=sk_test_replace_me
STRIPE_WEBHOOK_SECRET=whsec_replace_me
KINGUIN_MODE=mock
KINGUIN_ORDER_ENDPOINT=https://api.example.com/orders
KINGUIN_API_TOKEN=replace_me
NEXT_PUBLIC_DISCORD_URL=https://discord.com/invite/n7xThr8
NEXT_PUBLIC_YOUTUBE_URL=https://www.youtube.com/@TheHardwareGuru_Czech
NEXT_PUBLIC_KICK_URL=https://kick.com/thehardwareguru
```

## Přepnutí na ostrý Stripe

1. Ve Stripe vytvoř produktový/checkout flow přes API.
2. Nastav `STRIPE_SECRET_KEY`.
3. Nastav webhook endpoint: `https://nejlevnejsihry.link/api/webhook/stripe`.
4. Do Netlify vlož `STRIPE_WEBHOOK_SECRET`.
5. Změň `STRIPE_MOCK_MODE=false`.

## Přepnutí distributora z mock na live

V `lib/kinguin.ts` je obecný live klient. Protože přesná struktura API se může podle distributora lišit, ostrý endpoint nastavíš proměnnými:

```env
KINGUIN_MODE=live
KINGUIN_ORDER_ENDPOINT=https://real-distributor-endpoint.example/orders
KINGUIN_API_TOKEN=real_token
```

Po přidání reálných API údajů doporučený další krok: doplnit server-only databázi pro ukládání objednávek a klíčů. Netlify Database existuje, ale je kreditový/účtovaný režim; pokud chceš držet nulové náklady, nech web v mock/demo režimu a databázi připoj až před ostrým prodejem.

## Důležité právní upozornění

Právní stránky v tomto buildu jsou technické šablony. Před ostrým prodejem digitálního obsahu je nutné doplnit IČO, kontakty, finální obchodní podmínky, GDPR a proces odstoupení/reklamací podle aktuální legislativy.
