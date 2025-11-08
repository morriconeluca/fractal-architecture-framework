# Fractal Architecture Framework (FAF)

**_Working Draft - 07 Novembre 2025_**

---

## Abstract

Questa specifica descrive il `Fractal Architecture Framework` (`Framework di Architettura Frattale`) (`FAF`), un framework agnostico di architettura del codice sorgente, che si ispira ai frattali naturali e in particolare al sistema complesso e auto-simile delle fronde degli alberi. Trasforma la codebase da un semplice insieme di file e cartelle in una struttura auto-esplicativa che rappresenta la scomposizione logica di un problema.

**Disclaimer**: Questa specifica è un _work in progress_, perciò si raccomanda di usare il framework consapevoli del rischio di possibili difetti. Mancano meccanismi di _enforcement_ specifici, ma si possono usare tool già esistenti (es. `eslint-plugin-boundaries`). Gli esempi presentati si riferiscono unicamente agli ecosistemi TypeScript e React anche se il `FAF` è definito come agnostico.

## Obiettivi

- **Prevedibilità**

  > Permettere una lettura intuitiva della struttura del codice e del flusso delle dipendenze.

- **Testabilità**

  > Semplificare la verifica del software, grazie a codice **disaccoppiato** e **incapsulato**.

- **Scalabilità**

  > Guidare l'evoluzione della codebase tramite un **sistema di crescita coerente e auto-simile**.

- **Manutenibilità**

  > Minimizzare i rischi e i costi degli aggiornamenti, isolando l'impatto delle modifiche.

## Concetti

- **Il Principio della Scomposizione Frattale**

  > La codebase è un problema logico da risolvere attraverso una scomposizione ricorsiva in parti più piccole. Ogni parte di questa scomposizione, a qualsiasi livello di scala, è un sotto-problema auto-simile del problema più grande.

- **Il Principio della Forma Semantica**

  > L'alberatura del codice sorgente e i nomi di file e cartelle devono rivelare lo scopo architetturale di ogni parte della codebase.

- **Il Principio della Proporzionalità**

  > La complessità della codebase deve essere direttamente proporzionale alla complessità del problema che risolve.

- **Il Grafo delle Dipendenze**

  > Il codice sorgente deve essere pensato come un grafo orientato i cui nodi si relazionano fra loro secondo rapporti di dipendenza.

- **Logical Nodes**

  > Per semplificare il `Grafo delle Dipendenze` vengono scelti i file come suoi vertici.

- **La Legge del Grafo Aciclico Diretto**

  > Il `Grafo delle Dipendenze` deve essere un `Grafo Aciclico Diretto` (`DAG`).

- **Fasi e Contesti Operativi nel Ciclo di Vita del Software**

  > È bene osservare che il ciclo di vita di un software moderno si articola in **fasi** distinte (come _build-time_ e _runtime_) e **contesti operativi** specifici (come quello applicativo e quello di test). Ognuna di queste fasi e contesti opera su un `Grafo delle Dipendenze` isolato e distinto, la cui gestione è essenziale, ma è il grafo relativo alla fase di _build-time_ quello che influenza maggiormente la progettazione, lo sviluppo e la manutenibilità della codebase.

- **Logical Domain**

  > Qualsiasi directory del codice sorgente è un confine semantico che definisce un dominio di codice correlato e incapsulato.

- **Gerarchia Ricorsiva dei Logical Domains**

  > I `Logical Domains` contenuti da un `Logical Domain` genitore, fanno parte del suo confine contestuale e semantico.

