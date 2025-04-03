---
title: Discussione
---


## Zuppa alfabetica

Se il comando per scoprire chi siamo è `whoami`, il comando per scoprire dove siamo dovrebbe chiamarsi `whereami`, perché invece è `pwd`? La risposta abituale è che all'inizio degli anni '70, quando Unix è stato sviluppato, ogni battuta contava: i dispositivi dell'epoca erano lenti e il backspacing su una telescrivente era così doloroso che ridurre il numero di battute per ridurre il numero di errori di battitura era in realtà un vantaggio per l'usabilità. La realtà è che i comandi sono stati aggiunti a Unix uno alla volta, senza un piano generale, da persone immerse nel suo gergo. Il risultato è incoerente come lo spelling di roolz uv Inglish, ma ormai ci siamo abituati.

## Codici di controllo del lavoro

La shell accetta alcuni comandi speciali che consentono agli utenti di interagire con i processi o i programmi in esecuzione. È possibile inserire ciascuno di questi "codici di controllo" tenendo premuto il tasto `Ctrl` e poi premendo uno dei caratteri di controllo. In altri tutorial, si può vedere il termine `Control` o `^` usato per rappresentare il tasto `Ctrl` (ad esempio, i seguenti sono tutti equivalenti `Ctrl-C`, `Ctrl+C`, `Control-C`, `Control+C`, `^C`).

- `Ctrl-C`: interrompe e annulla un programma in esecuzione. È utile se si vuole annullare un comando che richiede troppo tempo per essere eseguito.

- `Ctrl-D`: indica la fine di un file o di un flusso di caratteri che si sta inserendo sulla riga di comando. Ad esempio, abbiamo visto in precedenza che il comando `wc` conta le righe, le parole e i caratteri di un file. Se si digita semplicemente `wc` e si preme il tasto Invio senza fornire un nome di file, allora `wc` penserà che vogliamo analizzare tutto ciò che digitiamo successivamente. Dopo aver digitato la nostra opera magna direttamente nel prompt della shell, possiamo digitare Ctrl-D per dire a `wc` che abbiamo finito e che vogliamo vedere i risultati del conteggio delle parole.

- `Ctrl-Z`: Sospende un processo ma non lo termina. Si può quindi usare il comando `fg` per riavviare il lavoro in primo piano.

Per i nuovi utenti della shell, questi codici di controllo possono sembrare avere tutti lo stesso effetto: fanno "sparire" le cose Ma è utile capire le differenze. In generale, se qualcosa è andato storto e si vuole solo riavere il prompt della shell, è meglio usare `Ctrl-C`.

## Altre shell

Prima che Bash diventasse popolare alla fine degli anni Novanta, gli scienziati usavano ampiamente (e alcuni usano ancora) un'altra shell, C-shell o Csh. Bash e Csh hanno caratteristiche simili, ma le loro regole di sintassi sono diverse e questo le rende incompatibili tra loro. Da allora sono apparse altre shell, tra cui ksh, zsh e altre; sono per lo più compatibili con Bash e Bash è la shell predefinita nella maggior parte delle moderne implementazioni di Unix (compresi la maggior parte dei pacchetti che forniscono strumenti simili a Unix per Windows), ma se si riscontrano strani errori negli script di shell scritti da colleghi, è bene verificare per quale shell sono stati scritti.

## Configurazioni di Bash

Volete personalizzare percorsi, variabili d'ambiente, alias e altri comportamenti della vostra shell? Questo eccellente post del blog "[Bash Configurations Demystified][bash-demystified]" di Dalton Hubble contiene suggerimenti, trucchi e indicazioni su come evitare i pericoli.

[bash-demystified]: https://blog.dghubble.io/posts/.bashprofile-.profile-and-.bashrc-conventions/




