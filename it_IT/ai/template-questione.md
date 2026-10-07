---
tipo-artefatto: template
documento: questione
descrizione: struttura canonica di una questione segregata nella cartella questioni/ (rilievo, revisione o anomalia)
fase: trasversale
autorita: operativa
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

Quali campi siano obbligatori, quali ammettano la lista vuota e quali siano
facoltativi lo stabilisce l'Allegato A del protocollo (Art. 3 comma 8).

Il campo `related` sostituisce la vecchia sezione `Questioni collegate` del
corpo. Il suo perimetro è locale all'opera e il legame verso un'altra opera
si scrive in prosa nel corpo: la norma è l'Art. 3 comma 6 del protocollo.

## Tipi

- **rilievo** — conoscenza nuova emersa, soluzione non ancora definita. Non modifica artefatti nel corso del suo ciclo: se emerge una soluzione pronta, aprire una revisione.
- **revisione** — correzione o modifica da applicare a uno o più artefatti esistenti.
- **anomalia** — comportamento difforme da quanto atteso.

## Sezioni opzionali

Il legame con altri elementi della medesima opera si esprime nel campo
`related` del frontmatter, non in una sezione del corpo (Art. 3 comma 6).

Aggiungere in fondo al corpo solo se presente:

```markdown
**Commenti**

COMMENTO-001 — {YYYY-MM-DD}
{testo del commento; finché la questione è aperta segue il regime del corpo (Art. 4 comma 9)}
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

## La questione aperta è un documento di lavoro

Finché la questione è aperta il suo corpo si modifica: si corregge la Descrizione, si riformula un passaggio rimasto oscuro, si riassorbe nel corpo una rettifica annotata a parte.
Il regime ordinario è nell'Art. 4 comma 7; `Domande aperte` e `Impatto` fanno eccezione e sono mutabili per sola addizione (Art. 4 comma 6).
I commenti appartengono al corpo: il refuso di un commento si corregge nel suo testo e non con un commento di rettifica (Art. 4 comma 9).

Una rettifica che renderebbe la questione più chiara si porta nel corpo invece di aggiungere un commento o una voce di Storia, secondo l'Art. 4 comma 8.
Prima di consolidare un passaggio errato, recupera quel comma con `get_protocol_rules`, perché stabilisce che cosa si conserva e che cosa si riscrive.
Nella redazione ne discendono tre attenzioni:

- la traccia di ciò che l'opera ha davvero creduto si conserva, il difetto di redazione estraneo al dominio si riscrive, e nel dubbio la classificazione la decide l'operatore e non chi redige (Art. 4 comma 8, lettere a e b);
- il testo consolidato si accorcia solo di ciò che era sbagliato, e non si comprime ciò che era esposto per esteso (lettera c);
- il commento redazionale si riassorbe solo con l'approvazione dell'operatore, e quello che registra un'interazione datata resta dov'è (lettera d).

## Regole

- Il tipo è immutabile dopo l'apertura.
- Il campo `descrizione` del frontmatter è la sintesi distillata delle motivazioni e proietta in forma queryable la sezione `Descrizione` del corpo; la sua qualificazione è nell'Allegato A del protocollo.
- La Descrizione descrive il problema, non la soluzione.
- Finché la questione è aperta il corpo è modificabile (Art. 4 comma 7) e si consolida secondo l'Art. 4 comma 8: vedi la sezione «La questione aperta è un documento di lavoro».
- I campi Domande aperte e Impatto sono mutabili per addizione nel corso del ciclo: si possono aggiungere nuove voci documentando il motivo. Una voce esistente non si cancella, ma si può dichiarare superata o inattuata con motivazione esplicita inline.
- La motivazione nella Storia risponde al "perché", non al "cosa": la Storia registra la ragione di un cambiamento di stato, non il contenuto del lavoro. Le deduzioni, le ipotesi, i risultati intermedi e le analisi vanno nel corpo, mai nella Storia.
- Un rilievo con Impatto non vuoto non può essere chiuso senza almeno una questione di revisione collegata aperta.
