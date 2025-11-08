# Come estendere il Fractal Architecture Framework con RDD e TDD

**_Working Draft - 07 Novembre 2025_**

---

## Abstract

Questa è un'estensione della specifica del `Fractal Architecture Framework`. Descrive come implementare il `Readme Driven Development` e il `Test Driven Development` in un progetto `FAF`, seguendo un _workflow virtuoso_ di `Documentazione Vivente` che richiede un approccio metodico e un cambiamento culturale all'interno del team.

**Disclaimer**: Questa estensione, come tutta la specifica, è un _work in progress_, perciò si raccomanda di farne un uso consapevole.

## Per una Documentazione Vivente

L'integrazione di un `Sistema di Documentazione Vivente` in un progetto software rappresenta un cambiamento strategico per garantire che la documentazione rimanga accurata, pertinente e costantemente aggiornata con il minimo sforzo manuale. Questo approccio contrasta con la documentazione tradizionale, che spesso diventa obsoleta e inaffidabile.

### Le Caratteristiche di una Documentazione Vivente

Per definire una `Documentazione Vivente`, questa deve possedere le seguenti caratteristiche, indipendenti da come viene prodotta:

- **Vicinanza al Codice:**

  > Deve _vivere_ assieme al codice: nello stesso repository, nella stessa directory o addirittura nello stesso file.

- **Affidabilità:**

  > Deve essere corretta e riflettere le modifiche al codice. Gli sviluppatori devono potersi fidare o smetterano di aggiornarla.

- **Basso Attrito:**

  > L'aggiornamento deve essere a basso costo di manutenzione. Modificare un `README.md` nella stessa PR è a basso attrito.

- **Integrazione nel Workflow:**

  > Non è un'attività opzionale, ma una parte non negoziabile del processo di sviluppo da includere nelle revisioni delle PR.

- **Unica Fonte di Verità:**

  > La `Documentazione Vivente` mira a essere l'unica fonte autorevole.

## Il Readme Driven Development

L'`RDD` si può sintetizzare in due frasi del suo ideatore, Tom Preston-Werner:

- _"Un'implementazione perfetta della specifica sbagliata è inutile."_

- _"Scrivete prima il vostro Readme."_

Questo approccio, che prevede di scrivere il file `README.md` come primissima cosa (ancora prima di iniziare a sviluppare il codice), implica la creazione di una solida base di documentazione che si evolve insieme al codice e costringe a riflettere in anticipo sugli aspetti fondamentali del software: il suo scopo, come funzionerà e come gli altri potranno utilizzarlo o contribuire.

## Il README.md come Sistema di Documentazione Gerarchico

Un file `README.md` non dovrebbe essere considerato come un singolo file di documentazione, perché ha le caratteristiche di un `Sistema di Documentazione Gerarchico e Distribuito`. In questo sistema, il file `README.md` **principale**, che si trova nella root del progetto, ha lo scopo di fornire una visione d'insieme del software e fargli da copertina. Piattaforme come GitHub, GitLab, ecc. lo riconoscono automaticamente e lo mostrano in primo piano sulla pagina del repository. Invece, i `README.md` **interni**, quelli che si trovano nelle sottodirectory, **hanno il compito di documentare i requisiti delle singole parti**. Questa pratica riflette il `Principio della Separazione delle Competenze`, applicandolo alla documentazione: per cui **ogni documento ha una responsabilità chiara e un ambito ben definito**.

## Integrazione tra RDD e FAF

Il `Sistema di Documentazione Gerarchico e Distribuito` basato sui file `README.md` si sovrappone perfettamente a una struttura frattale. Il `Readme Driven Development` incontra il `FAF` quando quest'ultimo definisce il `Principio della Scomposizione Frattale` e il `Fragment`: una directory che rappresenta **"un'unità di logica funzionale autocontenuta e coesa"**. Allora, i `README.md` **interni** trovano una collocazione naturale, non in qualsiasi sottodirectory del codice sorgente, ma in modo esclusivo nei `Fragments`.

## Dai Requisiti alle Specifiche Eseguibili

