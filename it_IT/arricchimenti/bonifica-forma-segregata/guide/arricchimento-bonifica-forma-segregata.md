---
tipo-artefatto: guida
documento: arricchimento-bonifica-forma-segregata
descrizione: arricchimento di bonifica per migrare un'opera Hodos dalla forma monolitica alla forma segregata degli strumenti di governo, con frontmatter e indici derivati
autorita: informativa
---

# Arricchimento — Bonifica verso la forma segregata

La versione 1.0.0 del protocollo Hodos introduce la forma segregata degli
strumenti di governo: le questioni, le note e il mastro cessano di essere file
monolitici accumulanti e diventano collezioni di file, uno per elemento, con un
frontmatter YAML di metadati e un indice che ne è la proiezione derivata.
Questo arricchimento accompagna le opere già avviate sulla forma monolitica
precedente nella migrazione verso la nuova forma.

L'arricchimento è opzionale e temporaneo per natura: serve una volta sola,
quando un'opera esistente adotta la versione 1.0.0 del protocollo.
Un'opera inizializzata direttamente sulla forma segregata non ne ha bisogno.

---

## Quando è utile

L'arricchimento è utile a ogni opera che soddisfa entrambe le condizioni:

- possiede un corpus di processo già scritto nella forma monolitica —
  `questioni.md`, `mastro.md` e `note.md` come singoli file accumulanti;
- adotta la versione 1.0.0 (o successiva) del protocollo, che prescrive la
  forma segregata.

La migrazione nasce da un'esigenza concreta osservata operando su un mastro
reale di migliaia di righe: un file monolitico oltre una certa dimensione non
è caricabile per intero da un agente con contesto limitato, gli header si
perdono nei risultati di ricerca testuale, i legami scritti in prosa non sono
traversabili in modo deterministico e gli indici mantenuti a mano divergono
dalla sorgente. La forma segregata risolve questi problemi alla radice; questo
arricchimento porta il corpus esistente dentro la nuova forma senza perdere
nulla della storia accumulata.

---

## Che cosa prescrive

L'arricchimento prescrive un processo di migrazione a due strati e ne fissa gli
invarianti di non-regressione. La descrizione operativa completa, passo per
passo, vive nello skill `arricchimento-bonifica-forma-segregata`.

In sintesi:

- **Primo strato — split deterministico.** Il monolite viene separato in un
  file per elemento, con il corpo trasferito verbatim e un frontmatter minimo
  ricavabile meccanicamente (identificativo, titolo, tipo, stato, date). Gli
  indici vengono rigenerati dai frontmatter. Questo strato è puramente
  meccanico e non richiede giudizio.
- **Secondo strato — arricchimento progressivo.** I campi di giudizio del
  frontmatter (`decisioni`, `related`, `tag`, `file-toccati`) vengono compilati
  leggendo il contenuto di ciascun elemento. Questo strato richiede lettura e
  interpretazione, può avvenire in tempi successivi e non blocca il primo.
- **Commit isolato.** La riformattazione di massa, che tocca l'intero corpus,
  va eseguita in un commit dedicato, senza alcun'altra modifica sostanziale,
  così che il diff della migrazione non si mescoli al lavoro vero.

---

## Tooling promosso, non prescritto

L'arricchimento **promuove** l'adozione di uno strumento di automazione che
esegua lo split del monolite, la generazione degli indici a partire dai
frontmatter e la validazione della coerenza tra corpo e frontmatter.
Non ne **prescrive** però né il linguaggio né l'architettura: lo strumento è
realizzato da ciascun progetto secondo il proprio stack tecnologico, tipicamente
in Python o in TypeScript.

Questa scelta è coerente con l'impianto del protocollo 1.0.0, che prescrive la
forma e le invarianti degli strumenti di governo ma lascia ai singoli progetti
la realizzazione del tooling di generazione degli indici e di validazione dei
frontmatter, accettando la divergenza implementativa come costo ragionevole
dell'indipendenza dallo stack.

---

## Come si abilita

L'arricchimento si dichiara nel `CLAUDE.md` dell'opera, nella sezione
`Arricchimenti abilitati`:

```
- arricchimento-bonifica-forma-segregata
```

La dichiarazione ha senso finché la migrazione è in corso. Completata la
bonifica e verificata la conformità del corpus alla forma segregata,
l'arricchimento può essere rimosso dalla dichiarazione: ha esaurito il suo
scopo.
