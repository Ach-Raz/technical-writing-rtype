# ⚙️ Documento di Analisi Funzionale – Project Arrowhead

---

## 1. Introduzione

### 1.1 Scopo del Documento

Il presente documento di **Analisi Funzionale** descrive il comportamento operativo, le logiche di gioco e le interazioni principali del videogioco *Project Arrowhead*.

Scopo del documento è fornire una descrizione strutturata e precisa delle **funzionalità da implementare**, costituendo un riferimento tecnico per lo sviluppo, il collaudo e la manutenzione del prodotto.

### 1.2 Ambito del Sistema

*Project Arrowhead* è un **videogioco arcade 2D a scorrimento orizzontale**, ispirato al classico *R-Type*, in cui il giocatore pilota la navicella R-9 Arrowhead contro orde di nemici spaziali.

Il sistema comprende:

- il **motore di gioco** con gestione fisica, eventi e collisioni;
- il **sistema grafico e sonoro** per la resa visiva e audio;
- l’**interfaccia utente (UI)** per menù, HUD e schermate di fine partita;
- la **logica di gameplay** (movimento, armi, nemici, boss, punteggio).

### 1.3 Attori Coinvolti

| Attore | Descrizione | Interazioni Principali |
| --- | --- | --- |
| **Giocatore** | L’utente che controlla la navicella R-9 Arrowhead. | Fornisce input da tastiera o gamepad, affronta nemici e raccoglie power-up. |
| **Sistema di Gioco** | Motore che gestisce logiche, eventi, collisioni e punteggi. | Elabora input, aggiorna lo stato del mondo di gioco e gestisce la progressione. |
| **Motore Grafico/Audio** | Componente responsabile della visualizzazione e del sonoro. | Renderizza sprite, effetti visivi e sonori sincronizzati con le azioni. |

---

## 2. Descrizione Generale

### 2.1 Contesto Operativo

Il gioco è progettato per piattaforme **Windows, Linux e macOS**, con esecuzione in modalità desktop.

Verrà realizzato con un **motore 2D moderno** (ad es. Godot o Unity), mantenendo uno stile grafico retro con animazioni fluide.

Il gameplay si basa su una progressione lineare: il giocatore attraversa un unico livello di difficoltà crescente fino allo scontro finale con il boss.

### 2.2 Vincoli e Dipendenze

- Input: tastiera e/o gamepad.
- Frame rate target: **60 FPS**.
- Risoluzione consigliata: **1920×1080** (scalabile).
- Il gioco non richiede connessione di rete.
- Tutti gli asset (sprite, suoni, UI) devono essere caricati in memoria all’avvio del livello.

---

## 3. Requisiti Funzionali

### 3.1 Movimento e Controlli della Navicella

| ID | Descrizione | Input | Output | Priorità |
| --- | --- | --- | --- | --- |
| RF-01 | Il giocatore può muovere la navicella lungo gli assi X e Y. | Frecce direzionali o analog stick. | Aggiornamento posizione e animazione movimento. | Alta |
| RF-02 | La navicella non può uscire dai limiti dello schermo. | Posizione oltre margini scena. | Blocco del movimento. | Alta |
| RF-03 | Collisione con nemici o proiettili causa la perdita di una vita. | Evento di contatto. | Riduzione vite, animazione esplosione, respawn o Game Over. | Alta |

---

### 3.2 Sistema d’Arma Principale

| ID | Descrizione | Condizione | Effetto | Priorità |
| --- | --- | --- | --- | --- |
| RF-04 | Il giocatore può sparare colpi standard. | Pressione del tasto “Fire”. | Generazione proiettile base con danno fisso. | Alta |
| RF-05 | Il giocatore può caricare il “Wave Cannon”. | Tasto “Fire” tenuto > 2 secondi. | Emissione colpo potenziato con maggiore danno. | Alta |
| RF-06 | I proiettili colpiscono nemici e ostacoli. | Collisione proiettile/nemico. | Distruzione nemico o riduzione energia boss. | Alta |

---

### 3.3 Meccanica del “Force”

