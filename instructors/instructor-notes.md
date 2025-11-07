---
title: Note dell'istruttore
---


- Perché impariamo a usare la shell?
  - Permette agli utenti di automatizzare le attività ripetitive
  - E catturare le piccole fasi di manipolazione dei dati che normalmente non vengono registrate per rendere la ricerca riproducibile
- Il problema
  - Eseguire lo stesso flusso di lavoro su più campioni può richiedere inutilmente molto lavoro
  - Manipolazione manuale dei file di dati:
    - spesso non viene catturato dalla documentazione
    - è difficile da riprodurre
    - è difficile da risolvere, rivedere o migliorare
- La shell
  - I flussi di lavoro possono essere automatizzati con l'uso di script di shell
  - I comandi integrati consentono una facile manipolazione dei dati (ad es. ordinamento, grep, ecc.)
  - Ogni passo può essere catturato nello script di shell e consentire la riproducibilità e la facile risoluzione dei problemi

## Complessivo

Molte persone si sono chieste se dovremmo ancora insegnare la shell. Dopo tutto, chi vuole rinominare diverse migliaia di file di dati può farlo facilmente in modo interattivo nell'interprete Python, e chi fa un'analisi seria dei dati probabilmente farà la maggior parte del suo lavoro all'interno di IPython Notebook o R Studio. Quindi perché insegnare la shell?

La prima risposta è: "Perché molto altro dipende da questo" L'installazione di software, la configurazione dell'editor predefinito e il controllo di macchine remote presuppongono spesso una familiarità di base con la shell e con concetti correlati come lo standard input e output. Molti strumenti utilizzano anche la sua terminologia (per esempio, i comandi magici `%ls` e `%cd` in IPython).

La seconda risposta è: "Perché è un modo semplice per introdurre alcune idee fondamentali sull'uso del computer" Quando insegniamo alle persone a usare la shell Unix, insegniamo loro che devono far ripetere le cose al computer (tramite il completamento con tabulazione, `!` seguito da un numero di comando e loop di `for`) piuttosto che ripetere le cose da soli. Insegniamo loro anche a prendere le cose che hanno scoperto di fare frequentemente e a salvarle per riutilizzarle in seguito (tramite script di shell), a dare nomi sensati alle cose e a scrivere un po' di documentazione (come i commenti in cima agli script di shell) per migliorare la vita dei loro futuri compagni.

La terza risposta è: "Perché permette di utilizzare molti strumenti specifici del dominio e risorse di calcolo a cui i ricercatori non possono accedere altrimenti" La familiarità con la shell è molto utile per l'accesso remoto alle macchine, per l'utilizzo dell'infrastruttura di calcolo ad alte prestazioni e per l'esecuzione di nuovi strumenti specialistici in molte discipline. Non insegniamo competenze specifiche per l'HPC o per il dominio, ma poniamo le basi per un ulteriore sviluppo di queste competenze. In particolare, la comprensione della sintassi dei comandi, dei flag e dei sistemi di aiuto è utile per gli strumenti specifici del dominio e la comprensione del file system (e di come navigarlo) è utile per l'accesso remoto.

Infine, e forse la cosa più importante, insegnare alle persone la shell ci permette di insegnare loro a pensare alla programmazione in termini di composizione di funzioni. Nel caso della shell, ciò assume la forma di pipeline piuttosto che di chiamate di funzione annidate, ma l'idea di base di "piccoli pezzi, uniti in modo lasco" è la stessa.

Tutto questo materiale può essere trattato in tre ore, a patto che gli studenti che usano Windows non incontrino ostacoli quali:

- non riuscire a capire dove si trova la propria home directory (soprattutto se si usa Cygwin);
- non è possibile eseguire un editor di testo normale; e
- la shell che rifiuta di eseguire script che includono terminazioni di riga DOS.

## Preparazione all'insegnamento

- Usare la cartella `data` per gli esercizi in laboratorio e gli esempi di codifica dal vivo. È possibile clonare la cartella shell-novice o utilizzare il pulsante *Download ZIP* sulla destra per ottenere l'intero [repository Git](https://github.com/swcarpentry/shell-novice). Ora forniamo anche un file zip della cartella `data` nella [pagina di installazione](../learners/setup.md).

- Sito web: sono state utilizzate diverse pratiche.

  - Opzione 1: può dare dei link agli studenti prima della lezione in modo che possano seguire, recuperare e vedere gli esercizi (in particolare se si sta seguendo il contenuto della lezione senza molte modifiche).
  - Opzione 2: non mostrare il sito web agli studenti durante la lezione, perché può essere fonte di distrazione: gli studenti potrebbero leggere invece di ascoltare, e avere un'altra finestra aperta è un ulteriore carico cognitivo.
  - In ogni caso, assicuratevi di puntare al sito web come riferimento post-workshop.

