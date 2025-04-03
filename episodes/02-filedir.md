---
title: Navigazione tra file e directory
teaching: 30
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Spiegare le somiglianze e le differenze tra un file e una directory.
- Traduce un percorso assoluto in un percorso relativo e viceversa.
- Costruire percorsi assoluti e relativi che identificano file e directory specifici.
- Usare opzioni e argomenti per modificare il comportamento di un comando di shell.
- Dimostrare l'uso del completamento a schede e spiegarne i vantaggi.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come posso muovermi nel mio computer?
- Come posso vedere quali file e directory ho?
- Come posso specificare la posizione di un file o di una directory sul mio computer?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: instructor

L'introduzione e la navigazione del filesystem nella shell (trattata nella sezione [Navigare tra file e directory](02-filedir.md)) può creare confusione. Si possono tenere aperti fianco a fianco sia il terminale che il file explorer della GUI, in modo che gli studenti possano vedere il contenuto e la struttura dei file mentre usano il terminale per navigare nel sistema.

::::::::::::::::::::::::::::::::::::::::::::::::::

La parte del sistema operativo responsabile della gestione dei file e delle directory si chiama **file system**. Organizza i dati in file, che contengono informazioni, e directory (chiamate anche "cartelle"), che contengono file o altre directory.

Diversi comandi sono usati frequentemente per creare, ispezionare, rinominare e cancellare file e directory. Per iniziare a esplorarli, andiamo alla nostra finestra di shell aperta.

Per prima cosa, scopriamo dove ci troviamo eseguendo un comando chiamato `pwd` (che sta per 'print working directory'). Le directory sono come *luoghi*: in qualsiasi momento, mentre si utilizza la shell, ci si trova esattamente in un luogo chiamato **current working directory**. I comandi leggono e scrivono i file nella directory di lavoro corrente, cioè "qui", quindi è importante sapere dove ci si trova prima di eseguire un comando. `pwd` mostra la posizione in cui ci si trova:

```bash
$ pwd
```

```output
/Users/nelle
```

Qui, la risposta del computer è `/Users/nelle`, che è la **home directory** di Nelle:

::::::::::::::::::::::::::::::::::::::::: callout

## Variazione della directory principale