| ID | Descrizione | Azione | Effetto | Priorità |
| --- | --- | --- | --- | --- |
| RF-07 | Il “Force” può agganciarsi davanti o dietro la navicella. | Tasto “Attach/Detach”. | Cambio posizione e potenziamento offensivo. | Alta |
| RF-08 | Il “Force” può muoversi autonomamente se sganciato. | Comando di rilascio. | Movimento indipendente, attacco automatico. | Media |
| RF-09 | Il “Force” può bloccare proiettili nemici standard. | Collisione proiettile/Force. | Distruzione del proiettile. | Alta |

---

### 3.4 Nemici e Interazioni

| ID | Descrizione | Condizione | Risultato |
| --- | --- | --- | --- |
| RF-10 | I nemici base seguono pattern di movimento predefiniti. | Avvio livello. | Movimento ciclico o diretto verso il giocatore. |
| RF-11 | I nemici possono sparare a intervalli regolari. | Timer interno. | Generazione proiettile nemico. |
| RF-12 | Il boss possiede pattern multipli e punti deboli. | Entrata nella zona finale. | Cambi di attacco, fasi multiple di combattimento. |

---

### 3.5 Ciclo di Gioco

| ID | Descrizione | Evento | Azione |
| --- | --- | --- | --- |
| RF-13 | All’avvio del livello la navicella viene posizionata al punto iniziale. | Start Game. | Spawn giocatore e nemici base. |
| RF-14 | La perdita di tutte le vite genera il Game Over. | Vite = 0. | Visualizzazione schermata Game Over. |
| RF-15 | Il punteggio aumenta in base ai nemici distrutti. | Evento “nemico distrutto”. | Aggiornamento punteggio e HUD. |

---

## 4. Requisiti Non Funzionali

| ID | Categoria | Descrizione |
| --- | --- | --- |
| RNF-01 | Performance | Il gioco deve mantenere un frame rate stabile di 60 FPS. |
| RNF-02 | Usabilità | I controlli devono essere fluidi, con risposta <100 ms. |
| RNF-03 | Affidabilità | Tutte le collisioni devono essere gestite senza bug. |
| RNF-04 | Manutenibilità | Codice modulare, commentato e organizzato per moduli (Input, Gameplay, UI). |
| RNF-05 | Portabilità | Compatibilità garantita su Windows, Linux e macOS. |

---

## 5. Flusso di Gioco

### 5.1 Descrizione del Flusso

1. **Avvio applicazione** → caricamento risorse e schermata iniziale.
2. **Main Menu** → opzioni “Start”, “Settings”, “Exit”.
3. **Start Game** → spawn navicella e nemici.
4. **Gameplay loop** → movimento, combattimento, punteggio, power-up.
5. **Boss Battle** → scontro finale con il boss principale.
6. **Fine livello** → schermata “Victory” o “Game Over”.
7. **Restart o uscita** → ritorno al menu principale.

### 5.2 Diagramma del Flusso

```
[Start] → [Main Menu] → [Level Start] → [Combat Loop] → [Boss Battle]
      ↓                                  ↓
   [Game Over] ←––––––––––––––––––––––– [Victory]

```

---

## 6. Interfaccia Utente

### 6.1 Schermate Principali

- **Main Menu:** logo del gioco, opzioni Start / Settings / Exit.
- **HUD di Gioco:**
    - Contatore vite residue.
    - Indicatore di carica “Wave Cannon”.
    - Punteggio attuale.
    - Barra energia boss (quando presente).
- **Game Over:** visualizzazione punteggio finale e opzione di riavvio.

### 6.2 Interazioni UI

- Navigazione menu tramite frecce e tasto “Enter” o pulsante “A”.
- Feedback visivo per selezioni attive.
- Tutti gli elementi devono mantenere leggibilità su risoluzioni 720p e superiori.

---

## 7. Glossario dei Termini

| Termine | Descrizione |
| --- | --- |
| **R-9 Arrowhead** | Navicella controllata dal giocatore. |
| **Force** | Unità secondaria che può essere agganciata o rilasciata per combattere. |
| **Wave Cannon** | Arma principale con possibilità di carica per colpi potenziati. |
| **Pattern di movimento** | Percorso predefinito di nemici o boss. |
| **HUD** | Interfaccia grafica che mostra vite, punteggio e stato del gioco. |

---

## 8. Allegati e Riferimenti

- Documento PRD: *Project Arrowhead – Product Requirements Document*
- Mockup UI e concept sprite (navicella, Force, boss)
- Diagrammi di stato e flussi di gioco (allegati al documento tecnico di sviluppo)

---
