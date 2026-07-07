---
tipo-artefatto: template
documento: nota
descrizione: struttura canonica di una nota segregata nella cartella note/
fase: trasversale
---

# Template — Nota

Una nota registra un memo, un'osservazione o una decisione informale.
Ogni nota vive nel proprio file `note/NOTA-{NNN}-slug.md`.
L'indice `note.md` è una proiezione derivata dei frontmatter e si rigenera.

## Struttura

Frontmatter YAML di metadati più corpo markdown a formato libero.

```markdown
---
id: NOTA-{ID}
titolo: {Descrizione sintetica}
tipo-elemento: nota
data: {YYYY-MM-DD}
related: [QUESTIONE-NNN]
tag: [tema-uno]
---

## NOTA-{ID} — {YYYY-MM-DD} — {Descrizione sintetica}

{corpo della nota}
```

I campi `related` e `tag` accettano liste vuote (`[]`) quando non applicabili.

## Commento a una nota esistente

Per rettificare o integrare una nota senza modificarne il corpo:

```markdown
**Commenti**

COMMENTO-{NNN} — {YYYY-MM-DD}
{testo del commento}
```

## Aggiornamento indice

L'indice `note.md` è una proiezione derivata: dopo aver creato il file della
nota, si rigenera l'indice dai frontmatter con lo strumento dell'opera. Non
si modifica l'indice a mano.

## Prima di scrivere

Non scrivere la nota senza conferma dell'operatore.

1. Leggi questioni.md per verificare se esistono questioni aperte sullo
   stesso tema o su un tema correlato al prompt dell'operatore.
2. Se esiste una questione correlata, usa il tool AskUserQuestion per
   proporre le opzioni all'operatore:
   - aggiungere un commento alla questione esistente (indicare quale)
   - creare una nota separata
   - non operare
3. Se non esiste una questione correlata, proponi il contenuto della nota
   e attendi approvazione.
4. Non scrivere nulla finché l'operatore non ha scelto.

Usare il tool AskUserQuestion ogni volta che le opzioni sono più di una.
Non proporre opzioni in testo libero.

## Regole

- Il formato è leggero: nessuna sezione strutturata, nessuno stato.
- La descrizione sintetica è quella che appare nell'indice: deve essere comprensibile senza leggere il corpo.
- Il corpo di una nota è immutabile dopo la scrittura.
- Per rettifiche o nuove conoscenze sullo stesso argomento, aggiungere un commento (COMMENTO-NNN) alla nota esistente invece di aprirne una nuova.
- I commenti sono additivi e immutabili.
