# GymArena come PWA

File: `index.html`, `manifest.webmanifest`, `sw.js`, `icon.svg`, `icon-192.png`, `icon-512.png`. Vanno tutti nella stessa cartella, serviti via **https**.

## Pubblicare gratis con GitHub Pages
1. Crea un repository su github.com (es. `gymarena`) e carica questi file nella radice.
2. Settings → Pages → Source: *Deploy from a branch* → `main` / `/ (root)` → Save.
3. Dopo un minuto trovi l'app su `https://TUONOME.github.io/gymarena/`.

## Installare sul telefono
- **Android (Chrome)**: menu ⋮ → *Installa app* / *Aggiungi a schermata Home*.
- **iPhone (Safari)**: Condividi → *Aggiungi alla schermata Home*.

## Da sapere
- Apri l'app una volta con internet: poi funziona offline (font e immagini wger si salvano dopo il primo uso).
- I dati stanno nel browser di *quel* telefono, separati dal sito nel browser normale e dalla versione pubblicata su Claude. Per spostarli usa Profilo → Esporta / Importa.
- Cancellare i dati del sito azzera tutto: esporta ogni tanto.
- Dopo una modifica a `index.html` cambia `gymarena-v4` in `sw.js` (es. `v2`) per forzare l'aggiornamento.
- Su iPhone le notifiche del browser richiedono l'app installata in Home e iOS 16.4+.
- **Scanner codice a barre** (Dispensa → 📷): funziona con Chrome su Android e serve la rete. Su iPhone (Safari) il browser non lo supporta: scrivi il codice a mano e premi Cerca.
