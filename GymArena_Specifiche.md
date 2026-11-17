# GymArena 🏋️🍽️ — Specifiche di progetto

> App mobile che unisce **allenamento gamificato** e **alimentazione personalizzata**.
> Impara i tuoi gusti (negli esercizi e nel cibo), si adatta agli attrezzi e alla cucina che hai, traccia i tuoi progressi e ti fa competere con gli amici.
> Obiettivo di fondo: **rendere piacevole sia andare in palestra sia mangiare bene**, senza che diventi un obbligo.

---

## 1. Visione e principi

| Principio | Cosa significa |
|---|---|
| **Divertimento prima di tutto** | XP, livelli, streak, badge e sfide trasformano ogni serie e ogni pasto in un piccolo obiettivo. |
| **L'app impara da te** | Dopo ogni esercizio e ogni ricetta dici se ti è piaciuto; col tempo i suggerimenti privilegiano ciò che ami ed evitano ciò che odi. |
| **Realismo** | Consiglia solo ciò che puoi davvero fare: con gli attrezzi che hai, gli ingredienti che hai in casa, il tempo che hai. |
| **Il progresso è visibile** | Pesi usati, trend, streak, piani rispettati: tutto salvato e mostrato in modo chiaro. |
| **Allenamento e cibo parlano tra loro** | Il piano pasti tiene conto di cosa alleni oggi e dello sport che hai fatto. |
| **Niente pressione** | Le meccaniche di gioco premiano la costanza, non puniscono gli errori. |
| **Sicurezza** | Allergie e intolleranze sono vincoli rigidi; nessun obiettivo calorico estremo. |

---

## 2. Moduli dell'app

1. Allenamento
2. Gamification
3. Sport del giorno
4. Preferenze esercizi ("AI dei gusti")
5. Tracciamento pesi
6. Schede personalizzate
7. **Nutrizione** (profilo, attrezzatura, dispensa, gusti, ricette, piano settimanale, lista della spesa)
8. Amici e classifica
9. Profilo e impostazioni

---

## 3. Allenamento

