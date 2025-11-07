---
title: Cicli
teaching: 40
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Scrivere un ciclo che applichi uno o più comandi separatamente a ciascun file di un insieme di file.
- Tracciare dei valori assunti da una variabile del ciclo durante la sua esecuzione.
- Spiegare la differenza tra il nome di una variabile e il suo valore.
- Spiegare perché gli spazi e alcuni caratteri di punteggiatura non dovrebbero essere usati nei nomi dei file.
- Dimostrare come vedere quali comandi sono stati eseguiti di recente.
- Eseguire nuovamente i comandi eseguiti di recente senza riscriverli.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come posso eseguire le stesse azioni su molti file diversi?

::::::::::::::::::::::::::::::::::::::::::::::::::

**I loop** sono un costrutto di programmazione che ci permette di ripetere un comando o un insieme di comandi per ogni elemento di un elenco. In quanto tali, sono fondamentali per migliorare la produttività attraverso l'automazione. Analogamente ai caratteri jolly e al completamento delle schede, l'uso dei cicli riduce anche la quantità di battitura necessaria (e quindi il numero di errori di battitura).

Supponiamo di avere diverse centinaia di file di dati del genoma denominati `basilisk.dat`, `minotaur.dat` e `unicorn.dat`. Per questo esempio, utilizzeremo la directory `exercise-data/creatures` che contiene solo tre file di esempio, ma i principi possono essere applicati a molti più file contemporaneamente.

La struttura di questi file è la stessa: il nome comune, la classificazione e la data di aggiornamento sono presentati sulle prime tre righe, con le sequenze di DNA sulle righe successive. Esaminiamo i file:

```bash
$ head -n 5 basilisk.dat minotaur.dat unicorn.dat
```

Vorremmo stampare la classificazione di ogni specie, che è riportata nella seconda riga di ogni file. Per ogni file, dobbiamo eseguire il comando `head -n 2` e inviarlo a `tail -n 1`. Per risolvere questo problema utilizzeremo un ciclo, ma prima vediamo la forma generale di un ciclo, utilizzando lo pseudo-codice seguente:

```bash
# "for" indica l'inizio di un "For-loop" 
for thing in list_of_things 
# "do" indica l'inizio dell'esecuzione
do 
    # L'intentazione  non è richiesta ma rende il codice più leggibile
    operation_using/command $thing 
# "done" indica la fine del for loop
done  
```

e possiamo applicarla al nostro esempio in questo modo:

```bash
$ for filename in basilisk.dat minotaur.dat unicorn.dat
> do
>     echo $filename
>     head -n 2 $filename | tail -n 1
> done
```

```output
basilisk.dat
CLASSIFICATION: basiliscus vulgaris
minotaur.dat
CLASSIFICATION: bos hominus
unicorn.dat
CLASSIFICATION: equus monoceros
```

::::::::::::::::::::::::::::::::::::::::: callout

## Seguire il prompt

Il prompt della shell cambia da `$` a `>` e viceversa mentre digitiamo il nostro ciclo. Il secondo prompt, `>`, è diverso per ricordarci che non abbiamo ancora finito di digitare un comando completo. Il punto e virgola, `;`, può essere usato per separare due comandi scritti su una singola riga.


::::::::::::::::::::::::::::::::::::::::::::::::::

Quando la shell vede la parola chiave `for`, sa che deve ripetere un comando (o un gruppo di comandi) una volta per ogni elemento di un elenco. Ogni volta che il ciclo viene eseguito (chiamato iterazione), un elemento dell'elenco viene assegnato in sequenza alla **variabile** e i comandi all'interno del ciclo vengono eseguiti, prima di passare all'elemento successivo dell'elenco. All'interno del ciclo, si richiede il valore della variabile anteponendo `$`. La `$` indica all'interprete della shell di trattare la variabile come un nome di variabile e di sostituire il suo valore al suo posto, anziché trattarla come un testo o un comando esterno.

