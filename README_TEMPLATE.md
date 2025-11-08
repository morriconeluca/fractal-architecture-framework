# FAF System Requirements Document for {{FRAGMENT NAME}}

<!-- Il presente documento definisce i requisiti di sistema di questo Fragment. Serve come "Unica Fonte di Verità" per guidare lo sviluppo e i test. Compilare ogni sezione in modo chiaro e conciso. I placeholder {{NOME PLACEHOLDER}} devono essere sostituiti con i valori specifici. -->

**Fragment_Name:** {{FRAGMENT NAME}}

**Fragment_Role:** {{FRAGMENT ROLE}}

**Parent_README_Reference:** [{{PARENT NAME}}/README.md]({{PARENT README REF}})

<!-- Link al README del Fragment genitore. Se non esiste, può essere omesso o linkare al README principale del progetto. -->

## Description

<!-- Descrivere in una o due frasi cos'è questo Fragment e a cosa serve. Focalizzarsi sul "perché" esiste. -->

{{FRAGMENT DESCRIPTION}}

### What it must NOT do

<!-- Questa sezione è cruciale per definire i confini. Elencare esplicitamente ciò che è fuori dallo scopo di questo Fragment previene complessità non necessarie e ne promuove la riusabilità. -->

_Lista delle cose che NON deve fare:_

- {{WHAT IT MUST NOT DO 1}}
- {{WHAT IT MUST NOT DO 2}}
- ...

## Fractal Break Down

<!-- Elencare qui SOLO i Fragment figli diretti. I dettagli di ogni figlio sono demandati al rispettivo README, creando una gerarchia navigabile. -->

_Lista dei `Fragments` dello stesso `Role` da cui questo `Fragment` dipende direttamente e che appartengono al suo `Logical Domain`._

### Private Fractal Dependencies

<!-- Dipendenze che sono un dettaglio implementativo di QUESTO Fragment. Non dovrebbero essere usate da nessun altro. -->

- **SFN_P1:** {{SUB FRAGMENT NAME P1}}

  - **README Reference**: [{{SUB FRAGMENT NAME P1}}/README.md](./__{{Fragment_Name}}.{{Fragment_Role}}/{{Fragment_Role}}s/{{SFN_P1}}/README.md)

- **SFN_P2:** {{SUB FRAGMENT NAME P2}}

  - **README Reference**: [{{SUB FRAGMENT NAME P2}}/README.md](./__{{Fragment_Name}}.{{Fragment_Role}}/{{Fragment_Role}}s/{{SFN_P2}}/README.md)

- ...

### Shared Fractal Dependencies

<!-- Dipendenze che sono un dettaglio implementativo di QUESTO Fragment. Possono essere usate anche da altri Fragments all'interno di QUESTO Logical Domain. -->

- **SFN_S1:** {{SUB FRAGMENT NAME S1}}

  - **README Reference**: [{{SUB FRAGMENT NAME S1}}/README.md](./__shared/{{Fragment_Role}}s/{{SFN_S1}}/README.md)

- **SFN_S2:** {{SUB FRAGMENT NAME S2}}

  - **README Reference**: [{{SUB FRAGMENT NAME S2}}/README.md](./__shared/{{Fragment_Role}}s/{{SFN_S2}}/README.md)

- ...

## Structure

<!-- Questo diagramma deve rispecchiare la struttura delle directory come definita nella sezione "Fractal Break Down". Serve come una rapida verifica visuale della coerenza. -->

```text
{{Fragment_Name}}/
├── README.md
├── __{{Fragment_Name}}.{{Fragment_Role}}/
│    └── {{Fragment_Role}}s/
│        ├── {{SFN_P1}}/
│        │   └── README.md
│        ├── {{SFN_P2}}/
│        │   └── README.md
│        └── ...
└── __shared/
    └── {{Fragment_Role}}s/
        ├── {{SFN_S1}}/
        │   └── README.md
        ├── {{SFN_S2}}/
        │   └── README.md
        └── ...
```

---

## System Requirements

### Functional Requirements

<!-- Un requisito funzionale definisce una funzione specifica che il sistema deve svolgere, descrivendo cosa il software deve fare, quali sono le sue caratteristiche e i comportamenti attesi. Questi requisiti si concentrano su azioni, interazioni utente, elaborazione dati e calcoli, e spiegano il "cosa" e il "come" del comportamento del sistema. -->

#### User Stories

<!-- Scrivere le storie dal punto di vista del "consumatore" di questo Fragment. Se è un componente della UI, il consumatore è l'utente finale. Se è un servizio, il consumatore potrebbe essere un altro servizio o uno sviluppatore. -->

- **US_1:** {{USER STORY 1}}

  - **Description:** {{DESCRIPTION US_1}}
  <!-- Una breve spiegazione della storia o del suo contesto. -->

  - **Acceptance Criteria:**
    <!-- Questi criteri sono la base per i test. Ogni AC dovrebbe descrivere un singolo scenario in modo inequivocabile. -->

    - **AC_1:** _Dato_ {{CONTEXT AC_1}}, _Quando_ {{EVENT AC_1}}, _Allora_ {{EXPECTED OUTCOME AC_1}}.
    - **AC_2:** _Dato_ {{CONTEXT AC_2}}, _Quando_ {{EVENT AC_2}}, _Allora_ {{EXPECTED OUTCOME AC_2}}.
    - ...

- **US_2:** {{USER STORY 2}}

  - **Description:** {{DESCRIPTION US_2}}

  - **Acceptance Criteria:**

    - **AC_1:** _Dato_ {{CONTEXT AC_1}}, _Quando_ {{EVENT AC_1}}, _Allora_ {{EXPECTED OUTCOME AC_1}}.
    - **AC_2:** _Dato_ {{CONTEXT AC_2}}, _Quando_ {{EVENT AC_2}}, _Allora_ {{EXPECTED OUTCOME AC_2}}.
    - ...

- ...

### Non-Functional Requirements

<!-- Un requisito non funzionale definisce le qualità e le caratteristiche di un sistema, come performance, sicurezza e usabilità. In sostanza, specificano "come" il sistema deve funzionare, non "cosa" deve fare. Forniscono vincoli e criteri di valutazione per le operazioni del sistema, che possono influenzare l'architettura del software. -->

- **NFR_1:** {{NON-FUNCTIONAL REQUIREMENT 1}}

  - **Description:** {{DESCRIPTION NFR_1}}

  - **Details or Attachments:**
    - ...

- **NFR_2:** {{NON-FUNCTIONAL REQUIREMENT 2}}

  - **Description:** {{DESCRIPTION NFR_2}}

  - **Details or Attachments:**
    - ...

- ...

### Domain Requirements

<!-- Regole o vincoli che derivano specificamente dal dominio di business dell'applicazione. Questi requisiti possono includere normative, leggi, standard del settore e terminologia specifica. -->

- **DR_1:** {{DOMAIN REQUIREMENT 1}}

  - **Description:** {{DESCRIPTION DR_1}}

  - **Details:**
    - ...

- **DR_2:** {{DOMAIN REQUIREMENT 2}}

  - **Description:** {{DESCRIPTION DR_2}}

  - **Details:**
    - ...

- ...
