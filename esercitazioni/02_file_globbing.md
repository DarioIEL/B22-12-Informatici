# Laboratorio Linux: gestione file e globbing

**Prerequisiti:** terminale bash su Linux. Lavorare sempre dentro `~/lab_linux`.
**Regola d'oro:** prima di un `mv` o `cp` con un pattern, controllare con `echo pattern` quali file verranno toccati.

---

## Parte A – Creazione di file e cartelle

**A1.** Crea la cartella `lab_linux` nella tua home ed entraci.

**A2.** Crea un file vuoto `primo.txt` e verifica con `ls -l` che la dimensione sia 0.

**A3.** Senza usare un editor, crea `saluto.txt` contenente la riga `Ciao Linux`. Visualizzane il contenuto.

**A4.** Aggiungi a `saluto.txt` la riga `Seconda riga` senza cancellare la prima.
*Domanda:* cosa succede se usi `>` al posto di `>>`?

**A5.** Con **un solo comando** crea la struttura `progetto/src`, `progetto/docs`, `progetto/test`.

**A6.** Con **un solo comando** crea `capitolo1.md` … `capitolo5.md` dentro `progetto/docs`.

**A7.** Esegui `ls -l saluto.txt`, attendi un minuto, poi `touch saluto.txt` e rilancia `ls -l`.
*Domanda:* cosa è cambiato? Il contenuto è stato modificato?

## Parte B – Copia

**B1.** Copia `saluto.txt` in `saluto_copia.txt`.

**B2.** Copia `saluto.txt` dentro `progetto/docs/` mantenendo lo stesso nome.

**B3.** Copia l'intera cartella `progetto` in `progetto_backup`. Prova prima **senza** opzioni: che errore ottieni? Come si risolve?

**B4.** Ricopia `saluto.txt` su `saluto_copia.txt` facendo in modo che il sistema chieda conferma prima di sovrascrivere.

**B5.** Copia `saluto.txt` in `saluto_old.txt` conservando la data di modifica originale. Verifica con `ls -l`.

## Parte C – Spostamento e rinomina

**C1.** Rinomina `primo.txt` in `vuoto.txt`.

**C2.** Sposta `saluto_copia.txt` in `progetto/test/`.

**C3.** Con **un solo comando** sposta `progetto/test/saluto_copia.txt` in `progetto/src/` rinominandolo `benvenuto.txt`.

**C4.** Rinomina la cartella `progetto_backup` in `backup_ottobre`.
*Domanda:* perché `cp` su una cartella richiede `-r` e `mv` no?

**C5.** Sposta `saluto_old.txt` in `progetto/docs/` chiedendo conferma in caso di sovrascrittura.

---

## Parte D – Ricerca con il globbing

Prepara il dataset (copia e incolla):

```bash
mkdir -p ~/lab_linux/archivio && cd ~/lab_linux/archivio
touch relazione.txt relazione.doc relazione_finale.txt appunti.txt Appunti.TXT
touch foto_{01..12}.jpg foto_{01..03}.png
touch data1.csv data2.csv data10.csv dataA.csv
touch script.sh backup.sh.bak note .nascosto.txt
ls -a
```

Usa solo `ls` (o `echo`) con un pattern. Per ogni esercizio scrivi prima **quali file ti aspetti**, poi verifica.

| # | Trova… |
|---|---|
| D1 | tutti i file `.txt` (minuscolo) |
| D2 | tutti i file il cui nome inizia con `relazione` |
| D3 | i file `relazione` con un'estensione di esattamente 3 caratteri |
| D4 | i file `data` seguiti da **un solo** carattere qualsiasi, estensione `.csv` |
| D5 | i file `data` seguiti da **una sola cifra** |
| D6 | i file `data` seguiti da un solo carattere che **non** è una cifra |
| D7 | le foto `.jpg` dalla 01 alla 05 |
| D8 | le foto `.jpg` dalla 10 alla 12 |
| D9 | tutte le foto, sia `.jpg` sia `.png` |
| D10 | tutti i file `.txt` senza distinguere maiuscole/minuscole |
| D11 | i file che terminano esattamente in `.sh` |
| D12 | i file nascosti (escludendo `.` e `..`) |
| D13 | un pattern che non corrisponde a nulla, es. `*.xyz`. Cosa succede? |

*Domande di riflessione:*
- Perché in D1 non compare `.nascosto.txt`?
- Perché in D4 non compare `data10.csv`?

## Parte E – Globbing + copia/spostamento

Sempre in `~/lab_linux/archivio`:

**E1.** Crea le cartelle `immagini`, `documenti`, `dati`.

**E2.** Sposta tutte le foto (jpg e png) in `immagini/` con un solo comando.

**E3.** Copia tutti i file `.txt` e `.TXT` in `documenti/`.

**E4.** Sposta in `dati/` solo i CSV con suffisso numerico a una cifra.

**E5.** Esegui `cp *.txt copia_testi` (cartella **non** esistente). Cosa succede? Ripeti con `cp relazione.txt copia_singola`. Perché il comportamento è diverso?

**E6.** Dentro `immagini/`, sposta in una nuova sottocartella `primo_trimestre/` le foto da 01 a 03, sia jpg sia png.

## Parte F – Sfida: ricerca ricorsiva

**F1.** Da `~/lab_linux`, elenca **tutti** i file `.txt` in qualsiasi sottocartella usando solo il globbing.

**F2.** Ottieni lo stesso risultato con `find`. Prova anche senza virgolette attorno al pattern, lanciando il comando da `~/lab_linux/archivio`: perché il risultato cambia?