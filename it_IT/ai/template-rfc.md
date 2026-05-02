---
tipo-artefatto: template
documento: rfc
descrizione: struttura canonica di un documento RFC e regole operative del ciclo outbound/inbound
fase: trasversale
---

# Template — RFC

Una RFC è un documento formale generato quando una questione richiede l'intervento
di un attore esterno (Team-B). È bidirezionale: Team-A descrive la richiesta,
Team-B compila la risposta nella sezione Response RFC e restituisce il documento.

La RFC è autocontenuta: leggibile senza conoscere la storia interna dell'opera
richiedente.

## Struttura del documento

```markdown
# RFC — {QUESTIONE-ID}

**Data**: {YYYY-MM-DD}
**Commit generazione**: {SHA del commit che ha generato la RFC}
**Da**: Team-A / {nome progetto}
**A**: {Team-B}
**Consegna RFC**: {canale o percorso per consegnare la RFC a Team-B — omettere se implicito}
**Consegna risposta**: {canale o percorso per restituire la risposta a Team-A — omettere se implicito}
**Questione di origine**: {QUESTIONE-ID} — {Titolo questione}

## Contesto

{Descrizione del progetto e del contesto. Autocontenuto: leggibile senza
conoscere la storia interna del progetto richiedente.}

## Richiesta

{Descrizione precisa di cosa viene richiesto.}

## Motivazione

{Perché questa modifica è necessaria. Quale problema risolve.}

## Criteri di Accettazione

{Come Team-A verificherà che il lavoro soddisfi l'esigenza.}

---

## Response RFC

**Data risposta**:
**Stato**:
**Da**:
**A**:

### Decisione

### Lavoro svolto

### Deviazioni
```

## Ciclo outbound

1. La questione passa a `pending-rfc`.
2. La RFC viene generata e consegnata a Team-B.
3. Team-B compila la sezione Response RFC e restituisce il documento.
4. Team-A verifica che il lavoro soddisfi l'esigenza.
5. Solo se la verifica ha esito positivo, la questione viene chiusa.

La risposta di Team-B non chiude la questione: sblocca la fase di verifica.
La responsabilità della verifica resta in capo a Team-A.

## Ciclo inbound

1. La RFC viene valutata prima di aprire qualsiasi questione.
2. La valutazione determina la distribuzione del lavoro.
3. Viene aperta una questione appropriata nel normale ciclo Hodos.
4. Al completamento, la sezione Response RFC viene compilata e restituita.
5. La questione viene chiusa solo dopo la restituzione della risposta.

## Nome del file

Il file RFC si chiama `rfc-Q{NNN}-{descrizione}.md`, dove
`{NNN}` è il numero della questione di origine e
`{descrizione}` è uno slug kebab-case che riassume il
contenuto. Il file va nella sottodirectory `rfc/` della
directory che contiene questioni.md.

Esempio: `rfc/rfc-Q042-migrazione-schema-utenti.md`

## Prima di scrivere

Non redigere il documento RFC senza aver completato
questa sequenza.

1. Verificare che esista una questione dedicata
   all'esigenza che richiede intervento esterno. Se il
   prompt dell'operatore riguarda un'esigenza non ancora
   tracciata, aprire prima la questione.
2. Verificare che la questione sia in stato
   `pending-rfc`. Se è in stato diverso, chiedere
   conferma all'operatore prima di procedere con la
   transizione.
3. Verificare di aver consultato questo template con
   `get_template("rfc")` nella sessione corrente.
   Non redigere basandosi sulla struttura ricordata da
   sessioni precedenti.
4. Redigere il documento seguendo la struttura
   dichiarata in questo template.
5. Nominare il file secondo la convenzione descritta
   nella sezione precedente.
6. Dopo il commit, aggiornare il campo
   `**Commit generazione**` con il SHA del commit e
   committare nuovamente con amend.

## Regole

- La sezione di richiesta è immutabile dopo la
  generazione. I contributi successivi avvengono solo
  tramite Response RFC e commenti.
- La RFC deve essere autocontenuta: Team-B non deve
  conoscere il progetto richiedente per capire cosa
  gli viene chiesto.
- I Criteri di Accettazione descrivono il punto di
  vista di Team-A, non le istruzioni realizzative per
  Team-B.
- La questione resta in `pending-rfc` per l'intero
  ciclo RFC, fino all'avvio effettivo del lavoro.
- La sezione Richiesta può contenere un elenco di item
  (BL o EVO) anziché una singola richiesta puntuale,
  quando la RFC è usata per assegnare un pacchetto di
  lavoro a un team esterno che svolge il ruolo di
  operations. Il ciclo RFC si applica invariato.
- Nel ciclo multi-round — quando Team-B rifiuta e
  segnala un gap che governance deve analizzare prima
  di procedere — i round intermedi si svolgono tramite
  commenti alla RFC: Team-B documenta il rifiuto e il
  gap come COMMENTO-NNN, governance risponde con il
  commento successivo. La Response RFC è unica e
  riservata alla risposta conclusiva definitiva, quella
  su cui governance basa la verifica.
