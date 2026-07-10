# Dashboard Stato Review — Sign-Off

Dashboard interattiva per monitorare lo stato di avanzamento delle review
documentali verso il Sign-Off finale, con **memoria condivisa in tempo reale**.

Ogni modifica (First-Pass / Sign-Off completato) è visibile a tutti
istantaneamente e persistente nel tempo. Il progresso è ponderato
sull'effort di revisione di ciascun documento.

## Demo live
Una volta pubblicata su GitHub Pages: `https://<tuo-utente>.github.io/<repo>/`

---

## Setup in 3 passi

### 1. Crea il database Supabase (gratuito)
- Vai su [supabase.com](https://supabase.com) → *Start your project*.
- Crea un nuovo progetto e attendi ~30 secondi.
- Apri **SQL Editor** → *New query*, incolla il contenuto di
  [`supabase-setup.sql`](./supabase-setup.sql) e premi **Run**.
- Vai in **Project Settings → API Keys** (o *Connect*) e copia:
  - **Project URL** (es. `https://abcd1234.supabase.co`)
  - **Publishable key** (`sb_publishable_...`) oppure la **anon** key legacy.

### 2. Inserisci le chiavi
In `index.html`, nel blocco `CONFIGURAZIONE SUPABASE` in fondo al file:

```js
const SUPABASE_URL = "https://abcd1234.supabase.co";
const SUPABASE_KEY = "sb_publishable_xxxxxxxxxxxxx";
const ROOM = "gara-fs-review";
```

### 3. Pubblica su GitHub Pages
- Carica i file in un repository **public**.
- **Settings → Pages → Source: Deploy from a branch → main / (root)**.
- Dopo 1-2 minuti ottieni il link pubblico da condividere.

---

## Comportamento

| Situazione | Cosa succede |
|---|---|
| Apri il link | Vedi l'ultimo stato salvato sul database |
| Clicchi un cerchio | Salvato subito, visibile a tutti in tempo reale |
| Chiudi e riapri | Lo stato resta (memoria persistente) |
| Chiavi non inserite | Funziona in locale sul singolo browser (fallback) |

## Personalizzazione
I documenti e i pesi di effort sono nell'array `DOCS` in `index.html`.
Il campo `weight` è il peso % del documento; `fp` e `so` sono le quote
di First-Pass e Sign-Off (la loro somma è il peso del documento).

## Note
- Lo script SQL apre la board in lettura/scrittura pubblica: adatto a un
  cruscotto di stato condiviso. Per limitare la scrittura serve un login.
- I progetti Supabase free vanno in pausa dopo ~1 settimana di inattività;
  riaprire la dashboard li riattiva.
