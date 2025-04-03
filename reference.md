---
title: Riassunto dei comandi di base
---


## Riassunto dei comandi di base

| Action       | Files | Folders      |
| ------------ | ----- | ------------ |
| Inspect      | ls    | ls           |
| View content | cat   | ls           |
| Navigate to  |       | cd           |
| Move         | mv    | mv           |
| Copy         | cp    | cp -r        |
| Create       | nano  | mkdir        |
| Delete       | rm    | rmdir, rm -r |

## Gerarchia del filesystem

La seguente è una panoramica di un filesystem Unix standard. La gerarchia esatta dipende dalla piattaforma. La struttura dei file e delle directory potrebbe differire leggermente:

![](fig/standard-filesystem-hierarchy.svg){alt='Gerarchia del filesystem Linux'}

## Glossario

[percorso assoluto]{#percorsoassoluto} : Un [percorso](#percorso) che si riferisce a una particolare posizione in un file system. I percorsi assoluti sono solitamente scritti rispetto alla [directory principale](#root-directory) del file system e iniziano con "/" (su Unix) o "\" (su Microsoft Windows). Vedere anche: [percorso relativo](#relative-path).

[argomento]{#argomento} : valore dato a una funzione o a un programma quando viene eseguito. Il termine è spesso usato in modo intercambiabile (e incoerente) con [parametro](#parametro).

[comando shell]{#command-shell} : Vedere [shell](#shell)

[interfaccia a riga di comando]{#command-line-interface} : Un'interfaccia utente basata sulla digitazione di comandi, di solito in un [REPL](#read-evaluate-print-loop). Vedere anche: [interfaccia grafica](#graphical-user-interface).

[commento]{#commento} : Un'osservazione in un programma che ha lo scopo di aiutare i lettori umani a capire cosa sta succedendo, ma che viene ignorata dal computer. I commenti in Python, R e nella shell Unix iniziano con un carattere `#` e vanno fino alla fine della riga; i commenti in SQL iniziano con `--` e altri linguaggi hanno altre convenzioni.

[directory di lavoro corrente]{#current-working-directory} : La directory da cui vengono calcolati i [percorsi relativi](#relative-path); equivalentemente, il luogo in cui vengono cercati i file a cui si fa riferimento solo per nome. Ogni [processo](#processo) ha una directory di lavoro corrente. La directory di lavoro corrente è solitamente indicata con la notazione abbreviata `.` (pronunciato "punto").

[file system]{#file-system} : Un insieme di file, directory e dispositivi di I/O (come tastiere e schermi). Un file system può essere distribuito su molti dispositivi fisici, oppure molti file system possono essere memorizzati su un singolo dispositivo fisico; il [sistema operativo](#operating-system) ne gestisce l'accesso.

[estensione del nome del file]{#filename-extension} : La parte del nome di un file che viene dopo il carattere finale ".". Per convenzione, identifica il tipo di file: `.txt` significa "file di testo", `.png` significa "file grafico di rete portatile" e così via. Queste convenzioni non sono applicate dalla maggior parte dei sistemi operativi: è perfettamente possibile (ma confuso!) chiamare un file audio MP3 `homepage.html`. Poiché molte applicazioni utilizzano le estensioni dei nomi dei file per identificare il [tipo MIME](#mime-type) del file, un nome errato può causare il fallimento di tali applicazioni.

[filtro]{#filtro} : Programma che trasforma un flusso di dati. Molti strumenti della riga di comando di Unix sono scritti come filtri: leggono dati da [standard input](#standard-input), li elaborano e scrivono il risultato su [standard output](#standard-output).

[ciclo for]{#for-loop} : Un ciclo che viene eseguito una volta per ogni valore in un qualche tipo di insieme, elenco o intervallo. Vedere anche: [ciclo while](#while-loop).

[interfaccia utente grafica]{#graphical-user-interface} : Interfaccia utente basata sulla selezione di elementi e azioni da un display grafico, di solito controllata con il mouse. Vedi anche: [interfaccia a riga di comando](#command-line-interface).

[home directory]{#home-directory} : la directory predefinita associata a un account su un sistema informatico. Per convenzione, tutti i file di un utente sono memorizzati nella o sotto la sua home directory.

[loop]{#loop} : Un insieme di istruzioni da eseguire più volte. Consiste in un [corpo del ciclo](#loop-body) e (di solito) in una condizione per uscire dal ciclo. Si veda anche [for loop](#for-loop) e [while loop](#while-loop).

[loop body]{#loop-body} : L'insieme delle istruzioni o dei comandi che vengono ripetuti all'interno di un [ciclo for](#for-loop) o [ciclo while](#while-loop).

[Tipo MIME]{#mime-type} : I tipi MIME (Multi-Purpose Internet Mail Extensions) descrivono diversi tipi di file da scambiare su Internet, ad esempio immagini, audio e documenti.

[sistema operativo]{#operating-system} : Software che gestisce le interazioni tra utenti, hardware e software [processi](#processo). Esempi comuni sono Linux, macOS e Windows.

[option]{#option} : modo per specificare un argomento o un'impostazione di un programma a riga di comando. Per convenzione le applicazioni Unix usano un trattino seguito da una singola lettera, come `-v`, o due trattini seguiti da una parola, come `--verbose`, mentre le applicazioni DOS usano una barra, come `/V`. A seconda dell'applicazione, un'opzione può essere seguita da un singolo argomento, come in `-o /tmp/output.txt`.

[parametro]{#parametro} : una variabile denominata nella dichiarazione di una funzione e utilizzata per contenere un valore passato nella chiamata. Il termine è spesso usato in modo intercambiabile (e incoerente) con [argument](#argument).

[directory padre]{#parent-directory} : La directory che "contiene" quella in questione. Ogni directory in un file system, tranne la [directory principale](#root-directory), ha un genitore. Il genitore di una directory è solitamente indicato con la notazione abbreviata `..` (pronunciato "dot dot").

[percorso]{#percorso} : Descrizione che specifica la posizione di un file o di una directory all'interno di un [file system](#file-system). Vedere anche: [percorso assoluto](#percorsoassoluto), [percorso relativo](#percorsorelativo).

[pipe]{#pipe} : Una connessione dall'uscita di un programma all'ingresso di un altro. Quando due o più programmi sono collegati in questo modo, vengono chiamati "pipeline".

[processo]{#processo} : Un'istanza in esecuzione di un programma, contenente codice, valori di variabili, file aperti e connessioni di rete, e così via. I processi sono gli "attori" che il [sistema operativo](#operating-system) gestisce; in genere esegue ogni processo per pochi millisecondi alla volta per dare l'impressione che vengano eseguiti simultaneamente.

[prompt]{#prompt} : Uno o più caratteri visualizzati da un [REPL](#read-evaluate-print-loop) per mostrare che sta aspettando il suo prossimo comando.

[quoting]{#quoting} : (nella shell): Uso di virgolette di vario tipo per impedire alla shell di interpretare caratteri speciali. Ad esempio, per passare la stringa `*.txt` a un programma, è solitamente necessario scriverla come `'*.txt'` (con virgolette singole) in modo che la shell non cerchi di espandere il carattere jolly `*`.

[read-evaluate-print loop]{#read-evaluate-print-loop} : (REPL): Un'[interfaccia a riga di comando](#command-line-interface) che legge un comando dall'utente, lo esegue, stampa il risultato e attende un altro comando.

[redirect]{#redirect} : Per inviare l'output di un comando a un file piuttosto che allo schermo o a un altro comando, o equivalentemente per leggere l'input di un comando da un file.

[espressione regolare]{#regular-expression} : uno schema che specifica un insieme di stringhe di caratteri. Le RE sono utilizzate soprattutto per trovare sequenze di caratteri nelle stringhe.

[percorso relativo]{#percorso relativo} : Un [percorso](#percorso) che specifica la posizione di un file o di una directory rispetto alla [directory di lavoro corrente](#directory di lavoro corrente). Qualsiasi percorso che non inizia con un carattere separatore ("/" o "\") è un percorso relativo. Vedere anche: [percorso assoluto](#percorsoassoluto).

[directory principale]{#root-directory} : la directory più alta di un [file system](#file-system). Il suo nome è "/" su Unix (compresi Linux e macOS) e "/" su Microsoft Windows.

[shell]{#shell} : [interfaccia a riga di comando](#command-line-interface) come Bash (la Bourne-Again Shell) o la shell DOS di Microsoft Windows che permette all'utente di interagire con il [sistema operativo](#operating-system).

[script di shell]{#shell-script} : Un insieme di comandi [shell](#shell) memorizzati in un file per essere riutilizzati. Uno script di shell è un programma eseguito dalla shell; il nome "script" è usato per ragioni storiche.

[standard input]{#standard-input} : flusso di input predefinito di un processo. Nelle applicazioni interattive a riga di comando, è tipicamente collegato alla tastiera; in una [pipe](#pipe), riceve i dati dallo [standard output](#standard-output) del processo precedente.

[standard output]{#standard-output} : flusso di output predefinito di un processo. Nelle applicazioni interattive a riga di comando, i dati inviati allo standard output vengono visualizzati sullo schermo; in una [pipe](#pipe), vengono passati allo [standard input](#standard-input) del processo successivo.

[sottodirectory]{#sub-directory} : Una directory contenuta in un'altra directory.

[tab completion]{#tab-completion} : Una funzione fornita da molti sistemi interattivi in cui la pressione del tasto Tab attiva il completamento automatico della parola o del comando corrente.

[variabile]{#variabile} : Nome di un programma associato a un valore o a un insieme di valori.

[ciclo while]{#while-loop} : Un ciclo che continua a essere eseguito finché una certa condizione è vera. Vedere anche: [ciclo for](#for-loop).

[jolly]{#wildcard} : Carattere usato nella corrispondenza dei modelli. Nella shell Unix, il carattere jolly `*` corrisponde a zero o più caratteri, in modo che `*.txt` corrisponda a tutti i file il cui nome finisce in `.txt`.

## Riferimenti esterni

### Apertura di un terminale

- [Come usare il terminale su Mac](https://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/)
- [Git per Windows](https://git-for-windows.github.io/)
- [Come installare lo strumento a riga di comando della shell Bash su Windows 10](https://www.windowscentral.com/how-install-bash-shell-command-line-windows-10)
- [Installare e usare la Bash Shell di Linux su Windows 10](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/)
- [Utilizzo della shell Bash di Windows 10](https://www.howtogeek.com/265900/everything-you-can-do-with-windows-10s-new-bash-shell/)
- [Utilizzo di un emulatore UNIX/Linux (Cygwin) o di un client Secure Shell (SSH) (Putty)](https://faculty.smu.edu/reynolds/unixtut/windows.html)

### Manuali

- [Manuali GNU](https://www.gnu.org/manual/manual.html)
- [Utilità GNU di base](https://www.gnu.org/software/coreutils/manual/coreutils.html)

### Varie

- [Giro del Pacifico settentrionale](https://en.wikipedia.org/wiki/North_Pacific_Gyre)
- [Great Pacific Garbage Patch](https://en.wikipedia.org/wiki/Great_Pacific_Garbage_Patch)
- ['Garantire la longevità delle informazioni digitali' di Jeff Rothenberg](https://www.clir.org/pubs/archives/ensuring.pdf)
- [Haikus sugli errori del computer](https://wiki.c2.com/?ComputerErrorHaiku)
- [Come nominare bene i file, di Jenny Bryan](https://speakerdeck.com/jennybc/how-to-name-files)


