# Guida Operativa — Team Interno

Questa guida descrive come applicare il processo di gestione dei progetti
definito in `protocollo.md`. Si rivolge al team che gestisce il progetto
(Team-A). Non richiede l'uso di strumenti specifici né di AI.

Per i termini tecnici usati in questa guida, consulta `glossario.md`.

---

## Ciclo di vita

Hodos non prescrive un ciclo di vita a fasi. Il team definisce il proprio
percorso in base alla natura dell'opera.

Un percorso di riferimento opzionale basato su fasi sequenziali (P0 Definizione,
P1 Analisi, P2 Realizzazione, P3 Integrazione, P4 Consegna) è disponibile
come arricchimento: consulta lo skill `arricchimento-fasi.md` per la struttura dettagliata,
la directory dei documenti attesi e le approvazioni.

---

## Gestione delle questioni

Ogni progetto mantiene `questioni.md` e `mastro.md` nella root documentale.

**Aprire una questione**: quando emerge un problema inatteso, una conoscenza
nuova da tracciare o una revisione necessaria. Usare lo skill `/hodos-questione`
se disponibile, altrimenti compilare manualmente seguendo la struttura definita
nel protocollo.

**Aggiornare uno stato**: ad ogni cambio di stato aggiungere una nota nella
Storia che risponde al "perché". Usare `/hodos-aggiorna-questione` se
disponibile.

**Chiudere una questione**: quando il problema è risolto, usare
`/hodos-aggiorna-questione` con stato `closed`. Lo skill rimuove la questione da
`questioni.md` e scrive la voce corrispondente in `mastro.md`.

**Confine dei ruoli su `pending-approval`**: è chi realizza a portare la
questione a `pending-approval` — è il segnale di consegna verso chi governa.
Il ciclo completo: chi governa apre e assegna, chi realizza porta a
`in-progress`, chi realizza porta a `pending-approval`, chi governa chiude
e scrive nel mastro.

**Propagazione a ritroso**: se una questione in una fase avanzata invalida
assunzioni di fasi precedenti, aprire questioni collegate nelle fasi impattate.
Risolvere sempre dalla fase radice verso la fase più avanzata.

---

## Gestione delle RFC

**RFC outbound** (verso Team-B):

1. Portare la questione allo stato `pending-rfc`
2. Generare la RFC con lo skill `/hodos-rfc` o seguendo il template
3. Consegnare il documento a Team-B
4. Quando Team-B compila la sezione Response RFC e restituisce il documento,
   verificare che il lavoro soddisfi i criteri di accettazione
5. Solo se la verifica è positiva, aggiornare la questione per procedere
   con il lavoro rimanente; se la RFC esauriva l'intera questione, chiuderla

**Confine dei ruoli sulla ricezione RFC**: la risposta a una RFC outbound torna
a chi governa, non a chi realizza. La questione `pending-rfc` è stata aperta
da chi governa; la risposta viene interpretata da chi governa, che valuta le
implicazioni e apre le questioni figlie se necessario. Chi realizza può
materialmente ricevere il documento, ma l'interpretazione e le decisioni di
processo appartengono a chi governa.

**RFC inbound** (da Team-B):

1. Valutare la RFC ricevuta: determinare a quale fase appartiene il lavoro
   richiesto
2. Aprire una questione nella fase appropriata
3. Svolgere il lavoro nel normale ciclo di realizzazione
4. Compilare la sezione Response RFC e restituire il documento a Team-B
5. Chiudere la questione