In questo esempio, l'elenco è costituito da tre nomi di file: `basilisk.dat`, `minotaur.dat` e `unicorn.dat`. Ogni volta che il ciclo itera, si usa prima `echo` per stampare il valore che la variabile `$filename` contiene attualmente. Questo non è necessario ai fini del risultato, ma è utile per seguire più facilmente la procedura. Successivamente, verrà eseguito il comando `head` sul file a cui fa riferimento `$filename`. La prima volta che viene eseguito il ciclo, `$filename` è `basilisk.dat`. L'interprete esegue il comando `head` su `basilisk.dat` e trasmette le prime due righe al comando `tail`, che stampa la seconda riga di `basilisk.dat`. Per la seconda iterazione, `$filename` diventa `minotaur.dat`. Questa volta, la shell esegue `head` su `minotaur.dat` e invia le prime due righe al comando `tail`, che stampa la seconda riga di `minotaur.dat`. Per la terza iterazione, `$filename` diventa `unicorn.dat`, quindi la shell esegue il comando `head` su quel file e `tail` sul suo output. Poiché l'elenco era composto da soli tre elementi, la shell esce dal ciclo `for`.

::::::::::::::::::::::::::::::::::::::::: callout

## Stessi simboli, significati diversi

Qui vediamo `>` usato come prompt della shell, mentre `>` è usato anche per reindirizzare l'output. Allo stesso modo, `$` è usato come prompt della shell, ma, come abbiamo visto prima, è anche usato per chiedere alla shell di ottenere il valore di una variabile.

Se la *shell* stampa `>` o `$`, allora si aspetta che venga digitato qualcosa, e il simbolo è un prompt.

Se si digita `>` o `$`, si tratta di un'istruzione che indica alla shell di reindirizzare l'output o di ottenere il valore di una variabile.


::::::::::::::::::::::::::::::::::::::::::::::::::

Quando si usano le variabili è anche possibile mettere i nomi tra parentesi graffe per delimitare chiaramente il nome della variabile: `$filename` è equivalente a `${filename}`, ma è diverso da `${file}name`. È possibile trovare questa notazione nei programmi di altre persone.

Abbiamo chiamato la variabile in questo ciclo `filename` per rendere il suo scopo più chiaro ai lettori umani. Alla shell stessa non interessa come viene chiamata la variabile; se scrivessimo questo ciclo come:

```bash
$ for x in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $x | tail -n 1
> done
```

o:

```bash
$ for temperature in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $temperature | tail -n 1
> done
```

funzionerebbe esattamente allo stesso modo. *I programmi sono utili solo se le persone possono capirli, quindi nomi senza senso (come `x`) o fuorvianti (come `temperature`) aumentano le probabilità che il programma non faccia ciò che i lettori pensano che faccia.

Negli esempi precedenti, alle variabili (`thing`, `filename`, `x` e `temperature`) si sarebbe potuto dare qualsiasi altro nome, purché significativo sia per chi scrive il codice sia per chi lo legge.

Si noti anche che i cicli possono essere usati per cose diverse dai nomi di file, come un elenco di numeri o un sottoinsieme di dati.

::::::::::::::::::::::::::::::::::::::: challenge

## Scrivete il vostro ciclo personale

Come si scrive un ciclo che fa l'eco di tutti i 10 numeri da 0 a 9?

::::::::::::::: solution

## Soluzione

```bash
$ for loop_variable in 0 1 2 3 4 5 6 7 8 9
> do
>     echo $loop_variable
> done
```

