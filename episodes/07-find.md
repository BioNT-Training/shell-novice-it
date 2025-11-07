---
title: Trovare le cose
teaching: 25
exercises: 20
---


::::::::::::::::::::::::::::::::::::::: objectives

- Usare `grep` per selezionare righe da file di testo che corrispondono a modelli semplici.
- Usare `find` per trovare file e cartelle i cui nomi corrispondono a schemi semplici.
- Utilizzare l'output di un comando come argomento della riga di comando di un altro comando.
- Spiegare cosa si intende per file "di testo" e "binari" e perché molti strumenti comuni non gestiscono bene questi ultimi.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come posso trovare i file?
- Come posso trovare le cose nei file?

::::::::::::::::::::::::::::::::::::::::::::::::::

Allo stesso modo in cui molti di noi usano 'Google' come verbo che significa 'trovare', i programmatori Unix usano spesso la parola 'grep'. 'grep' è una contrazione di 'global/regular expression/print', una sequenza comune di operazioni nei primi editor di testo Unix. È anche il nome di un programma a riga di comando molto utile.

`grep` trova e stampa le righe dei file che corrispondono a uno schema. Per i nostri esempi, useremo un file che contiene tre haiku tratti da un [concorso 1998](https://web.archive.org/web/19991201042211/http://salon.com/21st/chal/1998/01/26chal.html) della rivista *Salon* (merito degli autori Bill Torcaso, Howard Korder e Margaret Segall, rispettivamente. Si vedano i messaggi di errore Haiku archiviati [Pagina 1](https://web.archive.org/web/20000310061355/http://www.salon.com/21st/chal/1998/02/10chal2.html) e [Pagina 2](https://web.archive.org/web/20000229135138/http://www.salon.com/21st/chal/1998/02/10chal3.html)). Per questa serie di esempi, lavoreremo nella sottocartella della scrittura:

```bash
$ cd
$ cd Desktop/shell-lesson-data/exercise-data/writing
$ cat haiku.txt
```

```output
The Tao that is seen
Is not the true Tao, until
You bring fresh toner.

With searching comes loss
and the presence of absence:
"My Thesis" not found.

Yesterday it worked
Today it is not working
Software is like that.
```

Troviamo le righe che contengono la parola "non":

```bash
$ grep not haiku.txt
```

```output
Is not the true Tao, until
"My Thesis" not found
Today it is not working
```

Qui, `not` è lo schema che stiamo cercando. Il comando grep cerca nel file le corrispondenze con lo schema specificato. Per utilizzarlo, digitare `grep`, quindi lo schema che si vuole cercare e infine il nome del file (o dei file) in cui si vuole effettuare la ricerca.

L'output è costituito dalle tre righe del file che contengono le lettere "non".

Per impostazione predefinita, grep cerca un modello in modo sensibile alle maiuscole e alle minuscole. Inoltre, il modello di ricerca selezionato non deve necessariamente formare una parola completa, come vedremo nel prossimo esempio.

Cerchiamo il modello: 'Il'.

```bash
$ grep The haiku.txt
```

```output
The Tao that is seen
"My Thesis" not found.
```

Questa volta vengono prodotte due righe che includono le lettere "The", una delle quali conteneva il nostro modello di ricerca all'interno di una parola più grande, "Thesis".

Per limitare le corrispondenze alle righe contenenti la parola 'The' da sola, si può dare a `grep` l'opzione `-w`. Questo limiterà le corrispondenze ai confini della parola.

Più avanti in questa lezione vedremo anche come modificare il comportamento di ricerca di grep rispetto alla sensibilità alle maiuscole.

```bash
$ grep -w The haiku.txt
```

```output
The Tao that is seen
```

Si noti che un "confine di parola" include l'inizio e la fine di una riga, quindi non solo le lettere circondate da spazi. A volte non si vuole cercare una singola parola, ma una frase. È possibile farlo anche con `grep`, mettendo la frase tra virgolette.

```bash
$ grep -w "is not" haiku.txt
```

```output
Today it is not working
```

Abbiamo visto che non è necessario mettere le virgolette intorno alle singole parole, ma è utile usare le virgolette quando si cercano più parole. Inoltre, aiuta a distinguere più facilmente tra il termine o la frase di ricerca e il file ricercato. Negli altri esempi utilizzeremo le virgolette.

Un'altra opzione utile è `-n`, che numera le righe corrispondenti:

```bash
$ grep -n "it" haiku.txt
```

```output
5:With searching comes loss
9:Yesterday it worked
10:Today it is not working
```

Qui possiamo vedere che le righe 5, 9 e 10 contengono le lettere "it".

Possiamo combinare le opzioni (cioè i flag) come facciamo con altri comandi Unix. Per esempio, cerchiamo di trovare le righe che contengono la parola "il". Possiamo combinare l'opzione `-w` per trovare le righe che contengono la parola 'the' e `-n` per numerare le righe che corrispondono:

```bash
$ grep -n -w "the" haiku.txt
```

```output
2:Is not the true Tao, until
6:and the presence of absence:
```

Ora vogliamo usare l'opzione `-i` per rendere la nostra ricerca insensibile alle maiuscole e alle minuscole:

```bash
$ grep -n -w -i "the" haiku.txt
```

```output
1:The Tao that is seen
2:Is not the true Tao, until
6:and the presence of absence:
```

Ora vogliamo usare l'opzione `-v` per invertire la nostra ricerca, cioè vogliamo produrre le righe che non contengono la parola 'the'.

```bash
$ grep -n -w -v "the" haiku.txt
```

```output
1:The Tao that is seen
3:You bring fresh toner.
4:
5:With searching comes loss
7:"My Thesis" not found.
8:
9:Yesterday it worked
10:Today it is not working
11:Software is like that.
```

Se si usa l'opzione `-r` (ricorsiva), `grep` può cercare un modello in modo ricorsivo in un insieme di file in sottodirectory.

Cerchiamo ricorsivamente `Yesterday` nella directory `shell-lesson-data/exercise-data/writing`:

```bash
$ grep -r Yesterday .
```

```output
./LittleWomen.txt:"Yesterday, when Aunt was asleep and I was trying to be as still as a
./LittleWomen.txt:Yesterday at dinner, when an Austrian officer stared at us and then
./LittleWomen.txt:Yesterday was a quiet day spent in teaching, sewing, and writing in my
./haiku.txt:Yesterday it worked
```

`grep` ha molte altre opzioni. Per scoprire quali sono, si può digitare:

```bash
$ grep --help
```

```output
Usage: grep [OPTION]... PATTERN [FILE]...
Search for PATTERN in each FILE or standard input.
PATTERN is, by default, a basic regular expression (BRE).
Example: grep -i 'hello world' menu.h main.c

Regexp selection and interpretation:
  -E, --extended-regexp     PATTERN is an extended regular expression (ERE)
  -F, --fixed-strings       PATTERN is a set of newline-separated fixed strings
  -G, --basic-regexp        PATTERN is a basic regular expression (BRE)
  -P, --perl-regexp         PATTERN is a Perl regular expression
  -e, --regexp=PATTERN      use PATTERN for matching
  -f, --file=FILE           obtain PATTERN from FILE
  -i, --ignore-case         ignore case distinctions
  -w, --word-regexp         force PATTERN to match only whole words
  -x, --line-regexp         force PATTERN to match only whole lines
  -z, --null-data           a data line ends in 0 byte, not newline

Miscellaneous:
...        ...        ...
```

::::::::::::::::::::::::::::::::::::::: challenge

## Uso di `grep`

Quale comando produrrebbe il seguente output:

```output
and the presence of absence:
```

1. `grep "of" haiku.txt`
2. `grep -E "of" haiku.txt`
3. `grep -w "of" haiku.txt`
4. `grep -i "of" haiku.txt`

::::::::::::::: solution

## Soluzione

La risposta corretta è 3, perché l'opzione `-w` cerca solo le corrispondenze con le parole intere. Le altre opzioni corrispondono anche a "di" quando è parte di un'altra parola.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Caratteri jolly

la vera potenza di `grep` non deriva dalle sue opzioni, ma dal fatto che i pattern possono includere caratteri jolly. (Il nome tecnico di queste espressioni è **espressioni regolari**, che è il significato di "re" in "grep") Le espressioni regolari sono complesse e potenti; se volete fare ricerche complesse, consultate la lezione su [il nostro sito web](https://librarycarpentry.org/lc-data-intro/01-regular-expressions.html). Come assaggio, possiamo trovare le righe che hanno una 'o' in seconda posizione come questa:

```bash
$ grep -E "^.o" haiku.txt
```

```output
You bring fresh toner.
Today it is not working
Software is like that.
```

Usiamo l'opzione `-E` e mettiamo il pattern tra virgolette per evitare che la shell cerchi di interpretarlo. (Se il pattern contenesse un `*`, per esempio, la shell cercherebbe di espanderlo prima di eseguire `grep`) Il `^` nel pattern fissa la corrispondenza all'inizio della riga. La `.` corrisponde a un singolo carattere (proprio come la `?` nella shell), mentre la `o` corrisponde a una "o" vera e propria.


::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Tracciare una specie

Leah ha diverse centinaia di file di dati salvati in una directory, ognuno dei quali è formattato come segue:

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

Vuole scrivere uno script di shell che prenda una specie come primo argomento della riga di comando e una directory come secondo argomento. Lo script dovrebbe restituire un file chiamato `<species>.txt` contenente un elenco di date e il numero di specie osservate in ciascuna data. Ad esempio, utilizzando i dati mostrati sopra, `rabbit.txt` conterrebbe:

```source
2012-11-05,22
2012-11-06,19
2012-11-07,16
```

Di seguito, ogni riga contiene un singolo comando, o pipe. Organizzare la loro sequenza in un comando per raggiungere l'obiettivo di Leah:

```bash
cut -d : -f 2
>
|
grep -w $1 -r $2
|
$1.txt
cut -d , -f 1,3
```

Suggerimento: usare `man grep` per cercare come grepare il testo in modo ricorsivo in una cartella e `man cut` per selezionare più di un campo in una riga.

Un esempio di tale file è fornito in `shell-lesson-data/exercise-data/animal-counts/animals.csv`

::::::::::::::: solution

## Soluzione

```source
grep -w $1 -r $2 | cut -d : -f 2 | cut -d , -f 1,3 > $1.txt
```

In realtà, è possibile scambiare l'ordine dei due comandi di taglio e funziona ancora. Alla riga di comando, provate a cambiare l'ordine dei comandi di taglio e date un'occhiata all'output di ogni passaggio per capire perché è così.

Lo script precedente viene chiamato in questo modo:

```bash
$ bash count-species.sh bear .
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Piccole donne

Tu e la tua amica, dopo aver appena finito di leggere *Piccole donne* di Louisa May Alcott, state discutendo. Delle quattro sorelle del libro, Jo, Meg, Beth e Amy, la vostra amica pensa che Jo sia la più citata. Voi, invece, siete certi che si tratti di Amy. Fortunatamente si dispone di un file `LittleWomen.txt` contenente il testo completo del romanzo (`shell-lesson-data/exercise-data/writing/LittleWomen.txt`). Utilizzando un ciclo `for`, come si potrebbe tabulare il numero di volte in cui ciascuna delle quattro sorelle viene menzionata?

Suggerimento: una soluzione potrebbe utilizzare i comandi `grep` e `wc` e un `|`, mentre un'altra potrebbe utilizzare le opzioni `grep`. Spesso esiste più di un modo per risolvere un compito di programmazione, quindi una particolare soluzione viene solitamente scelta in base a una combinazione di risultati corretti, eleganza, leggibilità e velocità.

::::::::::::::: solution

## Soluzioni

```source
for sis in Jo Meg Beth Amy
do
    echo $sis:
    grep -ow $sis LittleWomen.txt | wc -l
done
```

Soluzione alternativa, leggermente inferiore:

```source
for sis in Jo Meg Beth Amy
do
    echo $sis:
    grep -ocw $sis LittleWomen.txt
done
```

Questa soluzione è inferiore perché `grep -c` riporta solo il numero di righe corrispondenti. Il numero totale di corrispondenze riportato da questo metodo sarà inferiore se c'è più di una corrispondenza per riga.

Gli osservatori più attenti avranno notato che i nomi dei personaggi a volte appaiono in tutte le maiuscole nei titoli dei capitoli (per esempio, "MEG VA ALLA FIERA DELLA VANITÀ"). Se si volesse contare anche questi, si potrebbe aggiungere l'opzione `-i` per l'insensibilità alle maiuscole e minuscole (anche se in questo caso non influisce sulla risposta a quale sorella è menzionata più frequentemente).



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

Mentre `grep` trova le righe nei file, il comando `find` trova i file stessi. Anche in questo caso, ha molte opzioni; per mostrare come funzionano le più semplici, useremo l'albero `shell-lesson-data/exercise-data` mostrato di seguito.

```output
.
├── animal-counts/
│   └── animals.csv
├── creatures/
│   ├── basilisk.dat
│   ├── minotaur.dat
│   └── unicorn.dat
├── numbers.txt
├── alkanes/
│   ├── cubane.pdb
│   ├── ethane.pdb
│   ├── methane.pdb
│   ├── octane.pdb
│   ├── pentane.pdb
│   └── propane.pdb
└── writing/
    ├── haiku.txt
    └── LittleWomen.txt
```

La cartella `exercise-data` contiene un file, `numbers.txt` e quattro cartelle: `animal-counts`, `creatures`, `alkanes` e `writing` contenenti vari file.

Per il nostro primo comando, eseguiamo `find .` (ricordate di eseguire questo comando dalla cartella `shell-lesson-data/exercise-data`).

```bash
$ find .
```

```output
.
./writing
./writing/LittleWomen.txt
./writing/haiku.txt
./creatures
./creatures/basilisk.dat
./creatures/unicorn.dat
./creatures/minotaur.dat
./animal-counts
./animal-counts/animals.csv
./numbers.txt
./alkanes
./alkanes/ethane.pdb
./alkanes/propane.pdb
./alkanes/octane.pdb
./alkanes/pentane.pdb
./alkanes/methane.pdb
./alkanes/cubane.pdb
```

Come sempre, `.` da solo significa la cartella di lavoro corrente, che è il punto da cui vogliamo iniziare la nostra ricerca. l'output di `find` è il nome di ogni file **e** cartella sotto la cartella di lavoro corrente. All'inizio può sembrare inutile, ma `find` ha molte opzioni per filtrare l'output e in questa lezione ne scopriremo alcune.

La prima opzione del nostro elenco è `-type d` che significa "cose che sono directory". Certamente, l'output di `find` è il nome delle cinque cartelle (inclusa `.`):

```bash
$ find . -type d
```

```output
.
./writing
./creatures
./animal-counts
./alkanes
```

Si noti che gli oggetti trovati da `find` non sono elencati in un ordine particolare. Se si cambia `-type d` con `-type f`, si ottiene invece un elenco di tutti i file:

```bash
$ find . -type f
```

```output
./writing/LittleWomen.txt
./writing/haiku.txt
./creatures/basilisk.dat
./creatures/unicorn.dat
./creatures/minotaur.dat
./animal-counts/animals.csv
./numbers.txt
./alkanes/ethane.pdb
./alkanes/propane.pdb
./alkanes/octane.pdb
./alkanes/pentane.pdb
./alkanes/methane.pdb
./alkanes/cubane.pdb
```

Ora proviamo a fare una corrispondenza per nome:

```bash
$ find . -name *.txt
```

```output
./numbers.txt
```

Ci si aspettava che trovasse tutti i file di testo, ma stampa solo `./numbers.txt`. Il problema è che la shell espande i caratteri jolly come `*` *prima* dell'esecuzione dei comandi. Poiché `*.txt` nella cartella corrente si espande a `./numbers.txt`, il comando effettivamente eseguito è stato:

```bash
$ find . -name numbers.txt
```

`find` ha fatto quello che abbiamo chiesto; abbiamo solo chiesto la cosa sbagliata.

Per ottenere ciò che vogliamo, facciamo come con `grep`: mettiamo `*.txt` tra virgolette per evitare che la shell espanda il carattere jolly `*`. In questo modo, `find` ottiene effettivamente il pattern `*.txt`, non il nome del file espanso `numbers.txt`:

```bash
$ find . -name "*.txt"
```

```output
./writing/LittleWomen.txt
./writing/haiku.txt
./numbers.txt
```

::::::::::::::::::::::::::::::::::::::::: callout

## Elenco vs. ricerca

`ls` e `find` possono fare cose simili con le giuste opzioni, ma in circostanze normali, `ls` elenca tutto ciò che può, mentre `find` cerca cose con certe proprietà e le mostra.


::::::::::::::::::::::::::::::::::::::::::::::::::

Come abbiamo detto prima, la potenza della riga di comando sta nel combinare gli strumenti. Abbiamo visto come farlo con le pipe; vediamo un'altra tecnica. Come abbiamo appena visto, `find . -name "*.txt"` ci fornisce un elenco di tutti i file di testo presenti nella cartella corrente o al di sotto di essa. Come possiamo combinarlo con `wc -l` per contare le righe in tutti questi file?

Il modo più semplice è quello di inserire il comando `find` all'interno di `$()`:

```bash
$ wc -l $(find . -name "*.txt")
```

```output
  21022 ./writing/LittleWomen.txt
     11 ./writing/haiku.txt
      5 ./numbers.txt
  21038 total
```

Quando la shell esegue questo comando, la prima cosa che fa è eseguire qualsiasi cosa si trovi all'interno della `$()`. Quindi sostituisce l'espressione `$()` con l'output di quel comando. Poiché l'output di `find` è costituito dai tre nomi di file `./writing/LittleWomen.txt`, `./writing/haiku.txt` e `./numbers.txt`, la shell costruisce il comando:

```bash
$ wc -l ./writing/LittleWomen.txt ./writing/haiku.txt ./numbers.txt
```

che è quello che volevamo. Questa espansione è esattamente ciò che fa la shell quando espande i caratteri jolly come `*` e `?`, ma ci permette di usare qualsiasi comando come nostro 'carattere jolly'.

È molto comune usare `find` e `grep` insieme. Il primo trova i file che corrispondono a uno schema; il secondo cerca le righe all'interno di quei file che corrispondono a un altro schema. Qui, per esempio, possiamo trovare i file txt che contengono la parola "searching" cercando la stringa 'searching' in tutti i file `.txt` nella directory corrente:

```bash
$ grep "searching" $(find . -name "*.txt")
```

```output
./writing/LittleWomen.txt:sitting on the top step, affected to be searching for her book, but was
./writing/haiku.txt:With searching comes loss
```

::::::::::::::::::::::::::::::::::::::: challenge

## Corrispondenza e sottrazione

L'opzione `-v` di `grep` inverte la corrispondenza dei pattern, in modo che vengano stampate solo le righe che *non* corrispondono al pattern. In base a ciò, quale dei seguenti comandi troverà tutti i file .dat in `creatures` tranne che in `unicorn.dat`? Dopo aver pensato alla risposta, si possono testare i comandi nella directory `shell-lesson-data/exercise-data`.

1. `find creatures -name "*.dat" | grep -v unicorn`
2. `find creatures -name *.dat | grep -v unicorn`
3. `grep -v "unicorn" $(find creatures -name "*.dat")`
4. Nessuno dei precedenti.

::::::::::::::: solution

## Soluzione

L'opzione 1 è corretta. Mettere l'espressione di corrispondenza tra virgolette impedisce alla shell di espanderla, quindi viene passata al comando `find`.

L'opzione 2 funziona anche in questo caso, perché la shell tenta di espandere `*.dat` ma non ci sono file `*.dat` nella cartella corrente, quindi l'espressione jolly viene passata a `find`. L'abbiamo incontrato per la prima volta in [episodio 3] (03-create.md).

L'opzione 3 non è corretta perché cerca nel contenuto dei file le righe che non corrispondono a "unicorno", anziché cercare nei nomi dei file.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## File binari

Ci siamo concentrati esclusivamente sulla ricerca di modelli nei file di testo. Cosa succede se i dati sono archiviati come immagini, in database o in altri formati?

Una manciata di strumenti estende `grep` per gestire alcuni formati diversi dal testo. Ma un approccio più generalizzabile è quello di convertire i dati in testo o di estrarre gli elementi simili al testo dai dati. Da un lato, questo rende le cose semplici facili da fare. D'altra parte, le cose complesse sono di solito impossibili. Per esempio, è abbastanza facile scrivere un programma che estragga le dimensioni X e Y da file di immagini per giocare con `grep`, ma come si potrebbe scrivere qualcosa per trovare valori in un foglio di calcolo le cui celle contengono formule?

Un'ultima opzione è riconoscere che la shell e l'elaborazione del testo hanno i loro limiti e utilizzare un altro linguaggio di programmazione. Quando arriva il momento di farlo, non siate troppo duri con la shell. Molti linguaggi di programmazione moderni hanno preso in prestito molte idee da essa, e l'imitazione è anche la forma più sincera di lode.


::::::::::::::::::::::::::::::::::::::::::::::::::

La shell Unix è più vecchia della maggior parte delle persone che la usano. È sopravvissuta così a lungo perché è uno degli ambienti di programmazione più produttivi mai creati, forse addirittura il più produttivo. La sua sintassi può essere criptica, ma chi la padroneggia può sperimentare diversi comandi in modo interattivo e poi usare ciò che ha imparato per automatizzare il proprio lavoro. Le interfacce utente grafiche possono essere più facili da usare all'inizio, ma una volta imparate, la produttività della shell è imbattibile. E come scrisse Alfred North Whitehead nel 1911, "la civiltà progredisce ampliando il numero di operazioni importanti che possiamo eseguire senza pensarci"

::::::::::::::::::::::::::::::::::::::: challenge

## `find` Comprensione della lettura del gasdotto

Scrivere un breve commento esplicativo per il seguente script di shell:

```bash
wc -l $(find . -name "*.dat") | sort -n
```

::::::::::::::: solution

## Soluzione

1. Trova tutti i file con estensione `.dat` ricorsivamente dalla cartella corrente
2. Conta il numero di righe contenute in ciascuno di questi file
3. Ordina numericamente l'output del passo 2

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::: keypoints

- `find` trova file con proprietà specifiche che corrispondono ai modelli.
- `grep` seleziona le righe dei file che corrispondono ai modelli.
- `--help` è un'opzione supportata da molti comandi bash e programmi che possono essere eseguiti da Bash, per visualizzare ulteriori informazioni sull'uso di tali comandi o programmi.
- `man [command]` visualizza la pagina del manuale per un determinato comando.
- `$([command])` inserisce l'output di un comando al suo posto.

::::::::::::::::::::::::::::::::::::::::::::::::::