### 3.1 Home
- Scheda con **livello**, barra XP, sessioni, streak e badge.
- Check-in **sport del giorno**.
- Riepilogo **pasto del giorno** (prossimo pasto previsto, ricetta suggerita).
- Grafico dell'attività settimanale.
- Griglia dei gruppi muscolari: **Petto, Schiena, Gambe, Spalle, Braccia, Core** + **Full Body** (scheda generica che fa un po' di tutto).
- Ogni card mostra una barra di **affinità** (quanto ti piace quel gruppo).

### 3.2 Allenamento attivo
Flusso pensato per l'uso con una mano, in palestra:

1. Scegli il gruppo muscolare → lista esercizi ordinata in base ai tuoi gusti.
2. **Un tap per ogni serie** (non per ripetizione).
3. Inserisci il **peso usato**, precompilato con quello dell'ultima volta.
4. Dopo ogni serie parte il **timer di riposo** (default 60 s, configurabile) con anello circolare, **skippabile**, con vibrazione/suono a fine riposo.
5. A fine esercizio: **❤️ Adoro / 😐 Meh / 💀 Odio**.
6. Timer totale, pallini di avanzamento per esercizio e per serie, suggerimento tecnico per ogni esercizio.
7. A fine allenamento: bonus XP, aggiornamento streak e sessioni.

### 3.3 Dimostrazione degli esercizi
- Immagini o brevi animazioni (due frame o GIF/video) che mostrano **come eseguire** il movimento.
- Descrizione tecnica breve, muscoli coinvolti, errori comuni.
- Fonte principale: **wger.de** (API REST gratuita e open source), con database locale di riserva per l'uso offline.

---

## 4. Gamification

**Livelli** — si sale al livello `N+1` quando gli XP totali raggiungono `N × 500`.

**Fonti di XP**

| Azione | XP |
|---|---|
| Serie completata | `XP dell'esercizio ÷ numero di serie` |
| Allenamento completato | +100 bonus |
| Sport del giorno | vedi sezione 5 (una volta al giorno) |
| Pasto cucinato e registrato | +20–40 (vedi sezione 9.9) |
| Giornata del piano pasti rispettata | +50 |
| Lista della spesa completata | +30 |

**Streak** — separate per **allenamento** e per **alimentazione**. Se salti un giorno si riparte da 1; più allenamenti nello stesso giorno non contano doppio. Un "giorno di riposo dichiarato" non spezza la streak di allenamento.

**Badge (esempi)**

| Badge | Condizione |
|---|---|
| 🔥 Streak 7 | 7 giorni consecutivi di allenamento |
| 💎 10 / 🦾 50 / 🥇 100 Sessioni | Numero di allenamenti |
| ⚡ AI Master | 10 esercizi valutati |
| 🏃 Multi-Sport | 3 sport diversi nello stesso giorno |
| 👨‍🍳 Primo piatto | Prima ricetta cucinata |
| 🗓️ Settimana perfetta | Piano pasti rispettato per 7 giorni |
| 🧊 Zero sprechi | Ingredienti in scadenza usati 10 volte |
| 🌍 Chef del mondo | Ricette di 5 cucine diverse |
| 🔧 Padrone di casa | Cucinato con tutti gli attrezzi del profilo |

**Sfide** — Settimana di Fuoco, Century Club, Sportivo Completo (5 sport diversi), **Sfida dispensa** (cucina 3 ricette usando solo ciò che hai), **Mangia l'arcobaleno** (5 colori di verdure in una settimana). Le ricompense in XP vengono assegnate al completamento.

---

## 5. Sport del giorno

Ogni giorno l'app chiede **"Hai fatto altro sport oggi?"**. Serve a:
- assegnare **XP in base all'intensità**;
- mostrare un **consiglio contestuale** e **adattare davvero** il volume dell'allenamento (meno gambe se hai corso);
- **regolare i pasti del giorno** (più carboidrati/calorie dopo sport intensi).

| Sport | XP | Effetto sull'allenamento |
|---|---|---|
| 😴 Riposo | 0 | Recupero attivo |
| 🚶 Camminata | 30 | Nessuna restrizione |
| 🧘 Yoga | 40 | Allenamento completo consigliato |
| 🎾 Tennis | 55 | Spalle e braccia già attive |
| 🏃 Corsa | 60 | Riduci le gambe |
| 🥾 Trekking | 65 | Gambe moderate |
| 🚴 Ciclismo | 70 | Gambe affaticate, punta su upper body |
| ⚽ Calcio | 75 | Gambe molto stanche |
| 🏊 Nuoto | 80 | Upper body moderatamente sotto sforzo |
| 🥊 Boxe | 85 | Braccia affaticate |
| 🧗 Arrampicata | 90 | Braccia e schiena molto attive |

Regole: XP assegnati una volta al giorno; "Riposo" esclude gli altri sport.

---

## 6. Preferenze esercizi ("AI dei gusti")

Non è machine learning pesante: è una **media mobile esponenziale** semplice e trasparente.

- Voti: ❤️ Adoro = **+100**, 😐 Meh = **0**, 💀 Odio = **−80**.
- Primo voto → punteggio = voto. Poi: `nuovo = vecchio × 0.4 + voto × 0.6`.
- **≥ 60** preferito (in cima, badge "AI▲"); **< −20** evitato (in fondo).
- Pagina dedicata con preferiti, evitati, tutti i rating e piccoli insight.
- Barra di affinità per gruppo muscolare.

---

## 7. Tracciamento pesi

- Peso salvato per ogni serie completata, con data.
- Peso dell'ultima volta mostrato prima di iniziare l'esercizio e precompilato.
- Storico per esercizio: **ultimo peso, record personale, trend ▲/▼, mini-grafico**.
- **Progressive overload**: l'app suggerisce di aumentare il carico quando completi tutte le serie con facilità per più sessioni.

---

## 8. Schede personalizzate

- Scelta di **giorni a settimana** (2–5), **durata media** (30/45/60/90 min) e **obiettivo** (forza, ipertrofia, resistenza, dimagrimento, full body).
- La durata regola serie per esercizio e numero di esercizi per giornata.
- Esercizi ordinati in base ai gusti; stima dei minuti per giornata.
- La scheda viene **salvata**, si può avviare l'intera giornata (tutti i gruppi previsti) e modificare/sostituire singoli esercizi.
- Scheda **Full Body** generica sempre disponibile.

---

## 9. Nutrizione 🍽️

### 9.1 Profilo nutrizionale
- **Obiettivo**: dimagrire, mantenere, mettere massa, performance.
- **Fabbisogno stimato**: metabolismo basale (formula Mifflin-St Jeor da peso, altezza, età, sesso) × livello di attività, corretto in base agli allenamenti e allo sport registrati.
- **Macro target**: proteine, carboidrati, grassi (suggeriti in base all'obiettivo, modificabili).
- **Dieta**: onnivora, vegetariana, vegana, pescetariana, senza glutine, senza lattosio, ecc.
- **Allergie e intolleranze**: vincoli **rigidi**, mai superati da nessun suggerimento.
- **Ingredienti esclusi** a prescindere dai gusti (es. coriandolo, fegato).
- **Preferenze pratiche**: tempo massimo di preparazione, budget, numero di porzioni (single, coppia, famiglia), abilità in cucina.

### 9.2 Attrezzatura di cucina
L'app sa **con cosa puoi cucinare**. Checklist modificabile in qualsiasi momento:

| Categoria | Esempi |
|---|---|
| Cottura base | Fornelli, forno, forno ventilato, microonde, piastra/griglia |
| Cottura veloce | **Friggitrice ad aria**, pentola a pressione, bollitore |
| Cottura lenta | Slow cooker, vaporiera |
| Preparazione | Frullatore, frullatore a immersione, robot da cucina, bilancia, planetaria |
| Altro | Tostapane, sandwich maker, riscaldatore per riso, macchina del pane |

Uso dei dati:
- le ricette vengono **filtrate** in base agli attrezzi posseduti;
- ricette adattabili vengono proposte con la **variante** giusta (es. "pollo al forno" → "pollo in friggitrice ad aria, 18 min a 200°");
- si può dichiarare per ogni sessione "oggi ho solo il microonde" (modalità **cucina ridotta**).

### 9.3 Dispensa e frigo
Inventario di ciò che hai in casa:
- **Aggiunta** manuale, da **lista della spesa completata**, o da **scansione codice a barre** (Open Food Facts).
- Per ogni articolo: nome, quantità, unità, categoria (frigo/freezer/dispensa), **data di scadenza**.
- **Ingredienti base sempre presenti** (sale, olio, pepe, spezie comuni) configurabili, così non finiscono sempre in lista.
- Dopo aver cucinato una ricetta, gli ingredienti usati vengono **scalati** dalla dispensa.
- **Avvisi di scadenza** e suggerimenti "usa prima questo".

### 9.4 Gusti alimentari (stesso principio degli esercizi)
L'app impara cosa ti piace mangiare.

- Dopo ogni ricetta cucinata o piano completato: **❤️ Adoro / 😐 Meh / 💀 Odio**.
- Il voto si propaga a più livelli:
  - **ricetta** (peso maggiore);
  - **ingredienti principali** (es. salmone, broccoli);
  - **tipo di cucina** (italiana, asiatica, messicana…);
  - **metodo di cottura** (fritto, al forno, crudo…);
  - **profilo di sapore** (piccante, dolce, cremoso, leggero…).
- Stessa formula degli esercizi: `nuovo = vecchio × 0.4 + voto × 0.6`; soglie ≥ 60 preferito, < −20 evitato.
- **Quiz iniziale** di onboarding (20–30 immagini/piatti da swipare) per partire già con un profilo di gusto.
- **Esplorazione controllata**: una piccola quota (≈10–15%) di suggerimenti è "novità fuori dai tuoi gusti", per non restare sempre sugli stessi piatti.
- Pagina **"I miei gusti"** con ingredienti, cucine e ricette preferite/evitate, modificabile a mano.

### 9.5 Ricette in base a ciò che hai in casa
Funzione **"Cosa cucino adesso?"**:

1. Parte dalla dispensa.
2. Per ogni ricetta calcola la **percentuale di ingredienti posseduti** e cosa manca.
3. Filtra per **attrezzi**, **dieta**, **allergie**, **tempo disponibile**.
4. Ordina con un punteggio composito (modificabile):

```
punteggio = 0.40 × ingredienti posseduti
          + 0.30 × gusto personale
          + 0.15 × aderenza ai macro del momento
          + 0.15 × ingredienti in scadenza usati
```

Viste rapide:
- **Posso farla subito** (100% ingredienti presenti);
- **Manca 1 ingrediente** (con pulsante "aggiungi alla spesa");
- **Svuota-frigo** (usa gli articoli in scadenza);
- **Post-allenamento** (ricette ricche di proteine e carboidrati, veloci);
- **Pasto veloce** (≤ 15 min) e **meal prep**.

Ogni ricetta mostra: foto, tempo, difficoltà, attrezzi necessari, porzioni (con scaling), ingredienti, passaggi, **valori nutrizionali per porzione** e pulsante **"Cucina ora"** con passaggi uno alla volta e timer integrati.

### 9.6 Piano pasti settimanale
- Genera i pasti per **7 giorni**: colazione, pranzo, cena, spuntini (configurabili).
- Vincoli rispettati: **calorie e macro** giornalieri, dieta, allergie, gusti, attrezzi, tempo di preparazione per giorno (es. "lunedì 20 min, domenica libero").
- **Collegato all'allenamento**:
  - giorno gambe o sport intenso → più carboidrati e calorie;
  - giorno di riposo → porzioni più leggere;
  - **pasto pre/post allenamento** suggerito in base all'orario della sessione.
- **Varietà**: evita la stessa proteina o cucina più di 2 volte a settimana.
- **Meal prep e avanzi**: può pianificare "cucina una volta, mangia due volte" per risparmiare tempo.
- **Controllo manuale**: blocca un pasto, sostituiscilo (propone alternative simili), sposta tra giorni, segna "mangio fuori".
- **Rigenerazione** parziale (solo da mercoledì in poi, solo la cena, ecc.).
- Riepilogo settimanale: media calorie/macro, costo stimato, varietà.

### 9.7 Lista della spesa automatica
Generata dal piano pasti della settimana:

1. **Somma** gli ingredienti di tutte le ricette pianificate (con porzioni scalate).
2. **Converte e unifica** le unità (g, ml, cucchiai, pezzi).
3. **Sottrae** ciò che è già in dispensa.
4. **Raggruppa per reparto** (ortofrutta, carne e pesce, latticini, dispensa, surgelati, ecc.) per fare la spesa più in fretta.
5. Permette di **spuntare** gli articoli durante la spesa, **aggiungere** articoli extra, modificare quantità.
6. Alla chiusura, gli articoli acquistati **entrano in dispensa** con scadenza stimata.
7. **Condivisione** della lista (testo/link) con partner o coinquilini.
8. Opzione **"lista per N giorni"** (es. solo i prossimi 3 giorni) e **risparmio**: segnala quando un ingrediente è usato in più ricette, così conviene comprare il formato grande.

### 9.8 Registro pasti e nutrizione
- Registrazione rapida del pasto: "ho mangiato il piano", "ho cucinato la ricetta X", "ho mangiato altro" (inserimento manuale o scansione codice a barre).
- Riepilogo giornaliero di **calorie e macro** rispetto all'obiettivo, in forma **semplice e non ossessiva** (barre morbide, nessun rosso aggressivo).
- Trend settimanale di peso corporeo (opzionale) accanto ai progressi di forza.

### 9.9 Gamification nutrizionale
- XP per pasto cucinato e registrato, per giornata del piano rispettata, per lista della spesa completata.
- Streak alimentare **separata** da quella di allenamento, con "giorno libero" che non la spezza.
- Badge e sfide dedicati (vedi sezione 4).
- Sfide tra amici: "più ricette nuove provate questa settimana", "più giorni di piano rispettati".

### 9.10 Linee guida di sicurezza
- L'app **non è un servizio medico né dietistico**; mostra un avviso chiaro e invita a consultare un professionista per condizioni specifiche.
- **Allergie e intolleranze** sono filtri bloccanti.
- **Limiti di sicurezza** sugli obiettivi: nessun deficit calorico estremo, nessun obiettivo sotto soglie minime ragionevoli, niente messaggi che incoraggiano restrizioni.
- Linguaggio neutro: nessun cibo "buono/cattivo", nessuna colpevolizzazione.
- Opzione per **nascondere** conteggio calorie e peso per chi preferisce un approccio più rilassato.

---

## 10. Amici e classifica

- **Codice amico** per aggiungere persone; classifica per XP con medaglie 🥇🥈🥉.
- **Sfide a tempo** (allenamento e nutrizione) con metrica e scadenza.
- **Condivisione** di ricette, piani settimanali e liste della spesa.
- Si condividono solo **statistiche aggregate** (livello, XP, streak, badge); peso corporeo, altezza e dati di salute restano privati.

**Backend proposto**

| Servizio | Pro | Contro |
|---|---|---|
| **Firebase** (Auth + Firestore) | Setup rapido, SDK web, piano gratuito | Lock-in Google |
| **Supabase** (Postgres + Auth) | Open source, SQL, piano gratuito | Configurazione leggermente più lunga |

```
users/{uid}          → name, avatar, level, xp, trainingStreak, nutritionStreak, friendCode
friends/{uid}/list   → [friendUid, ...]
challenges/{id}      → from, to, metric, startDate, endDate, status
sharedRecipes/{id}   → ownerUid, recipeId, note
```

---

## 11. Profilo e impostazioni

- Nome, avatar, peso, altezza, età, sesso, livello di esperienza, obiettivo.
- Profilo nutrizionale, attrezzatura, dieta, allergie.
- Unità di misura (kg/lb, g/oz), lingua, notifiche, tema.
- **Backup e ripristino** dei dati (esporta/importa).

---

## 12. Dati e modello

### 12.1 Entità principali

```
UserProfile      { nome, avatar, peso, altezza, età, sesso, esperienza, obiettivo, xp, livello, streak... }
Exercise         { id, nome, gruppo, serie, ripetizioni, riposo, xp, difficoltà, immagine, suggerimento }
WorkoutSession   { data, durata, xp, serie[ {esercizio, peso, reps} ] }
WeightHistory    { esercizio → [ {data, kg, serie} ] }
Taste (esercizi) { esercizio → { punteggio, conteggio, storico } }

NutritionProfile { obiettivo, kcal, macro, dieta, allergie[], esclusi[], tempoMax, porzioni }
Equipment        { fornelli, forno, microonde, friggitriceAria, pentolaPressione, ... }
PantryItem       { ingrediente, quantità, unità, luogo, scadenza }
Recipe           { id, nome, ingredienti[], passaggi[], tempo, attrezzi[], cucina, tag[], macro, foto }
FoodTaste        { ricette, ingredienti, cucine, metodiCottura, sapori → punteggio }
MealPlan         { settimana → giorni[ { pasti[ {tipo, ricettaId, bloccato} ] } ] }
ShoppingList     { piano, articoli[ {ingrediente, quantità, reparto, spuntato} ] }
MealLog          { data, pasto, ricettaId | manuale, kcal, macro }
```

### 12.2 Archiviazione
- **Locale** (sul dispositivo) per tutto ciò che è personale; per i dati più voluminosi (ricette, dispensa, storico) si usa **IndexedDB** invece di localStorage.
- **Cloud** (opzionale) solo per account, amici, classifica e sfide.
- Funzionamento **offline-first**: ricette e piano già scaricati restano utilizzabili senza connessione.

---

## 13. Fonti dati ed esterne

| Esigenza | Candidati | Note |
|---|---|---|
| Esercizi, immagini, muscoli | **wger.de** | Gratuita, open source; database locale di riserva |
| Ricette | **TheMealDB**, **Spoonacular**, **Edamam** | Da valutare per copertura, lingua italiana, limiti del piano gratuito e licenza d'uso |
| Prodotti e codici a barre | **Open Food Facts** | Gratuito, aperto; qualità variabile per prodotto |
| Valori nutrizionali | Open Food Facts, **USDA FoodData Central** | Per ingredienti generici |
| Ricette proprie | Archivio locale curato | Soluzione di base per le ricette italiane e per le varianti per attrezzo |

Principio: l'app deve funzionare con un **nucleo di ricette incluso** e usare le API per ampliare il catalogo, così da non dipendere da un singolo servizio.

---

## 14. Architettura e piattaforma

**Percorso scelto**

```
Web app (HTML/CSS/JS)  →  Capacitor  →  APK / AAB Android
```

- Un'unica base di codice riusabile come **PWA** e come app Android (ed eventualmente iOS).
- **Capacitor** per il packaging nativo: icona, splash, notifiche locali, vibrazione, fotocamera (scanner codice a barre), accesso alle impostazioni.
- Plugin nativi utili: notifiche locali (promemoria allenamento, scadenze, spesa), scanner barcode, condivisione, haptics.

**Alternative valutate**

| Opzione | Valutazione |
|---|---|
| Unity | Sproporzionata per un'app di tracking/gestione dati |
| Kivy / BeeWare (Python) | Peggior rapporto sforzo/risultato rispetto al web |
| Flutter / React Native | Valide, ma richiedono di riscrivere tutto da zero |

---

## 15. Navigazione e schermate

```
Home          Allenamento · Sport del giorno · Prossimo pasto
Allena        Gruppi muscolari · Scheda · Allenamento attivo · Storico pesi
Cucina        Cosa cucino adesso · Piano settimanale · Ricette · Dispensa · Lista della spesa
Sfide         Sfide attive · Badge · Classifica amici
Profilo       Dati personali · Obiettivi · Attrezzi · Dieta · Gusti · Impostazioni
```

---

## 16. Design

- **Stile**: dark, energetico, da videogioco; per la sezione cucina stessa palette ma con più spazio alle foto dei piatti.
- **Palette**: sfondo `#0A0A0F`, rosso `#FF3C3C`, arancio `#FF8C00`, ciano `#00E5FF`, oro `#FFD700`, verde `#00E676`, viola `#7C3AED`.
- **Font**: Bebas Neue (titoli e numeri), DM Sans (testo).
- **Interazioni chiave**: popup XP animato, toast di conferma, anello di riposo, passaggi di ricetta a schermo intero con timer, spunta animata nella lista della spesa.
- **Mobile-first**, usabile con una mano, aree toccabili ampie.

---

## 17. Roadmap

### Fase 1 — MVP allenamento
- [x] Allenamento per serie con riposo skippabile e pesi
- [x] XP, livelli, streak, badge *(6 badge di allenamento; quelli di nutrizione arrivano nelle fasi successive)*
- [x] Sport del giorno con XP
- [x] Preferenze esercizi
- [x] Schede personalizzate salvate
- [x] Esercizi da wger con immagini e fallback locale *(codice scritto ma non verificato: vedi sezione 19.3; il fallback locale ha solo testo, senza immagini)*
- [x] Profilo modificabile
- [ ] Packaging Android con Capacitor

### Fase 2 — Nutrizione base
- [x] Profilo nutrizionale, dieta, allergie
- [x] Checklist attrezzatura di cucina
- [x] Catalogo ricette *(45 ricette locali, 10 cucine, emoji al posto delle foto; manca l'integrazione con API: vedi 19.5)*
- [x] Dispensa manuale con scadenze
- [x] Gusti alimentari con quiz iniziale *(quiz con emoji per cucina, senza foto)*
- [x] "Cosa cucino adesso?" con filtro per attrezzi e ingredienti

### Fase 3 — Pianificazione
- [x] Piano pasti settimanale con macro e varietà
- [x] Lista della spesa automatica con sottrazione dispensa e reparti
- [x] Integrazione allenamento ↔ pasti (pre/post workout, giorni gambe/riposo)
- [x] Registro pasti e gamification nutrizionale
- [x] Modalità "cucina ridotta" *(solo microonde)*

### Fase 4 — Social e rifinitura
- [ ] Account e backend (Firebase/Supabase) *(non fatto: per ora sostituito da codici scambiati a mano, vedi 19.6)*
- [x] Amici, classifica, sfide a tempo *(via codici, senza server: la classifica "reale" resta da fare col backend)*
- [x] Condivisione di ricette, piani e liste *(codici da incollare; lista come testo)*
- [x] Scanner codice a barre per la dispensa *(solo nella versione PWA, per dispensa e registro pasti)*
- [x] Notifiche *(promemoria in app e notifiche del browser all'apertura; quelle programmate richiedono Capacitor)*
- [x] Backup/ripristino dati *(locale, esporta/importa; backup cloud non fatto)*
- [ ] Pubblicazione su Play Store

### Idee future
- [ ] Integrazione con Google Fit / Health Connect per rilevare sport e passi in automatico
- [ ] Suggerimenti di sostituzione ingredienti ("non hai il latte? usa…")
- [ ] Modalità famiglia con gusti e porzioni per più persone
- [ ] Controllo del budget e confronto prezzi
- [ ] Foto del frigo per riconoscere gli ingredienti
- [ ] Avatar e temi sbloccabili con i livelli
- [ ] Stagioni con classifiche a tempo
- [ ] Multilingua

---

## 18. Rischi e decisioni aperte

| Tema | Domanda / rischio |
|---|---|
| **Fonte ricette** | Quale API o archivio offre ricette in italiano, con licenza compatibile e limiti accettabili? |
| **Qualità dati nutrizionali** | I valori per porzione sono stime: vanno presentati come indicativi. |
| **Complessità del piano pasti** | Rispettare macro, gusti, attrezzi e varietà insieme è un problema di ottimizzazione: partire con regole semplici e migliorare per iterazioni. |
| **Dispensa** | Mantenerla aggiornata richiede impegno: ridurre l'attrito con scanner, "ingredienti sempre presenti" e scalatura automatica. |
| **Salute** | Contenuti nutrizionali richiedono avvisi e limiti di sicurezza chiari (sezione 9.10). |
| **Privacy** | Dati di salute e abitudini alimentari restano locali per impostazione predefinita; la parte cloud è facoltativa. |
| **Costi** | Le API gratuite hanno limiti: servono cache locale e catalogo di base incluso. |

---

## 19. Stato di implementazione

*Aggiornato al 10 novembre 2026.*

**Prototipo:** un unico file `gymarena.html` (HTML/CSS/JS senza dipendenze, solo Google Fonts), pubblicato come pagina web. Dati salvati in `localStorage`. Non è ancora stato provato su un dispositivo reale. È stato verificato con uno smoke test automatico su DOM simulato (viste, flussi, filtri di sicurezza, streak, XP), non incluso nel progetto.

### 19.1 Fatto (Fase 1)

- **Home**: livello, barra XP, sessioni, streak, badge, grafico dell'attività degli ultimi 7 giorni, sport del giorno.
- **Allenamento attivo**: un tap per serie, peso precompilato con l'ultimo usato (pulsanti ±2,5 kg), timer di riposo ad anello e skippabile (30/60/90/120 s) con vibrazione e suono, timer totale, pallini di avanzamento, valutazione ❤️/😐/💀 a fine esercizio, riepilogo finale.
- **Gamification**: livello `N+1` a `N × 500` XP, XP per serie (`XP esercizio ÷ serie`), +100 a fine allenamento, streak di allenamento, badge Streak 7, 10/50/100 sessioni, AI Master, Multi-Sport.
- **Sport del giorno**: tabella della sezione 5, XP una volta per sport al giorno, effetto reale sulle serie (−1 o −2, minimo 2) del gruppo affaticato.
- **Preferenze**: formula `nuovo = vecchio × 0.4 + voto × 0.6`, preferiti (≥ 60, tag AI▲) in cima, evitati (< −20) in fondo ed esclusi dall'allenamento, barra di affinità per gruppo, pagina "Gusti".
- **Pesi**: peso per serie con data, ultimo peso, record, trend ▲/▼ e mini-grafico per esercizio, suggerimento +2,5 kg dopo 3 sessioni senza aumento di peso.
- **Schede**: giorni (2–5), durata (30/45/60/90) e obiettivo (forza, ipertrofia, resistenza, dimagrimento, full body); scheda salvata, avvio di un'intera giornata, sostituzione dei singoli esercizi, stima dei minuti.
- **Profilo**: nome, avatar, peso, altezza, età, sesso, esperienza, obiettivo; esportazione, importazione e azzeramento dei dati.
- **Esercizi**: 30 esercizi locali (5 per gruppo) con suggerimento tecnico.
- **wger**: ricerca per esercizio, 2 immagini alternate, muscoli e descrizione, con cache locale.

### 19.2 Scelte implementative (differenze o dettagli rispetto alle specifiche)

| Tema | Scelta |
|---|---|
| Archiviazione | `localStorage` invece di IndexedDB: il volume è ancora piccolo. Da migrare quando crescono catalogo ricette e storico. |
| Livello | `livello = floor(XP / 500) + 1`. |
| Allenamento di gruppo | Primi 4 esercizi per gusto; il Full Body ne prende 1 per gruppo. |
| Sport multipli | Più sport nello stesso giorno sono ammessi, con XP una sola volta per sport. Se togli uno sport, gli XP vengono ritirati. Scegliere Riposo deseleziona gli altri e ritira i loro XP. |
| Riposo e streak | Scegliere Riposo registra un giorno di riposo che non spezza la streak. |
| Scheda | Serie per durata: 2 (≤30 min), 3 (≤45), 4 (oltre). Ripetizioni per obiettivo: forza 5, ipertrofia 10, resistenza 18, dimagrimento 14. Numero di esercizi = `(durata − 5) / tempo per esercizio`, tra 3 e 8. Full body come obiettivo: tutti i gruppi in ogni giornata. |
| Dati del profilo | Peso, altezza, età e sesso alimentano il fabbisogno stimato (Mifflin-St Jeor × (1,375 + 0,04 per allenamento negli ultimi 7 giorni, max 5); −15% dimagrire, +10% massa; minimo 1200 kcal F / 1500 kcal M). |
| Avviso a fine riposo | Vibrazione e un breve suono generato dal browser. |

### 19.3 Fatto (Fasi 2 e 3)

- **Cucina** (nuova scheda): hub con "Cosa cucino adesso?", dispensa, dieta e attrezzi, quiz gusti, piano, spesa, cucina ridotta.
- **Profilo nutrizionale**: obiettivo, dieta (onnivora, vegetariana, vegana, pescetariana, senza glutine, senza lattosio), allergie (glutine, lattosio, uova, pesce, frutta a guscio), ingredienti esclusi, tempo massimo, fabbisogno stimato. Allergie, dieta ed esclusi sono filtri bloccanti anche per il piano.
- **Attrezzatura**: checklist di 9 voci; le ricette richiedono uno o più attrezzi (alternative con "o", es. forno o friggitrice).
- **Ricette**: 45 ricette locali (italiana, mediterranea, messicana, asiatica, indiana, thai, giapponese, greca, spagnola, francese, colazioni) con tag di allergeni, macro per porzione, passaggi e vista "Ho cucinato".
- **Dispensa**: nome, quantità, luogo, scadenza, avviso a 3 giorni; gli ingredienti usati scalano di 1 quando cucini.
- **Gusti alimentari**: voto ❤️/😐/💀 con formula `nuovo = vecchio × 0.4 + voto × 0.6` su ricetta (peso doppio), cucina e ingredienti (voto dimezzato); quiz iniziale; le ricette evitate (< −20) spariscono dai suggerimenti.
- **Cosa cucino adesso?**: punteggio `0.40 ingredienti + 0.30 gusto + 0.15 macro + 0.15 scadenze`; viste Per te, Subito, Manca 1, Svuota-frigo, ≤15 min, Post-workout.
- **Piano settimanale**: 7 giorni × colazione, pranzo, cena; fabbisogno per giorno (+10% giorno gambe, +5% altro allenamento, −5% riposo, +10% se oggi hai fatto sport intenso); varietà (penalità oltre 2 usi di proteina o cucina); blocco 🔒, cambio ↻, "mangio fuori" 🍴 con kcal, scambio col giorno dopo ⇄, avanzi ♻️ (cena → pranzo), limite di tempo per giorno ⏱, giorno libero 🎉; pasti pre/post workout in base all'orario della sessione; rigenerazione parziale (per pasto e da un giorno in poi).
- **Registro e gamification**: ✓ per pasto (non nei giorni futuri), +50 XP per giornata rispettata, streak alimentare separata (il giorno libero non la spezza), +20/+40 XP per piatto cucinato (+40 con ingredienti in scadenza), +30 XP a lista completata, badge Primo piatto, Chef del mondo, Settimana perfetta.
- **Lista della spesa**: somma gli ingredienti dei pasti non ancora mangiati (3 o 7 giorni), sottrae la dispensa, raggruppa per reparto, quantità stimate per porzione, articoli extra, condivisione come testo, chiusura con ingresso in dispensa e scadenza stimata, segnalazione "formato grande" da 3 usi.

**Rifiniture (secondo giro)**
- **Cucina ora**: passaggi uno alla volta a schermo, con timer automatico quando il passaggio indica una durata ("N min") e vibrazione a fine timer.
- **Porzioni e varianti**: scelta 1–4 porzioni con quantità stimate; varianti per attrezzo (es. pollo: friggitrice 18 min a 200° o forno 35 min) per le ricette che le prevedono.
- **Gusti**: il voto si propaga anche a metodo di cottura (forno, friggitrice, padella, crudo, frullato) e profilo di sapore (piccante, cremoso, dolce, leggero); pagina "I miei gusti" con tutti i punteggi modificabili a mano o azzerabili; quota di novità (~12% delle scelte del piano, tag "✨ novità" per le cucine mai valutate).
- **Macro**: target in % kcal modificabili (default per obiettivo), grammi stimati, peso nel punteggio delle ricette e del piano; fabbisogno corretto dagli allenamenti recenti; opzione "Nascondi calorie".
- **Sfide e badge**: Sfida dispensa (3 ricette con tutti gli ingredienti in casa, +60 XP), Mangia l'arcobaleno (5 colori in 7 giorni, +50 XP), badge Zero sprechi (10 ingredienti in scadenza usati) e Padrone di casa (cucinato con tutti gli attrezzi posseduti tra fornelli, forno, microonde, friggitrice, frullatore).
- **Home**: card "Prossimo pasto" dal piano.

### 19.4 Scelte implementative (Fasi 2 e 3)

| Tema | Scelta |
|---|---|
| Sicurezza | Se nessuna ricetta compatibile esiste per un pasto, il piano lo segna "mangio fuori": allergie e dieta non vengono mai rilassate. |
| Quantità | Le ricette non hanno quantità: la dispensa conta porzioni e la spesa mostra una stima in g/ml/pz per ingrediente. |
| Giorni di allenamento nel piano | Distribuiti in modo uniforme sulla settimana in base ai giorni della scheda, non legati a date scelte dall'utente. |
| Ingredienti sempre presenti | Sale, olio e pepe sono ignorati dalle ricette; l'elenco non è ancora configurabile. |
| Correzioni dopo il test | Campo "ingredienti esclusi" svuotato bloccava la scheda Cucina; piano e quiz potevano proporre ricette non compatibili con dieta o allergie quando il filtro non lasciava risultati; la vista ricetta falliva con id non valido; articoli extra con apostrofi rompevano i pulsanti. |
| Foto | Le pagine pubblicate bloccano le immagini remote: al posto delle foto c'è un'emoji per cucina. |
| Metodo e sapore | Derivati automaticamente da attrezzi e ingredienti della ricetta, non assegnati a mano. |
| Padrone di casa | Conta solo gli attrezzi usati da almeno una ricetta; pentola a pressione, slow cooker, robot e bilancia non hanno ricette. |

### 19.5 Limiti noti e da fare

- **wger non verificato.** Le pagine pubblicate bloccano le richieste verso altri siti, quindi nell'anteprima si vede solo il testo. Va provato su un hosting proprio, in locale o dentro Capacitor. Ogni esercizio è associato a un termine di ricerca in inglese e la prima corrispondenza viene usata: alcune associazioni potrebbero essere imprecise. La descrizione può risultare in inglese. Manca ancora un fallback locale con immagini.
- **Ricette**: nessuna integrazione con API (TheMealDB, Spoonacular, Edamam): richiede la traduzione degli ingredienti in italiano per far funzionare dispensa e spesa, e non è verificabile dall'anteprima, che blocca le richieste esterne. Nessuna foto reale. Le quantità sono stime per ingrediente, non valori per ricetta.
- **Dispensa**: niente scanner codice a barre, niente ingredienti sempre presenti configurabili, niente avvisi di scadenza come notifica (servono Capacitor e notifiche locali).
- **Piano e registro**: costo stimato e meal prep multi-porzione non gestiti.
- **Sfide**: solo quelle nutrizionali di base; mancano le sfide a tempo tra amici (Fase 4).
- **Packaging Android con Capacitor**: non fatto.
- **Impostazioni mancanti**: lingua.
- **Da provare**: uso reale in palestra e in cucina, comportamento offline, salvataggio dei dati su più giorni, prestazioni con piano e dispensa grandi.
- **Fasi 4 e successive**: account, amici, classifica, sfide, notifiche, backup cloud, pubblicazione.

### 19.6 Fase 4 (parziale)

- **Amici** (nuova scheda): codice amico `GA1:` con sole statistiche aggregate (nome, avatar, livello, XP, sessioni, ricette, streak, badge). Incollando il codice di un amico lo si aggiunge o lo si aggiorna; classifica per XP con medaglie 🥇🥈🥉.
- **Sfide a tempo**: contro un amico, su XP guadagnati, allenamenti o ricette cucinate, per 3/7/14 giorni. I punti dell'amico si aggiornano reimportando il suo codice. A fine sfida +60 XP a chi ha partecipato, anche se perde.
- **Condivisione**: ricetta (`GR1:`) dalla pagina ricetta; piano settimanale (`GP1:`) dalla pagina piano. Un piano importato rispetta dieta e allergie di chi lo riceve: i pasti non compatibili diventano "mangio fuori". La lista della spesa si condivide già come testo.
- **Promemoria**: card in Home per ingredienti in scadenza e streak a rischio; opzione "Notifiche sul dispositivo" nel Profilo (una al giorno, all'apertura dell'app).

**Scelta**: niente server per ora. Il codice scambiato a mano mantiene i dati sul dispositivo (privacy) e funziona offline, ma non c'è aggiornamento automatico né verifica dei punteggi: chi vuole può barare. Per classifica reale e sfide sincronizzate serve il backend.

**Non fatto**: account e backend, notifiche programmate ad app chiusa, backup cloud, Capacitor e Play Store. Non provato su dispositivo.

**Scanner codice a barre (versione PWA)**: dalla Dispensa, 📷 apre la fotocamera (API `BarcodeDetector`: Chrome su Android; non Safari) oppure si scrive il codice a mano. Il nome viene cercato su Open Food Facts e proposto come ingrediente: se contiene un ingrediente delle ricette (es. "pasta") viene suggerito quello, altrimenti resta il nome del prodotto, che non verrà abbinato alle ricette finché non lo si rinomina. L'aggiunta richiede sempre conferma. I prodotti già cercati si salvano sul dispositivo. Non provato.

**Registro pasti (cucina → 📒 Registro)**: riepilogo di oggi con kcal e macro rispetto al target (barre morbide, nascosto con "Nascondi calorie"); "Ho mangiato il piano di oggi" segna i pasti rimasti; "Ho mangiato altro" con nome, kcal e macro a mano oppure da codice a barre (valori per 100 g di Open Food Facts scalati sui grammi indicati, dalla versione PWA). Contano nel totale anche i pasti del piano mangiati e quelli "fuori" con kcal indicate. Elenco degli ultimi 7 giorni. Le voci "altro" non danno XP e non incidono su streak e giornata rispettata. Valori indicativi, non provato.

**Peso corporeo e impostazioni (versione PWA)**: nella scheda Pesi, card facoltativa "Peso corporeo" con registrazione, mini-grafico e differenza rispetto a una settimana prima; aggiorna anche il peso del profilo (e quindi il fabbisogno stimato). Si nasconde con "Nascondi calorie". Nel Profilo: unità **kg/lb** (pesi degli esercizi e peso corporeo; internamente sempre in kg; il campo "Peso" del profilo resta in kg) e tema **scuro / chiaro / automatico**.

**wger**: sotto l'immagine compare il nome dell'esercizio trovato e il pulsante **↻ Altro**, che passa al risultato successivo della ricerca e ricorda la scelta per quell'esercizio. Serve a correggere a mano gli abbinamenti sbagliati; la verifica vera sul sito pubblicato resta da fare.