```output
0
1
2
3
4
5
6
7
8
9
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Variabili nei loop

Questo esercizio si riferisce alla cartella `shell-lesson-data/exercise-data/alkanes`. la cartella `ls *.pdb` fornisce il seguente output:

```output
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
```

Qual è l'output del seguente codice?

```bash
$ for datafile in *.pdb
> do
>     ls *.pdb
> done
```

Ora, qual è l'output del seguente codice?

```bash
$ for datafile in *.pdb
> do
>     ls $datafile
> done
```

Perché questi due cicli danno risultati diversi?

::::::::::::::: solution

## Soluzione

Il primo blocco di codice dà lo stesso risultato a ogni iterazione del ciclo. Bash espande il carattere jolly `*.pdb` all'interno del corpo del ciclo (e anche prima dell'inizio del ciclo) in modo che corrisponda a tutti i file che terminano con `.pdb` e poi li elenca usando `ls`. Il ciclo espanso avrebbe il seguente aspetto:

```bash
$ for datafile in cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> do
>     ls cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> done
```

```output
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
```

Il secondo blocco di codice elenca un file diverso a ogni iterazione del ciclo. Il valore della variabile `datafile` viene valutato con `$datafile` e poi elencato con `ls`.

```output
cubane.pdb
ethane.pdb
methane.pdb
octane.pdb
pentane.pdb
propane.pdb
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Limitare gli insiemi di file

Quale sarebbe l'output dell'esecuzione del seguente ciclo nella directory `shell-lesson-data/exercise-data/alkanes`?

```bash
$ for filename in c*
> do
>     ls $filename
> done
```

1. Non sono elencati file.
2. Tutti i file sono elencati.
3. Sono elencati solo `cubane.pdb`, `octane.pdb` e `pentane.pdb`.
4. Viene elencato solo `cubane.pdb`.

::::::::::::::: solution

## Soluzione

4 è la risposta corretta. `*` corrisponde a zero o più caratteri, quindi qualsiasi nome di file che inizia con la lettera c, seguita da zero o più altri caratteri, verrà trovato.


:::::::::::::::::::::::::

In che modo l'output sarebbe diverso se si usasse invece questo comando?

```bash
$ for filename in *c*
> do
>     ls $filename
> done
```

1. verrebbero elencati gli stessi file.
2. Questa volta vengono elencati tutti i file.
3. Questa volta non sono elencati file.
4. I file `cubane.pdb` e `octane.pdb` saranno elencati.
5. Verrà elencato solo il file `octane.pdb`.

::::::::::::::: solution

## Soluzione

4 è la risposta corretta. `*` corrisponde a zero o più caratteri, quindi un nome di file con zero o più caratteri prima di una lettera c e zero o più caratteri dopo la lettera c sarà corrisposto.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Salvataggio su un file in un ciclo - Prima parte

Nella cartella `shell-lesson-data/exercise-data/alkanes`, qual è l'effetto di questo ciclo?

```bash
for alkanes in *.pdb
do
    echo $alkanes
    cat $alkanes > alkanes.pdb
done
```

1. Stampa `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb` e `propane.pdb`, e il testo di `propane.pdb` sarà salvato in un file chiamato `alkanes.pdb`.
2. stampa `cubane.pdb`, `ethane.pdb` e `methane.pdb`, e il testo di tutti e tre i file viene concatenato e salvato in un file chiamato `alkanes.pdb`.
3. Stampa `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb` e `pentane.pdb`, e il testo di `propane.pdb` sarà salvato in un file chiamato `alkanes.pdb`.
4. Nessuno dei precedenti.

::::::::::::::: solution

## Soluzione

1. il testo di ogni file viene scritto a turno nel file `alkanes.pdb`. Tuttavia, il file viene sovrascritto a ogni iterazione del ciclo, quindi il contenuto finale di `alkanes.pdb` è il testo del file `propane.pdb`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Salvataggio su un file in un ciclo - Parte seconda

Sempre nella cartella `shell-lesson-data/exercise-data/alkanes`, quale sarebbe l'output del seguente ciclo?

```bash
for datafile in *.pdb
do
    cat $datafile >> all.pdb
done
```

1. Tutto il testo di `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb` e `pentane.pdb` verrebbe concatenato e salvato in un file chiamato `all.pdb`.
2. Il testo di `ethane.pdb` verrà salvato in un file chiamato `all.pdb`.
3. Tutto il testo di `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb` e `propane.pdb` verrebbe concatenato e salvato in un file chiamato `all.pdb`.
4. Tutto il testo di `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb` e `propane.pdb` verrebbe stampato sullo schermo e salvato in un file chiamato `all.pdb`.

