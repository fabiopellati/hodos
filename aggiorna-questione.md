Aggiorna lo stato di una questione esistente in questioni.md.

## 1. Trova questioni.md

Cerca `questioni.md` nella directory corrente e nelle sottodirectory immediate.
Se non esiste, interrompi e avvisa l'utente.

## 2. Identifica la questione

Se il messaggio specifica un ID (es. QUESTIONE-003) o un titolo, individua la
questione direttamente.

Altrimenti, mostra la lista delle questioni presenti nell'indice tramite
AskUserQuestion e chiedi quale aggiornare.

## 3. Determina il nuovo stato

Stati validi:

| Stato | Quando usarlo |
|---|---|
| `in-progress` | analisi avviata o ripresa dopo blocco |
| `pending-approval` | proposta redatta, in attesa di approvazione umana |
| `pending-rfc` | RFC inviata a Team-B, in attesa di risposta |
| `in-verification` | risposta RFC ricevuta, verifica in corso |
| `deferred` | rimandato con motivazione esplicita |

Se il nuovo stato non e' chiaro dal contesto, chiedi tramite AskUserQuestion.

## 4. Richiedi la motivazione

Ogni cambio di stato richiede una nota che risponde al "perche'".
Se il messaggio non la contiene, chiedila prima di procedere.

## 5. Aggiorna il file

Modifica il campo **Stato** della questione e aggiungi una riga in fondo alla
sezione **Storia**:

```markdown
- {YYYY-MM-DD} {nuovo-stato} — {motivazione}
```

Aggiorna la riga corrispondente nell'indice con il nuovo stato.

## Regole

- Non modificare mai il corpo della questione (Descrizione, Domande aperte, Impatto)
  tramite questa skill: usa /chiudi-questione per chiuderla o edita manualmente
- La motivazione e' obbligatoria: non aggiornare senza di essa
- Lo stato `closed` non e' raggiungibile con questa skill: usa /chiudi-questione
