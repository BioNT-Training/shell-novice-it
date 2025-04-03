---
title: Introduzione alla shell
teaching: 5
exercises: 0
---


::::::::::::::::::::::::::::::::::::::: objectives

- Spiegare come la shell si relaziona con la tastiera, lo schermo, il sistema operativo e i programmi degli utenti.
- Spiegare quando e perché si dovrebbero usare le interfacce a riga di comando invece delle interfacce grafiche.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Cos'è una shell di comando e perché dovrei usarla?

::::::::::::::::::::::::::::::::::::::::::::::::::

### Sfondo

L'uomo e il computer interagiscono comunemente in molti modi diversi, ad esempio tramite tastiera e mouse, interfacce touch screen o sistemi di riconoscimento vocale. Il modo più diffuso di interagire con i personal computer è chiamato **interfaccia utente grafica** (GUI). Con una GUI, le istruzioni vengono impartite facendo clic con il mouse e utilizzando interazioni guidate da menu.

Sebbene l'aiuto visivo di un'interfaccia grafica ne renda intuitivo l'apprendimento, questo modo di fornire istruzioni a un computer è molto poco scalabile. Immaginate il seguente compito: per una ricerca bibliografica, dovete copiare la terza riga di mille file di testo in mille directory diverse e incollarla in un unico file. Utilizzando un'interfaccia grafica, non solo dovreste cliccare alla vostra scrivania per diverse ore, ma potreste anche commettere un errore nel completare questo compito ripetitivo. È qui che ci avvantaggiamo della shell Unix. La shell Unix è sia un'interfaccia a riga di comando (CLI) che un linguaggio di scripting, che consente di svolgere tali compiti ripetitivi in modo automatico e veloce. Con i comandi appropriati, la shell può ripetere le operazioni con o senza modifiche tutte le volte che si vuole. Utilizzando la shell, l'operazione descritta nell'esempio di letteratura può essere eseguita in pochi secondi.

### La shell

La shell è un programma in cui gli utenti possono digitare comandi. Con la shell è possibile richiamare programmi complicati come il software di modellazione climatica o semplici comandi che creano una directory vuota con una sola riga di codice. La shell Unix più diffusa è Bash (Bourne Again SHell --- così chiamata perché deriva da una shell scritta da Stephen Bourne). Bash è la shell predefinita nella maggior parte delle moderne implementazioni di Unix e nella maggior parte dei pacchetti che forniscono strumenti simili a Unix per Windows. Si noti che "Git Bash" è un software che consente agli utenti di Windows di utilizzare un'interfaccia simile a Bash quando interagiscono con Git.

L'uso della shell richiede un certo sforzo e un po' di tempo per essere appreso. Mentre l'interfaccia grafica presenta delle scelte da selezionare, le scelte della CLI non vengono presentate automaticamente, quindi è necessario imparare alcuni comandi come un nuovo vocabolario in una lingua che si sta studiando. Tuttavia, a differenza di una lingua parlata, un piccolo numero di "parole" (cioè di comandi) permette di fare molta strada e oggi ci occuperemo di questi pochi elementi essenziali.

La grammatica di una shell consente di combinare gli strumenti esistenti in potenti pipeline e di gestire automaticamente grandi volumi di dati. Le sequenze di comandi possono essere scritte in un *script*, migliorando la riproducibilità dei flussi di lavoro.

Inoltre, la riga di comando è spesso il modo più semplice per interagire con macchine e supercomputer remoti. La familiarità con la shell è quasi essenziale per eseguire una serie di strumenti e risorse specializzate, compresi i sistemi di calcolo ad alte prestazioni. Con l'aumento della popolarità dei cluster e dei sistemi di cloud computing per l'elaborazione di dati scientifici, la capacità di interagire con la shell sta diventando un'abilità necessaria. Possiamo basarci sulle competenze della riga di comando qui trattate per affrontare un'ampia gamma di domande scientifiche e sfide computazionali.

Iniziamo.

Quando la shell viene aperta per la prima volta, viene visualizzato un **prompt**, che indica che la shell è in attesa di input.

```bash
$
```

La shell usa tipicamente `$ ` come prompt, ma può usare un simbolo diverso. Negli esempi di questa lezione, mostreremo il prompt come `$ `. La cosa più importante è *non digitare il prompt* quando si digitano i comandi. Digitate solo il comando che segue il prompt. Questa regola si applica sia in queste lezioni che in quelle di altre fonti. Si noti inoltre che dopo aver digitato un comando, è necessario premere il tasto <kbd>Invio</kbd> per eseguirlo.

