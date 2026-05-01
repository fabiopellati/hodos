---
tipo-artefatto: template
documento: questione
descrizione: struttura canonica di una questione in questioni.md (rilievo, revisione o anomalia)
fase: trasversale
---

# Template — Questione

Una questione traccia un problema, un rilievo o una revisione nel ciclo di lavoro Hodos.
Va inserita in cima a `questioni.md`, dopo la sezione Indice.

## Struttura

```markdown
## QUESTIONE-{ID} — {Titolo}

**Tipo**: {rilievo | revisione | anomalia}
**Stato**: open

**Storia**
- {YYYY-MM-DD} open — {motivazione apertura, una riga}

**Descrizione**

{descrizione del problema, rilievo, revisione o anomalia}

**Domande aperte**
- [ ] {prima domanda, se presente}

**Impatto**
- {artefatto o fase} — {descrizione dell'impatto}

---
```

## Tipi

- **rilievo** — conoscenza nuova emersa, soluzione non ancora definita. Non modifica artefatti nel corso del suo ciclo: se emerge una soluzione pronta, aprire una revisione.
- **revisione** — correzione o modifica da applicare a uno o più artefatti esistenti.
- **anomalia** — comportamento difforme da quanto atteso.

## Sezioni opzionali

Aggiungere dopo `**Impatto**` solo se presenti:

```markdown
**Questioni collegate**: QUESTIONE-NNN, QUESTIONE-MMM
```

```markdown
**Commenti**

COMMENTO-001 — {YYYY-MM-DD}
{testo del commento, immutabile dopo la scrittura}
```

## Aggiornamento indice

Aggiungere in cima all'elenco dell'indice:

```markdown
- **QUESTIONE-{ID}** — {Titolo} — open
```

Aggiornare la nota:

```
> Ultima questione inserita: QUESTIONE-{ID} — {YYYY-MM-DD}.
```

## Prima di scrivere

Non scrivere la questione senza conferma dell'operatore.

1. Leggi questioni.md per verificare se esistono questioni aperte sullo
   stesso tema o su un tema correlato al prompt dell'operatore.
2. Se esiste una questione correlata, usa il tool AskUserQuestion per
   proporre le opzioni all'operatore:
   - aggiungere un commento alla questione esistente (indicare quale)
   - aprire una nuova questione collegata
   - non operare
3. Se non esiste una questione correlata, proponi i parametri della nuova
   questione (tipo, titolo, descrizione sintetica) e attendi approvazione.
4. Non scrivere nulla finché l'operatore non ha scelto.

Usare il tool AskUserQuestion ogni volta che le opzioni sono più di una.
Non proporre opzioni in testo libero.

## Regole

- Il tipo è immutabile dopo l'apertura.
- La Descrizione descrive il problema, non la soluzione. È immutabile dopo la scrittura: usare un commento per rettifiche o integrazioni.
- I campi Domande aperte e Impatto sono mutabili per addizione nel corso del ciclo: si possono aggiungere nuove voci documentando il motivo. Una voce esistente non si cancella, ma si può dichiarare superata o inattuata con motivazione esplicita inline.
- La motivazione nella Storia risponde al "perché", non al "cosa".
- Un rilievo con Impatto non vuoto non può essere chiuso senza almeno una questione di revisione collegata aperta.
