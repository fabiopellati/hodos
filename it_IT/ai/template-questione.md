---
tipo-artefatto: template
documento: questione
descrizione: struttura canonica di una questione segregata nella cartella questioni/ (rilievo, revisione o anomalia)
fase: trasversale
---

# Template — Questione

Una questione traccia un problema, un rilievo o una revisione nel ciclo di lavoro Hodos.
Ogni questione vive nel proprio file `questioni/Q{NNN}-slug.md`, dove `{NNN}`
è l'identificativo e `slug` è uno slug kebab-case del titolo.
L'indice `questioni.md` è una proiezione derivata dei frontmatter e si
rigenera: non si scrive la questione dentro l'indice.

## Struttura

Il file è composto da un frontmatter YAML di metadati queryable e da un corpo
markdown narrativo. I campi `tipo` e `stato` compaiono in entrambi: la
coerenza è presidiata dal validatore dell'opera.

```markdown
---
id: QUESTIONE-{ID}
titolo: {Titolo}
descrizione: {sintesi distillata delle motivazioni: perché la questione esiste, il problema o il bisogno che la origina}
tipo-elemento: questione
tipo: {rilievo | revisione | anomalia}
stato: open
aperta: {YYYY-MM-DD}
aggiornata: {YYYY-MM-DD}
related: [QUESTIONE-NNN]
tag: [tema-uno, tema-due]
---

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
```

Il campo `descrizione` è la sintesi distillata delle motivazioni della
questione — il "prima", cioè il perché la questione esiste — ed è la proiezione
queryable della sezione `Descrizione` del corpo. Nel mastro farà da contraltare
a `decisioni`, il "dopo".

Il campo `related` è opzionale nel caso generale; sostituisce la vecchia
sezione `Questioni collegate` del corpo. I campi `related` e `tag` accettano
liste vuote (`[]`) quando non applicabili.

## Tipi

- **rilievo** — conoscenza nuova emersa, soluzione non ancora definita. Non modifica artefatti nel corso del suo ciclo: se emerge una soluzione pronta, aprire una revisione.
- **revisione** — correzione o modifica da applicare a uno o più artefatti esistenti.
- **anomalia** — comportamento difforme da quanto atteso.

## Sezioni opzionali

Il legame con altre questioni si esprime nel campo `related` del frontmatter,
non in una sezione del corpo.

Aggiungere in fondo al corpo solo se presente:

```markdown
**Commenti**

COMMENTO-001 — {YYYY-MM-DD}
{testo del commento, immutabile dopo la scrittura}
```

## Aggiornamento indice

L'indice `questioni.md` è una proiezione derivata: dopo aver creato o
aggiornato il file della questione, si rigenera l'indice dai frontmatter con
lo strumento dell'opera. Non si modifica l'indice a mano.

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
- Il campo `descrizione` del frontmatter è la sintesi distillata delle motivazioni ed è obbligatorio: proietta in forma queryable la sezione `Descrizione` del corpo.
- La Descrizione descrive il problema, non la soluzione. È immutabile dopo la scrittura: usare un commento per rettifiche o integrazioni.
- I campi Domande aperte e Impatto sono mutabili per addizione nel corso del ciclo: si possono aggiungere nuove voci documentando il motivo. Una voce esistente non si cancella, ma si può dichiarare superata o inattuata con motivazione esplicita inline.
- La motivazione nella Storia risponde al "perché", non al "cosa".
- Un rilievo con Impatto non vuoto non può essere chiuso senza almeno una questione di revisione collegata aperta.
