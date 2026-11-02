# Fractal Architecture Framework (FAF)

**_Working Draft - 2 Novembre 2026_**

---

## 1. Abstract

Questa specifica descrive il _Fractal Architecture Framework_ (_FAF_), un insieme di convenzioni e tassonomie per la progettazione e l'organizzazione di codebase TypeScript. Ispirato ai frattali naturali, FAF mappa la scomposizione logica di un sistema software sulla gerarchia di file e directory: la creazione di una directory e la denominazione di un file costituiscono al contempo decisioni architetturali e atti di codifica (_Architecture is Code_).

### 1.1. Natura del Framework

FAF non è una libreria né un runtime, bensì la specializzazione per l'ecosistema TypeScript del paradigma _Fractal Architecture_, definito come l'applicazione ricorsiva del principio di autosimilarità all'organizzazione della codebase. Il framework condivide la finalità di una struttura autoesplicativa, tipica della _Screaming Architecture_, e l'approccio all'evoluzione incrementale proprio della _Evolutionary Architecture_.

### 1.2. Stato del Documento e Conformità

Questa specifica è una bozza in evoluzione.

Una _Declaration_ è una decisione architetturale formalmente dichiarata dall'architetto. Le Declarations costituiscono vincoli architetturali e integrano le convenzioni FAF.

Le prescrizioni FAF si distinguono in norme e raccomandazioni. Le raccomandazioni sono introdotte dalla formula _è raccomandato_; ogni altra prescrizione è una norma. La conformità richiede il rispetto di tutte le norme e di tutte le Declarations, indipendentemente dagli strumenti di verifica adottati (es. analisi statica, _fitness functions_). L'inosservanza di una raccomandazione non pregiudica la conformità.

---

## Table of Contents