::::::::::::::: solution

## Soluzione

3 è la risposta corretta. `>>` aggiunge a un file, invece di sovrascriverlo con l'output rediretto da un comando. Dato che l'output del comando `cat` è stato reindirizzato, non viene stampato nulla sullo schermo.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

Continuiamo con il nostro esempio nella cartella `shell-lesson-data/exercise-data/creatures`. Ecco un ciclo leggermente più complicato:

```bash
$ for filename in *.dat
> do
>     echo $filename
>     head -n 100 $filename | tail -n 20
> done
```

La shell inizia espandendo `*.dat` per creare l'elenco dei file che elaborerà. Il **corpo del ciclo** esegue quindi due comandi per ciascuno di questi file. Il primo comando, `echo`, stampa i suoi argomenti della riga di comando sullo standard output. Ad esempio:

```bash
$ echo hello there
```

stampa:

```output
hello there
```

In questo caso, poiché la shell espande `$filename` come nome di un file, `echo $filename` stampa il nome del file. Si noti che non si può scrivere come:

```bash
$ for filename in *.dat
> do
>     $filename
>     head -n 100 $filename | tail -n 20
> done
```

perché così la prima volta nel ciclo, quando `$filename` si espande in `basilisk.dat`, la shell cercherebbe di eseguire `basilisk.dat` come programma. Infine, la combinazione `head` e `tail` seleziona le righe da 81 a 100 da qualsiasi file venga elaborato (assumendo che il file abbia almeno 100 righe).

::::::::::::::::::::::::::::::::::::::::: callout

## Spazi nei nomi

Gli spazi sono usati per separare gli elementi dell'elenco su cui si vuole eseguire il ciclo. Se uno di questi elementi contiene un carattere di spazio, dobbiamo circondarlo con le virgolette e fare la stessa cosa con la nostra variabile loop. Supponiamo che i nostri file di dati si chiamino:

```source
red dragon.dat
purple unicorn.dat
```

Per eseguire il ciclo su questi file, occorre aggiungere i doppi apici in questo modo:

```bash
$ for filename in "red dragon.dat" "purple unicorn.dat"
> do
>     head -n 100 "$filename" | tail -n 20
> done
```

È più semplice evitare di usare spazi (o altri caratteri speciali) nei nomi dei file.

I file di cui sopra non esistono, quindi se si esegue il codice precedente, il comando `head` non sarà in grado di trovarli; tuttavia, il messaggio di errore restituito mostrerà il nome dei file che si aspetta:

```error
head: cannot open ‘red dragon.dat' for reading: No such file or directory
head: cannot open ‘purple unicorn.dat' for reading: No such file or directory
```

Provate a rimuovere le virgolette intorno a `$filename` nel ciclo precedente per vedere l'effetto delle virgolette sugli spazi. Si noti che si ottiene un risultato dal comando loop per unicorn.dat quando si esegue questo codice nella directory `creatures`:

```output
head: cannot open ‘red' for reading: No such file or directory
head: cannot open ‘dragon.dat' for reading: No such file or directory
head: cannot open ‘purple' for reading: No such file or directory
CGGTACCGAA
AAGGGTCGCG
CAAGTGTTCC
...
```

::::::::::::::::::::::::::::::::::::::::::::::::::

Vogliamo modificare ciascuno dei file in `shell-lesson-data/exercise-data/creatures`, ma anche salvare una versione dei file originali. Vogliamo copiare i file originali in nuovi file chiamati `original-basilisk.dat` e `original-unicorn.dat`, per esempio. Non possiamo usare:

```bash
$ cp *.dat original-*.dat
```

perché si espanderebbe in:

```bash
$ cp basilisk.dat minotaur.dat unicorn.dat original-*.dat
```

Questo non avrebbe eseguito il backup dei nostri file, invece si ottiene un errore:

