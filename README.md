# Estella — Assistente Summer School 2026

Chatbot AI per rispondere a domande sulla Summer School 2026 di Wedding Planners Pro.

## Struttura

```
summer-school-chatbot/
├── index.html              ← L'app chatbot
├── netlify/functions/
│   └── chat.js             ← Proxy verso Claude API
├── netlify.toml            ← Config Netlify
└── README.md
```

## Setup in 3 step

### 1. Carica su GitHub
Crea un nuovo repository e carica l'intera cartella `summer-school-chatbot/`.

### 2. Collega a Netlify
- Vai su [netlify.com](https://netlify.com) → "Add new site" → "Import from Git"
- Seleziona il repo
- Build command: (lascia vuoto)
- Publish directory: `.`
- Deploy

### 3. Aggiungi la variabile d'ambiente
Su Netlify → Site settings → Environment variables → Add:

| Variabile | Valore |
|-----------|--------|
| `ANTHROPIC_API_KEY` | La tua API key di [console.anthropic.com](https://console.anthropic.com) |

Riavvia il deploy (Deploys → Trigger deploy).

## Personalizzazione

### Aggiornare la knowledge base
Apri `index.html` e modifica il contenuto della costante `KNOWLEDGE` (inizia a circa riga 350). Contiene tutte le informazioni sul corso che Estella userà per rispondere.

### Cambiare i link di iscrizione
Nello script, modifica:
```js
const FREE_URL = "https://weddingplannerspro.com/summerschoolbooking";
const VIP_URL = "https://weddingplannerspro.com/summer-school-vip";
```

### Cambiare il modello AI
In `netlify/functions/chat.js`, modifica:
```js
model: 'claude-sonnet-4-20250514'
```

## Integrazione nel sito

### Come iframe (pagina dedicata)
```html
<iframe
  src="https://nome-del-tuo-sito.netlify.app"
  width="100%"
  height="700px"
  style="border:none; border-radius:16px;">
</iframe>
```

### Come bubble flottante
Aggiungi nel footer del tema WordPress:
```html
<div id="chat-bubble" onclick="window.open('https://nome-del-tuo-sito.netlify.app','_blank','width=500,height=750')">
  💬 Chiedi a Estella
</div>
<style>
  #chat-bubble {
    position: fixed; bottom: 20px; right: 20px;
    background: linear-gradient(135deg, #4E7AB5, #3A5A8C);
    color: white; padding: 14px 22px; border-radius: 30px;
    cursor: pointer; box-shadow: 0 8px 24px rgba(58,90,140,0.3);
    font-family: sans-serif; z-index: 9999;
  }
</style>
```

## Funzionalità

- Knowledge base completa sulla Summer School 2026
- 4 quick action all'inizio (Come funziona, 3 livelli, Prezzi, Free vs VIP)
- CTA automatiche (Iscriviti Free / Scopri VIP) quando Estella suggerisce l'iscrizione
- Memoria della conversazione (Estella ricorda cosa hai detto prima)
- Fallback su email team@weddingplannerspro.it in caso di errore
- Responsive mobile
