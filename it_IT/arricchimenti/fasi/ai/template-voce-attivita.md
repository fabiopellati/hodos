---
tipo-artefatto: template
documento: voce-attivita
descrizione: struttura canonica di una voce nel file 2-attivita.md di un'unità in fase P2
fase: P2
---

# Template — Voce Attività

**Arricchimento**: questo template appartiene all'arricchimento fasi (P2).
Prima di usarlo, verificare che il CLAUDE.md dell'opera includa questo
arricchimento nella sezione `Arricchimenti abilitati`. Se non è abilitato,
non proporre voci di attività all'operatore.

Una voce di attività è un contratto in due tempi: all'apertura definisce cosa
deve essere fatto e come verificarlo; alla chiusura documenta cosa è stato
consegnato e ne verifica la conformità. Va aggiunta in append al file
`2-attivita.md` dell'unità corrente.

## Struttura — Apertura

```markdown
## BL-{N} — {Titolo breve}

### Richiesta

{Cosa deve essere realizzato e perché. Descrive il "cosa" e il "perché",
non il "come". Se la realizzazione è delegata, questo è il documento
di riferimento per chi realizza.}

### Criteri di verifica

{Come si verifica che la realizzazione soddisfi la richiesta. Condizioni
osservabili e misurabili. Usato alla chiusura per la verifica di conformità.}

### Note

{Vincoli rilevanti, riferimenti utili. Opzionale.}
```

## Struttura — Chiusura

Aggiungere in append alla voce aperta, senza modificare il testo esistente:

```markdown
### Consegna [{YYYY-MM-DD}]

**Conformita'**: {conforme | parziale | non conforme}

{Descrizione di quanto realizzato. Se parziale o non conforme, documenta
gli scostamenti rispetto alla Richiesta e la motivazione.}
```

## Regole

- La Richiesta descrive il risultato atteso, non i passi realizzativi.
- I Criteri di verifica devono essere verificabili da chi non ha realizzato.
- Non inserire stime di tempo né dettagli di diagnosi nella Richiesta.
- La sezione Consegna si aggiunge in append, mai in sostituzione del testo originale.
- Il campo Conformità è obbligatorio: valuta rispetto ai Criteri di verifica.
- Scostamenti parziali o non conformi devono essere motivati esplicitamente.
- Rilievi o anomalie emersi durante la realizzazione appartengono a una questione, non alla voce di attività.
