---
skill: arricchimento-firma-utente
client: Claude Code CLI
invocazione: /hodos-arricchimento-firma-utente
tipo: descrittivo
locale: it_IT
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

**Voci di storia** (questioni.md, ogni aggiornamento di stato):
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

**Note** (notes.md):
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

La firma fa parte dell'elemento a cui appartiene e segue le stesse regole
di immutabilità: una voce di storia firmata non si modifica, un commento
firmato non si modifica.

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
l'attribuzione sia immutabile come l'elemento a cui appartiene.

Il formato differenziato per tipo di elemento riflette i vincoli strutturali
di ciascuno: le voci di storia sono righe singole e richiedono firma inline;
commenti e note sono blocchi e possono ospitare un campo header strutturato,
più estraibile e componibile con altri arricchimenti.

La configurazione per opera (non globale) riflette il fatto che la firma è
contestuale: lo stesso operatore può avere ruoli diversi in opere diverse,
o un'opera può essere a utente singolo e non richiedere attribuzione.
