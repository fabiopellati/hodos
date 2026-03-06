Genera una RFC da una questione esistente in stato pending-rfc.

## 1. Trova questioni.md

Cerca `questioni.md` nella directory corrente e nelle sottodirectory immediate.
Se non esiste, interrompi e avvisa l'utente.

## 2. Identifica la questione

Se il messaggio specifica un ID, individua la questione direttamente e verifica
che sia in stato `pending-rfc`.

Altrimenti, mostra tramite AskUserQuestion le questioni in stato `pending-rfc`
e chiedi quale usare. Se non ce ne sono, interrompi e avvisa l'utente.

## 3. Raccogli le informazioni mancanti

Leggi la questione per estrarre il contesto disponibile. Per le informazioni
non deducibili dalla questione, chiedi tramite AskUserQuestion:

- **Team-B**: nome del team destinatario
- **Sistema**: sistema o unita' su cui e' richiesto l'intervento
- **Criteri di accettazione**: come Team-A verifichera' il lavoro (se non gia' nella questione)

## 4. Determina il percorso del file RFC

Il file RFC va nella stessa directory di questioni.md, in una sottodirectory `rfc/`.
Crea la directory se non esiste.

Nome file: `rfc-{QUESTIONE-ID}-{slug-titolo}.md`
Esempio: `rfc-QUESTIONE-003-aggiunta-campo-mgzsp00f.md`

## 5. Scrivi il file RFC

```markdown
# RFC — {QUESTIONE-ID}

**Data**: {YYYY-MM-DD}
**Da**: Team-A / {nome progetto}
**A**: Team-B / {Team-B}
**Questione di origine**: {QUESTIONE-ID} — {Titolo questione}

## Contesto

{Descrizione del progetto e del contesto in cui e' emersa la necessita'.
Autocontenuto: leggibile senza conoscere la storia interna del progetto.}

## Richiesta

{Descrizione precisa di cosa viene richiesto: quale sistema, quale modifica,
quale campo, quale comportamento atteso.}

## Motivazione

{Perche' questa modifica e' necessaria. Quale problema risolve.}

## Criteri di Accettazione

{Come Team-A verifichera' che il lavoro soddisfi l'esigenza.}

---

## Response RFC

**Data risposta**:
**Stato**:

### Decisione

### Lavoro svolto

### Deviazioni
```

## Regole

- La RFC deve essere autocontenuta: Team-B non deve conoscere il progetto
  richiedente per capire cosa gli viene chiesto
- Non includere dettagli interni del progetto non rilevanti per Team-B
- I Criteri di Accettazione descrivono il punto di vista di Team-A,
  non le istruzioni realizzative per Team-B
