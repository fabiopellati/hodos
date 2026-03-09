# Guida Operativa — Team Interno

Questa guida descrive come applicare il processo di gestione dei progetti
definito in `protocollo.md`. Si rivolge al team che gestisce il progetto
(Team-A). Non richiede l'uso di strumenti specifici ne' di AI.

Per i termini tecnici usati in questa guida, consulta `glossario.md`.

---

## Ciclo di vita

Hodos non prescrive un ciclo di vita a fasi. Il team definisce il proprio
percorso in base alla natura dell'opera.

Un percorso di riferimento opzionale basato su fasi sequenziali (P0 Definizione,
P1 Analisi, P2 Realizzazione, P3 Integrazione, P4 Consegna) e' disponibile
come arricchimento: consulta lo skill `fasi.md` per la struttura dettagliata,
la directory dei documenti attesi e le approvazioni.

---

## Gestione delle questioni

Ogni progetto mantiene `questioni.md` e `mastro.md` nella root documentale.

**Aprire una questione**: quando emerge un problema inatteso o una revisione
necessaria. Usare la skill `/questione` se disponibile, altrimenti compilare
manualmente seguendo la struttura definita nel protocollo.

**Aggiornare uno stato**: ad ogni cambio di stato aggiungere una nota nella
Storia che risponde al "perche'". Usare `/aggiorna-questione` se disponibile.

**Chiudere una questione**: quando il problema e' risolto, usare
`/aggiorna-questione` con stato `closed`. Lo skill rimuove la questione da
`questioni.md` e scrive l'entry corrispondente in `mastro.md`.

**Propagazione a ritroso**: se una questione in una fase avanzata invalida
assunzioni di fasi precedenti, aprire questioni collegate nelle fasi impattate.
Risolvere sempre dalla fase radice verso la fase piu' avanzata.

---

## Gestione delle RFC

**RFC outbound** (verso Team-B):
1. La questione passa a stato `pending-rfc`
2. Generare la RFC seguendo il template `rfc.md`
3. Consegnare il documento a Team-B
4. Quando Team-B compila la sezione Response RFC e restituisce il documento,
   verificare che il lavoro soddisfi i criteri di accettazione
5. Solo se la verifica e' positiva, aggiornare la questione a `in-progress`
   per completare il lavoro rimanente

**RFC inbound** (da Team-B):
1. Valutare la RFC ricevuta: determinare fase e distribuzione del lavoro
2. Aprire una questione nella fase appropriata
3. Svolgere il lavoro nel normale ciclo di realizzazione
4. Compilare la sezione Response RFC e restituire il documento a Team-B
5. Chiudere la questione