```error
cp: target `original-*.dat' is not a directory
```

Questo problema si presenta quando `cp` riceve più di due input. Quando ciò accade, si aspetta che l'ultimo ingresso sia una cartella in cui copiare tutti i file che gli sono stati passati. Poiché non esiste una cartella denominata `original-*.dat` nella cartella `creatures`, si ottiene un errore.

Invece, possiamo usare un ciclo:

```bash
$ for filename in *.dat
> do
>     cp $filename original-$filename
> done
```

Questo ciclo esegue il comando `cp` una volta per ogni nome di file. La prima volta, quando `$filename` si espande a `basilisk.dat`, la shell esegue:

```bash
cp basilisk.dat original-basilisk.dat
```

La seconda volta, il comando è:

```bash
cp minotaur.dat original-minotaur.dat
```

La terza e ultima volta, il comando è:

```bash
cp unicorn.dat original-unicorn.dat
```

Poiché il comando `cp` normalmente non produce alcun output, è difficile verificare che il ciclo funzioni correttamente. Tuttavia, abbiamo imparato in precedenza a stampare stringhe usando `echo` e possiamo modificare il ciclo per usare `echo` per stampare i nostri comandi senza eseguirli. Possiamo quindi verificare quali comandi verrebbero eseguiti nel ciclo non modificato.

Il diagramma seguente mostra cosa succede quando viene eseguito il ciclo modificato e dimostra come l'uso giudizioso di `echo` sia una buona tecnica di debug.

![](fig/shell_script_for_loop_flow_chart.svg){alt='Il ciclo for "for filename in .dat; do echo cp $filename original-$filename;done" assegnerà successivamente i nomi di tutti i file ".dat" nella cartella corrente alla variabile "$filename" e quindi eseguirà il comando. Con i file "basilisk.dat", "minotaur.dat" e "unicorn.dat" nella cartella corrente, il ciclo richiamerà successivamente il comando echo tre volte e stamperà tre righe: "cp basislisk.dat original-basilisk.dat", poi "cp minotaur.datoriginal-minotaur.dat" e infine "cp unicorn.datoriginal-unicorn.dat"'}

## Pipeline di Nelle: Elaborazione dei file

Nelle è ora pronta a elaborare i suoi file di dati usando `goostats.sh` --- uno script di shell scritto dal suo supervisore. Questo calcola alcune statistiche da un file campione di proteine e prende due argomenti:

1. un file di ingresso (contenente i dati grezzi)
2. un file di uscita (per memorizzare le statistiche calcolate)

Poiché sta ancora imparando a usare la shell, decide di costruire i comandi necessari per gradi. Il primo passo consiste nell'assicurarsi di poter selezionare i giusti file di input --- ricordate, questi sono quelli i cui nomi terminano in 'A' o 'B', piuttosto che in 'Z'. Spostandosi nella cartella `north-pacific-gyre`, Nelle digita:

```bash
$ cd
$ cd Desktop/shell-lesson-data/north-pacific-gyre
$ for datafile in NENE*A.txt NENE*B.txt
> do
>     echo $datafile
> done
```

```output
NENE01729A.txt
NENE01736A.txt
NENE01751A.txt

