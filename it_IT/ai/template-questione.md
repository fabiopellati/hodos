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

## La questione aperta è un documento di lavoro

Finché la questione non è chiusa, il suo corpo si può modificare.
Si corregge la Descrizione, si riformula un passaggio rimasto oscuro, si riassorbe nel corpo una rettifica che era stata annotata a parte.

Il protocollo concede l'immutabilità del corpo in modo esplicito e solo dove la vuole: alla nota (Art. 5 comma 5) e alla voce del mastro (Art. 6 comma 7 e Art. 10 comma 1).
Sulla questione vincola per addizione i soli campi `Domande aperte` e `Impatto` (Art. 4 comma 6), e tace sul resto del corpo.
Hodos non è quindi esclusivamente additivo, e trattarlo come tale su una questione aperta è un errore di applicazione, non un eccesso di prudenza.

**Preferire il consolidamento all'accumulo.**
Quando una rettifica renderebbe la questione più chiara, più ordinata e più concreta, si consolida il corpo invece di aggiungere l'ennesimo commento o l'ennesima voce di Storia.
La ragione non è estetica.
Un testo che afferma una cosa e più avanti la smentisce è faticoso da leggere per una persona e induce in errore chi lo consulti per frammenti: un corpus che non entra per intero in contesto viene interrogato per ricerca, e nulla garantisce che un'affermazione e la sua negazione vengano recuperate insieme.
Il modo affidabile di impedire che un'idea errata rientri nel ragionamento non è dichiararla errata, ma non nominarla.

**Che cosa si consolida e che cosa si conserva.**
Il criterio è che cosa l'errore riguardava, non chi l'ha commesso.

- Se è esistito un momento in cui l'opera credeva davvero una cosa e poi ha appreso il contrario — una decisione mutata, un chiarimento che rovescia un'assunzione, una condizione di campo diversa da come era stata descritta — la traccia **si conserva**: era corretta rispetto a ciò che si sapeva allora, e serve a ricostruire il perché di una decisione.
- Se invece l'affermazione non è mai stata vera per l'opera ed era un difetto di redazione di chi scrive, estraneo al dominio, il testo **si riscrive** come se fosse stato redatto correttamente fin dall'inizio, insieme a tutto ciò che ne era stato dedotto.

Nel dubbio si conserva, e la classificazione la decide l'operatore, non chi redige: chi ha commesso l'errore non è il giudice adatto a stabilire se sia stato un refuso.
Una regola pratica aiuta: se anche una sola decisione dell'opera si è appoggiata a quell'affermazione, l'affermazione è entrata nel dominio e la traccia resta.

**Consolidare non significa abbreviare.**
Il consolidamento rimuove ciò che è errato e riscrive ciò che è confuso a parità di ricchezza espositiva: non è un'operazione di sintesi, non accorcia il testo corretto e non comprime in forma telegrafica ciò che era esposto per esteso.
Se al termine il testo risulta più breve, deve esserlo perché è stato tolto ciò che era sbagliato, non perché è stato compresso ciò che era giusto.
La brevità non è un valore del processo, e un corpo consolidato che sia diventato illeggibile ha sostituito un difetto con un altro.

Nulla va perduto: il testo rimosso resta nella cronologia git, che è la sede propria di un refuso di redazione.
La differenza è precisamente ciò che rende la questione importante — git conserva senza immettere in contesto, il documento conserva immettendo in contesto.

## Regole

- Il tipo è immutabile dopo l'apertura.
- Il campo `descrizione` del frontmatter è la sintesi distillata delle motivazioni ed è obbligatorio: proietta in forma queryable la sezione `Descrizione` del corpo.
- La Descrizione descrive il problema, non la soluzione.
- Finché la questione è aperta il corpo è modificabile: vedi la sezione «La questione aperta è un documento di lavoro». L'immutabilità del corpo appartiene alla nota e alla voce del mastro, non alla questione aperta.
- I campi Domande aperte e Impatto sono mutabili per addizione nel corso del ciclo: si possono aggiungere nuove voci documentando il motivo. Una voce esistente non si cancella, ma si può dichiarare superata o inattuata con motivazione esplicita inline.
- La motivazione nella Storia risponde al "perché", non al "cosa": la Storia registra la ragione di un cambiamento di stato, non il contenuto del lavoro. Le deduzioni, le ipotesi, i risultati intermedi e le analisi vanno nel corpo, mai nella Storia.
- Un rilievo con Impatto non vuoto non può essere chiuso senza almeno una questione di revisione collegata aperta.
