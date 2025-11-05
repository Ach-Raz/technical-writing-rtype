# 🤖 Linee Guida per l'Uso di AI Companion - Progetto Arrowhead

## **1.0 Scopo del Documento**

Questo documento stabilisce le linee guida e le best practice per l'utilizzo di strumenti di intelligenza artificiale (AI Companion) a supporto dello sviluppo del "Progetto Arrowhead". L'obiettivo è massimizzare l'efficienza, la qualità del codice e la creatività, minimizzando al contempo i rischi associati, come l'introduzione di bug, vulnerabilità di sicurezza o codice non ottimizzato.

## **2.0 Principi Fondamentali**

1. **L'AI è un Assistente, non il Lead Developer:** L'AI è un potente strumento di "pair programming". Il developer umano ha sempre la responsabilità finale sul codice, sulla sua qualità e sul suo corretto funzionamento.
2. **Il Pensiero Critico Viene Prima di Tutto:** Comprendi il problema che stai cercando di risolvere prima di chiedere aiuto all'AI. Non usare l'AI come una scorciatoia per evitare di comprendere la logica di programmazione.
3. **Verifica, Non Fidarti Ciecamente:** Tutto il codice generato dall'AI deve essere attentamente revisionato, testato e compreso. L'AI può generare codice obsoleto, inefficiente o palesemente errato.
4. **Sicurezza e Privacy:** Non inserire mai dati sensibili, chiavi API, password o logiche di business proprietarie nei prompt degli AI Companion, specialmente se basati su modelli cloud pubblici.

## **3.0 Casi d'Uso Approvati (Cosa FARE ✅)**

L'uso dell'AI Companion è incoraggiato per le seguenti attività:

- **Scrittura di Codice Boilerplate:**
    - **Esempio:** "Crea una classe JavaScript `Enemy` con un costruttore che accetta `x`, `y`, `speed` e un metodo `draw(context)` per disegnarlo su un canvas HTML5."
- **Sviluppo di Algoritmi e Funzioni Specifiche:**
    - **Esempio:** "Scrivi una funzione JavaScript pura per il rilevamento delle collisioni tra due rettangoli, dati i loro oggetti con proprietà `x`, `y`, `width`, `height`."
- **Debugging e Refactoring:**
    - **Esempio:** "Il mio `WaveCannon` non si ricarica correttamente. Ecco il codice della funzione `charge()`. Riesci a individuare un potenziale errore logico?"
    - **Esempio:** "Suggerisci un modo per refattorizzare questo ciclo `for` per renderlo più leggibile usando i metodi `map` o `forEach`."
- **Scrittura di Documentazione e Commenti:**
    - **Esempio:** "Genera commenti in stile JSDoc per questa funzione, spiegando i parametri di input e il valore di ritorno."
- **Creazione di Test Unitari:**
    - **Esempio:** "Scrivi uno scheletro di test unitario per la funzione `player.move(direction)` per verificare che la posizione del giocatore venga aggiornata correttamente."

## **4.0 Pratiche da Evitare (Cosa NON FARE ❌)**

- **Non Fare "Copia e Incolla" Cieco:** Non integrare mai codice nel progetto senza averne compreso appieno il funzionamento, l'impatto e le potenziali implicazioni.
- **Non Sostituire la Fase di Progettazione:** Non chiedere all'AI di progettare intere architetture o sistemi complessi (es. "Costruisci il motore di gioco"). L'AI va usata per risolvere problemi ben definiti all'interno di un'architettura già progettata da un umano.
- **Non Ignorare le Convenzioni del Progetto:** Il codice generato deve essere adattato per rispettare lo stile di codifica, le convenzioni di denominazione e l'architettura del "Progetto Arrowhead".
- **Non Affidargli la Logica di Business Critica:** La logica fondamentale del gioco (es. il sistema di punteggio, la progressione dei livelli) dovrebbe essere scritta e compresa a fondo dai developer, anche se l'AI può aiutare a implementarla.

## **5.0 Workflow Consigliato**

1. **Definisci il Compito:** Il developer scompone un problema in un task piccolo e specifico.
2. **Scrivi un Prompt Efficace:** Formula una richiesta chiara e contestualizzata all'AI.
    - **Prompt SCORRETTO:** `// fai un nemico`
    - **Prompt CORRETTO:** `// Scrivi una funzione JS che aggiorna la posizione di un nemico. L'oggetto nemico ha x, y, speed. Deve muoversi da destra a sinistra e, una volta uscito dallo schermo a sinistra, riapparire a destra.`
3. **Analizza e Comprendi:** Esamina il suggerimento dell'AI. Capisci *perché* funziona in quel modo.
4. **Adatta e Integra:** Modifica il codice per adattarlo perfettamente al progetto, correggendo eventuali errori o inefficienze.
5. **Testa Rigorosamente:** Sottoponi il codice a test approfonditi come se lo avessi scritto interamente tu.
6. **Commit:** Esegui il commit del codice, assumendotene la piena responsabilità. Nella revisione del codice, il fatto che sia stato generato con l'AI è irrilevante; conta solo la sua qualità.