- **Fragments, Categories e Subcategories**

  > Un `Logical Domain` può essere definito come `Fragment` (es. `cart/`, `get-users/`), `Category` (es. `components/`, `utils/`) o `Subcategory` (es. `atoms/`, `molecules/` che nell'_Atomic Design_ sono `Subcategories` di `components/`).

  - **Fragments**

    > Il `Logical Domain` definito come un `Fragment` è una porzione auto-simile dell'architettura, ossia un sotto-problema logico all'interno della scomposizione frattale che, a sua volta, può essere scomposto in `Fragments` più piccoli, in modo ricorsivo e auto-simile. È **un'unità di logica funzionale autocontenuta e coesa** che espone una o più interfacce pubbliche necessarie per interagire con essa (es. una feature di business, un componente UI, una rotta del backend, ecc.).

  - **Fragments e Logical Nodes**

    > Il nome di un `Fragment` formalizza la parte fondamentale del nome dei file di primo livello che gli appartengono e che ne rappresentano l'immediata scomposizione logica (es. `button.component.tsx`, `button.util.ts`). Possiamo infatti pensare a un `Fragment` come a un `Logical Node` che è stato scomposto in diversi `Logical Nodes` che a loro volta potrebbero essere scomposti in altri `Logical Nodes` incapsulati in `Fragments` e cosi via.

  - **Logical Nodes e Roles**

    > I nomi dei `Logical Nodes` dovrebbero contenere un **suffisso** o un **prefisso** per indicare il `Role` dei file (es. `get-users.spec.ts` in TypeScript, `test_get_users.py` in Python). Per coerenza, devono essere indicati al **singolare** e sono separati dal resto del nome del file per mezzo del punto `.` o di un altro separatore in base alle convenzioni del linguaggio, del framework o della tecnologia: inoltre devono essere omessi quando confliggono con esse (es. `index.ts` in TypeScript, `main.tsx` l'_entrypoint_ di default di un progetto Vite.js/React, i file `page.tsx`, `layout.tsx`, ecc. in Next.js).

  - **Fragments ed Entry Files**

    > All'interno di un `Fragment` possono convivere molteplici _Entry Files_ in base ai flussi di esecuzione esistenti. Per esempio, avremo un _Entry File_ anche per il contesto operativo di test (es. `button.spec.tsx`).

    **Esempio:**

    > In TypeScript il _Barrel File_ (`index.ts`) è uno strumento utile a controllare ciò che si esporta all'esterno di una directory. In questo esempio serve a riesportare il componente React contenuto nel `Logical Node` che ha dato origine al `Fragment` (`button.component.tsx`) e la sua interfaccia, presente in `button.model.ts`. Il resto del codice non è esposto fuori dal `Fragment`, perché è un dettaglio implementativo privato o perché non fa parte del `Grafo delle Dipendenze` principale.

    ```text
      button/                         <----- Fragment con Role 'component'
        ├── README.md                 <----- File di documentazione del Fragment
        ├── button.component.tsx      <----- Il file che origina il Fragment
        ├── button.hook.ts
        ├── button.model.ts           <----- Interfaccia del Fragment
        ├── button.spec.tsx           <----- Entry File per i test
        ├── button.style.ts
        ├── button.story.tsx          <----- Entry File per Storybook
        ├── button.util.ts
        └── index.ts                  <----- Barrel File che esporta componente e interfaccia
    ```

  - **Categories, Subcategories e Roles**

    > Il `Logical Domain` definito come `Category` o `Subcategory` è quello che contiene ed esporta, direttamente o no, molteplici unità di logica funzionale con lo stesso `Role`. Le `Categories` e le `Subcategories` possono contenere molteplici `Subcategories`, `Fragments` o `Logical Nodes`. Non servono a scomporre un problema logico in sotto-problemi, ma a organizzare e raggruppare i sotto-problemi logici per tipologia: ossia molteplici `Fragments` o molteplici `Logical Nodes` con lo stesso `Role`.

    **Esempio:**

    ```text
    components/                       <----- Category che dichiara il Role 'component'
    ├── index.ts
    ├── atoms/                        <----- Subcategory con finalità organizzativa
    │   ├── index.ts
    │   └── ...
    ├── molecules/                    <----- Subcategory con finalità organizzativa
    │   ├── index.ts
    │   └── ...
    ├── organisms/                    <----- Subcategory con finalità organizzativa
    │   ├── index.ts
    │   └── ...
    └── templates/                    <----- Subcategory con finalità organizzativa
        ├── index.ts
        └── ...
    ```

  - **Categories e Roles**

    > Il nome di una `Category` equivale alla forma plurale del `Role` delle unità di logica funzionale che esporta. Di contro, il `Role` è anche l'aspettativa architetturale che una `Category` impone ai figli agendo come vincolo. Perciò, la nomenclatura dei `Roles` e quella delle `Categories` sono strettamente legate e rappresentano un fondamento dell'auto-similarità di un'architettura frattale. Identificare e definire un nuovo `Role` all'interno della codebase significa prendere un'importante decisione architetturale, che può scaturire sia dall'osservazione delle caratteristiche di un `Logical Node`, sia dalla creazione di una nuova `Category` che evidenzia la necessità di un nuovo `Role`.

    **Esempio 1:**

    ```text
    components/                           <----- Category che dichiara il Role 'component'
    ├── index.ts
    ├── atoms/                            <----- Subcategory con finalità organizzativa
    │   ├── index.ts
    │   ├── avatar/                       <----- Fragment con Role 'component'
    │   │   ├── README.md
    │   │   ├── avatar.component.tsx      <----- Il file che origina il Fragment
    │   │   ├── avatar.hook.ts            <----- 'hook' è coerente con una Category hooks/
    │   │   ├── avatar.model.ts           <----- 'model' è coerente con una Category models/
    │   │   ├── avatar.spec.tsx           <----- 'spec' è coerente con una Category specs/
    │   │   ├── avatar.story.tsx          <----- 'story' è coerente con una Category stories/
    │   │   ├── avatar.style.ts           <----- 'style' è coerente con una Category styles/
    │   │   ├── avatar.util.ts            <----- 'util' è coerente con una Category utils/
    │   │   └── index.ts
    │   ├── icon/                         <----- Fragment con Role 'component'
    │   │   ├── README.md
    │   │   ├── icon.component.tsx        <----- Il file che origina il Fragment
    │   │   ├── icon.hook.ts
    │   │   ├── icon.model.ts
    │   │   ├── icon.spec.tsx
    │   │   ├── icon.story.tsx
    │   │   ├── icon.style.ts
    │   │   ├── icon.util.ts
    │   │   └── index.ts
    │   └── ...
    ├── molecules/
    │   ├── index.ts
    │   ├── button/                       <----- Fragment con Role 'component'
    │   │   ├── README.md
    │   │   ├── button.component.tsx      <----- Ciò che resta del file che origina il Fragment
    │   │   ├── button.hook.ts
    │   │   ├── button.model.ts
    │   │   ├── button.spec.tsx
    │   │   ├── button.story.tsx
    │   │   ├── button.style.ts
    │   │   ├── button.util.ts
    │   │   └── index.ts
    │   ├── input/                        <----- Fragment con Role 'component'
    │   │   ├── README.md
    │   │   ├── input.component.tsx       <----- Ciò che resta del file che origina il Fragment
    │   │   ├── input.hook.ts
    │   │   ├── input.model.ts
    │   │   ├── input.spec.tsx
    │   │   ├── input.story.tsx
    │   │   ├── input.style.ts
    │   │   ├── input.util.ts
    │   │   └── index.ts
    │   └── ...
    └── ...
    ```

    **Esempio 2:**

    > In questo secondo esempio la creazione di una `Category` `pages/` determina l'esigenza di definire un nuovo `Role` (`page`) laddove normalmente avremmo usato `component`.

    ```text
    pages/                            <----- Category che dichiara il Role 'page'
    ├── index.ts
    ├── about/
    │   ├── README.md
    │   ├── about.hook.ts
    │   ├── about.model.ts
    │   ├── about.page.tsx            <----- Il file che origina il Fragment
    │   ├── about.spec.tsx
    │   ├── about.style.ts
    │   ├── about.util.ts
    │   ├── index.ts
    │   └── ...
    ├── blog/
    │   ├── README.md
    │   ├── blog.hook.ts
    │   ├── blog.model.ts
    │   ├── blog.page.tsx             <----- Il file che origina il Fragment
    │   ├── blog.spec.tsx
    │   ├── blog.style.ts
    │   ├── blog.util.ts
    │   ├── index.ts
    │   └── ...
    └── ...
    ```

    **Esempio 3:**

    > In questo terzo esempio il _Barrel File_ (`index.ts`) serve a riesportare le singole utility e le relative interfacce che convivono pragmaticamente negli stessi file.

    ```text
      utils/                      <----- Category che dichiara il Role 'util'
        ├── get-product-sizes-by-variant-id.util.ts
        ├── get-product-variants-by-id.util.ts
        ├── index.ts              <----- Barrel File che riesporta le utility e le interfacce
        ├── is-product-out-of-stock.util.ts
        ├── is-product-variant-out-of-stock.util.ts
        └── is-product-variant-size-out-of-stock.util.ts
    ```

    **Esempio 4:**

    > In questo quarto esempio si rielabora l'architettura dell'esempio precedente, preferendo al pragmatismo un approccio più strutturato che, nel lungo periodo, offre vantaggi in termini di leggibilità, scalabilità, manutenibilità e coerenza. I singoli `Logical Nodes`, in cui convivevano le utility e le loro interfacce, sono stati scomposti in `Fragments`.

    ```text
      utils/                      <----- Category che dichiara il Role 'util'
        ├── index.ts              <----- Il Barrel File che riesporta le utility e le interfacce
        ├── get-product-sizes-by-variant-id/                     <----- Fragment con Role 'util'
        │   ├── README.md
        │   ├── get-product-sizes-by-variant-id.model.ts
        │   ├── get-product-sizes-by-variant-id.util.ts          <----- L'origine del Fragment
        │   └── index.ts
        ├── get-product-variants-by-id/                          <----- Fragment con Role 'util'
        │   ├── README.md
        │   ├── get-product-variants-by-id.model.ts
        │   ├── get-product-variants-by-id.util.ts.              <----- L'origine del Fragment
        │   └── index.ts
        ├── is-product-out-of-stock/                             <----- Fragment con Role 'util'
        │   ├── README.md
        │   ├── is-product-out-of-stock.model.ts
        │   ├── is-product-out-of-stock.util.ts                  <----- L'origine del Fragment
        │   └── index.ts
        ├── is-product-variant-out-of-stock/                     <----- Fragment con Role 'util'
        │   ├── README.md
        │   ├── is-product-variant-out-of-stock.model.ts
        │   ├── is-product-variant-out-of-stock.util.ts          <----- L'origine del Fragment
        │   └── index.ts
        ├── is-product-variant-size-out-of-stock/                <----- Fragment con Role 'util'
        │   ├── README.md
        │   ├── is-product-variant-size-out-of-stock.model.ts
        │   ├── is-product-variant-size-out-of-stock.util.ts     <----- L'origine del Fragment
        │   └── index.ts
        └── ...
    ```

- **Struttura Gerarchica Orizzontale o tra Pari**

  > Una struttura gerarchica orizzontale o tra pari è una struttura orizzontale costituita da file o directory che hanno relazioni di dipendenza tra loro (es. le `Subcategories` dell'_Atomic Design_, i `Logical Nodes` di primo livello di un `Fragment`). **Una struttura di questo tipo è la semplificazione di una struttura gerarchica verticale.**

- **La Regola dell'Ordine Gerarchico Orizzontale**

  > Le relazioni di dipendenza tra pari devono sempre seguire precisi ordini gerarchici che dovrebbero essere formalizzati e documentati nella codebase nel file README deputato alla descrizione dell'architettura, e garantiti da strumenti di linting. Per esempio, andrebbe introdotta una sezione della documentazione che definisca esplicitamente le relazioni di dipendenza consentite tra i `Roles`, così come servirebbero meccanismi di _enforcement_.

  - **L'Ordine Gerarchico Orizzontale tra Categories o Subcategories**

    > La direzione del flusso di dipendenze tra `Categories` o tra `Subcategories`, facenti parte di una struttura orizzontale, deve essere intuibile dalla loro nomenclatura (es. `organisms/ -> molecules/ -> atoms/` nell'_Atomic Design_).

  - **L'Ordine Gerarchico Orizzontale tra Logical Nodes**

    > Le relazioni di dipendenze tra `Logical Nodes` (es. quelli di primo livello di un `Fragment`) deve essere intuibile dai nomi e dai `Roles` dei singoli file (es. `index.ts -> button.component.tsx -> button.hook.ts -> button.util.ts`, ma anche `button.component.tsx -> button.model.ts` e `button.hook.ts -> button.model.ts`, ecc.).

- **Fractal Branches**

  > Sono `Logical Domains` speciali che seguono specifiche convenzioni di nomenclatura. Un `Fractal Branch` è un contenitore privato di dipendenze, accessibile esclusivamente dai file appartenenti allo `Scope` a cui il `Fractal Branch` si riferisce. Serve a tracciare le relazioni di dipendenza e a favorire l'incapsulamento e la scomposizione del codice, poiché è il punto da cui ramificano le dipendenze, permettendo di scomporre le unità logiche funzionali di un `Fragment` in unità più elementari in modo ricorsivo e auto-simile (dando origine in questo modo a una struttura gerarchica verticale), oppure permettendo di elevare uno spazio condiviso di codice all'interno di un `Logical Domain` che ne possa fruire.

- **Visibilità e Incapsulamento del Codice**

  > È importante controllare la visibilità del codice: ciò che deve essere accessibile e ciò che deve restare nascosto in `Fragments`, `Categories`, `Subcategories` e `Fractal Branches`. Per tale scopo si usano gli strumenti peculiari del linguaggio (es. _Barrel Files_ in TypeScript come contratto pubblico di un `Logical Domain`), perché è fondamentale nascondere i dettagli di implementazione ed esporre unicamente ciò che serve di quanto si trova al primo livello di nidificazione, in maniera ricorsiva.

- **La Regola delle Dipendenze**

  > In un'architettura frattale del codice sorgente, qualsiasi dipendenza che attraversa il confine di un `Logical Domain` non deve mai puntare verso un dettaglio di implementazione che non sia il proprio, poiché ciò ne violerebbe l'incapsulamento. Ciò vuol dire che un `Logical Domain` è come un'istanza di una classe. È possibile interagire solo con i suoi metodi pubblici (es. in TypeScript, ciò che è riesportato dai _Barrel Files_ `index.ts`), non con le sue proprietà private (i file interni).

## Convenzioni Generali di Nomenclatura

Si raccomanda l'uso del **`kebab-case`** per tutti i nomi di file e cartelle, a eccezione dei casi in cui la convenzione sia definita dal linguaggio, dal framework o dalla tecnologia. Il `kebab-case` **previene problemi di _case sensitivity_ e si allinea alle best practice per gli URL web**. Tuttavia, se esistono convenzioni forti e consolidate (es. `snake_case` in Python), quest'ultime devono essere preferite.

## Fractal Branches, Scopes e Convenzioni di Nomenclatura

Esistono due tipi di `Fractal Branch`, distinti per finalità e nomenclatura.

**Sintassi di Base:** Prevede un prefisso `__` (che denota la natura privata della directory).

### 1. Private Fractal Branches (Fractal Branches di Logical Node)

Le dipendenze sono accessibili **esclusivamente** dal `Logical Node` a cui si riferisce, permettendo la scomposizione frattale in scenari complessi e granulari, perciò si parla di **Scope di Logical Node o Privato**.

**Sintassi:** `__[nome file completo di Role (se esiste) senza estensione]`

**Esempio in un progetto Vite.js/React:**

```text
src/
├── README.md
├── main.tsx
└── __main/                         <----- Private Fractal Branch del file main.tsx (senza Role)
    ├── index.ts
    └── pages/
        ├── index.ts
        ├── about/
        │   ├── README.md
        │   ├── about.hook.ts
        │   ├── about.model.ts
        │   ├── about.page.tsx
        │   ├── about.spec.tsx
        │   ├── about.style.ts
        │   ├── about.util.ts
        │   ├── index.ts
        │   └── __about.page/       <----- Private Fractal Branch del file about.page.tsx
        │       ├── index.ts
        │       └── ...
        └── ...
```

### 2. Shared Fractal Branches (Fractal Branches di Logical Domain)

Le dipendenze sono accessibili da **tutti** i `Logical Nodes` contenuti nel `Logical Domain` genitore, anche ricorsivamente, anche nidificati in `Fractal Branches` sia privati, sia condivisi, perciò si parla di **Scope di Logical Domain o Shared**.

**Sintassi:** `__shared`

**Esempio in un progetto Next.js:**

```text
app/
├── README.md
├── page.tsx
├── layout.tsx
├── about/
│   └── ...
└── __shared/        <----- Shared Fractal Branch di tutto il Logical Domain app/
    ├── index.ts
    └── ...
```

### Fractal Braches Innestati

La logica descritta fin qui per i `Fractal Branches` si applica anche ricorsivamente. Un `Fractal Branch` può quindi contenere anche direttamente al suo interno altri `Fractal Branches` (sia privati, sia condivisi).

**Esempio in un progetto Next.js:**

```text
app/
├── README.md
├── page.tsx
├── layout.tsx
├── ...
└── __shared/
    ├── index.ts
    ├── ...
    └── __shared/           <----- Shared Fractal Branch del Logical Domain __shared/ genitore
        ├── index.ts
        └── ...
```

### Raccomandazioni di Nomenclatura

Per preservare la coerenza e la prevedibilità del framework, si raccomanda di non usare queste convenzioni per scopi diversi.

## Esempio di Architettura Frattale in un Progetto Vite.js/React

Questo esempio evidenzia come l'architettura frattale si adatti a pattern consolidati come l'_Atomic Design_ e scali in complessità. Si notino in particolare due aspetti:

- La `Category` `pages/` è gestita come una dipendenza privata dell'entrypoint `main.tsx` attraverso il `Private Fractal Branch` `__main/`, separando nettamente la struttura delle viste applicative dalla libreria di componenti condivisi (`__shared/`).

- La scomposizione frattale applicata al `Fragment` `select/` è granulare. Il componente complesso viene risolto ricorsivamente attraverso la creazione di sotto-problemi logici auto-simili (`list/`, `trigger/`, `option/`), ognuno incapsulato nel proprio `Logical Domain`. L'architettura risultante promuove così in modo naturale **un'alta coesione** e **un basso accoppiamento**, grazie a confini e contratti pubblici rigorosi.

```text
src/
├── README.md
├── main.tsx
├── __main/
│   └── pages/
│       ├── index.ts
│       ├── about/
│       │   ├── README.md
│       │   ├── about.hook.ts
│       │   ├── about.model.ts
│       │   ├── about.page.tsx
│       │   ├── about.spec.tsx
│       │   ├── about.style.ts
│       │   ├── about.util.ts
│       │   ├── index.ts
│       │   └── __about.page/
│       │       ├── index.ts
│       │       ├── components/
│       │       │   ├── index.ts
│       │       │   └── ...
│       │       └── ...
│       ├── blog/
│       │   ├── README.md
│       │   ├── blog.hook.ts
│       │   ├── blog.model.ts
│       │   ├── blog.page.tsx
│       │   ├── blog.spec.tsx
│       │   ├── blog.style.ts
│       │   ├── blog.util.ts
│       │   ├── index.ts
│       │   └── __blog.page/
│       │       ├── index.ts
│       │       ├── components/
│       │       │   ├── index.ts
│       │       │   └── ...
│       │       └── ...
│       ├── contact-us/
│       │   ├── README.md
│       │   ├── contact-us.hook.ts
│       │   ├── contact-us.model.ts
│       │   ├── contact-us.page.tsx
│       │   ├── contact-us.spec.tsx
│       │   ├── contact-us.style.ts
│       │   ├── contact-us.util.ts
│       │   ├── index.ts
│       │   └── __contact-us.page/
│       │       ├── index.ts
│       │       ├── components/
│       │       │   ├── index.ts
│       │       │   └── ...
│       │       └── ...
│       ├── home/
│       │   ├── README.md
│       │   ├── home.hook.ts
│       │   ├── home.model.ts
│       │   ├── home.page.tsx
│       │   ├── home.spec.tsx
│       │   ├── home.style.ts
│       │   ├── home.util.ts
│       │   ├── index.ts
│       │   └── __home.page/
│       │       ├── index.ts
│       │       ├── components/
│       │       │   ├── index.ts
│       │       │   └── ...
│       │       └── ...
│       └── ...
└── __shared/
    ├── index.ts
    ├── components/
    │   ├── index.ts
    │   ├── atoms/
    │   │   ├── index.ts
    │   │   ├── icon/
    │   │   │   ├── README.md
    │   │   │   ├── icon.component.tsx
    │   │   │   ├── icon.hook.ts
    │   │   │   ├── icon.model.ts
    │   │   │   ├── icon.spec.tsx
    │   │   │   ├── icon.story.tsx
    │   │   │   ├── icon.style.ts
    │   │   │   ├── icon.util.ts
    │   │   │   └── index.ts
    │   │   ├── image/
    │   │   │   ├── README.md
    │   │   │   ├── image.component.tsx
    │   │   │   ├── image.hook.ts
    │   │   │   ├── image.model.ts
    │   │   │   ├── image.spec.tsx
    │   │   │   ├── image.story.tsx
    │   │   │   ├── image.style.ts
    │   │   │   ├── image.util.ts
    │   │   │   └── index.ts
    │   │   └── ...
    │   ├── molecules/
    │   │   ├── index.ts
    │   │   ├── button/
    │   │   │   ├── README.md
    │   │   │   ├── button.component.tsx
    │   │   │   ├── button.hook.ts
    │   │   │   ├── button.model.ts
    │   │   │   ├── button.spec.tsx
    │   │   │   ├── button.story.tsx
    │   │   │   ├── button.style.ts
    │   │   │   ├── button.util.ts
    │   │   │   └── index.ts
    │   │   ├── input/
    │   │   │   ├── README.md
    │   │   │   ├── index.ts
    │   │   │   ├── input.component.tsx
    │   │   │   ├── input.hook.ts
    │   │   │   ├── input.model.ts
    │   │   │   ├── input.spec.tsx
    │   │   │   ├── input.story.tsx
    │   │   │   ├── input.style.ts
    │   │   │   └── input.util.ts
    │   │   └── ...
    │   ├── organisms/
    │   │   ├── index.ts
    │   │   ├── select/
    │   │   │   ├── README.md
    │   │   │   ├── index.ts
    │   │   │   ├── select.component.tsx
    │   │   │   ├── select.hook.ts
    │   │   │   ├── select.model.ts
    │   │   │   ├── select.spec.tsx
    │   │   │   ├── select.story.tsx
    │   │   │   ├── select.style.ts
    │   │   │   ├── select.util.ts
    │   │   │   ├── __select.component/
    │   │   │   │   ├── index.ts
    │   │   │   │   └── components/
    │   │   │   │       ├── index.ts
    │   │   │   │       ├── list/
    │   │   │   │       │   ├── README.md
    │   │   │   │       │   ├── index.ts
    │   │   │   │       │   ├── list.component.tsx
    │   │   │   │       │   ├── list.hook.ts
    │   │   │   │       │   ├── list.model.ts
    │   │   │   │       │   ├── list.spec.tsx
    │   │   │   │       │   ├── list.style.ts
    │   │   │   │       │   ├── list.util.ts
    │   │   │   │       │   └── __list.component/
    │   │   │   │       │       ├── index.ts
    │   │   │   │       │       └── components/
    │   │   │   │       │           ├── index.ts
    │   │   │   │       │           └── option/
    │   │   │   │       │               ├── README.md
    │   │   │   │       │               ├── index.ts
    │   │   │   │       │               ├── option.component.tsx
    │   │   │   │       │               ├── option.hook.ts
    │   │   │   │       │               ├── option.model.ts
    │   │   │   │       │               ├── option.spec.tsx
    │   │   │   │       │               ├── option.style.ts
    │   │   │   │       │               └── option.util.ts
    │   │   │   │       └── trigger/
    │   │   │   │           ├── README.md
    │   │   │   │           ├── index.ts
    │   │   │   │           ├── trigger.component.tsx
    │   │   │   │           ├── trigger.hook.ts
    │   │   │   │           ├── trigger.model.ts
    │   │   │   │           ├── trigger.spec.tsx
    │   │   │   │           ├── trigger.style.ts
    │   │   │   │           └── trigger.util.ts
    │   │   │   └── __shared/
    │   │   │       ├── index.ts
    │   │   │       └── select-item.model.ts
    │   │   └── ...
    │   └── templates/
    │       ├── index.ts
    │       └── ...
    ├── hooks/
    │   ├── index.ts
    │   └── ...
    ├── models/
    │   ├── index.ts
    │   └── ...
    ├── styles/
    │   ├── index.ts
    │   └── ...
    └── utils/
        ├── index.ts
        └── ...
```

## Esempio di Riscrittura di un'Architettura n-Tier come Architettura Frattale

Questo esempio descrive la riscrittura di un semplice progetto backend con `Architettura N-Tier` usando il `Fractal Architecture Framework`. Emergono i vantaggi del `FAF` in termini di alta coesione, basso accoppiamento, leggibilità e scalabilità, mostrando come la forma stessa dell'architettura possa diventare una guida per l'evoluzione del software.

### Un Semplice Progetto Backend con Architettura n-Tier

L'`Architettura N-Tier` è un approccio consolidato che organizza il codice sorgente per _layer_ (es. _Router_, _Controller_, _Service Layer_, _Data Access Layer_, ecc.). Questo modello si traduce in una **struttura gerarchica orizzontale** in cui la logica di una singola funzionalità di business (es. la gestione degli utenti) risulta frammentata tra molteplici cartelle. Questa dispersione promuove una **bassa coesione** e un **alto accoppiamento** tra i _layer_, rendendo la codebase progressivamente più difficile da decifrare: la sua forma rivela l'organizzazione tecnica, ma nasconde le relazioni logiche e funzionali tra le sue parti, complicando la manutenzione e l'evoluzione del progetto.

```text
src/
├── index.ts
├── controllers/
│   ├── authentication.ts
│   └── users.ts
├── db/
│   └── users.ts
├── helpers/
│   └── index.ts
├── middlewares/
│   └── index.ts
└── router/
    ├── authentication.ts
    ├── index.ts
    └── users.ts

```

### Riscrittura dello Stesso Progetto Backend con FAF

Il `FAF` abbandona la logica dei _layer_ per adottare una scomposizione frattale basata su `Categories`, `Subcategories` e `Fragments`. La struttura che ne deriva rende comprensibile lo scopo di ogni sua parte. L'uso dei `Fragments` per incapsulare le singole rotte e di `Fractal Branches` (es. `__main/`, `__app/`, `__shared/`) per gestire gli scope di visibilità e le dipendenze condivise, favorisce una **scomposizione granulare e controllata**. In questo modo, il codice sorgente diventa **più coeso e disaccoppiato**, e la prevedibilità dell'architettura guida lo sviluppatore nella manutenzione e nell'evoluzione del progetto.

```text
src/
├── README.md
├── app.ts
├── main.ts
├── __app/
│   ├── index.ts
│   ├── routers/
│   │   ├── index.ts
│   │   ├── __shared/
│   │   │   ├── index.ts
│   │   │   ├── helpers/
│   │   │   │   ├── index.ts
│   │   │   │   ├── authenticate/
│   │   │   │   │   ├── README.md
│   │   │   │   │   ├── authenticate.helper.ts
│   │   │   │   │   └── index.ts
│   │   │   │   └── generate-salt/
│   │   │   │       ├── README.md
│   │   │   │       ├── generate-salt.helper.ts
│   │   │   │       └── index.ts
│   │   │   └── middlewares/
│   │   │       ├── index.ts
│   │   │       ├── is-authenticated/
│   │   │       │   ├── README.md
│   │   │       │   ├── index.ts
│   │   │       │   └── is-authenticated.middleware.ts
│   │   │       └── is-owner/
│   │   │           ├── README.md
│   │   │           ├── index.ts
│   │   │           └── is-owner.middleware.ts
│   │   └── v1/
│   │       ├── README.md
│   │       ├── index.ts
│   │       ├── v1.router.ts
│   │       └── __v1.router/
│   │           ├── index.ts
│   │           └── routes/
│   │               ├── index.ts
│   │               ├── auth/
│   │               │   ├── index.ts
│   │               │   ├── login/
│   │               │   │   ├── README.md
│   │               │   │   ├── index.ts
│   │               │   │   ├── login.controller.ts
│   │               │   │   └── login.route.ts
│   │               │   └── register/
│   │               │       ├── README.md
│   │               │       ├── index.ts
│   │               │       ├── register.controller.ts
│   │               │       └── register.route.ts
│   │               └── users/
│   │                   ├── index.ts
│   │                   ├── delete-user/
│   │                   │   ├── README.md
│   │                   │   ├── delete-user.controller.ts
│   │                   │   ├── delete-user.route.ts
│   │                   │   └── index.ts
│   │                   ├── get-user/
│   │                   │   ├── README.md
│   │                   │   ├── get-user.controller.ts
│   │                   │   ├── get-user.route.ts
│   │                   │   └── index.ts
│   │                   └── update-user/
│   │                       ├── README.md
│   │                       ├── index.ts
│   │                       ├── update-user.controller.ts
│   │                       └── update-user.route.ts
│   └── __shared/
│       ├── index.ts
│       └── operations/
│           ├── index.ts
│           ├── __shared/
│           │   ├── index.ts
│           │   └── dbmodels/
│           │       ├── index.ts
│           │       └── user/
│           │           ├── README.md
│           │           ├── index.ts
│           │           ├── user.dbmodel.ts
│           │           └── user.schema.ts
│           ├── mutations/
│           │   ├── index.ts
│           │   └── users/
│           │       ├── index.ts
│           │       ├── create-user/
│           │       │   ├── README.md
│           │       │   ├── create-user.operation.ts
│           │       │   └── index.ts
│           │       ├── delete-user-by-id/
│           │       │   ├── README.md
│           │       │   ├── delete-user-by-id.operation.ts
│           │       │   └── index.ts
│           │       └── update-user-by-id/
│           │           ├── README.md
│           │           ├── index.ts
│           │           └── update-user-by-id.operation.ts
│           └── queries/
│               ├── index.ts
│               └── users/
│                   ├── index.ts
│                   ├── get-user-by-email/
│                   │   ├── README.md
│                   │   ├── get-user-by-email.operation.ts
│                   │   └── index.ts
│                   ├── get-user-by-id/
│                   │   ├── README.md
│                   │   ├── get-user-by-id.operation.ts
│                   │   └── index.ts
│                   └── get-user-by-session-token/
│                       ├── README.md
│                       ├── get-user-by-session-token.operation.ts
│                       └── index.ts
└── __main
    ├── index.ts
    └── helpers
        ├── index.ts
        └── connect-to-db
            ├── README.md
            ├── connect-to-db.helper.ts
            └── index.ts

```

### Pro e Contro dell'Adozione del FAF

L'adozione del `Fractal Architecture Framework` offre importanti vantaggi in termini di **scalabilità**, **manutenibilità** e **prevedibilità**, promuovendo un **basso accoppiamento** e un'**alta coesione** del codice, grazie a confini (`Logical Domains`) e contratti pubblici ben definiti. Tuttavia, è innegabile che questo approccio introduce una **curva di apprendimento** che può rappresentare un ostacolo per i team abituati ad architetture più tradizionali. Inoltre, la sua natura prescrittiva può portare a una maggiore **verbosità** e alla generazione di un apparente _boilerplate_ strutturale nella codebase.

## L'Architettura Frattale come Algoritmo

In senso lato, un algoritmo è un insieme finito di istruzioni chiare e non ambigue, che definisce una sequenza di passi per risolvere un problema specifico o completare un'attività. Perciò, l'architettura frattale, che definisce la codebase come un problema logico da scomporre e risolvere, presenta le caratteristiche di un algoritmo e pone l'attenzione sulla necessità da parte degli sviluppatori di **guardare all'architettura di file e cartelle con la stessa attitudine con cui si guarda al codice (_Architecture as Code_)**.

## A chi si rivolge

Il `Fractal Architecture Framework` non è una soluzione adatta a ogni progetto. **È una metodologia _opinionated_** che privilegia la robustezza e la coerenza, anziché la velocità di implementazione iniziale. È stato progettato per rispondere alle esigenze di specifici contesti di sviluppo, dove la chiarezza strutturale e la salute del progetto a lungo termine sono considerate priorità. Si rivolge in particolare a:

- **Team di Prodotto**

  > Che operano su codebase complesse e di lunga durata, dove la manutenibilità e la scalabilità sono requisiti non negoziabili.

- **Architetti del Software**

  > Che cercano un sistema prescrittivo per guidare l'evoluzione della codebase, garantendo coerenza e riducendo il debito tecnico.

- **Sviluppatori**

  > Che desiderano una struttura di progetto chiara e auto-esplicativa, che semplifichi l'_onboarding_ di nuovi membri nel team.

- **Entusiasti dell'Uso di AI Agents per la Generazione di Codice**

  > Che intendono sfruttare la prevedibilità del `FAF` come _guardrail_ architetturale per far generare codice coerente e di alta qualità.