In Ingegneria dei Requisiti si distinguono vari momenti di formalizzazione dei requisiti di un sistema software. Si tratta di un processo che dagli `User Requirements` (**cosa vuole l'utente**), passando ai `System Requirements` (**cosa deve fare il sistema**), arriva al `Software Design Specification` (**come sarà costruito il software**). Questa progressiva formalizzazione tecnica, che permette di chiarire tutti gli aspetti del software, può culminare nell'elaborazione di **specifiche eseguibili**, che sono la traduzione diretta dei `System Requirements` in codice che ne verifica l'implementazione. Non a caso, i file di test hanno spesso un suffisso o un prefisso `spec`. Questa convenzione si è diffusa con il `Behavior Driven Development`, che è un'evoluzione del `Test Driven Development`.
L'idea centrale è quella di scrivere i test in un formato che descriva il comportamento del software in un linguaggio quasi naturale e comprensibile. Per cui, laddove i `README.md` sono il luogo deputato alla scriturra dei requisiti, i test rappresentano le specifiche tecniche diventando un elemento fondamentale della `Documentazione Vivente` e la guida per l'implementazione delle parti del codice.

## Il Workflow Virtuoso del FAF con RDD e TDD

Così `FAF`, `RDD` e `TDD` si completano in un _workflow virtuoso_ che consegna le chiavi della sua efficacia nella cultura e nell'autodisciplina del team di sviluppatori. Il `Readme Driven Development` crea le fondamenta della `Documentazione Vivente` e struttura i requisiti. Il `Test Driven Development` consolida la documentazione (di cui diventa il contratto) e trasforma i requisiti in specifiche eseguibili che guidano e verificano la loro implementazione. Il `Fractal Architecture Framework` definisce il terreno su cui poggiano le altre due metodologie, dando forma all'architettura e coerenza al flusso di lavoro.

## L'Evoluzione del Workflow: l'Uso Flessibile degli Agenti IA

Il _workflow virtuoso_ appena descritto è interamente basato sull'autodisciplina del team e sulla chiarezza metodologica. Per abbattere l'attrito e massimizzarne l'efficienza, questo processo può evolvere con l'uso di agenti di intelligenza artificiale. Questa integrazione non mira a sostituire il processo, ma a potenziarlo, agendo come un **acceleratore** che mantiene inalterata la sequenza e la responsabilità dello sviluppatore, rendendo l'adozione dell'IA una scelta flessibile e non un vincolo.

### I Due Binari del Workflow

L'idea centrale è che il _workflow virtuoso_ possa operare su due binari, uno manuale e uno assistito dall'IA, conservandone l'integrità. Sia i `README.md` basati su template, sia i test come **specifiche eseguibili**, rappresentano l'interfaccia perfetta per questa interazione.

#### Fase RDD: Dalla Scrittura alla Revisione

- **Senza l'IA:** Lo sviluppatore compila manualmente il template del `README.md`, un'attività che richiede concentrazione e tempo.

- **Con l'IA:** Lo sviluppatore fornisce all'agente un input concettuale (es. il nome e lo scopo del `Fragment`). L'agente genera una bozza di alta qualità del `README.md`, completa di una descrizione plausibile, `User Stories` e `Acceptance Criteria`. Così, il ruolo dello sviluppatore si trasforma da quello di autore a quello di **revisore**, che corregge, perfeziona e valida un documento già strutturato, con un notevole risparmio di carico cognitivo.

#### Fase TDD: Dai Requisiti ai Test

- **Senza l'IA:** Lo sviluppatore traduce ogni `Acceptance Criteria` in uno scheletro di test (_test stub_) all'interno del file delle specifiche (es. `get-users.spec.ts`).

- **Con l'IA:** L'agente analizza la sezione dei `System Requirements` del `README.md` e **genera automaticamente il file di test completo di tutti gli scheletri necessari**. Lo sviluppatore può così concentrarsi immediatamente sull'implementazione della logica di test, anziché sulla stesura di codice ripetitivo.

### Conclusioni

In questa forma evoluta del _workflow virtuoso_, l'intelligenza artificiale agisce come un collega che si occupa delle attività a minor valore aggiunto, lasciando allo sviluppatore il totale controllo e la responsabilità finale. Il _workflow_ resta lo stesso, la `Documentazione Vivente` continua a essere l'_Unica Fonte di Verità_ e la cultura della qualità non viene erosa.
