# Gestione del progetto 
1. [Organizzazione del team](#organizzazione-del-team)<br/>
2. [Ciclo di vita del software](#ciclo-di-vita-del-software)<br/>
3. [Gestione della configurazione](#gestione-della-configurazione)<br/>


## Organizzazione del team

Come da project plan, il processo di sviluppo adottato dal nostro team è stato di tipo agile SCRUM con product owner (Shoeib Yousef) e uno scrum master (Sergi Annalisa e Ferrari Mattia che si sono alternati ad ogni sprint). Data la piccola dimensione del team, ciascun membro ha lavorato in modo collaborativo e autogestito, senza alcuna netta distinzione dei ruoli. Ognuno ha contribuito in modo versatile a tutte le fasi del progetto, dalla pianificazione e progettazione, allo sviluppo, test e manutenzione. Questo approccio ha permesso di sfruttare al meglio le competenze di ogni persona del team e ha consentito il rilascio della prima versione funzionale (MVP) dell’applicazione di rendering 3d <a href="https://github.com/yousef-shoeib/MAY.git">MAY</a>. Nei successivi sprint verranno aggiunte altre funzionalità quali mesh editing, luci multiple, skybox, rendering di più oggetti (di cui è stato fornito un “proof of concept”), spot lights, grid di base (seguendo lo stile di blender), trasparenza, nebbia e altro ed eventuali ottimizzazioni. 

## Ciclo di vita del software 

Per la gestione delle varie attività da svolgere, dalla selezione dal backlog fino al loro completamento, abbiamo usato la kanban board messa a disposizione da Jira. Tuttavia, a differenza di quanto stabilito nel project plan, i giorni degli sprint e le varie scadenze non sono stati decisi usando la stessa applicazione, bensì tramite un calendario Google dove venivano indicati gli incontri (Daily scrum) in cui si discuteva lo stato di avanzamento delle attività assegnate, eventuali problematiche e la pianificazione di azioni correttive. Durante questi incontri, i membri del team hanno collaborato per risolvere i problemi e riassegnare i compiti in base alle esigenze del progetto.

Il MVP (versione 0.0.0–SNAPSHOT dell’applicazione) è stato realizzato in 10 sprint seguendo la suddivisione in fasi stabilita nel project plan: 
<li>progettazione iniziale: sono stati dedicati 7 sprint, 4 per consentire al team di conoscere il dominio applicativo (è stato organizzato un solo  daily scrum) e 3 per fare una bozza dei diagrammi uml; </li>
<li>implementazione: partendo da quanto definito nella fase precedente abbiamo stabilito quali fossero le attività da svolgere (in ordine di importanza) e le abbiamo inserite nel backlog. Ad ogni sprint venivano quindi selezionate quelle con maggiore priorità e alla fine di ogni sprint il team si riuniva per risolvere eventuali problemi.La fase di programmazione della versione 0.0.0-SNAPSHOT ha richiesto complessivamente 3 sprint; in concomitanza, venivano aggiornati i diagrammi uml aggiungendo o togliendo dettagli irrilevanti;</li>
<li> testing: tale attività è stata eseguita alla fine di ogni gruppo di funzionalità correlate nei tre sprint dedicati alla programmazione a cui è seguito un test finale di tutto il programma al rilascio come indicato nel documento di test;</li>
<li> revisione e ottimizzazione: dal momento che manca l’implementazione di alcune funzionalità non è stata eseguita una vera attività di ottimizzazione oltre al semplice refactoring fatto a fine sprint <a href="https://github.com/yousef-shoeib/MAY/blob/docs/Documents/5%20Maintenance.md" >MAINTENANCE</a> . La revisione si è incentrata sulla documentazione dove è stata realizzata la versione finale basandosi sulle note prese durante i daily scrum e gli sprint da ogni membro del team.</li>

#### Sprint e daily scrum organizzati
![novembre](immagini/Novembre2024.png)
![dicembre](immagini/Dicembre2024.png)
![gennaio](immagini/Gennaio2025.png)
#### Backlog dei vari sprint
![sprint 6](immagini/Sprint6.png)
![sprint 8](immagini/Sprint8.png)


## Gestione della configurazione  

Nella gestione dei cambiamenti il team si è attenuto a quanto specificato nel project plan (eccezione fatta per l’utilizzo del Jira Service Management). Le richieste di modifica sono state dapprima identificate e valutate in base all'impatto che avrebbero avuto sull’intero progetto. Si è quindi deciso se approvarle o meno e, in caso di approvazione, sono state implementate in un nuovo branch. La revisione post-implementazione ha permesso di osservare i risultati del cambiamento rispetto agli obiettivi iniziali, verificando se il cambiamento avesse prodotto i benefici attesi e se fosse allineato con la strategia generale. In caso di esito positivo, il nuovo branch è stato unito al main.
Il sistema per il configuration management utilizzato è stato github con tutti i comandi associati (git push, git pull, git commit ecc.). In caso di errori si apriva un issue specificando nella sezione di testo quale fosse il problema e lo si assegnava a un membro del gruppo. La persona in questione poteva decidere, dopo essersi confrontata con gli altri, se creare un nuovo branch per implementare azioni correttive o modificare direttamente sul main, a seconda della gravità del problema da risolvere.
#### Esempio di bug nel rendering del cubo. In questo caso il bug è stato risolto senza bisogno di un nuovo branch
![BUG](immagini/Bug.png)
#### Branch GUI con pull request e approvazione. è stata quindi rilasciata v1.0.0
![GUI](immagini/GUI.png)
![release](immagini/v1.0.0.png)
#### Issues
![Issues](immagini/issues.png)
#### Pull request
![pull request](immagini/PullRequest1.png)
#### Commits
![commit](immagini/Commits.png)

È stato adottato anche un approccio MDA per la generazione delle classi principali con Papyrus quali ad esempio Loader, Shape 3D e classi che la estendono, Light e le classi che la estendono, colors (sarà utilizzata in versioni successive) ed altre.

Diversamente da quanto indicato nel project plan non è stato possibile effettuare delle misurazioni di complessità con Stan4j a causa di alcuni problemi nel download del tool. L’utilizzo di SonarLint ci ha permesso di individuare alcuni errori commessi durante la fase di programmazione, ad esempio variabili non dichiarate secondo gli standard di Oracle, e di correggerli tempestivamente.


