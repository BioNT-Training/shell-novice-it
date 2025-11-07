---
title: Lavorare con i file e le directory
teaching: 30
exercises: 20
---


::::::::::::::::::::::::::::::::::::::: objectives

- Eliminare, copiare e spostare file e/o cartelle.
- Creare i file in questa gerarchia usando un editor o copiando e rinominando i file esistenti.
- Creare una gerarchia di cartelle che corrisponda a un diagramma dato.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come posso creare, copiare ed eliminare file e cartelle?
- Come posso modificare i file?

::::::::::::::::::::::::::::::::::::::::::::::::::


## Creazione di directory

Ora sappiamo come esplorare i file e le cartelle, ma come crearli?

In questo episodio impareremo a creare e spostare file e directory, utilizzando come esempio la cartella `exercise-data/writing`.

### Fase uno: vedere dove siamo e cosa abbiamo già

Dovremmo ancora trovarci nella cartella `shell-lesson-data` sul Desktop, che possiamo controllare usando:

```bash
$ pwd
```

```output
/Users/nelle/Desktop/shell-lesson-data
```

Ora ci sposteremo nella cartella `exercise-data/writing` e vedremo cosa contiene:

```bash
$ cd exercise-data/writing/
$ ls -F
```

```output
haiku.txt  LittleWomen.txt
```

### Creare una cartella

Creiamo una nuova cartella chiamata `thesis` usando il comando `mkdir thesis` (che non ha output):

```bash
$ mkdir thesis
```

Come si può intuire dal nome, `mkdir` significa "directory make". Poiché `thesis` è un percorso relativo (cioè non ha una barra iniziale, come `/what/ever/thesis`), la nuova cartella viene creata nella cartella di lavoro corrente:

```bash
$ ls -F
```

```output
haiku.txt  LittleWomen.txt  thesis/
```

Dato che abbiamo appena creato la cartella `thesis`, non c'è ancora nulla al suo interno:

```bash
$ ls -F thesis
```

Si noti che `mkdir` non si limita a creare singole cartelle una alla volta. L'opzione `-p` permette a `mkdir` di creare una cartella con sottocartelle annidate in una singola operazione:

```bash
$ mkdir -p ../project/data ../project/results
```

L'opzione `-R` del comando `ls` elenca tutte le sottocartelle annidate all'interno di una cartella. Usiamo `ls -FR` per elencare ricorsivamente la nuova gerarchia di cartelle appena creata nella cartella `project`:

```bash
$ ls -FR ../project
```

```output
../project/:
data/  results/

../project/data:

../project/results:
```

::::::::::::::::::::::::::::::::::::::::: callout

## Due modi di fare la stessa cosa

l'uso della shell per creare una cartella non è diverso dall'uso di un file explorer. Se si apre la cartella corrente utilizzando il file explorer grafico del sistema operativo, la cartella `thesis` apparirà anche lì. Mentre la shell e il file explorer sono due modi diversi di interagire con i file, i file e le cartelle sono gli stessi.

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Buoni nomi per i file e le directory

I nomi complicati di file e cartelle possono rendere la vita difficile quando si lavora alla riga di comando. Qui forniamo alcuni suggerimenti utili per i nomi dei file e delle cartelle.

1. Non usare spazi.

Gli spazi possono rendere un nome più significativo, ma poiché gli spazi sono usati per separare gli argomenti sulla riga di comando, è meglio evitarli nei nomi di file e directory. Al loro posto si può usare `-` o `_` (ad esempio `north-pacific-gyre/` piuttosto che `north pacific gyre/`). Per verificarlo, provare a digitare `mkdir north pacific gyre` e vedere quale directory (o directory!) viene creata quando si controlla con `ls -F`.

2. Non iniziare il nome con `-` (trattino).

I comandi trattano i nomi che iniziano con `-` come opzioni.

3. attenersi a lettere, numeri, `.` (punto o 'stop completo'), `-` (trattino) e `_` (trattino basso).

Molti altri caratteri hanno un significato speciale sulla riga di comando. Ne conosceremo alcuni nel corso di questa lezione. Ci sono caratteri speciali che possono far sì che il vostro comando non funzioni come previsto e possono persino causare la perdita di dati.