- [Fractal Architecture Framework (FAF)](#fractal-architecture-framework-faf)
  - [1. Abstract](#1-abstract)
    - [1.1. Natura del Framework](#11-natura-del-framework)
    - [1.2. Stato del Documento e Conformità](#12-stato-del-documento-e-conformità)
  - [Table of Contents](#table-of-contents)
  - [2. Obiettivi](#2-obiettivi)
  - [3. Principi](#3-principi)
  - [4. Fondamenti](#4-fondamenti)
  - [5. Leggi del Dependency Graph](#5-leggi-del-dependency-graph)
  - [6. Tassonomia dei Logical Domains](#6-tassonomia-dei-logical-domains)
    - [6.1. Fragments](#61-fragments)
      - [6.1.1. Tassonomia dei Logical Nodes del Fragment](#611-tassonomia-dei-logical-nodes-del-fragment)
      - [6.1.2. Separazione delle Competenze e Univocità del Symbol](#612-separazione-delle-competenze-e-univocità-del-symbol)
      - [6.1.3. Horizontal Hierarchy Interna e Modello dei Roles](#613-horizontal-hierarchy-interna-e-modello-dei-roles)
        - [Modello di Riferimento per i Roles](#modello-di-riferimento-per-i-roles)
      - [6.1.4. Esempi di Riferimento](#614-esempi-di-riferimento)
        - [Esempio 6.1.4.1. Fragment con Role 'component' in un'applicazione React](#esempio-6141-fragment-con-role-component-in-unapplicazione-react)
        - [Esempio 6.1.4.2. Access Node di un Fragment con Role 'component'](#esempio-6142-access-node-di-un-fragment-con-role-component)
        - [Esempio 6.1.4.3. Fragment con Role 'hook'](#esempio-6143-fragment-con-role-hook)
        - [Esempio 6.1.4.4. Fragment con Role 'util'](#esempio-6144-fragment-con-role-util)
    - [6.2. Root Fragments](#62-root-fragments)
      - [6.2.1. Tassonomia dei Nodi del Root Fragment](#621-tassonomia-dei-nodi-del-root-fragment)
      - [6.2.2. Disciplina delle Dipendenze dei Root Nodes](#622-disciplina-delle-dipendenze-dei-root-nodes)
      - [6.2.3. Esempi di Riferimento](#623-esempi-di-riferimento)
        - [Esempio 6.2.3.1. Root Fragment in una Single Page Application (SPA)](#esempio-6231-root-fragment-in-una-single-page-application-spa)
        - [Esempio 6.2.3.2. Root Fragments gerarchici con File-System Routing (Next.js App Router)](#esempio-6232-root-fragments-gerarchici-con-file-system-routing-nextjs-app-router)
    - [6.3. Categories](#63-categories)
      - [6.3.1. Mutua Esclusività del Contenuto e Category Nodes](#631-mutua-esclusività-del-contenuto-e-category-nodes)
      - [6.3.2. Sub-Categories](#632-sub-categories)
      - [6.3.3. Private Categories](#633-private-categories)
      - [6.3.4. Horizontal Hierarchies per Categories e Sub-Categories](#634-horizontal-hierarchies-per-categories-e-sub-categories)
        - [Modelli di Riferimento per le Sub-Categories](#modelli-di-riferimento-per-le-sub-categories)
      - [6.3.5. Mimetic Path Structure e Path Sub-Categories](#635-mimetic-path-structure-e-path-sub-categories)
      - [6.3.6. Esempi di Riferimento](#636-esempi-di-riferimento)
        - [Esempio 6.3.6.1. Category di Fragments articolata in Sub-Categories (Atomic Design)](#esempio-6361-category-di-fragments-articolata-in-sub-categories-atomic-design)
        - [Esempio 6.3.6.2. Category di Category Nodes con Role esplicito e Sub-Categories](#esempio-6362-category-di-category-nodes-con-role-esplicito-e-sub-categories)
        - [Esempio 6.3.6.3. Category di Category Nodes con Role implicito](#esempio-6363-category-di-category-nodes-con-role-implicito)
        - [Esempio 6.3.6.4. Private Category in un Fragment](#esempio-6364-private-category-in-un-fragment)
        - [Esempio 6.3.6.5. Mimetic Path Structure per endpoint REST](#esempio-6365-mimetic-path-structure-per-endpoint-rest)
        - [Esempio 6.3.6.6. Mimetic Path Structure per routing programmatico di pagine](#esempio-6366-mimetic-path-structure-per-routing-programmatico-di-pagine)
    - [6.4. Layers](#64-layers)
      - [6.4.1. Anatomia Interna e Sub-Layers](#641-anatomia-interna-e-sub-layers)
      - [6.4.2. Horizontal Hierarchies tra Layers](#642-horizontal-hierarchies-tra-layers)
      - [6.4.3. Esempi di Riferimento](#643-esempi-di-riferimento)
        - [Esempio 6.4.3.1. Stratificazione in Layers ordinati da una Horizontal Hierarchy](#esempio-6431-stratificazione-in-layers-ordinati-da-una-horizontal-hierarchy)
    - [6.5. Root Layers](#65-root-layers)
      - [6.5.1. Anatomia Interna e Gerarchie](#651-anatomia-interna-e-gerarchie)
      - [6.5.2. Esempi di Riferimento](#652-esempi-di-riferimento)
        - [Esempio 6.5.2.1. Root Layer articolato in Categories](#esempio-6521-root-layer-articolato-in-categories)
        - [Esempio 6.5.2.2. Root Layer stratificato in Layers](#esempio-6522-root-layer-stratificato-in-layers)
    - [6.6. Fractal Branches](#66-fractal-branches)
      - [6.6.1. Anatomia Interna](#661-anatomia-interna)
      - [6.6.2. Visibilità Discendente Ricorsiva e Unidirezionalità](#662-visibilità-discendente-ricorsiva-e-unidirezionalità)
      - [6.6.3. Esempi di Riferimento](#663-esempi-di-riferimento)
        - [Esempio 6.6.3.1. Fractal Branch di un Root Fragment articolato in Layers](#esempio-6631-fractal-branch-di-un-root-fragment-articolato-in-layers)
        - [Esempio 6.6.3.2. Fractal Branch locale di un Fragment](#esempio-6632-fractal-branch-locale-di-un-fragment)
        - [Esempio 6.6.3.3. Fractal Branch di una Category di Category Nodes](#esempio-6633-fractal-branch-di-una-category-di-category-nodes)
        - [Esempio 6.6.3.4. Compound Component con Context e Fractal Branches annidati](#esempio-6634-compound-component-con-context-e-fractal-branches-annidati)
    - [6.7. Foreign Domains](#67-foreign-domains)
      - [6.7.1. Esempi di Riferimento](#671-esempi-di-riferimento)
        - [Esempio 6.7.1.1. Foreign Domain in un Root Fragment](#esempio-6711-foreign-domain-in-un-root-fragment)
    - [6.8. Matrice di Contenimento dei Logical Domains](#68-matrice-di-contenimento-dei-logical-domains)
    - [6.9. Completezza della Classificazione](#69-completezza-della-classificazione)
  - [7. Frontiera e Relazioni Esterne dei Fractal Trees](#7-frontiera-e-relazioni-esterne-dei-fractal-trees)
    - [7.1. Public Surface del Fractal Tree](#71-public-surface-del-fractal-tree)
    - [7.2. Relazioni tra Fractal Trees](#72-relazioni-tra-fractal-trees)
    - [7.3. Relazioni con Codice Locale Esterno ai Fractal Trees](#73-relazioni-con-codice-locale-esterno-ai-fractal-trees)
    - [7.4. Disciplina dei Path Aliases](#74-disciplina-dei-path-aliases)
  - [8. Criteri di Progettazione ed Evoluzione](#8-criteri-di-progettazione-ed-evoluzione)
    - [8.1. Collocazione per Prossimità e Rilevanza di Dominio](#81-collocazione-per-prossimità-e-rilevanza-di-dominio)
    - [8.2. Controllo della Profondità e Dualità tra Incapsulamento e Horizontal Hierarchy](#82-controllo-della-profondità-e-dualità-tra-incapsulamento-e-horizontal-hierarchy)
    - [8.3. Evoluzione Iterativa e Ricorsiva dell'Architettura](#83-evoluzione-iterativa-e-ricorsiva-dellarchitettura)
    - [8.4. Isolamento delle Dipendenze Locali Esterne](#84-isolamento-delle-dipendenze-locali-esterne)

## 2. Obiettivi

- **Prevedibilità**

  > Permettere una lettura immediata della struttura della codebase e del flusso delle dipendenze.

- **Testabilità**

  > Semplificare la verifica del software, garantendo l'isolamento dei confini di ciascuna unità logica.

- **Scalabilità**

  > Sostenere l'evoluzione della codebase mediante un modello di accrescimento autosimile.

- **Manutenibilità**

  > Ridurre l'impatto delle modifiche confinandone la portata all'interno della singola unità logica.

## 3. Principi

Un _Fractal Tree_ è il sotto-albero della codebase con origine in una directory identificata da una Declaration.

- **Il Principio della Scomposizione Frattale**

  > La codebase modella il sistema software mediante uno o più Fractal Trees, dedicati ciascuno a uno specifico problema. Ogni Fractal Tree costituisce uno spazio architetturale autonomo. I Fractal Trees non condividono file o directory; file e directory esterni ai Fractal Trees esulano dalla tassonomia di FAF. All'interno di ciascun Fractal Tree, la risoluzione procede per scomposizione ricorsiva: a ogni livello di scala, ciascun sotto-problema coeso è risolto da un'unità logica dedicata, e l'insieme di tali unità è governato da una struttura organizzativa autosimile.

- **Il Principio della Forma Semantica**

  > La gerarchia e la nomenclatura di file e directory devono rivelare lo scopo architetturale di ogni unità logica.

- **Il Principio della Proporzionalità**

  > Il grado di scomposizione della codebase deve essere commisurato alla complessità del problema da risolvere.

## 4. Fondamenti

- **Dependency Graph**

  > All'interno di un Fractal Tree, la codebase è modellata come un grafo orientato, il _Dependency Graph_, in cui ciascun arco connette un vertice sorgente al vertice destinatario direttamente importato. Un'importazione è ogni riferimento statico con cui un file richiede la risoluzione di un altro file della codebase (es. `import`, `import type`, `export … from`, `import()` con specificatore letterale, `require`, `@import` e `url()` nei fogli di stile).

- **Logical Nodes**

  > I _Logical Nodes_ sono i file del Fractal Tree che costituiscono i vertici del Dependency Graph, ammessi a importare, esportare o essere importati.

- **Foreign Nodes**

  > I _Foreign Nodes_ sono i file del Fractal Tree identificati da una Declaration come esclusi dal Dependency Graph. Ai Foreign Nodes è interdetta ogni relazione di importazione, in ingresso o in uscita, con file della codebase. Ogni file di un Fractal Tree è un Logical Node oppure un Foreign Node.

- **Asset**

  > Un _Asset_ è un Logical Node il cui contenuto non è codice TypeScript o JavaScript (es. fogli di stile, font, immagini, file JSON).

- **Symbol**

  > Un _Symbol_ è ciascuna dichiarazione nello scope radice di un Logical Node diverso da un Asset, nello spazio dei valori o nello spazio dei tipi, esportata o non esportata (es. `const`, `let`, `var`, `function`, `class`, `enum`, `type`, `interface`, `namespace`). Costituiscono Symbols distinti i singoli binding introdotti da dichiarazioni multiple o destrutturate, ciascuna delle dichiarazioni omonime soggette a fusione (_declaration merging_) e ogni dichiarazione inizializzata con un binding importato. Costituiscono un unico Symbol l'insieme delle firme di overload con la relativa implementazione della medesima funzione, così come un'esportazione `default` anonima. Le dichiarazioni di importazione non introducono Symbols.

- **Role**

  > Il _Role_ è l'etichetta semantica che qualifica la competenza architetturale di un Logical Node. Per uno o più Fractal Trees, una Declaration stabilisce il catalogo chiuso dei Roles e, per ciascun Role, le eventuali estensioni implicite, ossia le estensioni di Asset associate al Role. Ciascuna estensione implicita appartiene a un unico Role del catalogo; il primo segmento di un'estensione implicita non coincide con il nome di alcun Role del catalogo.
  >
  > Nel nome di un file, `<nome>` designa il segmento iniziale, privo del carattere `.`, mentre `<estensione>` designa il segmento finale oppure una sequenza di segmenti finali coincidente con un'estensione implicita (es. `.tar.gz`). Il Role di un Logical Node è:
  >
  > - **Esplicito**: se il nome del file ha la forma `<nome>.<role>.<estensione>`, con `<role>` appartenente al catalogo (es. `button.component.tsx`, `button.module.css`).
  > - **Implicito**: se il Logical Node è un Asset il cui nome ha la forma `<nome>.<estensione>`, con `<estensione>` estensione implicita del Role (es. `theme.css`, `inter.woff2`, `bundle.tar.gz`).
  > - **Assente**: se il nome del file non ha alcuna delle due forme precedenti (es. `index.ts`, `example.util.spec.ts`).

- **Execution Sub-Graphs**

  > Ogni contesto di esecuzione (es. _build-time_, _runtime_, _test_, ambienti dedicati come _Storybook_) opera su uno specifico _Execution Sub-Graph_ del Dependency Graph, generato per raggiungibilità a partire dai rispettivi Logical Nodes di ingresso.

- **Sub-Graph Role**

  > Il _Sub-Graph Role_ è un Role riservato ai Logical Nodes di ingresso in Execution Sub-Graphs dedicati (es. `spec`, `story`). La Declaration del catalogo distingue i Sub-Graph Roles dagli altri Roles. Un Sub-Graph Role è attribuito esclusivamente in forma esplicita.

- **Sub-Graph Node**

  > Il _Sub-Graph Node_ è un Logical Node con un Sub-Graph Role. Un Sub-Graph Node non può essere importato da alcun Logical Node.

- **Logical Domain**

  > All'interno di un Fractal Tree, ogni directory costituisce un _Logical Domain_: un confine semantico per i file e le directory contenuti nel proprio sotto-albero. Ogni Logical Domain può ospitare direttamente Foreign Nodes ed è:
  >
  > - **Functional**: se isola una singola unità logica.
  > - **Organizational**: se non costituisce una singola unità logica.

- **Gerarchia dei Logical Domains**

  > La relazione di inclusione dei Logical Domains è transitiva: ogni Logical Domain include nel proprio confine semantico tutti i Logical Domains, i Logical Nodes e i Foreign Nodes contenuti nel proprio sotto-albero.

- **Horizontal Hierarchy**

  > Una _Horizontal Hierarchy_ è l'assegnazione, stabilita da una Declaration, di un _Rank_ espresso da un numero naturale a ciascun elemento di un insieme di elementi fratelli: Logical Nodes oppure Logical Domains figli diretti del medesimo Logical Domain, senza commistione tra Logical Nodes e Logical Domains. Una Horizontal Hierarchy autorizza dipendenze esclusivamente tra elementi del proprio insieme, da un elemento di Rank $N$ verso un elemento di Rank strettamente inferiore $M$ ($M < N$).
  >
  > Più Horizontal Hierarchies possono coesistere sotto lo stesso genitore soltanto se ordinano insiemi disgiunti di figli diretti. I Ranks di Horizontal Hierarchies distinte non sono confrontabili.

- **Nomenclatura**

  > Salvo ove diversamente prescritto da contratti tecnologici esterni o dalla presente specifica, gli identificatori di file e directory adottano la convenzione _kebab-case_, combinata con i delimitatori sintattici previsti dal framework. I Foreign Nodes e la directory di origine di ciascun Fractal Tree sono a denominazione libera. Per gli altri Logical Domains, il prefisso _underscore_ (`_`) distingue la natura del Logical Domain:
  >
  > - **Senza prefisso `_`**: Logical Domains Functional.
  > - **Con prefisso `_`**: Logical Domains Organizational.

## 5. Leggi del Dependency Graph

- **La Legge del Grafo Aciclico Diretto**

  > Il Dependency Graph deve essere un grafo aciclico diretto (_DAG_).

- **La Legge della Separazione tra Pari**

  > È interdetta qualsiasi dipendenza tra Logical Nodes appartenenti a sotto-alberi di Logical Domains fratelli, nonché tra Logical Nodes fratelli all'interno del medesimo Logical Domain, salvo ove disciplinata da una Horizontal Hierarchy o dalle regole di visibilità proprie di specifici Logical Domains.

- **La Legge dell'Univocità del Symbol**

  > Ciascun Logical Node con Role esplicito, diverso da un Asset e da un Sub-Graph Node, definisce al più un Symbol coerente con il proprio Role, salvo che la Declaration del catalogo ammetta più Symbols per tale Role. Symbols ulteriori richiedono ciascuno un Logical Node dedicato.

- **La Legge del Divieto di Riesportazione**

  > A ogni Logical Node con Role esplicito è interdetta la riesportazione di Symbols importati.

## 6. Tassonomia dei Logical Domains

### 6.1. Fragments

Il _Fragment_ è il Logical Domain Functional deputato a implementare un'unità logica coesa e autocontenuta. Il nome del Fragment designa l'unità implementata (es. `button/`, `use-example/`, `get-todos/`). Ogni Fragment possiede un Role, detto _Role del Fragment_, che qualifica l'unità implementata.

In virtù della natura ricorsiva della scomposizione, un Fragment può racchiudere nel proprio sotto-albero, esclusivamente per il tramite di Logical Domains Organizational intermedi, ulteriori Fragments dedicati a dettagli implementativi interni. Ciascuno di tali Fragments assume la qualifica relazionale di _Sub-Fragment_ rispetto al _Parent Fragment_, ossia il Fragment che lo contiene senza altri Fragments interposti.

#### 6.1.1. Tassonomia dei Logical Nodes del Fragment

I Logical Nodes figli diretti di un Fragment, nel quale ciascun Role esplicito compare al più una volta, si articolano nelle seguenti tipologie:

- **Fragment Nodes**: Logical Nodes con Role esplicito diverso da un Sub-Graph Role, il cui `<nome>` coincide con il nome del Fragment, che implementano le competenze interne del Fragment (es. `button.component.tsx`, `button.hook.ts`, `button.type.ts`, ecc.). Ogni Fragment contiene un **Master Node**: l'unico Fragment Node con il Role del Fragment, che incarna la competenza architetturale dell'unità logica e definisce ed esporta un unico Symbol, anche quando la Declaration del catalogo ammette più Symbols per il Role del Fragment. A ogni Logical Node esterno alla directory del Fragment è interdetta l'importazione dei Fragment Nodes del Fragment.
- **Access Node** (`index.ts`): l'unico Logical Node con Role assente, obbligatorio in ogni Fragment, che costituisce l'esclusiva interfaccia pubblica del Fragment. L'Access Node può importare e riesportare esclusivamente Symbols definiti dai Fragment Nodes del medesimo Fragment: ha l'obbligo di riesportare il Symbol del Master Node, la facoltà di riesportare selettivamente i Symbols degli altri Fragment Nodes e il divieto di definire Symbols propri.
- **Sub-Graph Nodes**: Logical Nodes con Sub-Graph Role, il cui `<nome>` coincide con il nome del Fragment, che consumano o osservano i Fragment Nodes del medesimo Fragment a beneficio di Execution Sub-Graphs dedicati. Non essendo importabili da alcun Logical Node, i Sub-Graph Nodes non concorrono alla logica del Fragment.

#### 6.1.2. Separazione delle Competenze e Univocità del Symbol

È raccomandato ammettere più Symbols esclusivamente per i Roles la cui natura comporta dichiarazioni correlate o ausiliarie (es. `constant`, `mock`, `recipe`, `schema`, `styled`, `type`, `util`, ecc.).

In un Logical Node il cui Role ammette più Symbols possono coesistere esclusivamente Symbols mutuamente inscindibili all'interno della medesima competenza; Symbols autonomi richiedono Logical Nodes distinti o Sub-Fragments dedicati.

La derivabilità meccanica tra Symbols non implica identità architetturale: Symbols associati a competenze distinte risiedono in Logical Nodes distinti con Roles differenti (es. uno schema di validazione e il rispettivo tipo inferito).

#### 6.1.3. Horizontal Hierarchy Interna e Modello dei Roles

La Declaration del catalogo assegna a ciascun Role diverso da un Sub-Graph Role un Rank, in funzione del dominio e dello stack tecnologico. I Logical Nodes figli diretti di ciascun Fragment sono ordinati dalla Horizontal Hierarchy in cui ciascun Fragment Node assume il Rank del proprio Role, mentre l'Access Node e i Sub-Graph Nodes occupano congiuntamente il Rank immediatamente superiore al Rank massimo del catalogo. Ogni Fragment Node diverso dal Master Node ha Rank strettamente inferiore al Rank del Master Node.

##### Modello di Riferimento per i Roles

FAF realizza la modularità mediante la composizione anziché mediante l'ereditarietà: i Roles qualificano le competenze architetturali che concorrono per composizione progressiva alla costruzione di un Fragment, non gerarchie di classi o costrutti sintattici del linguaggio.

Il modello seguente costituisce un esempio di riferimento: l'allineamento sul medesimo Rank delle competenze di coordinamento applicativo impedisce di accorpare molteplici responsabilità primarie nei Fragment Nodes di uno stesso Fragment e impone la composizione di Fragments e Sub-Fragments distinti attraverso i rispettivi Access Nodes.

- **Rank 0: Asset Statici Puri**
  - `font`: Asset tipografici.
  - `image`: Asset grafici e iconografici.
- **Rank 1: Stili e Markup Dichiarativi**
  - `markup`: Documenti dichiarativi di markup o testo.
  - `module`: Fogli di stile CSS Modules con scope locale.
  - `style`: Fogli di stile CSS.
- **Rank 2: Costanti Primitive**
  - `constant`: Valori immutabili e letterali primitivi.
- **Rank 3: Modelli Dichiarativi di Dati**
  - `model`: Definizioni dichiarative di strutture o schemi dati.
- **Rank 4: Ricette Grafiche**
  - `recipe`: Varianti e composizioni di stile.
- **Rank 5: Schemi di Validazione**
  - `schema`: Schemi di validazione e parsing runtime.
- **Rank 6: Tipizzazione**
  - `type`: Definizioni statiche di tipo.
- **Rank 7: Errori Tipizzati**
  - `error`: Costruttori e strutture di errore tipizzati.
- **Rank 8: Dati di Simulazione**
  - `mock`: Dati sintetici, fixture e stub.
- **Rank 9: Configurazione Applicativa**
  - `config`: Parametri e oggetti di configurazione.
- **Rank 10: Stili con Contratto di Tipo**
  - `styled`: Componenti stilizzati con binding di tipo.
- **Rank 11: Helper Funzionali**
  - `util`: Funzioni di utilità ed elaborazione pura.
- **Rank 12: Costrutti con Stato Incapsulato**
  - `class`: Costrutti con stato incapsulato o strutture dati dedicate.
- **Rank 13: Pattern Creazionali**
  - `factory`: Funzioni factory per la creazione di istanze o strutture.
- **Rank 14: Istanze Preconfigurate**
  - `instance`: Istanze preconfigurate di oggetti o client.
- **Rank 15: Logiche di Coordinamento Locale**
  - `controller`: Coordinatori del flusso di esecuzione locale.
  - `handler`: Gestori di eventi o esecutori di comandi.
  - `hook`: Hook e funzioni con gestione del ciclo di vita.
- **Rank 16: Logiche di Coordinamento Applicativo**
  - `api`: Client e integrazioni con servizi esterni.
  - `component`: Componenti di interfaccia utente.
  - `context`: Contesti per la condivisione dello stato.
  - `job`: Processori di task schedulati o code asincrone.
  - `layout`: Strutture di layout e impaginazione.
  - `middleware`: Intercettatori di flussi o richieste.
  - `page`: Pagine o viste di navigazione.
  - `repository`: Moduli di persistenza o accesso ai dati.
  - `route`: Definizioni di rotte.
  - `router`: Aggregatori e distributori di rotte.
  - `service`: Moduli di logica di business e orchestrazione.
  - `store`: Gestori di stato globale o condiviso.
- **Rank 17: Rank Sommitale**
  - `index.ts` (Access Node): Interfaccia pubblica esclusiva del Fragment.
  - `spec` (Sub-Graph Node): Entry point dell'Execution Sub-Graph di Test.
  - `story` (Sub-Graph Node): Entry point dell'Execution Sub-Graph di Storybook.

#### 6.1.4. Esempi di Riferimento

##### Esempio 6.1.4.1. Fragment con Role 'component' in un'applicazione React

```text
example/                                       <-- Fragment con Role 'component'
  ├── example.component.tsx                    <-- Master Node (Rank 16)
  ├── example.constant.ts                      <-- Fragment Node (Rank 2)
  ├── example.hook.ts                          <-- Fragment Node (Rank 15)
  ├── example.module.css                       <-- Fragment Node (Rank 1)
  ├── example.spec.tsx                         <-- Sub-Graph Node dell'Execution Sub-Graph di Test (Rank 17)
  ├── example.story.tsx                        <-- Sub-Graph Node dell'Execution Sub-Graph di Storybook (Rank 17)
  ├── example.type.ts                          <-- Fragment Node (Rank 6)
  ├── example.util.ts                          <-- Fragment Node (Rank 11)
  ├── index.ts                                 <-- Access Node (Rank 17)
  └── README.md                                <-- Foreign Node
```

> **Nota**: Il Fragment racchiude la propria logica nei Fragment Nodes (`example.*`) ordinati dalla Horizontal Hierarchy interna. Il Master Node `example.component.tsx` ha il Role del Fragment, `component`, e il Rank massimo tra i Fragment Nodes. L'accesso pubblico è consentito unicamente tramite `index.ts`, mentre `example.spec.tsx` ed `example.story.tsx` fungono da punti di ingresso isolati per i rispettivi Execution Sub-Graphs.

##### Esempio 6.1.4.2. Access Node di un Fragment con Role 'component'

```typescript
// .../example/index.ts

export * from './example.component';
export type * from './example.type';
```

> **Nota**: L'Access Node definisce l'interfaccia pubblica esclusiva del Fragment mediante la riesportazione dei Symbols definiti dai propri Fragment Nodes. Oltre alla riesportazione obbligatoria del Symbol del Master Node, in questo scenario l'architetto sceglie di esporre i relativi contratti di tipo, preservando l'incapsulamento dei restanti Fragment Nodes interni (es. hook, costanti, utilità e stili).

##### Esempio 6.1.4.3. Fragment con Role 'hook'

```text
use-example/                                   <-- Fragment con Role 'hook'
  ├── index.ts                                 <-- Access Node (Rank 17)
  ├── README.md                                <-- Foreign Node
  ├── use-example.constant.ts                  <-- Fragment Node (Rank 2)
  ├── use-example.hook.ts                      <-- Master Node (Rank 15)
  ├── use-example.spec.ts                      <-- Sub-Graph Node dell'Execution Sub-Graph di Test (Rank 17)
  └── use-example.type.ts                      <-- Fragment Node (Rank 6)
```

> **Nota**: Il Master Node `use-example.hook.ts` ha il Role del Fragment, `hook`. `use-example.hook.ts` (Rank 15) può importare `use-example.type.ts` (Rank 6) e `use-example.constant.ts` (Rank 2), mentre non può dipendere dall'Access Node né dal Sub-Graph Node di test.

##### Esempio 6.1.4.4. Fragment con Role 'util'

```text
do-something/                                  <-- Fragment con Role 'util'
  ├── do-something.constant.ts                 <-- Fragment Node (Rank 2)
  ├── do-something.spec.ts                     <-- Sub-Graph Node dell'Execution Sub-Graph di Test (Rank 17)
  ├── do-something.type.ts                     <-- Fragment Node (Rank 6)
  ├── do-something.util.ts                     <-- Master Node (Rank 11)
  ├── index.ts                                 <-- Access Node (Rank 17)
  └── README.md                                <-- Foreign Node
```

> **Nota**: Il Master Node `do-something.util.ts` ha il Role del Fragment, `util`. La funzione di utilità importa i tipi e le costanti collocati a Ranks inferiori, ed è esposta all'esterno unicamente tramite `index.ts`.

### 6.2. Root Fragments

Il _Root Fragment_ è il Logical Domain Functional, a denominazione libera (es. `src/`, `app/`), deputato a fungere da punto di frontiera con strumenti esterni (es. il _file-system routing_ di Next.js, Astro, ecc.). È raccomandato che il nome di un Root Fragment non adotti il prefisso `_`.

Un Root Fragment può essere collocato esclusivamente come origine di un Fractal Tree o come figlio diretto di un altro Root Fragment. Ciascun Root Fragment è identificato esclusivamente da una Declaration, che ne enumera anche i Root Fragments figli diretti. Il Root Fragment non ha Master Node né Access Node.

#### 6.2.1. Tassonomia dei Nodi del Root Fragment

La totalità dei Logical Nodes figli diretti di un Root Fragment prende il nome di **Root Nodes**. Una Declaration enumera esaustivamente i Root Nodes di ciascun Root Fragment; ogni altro file figlio diretto del Root Fragment deve essere identificato come Foreign Node da una Declaration.

I Root Nodes sono a denominazione libera e hanno Role assente, indipendentemente dalla forma del nome.

Un Root Node il cui nome in un Fragment identificherebbe un Fragment Node (es. `app.component.tsx`), un Sub-Graph Node (es. `app.spec.tsx`) o un Access Node (es. `index.ts`), o in un altro Logical Domain attribuirebbe un Role implicito (es. `main.css`), non assume alcun Role né alcuna qualifica: ai Root Nodes non si applicano i Ranks dei Roles.

#### 6.2.2. Disciplina delle Dipendenze dei Root Nodes

All'interno del medesimo Fractal Tree, un Root Node non può essere importato da alcun Logical Node diverso da un altro Root Node. Le dipendenze tra Root Nodes sono interdette salvo autorizzazione mediante una delle due forme seguenti:

- **Nel medesimo Root Fragment**: un'unica Horizontal Hierarchy ordina i Root Nodes.
- **Tra Root Fragments distinti**: una Declaration autorizza le dipendenze da Root Nodes del Root Fragment sorgente verso Root Nodes destinatari di altri Root Fragments dello stesso Fractal Tree. Una Declaration con più sorgenti e più destinatari autorizza ogni coppia sorgente-destinatario. Il riferimento a un destinatario non ne modifica l'appartenenza al Root Fragment che lo contiene.

Le autorizzazioni non impongono l'esistenza delle importazioni. Un'autorizzazione tra Root Fragments non autorizza l'arco inverso né ulteriori archi per transitività.

#### 6.2.3. Esempi di Riferimento

##### Esempio 6.2.3.1. Root Fragment in una Single Page Application (SPA)

In una SPA basata su bundler come Vite, la directory `src/` opera come Root Fragment dell'applicazione:

```text
src/                                           <-- Root Fragment
  ├── main.css                                 <-- Root Node (Rank 0)
  ├── main.tsx                                 <-- Root Node (Rank 1)
  ├── vite-env.d.ts                            <-- Foreign Node
  ├── README.md                                <-- Foreign Node
  └── app/                                     <-- Root Fragment
        └── app.tsx                            <-- Root Node (Rank 0)
```

> **Nota**: Le Declarations enumerano `main.css` e `main.tsx` come Root Nodes di `src/`, con Ranks rispettivamente 0 e 1, `app/` come Root Fragment figlio diretto di `src/` e `app.tsx` come Root Node di `app/`. La Horizontal Hierarchy di `src/` autorizza `main.tsx` a importare `main.css`; una distinta Declaration autorizza `src/main.tsx` a importare `src/app/app.tsx`. Il Rank di `app.tsx` non partecipa alla Horizontal Hierarchy di `src/`. I file `vite-env.d.ts` e `README.md` sono identificati come Foreign Nodes da Declarations.

##### Esempio 6.2.3.2. Root Fragments gerarchici con File-System Routing (Next.js App Router)

In un framework basato su file-system routing, la directory `app/` e le relative sotto-cartelle di rotta costituiscono una gerarchia annidata di Root Fragments:

```text
app/                                           <-- Root Fragment
  ├── layout.tsx                               <-- Root Node
  ├── page.tsx                                 <-- Root Node
  ├── about/                                   <-- Root Fragment
  │     ├── layout.tsx                         <-- Root Node
  │     └── page.tsx                           <-- Root Node
  └── blog/                                    <-- Root Fragment
        ├── layout.tsx                         <-- Root Node
        ├── page.tsx                           <-- Root Node
        └── ...
```

> **Nota**: Le Declarations identificano ciascuna directory di rotta come Root Fragment ed enumerano i relativi Root Nodes e Root Fragments figli diretti. I file `page.tsx` e `layout.tsx` adempiono ai contratti del framework esterno, definendo liberamente molteplici Symbols esportati. La struttura delle rotte non autorizza importazioni tra Root Fragments distinti.

### 6.3. Categories

La _Category_ è il Logical Domain Organizational deputato a classificare unità omogenee accomunate dal medesimo Role (es. `_components/`, `_hooks/`, `_styles/`, `_types/`, `_utils/`).

La Declaration del catalogo associa a ciascun Role diverso da un Sub-Graph Role il nome esatto di una Category, distinto per ciascun Role; l'associazione non presuppone la presenza effettiva di una Category con tale nome. È raccomandata la denominazione al plurale. Salvo ove diversamente prescritto, una directory di un Fractal Tree il cui nome coincide con un nome di Category è una Category e impone il Role associato alle unità classificate.

Una Category non può essere figlia diretta di un'altra Category.

Non costituendo un'unità logica dotata di responsabilità funzionale propria, bensì una collezione di entità reciprocamente autonome, la Category non ammette un Access Node (`index.ts`): ciascuna unità classificata mantiene la propria identità distinta ed è importata individualmente.

#### 6.3.1. Mutua Esclusività del Contenuto e Category Nodes

Un _Category Node_ è un Logical Node privo di incapsulamento in Fragment, classificato da una Category e con Role coincidente con il Role imposto dalla Category.

In base alla forma che la Declaration del catalogo stabilisce per ciascun Role, una Category adotta una sola delle due seguenti forme mutuamente esclusive:

- **Category di Fragments**: classifica Fragments il cui Role del Fragment è il Role imposto dalla Category (es. `_components/button/` con Master Node `button.component.tsx`).
- **Category di Category Nodes**: classifica Category Nodes con Role esplicito (es. `_types/user.type.ts`, `_schemas/order.schema.ts`) oppure implicito (es. `_styles/theme.css`, `_fonts/inter.woff2`). All'interno di un Fractal Tree, i Logical Nodes con Role implicito sono ammessi esclusivamente in qualità di Category Nodes.

È interdetta in una Category la presenza diretta di Logical Nodes con Role assente o con Role difforme da quello imposto dalla Category. Poiché la forma della Category è vincolata al Role per l'intero Fractal Tree, un Role con forma Category Nodes non ammette l'incapsulamento di singole unità in Fragment né l'associazione di Sub-Graph Nodes dedicati al singolo Category Node. Tale Role resta ammesso in forma esplicita nei Fragment Nodes diversi dal Master Node.

Un Role dotato di estensioni implicite adotta la forma Category Nodes nell'intero Fractal Tree; una Declaration che gli assegni la forma Fragments è contraddittoria.

Tra Fragments fratelli e tra Category Nodes fratelli è interdetta qualsiasi Horizontal Hierarchy.

#### 6.3.2. Sub-Categories

Una Category può ripartire tassonomicamente il proprio contenuto in Logical Domains Organizational annidati, denominati **Sub-Categories** (es. `_atoms/`, `_molecules/`, `_primitives/`, `_dtos/`). Salvo ove diversamente prescritto, ogni directory Organizational figlia diretta di una Category o di una Sub-Category, il cui nome non coincide con un nome di Category, è una Sub-Category. È raccomandata la denominazione al plurale.

Una Sub-Category può essere collocata esclusivamente come figlia diretta di una Category o di un'altra Sub-Category. La Category da cui discende una catena di Sub-Categories assume, rispetto a ciascuna di esse, la qualifica relazionale di **Parent Category**. La Sub-Category non ridefinisce il Role, bensì propaga invariato il Role imposto dalla Parent Category, fermi restando il divieto di Access Node e la forma della Parent Category (Fragments oppure Category Nodes).

Una Category non può essere figlia diretta di una Sub-Category; Categories e Sub-Categories non possono essere sorelle.

In ciascuna Category e in ciascuna Sub-Category, la ramificazione in Sub-Categories e la presenza diretta di Fragments o Category Nodes sono mutuamente esclusive.

#### 6.3.3. Private Categories

Una Category figlia diretta di un Fragment o di un Root Fragment assume la qualifica relazionale di **Private Category**, deputata a incapsulare unità implementative interne del Logical Domain genitore (quali Sub-Fragments o Category Nodes privati).

Dall'esterno del confine della Private Category, le unità contenute nella Private Category possono essere importate esclusivamente dai Logical Nodes figli diretti del Logical Domain genitore:

- **Nel Fragment**: dai Fragment Nodes e dai Sub-Graph Nodes figli diretti del Fragment.
- **Nel Root Fragment**: dai Root Nodes figli diretti del Root Fragment.

La relazione di dipendenza è rigidamente unidirezionale: nessun Logical Node appartenente al sotto-albero di una Private Category può importare i Logical Nodes figli diretti del Logical Domain genitore.

#### 6.3.4. Horizontal Hierarchies per Categories e Sub-Categories

- **Tra Categories**: Categories sorelle non private possono essere ordinate da una Horizontal Hierarchy stabilita in funzione del dominio, inclusa l'adozione dei Ranks dei rispettivi Roles. Tra Private Categories sorelle è interdetta qualsiasi Horizontal Hierarchy.
- **Tra Sub-Categories**: Sub-Categories sorelle, anche interne a una Private Category, possono essere ordinate da una Horizontal Hierarchy stabilita in funzione del dominio oppure conforme a uno dei due modelli di riferimento seguenti.

##### Modelli di Riferimento per le Sub-Categories

- **Atomic Design** (per Categories di componenti di interfaccia utente):
  - **Rank 0**: `_atoms`
  - **Rank 1**: `_molecules`
  - **Rank 2**: `_organisms`
  - **Rank 3**: `_templates`
- **Systemic Design** (per domini logici, algoritmici o infrastrutturali):
  - **Rank 0**: `_primitives`
  - **Rank 1**: `_compounds`
  - **Rank 2**: `_aggregates`
  - **Rank 3**: `_systems`
  - **Rank 4**: `_ecosystems`

Nell'adozione dell'Atomic Design è raccomandato classificare lo stadio _pages_ mediante una Category associata a un Role distinto dal Role dei componenti (es. `_pages/` con Role `page`), collocata come sorella della Category dei componenti anziché come Sub-Category di quest'ultima.

#### 6.3.5. Mimetic Path Structure e Path Sub-Categories

Una _Mimetic Path Structure_ è la configurazione topologica, stabilita da una Declaration su una Category di Fragments (es. `_apis/`, `_pages/`, `_routes/`, `_commands/`, `_handlers/`), deputata a mappare sul file system uno spazio di indirizzamento gerarchico esterno (quali endpoint HTTP/REST, alberi di URL per il routing programmatico di interfacce utente, gerarchie di comandi CLI, alberi di topic in sistemi a eventi o namespace di procedure RPC/IPC). A differenza dei Root Fragments, deputati a soddisfare contratti sul file system scansionati direttamente da strumenti esterni, la Mimetic Path Structure modella la corrispondenza con lo spazio di indirizzamento esterno all'interno della tassonomia delle Categories. È interdetta l'applicazione di una Mimetic Path Structure a una Category di Category Nodes.

La Mimetic Path Structure si articola nei seguenti elementi:

- **Parent Category**: la Category su cui è stabilita la struttura, che rappresenta l'origine dello spazio di indirizzamento mappato e assume la qualifica di Parent Category rispetto alle Path Sub-Categories e ai Path Fragments della struttura.
- **Path Sub-Categories**: salvo ove diversamente prescritto, le directory Organizational figlie dirette della Parent Category o di un'altra Path Sub-Category, prive di Access Node, che rappresentano in corrispondenza biunivoca i singoli segmenti del percorso gerarchico esterno e propagano invariato il Role della Parent Category. Una Path Sub-Category assume forma:
  - **Statica**: denominata `_<segmento>/`, con `<segmento>` in _kebab-case_ fedele al segmento dell'indirizzo rappresentato e svincolato dal plurale (es. `_todos/`, `_blog/`, `_status/`, `_v1/`);
  - **Dinamica**: denominata `_[<parametro>]/`, con `<parametro>` in _kebab-case_ racchiuso tra parentesi quadre immediatamente dopo il prefisso `_` (es. `_[todo-id]/`, `_[post-id]/`).
- **Path Fragments**: i Fragments figli diretti della Parent Category, per le unità attestate alla radice dello spazio di indirizzamento, o di una Path Sub-Category, per le unità attestate alla coordinata individuata dalla catena di Path Sub-Categories antenate. Il Role di ciascun Path Fragment è il Role imposto dalla Parent Category. Un Path Fragment non sostituisce la Path Sub-Category corrispondente a un segmento dell'indirizzo, bensì implementa l'unità funzionale attestata su tale coordinata. In base alla Declaration della Mimetic Path Structure, la denominazione dei Path Fragments adotta una sola delle due seguenti forme mutuamente esclusive:
  - **Con Action Catalog**: quando una medesima coordinata può ospitare molteplici operazioni distinte da un qualificatore operativo (es. metodi HTTP su una risorsa REST), la Declaration stabilisce per la Parent Category un _Action Catalog_ chiuso e ciascun Path Fragment è denominato secondo lo schema `<action>-<target>` in _kebab-case_ (es. `get-todos/`, `patch-todo-status/`), dove `<action>` appartiene all'Action Catalog e `<target>` identifica l'entità o la risorsa destinataria; qualora l'Action Catalog contenga azioni composte in _kebab-case_ di cui una sia prefisso di un'altra, la scomposizione tra `<action>` e `<target>` è determinata dal prefisso più lungo appartenente all'Action Catalog;
  - **Senza Action Catalog**: quando lo spazio di indirizzamento non richiede un qualificatore operativo per distinguere le unità attestate sulla coordinata (es. viste associate a URL, sottocomandi terminali di una CLI o sottoscrittori dedicati a un topic), la Declaration omette l'Action Catalog e ciascun Path Fragment adotta la denominazione `<target>` in _kebab-case_ (es. `home/`, `blog-feed/`, `blog-post/`).

La classificazione come Path Sub-Category prevale sull'associazione tra nomi di Categories e Roles: un segmento il cui nome coincide con un nome di Category propaga il Role della Parent Category e non costituisce una Category.

Come figli diretti della Parent Category o di una Path Sub-Category è interdetta la presenza di Category Nodes, mentre è ammessa la coesistenza di Path Sub-Categories e Path Fragments. Poiché i segmenti modellano coordinate di indirizzamento e non Ranks di astrazione, è interdetta qualsiasi Horizontal Hierarchy che includa una Path Sub-Category.

Un Fragment può essere collocato esclusivamente come figlio diretto di una Category, di una Sub-Category o di una Path Sub-Category.

#### 6.3.6. Esempi di Riferimento

##### Esempio 6.3.6.1. Category di Fragments articolata in Sub-Categories (Atomic Design)

```text
_components/                                   <-- Category (Role 'component')
  ├── _atoms/                                  <-- Sub-Category (Rank 0)
  │   ├── icon/                                <-- Fragment con Role 'component'
  │   │   ├── icon.component.tsx               <-- Master Node (Rank 16)
  │   │   ├── icon.spec.tsx                    <-- Sub-Graph Node dell'Execution Sub-Graph di Test (Rank 17)
  │   │   ├── icon.type.ts                     <-- Fragment Node (Rank 6)
  │   │   ├── index.ts                         <-- Access Node (Rank 17)
  │   │   └── README.md                        <-- Foreign Node
  │   └── ...
  └── _molecules/                              <-- Sub-Category (Rank 1)
      ├── input/                               <-- Fragment con Role 'component'
      │   ├── index.ts                         <-- Access Node (Rank 17)
      │   ├── input.component.tsx              <-- Master Node (Rank 16)
      │   ├── input.spec.tsx                   <-- Sub-Graph Node dell'Execution Sub-Graph di Test (Rank 17)
      │   ├── input.type.ts                    <-- Fragment Node (Rank 6)
      │   └── README.md                        <-- Foreign Node
      └── ...
```

> **Nota**: `_atoms/` e `_molecules/` ereditano il Role `component` da `_components/`, senza ammettere Fragments diretti al livello di `_components/`. In virtù della Horizontal Hierarchy basata su Atomic Design, `input.component.tsx` (in `_molecules/`, Rank 1) può importare `icon/index.ts` (in `_atoms/`, Rank 0), mentre il flusso inverso è interdetto.

##### Esempio 6.3.6.2. Category di Category Nodes con Role esplicito e Sub-Categories

```text
_schemas/                                      <-- Category (Role 'schema')
  ├── _dtos/                                   <-- Sub-Category (Rank 1)
  │   ├── user-dto.schema.ts                   <-- Category Node con Role esplicito 'schema'
  │   └── ...
  └── _enums/                                  <-- Sub-Category (Rank 0)
      ├── user-role.schema.ts                  <-- Category Node con Role esplicito 'schema'
      └── ...
```

> **Nota**: La Declaration del catalogo assegna al Role `schema` la forma Category Nodes; `_schemas/` è ripartita nelle Sub-Categories `_enums/` e `_dtos/` con una Horizontal Hierarchy stabilita in funzione del dominio (`_enums` al Rank 0, `_dtos` al Rank 1): `user-dto.schema.ts` può importare `user-role.schema.ts`, mentre tra Category Nodes fratelli nella medesima Sub-Category resta interdetta ogni dipendenza.

##### Esempio 6.3.6.3. Category di Category Nodes con Role implicito

```text
_styles/                                       <-- Category (Role 'style')
  ├── README.md                                <-- Foreign Node
  ├── reset.css                                <-- Category Node con Role implicito 'style'
  └── variables.css                            <-- Category Node con Role implicito 'style'
```

> **Nota**: La Declaration del catalogo associa al Role `style` l'estensione implicita `.css`. I file `reset.css` e `variables.css` operano come Category Nodes autonomi all'interno di `_styles/`, privi di Access Node e reciprocamente isolati.

##### Esempio 6.3.6.4. Private Category in un Fragment

```text
example/                                       <-- Fragment con Role 'component'
  ├── example.component.tsx                    <-- Master Node (Rank 16)
  ├── example.spec.tsx                         <-- Sub-Graph Node dell'Execution Sub-Graph di Test (Rank 17)
  ├── example.type.ts                          <-- Fragment Node (Rank 6)
  ├── index.ts                                 <-- Access Node (Rank 17)
  ├── README.md                                <-- Foreign Node
  └── _components/                             <-- Private Category (Role 'component')
      └── example-child/                       <-- Sub-Fragment con Role 'component'
          ├── example-child.component.tsx      <-- Master Node (Rank 16)
          ├── index.ts                         <-- Access Node (Rank 17)
          └── README.md                        <-- Foreign Node
```

> **Nota**: Collocata direttamente nel Fragment `example/`, `_components/` assume la qualifica di Private Category. L'Access Node `example-child/index.ts` può essere importato unicamente dai Fragment Nodes e dai Sub-Graph Nodes figli diretti di `example/` (es. `example.component.tsx` ed `example.spec.tsx`), restando inaccessibile a `example/index.ts` e a qualsiasi Logical Node esterno.

##### Esempio 6.3.6.5. Mimetic Path Structure per endpoint REST

```text
_apis/                                         <-- Parent Category (Role 'api')
  └── _todos/                                  <-- Path Sub-Category statica
      ├── _[todo-id]/                          <-- Path Sub-Category dinamica
      │   ├── _status/                         <-- Path Sub-Category statica
      │   │   └── patch-todo-status/           <-- Path Fragment
      │   │       ├── index.ts                 <-- Access Node (Rank 17)
      │   │       └── patch-todo-status.api.ts <-- Master Node (Rank 16)
      │   └── get-todo/                        <-- Path Fragment
      │       ├── get-todo.api.ts              <-- Master Node (Rank 16)
      │       └── index.ts                     <-- Access Node (Rank 17)
      ├── get-todos/                           <-- Path Fragment
      │   ├── get-todos.api.ts                 <-- Master Node (Rank 16)
      │   └── index.ts                         <-- Access Node (Rank 17)
      └── post-todo/                           <-- Path Fragment
          ├── index.ts                         <-- Access Node (Rank 17)
          └── post-todo.api.ts                 <-- Master Node (Rank 16)
```

> **Nota**: `_apis/` è la Parent Category di una Mimetic Path Structure con Action Catalog (`get`, `post`, `patch`) in cui `_todos/`, `_[todo-id]/` e `_status/` operano come Path Sub-Categories che propagano il Role `api` ai Path Fragments (`get-todos/`, `post-todo/`, `get-todo/`, `patch-todo-status/`). All'interno di `_todos/` e di `_[todo-id]/`, Path Sub-Categories annidate e Path Fragments coesistono legittimamente al medesimo livello in totale isolamento reciproco.

##### Esempio 6.3.6.6. Mimetic Path Structure per routing programmatico di pagine

```text
_pages/                                        <-- Parent Category (Role 'page')
  ├── home/                                    <-- Path Fragment ('/')
  │   ├── home.page.tsx                        <-- Master Node (Rank 16)
  │   └── index.ts                             <-- Access Node (Rank 17)
  └── _blog/                                   <-- Path Sub-Category statica ('/blog')
      ├── _[post-id]/                          <-- Path Sub-Category dinamica ('/blog/:postId')
      │   ├── _comments/                       <-- Path Sub-Category statica ('/blog/:postId/comments')
      │   │   └── post-comments/               <-- Path Fragment ('/blog/:postId/comments')
      │   │       ├── index.ts                 <-- Access Node (Rank 17)
      │   │       └── post-comments.page.tsx   <-- Master Node (Rank 16)
      │   └── blog-post/                       <-- Path Fragment ('/blog/:postId')
      │       ├── blog-post.page.tsx           <-- Master Node (Rank 16)
      │       └── index.ts                     <-- Access Node (Rank 17)
      └── blog-feed/                           <-- Path Fragment ('/blog')
          ├── blog-feed.page.tsx               <-- Master Node (Rank 16)
          └── index.ts                         <-- Access Node (Rank 17)
```

> **Nota**: In assenza di un Action Catalog su `_pages/`, ciascun segmento dell'URL è rappresentato da una Path Sub-Category (`_blog/`, `_[post-id]/`, `_comments/`), mentre i Path Fragments (`home/`, `blog-feed/`, `blog-post/`, `post-comments/`) adottano la denominazione ordinaria in _kebab-case_ e implementano le pagine attestate sulle rispettive coordinate, incluso `home/` alla radice `/`.

### 6.4. Layers

Il _Layer_ è il Logical Domain Organizational deputato a definire un piano di astrazione architetturale trasversale a molteplici Roles (es. `_domain/`, `_network/`, `_state/`, `_ui/`).

A differenza della Category, il Layer non è associato a un singolo Role e non impone alcun Role al proprio sotto-albero, bensì raccoglie Categories eterogenee afferenti al medesimo strato concettuale.

Un Layer non può essere collocato come figlio diretto di un Fragment, di un Root Fragment, di una Category, di una Sub-Category o di una Path Sub-Category.

#### 6.4.1. Anatomia Interna e Sub-Layers

Un Layer non può ospitare direttamente Logical Nodes, Root Fragments, Fragments, Sub-Categories o Path Sub-Categories.

Un Layer figlio diretto di un altro Layer assume la qualifica relazionale di **Sub-Layer**, priva di disciplina propria.

Ogni Layer adotta una sola delle due configurazioni mutuamente esclusive: l'esposizione diretta di Categories oppure la ramificazione in Sub-Layers.

Un Layer non può essere fratello di una Category o di una Sub-Category.

#### 6.4.2. Horizontal Hierarchies tra Layers

Per i Layers il framework non prevede modelli tassonomici predefiniti: le relazioni di dipendenza tra Layers fratelli sono governate esclusivamente da Horizontal Hierarchies stabilite in funzione del dominio applicativo.

#### 6.4.3. Esempi di Riferimento

##### Esempio 6.4.3.1. Stratificazione in Layers ordinati da una Horizontal Hierarchy

```text
_domain/                                       <-- Layer (Rank 0)
  ├── _models/                                 <-- Category (Role 'model')
  ├── _schemas/                                <-- Category (Role 'schema')
  └── _types/                                  <-- Category (Role 'type')
_network/                                      <-- Layer (Rank 1)
  ├── _apis/                                   <-- Category (Role 'api')
  └── _types/                                  <-- Category (Role 'type')
_ui/                                           <-- Layer (Rank 2)
  ├── _components/                             <-- Category (Role 'component')
  └── _hooks/                                  <-- Category (Role 'hook')
```

> **Nota**: Una Horizontal Hierarchy tra i Layers assegna `_domain/` al Rank 0, `_network/` al Rank 1 e `_ui/` al Rank 2. I Logical Nodes contenuti nel sotto-albero di `_ui/` possono importare unità esposte da `_network/` e da `_domain/`, mentre `_domain/` non può dipendere da alcuno strato superiore.

### 6.5. Root Layers

Il _Root Layer_ è il Logical Domain Organizational deputato a strutturare direttamente l'origine di un Fractal Tree in partizioni organizzative (es. `src/`, `lib/`).

Un Root Layer è identificato esclusivamente da una Declaration e può essere collocato esclusivamente come origine di un Fractal Tree. L'origine di ciascun Fractal Tree è un Root Fragment oppure un Root Layer.

#### 6.5.1. Anatomia Interna e Gerarchie

Un Root Layer non può ospitare direttamente Logical Nodes, Root Fragments, Fragments, Sub-Categories, Path Sub-Categories o ulteriori Root Layers.

Al pari del Layer, il Root Layer non è associato a un singolo Role, non impone alcun Role al proprio sotto-albero e adotta una sola delle due seguenti configurazioni mutuamente esclusive:

- **Esposizione diretta di Categories**: le Categories figlie dirette di un Root Layer non assumono la qualifica di Private Categories e possono essere ordinate mediante una Horizontal Hierarchy secondo la disciplina ordinaria delle Categories non private.
- **Stratificazione in Layers**: i Layers figli diretti di un Root Layer possono essere ordinati mediante una Horizontal Hierarchy secondo la disciplina ordinaria dei Layers.

#### 6.5.2. Esempi di Riferimento

##### Esempio 6.5.2.1. Root Layer articolato in Categories

```text
src/                                           <-- Root Layer (origine del Fractal Tree)
  ├── _components/                             <-- Category (Role 'component', Rank 2)
  │   └── button/                              <-- Fragment con Role 'component'
  │       ├── button.component.tsx             <-- Master Node (Rank 16)
  │       └── index.ts                         <-- Access Node (Rank 17)
  ├── _hooks/                                  <-- Category (Role 'hook', Rank 1)
  │   └── use-toggle/                          <-- Fragment con Role 'hook'
  │       ├── index.ts                         <-- Access Node (Rank 17)
  │       └── use-toggle.hook.ts               <-- Master Node (Rank 15)
  └── _types/                                  <-- Category (Role 'type', Rank 0)
      └── size.type.ts                         <-- Category Node con Role esplicito 'type'
```

> **Nota**: Essendo `src/` identificata come Root Layer, le Categories `_components/`, `_hooks/` e `_types/` non costituiscono Private Categories e sono ordinate da una Horizontal Hierarchy che consente a `_components/` di dipendere da `_hooks/` e da `_types/`.

##### Esempio 6.5.2.2. Root Layer stratificato in Layers

```text
src/                                           <-- Root Layer (origine del Fractal Tree)
  ├── _domain/                                 <-- Layer (Rank 0)
  │   ├── _schemas/                            <-- Category (Role 'schema')
  │   └── _types/                              <-- Category (Role 'type')
  └── _ui/                                     <-- Layer (Rank 1)
      ├── _components/                         <-- Category (Role 'component')
      └── _hooks/                              <-- Category (Role 'hook')
```

> **Nota**: Il Root Layer `src/` organizza direttamente i Layers `_domain/` e `_ui/` senza richiedere Root Nodes né livelli intermedi di incapsulamento.

### 6.6. Fractal Branches

Il _Fractal Branch_ è il Logical Domain Organizational deputato a incapsulare e condividere unità e dettagli implementativi tra i sotto-alberi afferenti a un medesimo Logical Domain genitore.

Il Fractal Branch è identificato dalla denominazione `_<scope>@shared/`, riservata ai Fractal Branches, dove `<scope>` coincide con il nome della directory del Logical Domain genitore privato dell'eventuale prefisso `_` iniziale (es. `src/` genera `_src@shared/`, `button/` genera `_button@shared/`, `_hooks/` genera `_hooks@shared/`, `_[todo-id]/` genera `_[todo-id]@shared/`). In virtù di tale vincolo nominale, ciascun Logical Domain può ospitare come figlio diretto al più un Fractal Branch.

Un Fractal Branch non può essere collocato come figlio diretto di un altro Fractal Branch; può risiedere come figlio diretto di un Root Fragment, di un Root Layer, di un Fragment, di una Category, di una Sub-Category, di una Path Sub-Category o di un Layer.

#### 6.6.1. Anatomia Interna

Un Fractal Branch non può ospitare direttamente Logical Nodes, Root Fragments, Root Layers, Fragments, Sub-Categories o Path Sub-Categories.

Un Fractal Branch adotta una sola delle due seguenti configurazioni mutuamente esclusive: l'esposizione diretta di Categories oppure la stratificazione in Layers. Un Layer può essere figlio diretto esclusivamente di un altro Layer, di un Root Layer o di un Fractal Branch.

#### 6.6.2. Visibilità Discendente Ricorsiva e Unidirezionalità

L'accessibilità di un Fractal Branch è governata dai tre vincoli seguenti:

- **Perimetro dei consumatori autorizzati**: dall'esterno del Fractal Branch, l'accesso è consentito esclusivamente ai Logical Nodes appartenenti al sotto-albero del Logical Domain genitore, con esclusione dell'Access Node del genitore quando il genitore è un Fragment.
- **Confine di incapsulamento**: i consumatori autorizzati possono importare esclusivamente le unità classificate dalle Categories figlie dirette del Fractal Branch o dei Layers contenuti nel Fractal Branch, incluse le relative Sub-Categories e Path Sub-Categories: di ciascun Fragment l'Access Node, di ciascun Category Node il Category Node stesso. Tale visibilità non attraversa i Fragments, le Private Categories né i Fractal Branches annidati.
- **Unidirezionalità**: nessun Logical Node appartenente al sotto-albero di un Fractal Branch può dipendere, direttamente o indirettamente, dai Logical Nodes figli diretti del Logical Domain genitore del Fractal Branch né da alcun Logical Node appartenente agli altri sotto-alberi di tale Logical Domain genitore.

#### 6.6.3. Esempi di Riferimento

##### Esempio 6.6.3.1. Fractal Branch di un Root Fragment articolato in Layers

```text
src/                                           <-- Root Fragment (origine del Fractal Tree)
  ├── main.css                                 <-- Root Node
  ├── main.tsx                                 <-- Root Node
  ├── _src@shared/                             <-- Fractal Branch di src/
  │   ├── _domain/                             <-- Layer (Rank 0)
  │   │   └── _schemas/                        <-- Category (Role 'schema')
  │   │       └── ...
  │   └── _ui/                                 <-- Layer (Rank 1)
  │       └── _components/                     <-- Category (Role 'component')
  │           └── _atoms/                      <-- Sub-Category (Rank 0)
  │               └── button/                  <-- Fragment con Role 'component'
  │                   ├── button.component.tsx <-- Master Node (Rank 16)
  │                   ├── index.ts             <-- Access Node (Rank 17)
  │                   └── ...
  └── app/                                     <-- Root Fragment
      ├── app.tsx                              <-- Root Node
      ├── _app@shared/                         <-- Fractal Branch di app/
      │   └── ...
      └── _layouts/                            <-- Private Category di app/ (Role 'layout')
          └── shell/                           <-- Fragment con Role 'layout'
              ├── index.ts                     <-- Access Node (Rank 17)
              ├── shell.layout.tsx             <-- Master Node (Rank 16)
              └── ...
```

> **Nota**: `button/index.ts` in `_src@shared/` è accessibile ricorsivamente dall'intero sotto-albero di `src/` esterno a `_src@shared/` (inclusi `main.tsx`, `app/app.tsx`, `_app@shared/` e `shell.layout.tsx`). Al contrario, `_app@shared/` è inaccessibile a `src/main.tsx`, e `_layouts/shell/index.ts` (Private Category di `app/`) è accessibile esclusivamente al Root Node `app/app.tsx`.

##### Esempio 6.6.3.2. Fractal Branch locale di un Fragment

```text
button/                                        <-- Fragment con Role 'component'
  ├── button.component.tsx                     <-- Master Node (Rank 16)
  ├── index.ts                                 <-- Access Node (Rank 17)
  ├── _button@shared/                          <-- Fractal Branch di button/
  │   └── _components/                         <-- Category (Role 'component')
  │       └── button-icon/                     <-- Sub-Fragment con Role 'component'
  │           ├── button-icon.component.tsx    <-- Master Node (Rank 16)
  │           └── index.ts                     <-- Access Node (Rank 17)
  └── _components/                             <-- Private Category di button/ (Role 'component')
      └── button-label/                        <-- Sub-Fragment con Role 'component'
          ├── button-label.component.tsx       <-- Master Node (Rank 16)
          └── index.ts                         <-- Access Node (Rank 17)
```

> **Nota**: Collocando il Sub-Fragment `button-icon/` nel Fractal Branch `_button@shared/` anziché nella Private Category `_components/`, `button-icon/index.ts` risulta importabile sia da `button.component.tsx` sia da `button-label.component.tsx`, pur restando integralmente incapsulato nel confine di `button/`.

##### Esempio 6.6.3.3. Fractal Branch di una Category di Category Nodes

```text
_styles/                                       <-- Category (Role 'style')
  ├── theme.css                                <-- Category Node con Role implicito 'style'
  ├── variables.css                            <-- Category Node con Role implicito 'style'
  └── _styles@shared/                          <-- Fractal Branch di _styles/
      └── _fonts/                              <-- Category (Role 'font')
          └── inter.woff2                      <-- Category Node con Role implicito 'font'
```

> **Nota**: La presenza del Fractal Branch `_styles@shared/` all'interno di `_styles/` non viola la mutua esclusività tra Sub-Categories e Category Nodes. I Category Nodes `theme.css` e `variables.css` possono importare l'Asset `inter.woff2` incapsulato in `_styles@shared/_fonts/`.

##### Esempio 6.6.3.4. Compound Component con Context e Fractal Branches annidati

```text
table/                                          <-- Fragment con Role 'component'
  ├── index.ts                                  <-- Access Node (Rank 17)
  ├── table.component.tsx                       <-- Master Node (Rank 16)
  ├── table.hook.ts                             <-- Fragment Node (Rank 15)
  ├── table.recipe.ts                           <-- Fragment Node (Rank 4)
  ├── table.spec.tsx                            <-- Sub-Graph Node dell'Execution Sub-Graph di Test (Rank 17)
  ├── table.type.ts                             <-- Fragment Node (Rank 6)
  ├── _components/                              <-- Private Category di table/ (Role 'component')
  │   ├── _components@shared/                   <-- Fractal Branch di _components/
  │   │   └── _hooks/                           <-- Category (Role 'hook')
  │   │       └── use-table-context/            <-- Sub-Fragment con Role 'hook'
  │   │           ├── index.ts                  <-- Access Node (Rank 17)
  │   │           └── use-table-context.hook.ts <-- Master Node (Rank 15)
  │   ├── table-body/                           <-- Sub-Fragment con Role 'component'
  │   │   ├── index.ts                          <-- Access Node (Rank 17)
  │   │   ├── table-body.component.tsx          <-- Master Node (Rank 16)
  │   │   ├── table-body.recipe.ts              <-- Fragment Node (Rank 4)
  │   │   └── table-body.type.ts                <-- Fragment Node (Rank 6)
  │   ├── table-cell/                           <-- Sub-Fragment con Role 'component'
  │   │   ├── index.ts                          <-- Access Node (Rank 17)
  │   │   ├── table-cell.component.tsx          <-- Master Node (Rank 16)
  │   │   ├── table-cell.recipe.ts              <-- Fragment Node (Rank 4)
  │   │   └── table-cell.type.ts                <-- Fragment Node (Rank 6)
  │   ├── table-head/                           <-- Sub-Fragment con Role 'component'
  │   │   ├── index.ts                          <-- Access Node (Rank 17)
  │   │   ├── table-head.component.tsx          <-- Master Node (Rank 16)
  │   │   ├── table-head.recipe.ts              <-- Fragment Node (Rank 4)
  │   │   └── table-head.type.ts                <-- Fragment Node (Rank 6)
  │   ├── table-header-cell/                    <-- Sub-Fragment con Role 'component'
  │   │   ├── index.ts                          <-- Access Node (Rank 17)
  │   │   ├── table-header-cell.component.tsx   <-- Master Node (Rank 16)
  │   │   ├── table-header-cell.hook.ts         <-- Fragment Node (Rank 15)
  │   │   ├── table-header-cell.recipe.ts       <-- Fragment Node (Rank 4)
  │   │   └── table-header-cell.type.ts         <-- Fragment Node (Rank 6)
  │   └── table-row/                            <-- Sub-Fragment con Role 'component'
  │       ├── index.ts                          <-- Access Node (Rank 17)
  │       ├── table-row.component.tsx           <-- Master Node (Rank 16)
  │       ├── table-row.recipe.ts               <-- Fragment Node (Rank 4)
  │       └── table-row.type.ts                 <-- Fragment Node (Rank 6)
  ├── _table@shared/                            <-- Fractal Branch di table/
  │   ├── _contexts/                            <-- Category (Role 'context', Rank 1)
  │   │   └── table-context/                    <-- Sub-Fragment con Role 'context'
  │   │       ├── index.ts                      <-- Access Node (Rank 17)
  │   │       ├── table-context.context.ts      <-- Master Node (Rank 16)
  │   │       └── table-context.type.ts         <-- Fragment Node (Rank 6)
  │   └── _types/                               <-- Category (Role 'type', Rank 0)
  │       └── table-sort.type.ts                <-- Category Node con Role esplicito 'type'
  └── _utils/                                   <-- Private Category di table/ (Role 'util')
      └── sort-table-rows/                      <-- Sub-Fragment con Role 'util'
          ├── index.ts                          <-- Access Node (Rank 17)
          ├── sort-table-rows.spec.ts           <-- Sub-Graph Node dell'Execution Sub-Graph di Test (Rank 17)
          ├── sort-table-rows.type.ts           <-- Fragment Node (Rank 6)
          └── sort-table-rows.util.ts           <-- Master Node (Rank 11)
```

> **Nota**: Il Fragment `table/` compone cinque Sub-Fragments reciprocamente isolati nella Private Category `_components/` (`table-body/`, `table-cell/`, `table-head/`, `table-header-cell/`, `table-row/`), aggregati da `table.component.tsx` senza dipendenze orizzontali tra fratelli. Poiché `context` e `component` condividono il Rank 16 e le Private Categories sono unidirezionali, il contesto non risiede nei Fragment Nodes diretti di `table/`, bensì nel Fractal Branch `_table@shared/`: la Category `_types/` (Rank 0) espone il Category Node `table-sort.type.ts` sia alla Private Category `_utils/` sia alla Category `_contexts/` (Rank 1), la quale incapsula il Sub-Fragment `table-context/`. L'hook di lettura `use-table-context/` è invece confinato nel Fractal Branch più specifico `_components/_components@shared/`, risultando accessibile ai soli sotto-componenti di `_components/` (che consumano `table-context/index.ts` per il tramite di `use-table-context/index.ts`) e inaccessibile a `table.component.tsx` e a `_utils/`.

### 6.7. Foreign Domains

Il _Foreign Domain_ è il Logical Domain Organizational identificato da una Declaration per isolare i Foreign Nodes (es. `_tooling/`). I Foreign Domains sono a denominazione libera; ove la denominazione non sia imposta da contratti tecnologici esterni, è raccomandato il prefisso `_`.

Un Foreign Domain può essere collocato come figlio diretto di qualsiasi Logical Domain e ammette al proprio interno esclusivamente Foreign Nodes e ulteriori Foreign Domains. La Declaration si estende all'intero sotto-albero: i file sono Foreign Nodes e le directory sono Foreign Domains, senza enumerazione individuale.

La Declaration di un percorso come Foreign Domain prevale sull'associazione del nome della directory a una Category, senza modificare tale associazione nelle altre occorrenze del medesimo nome.

I Foreign Nodes esterni ai Foreign Domains sono identificati da Declarations individuali o di famiglie di file, definite da un criterio esplicito e da un ambito di applicazione. Nessun file è un Foreign Node in assenza di una Declaration che lo includa, indipendentemente da estensione o contenuto.

#### 6.7.1. Esempi di Riferimento

##### Esempio 6.7.1.1. Foreign Domain in un Root Fragment

```text
src/                                           <-- Root Fragment
  ├── app.tsx                                  <-- Root Node
  ├── main.tsx                                 <-- Root Node
  ├── README.md                                <-- Foreign Node
  └── _tooling/                                <-- Foreign Domain
      ├── globals.d.ts                         <-- Foreign Node
      ├── vite-env.d.ts                        <-- Foreign Node
      ├── vitest-setup.ts                      <-- Foreign Node
      └── ...
```

> **Nota**: `_tooling/` è un Foreign Domain identificato da una Declaration per isolare i Foreign Nodes dedicati all'ambiente e agli strumenti esterni (es. `globals.d.ts`, `vite-env.d.ts`, `vitest-setup.ts`), privi di relazioni di importazione con i file della codebase.

### 6.8. Matrice di Contenimento dei Logical Domains

La matrice riepiloga le relazioni di inclusione diretta derivanti dai contratti dei Logical Domains, senza introdurre prescrizioni ulteriori. Le righe identificano i domini genitori e le colonne i tipi di figli diretti:

| Logical Domain Genitore \ Figlio Diretto                                        | Root Nodes | Fragment Nodes | Access Node | Sub-Graph Nodes | Category Nodes | Foreign Nodes | Root Fragment | Fragment | Category | Private Category | Sub-Category | Path Sub-Category | Layer  | Root Layer | Fractal Branch | Foreign Domain |
| :------------------------------------------------------------------------------ | :--------: | :------------: | :---------: | :-------------: | :------------: | :-----------: | :-----------: | :------: | :------: | :--------------: | :----------: | :---------------: | :----: | :--------: | :------------: | :------------: |
| **Root Fragment**                                                               |   **SÌ**   |       NO       |     NO      |       NO        |       NO       |    **SÌ**     |    **SÌ**     |    NO    |    NO    |      **SÌ**      |      NO      |        NO         |   NO   |     NO     |     **SÌ**     |     **SÌ**     |
| **Fragment** _(inclusi Sub-Fragment e Path Fragment)_                           |     NO     |     **SÌ**     |   **SÌ**    |     **SÌ**      |       NO       |    **SÌ**     |      NO       |    NO    |    NO    |      **SÌ**      |      NO      |        NO         |   NO   |     NO     |     **SÌ**     |     **SÌ**     |
| **Category / Private Category / Sub-Category** _(ramificata in Sub-Categories)_ |     NO     |       NO       |     NO      |       NO        |       NO       |    **SÌ**     |      NO       |    NO    |    NO    |        NO        |    **SÌ**    |        NO         |   NO   |     NO     |     **SÌ**     |     **SÌ**     |
| **Category / Private Category / Sub-Category** _(con Fragments diretti)_        |     NO     |       NO       |     NO      |       NO        |       NO       |    **SÌ**     |      NO       |  **SÌ**  |    NO    |        NO        |      NO      |        NO         |   NO   |     NO     |     **SÌ**     |     **SÌ**     |
| **Category / Private Category / Sub-Category** _(con Category Nodes diretti)_   |     NO     |       NO       |     NO      |       NO        |     **SÌ**     |    **SÌ**     |      NO       |    NO    |    NO    |        NO        |      NO      |        NO         |   NO   |     NO     |     **SÌ**     |     **SÌ**     |
| **Parent Category di Mimetic Path Structure / Path Sub-Category**               |     NO     |       NO       |     NO      |       NO        |       NO       |    **SÌ**     |      NO       |  **SÌ**  |    NO    |        NO        |      NO      |      **SÌ**       |   NO   |     NO     |     **SÌ**     |     **SÌ**     |
| **Layer / Sub-Layer** _(ramificato in Sub-Layers)_                              |     NO     |       NO       |     NO      |       NO        |       NO       |    **SÌ**     |      NO       |    NO    |    NO    |        NO        |      NO      |        NO         | **SÌ** |     NO     |     **SÌ**     |     **SÌ**     |
| **Layer / Sub-Layer** _(con esposizione diretta di Categories)_                 |     NO     |       NO       |     NO      |       NO        |       NO       |    **SÌ**     |      NO       |    NO    |  **SÌ**  |        NO        |      NO      |        NO         |   NO   |     NO     |     **SÌ**     |     **SÌ**     |
| **Root Layer** _(stratificato in Layers)_                                       |     NO     |       NO       |     NO      |       NO        |       NO       |    **SÌ**     |      NO       |    NO    |    NO    |        NO        |      NO      |        NO         | **SÌ** |     NO     |     **SÌ**     |     **SÌ**     |
| **Root Layer** _(con esposizione diretta di Categories)_                        |     NO     |       NO       |     NO      |       NO        |       NO       |    **SÌ**     |      NO       |    NO    |  **SÌ**  |        NO        |      NO      |        NO         |   NO   |     NO     |     **SÌ**     |     **SÌ**     |
| **Fractal Branch** _(stratificato in Layers)_                                   |     NO     |       NO       |     NO      |       NO        |       NO       |    **SÌ**     |      NO       |    NO    |    NO    |        NO        |      NO      |        NO         | **SÌ** |     NO     |       NO       |     **SÌ**     |
| **Fractal Branch** _(con esposizione diretta di Categories)_                    |     NO     |       NO       |     NO      |       NO        |       NO       |    **SÌ**     |      NO       |    NO    |  **SÌ**  |        NO        |      NO      |        NO         |   NO   |     NO     |       NO       |     **SÌ**     |
| **Foreign Domain**                                                              |     NO     |       NO       |     NO      |       NO        |       NO       |    **SÌ**     |      NO       |    NO    |    NO    |        NO        |      NO      |        NO         |   NO   |     NO     |       NO       |     **SÌ**     |

### 6.9. Completezza della Classificazione

Le Declarations e le convenzioni FAF devono determinare una classificazione univoca di ogni file e directory nei Fractal Trees: ogni file è un Logical Node oppure un Foreign Node e ogni directory è un Logical Domain di un unico tipo. Un file o una directory privi di classificazione univoca costituiscono una violazione. Le Declarations devono essere complete e compatibili con la tassonomia; una Declaration non deroga ad alcuna norma FAF.

Nei contenitori idonei a ospitare Layers, le directory Organizational non classificate come Categories, Fractal Branches o Foreign Domains sono Layers. Una Horizontal Hierarchy può ordinare esclusivamente i Logical Nodes figli diretti di un Fragment, i Root Nodes di un Root Fragment, Categories sorelle non private, Sub-Categories sorelle o Layers fratelli. L'appartenenza a una Horizontal Hierarchy non modifica la classificazione di un Logical Domain.

## 7. Frontiera e Relazioni Esterne dei Fractal Trees

### 7.1. Public Surface del Fractal Tree

La _Public Surface_ di un Fractal Tree costituisce l'esclusiva interfaccia del Fractal Tree verso consumatori esterni ed è determinata dal tipo di origine:

- **Root Fragment**: una Declaration designa zero, uno o più Root Nodes del Fractal Tree come Public Surface.
- **Root Layer**: la Public Surface è determinata dalla struttura, senza Declaration aggiuntiva, e comprende esclusivamente le unità classificate dalle Categories figlie dirette del Root Layer o dei Layers contenuti nel Root Layer, incluse le relative Sub-Categories e Path Sub-Categories: di ciascun Fragment l'Access Node, di ciascun Category Node il Category Node stesso. La Public Surface non attraversa i Fragments, le Private Categories né i Fractal Branches, incluso il Fractal Branch dell'origine.

La frontiera esterna del Fractal Tree è regolata da due invarianti:

- **Opacità esterna**: dall'esterno del Fractal Tree è consentita esclusivamente l'importazione dei Logical Nodes della Public Surface.
- **Invarianza interna**: l'esposizione di un Logical Node all'esterno del Fractal Tree non altera i vincoli di visibilità interni al medesimo Fractal Tree.

### 7.2. Relazioni tra Fractal Trees

In una codebase articolata in molteplici Fractal Trees, i Fractal Trees sono reciprocamente isolati per impostazione predefinita. Qualsiasi dipendenza di un Logical Node di un Fractal Tree sorgente verso un altro Fractal Tree destinatario è interdetta, salvo Declaration che autorizzi la relazione orientata dal Fractal Tree sorgente verso il Fractal Tree destinatario.

Quando la dipendenza da un Fractal Tree sorgente verso un Fractal Tree destinatario è autorizzata, qualsiasi Logical Node del Fractal Tree sorgente — con esclusione degli Access Nodes dei Fragments, vincolati ai soli Fragment Nodes del proprio Fragment — può importare esclusivamente i Logical Nodes della Public Surface del Fractal Tree destinatario, nel rispetto dei divieti di riesportazione applicabili al nodo importatore.

Il grafo orientato delle relazioni di dipendenza tra Fractal Trees deve costituire un grafo aciclico diretto (_DAG_): è interdetto qualsiasi ciclo di dipendenze, diretto o transitivo, che coinvolga due o più Fractal Trees.

### 7.3. Relazioni con Codice Locale Esterno ai Fractal Trees

Le dipendenze verso file modulari della codebase collocati al di fuori di tutti i Fractal Trees, distinti dai pacchetti e moduli di librerie esterne alla codebase, sono soggette ai seguenti vincoli:

- **Dipendenze in uscita dal Fractal Tree**: ai Logical Nodes di un Fractal Tree, ferma restando l'esclusione degli Access Nodes dei Fragments, è interdetta l'importazione di file della codebase esterni a tutti i Fractal Trees, salvo Declaration che individui i percorsi esterni ammessi e i Logical Nodes o Logical Domains del Fractal Tree abilitati a importarli.
- **Dipendenze indotte tra Fractal Trees**: un cammino di importazione da un Logical Node di un Fractal Tree a un Logical Node di un altro Fractal Tree, che attraversa esclusivamente file esterni a tutti i Fractal Trees, costituisce una dipendenza tra i due Fractal Trees.
- **Assenza di cammini di rientro**: nessun cammino di importazione che attraversa file esterni a tutti i Fractal Trees può rientrare nel Fractal Tree di partenza.

### 7.4. Disciplina dei Path Aliases

Un _Path Alias_ è un'abbreviazione di percorso associata a una destinazione di base (es. `#_src@shared/*`, `#_app@shared/*`). L'adozione dei Path Aliases è facoltativa e disaccoppia i percorsi di importazione dalla profondità fisica dei consumatori.

L'utilizzo dei Path Aliases è soggetto a due vincoli:

- **Ancoraggio**: l'importazione mediante Path Alias di un Logical Node appartenente al medesimo Fractal Tree del Logical Node importatore richiede un Path Alias con destinazione di base in un Fractal Branch di tale Fractal Tree.
- **Invarianza**: un Path Alias non modifica il Dependency Graph né deroga ai vincoli di visibilità, incapsulamento, unidirezionalità, aciclicità e autorizzazione.

## 8. Criteri di Progettazione ed Evoluzione

### 8.1. Collocazione per Prossimità e Rilevanza di Dominio

È raccomandato collocare ciascuna unità in funzione dei consumatori dell'unità e della rilevanza del concetto implementato nel dominio applicativo:

- **Prossimità e minimo antenato comune**: un dettaglio implementativo privo di valenza autonoma nel dominio applicativo risiede nel punto più specifico compatibile con i propri consumatori — in una Private Category del singolo Fragment o Root Fragment i cui Logical Nodes diretti consumano tale dettaglio in via esclusiva, oppure nel Fractal Branch del minimo Logical Domain antenato comune a tutti i consumatori di tale dettaglio.
- **Rilevanza semantica di dominio**: un'unità che modella un concetto primario del dominio applicativo risiede nel Logical Domain Organizational che esprime la competenza architetturale dell'unità (es. un Layer o una Category del Root Layer o del Fractal Branch pertinente), anche qualora conti un unico consumatore.

### 8.2. Controllo della Profondità e Dualità tra Incapsulamento e Horizontal Hierarchy

L'annidamento eccessivo dei Logical Domains accresce il carico cognitivo di attraversamento dell'albero e occulta le entità primarie del sistema sotto catene di domini intermedi, compromettendo la leggibilità della scomposizione. È raccomandato governare la profondità del Fractal Tree bilanciando due meccanismi strutturali duali:

- **Incapsulamento verticale** (mediante Private Categories e Fractal Branches): sottrae un'unità alla visibilità esterna confinandola nel sotto-albero del dominio che la governa, ed è adottato quando l'unità costituisce un dettaglio interno non destinato all'esposizione.
- **Ordinamento orizzontale** (mediante Horizontal Hierarchies su Sub-Categories, Categories, Sub-Layers o Layers): mantiene le partizioni al medesimo livello di profondità, preservando la visibilità esterna di ciascuna partizione rispetto al dominio contenitore e vincolando in modo unidirezionale le relative dipendenze senza introdurre ulteriore annidamento. Qualora uno di due Fragments o di due Category Nodes debba dipendere dall'altro restando entrambi esposti dal dominio contenitore, è raccomandato ripartire tali unità in Sub-Categories ordinate da una Horizontal Hierarchy.

### 8.3. Evoluzione Iterativa e Ricorsiva dell'Architettura

La struttura di un sistema software conforme a FAF non richiede una definizione immutabile a priori, ma evolve attraverso un processo iterativo nel tempo e ricorsivo nella scala. Nelle fasi iniziali o esplorative di un progetto, la perimetrazione dei Fractal Trees, la scelta dell'origine di ciascun Fractal Tree (Root Fragment o Root Layer), l'articolazione dei Root Nodes e la stratificazione in Layers e Categories convergono progressivamente con il consolidarsi della comprensione del dominio applicativo, rendendo fisiologico il refactoring strutturale dell'architettura portante.

A ogni livello del Fractal Tree, è raccomandato adattare l'architettura selezionando la trasformazione dotata della massima economia concettuale tra tre operazioni strutturali:

- **Estrazione**: separazione di Symbols autonomi in Logical Nodes distinti, quali ulteriori Fragment Nodes con Roles differenti o Category Nodes di una Private Category, oppure trasformazione di un Fragment Node in un Sub-Fragment collocato in una Private Category, quando la competenza estratta acquisisce dettagli collaboranti con Roles distinti o richiede un Sub-Graph Node dedicato. L'Estrazione confina l'unità estratta nel sotto-albero del Logical Domain genitore, senza renderla accessibile a Logical Nodes esterni a tale Logical Domain.
- **Promozione**: spostamento di un'unità in una Category, eventualmente collocata in un Layer, di un Fractal Branch che ne amplia i consumatori autorizzati (es. dalla Private Category di un Fragment al Fractal Branch del medesimo Fragment, oppure dal Fractal Branch di un Logical Domain al Fractal Branch di un Logical Domain antenato). Quanto più elevato è il Logical Domain genitore del Fractal Branch destinatario, tanto più ampio è l'insieme dei consumatori autorizzati. La Promozione presuppone consumatori esterni al perimetro corrente e dipendenze ammesse dalle regole di visibilità e dalle Horizontal Hierarchies applicabili.
- **Contrazione**: rimozione o riassorbimento di Layers, Sub-Layers, Sub-Categories, Fractal Branches o Sub-Fragments divenuti ridondanti o sproporzionati rispetto alla complessità effettiva del sotto-problema risolto (ivi inclusa la riconduzione di un Fractal Branch o di un Root Layer dalla stratificazione in Layers all'esposizione diretta di Categories).

Finché il contratto esposto dall'Access Node di un Fragment rimane invariato, ogni trasformazione confinata nel sotto-albero del Fragment resta trasparente ai consumatori esterni al Fragment.

### 8.4. Isolamento delle Dipendenze Locali Esterne

Nei contesti di adozione incrementale di FAF all'interno di codebase preesistenti, o in presenza di codice generato localmente al di fuori dei Fractal Trees, è raccomandato che l'autorizzazione di dipendenze in uscita verso file locali esterni non si traduca in un accoppiamento diffuso nei Logical Nodes interni del Fractal Tree.

È raccomandato confinare tali dipendenze autorizzando l'importazione dei moduli locali esterni esclusivamente all'interno di unità adattatrici dedicate del Fractal Tree (Fragments o Category Nodes collocati nella Category e nell'eventuale Layer corrispondenti alla competenza effettiva della dipendenza esterna). In tal modo il modulo esterno viene incapsulato dietro un contratto conforme a FAF, dotato di un Role e assoggettato alle Horizontal Hierarchies interne, circoscrivendo a un unico punto di contatto l'impatto di una successiva migrazione o sostituzione.
