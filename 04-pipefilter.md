---
title: Tubi e filtri
teaching: 25
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Spiegare il vantaggio di collegare i comandi con pipe e filtri.
- Combinare sequenze di comandi per ottenere un nuovo output
- Reindirizzare l'output di un comando a un file.
- Spiegate cosa succede di solito se a un programma o a una pipeline non viene dato alcun input da elaborare.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come posso combinare i comandi esistenti per produrre l'output desiderato?
- Come posso mostrare solo una parte dell'output?

::::::::::::::::::::::::::::::::::::::::::::::::::

Ora che conosciamo alcuni comandi di base, possiamo finalmente esaminare la caratteristica più potente della shell: la facilità con cui ci permette di combinare programmi esistenti in modi nuovi. Inizieremo con la cartella `shell-lesson-data/exercise-data/alkanes` che contiene sei file che descrivono alcune semplici molecole organiche. L'estensione `.pdb` indica che questi file sono in formato Protein Data Bank, un semplice formato di testo che specifica il tipo e la posizione di ogni atomo nella molecola.

```bash
$ ls
```

```output
cubane.pdb    methane.pdb    pentane.pdb
ethane.pdb    octane.pdb     propane.pdb
```

Eseguiamo un comando di esempio:

```bash
$ wc cubane.pdb
```

```output
20  156 1158 cubane.pdb
```

`wc` è il comando "contaparole": conta il numero di righe, parole e caratteri nei file (restituendo i valori in questo ordine, da sinistra a destra).

Se si esegue il comando `wc *.pdb`, il `*` in `*.pdb` corrisponde a zero o più caratteri, quindi la shell trasforma `*.pdb` in un elenco di tutti i file `.pdb` nella cartella corrente:

```bash
$ wc *.pdb
```

```output
  20  156  1158  cubane.pdb
  12  84   622   ethane.pdb
   9  57   422   methane.pdb
  30  246  1828  octane.pdb
  21  165  1226  pentane.pdb
  15  111  825   propane.pdb
 107  819  6081  total
```

Si noti che `wc *.pdb` mostra anche il numero totale di tutte le righe nell'ultima riga dell'output.

Se si esegue `wc -l` invece di `wc`, l'output mostra solo il numero di righe per file:

```bash
$ wc -l *.pdb
```

```output
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
  30  octane.pdb
  21  pentane.pdb
  15  propane.pdb
 107  total
```

Le opzioni `-m` e `-w` possono essere usate anche con il comando `wc` per mostrare rispettivamente solo il numero di caratteri o il numero di parole.

::::::::::::::::::::::::::::::::::::::::: callout

## Perché non fa nulla?

Cosa succede se un comando deve elaborare un file, ma non gli viene assegnato un nome? Ad esempio, cosa succede se digitiamo:

```bash
$ wc -l
```

ma non digita `*.pdb` (o qualsiasi altra cosa) dopo il comando? Poiché non ha alcun nome di file, `wc` presume di dover elaborare l'input dato dal prompt dei comandi, quindi se ne sta lì ad aspettare che gli si forniscano dei dati in modo interattivo. Dall'esterno, però, tutto ciò che si vede è che è seduto lì e il comando non sembra fare nulla.

Se commettete questo tipo di errore, potete uscire da questo stato tenendo premuto il tasto control (<kbd>Ctrl</kbd>) e premendo una volta la lettera <kbd>C</kbd>: <kbd>Ctrl</kbd>\+<kbd>C</kbd>. Quindi rilasciare entrambi i tasti.


::::::::::::::::::::::::::::::::::::::::::::::::::

## Cattura dell'output da comandi

Quale di questi file contiene il minor numero di righe? È facile rispondere a questa domanda quando ci sono solo sei file, ma se ce ne fossero 6000? Il primo passo verso la soluzione consiste nell'eseguire il comando:

```bash
$ wc -l *.pdb > lengths.txt
```

Il simbolo maggiore di, `>`, indica alla shell di **reindirizzare** l'output del comando a un file invece di stamparlo sullo schermo. Questo comando non stampa alcun output sullo schermo, perché tutto ciò che `wc` avrebbe stampato è andato invece nel file `lengths.txt`. Se il file non esiste prima dell'emissione del comando, la shell lo creerà. Se il file esiste già, verrà sovrascritto silenziosamente, con conseguente perdita di dati. Pertanto, i comandi **redirect** richiedono cautela.

`ls lengths.txt` conferma che il file esiste:

```bash
$ ls lengths.txt
```

```output
lengths.txt
```