- Contenuto: A meno che non abbiate una quantità di tempo veramente generosa (4+ ore), è probabile che non riuscirete a coprire TUTTO il materiale di questa lezione in una sola sessione di mezza giornata. Pianificate in anticipo ciò che potreste saltare, ciò che volete davvero enfatizzare, ecc.

- Esercizi: Pensate in anticipo a come gestire gli esercizi durante la lezione. Come li assegnate (sito web, slide, dispensa)? Volete che tutti provino e poi mostriate la soluzione? Chiedete a un discente di mostrare la soluzione? Fate in modo che i gruppi facciano ciascuno un esercizio diverso e presentino le loro soluzioni?

- La [pagina di riferimento](../learners/reference.md) può essere stampata e data agli studenti come riferimento, a vostra scelta.

- Altra preparazione: Sentitevi liberi di aggiungere i vostri esempi o commenti collaterali, ma sappiate che non dovrebbe essere necessario: gli argomenti e i comandi possono essere insegnati come indicato nelle pagine delle lezioni. Se pensate che ci sia un punto in cui la lezione è carente, sentitevi liberi di segnalare un problema o di inviare una richiesta di pull.

## Note didattiche

- Una risorsa online davvero interessante! [http://explainshell.com/](https://explainshell.com/) analizza qualsiasi comando di shell digitato e mostra il testo di aiuto per ogni parte. Un ulteriore strumento manuale potrebbe essere [http://tldr.sh/](https://tldr.sh/) con brevi manuali molto descrittivi per i comandi di shell, utili soprattutto su Windows mentre si usa Git BASH dove `man` non può funzionare.

- Un'altra risorsa online molto interessante è [http://www.shellcheck.net](https://www.shellcheck.net), che controlla gli script di shell (sia caricati che digitati) per gli errori più comuni.

- Risorse per "dividere" la shell in modo che i comandi recenti rimangano in vista: [https://github.com/rgaiacs/swc-shell-split-window](https://github.com/rgaiacs/swc-shell-split-window).

- Il completamento della tabulazione sembra una cosa da poco: non lo è. Anche la ripetizione di vecchi comandi usando `!123` o `!wc` non è una cosa da poco, e nemmeno l'espansione dei caratteri jolly e i loop di `for`. Ognuno di essi è un'opportunità per ripetere una delle grandi idee della carpenteria software: se il computer *può* ripeterlo, qualche programmatore da qualche parte avrà quasi certamente costruito un modo per farlo *ripetere*.

- Costruire una pipeline con quattro o cinque stadi, poi inserirla in uno script di shell da riutilizzare e richiamare tale script all'interno di un ciclo `for`, è una grande opportunità per mostrare come il "sette più o meno due" si colleghi alla programmazione. Una volta che abbiamo capito come fare qualcosa di moderatamente complicato, lo rendiamo riutilizzabile e gli diamo un nome in modo che occupi solo uno slot nella memoria di lavoro invece di molti. È anche una buona occasione per parlare di programmazione esplorativa: piuttosto che progettare un programma a priori, possiamo fare alcune cose utili e poi decidere retroattivamente quali valgono la pena di essere incapsulate per un riutilizzo futuro.

- Se tutto va bene, si può far capire che le estensioni dei file servono essenzialmente ad aiutare i computer (e i lettori umani) a capire il contenuto dei file e non sono un requisito dei file (trattato brevemente in [Navigare tra file e directory](../episodi/02-filedir.md)). Questo può essere fatto nella sezione [Pipes e filtri](../episodes/04-pipefilter.md) mostrando che è possibile reindirizzare l'output standard a un file senza estensione .txt (ad esempio, lengths) e che il file risultante è ancora un file di testo perfettamente utilizzabile. Fate notare che se si fa doppio clic nella GUI, il computer probabilmente vi chiederà cosa volete fare.

- Per motivi di tempo dobbiamo tralasciare molte cose importanti, tra cui i permessi dei file, il controllo dei lavori e SSH. Se gli studenti hanno già compreso il materiale di base, questo può essere trattato utilizzando le lezioni online come linee guida. Queste limitazioni hanno anche conseguenze successive:

- È difficile discutere di `#!` (shebang) senza prima discutere dei permessi, cosa che non facciamo. anche `#!` è [piuttosto complicato][shebang], quindi anche se discutessimo di permessi, probabilmente non vorremmo discutere di `#!`.

- L'installazione di Bash e di un insieme ragionevole di comandi Unix su Windows comporta sempre un po' di confusione e frustrazione. Si consiglia di consultare l'ultima serie di linee guida per l'installazione e di provarle personalmente *prima* di tenere una lezione.

- Per impostazione predefinita, è possibile che al prompt dei comandi di Git Bash sia allegata una lunga serie di informazioni. Per ridurre il "rumore" e procedere con un prompt più ordinato, immettere il comando:

  ```bash
  PS1='$ '
  ```

- Sui computer Windows se `nano` non è stato installato correttamente con il [Software Carpentry Windows Installer][windows-installer] è possibile utilizzare `notepad` come alternativa. Ci sarà un'interfaccia GUI e le terminazioni di riga saranno trattate in modo diverso, ma per il resto, ai fini di questa lezione, `notepad` e `nano` possono essere usati in modo quasi intercambiabile.

- Su Windows, risulta che:

  ```bash
  $ cd
  $ cd Desktop
  ```

  metterà sempre qualcuno sul suo desktop (a meno che il suo computer non sia sottoposto a backup tramite OneDrive aziendale, vedi punto successivo). Chiedete loro di creare la cartella di esempio per gli esercizi di shell, in modo che possano trovarla facilmente e osservarne l'evoluzione.

- Se il backup di un computer Windows viene eseguito con OneDrive aziendale, il desktop dell'interfaccia grafica potrebbe essere rappresentato da una cartella all'interno di OneDrive, che non corrisponde al contenuto di `~/Desktop`. Il desktop di OneDrive dovrebbe essere accessibile utilizzando uno dei seguenti comandi (se il nome dell'azienda non è chiaro, cercate nell'output di `ls` per trovare la cartella giusta):

  ```bash
  $ cd "~/OneDrive - Name Of Enterprise/Desktop"
  $ cd "C:/Users/Username/OneDrive - Name Of Enterprise/Desktop"
  ```

  Un modo per capire se il computer utilizza questo tipo di configurazione è quello di guardare i file, le cartelle o i collegamenti sul desktop. Di solito l'icona contiene un simbolo di collegamento/freccia se si tratta di un link, o solo l'icona semplice se il file è semplicemente salvato nella cartella `Desktop`. I file sincronizzati con OneDrive contengono un simbolo aggiuntivo che indica lo stato di sincronizzazione (in genere frecce blu per "sincronizzazione in corso" o un segno di spunta verde per "sincronizzato").

- Rimanete all'interno dei comandi conformi a POSIX, come fa tutto il materiale didattico. La vostra particolare shell potrebbe avere estensioni che vanno oltre POSIX e che non sono disponibili su altre macchine, in particolare sugli emulatori bash di macOS e bash di Windows. Per esempio, POSIX `ls` non ha un'opzione `--ignore=` o `-I`, e POSIX `head` accetta `-n 10` o `-10`, ma non la forma lunga di `--lines=10`.

## Windows

L'installazione di Bash e di un insieme ragionevole di comandi Unix su Windows comporta sempre un po' di confusione e frustrazione. Consultate l'ultima serie di linee guida per l'installazione e provate voi stessi *prima* di tenere una lezione. Le opzioni che abbiamo esplorato includono:

1. [msysGit](https://msysgit.github.io/) (chiamato anche "Git Bash"),
2. [Cygwin](https://www.cygwin.com/),
3. utilizzando una macchina virtuale desktop e
4. far collegare gli studenti a una macchina Unix remota (in genere una macchina virtuale nel cloud).

Cygwin era l'opzione preferita fino alla metà del 2013, ma quando abbiamo iniziato a insegnare Git, msysGit ha dimostrato di funzionare meglio. Le macchine virtuali desktop e le macchine virtuali basate su cloud funzionano bene per gli studenti tecnicamente sofisticati e possono ridurre l'installazione e la configurazione all'inizio del workshop, ma:

1. non funzionano bene su macchine poco potenti,
2. confondono i principianti (perché cose semplici come il copia e incolla funzionano in modo diverso),
3. gli studenti lasciano il workshop senza un ambiente di lavoro sul sistema operativo di loro scelta, e
4. gli studenti potrebbero presentarsi senza aver scaricato la VM o la rete wireless potrebbe andare fuori uso (o diventare congestionata) durante la lezione.

Qualunque cosa usiate, vi preghiamo di *provarla* su una macchina Windows *prima* del vostro workshop: le cose potrebbero sempre essere cambiate a vostra insaputa dall'ultimo workshop. E fate anche uso del nostro [Software Carpentry Windows Installer][windows-installer].

[shebang]: https://www.in-ulm.de/~mascheck/various/shebang/
[windows-installer]: https://github.com/swcarpentry/windows-installer




