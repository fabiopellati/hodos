Gestisci un item nel backlog di un'unita' in fase P2 — Realizzazione.

Il backlog item e' un contratto in due tempi tra chi pianifica e chi realizza:
all'apertura definisce cosa deve essere fatto e come verificarlo; alla chiusura
documenta cosa e' stato consegnato e ne verifica la compliance rispetto alla richiesta.

## 1. Trova il file backlog

Cerca `backlog.md` nella directory dell'unita' corrente
(es. `docs/unita'/[nome]/backlog.md`).

Se non esiste, chiedi all'utente dove crearlo prima di procedere.

## 2. Determina l'operazione

Se il contesto del messaggio non indica chiaramente l'operazione,
usa AskUserQuestion con queste opzioni:
- "Apri nuovo item" — si sta pianificando un task di realizzazione
- "Chiudi item esistente" — si sta documentando la consegna e verificando la compliance

---

## Apertura item

Leggi il file per determinare il prossimo numero BL disponibile (univoco).
Aggiungi in append al file:

```markdown
## BL-{N} — {Titolo breve}

### Richiesta

{Cosa deve essere realizzato e perche'. Descrive il "cosa" e il "perche'",
non il "come". Se la realizzazione e' delegata, questo e' il documento
di riferimento per chi realizza.}

### Criteri di verifica

{Come si verifica che la realizzazione soddisfi la richiesta. Condizioni
osservabili e misurabili. Usato alla chiusura per la verifica di compliance.}

### Note

{Vincoli rilevanti, riferimenti utili. Opzionale.}
```

**Regole:**
- La Richiesta descrive il risultato atteso, non i passi realizzativi
- I Criteri di verifica devono essere verificabili da chi non ha realizzato
- Non inserire stime di tempo ne' dettagli di diagnosi

---

## Chiusura item

Identifica l'item da chiudere (per numero BL o titolo).

Se il messaggio non specifica quale item chiudere, usa AskUserQuestion
mostrando la lista degli item aperti come opzioni.

### Individua gli artefatti da verificare

Prima di valutare la compliance, leggi il `CLAUDE.md` nella directory corrente
e cerca la sezione `Percorsi`. Il campo `Artefatti` indica dove cercare gli
output da verificare rispetto ai Criteri di verifica.

- Se il path e' definito: usa quella directory come base per la verifica
- Se il campo e' "nessuno": la compliance si valuta solo su documenti
- Se `CLAUDE.md` non esiste o la sezione manca: chiedi all'utente dove
  si trovano gli artefatti prima di procedere

### Scrivi la sezione di consegna

Aggiungi in append all'item:

```markdown
### Consegna [{YYYY-MM-DD}]

**Compliance**: conforme | parziale | non conforme

{Descrizione di quanto realizzato. Se parziale o non conforme, documenta
gli scostamenti rispetto alla Richiesta e la motivazione.}
```

**Regole:**
- NON modificare mai il testo originale dell'item (Richiesta, Criteri, Note)
- La sezione Consegna si aggiunge in append, mai in sostituzione
- Il campo Compliance e' obbligatorio: valuta rispetto ai Criteri di verifica
- Scostamenti parziali o non conformi devono essere motivati esplicitamente

---

## Cosa NON appartiene al backlog

- Finding, anomalie o problemi inattesi emersi durante la realizzazione — usare /issue
- Stime di tempo
- Note operative di sessione
- Dettagli di diagnosi
