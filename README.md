# Fractal Architecture Framework (FAF)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/88x31.png)](./LICENSE)

Benvenuti nel repository ufficiale del **Fractal Architecture Framework (FAF)**: un insieme di convenzioni e tassonomie per la progettazione e l'organizzazione di codebase **TypeScript**.

Ispirato ai frattali naturali, FAF mappa la scomposizione logica di un sistema software sulla gerarchia di file e directory: creare una directory e denominare un file sono al contempo decisioni architetturali e atti di codifica (_Architecture is Code_). FAF non è una libreria né un runtime, bensì una specifica.

## Il Problema: la "Big Ball of Mud"

Molti progetti software, anche quelli iniziati con le migliori intenzioni, tendono a degenerare in quello che Brian Foote e Joseph Yoder hanno definito una **"Big Ball of Mud"**: sistemi la cui struttura è cresciuta in modo disordinato, fino a diventare un groviglio di codice rigido, fragile e difficile da far evolvere.

Per approfondire cause e conseguenze del fenomeno:

- **[Il problema: "Big Ball of Mud"](./BIG_BALL_OF_MUD.md)**

## La Risposta: il Fractal Architecture Framework

FAF accoglie la crescita incrementale che rende la Big Ball of Mud così diffusa, ma la vincola a un modello di accrescimento autosimile:

- **Contro il codice rigido**: ogni unità logica (_Fragment_) espone un'unica interfaccia pubblica (_Access Node_), mentre i dettagli implementativi restano incapsulati in _Private Categories_ e _Fractal Branches_. Le dipendenze formano un grafo aciclico e sono interdette tra pari, salvo ove disciplinate da una _Horizontal Hierarchy_ o dalle regole di visibilità dei singoli Logical Domains.
- **Contro il codice fragile**: ogni Fragment implementa un'unità coesa e ogni file qualifica la propria competenza tramite un _Role_ riconoscibile dal nome (es. `button.component.tsx`); i file con Role esplicito definiscono al più un Symbol, salvo i Roles per cui una Declaration ne ammette di più.
- **Per un'evoluzione controllata**: la struttura non è fissata a priori, ma converge progressivamente attraverso tre operazioni (_Estrazione_, _Promozione_, _Contrazione_), con un grado di scomposizione commisurato alla complessità del problema.

La specifica completa, con principi, leggi del Dependency Graph, tassonomia dei Logical Domains ed esempi di riferimento, è disponibile qui:

- **[Fractal Architecture Framework (FAF)](./FAF.md)**

## Stato del Progetto

### Working Draft

La specifica è una bozza in evoluzione (_Working Draft - 2 Novembre 2026_). La conformità a FAF richiede il rispetto di tutte le norme della specifica e di tutte le _Declarations_ dell'architetto, indipendentemente dagli strumenti di verifica adottati (es. analisi statica, _fitness functions_): il repository non fornisce strumenti di verifica automatica.

### Lingua della Specifica

Al momento, tutta la documentazione è disponibile **esclusivamente in lingua italiana**. È in lavorazione la traduzione completa in **inglese**, che verrà rilasciata non appena sarà pronta.

### Contribuire al Progetto

I contributi sono benvenuti: segnalazioni di refusi ed errata, chiarimenti, proposte di modifica della specifica e traduzione in inglese. Issue e pull request possono essere redatte in italiano o in inglese.

Prima di contribuire, consultare le linee guida:

- **[Contributing to FAF](./CONTRIBUTING.md)**

## Licenza

La documentazione è rilasciata sotto licenza Creative Commons Attribuzione 4.0 Internazionale. Le eventuali porzioni incorporate nel codice sorgente sono invece rilasciate sotto licenza BSD 3-Clause.

Per i dettagli completi, consultare il file:

- **[LICENSE](./LICENSE)**
