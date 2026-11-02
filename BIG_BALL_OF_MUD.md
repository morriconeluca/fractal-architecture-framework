# Il Problema: Big Ball of Mud di Brian Foote e Joseph Yoder

Il paper _Big Ball of Mud_ (Grande Palla di Fango) di Brian Foote e Joseph Yoder è un'opera fondamentale nel campo dell'ingegneria del software. Presentato nel 1997 alla conferenza PLoP '97 (Pattern Languages of Programs) da due ricercatori del Department of Computer Science della University of Illinois at Urbana-Champaign, invece di concentrarsi su architetture ideali e pattern di alto livello, esamina con lucidità e pragmatismo l'architettura software _de facto_ più diffusa: sistemi la cui struttura è cresciuta in modo disordinato, casuale e spesso caotico.

> _La Big Ball of Mud è una giungla di codice spaghetti, strutturata a caso, tentacolare, sciatta, tenuta insieme con nastro adesivo e fil di ferro. […] Il suo codice mostra segni inconfondibili di crescita non regolamentata e di riparazioni ripetute e opportune. […] La struttura complessiva del sistema potrebbe non essere mai stata ben definita. Se lo era, potrebbe essersi erosa fino a diventare irriconoscibile._

## La Tesi Eversiva: Big Ball of Mud è un Pattern a Sé Stante

Invece di condannare semplicemente questa realtà, gli autori la analizzano come un pattern a sé stante, esplorando le forze che ne favoriscono la nascita e le ragioni della sua sorprendente persistenza ed efficacia. L'obiettivo è comprendere il divario tra ciò che si predica (le architetture pulite) e ciò che si pratica, per poter migliorare i sistemi esistenti.

> _Big Ball of Mud potrebbe essere considerato un anti-pattern, perché la nostra intenzione è mostrare come la passività di fronte a forze che minano l'architettura possa portare a una pozza di fango. Tuttavia, la sua innegabile popolarità porta alla conclusione inesorabile che si tratta di un pattern a pieno titolo. È certamente una soluzione pervasiva e ricorrente al problema di produrre un sistema funzionante nel contesto dello sviluppo software._

## Anatomia di un'Architettura in Decomposizione

Quali sono le sue caratteristiche? Un sistema che sta degenerando in una Big Ball of Mud manifesta una serie di patologie tecniche interconnesse. Queste non sono questioni di stile, ma difetti strutturali fondamentali che minano la salute dell'intera codebase:

- **Codice Rigido (Fortemente Accoppiato)**

  > Il sintomo di questa patologia si manifesta quando i componenti del software sono così strettamente intrecciati tra loro che anche un cambiamento piccolo e logicamente semplice richiede una cascata di modifiche in molteplici punti del sistema. Ciò accade quando una parte del codice dipende dai dettagli di implementazione privati di un'altra parte del codice.

- **Codice Fragile (Bassa Coesione)**

  > Questa seconda patologia si manifesta quando una modifica in un punto del sistema causa la rottura inaspettata di una funzionalità in un'altra area non correlata. Le unità di codice hanno perso la loro specializzazione e sono diventate contenitori di logica eterogenea. Per comprendere una singola funzionalità di business (es. gestire un pagamento), lo sviluppatore è costretto a rintracciare pezzi di codice sparsi in decine di file e directory non correlate.

## L'Entropia: Quali Sono le Forze che Generano una Big Ball of Mud

Una Big Ball of Mud non è il risultato di un singolo errore, ma l'esito finale di un processo di entropia graduale, alimentato da migliaia di piccole decisioni pragmatiche ma miopi. Diverse forze, spesso di natura pratica ed economica, spingono anche i team più competenti a produrre questi sistemi:

- **Poco Tempo**

  > Le scadenze imminenti non permettono una progettazione architetturale a lungo termine. Le decisioni si basano sull'urgenza.

- **Costo e Time-to-Market**

  > L'architettura è un lusso perché non produce ritorni immediati, a differenza del rilascio rapido di nuove funzionalità.

- **Competenza ed Esperienza**

  > Il livello di abilità dei programmatori varia. Inoltre, la mancanza di esperienza in un dominio specifico rende difficile progettare una buona architettura fin dall'inizio. A volte, l'architettura emerge solo dopo aver giocato con il problema.

- **Complessità del Dominio**

  > Citando Fred Brooks, il software è spesso complesso perché il problema che risolve è intrinsecamente complesso (_essential complexity_). L'architettura riflette questa complessità.

- **Cambiamento dei Requisiti**

  > L'architettura è un'ipotesi sul futuro. Requisiti imprevisti possono tagliare trasversalmente le decisioni architetturali fondamentali, costringendo a compromessi che erodono la struttura.

- **Turnover del Personale**

  > La perdita di personale causa una perdita di memoria istituzionale, che rende difficile preservare la visione architetturale originale.

## L'Eresia di un Concetto: Cosa C'è di Buono

Il paper non condanna la Big Ball of Mud, ma la riconosce come una conseguenza naturale e talvolta inevitabile delle pressioni economiche e pratiche dello sviluppo software. Un'architettura informale può essere addirittura vantaggiosa nelle prime fasi di un progetto, quando l'esplorazione e l'apprendimento sono più importanti della rigida aderenza a un piano. Sebbene disprezzata dagli architetti, questa non-architettura è estremamente popolare, anzi la più diffusa, perciò deve necessariamente fare qualcosa di giusto.

## Cosa Fa di Giusto?

Come pattern, la Big Ball of Mud asseconda la crescita incrementale (_Piecemeal Growth_), lo stesso approccio iterativo-incrementale che sarà poi promosso dalla filosofia _Agile_. La sua architettura cresce spontaneamente. I grandi piani architetturali _Waterfall_ erano rigidi e spesso fallivano. I requisiti di un sistema software complesso evolvono. Le esigenze degli utenti evolvono. Far evolvere il sistema in modo incrementale, aggiungendo funzionalità un pezzo alla volta, gli permette di adattarsi e crescere progressivamente. Ma questa crescita incontrollata porta a un'erosione della struttura architettonica, trasformando il sistema in una pozza di fango.

## Conclusione

Dopo aver letto il paper di Brian Foote e Joseph Yoder, ci si domanda:

> Può esistere un'architettura del codice sorgente in grado di adattarsi spontaneamente alle esigenze dello sviluppo del software moderno senza collassare in una Big Ball of Mud?
