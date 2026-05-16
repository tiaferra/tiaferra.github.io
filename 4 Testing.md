# Testing

## indice

1. [Scopo e modalità](#scopo-e-modalità)<br/>
2. [Risorse](#risorse)<br/>
3. [Programma delle attività di test](#programma-delle-attività-di-test)<br/>
   3.1 [Test manuali](#test-manuali)<br/>
   3.2 [Test automatici](#test-automatici)<br/>
4. [Metriche sui test (copertura)](<#metriche-sui-test-copertura>)<br/>
5. [Rischi](#rischi)<br/>

### Scopo e modalità

Per il nostro programma sono previsti dei test sia ai singoli componenti che all’intero programma, in modo tale da accertarsi del corretto funzionamento dei componenti e della cooperazione tra di loro.<br/>
È previsto un approccio misto di test automatici e manuali, questi ultimi necessari per via della natura grafica del programma; essi richiedono, infatti, la presenza di una persona che ispeziona visivamente il risultato.<br/>

### Risorse

Le risorse coinvolte sono:
tutte le parti del programma;
asset grafici per i test;
personale di test (Yousef e Annalisa);
IDE Eclipse;
libreria JUNIT;

### Programma delle attività di test

Il programma delle attività di test consiste di un test generale, dove l’utente dovrà controllare manualmente le varie funzionalità che il programma offre e sarà svolto nel seguente modo:

#### Test manuali

##### Main

eseguire il metodo testMain() della classe Test che si trova in MAY/test/test;
premere il tasto “show” e accertarsi sia che il modello si stato caricato correttamente e sia visibile;
modificare la luce diffusa controllando che le modifiche siano riflesse sul modello;
modificare la luce ambiente controllando che le modifiche siano riflesse sul modello;
aprire il pannello delle impostazioni del modello premendo il tasto “”;
modificare i valori di shineDamper e reflectivity verificando che le modifiche siano riflesse sul modello;
aprire il pannello di selezione delle texture premendo sul pulsante “”;
cambiare la texture con una delle texture già incluse verificando che il modello passi alla texture scelta;
cambiare texture con una nuova caricata da utente verificando che il modello passi alla texture scelta;
aprire il pannello di modifica modello premendo “” ;
scegliere uno per volta i modelli precaricati e verificare che nella scena sia visualizzato il modello scelto;
scegliere l'opzione di caricare un nuovo modello poi scegliere il modello da caricare;
verificare che nella scena sia visualizzato il modello scelto;
chiudere il programma.

##### Caricamento file

Un secondo test manuale, volto a controllare che la scelta di file sia eseguita correttamente e il cui svolgimento avviene secondo le seguenti modalità:

eseguire il metodo testFileLoading() della classe Test che si trova in MAY/test/test;
scegliere di caricare il modello “stall.obj”;
a questo punto viene fatto un controllo con JUNIT assertTrue che il file letto sia quello scelto dall’utente ;
a questo punto si apre una seconda finestra di caricamento in cui bisogna scegliere “white.png”;
si controlla di nuovo con JUNIT che il file letto sia quello scelto dall’utente.

#### Test automatici

I test automatici sono realizzati con JUNIT (senza l’intervento dell’utente) e includono:

##### Test rimozione estensioni

test per il metodo della rimozione delle estensioni dei file removeExtension() in MAY/src-gen/main/Main che consiste nel verificare con una serie di combinazioni diverse di estensioni file che il metodo ritorni solamente il nome del file senza estensione

<code>

    @Test
    public static void removeExtensionTest() {
    	assertTrue(Main.removeExtension("name.file").equals("name"));
    	assertTrue(Main.removeExtension("").equals(""));
    	assertTrue(Main.removeExtension("name.file1.file2.file3").equals("name"));
    	assertTrue(Main.removeExtension("name.obj.png").equals("name"));
    	assertTrue(Main.removeExtension("name").equals("name"));

    }

</code>

Risultato: in tutti i casi il metodo ritorna il nome del file senza l’estensione.

##### Test del caricamento dei modelli da file

per il test automatico del caricamento dei modelli da file. Sono previsti due test:

con i file corretti:
<code>

        @Test
    	public static void loadModelTest() {
    		Loader loader = new Loader();
    		assertDoesNotThrow(() -> OBJLoader.loadObjModelNew("./resources/models/Cottage_FREE.obj", loader));
    	assertDoesNotThrow(() -> OBJLoader.loadObjModelNew("./resources/models/Bench_LowRes.obj", loader));
        }

</code>
Risultato: dato che sono entrambi file validi non viene lanciata nessuna eccezione e quindi il test JUNIT assertDoesNotThrow è passato.

con file non esistente “ench_LowRes.obj” simulando un errore di battitura dove manca la b iniziale per accertarsi che in casi come questo venga lanciata l'eccezione “NullPointerException”

<code>

    @Test
    	public static void loadingWrongFileTest() {
    		Loader loader = new Loader();

    	NullPointerException e = assertThrows(NullPointerException.class, () -> {
    		OBJLoader.loadObjModelNew("./resources/models/ench_LowRes.obj", loader).getTexture();
    	}, "Expected to throw NullPointerException, but it didn't");
    	assertFalse(e.getMessage().isEmpty());
    }

</code>
Risultato: come previsto viene lanciata l’eccezione verificata usando i metodi JUNIT  assertThrows e assertFalse, usato per controllare che il suo messaggio non sia vuoto.

#### Test automatici per i controlli e il movimento

Questi test hanno lo scopo di verificare che i metodi per il movimento e la rotazione degli oggetti nella scena si comportino correttamente.

##### Movimento modello

Per il movimento la modalità prevista è:
istanziare un oggetto nell’origine degli assi (0,0,0);
verificare, con degli assertTrue di JUNIT, che la posizione iniziale sia l’origine;
chiamare i metodi per il movimento e portare l’oggetto in (1,2,3);
verificare di nuovo la posizione con assertTrue per controllare che sia (1,2,3) come previsto;
<code>

    @Test
    public static void moveTest() {
    	Map<String, Shape3d> shapes = new HashMap<>();
    	Main main = new Main();
    	main.loadSphere(shapes);
    	assertTrue(shapes.containsKey("Sphere"));
    	assertTrue(shapes.get("Sphere").getModel().getVertexCount() == Sphere.INDICES.length);
    	Shape3d sphere = shapes.get("Sphere");
    	Vector3f pos = sphere.getPosition();
    	assertTrue(pos.x == 0 && pos.y == 0 & pos.z == 0);
    	sphere.increasePosition(1, 2, 3);
    	pos = sphere.getPosition();
    	assertTrue(pos.x == 1 && pos.y == 2 & pos.z == 3);
    }

</code>

Risultato: il test è passato e la posizione degli oggetti dopo lo spostamento è quella prevista.

##### Rotazione modello

Per la rotazione la modalità prevista è:
istanziare un oggetto nell’origine degli assi (0,0,0);
verificare, con degli assertTrue di JUNIT, che la rotazione iniziale sia nulla;
chiamare i metodi per la rotazione e ruotare l’oggetto di 1 rad attorno all’asse X, 2 rad attorno all’asse Y e 3 rad attorno all’asse Z;
verificare di nuovo la rotazione con assertTrue per controllare che sia (1,2,3) come previsto
<code>

    @Test
    public static void rotationTest() {
    	Map<String, Shape3d> shapes = new HashMap<>();
    	Main main = new Main();
    	main.loadSphere(shapes);
    	assertTrue(shapes.containsKey("Sphere"));
    assertTrue(shapes.get("Sphere").getModel().getVertexCount() == Sphere.INDICES.length);
    	Shape3d sphere = shapes.get("Sphere");
    	float rotationX = sphere.getRotX();
    	float rotationY = sphere.getRotY();
    	float rotationZ = sphere.getRotZ();
    	assertTrue(rotationX == 0 && rotationY == 0 & rotationZ == 0);
    	sphere.increaseRotation(1, 2, 3);
    	rotationX = sphere.getRotX();
    	rotationY = sphere.getRotY();
    	rotationZ = sphere.getRotZ();
    	assertTrue(rotationX == 1 && rotationY == 2 & rotationZ == 3);
    }

</code>
Risultato: il test è passato e la rotazione degli oggetti dopo lo spostamento è quella prevista.

##### Movimento camera

per il movimento della camera nella scena per accertarsi che non si comporti in modo anomalo:
La modalità è:
chiamare il metodo getCamera che ritorna l’istanza del singleton camera;
impostare la posizione all’origine degli assi (0,0,0);
verificare, con degli assertTrue di JUNIT, che la posizione sia l’origine;
chiamare i metodi per il movimento e portare la camera in (1,2,3);
verificare di nuovo la posizione con assertTrue per controllare che sia (1,2,3) come previsto;
<code>

    @Test
    public static void cameraTest() {
    	Camera camera = Camera.getCamera();
    	camera.setPosition(new Vector3f(0, 0, 0));
    	assertEquals(camera.getPosition().x, 0);
    	assertEquals(camera.getPosition().y, 0);
    	assertEquals(camera.getPosition().z, 0);
    	camera.move(1, 2, 3);
    	assertEquals(camera.getPosition().x, 1);
    	assertEquals(camera.getPosition().y, 2);
    	assertEquals(camera.getPosition().z, 3);
    }

</code>
Risultato: il test è passato e la posizione della camera dopo lo spostamento è quella prevista.

### Metriche sui test (copertura)

abbiamo basato la nostra metrica di sulla copertura ottenendo questi risultati
#### risultato test copertura
![copertura](immagini/copertura.png)

### Rischi

Non sono previsti rischi correlati a nessuna delle attività di test.
