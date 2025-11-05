# VERBALI

# 🧾 Verbale Slot 1 – Lunedì

**Visione Prodotto**

**Data Simulata:** Lunedì – Settimana 1

**Partecipanti:** Davide, Tommaso, Achraf

**Doc. Riferimento:** PRD (Product Requirement Document)

## 🔹 Obiettivo

Allineare la visione globale del prodotto e definire priorità MVP.

## 🔹 Decisioni Prese

1. Il progetto si chiama **Project Arrowhead**: horizontally scrolling shooter ispirato a *R-Type*.
2. Piattaforma target: **PC (Windows/macOS/Linux)**; esportazione Web valutata come obiettivo secondario.
3. Priorità MVP: movimento e controlli → sistema d’arma → meccanica Force → prototipo boss.

## 🔸 Action Items

| Assegnato a | Compito | Scadenza Simulata |
| --- | --- | --- |
| Davide | Redigere PRD completo (obiettivi, MVP, motivazione). | Lunedì |
| Tommaso | Raccolta reference visive/sonore. | Lunedì |
| Achraf | Definire palette e tono visivo. | Lunedì |

## 🧭 Note

- Concordata la roadmap a breve termine: documentazione completa entro fine settimana, quindi passaggio a prototipazione.

---

# 🧾 Verbale Slot 2 – Martedì

**Funzionalità Dettagliate**

**Data Simulata:** Martedì – Settimana 1

**Partecipanti:** Davide, Tommaso, Achraf

**Doc. Riferimento:** Analisi Funzionale

## 🔹 Obiettivo

Definire user stories, flussi di gioco e comportamento entità principali.

## 🔹 Decisioni Prese

1. Definizione dettagliata delle meccaniche giocatore: movimento 2D, sparo standard e Wave Cannon con carica.
2. Il **Force** sarà unità tattica con stati: agganciato (davanti/dietro), sganciato (movimento autonomo), blocco proiettili.
3. Primo livello: prototipo con nemici base e boss di fine livello.

## 🔸 Action Items

| Assegnato a | Compito | Scadenza Simulata |
| --- | --- | --- |
| Davide | Completare l’Analisi Funzionale (user stories e flussi). | Martedì |
| Tommaso | Storyboard livello 1 (spawn pattern). | Martedì |
| Achraf | Documento stato Force (descrizione e transizioni). | Martedì |

## 🧭 Note

- HUD minimale (vite, carica Wave, punteggio). Sarà dettagliato nella AF.

---

# 🧾 Verbale Slot 3 – Mercoledì

**Design Tecnico**

**Data Simulata:** Mercoledì – Settimana 1

**Partecipanti:** Davide, Tommaso, Achraf

**Doc. Riferimento:** Analisi Tecnica

## 🔹 Obiettivo

Scegliere architettura, pattern e struttura delle scene/nodi Godot.

## 🔹 Decisioni Prese

1. Stack: **Godot 4.x + GDScript** confermato.
2. Struttura classi: `Player.gd`, `Weapon.gd`, `Force.gd`, `Enemy.gd`, `Projectile.gd`.
3. Performance: Object Pooling obbligatorio per proiettili e nemici.
4. Collision Manager centralizzato per semplificare logica contact handling.

## 🔸 Action Items

| Assegnato a | Compito | Scadenza Simulata |
| --- | --- | --- |
| Davide | Scrivere sezione “Architettura e Classi” in AT. | Mercoledì |
| Tommaso | Definire struttura cartelle e naming convention Godot. | Mercoledì |
| Achraf | Implementare test di pooling in sandbox Godot. | Mercoledì |

## 🧭 Note

- Registrare log di sviluppo (`dev_log.txt`) per tracking bug durante prototipazione.

---

# 🧾 Verbale Slot 4 – Giovedì

**Supporto allo Sviluppo — Linee Guida AI Companion**

**Data Simulata:** Giovedì – Settimana 1

**Partecipanti:** Davide, Tommaso, Achraf

**Doc. Riferimento:** *Linee Guida per l'Uso di AI Companion* (documento fornito)

## 🔹 Obiettivo

Formalizzare e integrare le *Linee Guida per l'Uso di AI Companion* nel workflow del progetto e distribuirne la versione definitiva nel repository.

## 🔹 Decisioni Prese (rif. documento)

