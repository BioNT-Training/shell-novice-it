---
title: Script di shell
teaching: 30
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Scrivere uno script di shell che esegua un comando o una serie di comandi per un insieme fisso di file.
- Eseguire uno script di shell dalla riga di comando.
- Scrive uno script di shell che opera su un insieme di file definiti dall'utente sulla riga di comando.
- Creare pipeline che includano script di shell scritti da voi e da altri.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come posso salvare e riutilizzare i comandi?

::::::::::::::::::::::::::::::::::::::::::::::::::

Siamo finalmente pronti a vedere cosa rende la shell un ambiente di programmazione così potente. Prenderemo i comandi che ripetiamo frequentemente e li salveremo in file, in modo da poter rieseguire tutte le operazioni in un secondo momento digitando un solo comando. Per ragioni storiche, un gruppo di comandi salvati in un file viene solitamente chiamato **scritto di shell**, ma non fatevi ingannare: si tratta in realtà di piccoli programmi.

La scrittura di script di shell non solo renderà il lavoro più veloce, ma eviterà anche di dover ridigitare gli stessi comandi più volte. Inoltre, il lavoro sarà più accurato (meno possibilità di errori di battitura) e più riproducibile. Se si torna al proprio lavoro in un secondo momento (o se qualcun altro trova il proprio lavoro e vuole basarsi su di esso), sarà possibile riprodurre gli stessi risultati semplicemente eseguendo il proprio script, invece di dover ricordare o digitare nuovamente un lungo elenco di comandi.

Iniziamo tornando a `alkanes/` e creando un nuovo file, `middle.sh`, che diventerà il nostro script di shell:

```bash
$ cd alkanes
$ nano middle.sh
```

