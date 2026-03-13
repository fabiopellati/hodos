---
tipo-artefatto: template
documento: voce-attivita
descrizione: struttura canonica di una voce nel file attivita.md di un'unita' in fase P2
fase: P2
---

# Template — Voce Attivita'

Una voce di attivita' e' un contratto in due tempi: all'apertura definisce cosa
deve essere fatto e come verificarlo; alla chiusura documenta cosa e' stato
consegnato e ne verifica la conformita'. Va aggiunta in append al file
`attivita.md` dell'unita' corrente.

## Struttura — Apertura

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
- Non inserire stime di tempo ne' dettagli di diagnosi nella Richiesta.
- La sezione Consegna si aggiunge in append, mai in sostituzione del testo originale.
- Il campo Conformita' e' obbligatorio: valuta rispetto ai Criteri di verifica.
- Scostamenti parziali o non conformi devono essere motivati esplicitamente.
- Rilievi o anomalie emersi durante la realizzazione appartengono a una questione, non alla voce di attivita'.