1. **AI = Assistente, non Lead Developer.** L'AI può aiutare (boilerplate, algoritmi specifici, test skeletons, debugging) ma il developer ha responsabilità finale.
2. **Workflow consigliato adottato ufficialmente:** definizione task → prompt efficace → analisi output → adattamento → test → commit. (Lo schema del documento è formalmente adottato come policy interna.)
3. **Casi d’uso approvati:** generazione boilerplate, funzioni pure (collision detection), suggerimenti per refactor, generazione di commenti/JSDoc, creazione scheletri test.
4. **Pratiche vietate:** copiare-output-AD-OC, chiedere all’AI di progettare intere architetture, affidare logiche di business critiche senza revisione umana, inserire dati sensibili nei prompt.
5. **Security & Privacy:** vietato includere API key, segreti o logiche proprietarie nei prompt; usare esempi anonimizzati se necessario.

## 🔸 Action Items

| Assegnato a | Compito | Scadenza Simulata |
| --- | --- | --- |
| Achraf | Finalizzare la Guida AI (testo + esempi di prompt corretti/errati) e inserirla in `/docs/guides/ai_companion.md`. | Giovedì |
| Davide | Scrivere sezione “Code Review Policy per output AI” (checklist obbligatoria prima del merge). | Giovedì |
| Tommaso | Configurare repository con template PR che richieda indicazione se parti di codice sono state generate dall’AI e checklist di test. | Giovedì |

## 🧭 Note e Azioni Operative

- Viene introdotta una **checklist obbligatoria** da usare in code review quando il PR contiene codice derivato/ispirato a output AI (comprensione, test, controllo performance, sicurezza).
- Esempi concreti da includere nella guida: prompt per movimento nemico, prompt per funzione collisione rettangoli, debug del `WaveCannon.charge()`.
- Si concorda: **nessun commit** contenente codice AI-generated verrà mergiato senza almeno un revisore umano che dichiari esplicitamente di aver eseguito la checklist.

---

# 🧾 Verbale Slot 5 – Venerdì

**Verbalizzazione e Decisioni Settimanali**

**Data Simulata:** Venerdì – Settimana 1

**Partecipanti:** Davide, Tommaso, Achraf

**Doc. Riferimento:** PRD, AF, AT, Guida AI Companion

## 🔹 Obiettivo

Raccogliere e consolidare le decisioni prese nella settimana e pianificare QA/revisione incrociata.

## 🔹 Decisioni Prese

1. Tutti i documenti principali (PRD, AF, AT, Guida AI) sono formalmente completati e messi in repo.
2. La Guida AI Companion è stata adottata come policy interna: obbligatoria per ogni uso di AI nel progetto.
3. Procedere con prototipo 1 in Godot: movimento + sparo standard + Force base + pooling.

## 🔸 Action Items

| Assegnato a | Compito | Scadenza Simulata |
| --- | --- | --- |
| Davide | Preparare checklist QA e creare `QA_review.md` con i test da eseguire su Prototipo 1. | Venerdì |
| Tommaso | Iniziare implementazione prototipo (Player movement + Weapon + Pooling). | Martedì (Settimana 2) |
| Achraf | Pubblicare la Guida AI nel repo e aggiungere template PR/checklist. | Venerdì |

## 🧭 Note

- Durante il merge request si dovrà indicare, tramite il template PR, se si sono usati strumenti AI e allegare la checklist di verifica.
- Prossimo step: slot QA per revisione incrociata dei documenti e apertura issue tecniche.

---

# 🧾 Verbale Slot QA – Revisione Incrociata (Revisione)

**Data Simulata:** Fine Settimana – Revisione incrociata

**Partecipanti:** Davide, Tommaso, Achraf

**Doc. Riferimento:** Tutti i documenti + checklist AI

## 🔹 Obiettivo

Eseguire revisione incrociata documenti e aprire issue per quanto non ancora completo.

## 🔹 Decisioni Prese

1. PRD, AF e AT approvati come coerenti con la vision.
2. Guida AI Companion approvata con le modifiche concordate (inserimento checklist PR, esempi di prompt).
3. Avviare prototipo 1 con backlog di issue note.

## 🔸 Issue Aperte (esempi)

| ID | Descrizione | Assegnato a | Stato |
| --- | --- | --- | --- |
| #001 | UML completo per `Force` non ancora allegato. | Davide | In corso |
| #002 | Verificare esportabilità HTML5 / Web Export. | Tommaso | Da testare |
| #003 | Aggiungere immagini esemplificative e sprite placeholder nel docs. | Achraf | Da fare |

## 🧭 Conclusione

Settimana 1 chiusa con documentazione pronta e policy AI integrata. Si procede a prototipazione tecnica con le regole d’uso AI chiaramente definite.