Ora possiamo inviare il contenuto di `lengths.txt` allo schermo usando `cat lengths.txt`. Il comando `cat` prende il nome da 'concatenate', cioè unire insieme, e stampa il contenuto dei file uno dopo l'altro. In questo caso c'è un solo file, quindi `cat` ci mostra solo ciò che contiene:

```bash
$ cat lengths.txt
```

```output
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
  30  octane.pdb
  21  pentane.pdb
  15  propane.pdb
 107  total
```

::::::::::::::::::::::::::::::::::::::::: callout

## Output Pagina per Pagina

In questa lezione continueremo a usare `cat` per comodità e coerenza, ma ha lo svantaggio di scaricare sempre l'intero file sullo schermo. Più utile nella pratica è il comando `less` (ad esempio `less lengths.txt`). Questo comando visualizza una schermata del file e poi si ferma. Si può andare avanti di una schermata premendo la barra spaziatrice, o indietro di una premendo `b`. Premere `q` per uscire.


::::::::::::::::::::::::::::::::::::::::::::::::::

## Filtraggio dell'output

Il prossimo passo sarà quello di usare il comando `sort` per ordinare il contenuto del file `lengths.txt`. Ma prima faremo un esercizio per imparare qualcosa sul comando sort:

::::::::::::::::::::::::::::::::::::::: challenge

## Cosa fa `sort -n`?

Il file `shell-lesson-data/exercise-data/numbers.txt` contiene le seguenti righe:

```source
10
2
19
22
6
```

Se eseguiamo `sort` su questo file, l'output è:

```output
10
19
2
22
6
```

Se si esegue `sort -n` sullo stesso file, si ottiene invece questo:

```output
2
6
10
19
22
```

Spiegare perché `-n` ha questo effetto.

::::::::::::::: solution

## Soluzione

L'opzione `-n` specifica un ordinamento numerico anziché alfanumerico.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

Useremo anche l'opzione `-n` per specificare che l'ordinamento è numerico invece che alfanumerico. Questo non modifica il file, ma invia il risultato dell'ordinamento allo schermo:

```bash
$ sort -n lengths.txt
```

```output
  9  methane.pdb
 12  ethane.pdb
 15  propane.pdb
 20  cubane.pdb
 21  pentane.pdb
 30  octane.pdb
107  total
```

Possiamo mettere l'elenco ordinato di righe in un altro file temporaneo chiamato `sorted-lengths.txt` mettendo `> sorted-lengths.txt` dopo il comando, proprio come abbiamo usato `> lengths.txt` per mettere l'output di `wc` in `lengths.txt`. Una volta fatto questo, si può eseguire un altro comando chiamato `head` per ottenere le prime righe in `sorted-lengths.txt`:

```bash
$ sort -n lengths.txt > sorted-lengths.txt
$ head -n 1 sorted-lengths.txt
```

```output
  9  methane.pdb
```

L'uso di `-n 1` con `head` indica che vogliamo solo la prima riga del file; `-n 20` otterrebbe le prime 20 e così via. Poiché `sorted-lengths.txt` contiene le lunghezze dei file ordinate dalla minore alla maggiore, l'output di `head` deve essere il file con il minor numero di righe.

::::::::::::::::::::::::::::::::::::::::: callout

## Reindirizzamento allo stesso file

È una pessima idea cercare di reindirizzare l'output di un comando che opera su un file allo stesso file. Ad esempio:

```bash
$ sort -n lengths.txt > lengths.txt
```

Fare qualcosa del genere potrebbe dare risultati errati e/o cancellare il contenuto di `lengths.txt`.


::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Cosa significa `>>`?

Abbiamo visto l'uso di `>`, ma esiste un operatore simile `>>` che funziona in modo leggermente diverso. Impareremo le differenze tra questi due operatori stampando alcune stringhe. Possiamo usare il comando `echo` per stampare delle stringhe, ad esempio

```bash
$ echo The echo command prints text
```

```output
The echo command prints text
```

Ora provate i comandi sottostanti per scoprire la differenza tra i due operatori:

```bash
$ echo hello > testfile01.txt
```

e:

```bash
$ echo hello >> testfile02.txt
```

Suggerimento: provate a eseguire ogni comando due volte di seguito e poi esaminate i file di output.

::::::::::::::: solution

## Soluzione

Nel primo esempio con `>`, la stringa 'hello' viene scritta in `testfile01.txt`, ma il file viene sovrascritto ogni volta che si esegue il comando.

Vediamo dal secondo esempio che anche l'operatore `>>` scrive 'hello' in un file (in questo caso `testfile02.txt`), ma aggiunge la stringa al file se questo esiste già (cioè quando lo eseguiamo per la seconda volta).



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Applicazione dei dati

