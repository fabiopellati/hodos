---
tipo-artefatto: template
documento: evoluzione
descrizione: struttura canonica di un'evoluzione per unità mature in fase P2
fase: P2
---

# Template — Evoluzione

**Arricchimento**: questo template appartiene all'arricchimento fasi (P2).
Prima di usarlo, verificare che il CLAUDE.md dell'opera includa questo
arricchimento nella sezione `Arricchimenti abilitati`. Se non è abilitato,
non proporre evoluzioni all'operatore.

Un'evoluzione documenta il passaggio da uno stato del design a un altro
per un'unità matura. È un contratto in due tempi: all'apertura descrive
il delta proposto e la motivazione; alla chiusura documenta l'esito della
realizzazione e la coerenza con il delta. Va aggiunta nella directory
dell'unità come file `EVO-{N}-{titolo}.md`, con numerazione progressiva
locale all'unità.

## Struttura — Apertura

```markdown
## EVO-{N} — {Titolo breve}

### Motivazione

{Perché questa evoluzione è necessaria. Cosa non funziona
o cosa manca nello stato corrente del design. Descrive il
"perché", non il "come".}

### Delta

{Cosa cambia rispetto allo stato corrente del design. Nuovi
scenari d'uso, modifiche al modello dati, transizioni di stato
aggiunte o modificate, impatto sulle interfacce. Se cross-unità,
indicare il riferimento all'evoluzione di coordinamento.}

### Impatto

{Quali documenti di design vanno aggiornati e in quale direzione.
Se cross-unità, quali unità sono coinvolte.}

### Note

{Vincoli rilevanti, alternative scartate, riferimenti utili.
Opzionale.}
```

## Struttura — Chiusura

Aggiungere in append all'evoluzione aperta, senza modificare
il testo esistente:

```markdown
### Consegna [{YYYY-MM-DD}]

**Conformità**: {conforme | parziale | non conforme}

{Descrizione di quanto realizzato. Se parziale o non conforme,
documenta gli scostamenti rispetto al Delta proposto e la
motivazione.}
```

## Regole

- La Motivazione descrive il problema, non la soluzione.
- Il Delta descrive cosa cambia, non come si realizza.
- L'Impatto elenca i documenti di design da aggiornare,
  non i file di codice.
- L'evoluzione è immutabile dopo l'approvazione: la sezione
  Consegna si aggiunge in append, mai in sostituzione.
- Il campo Conformità è obbligatorio: valuta rispetto al
  Delta proposto.
- Scostamenti parziali o non conformi devono essere motivati
  esplicitamente.
- Dopo la chiusura, i documenti di design devono riflettere
  lo stato corrente dell'unità (il delta è stato assorbito).
- L'evoluzione resta nella directory dell'unità come
  documento storico congelato.

## Criteri per aprire un'evoluzione

Un'evoluzione è necessaria quando la modifica soddisfa uno
o più di questi criteri:

- introduce nuovi scenari d'uso
- modifica il modello dati o le transizioni di stato
- ha impatto su altre unità

Modifiche entro i pattern esistenti dell'unità (nuovo filtro,
campo aggiuntivo, regola di validazione) non richiedono
un'evoluzione: si gestiscono con un BL in `2-attivita.md` che
prescrive anche l'aggiornamento dei documenti di design.

## Prima di scrivere

Non scrivere l'evoluzione senza conferma dell'operatore.

1. Verificare che l'arricchimento fasi sia abilitato nel
   CLAUDE.md dell'opera.
2. Verificare che la modifica soddisfi i criteri per
   un'evoluzione (non è una modifica minore gestibile con
   un BL).
3. Proporre i parametri dell'evoluzione (titolo, motivazione
   sintetica, delta sintetico) e attendere approvazione.
4. Non scrivere nulla finché l'operatore non ha scelto.