Se è necessario fare riferimento a nomi di file o cartelle che contengono spazi o altri caratteri speciali, è necessario circondare il nome con [virgolette] singole (https://www.gnu.org/software/bash/manual/html_node/Quoting.html) (`''`).

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: instructor

Gli studenti possono talvolta rimanere intrappolati in editor di testo a riga di comando come Vim, Emacs o Nano. Chiudere l'emulatore di terminale e aprirne uno nuovo può essere frustrante, perché gli studenti devono navigare di nuovo nella cartella corretta. La nostra raccomandazione per attenuare questo problema è che gli istruttori usino lo stesso editor di testo degli studenti durante i workshop (nella maggior parte dei casi Nano).

::::::::::::::::::::::::::::::::::::::::::::::::::

### Creare un file di testo

Cambiamo la nostra cartella di lavoro in `thesis` usando `cd`, quindi eseguiamo un editor di testo chiamato Nano per creare un file chiamato `draft.txt`:

```bash
$ cd thesis
$ nano draft.txt
```

::::::::::::::::::::::::::::::::::::::::: callout

## Quale editor?

Quando diciamo che "`nano` è un editor di testo" intendiamo proprio "testo". Può lavorare solo con i dati a caratteri semplici, non con tabelle, immagini o altri supporti di facile utilizzo. Lo usiamo negli esempi perché è uno degli editor di testo meno complessi. Tuttavia, a causa di questa caratteristica, potrebbe non essere abbastanza potente o flessibile per il lavoro che dovrete svolgere dopo questo workshop. Sui sistemi Unix (come Linux e macOS), molti programmatori usano [Emacs](https://www.gnu.org/software/emacs/) o [Vim](https://www.vim.org/) (entrambi richiedono più tempo per essere appresi), oppure un editor grafico come [Gedit](https://projects.gnome.org/gedit/) o [VScode](https://code.visualstudio.com/). Su Windows, si può usare [Notepad++](https://notepad-plus-plus.org/). Windows ha anche un editor incorporato chiamato `notepad` che può essere eseguito dalla riga di comando allo stesso modo di `nano` per gli scopi di questa lezione.

Indipendentemente dall'editor utilizzato, è necessario sapere dove cerca e salva i file. Se lo si avvia dalla shell, (probabilmente) userà la cartella di lavoro corrente come posizione predefinita. Se si utilizza il menu di avvio del computer, potrebbe voler salvare i file nella cartella Desktop o Documenti. È possibile cambiare questa scelta navigando in un'altra cartella la prima volta che si fa "Salva con nome..."

::::::::::::::::::::::::::::::::::::::::::::::::::

digitiamo alcune righe di testo.

![](fig/nano-screenshot.png){alt="schermata dell'editor di testo nano in azione con il testo Non è più pubblicare o morire, è condividere e prosperare"}

Una volta che siamo soddisfatti del nostro testo, possiamo premere <kbd>Ctrl</kbd>\+<kbd>O</kbd> (premere il tasto <kbd>Ctrl</kbd> o <kbd>Control</kbd> e, tenendolo premuto, premere il tasto <kbd>O</kbd>) per scrivere i nostri dati su disco. Verrà richiesto un nome per il file che conterrà il testo. Premete <kbd>Retro</kbd> per accettare il nome predefinito suggerito di `draft.txt`.

una volta salvato il nostro file, possiamo usare <kbd>Ctrl</kbd>\+<kbd>X</kbd> per uscire dall'editor e tornare alla shell.

::::::::::::::::::::::::::::::::::::::::: callout

## Tasto Control, Ctrl o ^

Il tasto Control è anche chiamato "Ctrl". L'uso del tasto Control può essere descritto in vari modi. Ad esempio, si può vedere l'istruzione di premere il tasto <kbd>Control</kbd> e, tenendolo premuto, premere il tasto <kbd>X</kbd>, descritto come uno dei seguenti:

- `Control-X`
- `Control+X`
- `Ctrl-X`
- `Ctrl+X`
- `^X`
- `C-x`

In nano, nella parte inferiore dello schermo si vedrà `^G Get Help ^O WriteOut`. Ciò significa che si può usare `Control-G` per ottenere aiuto e `Control-O` per salvare il file.

::::::::::::::::::::::::::::::::::::::::::::::::::

`nano` non lascia alcun output sullo schermo dopo la sua uscita, ma `ls` ora mostra che è stato creato un file chiamato `draft.txt`:

```bash
$ ls
```

```output
draft.txt
```

::::::::::::::::::::::::::::::::::::::: challenge

## Creare file in modo diverso

Abbiamo visto come creare file di testo usando l'editor `nano`. Ora provate il seguente comando:

```bash
$ touch my_file.txt
```

1. Cosa ha fatto il comando `touch`? Quando si guarda alla cartella corrente usando l'esploratore di file della GUI, il file appare?

2. Utilizzare `ls -l` per ispezionare i file. Quanto è grande `my_file.txt`?

3. Quando si potrebbe voler creare un file in questo modo?

::::::::::::::: solution

## Soluzione

1. Il comando `touch` genera un nuovo file chiamato `my_file.txt` nella cartella corrente. È possibile osservare questo nuovo file generato digitando `ls` al prompt della riga di comando. il file `my_file.txt` può anche essere visualizzato nel file explorer della GUI.

2. Quando si ispeziona il file con `ls -l`, si noti che la dimensione di `my_file.txt` è di 0 byte. In altre parole, non contiene dati. Se si apre `my_file.txt` con il proprio editor di testo, è vuoto.

3. Alcuni programmi non generano direttamente i file di output, ma richiedono che siano già stati generati dei file vuoti. Quando il programma viene eseguito, cerca un file esistente da riempire con il suo output. Il comando touch consente di generare in modo efficiente un file di testo vuoto da utilizzare per tali programmi.

:::::::::::::::::::::::::

Per evitare confusione in seguito, si consiglia di rimuovere il file appena creato prima di procedere con il resto dell'episodio, altrimenti i risultati futuri potrebbero variare rispetto a quelli forniti nella lezione. A tale scopo, utilizzare il seguente comando:

```bash
$ rm my_file.txt
```

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Cosa c'è in un nome?

Avrete notato che tutti i file di Nelle si chiamano "qualcosa punto qualcosa", e in questa parte della lezione abbiamo sempre usato l'estensione `.txt`. Questa è solo una convenzione; possiamo chiamare un file `mythesis` o qualsiasi altra cosa vogliamo. Tuttavia, la maggior parte delle persone usa nomi divisi in due parti per aiutare loro (e i loro programmi) a distinguere i diversi tipi di file. La seconda parte del nome è chiamata **estensione del nome del file** e indica il tipo di dati contenuti nel file: `.txt` segnala un file di testo semplice, `.pdf` indica un documento PDF, `.cfg` è un file di configurazione pieno di parametri per qualche programma o altro, `.png` è un'immagine PNG e così via.

Questa è solo una convenzione, anche se importante. I file contengono semplicemente dei byte; sta a noi e ai nostri programmi interpretarli secondo le regole dei file di testo, dei documenti PDF, dei file di configurazione, delle immagini e così via.

Nominare un'immagine PNG di una balena come `whale.mp3` non la trasforma magicamente in una registrazione di un canto di balena, anche se *potrebbe* far sì che il sistema operativo associ il file a un programma di riproduzione musicale. In questo caso, se qualcuno fa doppio clic su `whale.mp3` in un programma di esplorazione file, il lettore musicale tenterà automaticamente (ed erroneamente) di aprire il file `whale.mp3`.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Spostamento di file e directory

Ritorno alla cartella `shell-lesson-data/exercise-data/writing`,

```bash
$ cd ~/Desktop/shell-lesson-data/exercise-data/writing
```

Nella nostra cartella `thesis` abbiamo un file `draft.txt` che non è un nome particolarmente informativo, quindi cambiamo il nome del file usando `mv`, che è l'abbreviazione di 'move':

```bash
$ mv thesis/draft.txt thesis/quotes.txt
```

Il primo argomento dice a `mv` che cosa stiamo 'spostando', mentre il secondo è dove deve andare. In questo caso, stiamo spostando `thesis/draft.txt` in `thesis/quotes.txt`, il che ha lo stesso effetto di rinominare il file. Sicuramente, `ls` ci mostra che `thesis` ora contiene un file chiamato `quotes.txt`:

```bash
$ ls thesis
```

```output
quotes.txt
```

È necessario prestare attenzione quando si specifica il nome del file di destinazione, poiché `mv` sovrascriverà silenziosamente qualsiasi file esistente con lo stesso nome, con conseguente perdita di dati. Per impostazione predefinita, `mv` non chiede conferma prima di sovrascrivere i file. Tuttavia, un'opzione aggiuntiva, `mv -i` (o `mv --interactive`), farà sì che `mv` richieda tale conferma.

Si noti che `mv` funziona anche sulle cartelle.

Spostiamo `quotes.txt` nella cartella di lavoro corrente. Usiamo ancora una volta `mv`, ma questa volta useremo solo il nome di una cartella come secondo argomento per dire a `mv` che vogliamo mantenere il nome del file ma metterlo in un posto nuovo. (In questo caso, il nome della cartella che utilizziamo è il nome speciale della cartella `.` di cui abbiamo parlato in precedenza.

```bash
$ mv thesis/quotes.txt .
```

L'effetto è quello di spostare il file dalla cartella in cui si trovava alla cartella di lavoro corrente. `ls` ora mostra che `thesis` è vuoto:

```bash
$ ls thesis
```

```output
$
```

In alternativa, possiamo confermare che il file `quotes.txt` non è più presente nella cartella `thesis` provando esplicitamente a elencarlo:

```bash
$ ls thesis/quotes.txt
```

```error
ls: cannot access 'thesis/quotes.txt': No such file or directory
```

`ls` con un nome di file o una cartella come argomento elenca solo il file o la cartella richiesti. Se il file dato come argomento non esiste, la shell restituisce un errore come abbiamo visto sopra. Possiamo usare questa funzione per vedere che `quotes.txt` è ora presente nella nostra cartella corrente:

```bash
$ ls quotes.txt
```

```output
quotes.txt
```

::::::::::::::::::::::::::::::::::::::: challenge

## Spostamento dei file in una nuova cartella

Dopo aver eseguito i seguenti comandi, Jamie si rende conto di aver inserito i file `sucrose.dat` e `maltose.dat` nella cartella sbagliata. I file avrebbero dovuto essere inseriti nella cartella `raw`.

```bash
$ ls -F
 analyzed/ raw/
$ ls -F analyzed
fructose.dat glucose.dat maltose.dat sucrose.dat
$ cd analyzed
```

riempire gli spazi vuoti per spostare questi file nella cartella `raw/` (cioè quella in cui si è dimenticato di metterli)

```bash
$ mv sucrose.dat maltose.dat ____/____
```

::::::::::::::: solution

## Soluzione

```bash
$ mv sucrose.dat maltose.dat ../raw
```

Ricordate che `..` si riferisce alla cartella padre (cioè quella sopra la cartella corrente) e che `.` si riferisce alla cartella corrente.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Copia di file e directory

Il comando `cp` funziona in modo molto simile a `mv`, solo che copia un file invece di spostarlo. Possiamo verificare che abbia fatto la cosa giusta usando `ls` con due percorsi come argomenti --- come la maggior parte dei comandi Unix, a `ls` possono essere dati più percorsi contemporaneamente:

```bash
$ cp quotes.txt thesis/quotations.txt
$ ls quotes.txt thesis/quotations.txt
```

```output
quotes.txt   thesis/quotations.txt
```

Possiamo anche copiare una cartella e tutto il suo contenuto usando l'opzione [recursive](https://en.wikipedia.org/wiki/Recursion) `-r`, ad esempio per fare il backup di una cartella:

```bash
$ cp -r thesis thesis_backup
```

Possiamo verificare il risultato elencando il contenuto di entrambe le cartelle `thesis` e `thesis_backup`:

```bash
$ ls thesis thesis_backup
```

```output
thesis:
quotations.txt

thesis_backup:
quotations.txt
```

È importante includere il flag `-r`. Se si vuole copiare una cartella e si omette questa opzione, verrà visualizzato un messaggio che indica che la cartella è stata omessa perché `-r not specified`.

``` bash
$ cp thesis thesis_backup
cp: -r not specified; omitting directory 'thesis'
```


::::::::::::::::::::::::::::::::::::::: challenge

## Rinominare i file

Supponiamo di aver creato un file di testo semplice nella nostra cartella corrente per contenere un elenco dei test statistici che dovremo fare per analizzare i nostri dati, e di averlo chiamato `statstics.txt`

Dopo aver creato e salvato questo file ci si accorge di aver sbagliato il nome del file! Per correggere l'errore, quale dei seguenti comandi si può utilizzare?

1. `cp statstics.txt statistics.txt`
2. `mv statstics.txt statistics.txt`
3. `mv statstics.txt .`
4. `cp statstics.txt .`

::::::::::::::: solution

## Soluzione

1. No. Sebbene questa operazione crei un file con il nome corretto, il file con il nome sbagliato esiste ancora nella cartella e deve essere cancellato.
2. Sì, questo funzionerebbe per rinominare il file.
3. No, il punto(.) indica dove spostare il file, ma non fornisce un nuovo nome di file; non è possibile creare nomi di file identici.
4. No, il punto(.) indica dove copiare il file, ma non fornisce un nuovo nome di file; non è possibile creare nomi di file identici.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Spostare e copiare

Qual è l'output del comando di chiusura `ls` nella sequenza mostrata sotto?

```bash
$ pwd
```

```output
/Users/jamie/data
```

```bash
$ ls
```

```output
proteins.dat
```

```bash
$ mkdir recombined
$ mv proteins.dat recombined/
$ cp recombined/proteins.dat ../proteins-saved.dat
$ ls
```

1. `proteins-saved.dat recombined`
2. `recombined`
3. `proteins.dat recombined`
4. `proteins-saved.dat`

::::::::::::::: solution

## Soluzione

Partiamo dalla cartella `/Users/jamie/data` e creiamo una nuova cartella chiamata `recombined`. La seconda riga sposta (`mv`) il file `proteins.dat` nella nuova cartella (`recombined`). La terza riga crea una copia del file appena spostato. La parte difficile è dove il file è stato copiato. Ricordiamo che `..` significa "salire di livello", quindi il file copiato si trova ora in `/Users/jamie`. Si noti che `..` è interpretato rispetto alla cartella di lavoro corrente, **non** rispetto alla posizione del file copiato. Quindi, l'unica cosa che verrà mostrata usando ls (in `/Users/jamie/data`) è la cartella ricombinata.

1. No, vedi spiegazione sopra. `proteins-saved.dat` si trova in `/Users/jamie`
2. Si
3. No, vedi spiegazione sopra. `proteins.dat` si trova in `/Users/jamie/data/recombined`
4. No, vedi spiegazione sopra. `proteins-saved.dat` si trova in `/Users/jamie`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Rimozione di file e cartella

Tornando alla cartella `shell-lesson-data/exercise-data/writing`, riordiniamola rimuovendo il file `quotes.txt` che abbiamo creato. Il comando Unix che useremo a questo scopo è `rm` (abbreviazione di 'remove'):

```bash
$ rm quotes.txt
```

Possiamo confermare che il file è andato via usando `ls`:

```bash
$ ls quotes.txt
```

```error
ls: cannot access 'quotes.txt': No such file or directory
```

::::::::::::::::::::::::::::::::::::::::: callout

## L'eliminazione è per sempre

La shell di Unix non ha un cestino da cui recuperare i file cancellati (anche se la maggior parte delle interfacce grafiche di Unix ce l'ha). Invece, quando si cancellano i file, questi vengono scollegati dal file system in modo che il loro spazio di archiviazione sul disco possa essere riciclato. Esistono strumenti per trovare e recuperare i file cancellati, ma non è detto che funzionino in una particolare situazione, poiché il computer potrebbe riciclare subito lo spazio su disco del file.

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Usare `rm` in modo sicuro

Cosa succede quando si esegue `rm -i thesis_backup/quotations.txt`? Perché si vuole questa protezione quando si usa `rm`?

::::::::::::::: solution

## Soluzione

```output
rm: remove regular file 'thesis_backup/quotations.txt'? y
```

L'opzione `-i` chiederà prima di (ogni) rimozione (usare <kbd>Y</kbd> per confermare la cancellazione o <kbd>N</kbd> per mantenere il file). La shell Unix non ha un cestino, quindi tutti i file rimossi spariranno per sempre. Utilizzando l'opzione `-i`, si ha la possibilità di verificare che si stiano eliminando solo i file che si desidera rimuovere.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

Se si tenta di rimuovere la cartella `thesis` usando `rm thesis`, si ottiene un messaggio di errore:

```bash
$ rm thesis
```

```error
rm: cannot remove 'thesis': Is a directory
```

Questo accade perché `rm` per impostazione predefinita funziona solo sui file, non sulle cartelle.

`rm` può rimuovere una cartella *e tutto il suo contenuto* se si usa l'opzione ricorsiva `-r`, e lo farà *senza alcuna richiesta di conferma*:

```bash
$ rm -r thesis
```

Dato che non c'è modo di recuperare i file cancellati usando la shell, `rm -r` *dovrebbe essere usato con grande cautela* (si potrebbe considerare di aggiungere l'opzione interattiva `rm -r -i`).

## Operazioni con più file e cartelle

Spesso è necessario copiare o spostare più file contemporaneamente. Questo può essere fatto fornendo un elenco di singoli nomi di file o specificando un modello di denominazione utilizzando i caratteri jolly. I caratteri jolly sono caratteri speciali che possono essere utilizzati per rappresentare caratteri sconosciuti o insiemi di caratteri durante la navigazione nel file system Unix.

::::::::::::::::::::::::::::::::::::::: challenge

## Copia con più nomi di file

Per questo esercizio, è possibile provare i comandi nella cartella `shell-lesson-data/exercise-data`.

Nell'esempio seguente, cosa fa `cp` quando gli vengono dati diversi nomi di file e un nome di cartella?

```bash
$ mkdir backup
$ cp creatures/minotaur.dat creatures/unicorn.dat backup/
```

Nell'esempio seguente, cosa fa `cp` quando gli vengono dati tre o più nomi di file?

```bash
$ cd creatures
$ ls -F
```

```output
basilisk.dat  minotaur.dat  unicorn.dat
```

```bash
$ cp minotaur.dat unicorn.dat basilisk.dat
```

::::::::::::::: solution

## Soluzione

Se viene dato più di un nome di file seguito da un nome di cartella (cioè la cartella di destinazione deve essere l'ultimo argomento), `cp` copia i file nella cartella nominata.

Se vengono dati tre nomi di file, `cp` lancia un errore come quello che segue, perché si aspetta il nome di una cartella come ultimo argomento.

```error
cp: target 'basilisk.dat' is not a directory
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

### Uso dei caratteri jolly per accedere a più file contemporaneamente

::::::::::::::::::::::::::::::::::::::::: callout

## Caratteri jolly

`*` è un **wildcard**, che rappresenta zero o più altri caratteri. Consideriamo la cartella `shell-lesson-data/exercise-data/alkanes`: `*.pdb` rappresenta `ethane.pdb`, `propane.pdb` e ogni file che termina con '.pdb'. D'altra parte, `p*.pdb` rappresenta solo `pentane.pdb` e `propane.pdb`, perché la 'p' all'inizio può rappresentare solo nomi di file che iniziano con la lettera 'p'.

Anche `?` è un carattere jolly, ma rappresenta esattamente un carattere. Quindi `?ethane.pdb` potrebbe rappresentare `methane.pdb` mentre `*ethane.pdb` rappresenta sia `ethane.pdb` che `methane.pdb`.

I caratteri jolly possono essere usati in combinazione tra loro. Ad esempio, `???ane.pdb` indica tre caratteri seguiti da `ane.pdb`, che danno `cubane.pdb ethane.pdb octane.pdb`.

Quando la shell vede un carattere jolly, lo espande per creare un elenco di nomi di file corrispondenti *prima* di eseguire il comando precedente. Come eccezione, se un'espressione con il carattere jolly non corrisponde a nessun file, Bash passerà l'espressione come argomento al comando così com'è. Per esempio, digitando `ls *.pdf` nella cartella `alkanes` (che contiene solo file con nomi che terminano con `.pdb`) si ottiene un messaggio di errore che indica che non esiste un file chiamato `*.pdf`. Tuttavia, generalmente comandi come `wc` e `ls` vedono gli elenchi di nomi di file che corrispondono a queste espressioni, ma non i caratteri jolly stessi. È la shell, non gli altri programmi, a espandere i caratteri jolly.

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Elenca i nomi dei file che corrispondono a uno schema

Quando vengono eseguiti nella cartella `alkanes`, quali comandi `ls` produrranno questo output?

`ethane.pdb methane.pdb`

1. `ls *t*ane.pdb`
2. `ls *t?ne.*`
3. `ls *t??ne.pdb`
4. `ls ethane.*`

::::::::::::::: solution

## Soluzione

La soluzione è `3.`

`1.` mostra tutti i file il cui nome contiene zero o più caratteri (`*`) seguiti dalla lettera `t`, poi zero o più caratteri (`*`) seguiti da `ane.pdb`. Si ottiene così `ethane.pdb methane.pdb octane.pdb pentane.pdb`.

`2.` mostra tutti i file il cui nome inizia con zero o più caratteri (`*`) seguiti dalla lettera `t`, poi un singolo carattere (`?`), poi `ne.` seguito da zero o più caratteri (`*`). In questo modo si ottiene `octane.pdb` e `pentane.pdb`, ma non corrisponde a nulla che finisca in `thane.pdb`.

`3.` risolve i problemi dell'opzione 2 facendo corrispondere due caratteri (`??`) tra `t` e `ne`. Questa è la soluzione.

`4.` mostra solo i file che iniziano con `ethane.`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Altro sui caratteri jolly

Sam ha una cartella contenente i dati di calibrazione, i set di dati e le descrizioni dei set di dati:

```bash
.
├── 2015-10-23-calibration.txt
├── 2015-10-23-dataset1.txt
├── 2015-10-23-dataset2.txt
├── 2015-10-23-dataset_overview.txt
├── 2015-10-26-calibration.txt
├── 2015-10-26-dataset1.txt
├── 2015-10-26-dataset2.txt
├── 2015-10-26-dataset_overview.txt
├── 2015-11-23-calibration.txt
├── 2015-11-23-dataset1.txt
├── 2015-11-23-dataset2.txt
├── 2015-11-23-dataset_overview.txt
├── backup
│   ├── calibration
│   └── datasets
└── send_to_bob
    ├── all_datasets_created_on_a_23rd
    └── all_november_files
```

Prima di partire per un'altra gita, Sam vuole fare il backup dei suoi dati e inviare alcuni set di dati al suo collega Bob. Per farlo, Sam usa i seguenti comandi:

```bash
$ cp *dataset* backup/datasets
$ cp ____calibration____ backup/calibration
$ cp 2015-____-____ send_to_bob/all_november_files/
$ cp ____ send_to_bob/all_datasets_created_on_a_23rd/
```

Aiutate Sam a riempire gli spazi vuoti.

La struttura risultante dovrebbe essere la seguente

```bash
.
├── 2015-10-23-calibration.txt
├── 2015-10-23-dataset1.txt
├── 2015-10-23-dataset2.txt
├── 2015-10-23-dataset_overview.txt
├── 2015-10-26-calibration.txt
├── 2015-10-26-dataset1.txt
├── 2015-10-26-dataset2.txt
├── 2015-10-26-dataset_overview.txt
├── 2015-11-23-calibration.txt
├── 2015-11-23-dataset1.txt
├── 2015-11-23-dataset2.txt
├── 2015-11-23-dataset_overview.txt
├── backup
│   ├── calibration
│   │   ├── 2015-10-23-calibration.txt
│   │   ├── 2015-10-26-calibration.txt
│   │   └── 2015-11-23-calibration.txt
│   └── datasets
│       ├── 2015-10-23-dataset1.txt
│       ├── 2015-10-23-dataset2.txt
│       ├── 2015-10-23-dataset_overview.txt
│       ├── 2015-10-26-dataset1.txt
│       ├── 2015-10-26-dataset2.txt
│       ├── 2015-10-26-dataset_overview.txt
│       ├── 2015-11-23-dataset1.txt
│       ├── 2015-11-23-dataset2.txt
│       └── 2015-11-23-dataset_overview.txt
└── send_to_bob
    ├── all_datasets_created_on_a_23rd
    │   ├── 2015-10-23-dataset1.txt
    │   ├── 2015-10-23-dataset2.txt
    │   ├── 2015-10-23-dataset_overview.txt
    │   ├── 2015-11-23-dataset1.txt
    │   ├── 2015-11-23-dataset2.txt
    │   └── 2015-11-23-dataset_overview.txt
    └── all_november_files
        ├── 2015-11-23-calibration.txt
        ├── 2015-11-23-dataset1.txt
        ├── 2015-11-23-dataset2.txt
        └── 2015-11-23-dataset_overview.txt
```

::::::::::::::: solution

## Soluzione

```bash
$ cp *calibration.txt backup/calibration
$ cp 2015-11-* send_to_bob/all_november_files/
$ cp *-23-dataset* send_to_bob/all_datasets_created_on_a_23rd/
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Organizzazione di cartelle e file

Jamie sta lavorando a un progetto e vede che i suoi file non sono ben organizzati:

```bash
$ ls -F
```

```output
analyzed/  fructose.dat    raw/   sucrose.dat
```

I file `fructose.dat` e `sucrose.dat` contengono l'output dell'analisi dei dati. Quale/i comando/i trattato/i in questa lezione deve eseguire affinché i comandi sottostanti producano l'output mostrato?

```bash
$ ls -F
```

```output
analyzed/   raw/
```

```bash
$ ls analyzed
```

```output
fructose.dat    sucrose.dat
```

::::::::::::::: solution

## Soluzione

```bash
mv *.dat analyzed
```

Jamie deve spostare i suoi file `fructose.dat` e `sucrose.dat` nella cartella `analyzed`. La shell espanderà \*.dat in modo che corrisponda a tutti i file .dat presenti nella cartella corrente. Il comando `mv` sposta quindi l'elenco dei file .dat nella cartella 'analyzed'.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Riprodurre la struttura della cartella

si sta iniziando un nuovo esperimento e si vuole duplicare la struttura delle directory dell'esperimento precedente per poter aggiungere nuovi dati.

Si supponga che l'esperimento precedente si trovi in una cartella chiamata `2016-05-18`, che contiene una cartella `data` che a sua volta contiene cartelle chiamate `raw` e `processed` che contengono file di dati. L'obiettivo è copiare la struttura delle cartelle della cartella `2016-05-18` in una cartella chiamata `2016-05-20`, in modo che la struttura finale delle cartelle sia la seguente:

```output
2016-05-20/
└── data
   ├── processed
   └── raw
```

Quale dei seguenti comandi raggiungerebbe questo obiettivo? Cosa farebbero gli altri comandi?

```bash
$ mkdir 2016-05-20
$ mkdir 2016-05-20/data
$ mkdir 2016-05-20/data/processed
$ mkdir 2016-05-20/data/raw
```

```bash
$ mkdir 2016-05-20
$ cd 2016-05-20
$ mkdir data
$ cd data
$ mkdir raw processed
```

```bash
$ mkdir 2016-05-20/data/raw
$ mkdir 2016-05-20/data/processed
```

```bash
$ mkdir -p 2016-05-20/data/raw
$ mkdir -p 2016-05-20/data/processed
```

```bash
$ mkdir 2016-05-20
$ cd 2016-05-20
$ mkdir data
$ mkdir raw processed
```

::::::::::::::: solution

## Soluzione

Le prime due serie di comandi raggiungono questo obiettivo. La prima serie utilizza percorsi relativi per creare la cartella di primo livello prima delle sottocartelle.

La terza serie di comandi darà un errore perché il comportamento predefinito di `mkdir` non crea una sottocartella di una cartella inesistente: le cartelle di livello intermedio devono essere create per prime.

La quarta serie di comandi raggiunge questo obiettivo. Ricordate che l'opzione `-p`, seguita da un percorso di una o più cartelle, farà sì che `mkdir` crei tutte le sottocartelle intermedie necessarie.

La serie finale di comandi genera le cartelle 'raw' e 'processed' allo stesso livello della cartella 'data'.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- `cp [old] [new]` copia un file.
- `mkdir [path]` crea una nuova cartella.
- `mv [old] [new]` sposta (rinomina) un file o una cartella.
- `rm [path]` rimuove (elimina) un file.
- `*` corrisponde a zero o più caratteri in un nome di file, quindi `*.txt` corrisponde a tutti i file che terminano in `.txt`.
- `?` corrisponde a qualsiasi singolo carattere in un nome di file, quindi `?.txt` corrisponde a `a.txt` ma non a `any.txt`.
- L'uso del tasto Control può essere descritto in molti modi, tra cui `Ctrl-X`, `Control-X` e `^X`.
- La shell non ha un cestino: una volta che qualcosa è stato cancellato, è davvero sparito.
- La maggior parte dei nomi dei file è `something.extension`. L'estensione non è necessaria e non garantisce nulla, ma viene normalmente utilizzata per indicare il tipo di dati contenuti nel file.
- A seconda del tipo di lavoro svolto, potrebbe essere necessario un editor di testo più potente di Nano.

::::::::::::::::::::::::::::::::::::::::::::::::::