Abbiamo già incontrato il comando `head`, che stampa le righe dall'inizio di un file. il comando `tail` è simile, ma stampa le righe dalla fine di un file.

Considerare il file `shell-lesson-data/exercise-data/animal-counts/animals.csv`. Dopo questi comandi, selezionare la risposta che corrisponde al file `animals-subset.csv`:

```bash
$ head -n 3 animals.csv > animals-subset.csv
$ tail -n 2 animals.csv >> animals-subset.csv
```

1. Le prime tre righe di `animals.csv`
2. le ultime due righe di `animals.csv`
3. Le prime tre righe e le ultime due righe di `animals.csv`
4. La seconda e la terza riga di `animals.csv`

::::::::::::::: solution

## Soluzione

L'opzione 3 è corretta. Affinché l'opzione 1 sia corretta, si deve eseguire solo il comando `head`. Per l'opzione 2 è corretto eseguire solo il comando `tail`. Affinché l'opzione 4 sia corretta, occorre eseguire il pipe dell'output di `head` in `tail -n 2` facendo `head -n 3 animals.csv | tail -n 2 > animals-subset.csv`



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Passaggio dell'output a un altro comando

Nel nostro esempio di ricerca del file con il minor numero di righe, stiamo usando due file intermedi `lengths.txt` e `sorted-lengths.txt` per memorizzare l'output. Questo è un modo confuso di lavorare, perché anche una volta capito cosa fanno `wc`, `sort` e `head`, questi file intermedi rendono difficile capire cosa sta succedendo. Si può semplificare la comprensione eseguendo `sort` e `head` insieme:

```bash
$ sort -n lengths.txt | head -n 1
```

```output
  9  methane.pdb
```

La barra verticale, `|`, tra i due comandi è chiamata **pipe**. Indica alla shell che vogliamo usare l'output del comando a sinistra come input del comando a destra.

Questo ha eliminato la necessità del file `sorted-lengths.txt`.

## Combinazione di più comandi

Nulla ci impedisce di concatenare le pipe consecutivamente. Ad esempio, possiamo inviare l'output di `wc` direttamente a `sort`, e poi inviare l'output risultante a `head`. Questo elimina la necessità di file intermedi.

Inizieremo usando una pipe per inviare l'output di `wc` a `sort`:

```bash
$ wc -l *.pdb | sort -n
```

```output
   9 methane.pdb
  12 ethane.pdb
  15 propane.pdb
  20 cubane.pdb
  21 pentane.pdb
  30 octane.pdb
 107 total
```

Possiamo quindi inviare l'output attraverso un'altra pipe, a `head`, in modo che la pipeline completa diventi:

```bash
$ wc -l *.pdb | sort -n | head -n 1
```

```output
   9  methane.pdb
```

Questo è esattamente come un matematico che annida funzioni come *log(3x)* e dice "il log di tre volte *x*". Nel nostro caso, l'algoritmo è "testa dell'ordinamento del numero di righe di `*.pdb`".

Il reindirizzamento e le pipe utilizzate negli ultimi comandi sono illustrati di seguito:

