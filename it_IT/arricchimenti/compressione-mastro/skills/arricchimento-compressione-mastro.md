---
tipo-artefatto: skill
documento: arricchimento-compressione-mastro
descrizione: arricchimento deprecato dalla versione 1.0.0 del protocollo, superato dalla forma
  segregata degli strumenti di governo
skill: arricchimento-compressione-mastro
client: Claude Code CLI
invocazione: /hodos-arricchimento-compressione-mastro
tipo: descrittivo
locale: it_IT
stato: deprecato
deprecato-da: 1.0.0
---

> **ARRICCHIMENTO DEPRECATO (dalla versione 1.0.0 del protocollo).**
> La forma segregata degli strumenti di governo, introdotta dal protocollo
> 1.0.0, rende questo arricchimento ridondante e ne dispone la deprecazione.
> Non va adottato in nuove opere. Le opere che lo hanno adottato trovano il
> trattamento nella sezione "Deprecazione" in fondo a questo documento.
> Il rationale della deprecazione è in coda al file.

Arricchimento opzionale per opere che privilegiano un mastro essenziale.
Questo skill è descrittivo: non esegue azioni, non crea file. Fornisce le
istruzioni necessarie all'AI per omettere la sezione Percorso dalle entry
del mastro quando l'opera lo adotta.

---

## Trade-off

Il protocollo prevede che ogni entry del mastro possa includere una sezione
Percorso che documenta l'arco decisionale: stati intermedi attraversati,
alternative valutate, ripensamenti. Questa sezione è il principale veicolo
di tracciabilità del processo decisionale.

Omettere il Percorso produce un mastro più compatto e rapido da scrivere,
ma comporta una perdita irreversibile: il ciclo che ha portato alla decisione
non è più ricostruibile dal solo mastro. La storia della questione viene
rimossa alla chiusura, e senza il Percorso nell'entry del mastro l'unica
fonte residua è la cronologia git, che preserva i contenuti ma non li
organizza in forma narrativa.

L'adozione di questo arricchimento è una scelta deliberata e consapevole:
chi la compie dichiara che la compattezza del mastro ha più valore della
tracciabilità del percorso decisionale per quell'opera specifica.

---

## Quando è appropriato

L'omissione del Percorso è ragionevole in opere con queste caratteristiche:

- **Cicli brevi**: le questioni si aprono e si chiudono con pochi stati
  intermedi, senza ripensamenti o alternative significative
- **Team ridotto**: chi ha partecipato alla decisione ricorda il contesto
  e non ha bisogno di una traccia scritta per ricostruirlo
- **Backlog contenuto**: il numero di questioni è basso e il mastro resta
  leggibile anche senza sintesi dei percorsi
- **Decisioni dirette**: la maggior parte delle questioni si risolve senza
  passaggi intermedi significativi (apertura, analisi, chiusura)

Non è appropriato in opere dove le decisioni sono complesse, contestate,
o coinvolgono attori esterni che potrebbero aver bisogno di ricostruire
il ragionamento a posteriori.

---

## Normativa generale e opt-in

In assenza di questo arricchimento vale la normativa generale del protocollo:
il bias corretto è includere la sezione Percorso ogni volta che il ciclo
ha avuto qualsiasi complessità. L'omissione è giustificata solo quando la
decisione è stata diretta, senza stati intermedi significativi.

Questo arricchimento non si attiva implicitamente. Senza una dichiarazione
esplicita dell'opera, l'AI continua ad applicare la normativa generale e
propone il Percorso come previsto dalla skill questione.

---

## Adozione

L'opera attiva la compressione del mastro dichiarandola nel proprio
`CLAUDE.md` con questa riga:

```
**Compressione mastro**: attiva
```

La dichiarazione è una scelta espressa dell'operatore che governa l'opera.
Solo dopo questa dichiarazione l'AI omette la sezione Percorso dalle entry
del mastro. Senza di essa, il comportamento resta quello del protocollo.

---

## Variante operativa

Quando l'arricchimento è attivo, il ramo di chiusura della skill
questione cambia in un solo punto: il prompt che chiede all'operatore
di fornire una sintesi del percorso decisionale non viene proposto, e la
sezione Percorso non compare nell'entry del mastro.

Il formato dell'entry diventa:

```markdown
## {YYYY-MM-DD} — Chiusura {QUESTIONE-ID}: {Titolo}

**Questione**: {QUESTIONE-ID} — {Titolo}

**Decisioni prese**

- {decisione con motivazione}

**Impatto**

- `{artefatto}` — {descrizione della modifica applicata}

---
```

Tutti gli altri elementi dell'entry restano invariati: il titolo, le
decisioni prese con le rispettive motivazioni, e l'impatto sugli artefatti
continuano a essere registrati normalmente.

---

## Rationale

Questo arricchimento nasce dalla decisione registrata con la chiusura di
QUESTIONE-043. L'analisi ha stabilito che il Percorso è il meccanismo
corretto per preservare la tracciabilità nel mastro (conforme a tutti
i principi del protocollo), ma che la sua omissione non viola il protocollo:
è una rinuncia consapevole a un valore opzionale, non una violazione di
una regola vincolante.

L'arricchimento formalizza questa rinuncia come scelta esplicita dell'opera,
anziché lasciarla implicita o casuale. Si tratta di un arricchimento che
riduce anziché aggiungere: non introduce nuove sezioni o campi, ma
documenta la scelta deliberata di non utilizzare una sezione già prevista
dal protocollo.

---

## Deprecazione

Questo arricchimento è deprecato dalla versione 1.0.0 del protocollo.

### Perché è deprecato

L'arricchimento nasceva per un problema che la forma segregata risolve in
radice. La compressione del mastro serviva a tenere leggibile e navigabile un
registro che, nella forma monolitica, cresceva in un unico file: omettere il
Percorso riduceva la massa di testo da scorrere. La forma segregata introdotta
dal protocollo 1.0.0 fornisce quella navigabilità per costruzione — un file per
questione chiusa e un frontmatter interrogabile — senza sacrificare la
tracciabilità del percorso decisionale. Il campo `decisioni` del frontmatter
offre inoltre la distillazione queryable di ciò che è stato deciso, che è il
sommario essenziale a cui la compressione mirava, ma senza rinunciare al corpo
narrativo completo.

Venuta meno la ragione che lo giustificava — la fatica di navigare un monolite
crescente — non ha più senso barattare la tracciabilità del Percorso con una
compattezza che la segregazione ottiene gratis. L'arricchimento risulta quindi
ridondante.

### Trattamento delle opere che lo hanno adottato

- Le entry di mastro già scritte senza Percorso restano valide e immutabili:
  il corpo del mastro non si tocca, e la loro forma storica va preservata così
  com'è. La deprecazione non impone alcuna riscrittura del pregresso.
- Per il lavoro futuro, l'opera cessa di applicare l'omissione: torna a valere
  la normativa generale del protocollo, che include il Percorso ogni volta che
  il ciclo ha avuto complessità.
- La dichiarazione `**Compressione mastro**: attiva` nel `CLAUDE.md` va rimossa
  quando l'opera migra alla forma segregata (vedi l'arricchimento
  `bonifica-forma-segregata`).

### Nessuna nuova adozione

Le nuove opere non devono adottare questo arricchimento. Chi desidera un mastro
navigabile trova nella forma segregata del protocollo base la risposta corretta,
senza la perdita di tracciabilità che la compressione comportava.