...
NENE02040B.txt
NENE02043B.txt
```

Il passo successivo è decidere come chiamare i file che il programma di analisi `goostats.sh` creerà. Prefissare il nome di ogni file di input con "stats" sembra semplice, quindi modifica il suo ciclo per farlo:

```bash
$ for datafile in NENE*A.txt NENE*B.txt
> do
>     echo $datafile stats-$datafile
> done
```

```output
NENE01729A.txt stats-NENE01729A.txt
NENE01736A.txt stats-NENE01729A.txt
NENE01751A.txt stats-NENE01729A.txt
...
NENE02040B.txt stats-NENE02040B.txt
NENE02043B.txt stats-NENE02043B.txt
```

Non ha ancora eseguito `goostats.sh`, ma ora è sicura di poter selezionare i file giusti e generare i giusti nomi di file di output.

Digitare più volte i comandi sta diventando noioso e Nelle è preoccupata di commettere errori, quindi invece di rientrare nel ciclo, preme <kbd>↑</kbd>. In risposta, la shell ripropone l'intero ciclo su una riga (usando i punti e virgola per separare i pezzi):

```bash
$ for datafile in NENE*A.txt NENE*B.txt; do echo $datafile stats-$datafile; done
```

Utilizzando il comando <kbd>←</kbd>, Nelle passa al comando `echo` e lo cambia in `bash goostats.sh`:

```bash
$ for datafile in NENE*A.txt NENE*B.txt; do bash goostats.sh $datafile stats-$datafile; done
```

quando si preme <kbd>Invio</kbd>, la shell esegue il comando modificato. Tuttavia, non sembra accadere nulla: non c'è output. Dopo un attimo, Nelle si rende conto che, poiché il suo script non stampa più nulla sullo schermo, non ha idea se sia in esecuzione, e tanto meno a quale velocità. Uccide il comando in esecuzione digitando <kbd>Ctrl</kbd>\+<kbd>C</kbd>, usa <kbd>↑</kbd> per ripetere il comando e lo modifica in modo da leggere:

```bash
$ for datafile in NENE*A.txt NENE*B.txt; do echo $datafile;
bash goostats.sh $datafile stats-$datafile; done
```

::::::::::::::::::::::::::::::::::::::::: callout

## Inizio e fine

Possiamo spostarci all'inizio di una riga nella shell digitando <kbd>Ctrl</kbd>\+<kbd>A</kbd> e alla fine usando <kbd>Ctrl</kbd>\+<kbd>E</kbd>.


::::::::::::::::::::::::::::::::::::::::::::::::::

Quando il programma viene eseguito ora, produce una riga di output ogni cinque secondi circa:

```output
NENE01729A.txt
NENE01736A.txt
NENE01751A.txt
...
```

1518 per 5 secondi, diviso per 60, indica che il suo script impiegherà circa due ore per essere eseguito. Come controllo finale, apre un'altra finestra di terminale, entra in `north-pacific-gyre` e usa `cat stats-NENE01729B.txt` per esaminare uno dei file di output. Sembra tutto a posto, quindi decide di prendere un caffè e di mettersi in pari con la lettura.

::::::::::::::::::::::::::::::::::::::::: callout

## Chi conosce la storia può scegliere di ripeterla

Un altro modo per ripetere il lavoro precedente è quello di usare il comando `history` per ottenere un elenco delle ultime centinaia di comandi eseguiti, e poi usare `!123` (dove '123' è sostituito dal numero del comando) per ripetere uno di quei comandi. Ad esempio, se Nelle digita questo:

```bash
$ history | tail -n 5
```

```output
456  for datafile in NENE*A.txt NENE*B.txt; do   echo $datafile stats-$datafile; done
457  for datafile in NENE*A.txt NENE*B.txt; do echo $datafile stats-$datafile; done
458  for datafile in NENE*A.txt NENE*B.txt; do bash goostats.sh $datafile stats-$datafile; done
459  for datafile in NENE*A.txt NENE*B.txt; do echo $datafile; bash goostats.sh $datafile
stats-$datafile; done
460  history | tail -n 5
```

quindi può eseguire nuovamente `goostats.sh` sui file semplicemente digitando `!459`.


::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Altri comandi della cronologia

Esistono numerosi altri comandi di scelta rapida per accedere alla cronologia.

- <kbd>Ctrl</kbd>\+<kbd>R</kbd> entra in modalità di ricerca nella cronologia 'reverse-i-search' e trova il comando più recente nella cronologia che corrisponde al testo inserito successivamente. Premere <kbd>Ctrl</kbd>\+<kbd>R</kbd> una o più volte per cercare le corrispondenze precedenti. È quindi possibile utilizzare i tasti freccia sinistra e destra per scegliere la riga e modificarla, quindi premere <kbd>Return</kbd> per eseguire il comando.
- `!!` recupera il comando immediatamente precedente (si può trovare o meno più conveniente che usare <kbd>↑</kbd>)
- `!$` recupera l'ultima parola dell'ultimo comando. Questo è utile più spesso di quanto ci si possa aspettare: dopo `bash goostats.sh NENE01729B.txt stats-NENE01729B.txt`, si può digitare `less !$` per guardare il file `stats-NENE01729B.txt`, il che è più veloce che fare <kbd>↑</kbd> e modificare la riga di comando.

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Esecuzione a secco

Un ciclo è un modo per fare molte cose contemporaneamente --- o per fare molti errori contemporaneamente se fa la cosa sbagliata. Un modo per verificare cosa farebbe un ciclo è quello di `echo` i comandi che eseguirebbe invece di eseguirli effettivamente.

Supponiamo di voler vedere in anteprima i comandi che il seguente ciclo eseguirà senza eseguirli effettivamente:

```bash
$ for datafile in *.pdb
> do
>     cat $datafile >> all.pdb
> done
```

Qual è la differenza tra i due cicli sottostanti e quale vogliamo eseguire?

```bash
# Version 1
$ for datafile in *.pdb
> do
>     echo cat $datafile >> all.pdb
> done
```

```bash
# Version 2
$ for datafile in *.pdb
> do
>     echo "cat $datafile >> all.pdb"
> done
```

::::::::::::::: solution

## Soluzione

La seconda versione è quella che vogliamo eseguire. Questa stampa sullo schermo tutto ciò che è racchiuso tra le virgolette, espandendo il nome della variabile del ciclo perché lo abbiamo preceduto da un segno di dollaro. Inoltre, non modifica e non crea il file `all.pdb`, poiché `>>` viene trattato letteralmente come parte di una stringa e non come un'istruzione di reindirizzamento.

La prima versione aggiunge l'output del comando `echo cat $datafile` al file `all.pdb`. Questo file conterrà solo l'elenco: `cat cubane.pdb`, `cat ethane.pdb`, `cat methane.pdb` ecc.

provate voi stessi entrambe le versioni per vedere l'output! Assicurarsi di aprire il file `all.pdb` per visualizzarne il contenuto.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Cicli annidati

Supponiamo di voler impostare una struttura di directory per organizzare alcuni esperimenti di misurazione delle costanti di velocità di reazione con diversi composti *e* diverse temperature. Quale sarebbe il risultato del seguente codice:

```bash
$ for species in cubane ethane methane
> do
>     for temperature in 25 30 37 40
>     do
>         mkdir $species-$temperature
>     done
> done
```

::::::::::::::: solution

## Soluzione

Abbiamo un ciclo annidato, cioè contenuto all'interno di un altro ciclo, quindi per ogni specie nel ciclo esterno, il ciclo interno (il ciclo annidato) itera sull'elenco delle temperature e crea una nuova cartella per ogni combinazione.

provate voi stessi a eseguire il codice per vedere quali cartelle vengono create!



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::: keypoints

- Un ciclo `for` ripete i comandi una volta per ogni cosa in un elenco.
- Ogni ciclo `for` ha bisogno di una variabile per riferirsi alla cosa su cui sta operando.
- Usare `$name` per espandere una variabile (cioè per ottenere il suo valore). si può usare anche `${name}`.
- Non usare spazi, virgolette o caratteri jolly come '\*' o '?' nei nomi dei file, perché complicano l'espansione delle variabili.
- Dare ai file nomi coerenti e facili da abbinare con i caratteri jolly, per facilitarne la selezione per il loop.
- Usare il tasto freccia su per scorrere i comandi precedenti e modificarli e ripeterli.
- Usare <kbd>Ctrl</kbd>\+<kbd>R</kbd> per cercare tra i comandi precedentemente inseriti.
- Usare `history` per visualizzare i comandi recenti e `![number]` per ripetere un comando per numero.

::::::::::::::::::::::::::::::::::::::::::::::::::



