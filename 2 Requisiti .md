# REQUISITI 

## INDICE
1. [Introduzione](#introduzione)<br/>
   1.1. [Obiettivo del Progetto](#Obiettivo-del-Progetto)<br/>
   1.2. [Fase di Ricerca](#Fase-di-Ricerca)<br/>
2. [Elicitazione dei requisiti](#elicitazione-dei-requisiti)<br/>
   2.1 [Come è stata svolta](#Come-è-stata-svolta)<br/>
   2.2 [Approccio Utilizzato](#Approccio-Utilizzato)<br/>
3. [Specifica dei Requisiti](#Specifica-dei-requisiti)<br/>
   3.1 [Introduzione](#Introduzione)<br/> 
   3.2 [Definizioni, acronimi e abbreviazioni](#Definizioni,-acronimi-e-abbreviazioni)<br/>
   3.3 [Descrizione generale](#Descrizione-generale)<br/>
   3.4 [Requisiti specifici](#Requisiti-specifici)<br/>
   3.5 [Vincoli](#Vincoli-di-Progettazione)<br/>
   3.6 [Attributi](#Attributi-del-sistema-software)<br/>



## INTRODUZIONE
Questo programma è stato sviluppato come parte del progetto del corso di Ingegneria del Software per il terzo anno di Ingegneria Informatica presso l’Università di Bergamo.

### Obiettivo del Progetto
Data la natura del progetto, non ci sono stati clienti reali con cui interfacciarsi e, di conseguenza, non è stato possibile condurre interviste dirette per la raccolta dei requisiti. Tuttavia, abbiamo deciso di sviluppare un render 3D per metterci alla prova, testare le nostre competenze e creare qualcosa di diverso e stimolante rispetto ai classici progetti.

### Fase di Ricerca
Prima di iniziare lo sviluppo del codice, abbiamo dedicato diversi giorni alla comprensione dei concetti fondamentali del rendering 3D. Le nostre fonti principali di informazione sono state:

- Siti web specializzati,
- Repository GitHub relativi a progetti simili,
- Video YouTube per approfondire gli aspetti teorici e pratici.

Non abbiamo suddiviso in maniera netta il lavoro di ricerca, ritenendo più utile che tutti i membri del gruppo fossero pienamente consapevoli dei dettagli tecnici e teorici dietro alla realizzazione di un programma di rendering. Per questo motivo, abbiamo raccolto il maggior numero possibile di materiali, li abbiamo condivisi tra noi e li abbiamo analizzati insieme.

## ELICITAZIONE DEI REQUISITI

### Come è stata svolta
L’identificazione dei requisiti per il nostro progetto è stata suddivisa in due fasi principali:

1. **Fase di raccolta delle informazioni**: In questa fase iniziale, abbiamo raccolto tutte le informazioni che ritenevamo potessero essere utili per il nostro obiettivo. Abbiamo cercato materiale teorico, esempi pratici e risorse che potessero aiutarci a comprendere meglio le dinamiche del rendering 3D.

2. **Fase di analisi e selezione**: Una volta raccolto il materiale, abbiamo effettuato un’analisi superficiale per scartare le informazioni meno rilevanti, concentrandoci solo su documenti mirati che potessero realmente contribuire al nostro sviluppo. L’insieme di risorse selezionate comprendeva:
   - Siti web che spiegano la teoria del rendering 3D,
   - Video tutorial che supportano lo sviluppo di programmi di rendering,
   - Repository su GitHub che contengono esempi di codice utili.

### Approccio Utilizzato
La tecnica principale che abbiamo adottato può essere descritta come **derivazione da un sistema esistente**. Ci siamo basati su numerosi esempi già presenti online, imparando le tecniche utilizzate per costruire un software di rendering. Questo approccio ci ha permesso di ridurre il carico di lavoro, concentrandoci su soluzioni preesistenti e adattandole al nostro progetto.

Un altro approccio utilizzato è stato quello dell’**analisi delle attività**, suddividendo i requisiti principali in sotto-requisiti con specifiche dettagliate.

---

## SPECIFICA DEI REQUISITI

### Introduzione

- **Obiettivo**: Questo documento definisce i requisiti di un programma di rendering tridimensionale sviluppato come progetto per un corso del 3° anno di Ingegneria Informatica dell’Università di Bergamo. I requisiti definiti fungono da base per la procedura di accettazione di questo programma. Il documento è inoltre pensato come punto di partenza per la fase di progettazione.

- **Scopo**: Il programma permette di visualizzare figure tridimensionali nello spazio, con l’obiettivo di dimostrare le capacità apprese nello sviluppo software. I requisiti funzionali sono presentati nella sezione 3.2.

- **Riferimenti**:
     - **Introduzione ad OpenGL**: https://www.rastertek.com/tutgl40.html -
        https://www.youtube.com/watch?v=hPmEyAXdOdY&list=PLIbUZ3URbL0ESKHrvzXuHjrcLi7gxhBby&index=2
     - **Rendering 3D**: https://www.youtube.com/watch?v=U0_ONQQ5ZNM -
       https://www.youtube.com/watch?v=ih20l3pJoeU -
       https://www.youtube.com/watch?v=SPt-aogu72A
  
- **Panoramica**: La Sezione 2 di questo documento fornisce una panoramica generale del sistema. La Sezione 3 fornisce requisiti più specifici per le funzioni offerte. Queste funzioni mostrano ciò che l'utente può fare.

### Definizioni, acronimi e abbreviazioni

| **Termine**            | **Descrizione**                                                                                       |
|-------------------------|-------------------------------------------------------------------------------------------------------|
| **Vertex shader**      | Programma che lavora sui vertici di un modello 3D, calcolando la posizione e altre proprietà come colore e texture. |
| **Fragment shader**    | Programma che lavora sui pixel (frammenti) della scena, definendo colore, luci, ombre, texture ed effetti visivi. |
| **Texture**            | Immagine (2D o 3D) applicata su un oggetto 3D per aggiungere dettagli visivi.                         |
| **Entità**             | Qualsiasi componente autonomo di una scena 3D.                                                       |
| **VAOs**               | Contenitori che organizzano i dati dei vertici (posizioni, colori, texture, ecc.).                   |
| **VBOs**               | Memoria che contiene i dati effettivi dei vertici.                                                   |
| **OpenGL**             | API per comunicare con la scheda grafica e gestire immagini in modo efficiente.                      |
| **Imgui**              | Libreria per lo sviluppo di interfacce grafiche, spesso utilizzata con OpenGL.                       |
| **LWJGL**              | Libreria open-source per Java che consente l'accesso a API grafiche come OpenGL.                     |
| **ColorPicker**        | Strumento che consente di scegliere un colore tramite interfaccia visiva.                            |


### Descrizione generale

- **Prospettiva del prodotto**: Il programma consentirà di visualizzare forme geometriche 3D nello spazio, modificandone texture e colori. Sarà possibile osservare gli oggetti da ogni angolazione tramite una telecamera e caricare file esterni.

- **Funzioni del prodotto**: Visualizzazione di forme geometriche 3D, modifiche di texture e colori, osservazione degli oggetti tramite movimenti della telecamera e caricamento di file esterni.

- **Caratteristiche dell’utente**: Il programma non è destinato alla distribuzione, quindi non prevede differenze tra utente e sviluppatore.

- **Vincoli**: Non essendoci distinzione tra utente e amministratore, non sono presenti limitazioni sulle funzionalità disponibili.

- **Presupposti e Dipendenze**: junit, github.spair, joml, lwjgl, log4j, javagl.

### Requisiti specifici

#### Requisiti dell'interfaccia esterna

- **Interfacce utente**: Il formato dello schermo è Full HD. Una volta avviato il programma viene visualizzato lo spazio di lavoro e il menu principale. Lo spazio di lavoro inizialmente è vuoto. Nel menù principale sono presenti tutte le funzionalità che verranno spiegate di seguito. Ogni funzionalità ha una propria finestra e ogni finestra è indipendente possono essere spostate e ridimensionate a piaciere.
- **Interfacce hardware**: L'interfaccia utilizza fino a 12 tasti funzione.
- **Interfacce software**: abbiamo utilizzato la libreria LWJGL la quale si interfaccia direttamente con OpenGL.

#### Richieste funzionali

- **Cambio colore/texture alla forma (Could)**: Tramite un sottomenu nel menu principale "Model settings", è possibile selezionare e applicare colori o texture. Si crea una sottofinestra che presenta un colorpicker e delle opzioni per la scelta delle texture.
   - In OpenGL, le texture vengono applicate agli oggetti 3D combinando il lavoro del vertex shader e del fragment shader.
   - Il vertex shader calcola le posizioni dei vertici di un oggetto 3D nello spazio e assegna a ciascun vertice delle coordinate chiamate UV o coordinate di texture. Queste coordinate definiscono come la texture (un'immagine) deve essere "mappata" sulla superficie dell'oggetto. Per esempio, i vertici di un quadrato possono avere coordinate che indicano quale parte della texture deve coprire ogni angolo.
   - Il fragment shader, invece, si occupa di calcolare il colore di ogni pixel del modello basandosi sulle coordinate UV ricevute dal vertex shader. Quando il fragment shader elabora un pixel, accede alla texture tramite un sampler e preleva il colore corrispondente a quella posizione nella texture. In questo modo, ogni pixel del modello viene "dipinto" utilizzando i dati della texture.
   - In breve, il vertex shader stabilisce dove e come la texture viene mappata sull'oggetto, mentre il fragment shader usa queste informazioni per applicare effettivamente i dettagli della texture ai pixel visibili. Questo lavoro di squadra rende possibile aggiungere dettagli visivi realistici agli oggetti 3D, come colori, motivi e materiali. 

- **Importazione di file esterni (Must)**: Tramite il pulsante "import obj" nel menu principale, è possibile caricare file esterni.
   - Nei programmi di rendering con OpenGL, i file .obj vengono importati per caricare modelli 3D.Questi file contengono informazioni sui vertici, le facce e le normali del modello. Una volta letti i dati dal file, vengono organizzati e trasferiti alla GPU utilizzando i VBO (Vertex Buffer Object), che memorizzano i dati dei vertici come posizioni, colori o texture.
   - I VAO (Vertex Array Object) vengono poi utilizzati per gestire come questi dati devono essere interpretati. In pratica, il VAO tiene traccia della struttura dei dati nel VBO, specificando, ad esempio, quali attributi corrispondono alle posizioni, alle normali o alle texture.
   - Durante il rendering, OpenGL utilizza il VAO per sapere quali dati usare e come applicarli al modello 3D, rendendo così possibile visualizzare l'oggetto nella scena. Questo sistema permette di gestire in modo efficiente modelli anche molto complessi. 

- **Movimenti della telecamera (Must)**: La telecamera presenta 4 modalità di utilizzo 1 per la gestione della telecamera, e le altre hanno come soggeto ò'oggetto nella scena: 
  1. **Modalità Camera** (tasto C): Assumi il comando della telecamera e ti consente di muoverti nello spazio.
     - **W/S**: Avanti e indietro sull’asse Z.
     - **A/D**: Destra e sinistra.
     - **Q/E**: Rotazione laterale.
     - **Z/X:** Rotazione verticale.
     - **LShift/Space**: Salita e discesa.

  2. **Modalità Traslazione** (tasto T): Gestisci gli spostamenti dell'oggetto di scena
     - **W/S**: Avanti e indietro sull’asse Z.
     - **A/D**: Destra e sinistra.
     - **LShift/Space**: Salita e discesa.  

  3. **Modalità Rotazione** (tasto R): Ruota l’oggetto nella scena.
     - **W/S:** Rotazione attorno all'asse x.
     - **A/D**: Rotazione attorno all'asse z.
     - **Q/E**: Rotazione attorno all'asse y.

  4. **Modalità Scala** (tasto Y): Ingrandisce o riduce l’oggetto.
     - **W/S**: Ingrandisci e rimpicciolisci.

- **Modifica della luce dell'ambiente (Should)**: Tramite l'apposito menù "Show ambientlight settings", è possibile modifcare il colore e l'intensità della luce ambientale.

- **Modifica posizione fonte di luce (Should)**: Tramite il sottomenù è possibile cambiare colore e intensità della fonte di luce. E' inoltre possibile modificare la posizione della fonte:
     - **lungo l'asse x**: tasto W (+) e tasto S (-).
     - **lungo l'asse y**: tasto Spacebar (+) e tasto Lshift (-).
     - **lungo l'asse z**: tasto A (+) e tasto D (-).

- **Mesh Editing (Won't)**.
#### Requisiti di prestazione

- Sistema operativo: Windows 10 (64-bit), macOS 11 o Ubuntu 20.04.
- RAM: 8GB.
- Il programma supporta una sola interfaccia utente.
- Framework grafico: LWJGL 3 (per l'integrazione con OpenGL).
- Librerie: OpenGL, ImGui per l'interfaccia utente, Assimp per l'importazione di file .obj.
- Driver grafici: Driver aggiornati per la scheda grafica (NVIDIA/AMD).

#### Vincoli di Progettazione

- Il formato dei file caricati deve essere `.obj`.
- Il formato delle texture delle texture deve essere '.png', '.jpeg' e 'jpg'.

#### Attributi del sistema software

- **Affidabilità**: Il programma esegue correttamente tutte le richieste per il quale è stato sviluppato
- **Efficienza**: Il programma non richiede un grande dispendio di risorse dati per potere funzionare
- **Usabilità**: Il programma è molto semplice e intuito all'utilizzo.
- **Portabilità**: Il programma può essere comodamente scaricato tramite repository di github e funziona su tutti i dispositivi.
- **Riutilizzabilità**: Essendo di per se un programma nato ispirandosi ad un'altro è una base per sviluppo di applicazioni simili.
- **Modularità**: Ogni fase della pipeline è rappresentata da un modulo specifico, semplificando la gestione del sistema.
- **Scalabilità**: Nuove funzionalità, come effetti di illuminazione avanzati o tipi di materiali, possono essere aggiunte senza modificare le altre parti della                      pipeline.
- **Efficienza**: L’uso della GPU per operazioni di calcolo pesanti (tramite shader) garantisce alte prestazioni.
- **Separazione delle Responsabilità**: Ogni modulo si occupa di uno specifico stadio del processo, riducendo la complessità generale.

---
