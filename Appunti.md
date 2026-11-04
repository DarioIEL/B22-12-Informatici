# Appunti Linux  
In questa sezione prenderemo appunti circa  Linux e la CLI

## Appunti teorici da sapere

#### Struttura iniziale Shell
```shell
dario@UbuntuDario:~$
```
dario --> nome utente
UbuntuDario --> nome sitema op
~ --> directory in cui mi trovo (nel caso della ~ sono nella **HOME DIRECTORY**)

#### Differenze ~ o /
 - `~` è la Home Directory, cioè la cartella utente.
 - `/` è la Root Directory, cioè la cartella iniziale del File System


#### Variabile Locale e Variabile d'ambiente
Def. Variabile: la variabile è uno slot di memoria al quale assegnamo un nome e nel quale registriamo un'informazione che può cambiare. 

**Variabile Locale**: parametri di configurazione validi esclusivamente all'interno del processo o della sessione di shell in cui vengono creati.
Per impostare una variabile locale mi basta assegnare un nome e un valore.
```shell
nomeUser='Dario'
```
Per richiamare una variabile uso`echo $nomeVariabile`
```shell
echo $nomeUser
```

**Variabile Globale o d'ambiente** : valori dinamici memorizzati nel sistema operativo che i programmi e i processi in esecuzione possono leggere per ottenere informazioni sul contesto operativo
```shell
echo $USER
echo $PATH
echo $LOGNAME
echo $HISTSIZE
```
Solitamente le variabile d'ambiente sono scritte in maiuscolo

`echo` mostra a video il valore di una variabile 

#### Muoversi all'interno del file System
Differenze tra **path relativo** e **path assoluto**

#### Tipologie di comandi (cap 5.5 su Netacad)

## Comandi Shell Bash

```bash
comando [opzioni] [argomenti]
```

##### **ls**
- `ls` serve a listare il contenuto di una cartella: vedere il contenuto 

Opzioni più comuni per il comando `ls`
- `-a` permette di vedere file e cartelle nascoste
- `-l` long listing: fornisce più informazioni
- `-h` human reading: il peso di file e cartelle è espresso con le unità di misura
- `-r`reverse: inverte l'ordine di output


**Attenzione**: posso combinare le opzioni

##### Esempio
```shell
$ ls Documents -a
```


#### **history**
Con questo comando vedo la cronologia degli ultimi comandi lanciati.
Di default contiene 1000 comandi precedenti. Per verificare quanto è grande questa history devo richiamare la variabile d'ambiente HISTSIZE
```shell
echo $HISTSIZE
```

## Muoversi nel File System
Come attraversare l'alberatura del sistema operativo senza perdersi

##### Dove mi trovo ? 
```shell
pwd
```
Con il comando `pwd` stampo (scrive in console) la cartella nella quale mi trovo

### File System
E' la struttura di tutte le cartelle all'interno del mio sistema operativo

![](./img/filesys.png)

Due cartella fondamentali:
- **root (identificata con / ) directory**. La cartella che contiene tutto, quella iniziale
- **home (identificata con ~ ) directory**. La cartella che contiene le cartelle dei singoli utenti. Poi ogni cartella utente ha una struttura fissa (Download, Documenti, Musica, Immagini, ecc..)


### cd (Change Directory)
Con il comando `cd` mi muovo all'interno del filesystem. 
```shell
cd [option] [path]
```
path: percorso

**shortcut:**
- `./` "a partire dalla cartella in cui mi trovo". Di solito si usa per i path relativi

- `../` "a partire dalla cartella superiore"

### Path Relativo e Path Assoluto
Si chiama **path relativo** un percorso relativo alla cartella in cui mi trovo. Cioè il percorso comincia con la working directory

SI chiama **path assoluto** il percorso che comincia con / , cioè a partire dalla root directory

**Esempio**
Questo sotto è un path relativo perché parte dalla cartella ~ (home directory)
```shell
cd ~/Music/anni_70/rock
```

Questo sotto è un percorso assoluto perché parte dalla cartella / (root)
```shell
cd /home/utente/Music/anni_80/pop
```

#### Esercizio
Ti trovi nella seguente cartella `:~/Music/anni_70/pop` inserita in un file system standard. Voglio andare alla cartella `Pictures` contenuta nella home directory. Scrivi tutti i percorsi che ti vengono in mente per arrivare lì. 


