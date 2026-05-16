# Architettura e Design
## Indice
1. [Diagrammi UML](#-Diagrammi-UML)<br/>
    1.1 [Diagramma delle Classi](#Diagramma-delle-Classi)<br/>
    1.2 [Diagramma dei Casi d'Uso](#Diagramma-dei-Casi-d'Uso)<br/>
    1.3 [Diagramma della Macchina a Stati](#Diagramma-della-Macchina-a-Stati)<br/>
    1.4 [Diagramma delle Attività](#Diagramma-delle-Attività)<br/>
    1.5 [Diagramma dei Componenti](#Diagramma-dei-Componenti)<br/>
    1.6 [Diagramma di Sequenza](#Diagramma-di-Sequenza)<br/>
    1.7 [Diagramma delle Comunicazioni](#Diagramma-delle-Comunicazioni)<br/>
    1.8 [Diagramma dei Pacchetti](#Diagramma-dei-Pacchetti)<br/>
2. [Architettura Software](#Architettura-Software)<br/>
    2.1 [Descrizione Architettura](#Architettura)<br/>
    2.2 [Viste Architettoniche](#Viste-architettoniche)<br/>
3. [Design Software](#Software-Design)<br/>
    3.1 [Descrizione Design](#Descrizione-Design)<br/>
    3.2 [Misurazione Codice](#Misurazione-Codice)<br/>
    3.3 [Design Pattern](#Design-Pattern) <br/>

## Diagrammi UML
Di seguito verranno presentati i diagrammi UML relativi al progetto:
### Diagramma delle Classi
![Diagramma-delle-Classi](immagini/ClassDiagram.PNG)
### Diagramma dei Casi d'Uso
![Diagramma dei Casi d'Uso](immagini/UseCaseDiagram.PNG)
### Diagramma della Macchina a Stati
![Diagramma della Macchina a Stati](immagini/StateMachineDiagram.PNG)
### Diagramma delle Attività
![Diagramma delle Attività](immagini/activityDiagram.png)
### Diagramma dei Componenti
![Diagramma dei Componenti](immagini/ComponentDiagram.PNG)
### Diagramma di Sequenza
![Diagramma di Sequenza](immagini/sequenceDiagram.png)
### Diagramma delle Comunicazioni
![Diagramma delle Comunicazioni](immagini/CommunicationDiagram.PNG)
### Diagramma dei Pacchetti
![Diagramma dei Pacchetti](immagini/packageDiagram.png)

## Architettura Software 
### Architettura
Il nostro programma può essere identificato come un'architettura a pipeline, possiamo immaginarlo come una sequenza di passaggi logici e modulari in cui i dati (modelli, materiali, luci, ecc.) fluiscono attraverso diverse fasi di elaborazione per arrivare al rendering finale. In questo caso, l'architettura è strutturata per suddividere il processo complessivo in fasi sequenziali, ognuna con un ruolo ben definito.

Ecco le varie fasi:

1. **Input dei Dati**
La pipeline inizia con la raccolta e il caricamento dei dati. Questa fase è gestita dal modulo di caricamento:

**Loader**: carica i dati geometrici (vertici, indici, texture, normali) e li prepara per essere utilizzati nel rendering.
**OBJLoader**: si occupa specificamente di caricare file in formato OBJ, convertendo le informazioni in strutture dati utilizzabili dal sistema.
In questa fase, i dati sono trasferiti nei buffer della GPU (es. VAO e VBO), rendendoli pronti per l’elaborazione successiva.

2. **Preparazione degli Oggetti 3D**
Una volta caricati, i dati vengono associati a rappresentazioni logiche del sistema, come:

**Shape3D**: rappresenta un’entità geometrica generica.
Sottoclassi come Sphere, Cube, o altre forme specifiche estendono la logica di Shape3D per definire oggetti 3D concreti.
Ogni oggetto può essere arricchito con un materiale (gestito dalla classe Material) e con texture applicate tramite la classe Texture. Questi componenti definiscono l’aspetto visivo degli oggetti e vengono preparati per l’elaborazione successiva.

3. **Gestione della Scena**
La scena viene organizzata utilizzando una struttura centralizzata:

**World**: contiene e gestisce tutti gli oggetti (Shape3D), le luci e le altre entità.
**Camera**: definisce il punto di vista nella scena, specificando i parametri di proiezione e i movimenti.
In questa fase, il sistema crea una rappresentazione completa della scena 3D, pronta per essere processata dal motore di rendering.

4. **Elaborazione dei Dati per il Rendering**
Il passaggio successivo riguarda l’elaborazione e la configurazione degli shader:

**ShaderProgram**: gestisce gli shader utilizzati per il rendering. Gli shader definiscono come i dati verranno trasformati dalla GPU in un’immagine visiva.
**StaticShader**: implementa una configurazione predefinita di shader, utile per eseguire operazioni specifiche, come la gestione di ombreggiature o luci statiche.
Gli shader si occupano di operazioni critiche come:

- Applicare trasformazioni ai vertici (rotazioni, traslazioni, scaling).
- Calcolare i colori in base ai materiali, alle luci e alle texture.
- Proiettare la scena in uno spazio bidimensionale per il rendering finale.
  
5. **Fase di Rendering**
Il motore di rendering rappresenta il cuore della pipeline:

 **Renderer**: coordina la fase finale del processo, prendendo i dati elaborati da shader, geometrie, materiali e luci per generare l'immagine finale.
 Si occupa anche della configurazione delle proiezioni (es. prospettiva, ortogonale) tramite metodi come createProjectionMatrix().

6. **Calcoli di Supporto**
Durante l’intera pipeline, il modulo matematico, rappresentato da Maths, fornisce strumenti di supporto per:

- Creare matrici di trasformazione per traslazioni, rotazioni e scaling.
- Generare matrici di vista e proiezione per la camera.
Questa fase è strettamente integrata in più stadi della pipeline, rendendo possibili le trasformazioni geometriche necessarie per il rendering.

7. **Illuminazione e Post-Processing**
Il sistema gestisce la luce attraverso:

- **Light** e sue sottoclassi come AmbientLight: definiscono sorgenti luminose che influiscono sull’aspetto finale della scena.

Questi dati vengono elaborati dagli shader per calcolare come la luce interagisce con i materiali degli oggetti.
Il risultato finale della pipeline è una scena renderizzata, con oggetti illuminati e texture applicate.


### Viste architettoniche
Il sistema descritto può essere analizzato attraverso il modello **4+1** di Philippe Kruchten, che permette di osservare l'architettura da diverse prospettive.

---

#### 1. Vista Logica

Questa vista descrive la struttura statica del sistema, focalizzandosi sulle classi e le loro relazioni.

 **Componenti principali:**
- **Modulo geometrico:** `Shape3D`, `Sphere`, `Cube`, ecc.
- **Modulo materiali:** `Material`, `Texture`.
- **Modulo luci:** `Light`, `AmbientLight`.
- **Motore di rendering:** `Renderer`, `ShaderProgram`.
- **Modulo caricamento dati:** `Loader`, `OBJLoader`.
- **Modulo matematico:** `Maths`.
- **Gestione della scena:** `World`, `Camera`.

 **Relazioni:**
- `Shape3D` è la classe base per le forme geometriche.
- Oggetti geometrici sono associati a `Material` e `Texture`.

Questa vista aiuta a comprendere la **struttura del codice** e le interazioni tra le entità.

---

#### 2. Vista di Processo

Descrive il flusso di dati e le interazioni dinamiche tra i componenti durante l'esecuzione.

 **Esempio di flusso della pipeline:**
1. **Caricamento dati:** `Loader` legge modelli 3D e li trasferisce alla GPU.
2. **Inizializzazione della scena:** `Shape3D`, `Material` e `Texture` vengono associati.
3. **Elaborazione nella GPU:** Gli shader (`ShaderProgram`) elaborano geometrie e materiali.
4. **Rendering:** `Renderer` genera il frame finale della scena.

Questa vista aiuta a comprendere **il comportamento runtime del sistema**.

---

#### 3. Vista Fisica

Descrive la distribuzione del sistema su hardware e risorse.

 **Caratteristiche principali:**
- **CPU:** Gestisce caricamento e gestione della scena.
- **GPU:** Esegue operazioni di rendering e trasformazioni grafiche.
- **Buffer GPU:** `Loader` trasferisce i dati geometrici nei buffer (VAO, VBO).
- **Shader:** `ShaderProgram` esegue il rendering in tempo reale.

Questa vista è fondamentale per **l'ottimizzazione delle prestazioni**.

---

#### 4. Vista di Sviluppo

Mostra l'organizzazione del codice e la modularità del sistema.

 **Struttura del sistema per lo sviluppo:**
- **Moduli principali:**
  - **Geometria:** `Shape3D`, `Sphere`, `Cube`.
  - **Rendering:** `ShaderProgram`, `Renderer`.
  - **Gestione dati:** `Loader`, `OBJLoader`.
- **Organizzazione modulare:**
  - Separazione tra gestione della scena, rendering e caricamento dati.
  - Comunicazione tra moduli tramite interfacce definite.

Questa vista facilita **la collaborazione tra sviluppatori**.

---

#### 5. Vista dei Casi d'Uso

Descrive le interazioni degli utenti con il sistema.

 **Esempi di casi d’uso:**
- **Caricare un modello 3D:** Il file viene processato e visualizzato.
- **Applicare materiali e texture:** L'utente modifica l'aspetto degli oggetti.
- **Navigare nella scena:** `Camera` permette la visualizzazione dinamica.
- **Illuminare la scena:** `LightSource` gestisce le luci nella scena.

Questa vista collega **i requisiti funzionali con l'implementazione**.

---

## Software Design
### Descrizione Design
Al centro del sistema troviamo la classe **Shape3D**, che funge da base per tutti gli oggetti tridimensionali. Questa classe include attributi come posizione, rotazione e scala, e mette a disposizione metodi per modificarli e recuperarli. Da questa classe derivano diverse forme specifiche come Sphere, Torus, Cube e altre. Ogni sottoclasse aggiunge proprietà e comportamenti specifici, come i vertici e le normali per la sfera o il cubo.

![Shape](immagini/Shape.PNG)
---
Accanto alle forme troviamo la classe **Model**, che rappresenta i dati geometrici associati a un oggetto. La relazione tra Shape3D e Model è importante perché permette di associare i dati geometrici a una forma specifica, facilitando così la gestione della grafica.

![Model](immagini/Model.PNG)
---
Il sistema prevede anche un modulo per i materiali, gestito dalla classe **Material**, che definisce proprietà fisiche come trasparenza e riflettività. Ogni materiale può essere associato a una o più texture, gestite dalla classe Texture, che consente di caricare immagini e applicarle agli oggetti.

![Material](immagini/Material.PNG)
---
Un altro elemento chiave del sistema è la gestione delle luci. La classe base **Light** rappresenta una sorgente luminosa e contiene attributi come posizione e colore. Da essa derivano la AmbientLight, che rappresenta una luce diffusa regolabile in intensità, e altre luci specifiche, come LightSource.

![Light](immagini/Light.PNG)
--- 
La telecamera è gestita dalla classe **Camera**, che permette di definire una prospettiva di visione all'interno della scena 3D. Questa classe è essenziale per il rendering, poiché definisce i parametri di proiezione e i movimenti della visuale.

![Classe-Camera](immagini/Camera.PNG)
---
Il cuore del rendering è affidato alla classe **Renderer**, che utilizza una serie di strumenti per generare immagini finali della scena. Una componente importante è la classe ShaderProgram, responsabile della gestione degli shader, piccoli programmi eseguiti dalla GPU per calcolare l'aspetto visivo degli oggetti. Una sottoclasse, StaticShader, gestisce shader predefiniti con variabili fisse per specifiche operazioni di rendering.

![Renderer](immagini/Renderer.PNG)
---
Per supportare il caricamento e l’elaborazione di dati, il sistema include la classe **Loader**, che consente di caricare oggetti 3D nei buffer grafici. Un'estensione di questa classe, OBJLoader, è progettata per caricare modelli da file in formato OBJ, un comune standard per la grafica 3D.

![Loader](immagini/Loader.PNG)
---
Infine, il programma include alcune classi di supporto, come **Maths**, che offre metodi per creare matrici di trasformazione e vista, e un'enumerazione chiamata Colors, utile per standardizzare i colori utilizzati nel sistema.

![Maths](immagini/Maths.PNG)
---

### Misurazione del Codice
#### Grado di Astrattezza
Il grado di Astrattezza ti indica quanto un pacchetto del tuo progetto è concreto o astratto. Il calcolo viene fatto per ogni pacchetto e se il risultato è 0 il pacchetto è completamente concreto, mentre se è 1 è completamente astratto. Il calcolo per ogni pacchetto:
- **colors**: 0.5.
- **entities**: 0.1.
- **lights**: 0.33.
- **materials**: 0.
- **math**: 0.
- **RenderEngine**: 0.33.

#### Controllo Violazioni
Abbiamo eseguito un controllo con il tool pmd, è possibile visualizzare il report qui:
[Report](../reports/pmd-report.txt)

### Design Pattern 
Durante lo sviluppo del nostro progetto sono stati utilizzati dei design pattern. Analizzerò due casi in particolare utilizzando il Diagramma delle Classi:
- **singleton**: Nello sviluppo della classe Camera abbiamo utilizzato il design pattern singleton
  
![Classe-Camera](immagini/Camera.PNG)
---    
- **General Hyerarchy**: nello sviluppo della classe Shape3D abbiamo utilizzato il design pattern general hierarchy
  
![Shape](immagini/Shape.PNG)
---