Il comando `nano middle.sh` apre il file `middle.sh` all'interno dell'editor di testo 'nano' (che viene eseguito all'interno della shell). Se il file non esiste, verrà creato. È possibile utilizzare l'editor di testo per modificare direttamente il file inserendo la seguente riga:

```source
head -n 15 octane.pdb | tail -n 5
```

Questa è una variante della pipe costruita in precedenza, che seleziona le righe 11-15 del file `octane.pdb`. Ricordate che non lo stiamo ancora eseguendo come comando; stiamo solo incorporando i comandi in un file.

Poi si salva il file (`Ctrl-O` in nano) e si esce dall'editor di testo (`Ctrl-X` in nano). Verificare che la directory `alkanes` contenga ora un file chiamato `middle.sh`.

Una volta salvato il file, possiamo chiedere alla shell di eseguire i comandi in esso contenuti. La nostra shell si chiama `bash`, quindi eseguiamo il seguente comando:

```bash
$ bash middle.sh
```

```output
ATOM      9  H           1      -4.502   0.681   0.785  1.00  0.00
ATOM     10  H           1      -5.254  -0.243  -0.537  1.00  0.00
ATOM     11  H           1      -4.357   1.252  -0.895  1.00  0.00
ATOM     12  H           1      -3.009  -0.741  -1.467  1.00  0.00
ATOM     13  H           1      -3.172  -1.337   0.206  1.00  0.00
```

Sicuramente l'output del nostro script è esattamente quello che otterremmo se eseguissimo direttamente la pipeline.

::::::::::::::::::::::::::::::::::::::::: callout

## Testo vs. Qualsiasi cosa

Di solito chiamiamo "editor di testo" programmi come Microsoft Word o LibreOffice Writer, ma dobbiamo essere un po' più attenti quando si tratta di programmazione. Per impostazione predefinita, Microsoft Word utilizza i file `.docx` per memorizzare non solo il testo, ma anche le informazioni di formattazione relative a caratteri, intestazioni e così via. Queste informazioni extra non sono memorizzate come caratteri e non hanno alcun significato per strumenti come `head`, che si aspetta che i file di input contengano solo le lettere, le cifre e la punteggiatura di una tastiera standard. Quando si modificano i programmi, quindi, è necessario utilizzare un editor di testo normale o fare attenzione a salvare i file come testo normale.


::::::::::::::::::::::::::::::::::::::::::::::::::

E se volessimo selezionare delle righe da un file arbitrario? Potremmo modificare `middle.sh` ogni volta per cambiare il nome del file, ma questo probabilmente richiederebbe più tempo che digitare nuovamente il comando nella shell ed eseguirlo con un nuovo nome di file. Modifichiamo invece `middle.sh` e rendiamolo più versatile:

```bash
$ nano middle.sh
```

Ora, all'interno di "nano", sostituire il testo `octane.pdb` con la variabile speciale chiamata `$1`:

```source
head -n 15 "$1" | tail -n 5
```

All'interno di uno script di shell, `$1` significa "il primo nome di file (o altro argomento) sulla riga di comando". Ora possiamo eseguire il nostro script in questo modo:

```bash
$ bash middle.sh octane.pdb
```

```output
ATOM      9  H           1      -4.502   0.681   0.785  1.00  0.00
ATOM     10  H           1      -5.254  -0.243  -0.537  1.00  0.00
ATOM     11  H           1      -4.357   1.252  -0.895  1.00  0.00
ATOM     12  H           1      -3.009  -0.741  -1.467  1.00  0.00
ATOM     13  H           1      -3.172  -1.337   0.206  1.00  0.00
```

o su un file diverso come questo:

```bash
$ bash middle.sh pentane.pdb
```

```output
ATOM      9  H           1       1.324   0.350  -1.332  1.00  0.00
ATOM     10  H           1       1.271   1.378   0.122  1.00  0.00
ATOM     11  H           1      -0.074  -0.384   1.288  1.00  0.00
ATOM     12  H           1      -0.048  -1.362  -0.205  1.00  0.00
ATOM     13  H           1      -1.183   0.500  -1.412  1.00  0.00
```

::::::::::::::::::::::::::::::::::::::::: callout

## Doppie virgolette intorno agli argomenti

Per la stessa ragione per cui mettiamo la variabile loop tra virgolette doppie, nel caso in cui il nome del file contenga spazi, circondiamo `$1` con virgolette doppie.


::::::::::::::::::::::::::::::::::::::::::::::::::

Attualmente, dobbiamo modificare `middle.sh` ogni volta che vogliamo regolare l'intervallo di righe che viene restituito. Risolviamo questo problema configurando il nostro script in modo che utilizzi tre argomenti della riga di comando. Dopo il primo argomento da riga di comando (`$1`), ogni ulteriore argomento fornito sarà accessibile tramite le variabili speciali `$1`, `$2`, `$3`, che si riferiscono rispettivamente al primo, secondo e terzo argomento da riga di comando.

Sapendo questo, possiamo usare argomenti aggiuntivi per definire l'intervallo di righe da passare rispettivamente a `head` e `tail`:

```bash
$ nano middle.sh
```

```source
head -n "$2" "$1" | tail -n "$3"
```

Ora possiamo eseguire:

```bash
$ bash middle.sh pentane.pdb 15 5
```

```output
ATOM      9  H           1       1.324   0.350  -1.332  1.00  0.00
ATOM     10  H           1       1.271   1.378   0.122  1.00  0.00
ATOM     11  H           1      -0.074  -0.384   1.288  1.00  0.00
ATOM     12  H           1      -0.048  -1.362  -0.205  1.00  0.00
ATOM     13  H           1      -1.183   0.500  -1.412  1.00  0.00
```

Cambiando gli argomenti del nostro comando, possiamo cambiare il comportamento del nostro script:

```bash
$ bash middle.sh pentane.pdb 20 5
```

```output
ATOM     14  H           1      -1.259   1.420   0.112  1.00  0.00
ATOM     15  H           1      -2.608  -0.407   1.130  1.00  0.00
ATOM     16  H           1      -2.540  -1.303  -0.404  1.00  0.00
ATOM     17  H           1      -3.393   0.254  -0.321  1.00  0.00
TER      18              1
```

Questo funziona, ma la prossima persona che leggerà `middle.sh` potrebbe metterci un attimo a capire cosa fa. Possiamo migliorare il nostro script aggiungendo alcuni **commenti** all'inizio:

```bash
$ nano middle.sh
```

```source
# Select lines from the middle of a file.
# Usage: bash middle.sh filename end_line num_lines
head -n "$2" "$1" | tail -n "$3"
```

Un commento inizia con un carattere `#` e arriva fino alla fine della riga. Il computer ignora i commenti, ma sono preziosi per aiutare le persone (compreso il vostro futuro io) a capire e usare gli script. L'unica avvertenza è che ogni volta che si modifica lo script, bisogna controllare che il commento sia ancora corretto. Una spiegazione che manda il lettore nella direzione sbagliata è peggiore di nessuna.

Cosa succede se si vogliono elaborare molti file in una singola pipeline? Per esempio, se vogliamo ordinare i nostri file `.pdb` per lunghezza, digitiamo:

```bash
$ wc -l *.pdb | sort -n
```

perché `wc -l` elenca il numero di righe nei file (ricordate che `wc` sta per "conteggio delle parole", aggiungendo l'opzione `-l` significa invece "conteggio delle righe") e `sort -n` ordina le cose numericamente. Si potrebbe inserire in un file, ma in questo modo verrebbe ordinato solo un elenco di file `.pdb` nella directory corrente. Se vogliamo essere in grado di ottenere un elenco ordinato di altri tipi di file, abbiamo bisogno di un modo per inserire tutti questi nomi nello script. Non possiamo usare `$1`, `$2` e così via perché non sappiamo quanti file ci sono. Si usa invece la variabile speciale `$@`, che significa "Tutti gli argomenti della riga di comando dello script di shell". Si dovrebbe anche mettere `$@` tra doppi apici per gestire il caso di argomenti contenenti spazi (`"$@"` è una sintassi speciale ed è equivalente a `"$1"` `"$2"` ...).

Ecco un esempio:

```bash
$ nano sorted.sh
```

```source
# Sort files by their length.
# Usage: bash sorted.sh one_or_more_filenames
wc -l "$@" | sort -n
```

```bash
$ bash sorted.sh *.pdb ../creatures/*.dat
```

```output
9 methane.pdb
12 ethane.pdb
15 propane.pdb
20 cubane.pdb
21 pentane.pdb
30 octane.pdb
163 ../creatures/basilisk.dat
163 ../creatures/minotaur.dat
163 ../creatures/unicorn.dat
596 total
```

::::::::::::::::::::::::::::::::::::::: challenge

## Elenco delle specie uniche

Leah ha diverse centinaia di file di dati, ognuno dei quali è formattato in questo modo:

```source
2013-11-05,deer,5
2013-11-05,rabbit,22
2013-11-05,raccoon,7
2013-11-06,rabbit,19
2013-11-06,deer,2
2013-11-06,fox,1
2013-11-07,rabbit,18
2013-11-07,bear,1
```

Un esempio di questo tipo di file è riportato in `shell-lesson-data/exercise-data/animal-counts/animals.csv`.

Possiamo usare il comando `cut -d , -f 2 animals.csv | sort | uniq` per produrre le specie uniche in `animals.csv`. Per evitare di dover digitare ogni volta questa serie di comandi, uno scienziato può scegliere di scrivere uno script di shell.

Scrivere uno script di shell chiamato `species.sh` che accetta un numero qualsiasi di nomi di file come argomenti della riga di comando e utilizza una variante del comando precedente per stampare un elenco delle specie uniche che compaiono in ciascuno di questi file separatamente.

::::::::::::::: solution

## Soluzione

```bash
# Script to find unique species in csv files where species is the second data field
# This script accepts any number of file names as command line arguments

# Loop over all files
for file in $@
do
    echo "Unique species in $file:"
    # Extract species names
    cut -d , -f 2 $file | sort | uniq
done
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

Supponiamo di aver appena eseguito una serie di comandi che hanno fatto qualcosa di utile, ad esempio la creazione di un grafico che vorremmo utilizzare in un articolo. Se vogliamo essere in grado di ricreare il grafico in un secondo momento, vogliamo salvare i comandi in un file. Invece di digitarli di nuovo (e potenzialmente sbagliarli), possiamo fare così:

```bash
$ history | tail -n 5 > redo-figure-3.sh
```

Il file `redo-figure-3.sh` ora contiene:

```source
297 bash goostats.sh NENE01729B.txt stats-NENE01729B.txt
298 bash goodiff.sh stats-NENE01729B.txt /data/validated/01729.txt > 01729-differences.txt
299 cut -d ',' -f 2-3 01729-differences.txt > 01729-time-series.txt
300 ygraph --format scatter --color bw --borders none 01729-time-series.txt figure-3.png
301 history | tail -n 5 > redo-figure-3.sh
```

Dopo un attimo di lavoro in un editor per rimuovere i numeri di serie sui comandi e per rimuovere la riga finale in cui abbiamo chiamato il comando `history`, abbiamo una registrazione completamente accurata di come abbiamo creato la figura.

::::::::::::::::::::::::::::::::::::::: challenge

## Perché registrare i comandi nella cronologia prima di eseguirli?

Se si esegue il comando:

```bash
$ history | tail -n 5 > recent.sh
```

l'ultimo comando nel file è il comando `history` stesso, cioè la shell ha aggiunto `history` al registro dei comandi prima di eseguirlo. In effetti, la shell aggiunge *sempre* comandi al log prima di eseguirli. Perché pensate che lo faccia?

::::::::::::::: solution

## Soluzione

Se un comando provoca un arresto anomalo o un blocco, potrebbe essere utile sapere qual è il comando in questione, per poter indagare sul problema. Se il comando venisse registrato solo dopo la sua esecuzione, non avremmo una registrazione dell'ultimo comando eseguito in caso di crash.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

In pratica, la maggior parte delle persone sviluppa script di shell eseguendo i comandi al prompt della shell un paio di volte per assicurarsi che stiano facendo la cosa giusta, poi li salva in un file per riutilizzarli. Questo stile di lavoro consente di riciclare ciò che si scopre sui propri dati e sul proprio flusso di lavoro con una sola chiamata a `history` e un po' di modifiche per ripulire l'output e salvarlo come script di shell.

## Pipeline di Nelle: Creazione di uno script

Il supervisore di Nelle ha insistito sul fatto che tutte le sue analisi devono essere riproducibili. Il modo più semplice per catturare tutti i passaggi è uno script.

Per prima cosa torniamo alla directory del progetto di Nelle:

```bash
$ cd ../../north-pacific-gyre/
```

Crea un file usando `nano` ...

```bash
$ nano do-stats.sh
```

... che contiene quanto segue:

```bash
# Calculate stats for data files.
for datafile in "$@"
do
    echo $datafile
    bash goostats.sh $datafile stats-$datafile
done
```

Salva il tutto in un file chiamato `do-stats.sh`, in modo da poter rifare la prima fase della sua analisi digitando:

```bash
$ bash do-stats.sh NENE*A.txt NENE*B.txt
```

Può anche fare questo:

```bash
$ bash do-stats.sh NENE*A.txt NENE*B.txt | wc -l
```

in modo che l'output sia solo il numero di file elaborati piuttosto che i nomi dei file elaborati.

Una cosa da notare dello script di Nelle è che lascia che sia la persona che lo esegue a decidere quali file elaborare. Avrebbe potuto scriverlo come:

```bash
# Calculate stats for Site A and Site B data files.
for datafile in NENE*A.txt NENE*B.txt
do
    echo $datafile
    bash goostats.sh $datafile stats-$datafile
done
```

Il vantaggio è che in questo modo si selezionano sempre i file giusti, senza doversi ricordare di escludere i file "Z". Lo svantaggio è che seleziona *sempre* solo quei file --- non può eseguirlo su tutti i file (compresi i file 'Z'), o sui file 'G' o 'H' che i suoi colleghi in Antartide stanno producendo, senza modificare lo script. Se volesse essere più avventurosa, potrebbe modificare il suo script per verificare la presenza di argomenti da riga di comando e usare `NENE*A.txt NENE*B.txt` se non ne vengono forniti. Naturalmente, questo introduce un altro compromesso tra flessibilità e complessità.

::::::::::::::::::::::::::::::::::::::: challenge

## Variabili negli script di shell

Nella directory `alkanes`, immaginate di avere uno script di shell chiamato `script.sh` contenente i seguenti comandi:

```bash
head -n $2 $1
tail -n $3 $1
```

Mentre ci si trova nella directory `alkanes`, si digita il seguente comando:

```bash
$ bash script.sh '*.pdb' 1 1
```

Quale dei seguenti risultati vi aspettereste di vedere?

1. Tutte le righe tra la prima e l'ultima di ogni file che termina con `.pdb` nella directory `alkanes`
2. La prima e l'ultima riga di ogni file che termina con `.pdb` nella directory `alkanes`
3. La prima e l'ultima riga di ogni file nella directory `alkanes`
4. Errore a causa delle virgolette intorno a `*.pdb`

::::::::::::::: solution

## Soluzione

la risposta corretta è 2.

Le variabili speciali `$1`, `$2` e `$3` rappresentano gli argomenti della riga di comando dati allo script, in modo che i comandi eseguiti siano:

```bash
$ head -n 1 cubane.pdb ethane.pdb octane.pdb pentane.pdb propane.pdb
$ tail -n 1 cubane.pdb ethane.pdb octane.pdb pentane.pdb propane.pdb
```

La shell non espande `'*.pdb'` perché è racchiuso tra virgolette. Pertanto, il primo argomento dello script è `'*.pdb'` che viene espanso all'interno dello script da `head` e `tail`.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Trova il file più lungo con una data estensione

Scrivere uno script di shell chiamato `longest.sh` che prenda come argomenti il nome di una directory e l'estensione di un nome di file e stampi il nome del file con il maggior numero di righe in quella directory con quell'estensione. Ad esempio:

```bash
$ bash longest.sh shell-lesson-data/exercise-data/alkanes pdb
```

stamperebbe il nome del file `.pdb` in `shell-lesson-data/exercise-data/alkanes` che ha il maggior numero di righe.

Sentitevi liberi di testare il vostro script su un'altra directory, ad es.

```bash
$ bash longest.sh shell-lesson-data/exercise-data/writing txt
```

::::::::::::::: solution

## Soluzione

```bash
# Shell script which takes two arguments:
#    1. a directory name
#    2. a file extension
# and prints the name of the file in that directory
# with the most lines which matches the file extension.

wc -l $1/*.$2 | sort -n | tail -n 2 | head -n 1
```

La prima parte della pipeline, `wc -l $1/*.$2 | sort -n`, conta le righe di ogni file e le ordina numericamente (la più grande per ultima). Quando c'è più di un file, `wc` produce anche una riga finale di riepilogo, che dà il numero totale di righe in *tutti* i file. Si usa `tail -n 2 | head -n 1` per eliminare quest'ultima riga.

Con `wc -l $1/*.$2 | sort -n | tail -n 1` vedremo la riga di riepilogo finale: possiamo costruire la nostra pipeline a pezzi per essere sicuri di capire l'output.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Comprensione della lettura degli script

Per questa domanda, consideriamo ancora una volta la directory `shell-lesson-data/exercise-data/alkanes`. Questa contiene una serie di file `.pdb` oltre ad altri file eventualmente creati. Spiegare che cosa farebbe ciascuno dei tre script seguenti se eseguito rispettivamente come `bash script1.sh *.pdb`, `bash script2.sh *.pdb` e `bash script3.sh *.pdb`.

```bash
# Script 1
echo *.*
```

```bash
# Script 2
for filename in $1 $2 $3
do
    cat $filename
done
```

```bash
# Script 3
echo $@.pdb
```

::::::::::::::: solution

## Soluzioni

In ogni caso, la shell espande il carattere jolly in `*.pdb` prima di passare l'elenco risultante di nomi di file come argomenti allo script.

Lo script 1 stampa un elenco di tutti i file che contengono un punto nel loro nome. Gli argomenti passati allo script non vengono utilizzati in nessun punto dello script.

Lo script 2 stampa il contenuto dei primi 3 file con estensione `.pdb`. `$1`, `$2` e `$3` si riferiscono rispettivamente al primo, al secondo e al terzo argomento.

Lo script 3 stamperebbe tutti gli argomenti dello script (cioè tutti i file `.pdb`), seguiti da `.pdb`. `$@` si riferisce a *tutti* gli argomenti dati a uno script di shell.

```output
cubane.pdb ethane.pdb methane.pdb octane.pdb pentane.pdb propane.pdb.pdb
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Script di Debug

Si supponga di aver salvato il seguente script in un file chiamato `do-errors.sh` nella directory `north-pacific-gyre` di Nelle:

```bash
# Calculate stats for data files.
for datafile in "$@"
do
    echo $datfile
    bash goostats.sh $datafile stats-$datafile
done
```

Quando lo si esegue dalla directory `north-pacific-gyre`:

```bash
$ bash do-errors.sh NENE*A.txt NENE*B.txt
```

l'output è vuoto. Per capirne il motivo, rieseguire lo script utilizzando l'opzione `-x`:

```bash
$ bash -x do-errors.sh NENE*A.txt NENE*B.txt
```

Cosa mostra l'output? Quale riga è responsabile dell'errore?

::::::::::::::: solution

## Soluzione

L'opzione `-x` fa sì che `bash` venga eseguito in modalità di debug. In questo modo viene stampato ogni comando man mano che viene eseguito, il che aiuta a individuare gli errori. In questo esempio, possiamo vedere che `echo` non sta stampando nulla. Abbiamo commesso un errore di battitura nel nome della variabile del ciclo e la variabile `datfile` non esiste, quindi restituisce una stringa vuota.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::: keypoints

- Salva i comandi in file (di solito chiamati script di shell) per riutilizzarli.
- `bash [filename]` esegue i comandi salvati in un file.
- `$@` si riferisce a tutti gli argomenti della riga di comando di uno script di shell.
- `$1`, `$2`, ecc. si riferiscono al primo argomento della riga di comando, al secondo argomento della riga di comando, ecc.
- Mettere le variabili tra virgolette se i valori possono contenere spazi.
- Lasciare che siano gli utenti a decidere quali file elaborare è più flessibile e più coerente con i comandi Unix integrati.

::::::::::::::::::::::::::::::::::::::::::::::::::



