# Maintenance
Il seguente documento descrive le attività di manutenzione eseguite sull'applicazione di rendering 3D sviluppata dal nostro team. 

La manutenzione perfettiva prevede l’aggiunta di altre funzionalità  <a href="https://github.com/yousef-shoeib/MAY/blob/docs/Documents/1%20Gestione%20del%20progetto.md">Gestione progetto</a> o requisiti nuovi affinché l’applicazione rispecchi al meglio le esigenze degli utenti,  mantenendo il software rilevante in un mercato in continua evoluzione . 

Alla fine di ogni sprint sono state eseguite delle attività di refactoring al fine di migliorare la leggibilità del codice. La manutenzione preventiva riguarda appunto quell’insieme di procedure, eseguite regolarmente, volte a facilitare le operazioni di manutenzione correttiva e perfettiva. Alcune di queste includono: 

<li>la ridenominazione dei package secondo gli standard standard di Oracle per garantire conformità alle best practice e alle linee guida ufficiali per lo sviluppo in Java; </li>
<li>spostamento della logica di alcune classi in altre per applicare design pattern (e.g. la classe Camera è un singleton) o per assicurare coerenza e coesione con quanto già presente nel programma. È stata aggiunta ad esempio la classe Material (intermedia tra Model e Texture) che ha causato qualche problema vista l’eccessiva interconnessione tra le due classi precedentemente presenti;</li>
<li>eliminazione delle librerie importate ma non più utilizzate a seguito della riorganizzazione della logica di alcune classi;</li>
<li>riorganizzazione dei packages in folder secondo quanto stabilito nei <strong> requisiti_progetto24 25 v1_0_2.pdf</strong> </li>
<br/>
Dopo ogni attività di refactoring sono stati eseguiti dei test unitari e di integrazione <a href="https://github.com/yousef-shoeib/MAY/blob/docs/Documents/4%20Testing.md">Testing</a> per verificare che le modifiche non avessero introdotto bug o regressioni (manutenzione correttiva). 

Non è stata prevista alcuna manutenzione adattativa
