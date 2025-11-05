# ⚙️ Template di Analisi Tecnica: Project Arrowhead

**_
1. Introduzione e Obiettivi Tecnici**

1.1 Scopo del Documento: Descrivere l'approccio tecnico e le decisioni di design per implementare l'MVP del videogioco horizontally scrolling shooter Project Arrowhead, in linea con i requisiti del PRD e le meccaniche di *R-Type*.
1.2 Piattaforma e Stack Tecnologico:
• **Motore di Gioco:** **Godot Engine (Versione 4.x)**, per la sua robustezza nel 2D e il supporto multipiattaforma.
• **Linguaggio di Programmazione:** **GDScript**, per l'integrazione nativa con Godot e la velocità di prototipazione.
• **Target:** **PC (Windows/Linux/macOS)**, utilizzando l'esportazione nativa di Godot.
1.3 Obiettivi di Performance:
• **Target di frame rate:** **60 FPS stabili** (RNF-01). Ottenuto ottimizzando l'uso di $\_process$ e $set\_process(false)$ quando possibile.
• **Tempo di risposta dei controlli:** **Inferiore a 50ms** (RNF-02), gestendo l'input nel metodo $\_input$ o $set\_process(false)$ in Godot.

**2. Architettura e Struttura del Codice**

2.1 Pattern di Design:
• Implementazione dei sistemi di gioco (es. Controller della navicella, Spawner dei nemici, Punteggio) utilizzando il pattern **Component/Entity System** (caratteristico di Godot, dove i nodi fungono da componenti e le scene da entità) e **Singleton per Manager** (Node Autoload in Godot, es. `GameManager`, `ScoreManager`).
• Gestione degli stati di gioco (Menu, Gameplay, Pausa, Game Over) tramite un **State Machine** (utilizzando un nodo di tipo $Node$ come base per la macchina a stati).
2.2 Struttura delle Scene/Livelli:
La singola scena/livello sarà composta da:
• `GameManager (Autoload)`: Gestisce il flusso del gioco (vittoria/sconfitta, spawn, transizioni di stato).
• `Player (R-9 Arrowhead)`: Navicella e Force.
• `EnemySpawner`: Logica di generazione dei nemici in base al tempo o alla posizione dello schermo, letta da un file di configurazione del livello (es. JSON o risorsa Godot `.tres`).
• `ScrollingBackground`: Gestione dello sfondo a scorrimento orizzontale (ParallaxBackground in Godot) con effetto parallasse.
• `UIManager`: Contiene l'HUD (vite, punteggio, Wave Cannon Charge) e gestisce le schermate `Main Menu` e `Game Over`.
2.3 Asset Management:
Strategia per il caricamento degli asset (Texture, Sprite, Audio) per minimizzare i tempi di caricamento: Pre-caricamento (Preloading) di tutti gli asset del livello all'avvio della scena (come richiesto dal vincolo). Utilizzo di Object Pooling per proiettili, nemici base ed effetti particellari per ridurre l'overhead di istanziazione e de-istanziazione a runtime.

**3. Sistemi di Gioco Principali (MVP)**

**3.1 🚀 Navicella (R-9 "Arrowhead") e Controlli**
**Componente TecnicaDescrizione dell'ImplementazioneMovimento**`CharacterBody2D` di Godot, con controllo diretto della velocità (non basato sulla fisica ad hoc per evitare variazioni di velocità). Utilizzo di $Input.get\_vector$ per movimento fluido e indipendente dal framerate.**Limiti di Schermo**Calcolo dei confini della `Viewport` per limitare la posizione della navicella (Clamp sul *trasformer*). I limiti saranno definiti una sola volta all'avvio del livello per ottimizzare.**Collisioni (Navicella-Nemico/Proiettile)**Utilizzo di `Area2D` come `Hitbox` sottile per la navicella. Segnalazione del segnale `area_entered` per l'evento di contatto. Implementazione del meccanismo di morte al singolo colpo e gestione del **Respawn** con un timer per i *invincibility frames* temporanei.

**3.2 💥 Sistema d'Arma**
**Componente TecnicaDescrizione dell'ImplementazioneStandard ShotPooling** di proiettili (PackedScene) per evitare l'instanziazione continua. Frequenza di fuoco (`fireRate`) controllata da un timer interno (`Timer` Node).**Wave Cannon (Carica)**Stato del Cannone: **[Scarico, Carica In Corso, Pronto al Fuoco]**. Variabile `float chargeTimer` per tracciare il tempo di pressione del tasto. Visualizzazione di un **indicatore di carica** (UI Node) sincronizzato con `chargeTimer`. Rilascio di un proiettile diverso e più potente al raggiungimento della carica massima (2 secondi).

