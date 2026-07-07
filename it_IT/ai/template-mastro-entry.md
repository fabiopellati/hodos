---
tipo-artefatto: template
documento: mastro-entry
descrizione: struttura canonica di un'entry nel mastro.md, scritta alla chiusura di una questione
fase: trasversale
---

# Template — Voce del Mastro

Una voce del mastro documenta la chiusura di una questione.
Vive nel proprio file `mastro/Q{NNN}-slug.md`, ottenuto spostando il file
della questione da `questioni/` a `mastro/` alla chiusura.
Il corpo della voce è immutabile; il frontmatter è mutabile (doppio regime,
Art. 10 del protocollo).

## Norma sul Percorso

Il Percorso va incluso ogni volta che il ciclo ha avuto qualsiasi complessità:
stati multipli, ripensamenti, blocchi, alternative esplorate. Il bias corretto
è includere il Percorso. L'omissione è legittima solo quando la decisione è
stata diretta — apertura e chiusura senza stati intermedi significativi. Omettere
il Percorso per concisione vanifica il valore del registro.

## Struttura

Frontmatter (mutabile) più corpo (immutabile). I campi `decisioni` e
`file-toccati` del frontmatter sono la distillazione queryable,
rispettivamente, delle sezioni `Decisioni prese` e `Impatto` del corpo.

```markdown
---
id: {QUESTIONE-ID}
titolo: {Titolo}
tipo-elemento: voce-mastro
tipo: {rilievo | revisione | anomalia}
stato: closed
chiusa: {YYYY-MM-DD}
related: [QUESTIONE-NNN]
tag: [tema-uno, tema-due]
decisioni:
  - {sintesi distillata di una decisione presa}
file-toccati:
  - {percorso/artefatto/uno}
---

## {YYYY-MM-DD} — Chiusura {QUESTIONE-ID}: {Titolo}

**Questione**: {QUESTIONE-ID} — {Titolo}

**Percorso** (ometti solo se la decisione è stata diretta — nessuno stato intermedio)

{sintesi del percorso: aperta per X, bloccata per Y, reindirizzata per Z}

**Decisioni prese**

- {decisione con motivazione}

**Impatto**

- `{artefatto}` — {descrizione della modifica applicata}
```

## Regole

- Il file va scritto in `mastro/` prima di rimuovere la questione da
  `questioni/`; poi si rigenerano gli indici `questioni.md` e `mastro.md`.
- Il corpo della voce è immutabile: non modificarlo mai dopo la scrittura.
- Il frontmatter è mutabile per correzione di disallineamenti, affinamento
  dei campi di giudizio (`decisioni`, `related`, `tag`) e bonifica di versione.
- Decisioni prese e Impatto (corpo) sono obbligatori, così come i campi
  `decisioni` e `file-toccati` (frontmatter) che ne sono la proiezione.
- Il Percorso è obbligatorio salvo ciclo diretto: in caso di dubbio, includerlo.
