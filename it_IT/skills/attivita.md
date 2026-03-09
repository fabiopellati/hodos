---
skill: attivita
client: Claude Code CLI
invocazione: /hodos-attivita
tipo: operativo
locale: it_IT
---

Gestisci una voce nel file attivita.md di un'unita' in fase P2 — Realizzazione.

La voce di attivita' e' un contratto in due tempi tra chi pianifica e chi realizza:
all'apertura definisce cosa deve essere fatto e come verificarlo; alla chiusura
documenta cosa e' stato consegnato e ne verifica la conformita' rispetto alla richiesta.

## 1. Trova il file attivita'

Cerca `attivita.md` nella directory dell'unita' corrente
(es. `documenti/unita/[nome]/attivita.md`).

Se non esiste, chiedi all'utente dove crearlo prima di procedere.

## 2. Determina l'operazione

Se il contesto del messaggio non indica chiaramente l'operazione,
usa AskUserQuestion con queste opzioni:
- "Apri nuova voce" — si sta pianificando un task di realizzazione
- "Chiudi voce esistente" — si sta documentando la consegna e verificando la conformita'

---

## Apertura voce

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
osservabili e misurabili. Usato alla chiusura per la verifica di conformita'.}

### Note

{Vincoli rilevanti, riferimenti utili. Opzionale.}
```

**Regole:**
- La Richiesta descrive il risultato atteso, non i passi realizzativi
- I Criteri di verifica devono essere verificabili da chi non ha realizzato
- Non inserire stime di tempo ne' dettagli di diagnosi

---

## Chiusura voce

Identifica la voce da chiudere (per numero BL o titolo).

Se il messaggio non specifica quale voce chiudere, usa AskUserQuestion
mostrando la lista delle voci aperte come opzioni.

### Individua gli artefatti da verificare

Prima di valutare la conformita', leggi il `CLAUDE.md` nella directory corrente
e cerca la sezione `Percorsi`. Il campo `Artefatti` indica dove cercare gli
output da verificare rispetto ai Criteri di verifica.

- Se il path e' definito: usa quella directory come base per la verifica
- Se il campo e' "nessuno": la conformita' si valuta solo su documenti
- Se `CLAUDE.md` non esiste o la sezione manca: chiedi all'utente dove
  si trovano gli artefatti prima di procedere

### Scrivi la sezione di consegna

Aggiungi in append alla voce:

```markdown
### Consegna [{YYYY-MM-DD}]

**Conformita'**: conforme | parziale | non conforme

{Descrizione di quanto realizzato. Se parziale o non conforme, documenta
gli scostamenti rispetto alla Richiesta e la motivazione.}
```

**Regole:**
- NON modificare mai il testo originale della voce (Richiesta, Criteri, Note)
- La sezione Consegna si aggiunge in append, mai in sostituzione
- Il campo Conformita' e' obbligatorio: valuta rispetto ai Criteri di verifica
- Scostamenti parziali o non conformi devono essere motivati esplicitamente

---

## Cosa NON appartiene all'attivita'

- Rilievi, anomalie o problemi inattesi emersi durante la realizzazione — usare /questione
- Stime di tempo
- Note operative di sessione
- Dettagli di diagnosi