![](fig/redirects-and-pipes.svg){alt='Redirects and Pipes di diversi comandi: "wc -l \*.pdb" indirizzerà l'output alla shell. "wc -l \*.pdb > lunghezze" dirige l'output al file "lunghezze". "wc -l \*.pdb | sort -n | head -n 1" crea una pipeline in cui l'output del comando "wc" è l'input del comando "sort", l'output del comando "sort" è l'input del comando "head" e l'output del comando "head" è diretto alla shell'}

::::::::::::::::::::::::::::::::::::::: challenge

## Comandi piping insieme

Nella nostra cartella corrente, vogliamo trovare i 3 file che hanno il minor numero di righe. Quale comando elencato di seguito potrebbe funzionare?

1. `wc -l * > sort -n > head -n 3`
2. `wc -l * | sort -n | head -n 1-3`
3. `wc -l * | head -n 3 | sort -n`
4. `wc -l * | sort -n | head -n 3`

::::::::::::::: solution

## Soluzione

L'opzione 4 è la soluzione. Il carattere pipe `|` viene usato per collegare l'uscita di un comando all'ingresso di un altro. il carattere `>` è usato per reindirizzare l'output standard a un file. Provatelo nella cartella `shell-lesson-data/exercise-data/alkanes`!



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Strumenti progettati per funzionare insieme

Questa idea di collegare i programmi tra loro è il motivo per cui Unix ha avuto tanto successo. Invece di creare programmi enormi che cercano di fare molte cose diverse, i programmatori Unix si concentrano sulla creazione di molti strumenti semplici che svolgono bene un lavoro ciascuno e che funzionano bene tra loro. Questo modello di programmazione è chiamato "pipe e filtri". Abbiamo già visto le pipe; un **filtro** è un programma come `wc` o `sort` che trasforma un flusso di input in un flusso di output. Quasi tutti gli strumenti standard di Unix possono funzionare in questo modo. A meno che non venga detto di fare diversamente, essi leggono dallo standard input, fanno qualcosa con ciò che hanno letto e scrivono sullo standard output.

La chiave è che ogni programma che legge righe di testo dallo standard input e scrive righe di testo sullo standard output può essere combinato con ogni altro programma che si comporta in questo modo. Potete *e dovreste* scrivere i vostri programmi in questo modo, in modo che voi e altre persone possiate inserire quei programmi nelle pipe per moltiplicarne la potenza.

::::::::::::::::::::::::::::::::::::::: challenge

## Comprensione della lettura di pipe

Un file chiamato `animals.csv` (nella cartella `shell-lesson-data/exercise-data/animal-counts`) contiene i seguenti dati:

```source
2012-11-05,deer,5
2012-11-05,rabbit,22
2012-11-05,raccoon,7
2012-11-06,rabbit,19
2012-11-06,deer,2
2012-11-06,fox,4
2012-11-07,rabbit,16
2012-11-07,bear,1
```

Quale testo passa attraverso ciascuna delle pipe e il redirect finale nella pipeline sottostante? Si noti che il comando `sort -r` ordina in ordine inverso.

```bash
$ cat animals.csv | head -n 5 | tail -n 3 | sort -r > final.txt
```

Suggerimento: costruite la pipeline un comando alla volta per verificare la vostra comprensione

::::::::::::::: solution

## Soluzione

Il comando `head` estrae le prime 5 righe da `animals.csv`. Poi, le ultime 3 righe vengono estratte dalle precedenti 5 usando il comando `tail`. Con il comando `sort -r` queste 3 righe vengono ordinate in ordine inverso. Infine, l'output viene reindirizzato in un file: `final.txt`. Il contenuto di questo file può essere controllato eseguendo il comando `cat final.txt`. Il file dovrebbe contenere le seguenti righe:

```source
2012-11-06,rabbit,19
2012-11-06,deer,2
2012-11-05,raccoon,7
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Costruzione di un tubo

Per il file `animals.csv` dell'esercizio precedente, considerate il seguente comando:

```bash
$ cut -d , -f 2 animals.csv
```

Il comando `cut` è usato per rimuovere o "tagliare" certe sezioni di ogni riga del file, e `cut` si aspetta che le righe siano separate in colonne da un carattere <kbd>Tab</kbd>. Un carattere usato in questo modo è chiamato **delimitatore**. Nell'esempio precedente si usa l'opzione `-d` per specificare la virgola come carattere delimitatore. Abbiamo anche usato l'opzione `-f` per specificare che vogliamo estrarre il secondo campo (colonna). Si ottiene così il seguente risultato:

```output
deer
rabbit
raccoon
rabbit
deer
fox
rabbit
bear
```

Il comando `uniq` filtra le righe adiacenti corrispondenti in un file. Come si potrebbe estendere questa pipeline (usando `uniq` e un altro comando) per scoprire quali animali contiene il file (senza duplicati nei loro nomi)?

::::::::::::::: solution

## Soluzione

```bash
$ cut -d , -f 2 animals.csv | sort | uniq
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Quale tubo?

Il file `animals.csv` contiene 8 righe di dati formattati come segue:

```output
2012-11-05,deer,5
2012-11-05,rabbit,22
2012-11-05,raccoon,7
2012-11-06,rabbit,19
...
```

Il comando `uniq` ha un'opzione `-c` che fornisce un conteggio del numero di volte in cui una riga è presente nel suo input. Supponendo che la vostra directory corrente sia `shell-lesson-data/exercise-data/animal-counts`, quale comando usereste per produrre una tabella che mostri il numero totale di ogni tipo di animale nel file?

1. `sort animals.csv | uniq -c`
2. `sort -t, -k2,2 animals.csv | uniq -c`
3. `cut -d, -f 2 animals.csv | uniq -c`
4. `cut -d, -f 2 animals.csv | sort | uniq -c`
5. `cut -d, -f 2 animals.csv | sort | uniq -c | wc -l`

::::::::::::::: solution

## Soluzione

L'opzione 4. è la risposta corretta. Se avete difficoltà a capire perché, provate a eseguire i comandi o le sottosezioni delle pipeline (assicuratevi di essere nella cartella `shell-lesson-data/exercise-data/animal-counts`).



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Pipeline di Nelle: Controllo dei file

Nelle ha fatto passare i suoi campioni attraverso le macchine di analisi e ha creato 17 file nella cartella `north-pacific-gyre` descritta in precedenza. Per un rapido controllo, partendo dalla cartella `shell-lesson-data`, Nelle digita:

```bash
$ cd north-pacific-gyre
$ wc -l *.txt
```

l'output è costituito da 18 righe che assomigliano a queste:

```output
300 NENE01729A.txt
300 NENE01729B.txt
300 NENE01736A.txt
300 NENE01751A.txt
300 NENE01751B.txt
300 NENE01812A.txt
... ...
```

Ora digita questo:

```bash
$ wc -l *.txt | sort -n | head -n 5
```

```output
 240 NENE02018B.txt
 300 NENE01729A.txt
 300 NENE01729B.txt
 300 NENE01736A.txt
 300 NENE01751A.txt
```

Ops: uno dei file è 60 righe più corto degli altri. Quando torna indietro e controlla, vede che ha fatto quel saggio alle 8:00 di lunedì mattina --- probabilmente qualcuno ha usato la macchina nel fine settimana e lei ha dimenticato di resettarla. Prima di rieseguire il campione, controlla se qualche file ha troppi dati:

```bash
$ wc -l *.txt | sort -n | tail -n 5
```

```output
 300 NENE02040B.txt
 300 NENE02040Z.txt
 300 NENE02043A.txt
 300 NENE02043B.txt
5040 total
```

I numeri sembrano buoni, ma cosa ci fa quella "Z" nella terzultima riga? Tutti i suoi campioni dovrebbero essere contrassegnati con 'A' o 'B'; per convenzione, il suo laboratorio usa la 'Z' per indicare i campioni con informazioni mancanti. Per trovare altri campioni simili, fa così:

```bash
$ ls *Z.txt
```

```output
NENE01971Z.txt    NENE02040Z.txt
```

Quando controlla il registro sul suo portatile, non c'è alcuna profondità registrata per nessuno dei due campioni. Poiché è troppo tardi per ottenere le informazioni in altro modo, deve escludere questi due file dalla sua analisi. Potrebbe eliminarli usando `rm`, ma in realtà ci sono analisi che potrebbe fare in seguito in cui la profondità non è importante, quindi dovrà fare attenzione a selezionare i file usando le espressioni jolly `NENE*A.txt NENE*B.txt`.

::::::::::::::::::::::::::::::::::::::: challenge

## Rimozione dei file non necessari

Supponiamo di voler cancellare i file dei dati elaborati e di voler conservare solo i file grezzi e lo script di elaborazione per risparmiare spazio. I file grezzi terminano in `.dat` e quelli elaborati in `.txt`. Quale delle seguenti operazioni rimuoverà tutti i file di dati elaborati e *solo* i file di dati elaborati?

1. `rm ?.txt`
2. `rm *.txt`
3. `rm * .txt`
4. `rm *.*`

::::::::::::::: solution

## Soluzione

1. Questo rimuove i file `.txt` con nomi di un solo carattere
2. Questa è la risposta corretta
3. La shell espanderebbe `*` per far corrispondere tutto ciò che si trova nella cartella corrente, quindi il comando cercherebbe di rimuovere tutti i file corrispondenti e un file aggiuntivo chiamato `.txt`
4. La shell espande `*.*` per far corrispondere tutti i nomi di file contenenti almeno un `.`, compresi i file elaborati (`.txt`) *e* i file grezzi (`.dat`)

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::: keypoints

- `wc` conta righe, parole e caratteri nei suoi input.
- `cat` mostra il contenuto dei suoi input.
- `sort` ordina i suoi input.
- `head` visualizza le prime 10 righe del suo input per impostazione predefinita, senza ulteriori argomenti.
- `tail` visualizza le ultime 10 righe del suo input per impostazione predefinita, senza ulteriori argomenti.
- `command > [file]` reindirizza l'output di un comando a un file (sovrascrivendo qualsiasi contenuto esistente).
- `command >> [file]` aggiunge l'output di un comando a un file.
- `[first] | [second]` è una pipeline: l'output del primo comando viene usato come input del secondo.
- Il modo migliore per usare la shell è usare le pipe per combinare semplici programmi monouso (filtri).

::::::::::::::::::::::::::::::::::::::::::::::::::



