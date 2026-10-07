---
tipo-artefatto: skill
documento: arricchimento-firma-utente
descrizione: arricchimento opzionale che aggiunge la firma dell'autore alle contribuzioni
  tracciabili, per opere in cui più operatori toccano gli stessi file di processo
skill: arricchimento-firma-utente
client: Claude Code CLI
invocazione: /hodos-arricchimento-firma-utente
tipo: descrittivo
locale: it_IT
autorita: normativa
---

Arricchimento opzionale per opere in cui più operatori contribuiscono agli
stessi file di processo. Aggiunge la firma dell'autore a ogni contribuzione
tracciabile: voci di storia, commenti, note.

Questo skill è descrittivo: non esegue azioni, non crea file. Fornisce le
istruzioni necessarie all'AI per applicare la firma quando l'opera lo adotta.

---

## Adozione

L'opera dichiara la firma nel proprio `CLAUDE.md` con questa riga:

```
**Firma operatore**: [Nome]
```

Una volta presente, l'AI applica automaticamente la firma a ogni contribuzione
scritta nella sessione corrente.

---

## Elementi con firma

La firma si applica a tutti i punti di contribuzione tracciabile, con formato
differenziato per tipo di elemento.

**Voci di storia** (sezione `Storia` del file della questione in `questioni/`,
a ogni aggiornamento di stato):
```
- 2026-03-10 open [Nome] — motivazione dell'apertura
```
La firma precede il separatore `—` per garantire allineamento di colonna
ordinato nei log multi-operatore. I brackets `[]` sono mantenuti per
facilitare lo scanning visivo.

**Commenti** (sezione Commenti di questioni o note):
```
COMMENTO-001 — 2026-03-10 [Nome]
[testo del commento]
```
La firma è inline nell'header del commento, dopo la data.

**Note** (corpo del file della nota in `note/`):
```
## NOTA-042 — 2026-03-10 — Titolo sintetico
**Autore**: Nome
[corpo della nota]
```
La firma è un campo header strutturato, prima riga del blocco dopo
l'intestazione. Non fa parte del titolo.

---

## Formato

Il campo `Nome` corrisponde esattamente al valore dichiarato in `CLAUDE.md`.

La firma fa parte dell'elemento a cui appartiene e non si modifica mai: una
voce di storia firmata non si modifica, e la firma di un commento resta quella
che era anche quando il testo del commento è correggibile, come nella questione
aperta (Art. 4 comma 9), perché la correzione ripara la redazione e non
l'attribuzione.

---

## Arricchimenti multipli e storia

Gli arricchimenti possono aggiungere campi header a questioni e note
liberamente. La voce di storia tuttavia riporta solo i metadati
significativi per la storia dell'elemento: informazioni accessorie
restano nell'header e non compaiono nella storia.

---

## Casi non firmati

Non portano firma:

- Il corpo di una questione (Descrizione, Domande aperte, Impatto): sono
  scritti al momento dell'apertura e appartengono alla questione, non a un
  contributo successivo
- Il corpo immutabile di una nota (firmato nell'header)
- Le entry del mastro: il mastro registra decisioni collettive dell'opera,
  non contributi individuali

---

## Rationale

In team con più operatori, sapere chi ha aperto una questione, chi ha scritto
un commento o chi ha aggiornato la storia è informazione di processo rilevante.
La firma è parte dell'elemento e non è separabile: garantisce che
l'attribuzione resti immutabile anche dove il testo dell'elemento è
correggibile.

Il formato differenziato per tipo di elemento riflette i vincoli strutturali
di ciascuno: le voci di storia sono righe singole e richiedono firma inline;
commenti e note sono blocchi e possono ospitare un campo header strutturato,
più estraibile e componibile con altri arricchimenti.

La configurazione per opera (non globale) riflette il fatto che la firma è
contestuale: lo stesso operatore può avere ruoli diversi in opere diverse,
o un'opera può essere a utente singolo e non richiedere attribuzione.