Il prompt è seguito da un **cursore di testo**, un carattere che indica la posizione in cui verrà visualizzata la digitazione. Il cursore è solitamente un blocco lampeggiante o fisso, ma può anche essere un trattino basso o una pipe. Lo si può vedere in un programma di editor di testo, ad esempio.

Si noti che il prompt potrebbe avere un aspetto leggermente diverso. In particolare, gli ambienti di shell più diffusi mettono per default il nome dell'utente e il nome dell'host prima di `$`. Un prompt di questo tipo potrebbe apparire come, ad esempio:

```bash
nelle@localhost $
```

Il prompt potrebbe includere anche più di questo. Non preoccupatevi se il vostro prompt non è solo un breve `$ `. Questa lezione non dipende da queste informazioni aggiuntive e non dovrebbe nemmeno ostacolarvi. L'unico elemento importante su cui concentrarsi è il carattere `$ ` stesso e vedremo più avanti perché.

Proviamo il nostro primo comando, `ls`, abbreviazione di listing. Questo comando elencherà il contenuto della directory corrente:

```bash
$ ls
```

```output
Desktop     Downloads   Movies      Pictures
Documents   Library     Music       Public
```

::::::::::::::::::::::::::::::::::::::::: callout

## Comando non trovato

Se la shell non riesce a trovare un programma il cui nome corrisponde al comando digitato, stamperà un messaggio di errore come:

```bash
$ ks
```

```output
ks: command not found
```

Questo può accadere se il comando è stato digitato in modo errato o se il programma corrispondente a quel comando non è installato.


::::::::::::::::::::::::::::::::::::::::::::::::::

## La pipeline di Nelle: Un problema tipico

Nelle Nemo, una biologa marina, è appena tornata da un'indagine di sei mesi nel [North Pacific Gyre](https://en.wikipedia.org/wiki/North_Pacific_Gyre), dove ha campionato la vita marina gelatinosa nel [Great Pacific Garbage Patch](https://en.wikipedia.org/wiki/Great_Pacific_Garbage_Patch). Ha 1520 campioni che ha fatto passare attraverso una macchina di analisi per misurare l'abbondanza relativa di 300 proteine. Deve far passare questi 1520 file attraverso un programma immaginario chiamato `goostats.sh`. Oltre a questo enorme compito, deve scrivere i risultati entro la fine del mese, in modo che il suo articolo possa apparire in un numero speciale di *Aquatic Goo Letters*.

Se Nelle sceglie di eseguire `goostats.sh` a mano utilizzando un'interfaccia grafica, dovrà selezionare e aprire un file 1520 volte. Se `goostats.sh` impiega 30 secondi per eseguire ogni file, l'intero processo richiederà più di 12 ore dell'attenzione di Nelle. Con la shell, Nelle può invece assegnare al computer questo compito banale mentre si concentra sulla stesura del suo articolo.

Le prossime lezioni esploreranno i modi in cui Nelle può raggiungere questo obiettivo. In particolare, le lezioni spiegano come Nelle possa utilizzare una shell di comando per eseguire il programma `goostats.sh`, utilizzando dei loop per automatizzare i passaggi ripetitivi di inserimento dei nomi dei file, in modo che il suo computer possa lavorare mentre lei scrive il suo articolo.

Una volta messa insieme una pipeline di elaborazione, sarà in grado di riutilizzarla ogni volta che raccoglierà altri dati.

Per svolgere il suo compito, Nelle deve sapere come fare:

- navigare in un file/directory
- creare un file/directory
- verifica la lunghezza di un file
- concatenare i comandi tra loro
- recuperare un insieme di file
- iterazione di file
- esegue uno script di shell contenente la sua pipeline

:::::::::::::::::::::::::::::::::::::::: keypoints

- Una shell è un programma il cui scopo principale è leggere i comandi ed eseguire altri programmi.
- Questa lezione utilizza Bash, la shell predefinita in molte implementazioni di Unix.
- I programmi possono essere eseguiti in Bash inserendo i comandi nel prompt della riga di comando.
- I principali vantaggi della shell sono l'elevato rapporto tra azioni e battute, il supporto per l'automazione di attività ripetitive e la capacità di accedere a macchine in rete.
- Una sfida significativa nell'uso della shell può essere quella di sapere quali comandi devono essere eseguiti e come eseguirli.

::::::::::::::::::::::::::::::::::::::::::::::::::



