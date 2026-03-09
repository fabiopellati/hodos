# Guida Operativa — Team Esterno

Questa guida si rivolge a Team-B: un team che riceve una RFC da un progetto
gestito con questo processo (Team-A). Non richiede conoscenza del processo
interno di Team-A.

---

## Cos'e' una RFC

Una RFC (Request for Change) e' una richiesta formale di intervento su un
sistema gestito dal tuo team. Il documento e' autocontenuto:
contiene tutto il necessario per capire cosa viene chiesto e perche', senza
dover conoscere i dettagli interni del progetto richiedente.

---

## Struttura del documento

Una RFC e' composta da due parti:

**Parte compilata da Team-A** (la trovi gia' compilata):
- **Contesto** — il progetto richiedente e la situazione che ha generato la richiesta
- **Richiesta** — cosa viene chiesto al tuo team, in modo preciso
- **Motivazione** — perche' questa modifica e' necessaria
- **Criteri di Accettazione** — come Team-A verifichera' il lavoro

**Parte da compilare da te** (sezione Response RFC):
- **Stato** — `accepted`, `rejected` o `deferred`
- **Decisione** — la scelta presa con motivazione
- **Lavoro svolto** — descrizione di quanto realizzato
- **Deviazioni** — eventuali differenze rispetto alla richiesta, con motivazione

---

## Come rispondere a una RFC

### 1. Leggi la RFC per intero

Presta attenzione ai Criteri di Accettazione: descrivono esattamente cosa
Team-A verifichera' al momento della consegna.

### 2. Valuta la richiesta

Puoi rispondere con tre stati:

- **accepted** — la richiesta e' fattibile e la prendi in carico
- **rejected** — la richiesta non e' fattibile, con motivazione esplicita
- **deferred** — la richiesta e' accettabile ma non ora, con motivazione
  e indicazione di quando potrebbe essere ripresa

### 3. Realizza (se accepted)

Svolgi il lavoro sul tuo sistema. Se emergono ambiguita' o impedimenti,
contatta Team-A prima di deviare dalla richiesta.

### 4. Compila la sezione Response RFC

```markdown
## Response RFC

**Data risposta**: {YYYY-MM-DD}
**Stato**: accepted
**Da**: {il tuo team}
**A**: {Team-A richiedente}

### Decisione

{Descrizione della decisione presa.}

### Lavoro svolto

{Cosa e' stato realizzato. Includi riferimenti a versioni, documentazione
o qualsiasi elemento utile a Team-A per la verifica.}

### Deviazioni

{Eventuali differenze rispetto alla richiesta originale, con motivazione.
Se nessuna deviazione, scrivi: Nessuna.}
```

### 5. Restituisci il documento

Invia la RFC compilata a Team-A. Da questo momento la verifica e' in capo
a Team-A: potrebbero contattarti se la verifica evidenzia problemi.

---

## Note

- Non e' necessario conoscere il processo interno di Team-A per rispondere
  a una RFC
- Se la richiesta non e' chiara, chiedi chiarimenti a Team-A prima di
  iniziare il lavoro
- Le deviazioni vanno comunicate esplicitamente: Team-A verifica il lavoro
  rispetto ai Criteri di Accettazione originali
