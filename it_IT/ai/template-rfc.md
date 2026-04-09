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

## Regole

- La sezione di richiesta è immutabile dopo la generazione. I contributi successivi avvengono solo tramite Response RFC e commenti.
- La RFC deve essere autocontenuta: Team-B non deve conoscere il progetto richiedente per capire cosa gli viene chiesto.
- I Criteri di Accettazione descrivono il punto di vista di Team-A, non le istruzioni realizzative per Team-B.
- La questione resta in `pending-rfc` per l'intero ciclo RFC, fino all'avvio effettivo del lavoro.
- Il file RFC va nella sottodirectory `rfc/` della directory che contiene questioni.md.