Il percorso della home directory ha un aspetto diverso nei diversi sistemi operativi. Su Linux, può apparire come `/home/nelle`, mentre su Windows sarà simile a `C:\Documents and Settings\nelle` o `C:\Users\nelle`. (Negli esempi futuri, abbiamo utilizzato l'output del Mac come predefinito; l'output di Linux e Windows può differire leggermente, ma dovrebbe essere generalmente simile.

Si suppone inoltre che il comando `pwd` restituisca la home directory dell'utente. Se `pwd` restituisce qualcosa di diverso, potrebbe essere necessario navigare lì usando `cd` o alcuni comandi di questa lezione non funzioneranno come scritto. Vedere [Esplorare altre directory](#esplorare-altre-directory) per maggiori dettagli sul comando `cd`.


::::::::::::::::::::::::::::::::::::::::::::::::::

Per capire che cos'è una "home directory", diamo un'occhiata a come è organizzato il file system nel suo complesso. Per il bene di questo esempio, illustreremo il filesystem del computer della nostra scienziata Nelle. Dopo questa illustrazione, imparerete i comandi per esplorare il vostro filesystem, che sarà costruito in modo simile, ma non esattamente identico.

Sul computer di Nelle, il filesystem ha questo aspetto:

![](fig/filesystem.svg){alt='Il file system è costituito da una directory principale che contiene sottodirectory intitolate bin, data, users e tmp'}

Il filesystem ha l'aspetto di un albero capovolto. La directory più in alto è la **root directory** che contiene tutto il resto. Ci si riferisce ad essa usando un carattere slash, `/`, da solo; questo carattere è lo slash iniziale di `/Users/nelle`.

all'interno di questa directory ci sono diverse altre directory: `bin` (dove sono memorizzati alcuni programmi integrati), `data` (per i file di dati vari), `Users` (dove si trovano le directory personali degli utenti), `tmp` (per i file temporanei che non devono essere memorizzati a lungo) e così via.

Sappiamo che la nostra directory di lavoro corrente `/Users/nelle` è memorizzata all'interno di `/Users` perché `/Users` è la prima parte del suo nome. Allo stesso modo, sappiamo che `/Users` è memorizzata nella directory principale `/` perché il suo nome inizia con `/`.

::::::::::::::::::::::::::::::::::::::::: callout

## Slash

Si noti che il carattere `/` ha due significati. Quando compare davanti al nome di un file o di una directory, si riferisce alla directory principale. Quando appare *all'interno* di un percorso, è solo un separatore.


::::::::::::::::::::::::::::::::::::::::::::::::::

Sotto `/Users`, troviamo una directory per ogni utente con un account sulla macchina di Nelle, i suoi colleghi *imhotep* e *larry*.

![](fig/home-directories.svg){alt='Come altre directory, le directory home sono sottodirectory sotto "/Users", come "/Users/imhotep", "/Users/larry" o "/Users/nelle"'}

I file dell'utente *imhotep* sono memorizzati in `/Users/imhotep`, quelli dell'utente *larry* in `/Users/larry` e quelli di Nelle in `/Users/nelle`. Nelle è l'utente degli esempi; pertanto, la nostra home directory è `/Users/nelle`. In genere, quando si apre un nuovo prompt dei comandi, all'inizio ci si trova nella propria home directory.

Ora impariamo il comando che ci permetterà di vedere il contenuto del nostro filesystem. Possiamo vedere cosa c'è nella nostra home directory eseguendo `ls`:

```bash
$ ls
```

```output
Applications Documents    Library      Music        Public
Desktop      Downloads    Movies       Pictures
```

(Anche in questo caso, i risultati possono essere leggermente diversi a seconda del sistema operativo e di come è stato personalizzato il filesystem)

`ls` stampa i nomi dei file e delle directory nella directory corrente. È possibile rendere il suo output più comprensibile utilizzando l'opzione `-F` **che indica a `ls` di classificare l'output aggiungendo un marcatore ai nomi dei file e delle directory per indicare di cosa si tratta:

- il trattino `/` indica che si tratta di una directory
- `@` indica un link
- `*` indica un eseguibile

A seconda delle impostazioni predefinite della shell, questa potrebbe anche utilizzare dei colori per indicare se ogni voce è un file o una directory.

```bash
$ ls -F
```

```output
Applications/ Documents/    Library/      Music/        Public/
Desktop/      Downloads/    Movies/       Pictures/
```

Qui possiamo vedere che la directory home contiene solo **sottodirectory**. Tutti i nomi nell'output che non hanno un simbolo di classificazione sono **file** nella directory di lavoro corrente.

::::::::::::::::::::::::::::::::::::::::: callout

## Cancellazione del terminale

Se lo schermo è troppo ingombro, si può cancellare il terminale con il comando `clear`. È comunque possibile accedere ai comandi precedenti usando <kbd>↑</kbd> e <kbd>↓</kbd> per spostarsi riga per riga, oppure scorrendo il terminale.


::::::::::::::::::::::::::::::::::::::::::::::::::

### Ottenere aiuto

`ls` ha molte altre **opzioni**. Ci sono due modi comuni per scoprire come usare un comando e quali opzioni accetta --- **a seconda del vostro ambiente, potreste scoprire che solo uno di questi modi funziona:**

1. possiamo passare un'opzione `--help` a qualsiasi comando (disponibile su Linux e Git Bash), ad esempio:

  ```bash
  $ ls --help
  ```

2. possiamo leggere il suo manuale con `man` (disponibile su Linux e macOS):

  ```bash
  $ man ls
  ```

descriveremo entrambi i modi in seguito.

::::::::::::::::::::::::::::::::::::::::: callout

## Guida per i comandi incorporati

Alcuni comandi sono integrati nella shell Bash, anziché esistere come programmi separati nel filesystem. Un esempio è il comando `cd` (cambio di directory). Se si riceve un messaggio come `No manual entry for cd`, provare invece `help cd`. Il comando `help` è il modo per ottenere informazioni sull'uso di [Bash built-ins](https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins.html).


::::::::::::::::::::::::::::::::::::::::::::::::::

#### L'opzione `--help` è stata utilizzata per elencare i contenuti della directory di lavoro corrente

La maggior parte dei comandi di bash e dei programmi scritti per essere eseguiti all'interno di bash supportano un'opzione `--help` che mostra ulteriori informazioni su come utilizzare il comando o il programma.

```bash
$ ls --help
```

```output
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if neither -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options, too.
  -a, --all                  do not ignore entries starting with .
  -A, --almost-all           do not list implied . and ..
      --author               with -l, print the author of each file
  -b, --escape               print C-style escapes for nongraphic characters
      --block-size=SIZE      scale sizes by SIZE before printing them; e.g.,
                               '--block-size=M' prints sizes in units of
                               1,048,576 bytes; see SIZE format below
  -B, --ignore-backups       do not list implied entries ending with ~
  -c                         with -lt: sort by, and show, ctime (time of last
                               modification of file status information);
                               with -l: show ctime and sort by name;
                               otherwise: sort by ctime, newest first
  -C                         list entries by columns
      --color[=WHEN]         colorize the output; WHEN can be 'always' (default
                               if omitted), 'auto', or 'never'; more info below
  -d, --directory            list directories themselves, not their contents
  -D, --dired                generate output designed for Emacs' dired mode
  -f                         do not sort, enable -aU, disable -ls --color
  -F, --classify             append indicator (one of */=>@|) to entries
...        ...        ...
```

::::::::::::::::::::::::::::::::::::::::: callout

### Quando usare le opzioni brevi o lunghe
Quando le opzioni esistono sia come opzioni brevi che lunghe:

- Usare l'opzione breve quando si digitano comandi direttamente nella shell per ridurre al minimo la pressione dei tasti e svolgere più rapidamente il proprio compito.
- Usate l'opzione long negli script per fornire chiarezza. Verrà letto molte volte e digitato una sola volta.

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Opzioni della riga di comando non supportate

Se si cerca di usare un'opzione non supportata, `ls` e altri comandi di solito stampano un messaggio di errore simile a:

```bash
$ ls -j
```

```error
ls: invalid option -- 'j'
Try 'ls --help' for more information.
```

::::::::::::::::::::::::::::::::::::::::::::::::::

#### Il comando `man`

L'altro modo per conoscere `ls` è digitare

```bash
$ man ls
```

Questo comando trasformerà il vostro terminale in una pagina con una descrizione del comando `ls` e delle sue opzioni.

Per navigare tra le pagine di `man`, si possono usare <kbd>↑</kbd> e <kbd>↓</kbd> per spostarsi riga per riga, oppure provare <kbd>b</kbd> e <kbd>Spacebar</kbd> per saltare su e giù di una pagina intera. Per cercare un carattere o una parola nelle pagine di `man`, usare <kbd>/</kbd> seguito dal carattere o dalla parola che si sta cercando. A volte una ricerca produce più risultati. In tal caso, è possibile spostarsi tra i risultati utilizzando <kbd>N</kbd> (per andare avanti) e <kbd>Shift</kbd>\+<kbd>N</kbd> (per andare indietro).

Per uscire dalle pagine `man`, premere <kbd>q</kbd>.

::::::::::::::::::::::::::::::::::::::::: callout

## Pagine di manuale sul web

Naturalmente, esiste un terzo modo per accedere alla guida dei comandi: la ricerca su Internet tramite il browser. Quando si utilizza la ricerca su Internet, includere la frase `unix man page` nella query di ricerca aiuterà a trovare risultati pertinenti.

GNU fornisce collegamenti ai suoi [manuali](https://www.gnu.org/manual/manual.html), compreso il [core GNU utilities](https://www.gnu.org/software/coreutils/manual/coreutils.html), che copre molti comandi introdotti in questa lezione.


::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Esplorazione di altre opzioni `ls`

È anche possibile utilizzare due opzioni contemporaneamente. Cosa fa il comando `ls` quando viene usato con l'opzione `-l`? E se si utilizzano sia l'opzione `-l` che l'opzione `-h`?

Alcuni dei suoi risultati riguardano proprietà che non vengono trattate in questa lezione (come i permessi e la proprietà dei file), ma il resto dovrebbe essere comunque utile.

::::::::::::::: solution

## Soluzione

L'opzione `-l` fa sì che `ls` utilizzi un formato di elenco **l**lungo, mostrando non solo i nomi dei file/directory ma anche informazioni aggiuntive, come la dimensione del file e l'ora dell'ultima modifica. Se si usano sia l'opzione `-h` che l'opzione `-l`, si rende la dimensione del file "leggibile dall'uomo", cioè si visualizza qualcosa come `5.3K` invece di `5369`.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Elenco in ordine cronologico inverso

Per impostazione predefinita, `ls` elenca il contenuto di una directory in ordine alfabetico per nome. Il comando `ls -t` elenca gli elementi in base all'ora dell'ultima modifica invece che in ordine alfabetico. Il comando `ls -r` elenca il contenuto di una directory in ordine inverso. Quale file viene visualizzato per ultimo quando si combinano le opzioni `-t` e `-r`? Suggerimento: Potrebbe essere necessario usare l'opzione `-l` per vedere le ultime date di modifica.

::::::::::::::: solution

## Soluzione

Il file modificato più di recente è elencato per ultimo quando si usa `-rt`. Questo può essere molto utile per trovare le modifiche più recenti o per verificare se è stato scritto un nuovo file di output.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

### Esplorazione di altre directory

Non solo si può usare `ls` sulla directory di lavoro corrente, ma anche per elencare il contenuto di una directory diversa. Diamo un'occhiata alla nostra directory `Desktop` eseguendo `ls -F Desktop`, cioè il comando `ls` con la **opzione** `-F` e l'[**argomento**][Argomenti] `Desktop`. L'argomento `Desktop` indica a `ls` che si vuole un elenco di qualcosa di diverso dalla directory di lavoro corrente:

```bash
$ ls -F Desktop
```

```output
shell-lesson-data/
```

Si noti che se una directory denominata `Desktop` non esiste nella directory di lavoro corrente, questo comando restituirà un errore. In genere, una directory `Desktop` esiste nella propria home directory, che si presume sia la directory di lavoro corrente della shell bash.

L'output dovrebbe essere un elenco di tutti i file e le sottodirectory della vostra directory Desktop, compresa la directory `shell-lesson-data` che avete scaricato nel [setup per questa lezione](../learners/setup.md). (Nella maggior parte dei sistemi, il contenuto della directory `Desktop` nella shell viene visualizzato come icona in un'interfaccia grafica dietro tutte le finestre aperte. Verificate se questo è il vostro caso)

Organizzare le cose in modo gerarchico ci aiuta a tenere traccia del nostro lavoro. Sebbene sia possibile mettere centinaia di file nella nostra home directory, così come è possibile ammassare centinaia di fogli stampati sulla nostra scrivania, è molto più facile trovare le cose quando sono organizzate in sottodirectory con nomi ragionevoli.

Ora che sappiamo che la directory `shell-lesson-data` si trova nella nostra directory Desktop, possiamo fare due cose.

Per prima cosa, usando la stessa strategia di prima, possiamo esaminare il suo contenuto passando il nome di una directory a `ls`:

```bash
$ ls -F Desktop/shell-lesson-data
```

```output
exercise-data/  north-pacific-gyre/
```

In secondo luogo, possiamo cambiare la nostra posizione in una directory diversa, in modo da non trovarci più nella nostra home directory.

Il comando per cambiare posizione è `cd` seguito da un nome di directory per cambiare la nostra directory di lavoro. `cd` sta per 'change directory', il che è un po' fuorviante. Il comando non cambia la directory, ma la directory di lavoro corrente della shell. In altre parole, cambia le impostazioni della shell per quanto riguarda la directory in cui ci troviamo. Il comando `cd` è simile a un doppio clic su una cartella in un'interfaccia grafica per entrare in quella cartella.

Supponiamo di volerci spostare nella directory `exercise-data` che abbiamo visto sopra. Per arrivarci possiamo usare la seguente serie di comandi:

```bash
$ cd Desktop
$ cd shell-lesson-data
$ cd exercise-data
```

Questi comandi ci spostano dalla nostra home directory alla nostra directory Desktop, poi alla directory `shell-lesson-data`, quindi alla directory `exercise-data`. Si noterà che `cd` non stampa nulla. Questo è normale. Molti comandi di shell non producono nulla sullo schermo quando vengono eseguiti con successo. Ma se si esegue `pwd` dopo di esso, si può vedere che ora ci troviamo in `/Users/nelle/Desktop/shell-lesson-data/exercise-data`.

Se ora si esegue `ls -F` senza argomenti, viene elencato il contenuto di `/Users/nelle/Desktop/shell-lesson-data/exercise-data`, perché è lì che ci troviamo:

```bash
$ pwd
```

```output
/Users/nelle/Desktop/shell-lesson-data/exercise-data
```

```bash
$ ls -F
```

```output
alkanes/  animal-counts/  creatures/  numbers.txt  writing/
```

Ora sappiamo come scendere nell'albero delle directory (cioè come entrare in una sottodirectory), ma come salire (cioè come lasciare una directory e andare nella sua directory madre)? Potremmo provare a fare come segue:

```bash
$ cd shell-lesson-data
```

```error
-bash: cd: shell-lesson-data: No such file or directory
```

ma si ottiene un errore! Perché?

Con i metodi utilizzati finora, `cd` può vedere solo le sottodirectory all'interno della directory corrente. Esistono diversi modi per vedere le directory al di sopra della posizione corrente; inizieremo con il più semplice.

esiste una scorciatoia nella shell per spostarsi su un livello di directory. Funziona come segue:

```bash
$ cd ..
```

`..` è un nome speciale di directory che significa "la directory che contiene questa", o più brevemente, il **genitore** della directory corrente. Sicuramente, se si esegue `pwd` dopo aver eseguito `cd ..`, ci si ritrova in `/Users/nelle/Desktop/shell-lesson-data`:

```bash
$ pwd
```

```output
/Users/nelle/Desktop/shell-lesson-data
```

La directory speciale `..` di solito non viene visualizzata quando si esegue `ls`. Se si desidera visualizzarla, si può aggiungere l'opzione `-a` a `ls -F`:

```bash
$ ls -F -a
```

```output
./  ../  exercise-data/  north-pacific-gyre/
```

`-a` sta per "mostra tutto" (compresi i file nascosti); obbliga `ls` a mostrare i nomi dei file e delle directory che iniziano con `.`, come ad esempio `..` (che, se ci troviamo in `/Users/nelle`, si riferisce alla directory `/Users`). Come si può vedere, viene visualizzata anche un'altra directory speciale, chiamata `.`, che significa "la directory di lavoro corrente". Può sembrare superfluo avere un nome per questa directory, ma presto ne vedremo l'uso.

Si noti che nella maggior parte degli strumenti a riga di comando, più opzioni possono essere combinate con un singolo `-` e senza spazi tra le opzioni; `ls -F -a` è equivalente a `ls -Fa`.

::::::::::::::::::::::::::::::::::::::::: callout

## Altri file nascosti

Oltre alle directory nascoste `..` e `.`, è possibile che venga visualizzato anche un file chiamato `.bash_profile`. Questo file contiene solitamente le impostazioni di configurazione della shell. Si possono vedere anche altri file e directory che iniziano con `.`. Si tratta in genere di file e directory utilizzati per configurare diversi programmi sul computer. Il prefisso `.` è usato per evitare che questi file di configurazione ingombrino il terminale quando si usa il comando standard `ls`.


::::::::::::::::::::::::::::::::::::::::::::::::::

Questi tre comandi sono i comandi di base per navigare nel filesystem del computer: `pwd`, `ls` e `cd`. Esploriamo alcune variazioni di questi comandi. Cosa succede se si digita `cd` da solo, senza indicare una directory?

```bash
$ cd
```

Come si può controllare cosa è successo? `pwd` ci dà la risposta!

```bash
$ pwd
```

```output
/Users/nelle
```

Si scopre che `cd` senza un argomento vi riporterà alla vostra home directory, il che è ottimo se vi siete persi nel vostro filesystem.

Proviamo a tornare alla directory `exercise-data` di prima. L'ultima volta abbiamo usato tre comandi, ma possiamo mettere insieme l'elenco delle directory per spostarci a `exercise-data` in un solo passaggio:

```bash
$ cd Desktop/shell-lesson-data/exercise-data
```

Verificare che ci si sia spostati nel posto giusto eseguendo `pwd` e `ls -F`.

Se si vuole salire di un livello dalla directory dei dati, si può usare `cd ..`. Ma c'è un altro modo per spostarsi in qualsiasi directory, indipendentemente dalla posizione attuale.

Finora, quando si sono specificati i nomi delle directory, o anche un percorso di directory (come sopra), si sono usati **percorsi relativi**. Quando si usa un percorso relativo con un comando come `ls` o `cd`, si cerca di trovare quella posizione dal punto in cui ci si trova, piuttosto che dalla radice del file system.

Tuttavia, è possibile specificare il **percorso assoluto** di una directory includendo il suo intero percorso a partire dalla directory principale, indicata da una barra iniziale. La barra iniziale `/` indica al computer di seguire il percorso dalla radice del file system, in modo da riferirsi sempre esattamente a una directory, indipendentemente dalla posizione in cui ci si trova quando si esegue il comando.

Questo ci permette di spostarci nella nostra directory `shell-lesson-data` da qualsiasi punto del filesystem (anche da dentro `exercise-data`). Per trovare il percorso assoluto che stiamo cercando, possiamo usare `pwd` e poi estrarre il pezzo che dobbiamo spostare in `shell-lesson-data`.

```bash
$ pwd
```

```output
/Users/nelle/Desktop/shell-lesson-data/exercise-data
```

```bash
$ cd /Users/nelle/Desktop/shell-lesson-data
```

Eseguire `pwd` e `ls -F` per assicurarsi di essere nella directory prevista.

::::::::::::::::::::::::::::::::::::::::: callout

## Altre due scorciatoie

La shell interpreta il carattere tilde (`~`) all'inizio di un percorso come "la home directory dell'utente corrente". Ad esempio, se la home directory di Nelle è `/Users/nelle`, allora `~/data` è equivalente a `/Users/nelle/data`. Questo funziona solo se è il primo carattere del percorso; `here/there/~/elsewhere` è *non* `here/there/Users/nelle/elsewhere`.

Un'altra scorciatoia è il carattere `-` (trattino).`cd` tradurrà `-` in *la directory precedente in cui mi trovavo*, il che è più veloce che dover ricordare, e poi digitare, il percorso completo. Questo è un modo *molto* efficiente di spostarsi *avanti e indietro tra due directory* -- cioè se si esegue `cd -` due volte, si torna alla directory di partenza.

La differenza tra `cd ..` e `cd -` è che il primo porta *su*, mentre il secondo porta *indietro*.

***

Provate! Per prima cosa spostatevi in `~/Desktop/shell-lesson-data` (dovreste essere già lì).

```bash
$ cd ~/Desktop/shell-lesson-data
```

Poi `cd` nella directory `exercise-data/creatures`

```bash
$ cd exercise-data/creatures
```

ora se si esegue

```bash
$ cd -
```

vedrete che siete tornati in `~/Desktop/shell-lesson-data`. Eseguite di nuovo `cd -` e sarete di nuovo in `~/Desktop/shell-lesson-data/exercise-data/creatures`


::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Percorsi assoluti e relativi

Partendo da `/Users/nelle/data`, quale dei seguenti comandi potrebbe essere usato da Nelle per navigare verso la sua home directory, che è `/Users/nelle`?

1. `cd .`
2. `cd /`
3. `cd /home/nelle`
4. `cd ../..`
5. `cd ~`
6. `cd home`
7. `cd ~/data/..`
8. `cd`
9. `cd ..`

::::::::::::::: solution

## Soluzione

1. No: `.` sta per la directory corrente.
2. No: `/` sta per la directory principale.
3. No: la directory home di Nelle è `/Users/nelle`.
4. No: questo comando sale di due livelli, cioè termina con `/Users`.
5. Sì: `~` sta per la home directory dell'utente, in questo caso `/Users/nelle`.
6. No: questo comando naviga in una directory `home` nella directory corrente, se esiste.
7. Sì: inutilmente complicato, ma corretto.
8. Sì: scorciatoia per tornare alla directory principale dell'utente.
9. Sì: sale di un livello.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Risoluzione del percorso relativo

Utilizzando il diagramma del filesystem qui sotto, se `pwd` visualizza `/Users/thing`, cosa visualizzerà `ls -F ../backup`?

1. `../backup: No such file or directory`
2. `2012-12-01 2013-01-08 2013-01-27`
3. `2012-12-01/ 2013-01-08/ 2013-01-27/`
4. `original/ pnas_final/ pnas_sub/`

![](fig/filesystem-challenge.svg){alt='Un albero di directory sotto la directory Utenti dove "/Utenti" contiene le directory "backup" e "thing"; "/Utenti/backup" contiene "original", "pnas\_final" e "pnas\_sub"; "/Utenti/thing" contiene "backup"; e "/Utenti/thing/backup" contiene "2012-12-01", "2013-01-08" e "2013-01-27"'}

::::::::::::::: solution

## Soluzione

1. No: c'è *una directory `backup` in `/Users`.
2. No: questo è il contenuto di `Users/thing/backup`, ma con `..`, abbiamo chiesto un livello più in alto.
3. No: vedi spiegazione precedente.
4. Sì: `../backup/` si riferisce a `/Users/backup/`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## `ls` Comprensione della lettura

Utilizzando il diagramma del filesystem qui sotto, se `pwd` visualizza `/Users/backup` e `-r` dice a `ls` di visualizzare le cose in ordine inverso, quale/i comando/i produrrà il seguente output:

```output
pnas_sub/ pnas_final/ original/
```

![](fig/filesystem-challenge.svg){alt='Un albero di directory sotto la directory Utenti dove "/Utenti" contiene le directory "backup" e "thing"; "/Utenti/backup" contiene "original", "pnas\_final" e "pnas\_sub"; "/Utenti/thing" contiene "backup"; e "/Utenti/thing/backup" contiene "2012-12-01", "2013-01-08" e "2013-01-27"'}

1. `ls pwd`
2. `ls -r -F`
3. `ls -r -F /Users/backup`

::::::::::::::: solution

## Soluzione

1. No: `pwd` non è il nome di una directory.
2. Sì: `ls` senza l'argomento directory elenca i file e le directory nella directory corrente.
3. Sì: utilizza esplicitamente il percorso assoluto.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Sintassi generale di un comando di Shell

Abbiamo già incontrato comandi, opzioni e argomenti, ma forse è utile formalizzare un po' di terminologia.

Considerate il comando qui sotto come un esempio generale di comando, che verrà sezionato nelle sue parti componenti:

```bash
$ ls -F /
```

![](fig/shell_command_syntax.svg){alt='Sintassi generale di un comando di shell'}

`ls` è il **comando**, con una **opzione** `-F` e un **argomento** `/`. Abbiamo già incontrato opzioni che iniziano con un solo trattino (`-`), note come **opzioni corte**, o con due trattini (`--`), note come **opzioni lunghe**. le [Opzioni] modificano il comportamento di un comando e gli [Argomenti] indicano al comando su cosa operare (ad esempio, file e directory). A volte le opzioni e gli argomenti sono indicati come **parametri**. Un comando può essere chiamato con più di un'opzione e più di un argomento, ma non sempre un comando richiede un argomento o un'opzione.

A volte si può vedere che le opzioni vengono chiamate **scambi** o **flags**, specialmente per le opzioni che non richiedono argomenti. In questa lezione useremo il termine *opzione*.

Ogni parte è separata da spazi. Se si omette lo spazio tra `ls` e `-F` la shell cercherà un comando chiamato `ls-F`, che non esiste. Inoltre, la capitalizzazione può essere importante. Ad esempio, `ls -s` visualizzerà la dimensione dei file e delle directory accanto ai nomi, mentre `ls -S` ordinerà i file e le directory per dimensione, come mostrato di seguito:

```bash
$ cd ~/Desktop/shell-lesson-data
$ ls -s exercise-data
```

```output
total 28
 4 animal-counts   4 creatures  12 numbers.txt   4 alkanes   4 writing
```

Si noti che le dimensioni restituite da `ls -s` sono in *blocchi*. Poiché queste sono definite in modo diverso per i diversi sistemi operativi, è possibile che non si ottengano le stesse cifre dell'esempio.

```bash
$ ls -S exercise-data
```

```output
animal-counts  creatures  alkanes  writing  numbers.txt
```

Mettendo insieme tutti questi elementi, il comando `ls -F /` di cui sopra fornisce un elenco di file e directory nella directory principale `/`. Di seguito è riportato un esempio dell'output che si potrebbe ottenere dal comando precedente:

```bash
$ ls -F /
```

```output
Applications/         System/
Library/              Users/
Network/              Volumes/
```

### Pipeline di Nelle: Organizzare i file

sapendo queste informazioni su file e directory, Nelle è pronta a organizzare i file che la macchina per il saggio delle proteine creerà.

crea una directory chiamata `north-pacific-gyre` (per ricordarsi da dove provengono i dati), che conterrà i file di dati della macchina di analisi e i suoi script di elaborazione dei dati.

Ogni campione fisico è etichettato secondo la convenzione del suo laboratorio con un ID unico di dieci caratteri, ad esempio "NENE01729A". Questo ID viene utilizzato nel registro di raccolta per registrare la posizione, l'ora, la profondità e altre caratteristiche del campione, quindi decide di utilizzarlo nel nome di ogni file di dati. Poiché l'output della macchina di analisi è un testo semplice, chiamerà i suoi file `NENE01729A.txt`, `NENE01812A.txt` e così via. Tutti i 1520 file andranno nella stessa directory.

ora nella sua directory corrente `shell-lesson-data`, Nelle può vedere quali file ha usando il comando:

```bash
$ ls north-pacific-gyre/
```

Questo comando è molto impegnativo da digitare, ma si può lasciare che la shell faccia la maggior parte del lavoro attraverso il cosiddetto **completamento delle tabelle**. Se si digita:

```bash
$ ls nor
```

e poi preme <kbd>Tab</kbd> (il tasto tab della tastiera), la shell completa automaticamente il nome della directory:

```bash
$ ls north-pacific-gyre/
```

Premendo di nuovo <kbd>Tab</kbd> non si ottiene nulla, poiché ci sono più possibilità; premendo <kbd>Tab</kbd> due volte si ottiene un elenco di tutti i file.

Se Nelle preme <kbd>G</kbd> e poi di nuovo <kbd>Tab</kbd>, la shell aggiungerà 'goo' poiché tutti i file che iniziano con 'g' condividono i primi tre caratteri 'goo'.

```bash
$ ls north-pacific-gyre/goo
```

per vedere tutti quei file, si può premere <kbd>Tab</kbd> altre due volte.

```bash
ls north-pacific-gyre/goo
goodiff.sh   goostats.sh
```

questo si chiama **completamento delle tabelle** e lo vedremo in molti altri strumenti man mano che andremo avanti.



[Arguments]: https://swcarpentry.github.io/shell-novice/reference.html#argument


:::::::::::::::::::::::::::::::::::::::: keypoints

- Il file system è responsabile della gestione delle informazioni sul disco.
- Le informazioni sono memorizzate in file, che sono memorizzati in directory (cartelle).
- le directory possono anche memorizzare altre directory, che formano un albero di directory.
- `pwd` stampa la directory di lavoro corrente dell'utente.
- `ls [path]` stampa un elenco di uno specifico file o directory; `ls` da solo elenca la directory di lavoro corrente.
- `cd [path]` cambia la directory di lavoro corrente.
- La maggior parte dei comandi accetta opzioni che iniziano con un singolo `-`.
- i nomi delle directory in un percorso sono separati con `/` su Unix, ma `\` su Windows.
- `/` da sola è la directory principale dell'intero file system.
- Un percorso assoluto specifica una posizione dalla radice del file system.
- Un percorso relativo specifica una posizione a partire da quella corrente.
- `.` da solo significa "la directory corrente"; `..` significa "la directory sopra quella corrente".

::::::::::::::::::::::::::::::::::::::::::::::::::