---
### Installazione di tree
Installare `tree` con `sudo apt install tree` per poter " disegnare l'alberatura di un file system
**Osservazione**: se voglio interrompere l'esecuzione di un comando `Ctrl + C` 

---
#### Esercizio:
posizionati nella cartella `~/Music/anni_70/pop` dall'interno di questa cartella lancia il comando `tree` per poter vedere come è fatta la cartella `snap`

---
#### Esercizio:
Posizionati nella **root directory** da qui leggi il contenuto della cartella Music utilizzando sia il comando `ls` sia `tree`. Utilizza tutti i path possibili.
Spostati nella cartella Music, dall'interno di quest'ultima lista il contenuto della cartella `etc` che si trova in `/`. Utilizza tutti i path possibili.

## Manuali Comandi e Aiuto (`man` e `help`)

## Globbing
Il globbing aiuta tantissimo alla manipolazione dei file. Per Globbing si intende l'insieme di caratteri e simboli che hanno un valore particolare per la nostra shell.

Con il globbing è possibile risalire a gruppi di file richiamandoli per particolari pattern nel loro nome.

Questi caratteri speciali possono essere usati con tutti i comandi

### carattere " * "
Sostituisce tutti i caratteri per qualsiasi quantità. 
**esempio:** Messo davanti ad un'estensione file trova tutti i file con quell'estensione. Può sostituire anche parti di nomi file o cartelle 

### carattere " ? "
Va usato in numero esatto e sostituisce qualsiasi altro carattere.
**Esempio:** t???? --> sto cercando tutto ciò che comincia con t ed è seguito da esettamente altri 4 caratteri e basta.

### carattere [ ]
Con le parentesi quadre ho un range di ricerca
**esempio:** `[dl]*` trova tutti i file o cartelle che cominciano con **d** ed **l**
**esempio:** `[d-l]*` trova tutti i file o cartelle che cominciano con tutte le lettere all'interno dell'intervallo tra **d** ed **l** ---> d, e , f, g, h, i, l
 

## Manipolazione dei File
### Creazione dei file
I file, di qualsiasi estensione si creano con il comando `touch nomeFile.txt`

### Creazione di cartelle
Uso il comando `mkdir nome_cartella` 

### Copia File
Comando `cp sorgente destinazione`. La copia non è un comando distruttivo. Nella copia non si ottiene nessun output (no news is a good news). **Attenzione**: quando copio, se esiste già un file nella destinazione, sovrascrivo il contenuto.

**Evitare la sovrascrittura**: quando si copia possiamo evitare la sovrascrittura in due modi:
- `cp -i src dest` con -i mi faccio domandare se voglio sovrascrivere o meno in copia
- `cp -n src dest` con -n evito completamente la sovrascrittura. Quindi file già esistenti non verranno copiati

### Copia Cartelle
Si usa il comando `cp -r` dove -r sta per recursive e serve a copia integralmente una cartella. 

### Sposta e rinomina file
Comando `mv src dest`. Lo "sposta" è un comando distruttivo: nello spostamento il file viene eliminato dalla cartella sorgente e spostato nella cartella di destinazione. Questo comando serve anche a spostare un file rinominandolo.
**Esempio rinomina**: per SOLO rinominare un file posso eseguire il comando `mv` senza fornire una destinazione `mv la_divina.txt la_divina_commedia.txt`. Att posso rinominare un file anche spostandolo in un'altra cartella.

Anche in questo caso c'è il rischio di sovrascrittura. Stesse opzioni della copia:
- i (interactive) chiede all'utente
- n (No Clobber) non sovrascrive
- v (Verbose) Mostra il risultato


### Rimuovere un file
Comando `rm sorgente`

### Rimuovere una cartella
Comando `rm -r sorgente`

### STDIN e STDOUT
Con l'uso delle parentesi angolari `>` e `>>` posso creare al volo dei file con dei contenuti testuali.
**Esempio** `echo "Ciao Mondo" > saluto.txt` crea un file con la riga 'Ciao Mondo' all'interno

**Esempio** `echo "Ciao studente >> saluto.txt` aggiunge una riga di testo senza cancellare il contenuto precedente