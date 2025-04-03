---
title: Configurazione
---


## Scaricare i file

Per seguire questa lezione è necessario scaricare alcuni file.

1. Scaricare [shell-lesson-data.zip][file zip] e spostare il file sul desktop.
2. decomprimere/estrarre il file. **Se avete bisogno di aiuto in questo passaggio, fatelo sapere al vostro istruttore**. Si dovrebbe ottenere una nuova cartella chiamata **`shell-lesson-data`** sul desktop.

## Installare il software

Se non avete già installato il software di shell, dovrete [scaricare e installare][installare_shell].

## Aprire una nuova shell

Dopo l'installazione del software

3. aprire un terminale. Se non siete sicuri di come aprire un terminale sul vostro sistema operativo, consultate le istruzioni seguenti.
4. Nel terminale digitare `cd` e premere il tasto <kbd>Return</kbd>. Questo passo assicura che si parta dalla cartella home come directory di lavoro.

Nella lezione si scoprirà come accedere ai file di dati contenuti in questa cartella.

::::::::::::::::::::::::::::::::::::::::: callout

## Dove digitare i comandi: Come aprire una nuova shell

La shell è un programma che ci permette di inviare comandi al computer e di ricevere l'output. Viene anche chiamata terminale o riga di comando.

Alcuni computer includono un programma Unix Shell predefinito. I passi che seguono descrivono alcuni metodi per identificare e aprire un programma Unix Shell se ne avete già uno installato. Esistono anche opzioni per identificare e scaricare un programma Unix Shell, un emulatore Linux/UNIX o un programma per accedere a Unix Shell su un server.

Se nessuna delle opzioni seguenti risponde alle vostre esigenze, provate a fare una ricerca online di: Shell Unix [modello di computer] [sistema operativo].


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::: solution

### Windows {#windows}

I computer con sistema operativo Windows non hanno automaticamente installato un programma di shell Unix. In questa lezione, vi invitiamo a usare un emulatore incluso in [Git per Windows][install_shell], che vi dà accesso sia ai comandi della shell Bash sia a Git.

Una volta installato, è possibile aprire un terminale eseguendo il programma Git Bash dal menu di avvio di Windows.

**Per utenti avanzati:**

In alternativa a Git per Windows si può scegliere [Installare il sottosistema Windows per Linux][wsl] che dà accesso a uno strumento a riga di comando della shell Bash in Windows 10 e superiori.

Si noti che i comandi del sottosistema Windows per Linux (WSL) possono differire leggermente da quelli mostrati nella lezione o presentati nel workshop.

::::::::::::

:::::::::::: solution

### MacOS {#macos}

Per un computer Mac con macOS Mojave o versioni precedenti, la shell Unix predefinita è Bash. Per un computer Mac con macOS Catalina o versioni successive, la shell Unix predefinita è Zsh. La shell predefinita è disponibile tramite il programma Terminale nella cartella Utilità.

Per aprire il Terminale, provare una o entrambe le seguenti opzioni:

- Nel Finder, selezionare il menu Vai, quindi selezionare Utilità. Individuare Terminale nella cartella Utilità e aprirlo.
- Utilizzare la funzione di ricerca del computer Mac 'Spotlight'. Cercare: `Terminal` e premere <kbd>Return</kbd>.

Per verificare se la propria macchina è impostata per utilizzare qualcosa di diverso da Bash, digitare `echo $SHELL` nella finestra del terminale.

Se la vostra macchina è impostata per usare qualcosa di diverso da Bash, potete eseguirlo aprendo un terminale e digitando `bash`.

[Come usare il terminale su un Mac][mac-terminal]

::::::::::::

:::::::::::: solution

### Linux {#linux}

La shell Unix predefinita per i sistemi operativi Linux è solitamente Bash. Sulla maggior parte delle versioni di Linux, è accessibile eseguendo [Gnome Terminal][gnome-terminal] o [KDE Konsole][kde-konsole] o [xterm], che possono essere trovati attraverso il menu delle applicazioni o la barra di ricerca. Se la vostra macchina è impostata per utilizzare qualcosa di diverso da Bash, potete eseguirlo aprendo un terminale e digitando `bash`.

::::::::::::

[zip-file]: data/shell-lesson-data.zip
[install_shell]: https://carpentries.github.io/workshop-template/install_instructions/#shell
[wsl]: https://learn.microsoft.com/en-us/windows/wsl/install
[mac-terminal]: https://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/
[gnome-terminal]: https://help.gnome.org/users/gnome-terminal/stable/
[kde-konsole]: https://konsole.kde.org/
[xterm]: https://en.wikipedia.org/wiki/Xterm