**3.3 🔮 Meccanica del "Force"**
**Componente TecnicaDescrizione dell'ImplementazioneAggancio/Sgancio**La navicella ha un riferimento al Force. **Aggancio** tramite *Parenting* al `Node2D` della navicella (davanti o dietro) e aggiornamento della posizione relativa. **Sgancio** tramite *Deparenting* e attivazione di un componente di movimento indipendente.**Movimento Force Indipendente**Il Force segue la navicella **in linea retta (vettore)** fino alla distanza massima definita (es. 500 pixel). Una volta sganciato, il Force mantiene l'ultima direzione e velocità per un breve periodo prima di passare al movimento a "trazione" (riavvicinamento lento alla navicella).**Indistruttibilità e Blocco**Il Force ha un `Area2D` dedicato che intercetta i proiettili nemici. I proiettili nemici che colpiscono il Force vengono **distrutti immediatamente** (senza danni). Il Force non ha un componente Health.

**3.4 👾 Nemici e Interazione**

• **Nemico Base:**
    ◦ `Enemy AI Component`: Logica di movimento predefinita (es. entra da destra e segue un percorso **sinusoidale/lineare**) basata su `Tween` o $move\_and\_slide$ in Godot.
    ◦ `Health Component`: Punti vita del nemico. Morte istantanea (`HP = 0`).
    ◦ `Collision Handling`: Distruzione del nemico e attivazione del sistema di punteggio (`ScoreManager.add_score()`) all'impatto con un proiettile del giocatore/Force.
• **Boss di Fine Livello:**
    ◦ `Boss AI Component`: Implementazione di un pattern di attacco **multi-fase** (State Machine del Boss) con transizioni basate sulla % di HP.
    ◦ `Weak Point Logic`: Definizione di `Area2D` (punti deboli) specifici, figli del nodo Boss, che subiscono danni maggiori rispetto al corpo del Boss.
• **Sistema di Spawning:** Utilizzo di un **Object Pool** per nemici e proiettili (gestito da `EnemySpawner` e `WeaponManager`) per ottimizzare le prestazioni, come definito in 2.3.

**4. Ciclo di Gioco, UI e Punteggio**

4.1 Flusso di Gioco (MVP): **[Carica Livello] -> [Inizio Gioco] -> [Gameplay Loop (Combat, Scoring)] -> [Boss Battle] -> [Vittoria / Morte del Giocatore] -> [Respawn / Game Over] -> [Fine Livello / Restart o Uscita]**. Le transizioni saranno gestite dal `GameManager`.
4.2 Sistema di Punteggio: Variabile intera globale (`score`) gestita da un **Singleton** (`ScoreManager`). Aumento del punteggio (`ScoreManager.add_score(value)`) all'eliminazione di nemici. Salvataggio del punteggio più alto (`HighScore`) in un file utente (`user://`) per persistenza.
4.3 UI (Heads-Up Display - HUD):
• Implementato tramite la struttura di `Control` Nodes di Godot (`Label`, `ProgressBar`).
• **Visualizzazione del Punteggio Corrente:** `Label` aggiornato tramite segnale dal `ScoreManager`.
• **Visualizzazione del Contatore Vite:** `Label` o icone sprite (`TextureRect`) aggiornate tramite segnale dal `Player`.
• **Indicatore di Carica del Wave Cannon:** `ProgressBar` o barra grafica, aggiornato in tempo reale dal `WeaponComponent` della navicella.
• **Schermata di Game Over:** Scena UI dedicata, attivata dal `GameManager`, con visualizzazione del punteggio finale e opzione di riavvio.

**📝 Prossimi Passaggi e Deliverables Tecnici**

• **Definizione Esatta dello Stack:** Confermare Godot 4.x e GDScript come ambiente di sviluppo.
• **Prototipo di Movimento:** Creare un sandbox per testare la fluidità del movimento (60 FPS) e la logica di collisione/limiti dello schermo (`RF-01`, `RF-02`, `RNF-02`).
• **Prototipo del Force:** Implementare il meccanismo di aggancio/sgancio e il blocco dei proiettili (il cuore dell'esperienza) (`RF-07`, `RF-09`).
• **Implementazione del Pooling:** Costruire e testare il sistema di **Object Pooling** per proiettili e nemici per garantire le performance (RNF-01).
