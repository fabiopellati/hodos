---
skill: arricchimento-firma-utente
client: Claude Code CLI
invocazione: /hodos-arricchimento-firma-utente
tipo: descrittivo
locale: it_IT
---

Arricchimento opzionale per opere in cui piu' operatori contribuiscono agli
stessi file di processo. Aggiunge la firma dell'autore a ogni contribuzione
tracciabile: voci di storia, commenti, note.

Questo skill e' descrittivo: non esegue azioni, non crea file. Fornisce le
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

La firma si applica a tutti i punti di contribuzione tracciabile:

**Voci di storia** (questioni.md, ogni aggiornamento di stato o nota):
```
- 2026-03-10 open — motivazione dell'apertura [Nome]
```

**Commenti** (sezione Commenti di questioni o note):
```
COMMENTO-001 — 2026-03-10 [Nome]
[testo del commento]
```

**Note** (notes.md, intestazione della nota):
```
## NOTA-042 — 2026-03-10 — Titolo sintetico [Nome]
```

---

## Formato

La firma e' `[Nome]` posizionata a fine riga dell'elemento a cui appartiene.
Fa parte del testo e segue le stesse regole di immutabilita' dell'elemento:
una voce di storia firmata non si modifica, un commento firmato non si modifica.

Il campo `Nome` corrisponde esattamente al valore dichiarato in `CLAUDE.md`.

---

## Casi non firmati

Non portano firma:

- Il corpo di una questione (Descrizione, Domande aperte, Impatto): sono
  scritti al momento dell'apertura e appartengono alla questione, non a un
  contributo successivo
- Il corpo immutabile di una nota (firmato nell'intestazione)
- Le entry del mastro: il mastro registra decisioni collettive dell'opera,
  non contributi individuali

---

## Rationale

In team con piu' operatori, sapere chi ha aperto una questione, chi ha scritto
un commento o chi ha aggiornato la storia e' informazione di processo rilevante.
La firma e' parte del testo e non e' separabile: garantisce che l'attribuzione
sia immutabile come l'elemento a cui appartiene.

La configurazione per opera (non globale) riflette il fatto che la firma e'
contestuale: lo stesso operatore puo' avere ruoli diversi in opere diverse,
o un'opera puo' essere a utente singolo e non richiedere attribuzione.
