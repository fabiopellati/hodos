Aggiorna lo stato di un issue esistente in issues.md.

## 1. Trova issues.md

Cerca `issues.md` nella directory corrente e nelle sottodirectory immediate.
Se non esiste, interrompi e avvisa l'utente.

## 2. Identifica l'issue

Se il messaggio specifica un ID (es. ISSUE-003) o un titolo, individua l'issue
direttamente.

Altrimenti, mostra la lista degli issue presenti nell'indice tramite
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

Modifica il campo **Stato** dell'issue e aggiungi una riga in fondo alla
sezione **Storia**:

```markdown
- {YYYY-MM-DD} {nuovo-stato} — {motivazione}
```

Aggiorna la riga corrispondente nell'indice con il nuovo stato.

## Regole

- Non modificare mai il corpo dell'issue (Descrizione, Domande aperte, Impatto)
  tramite questa skill: usa /issue-close per chiuderlo o edita manualmente
- La motivazione e' obbligatoria: non aggiornare senza di essa
- Lo stato `closed` non e' raggiungibile con questa skill: usa /issue-close
