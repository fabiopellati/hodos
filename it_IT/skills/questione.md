---
skill: questione
client: Claude Code CLI
invocazione: /hodos-questione
tipo: operativo
locale: it_IT
---

Apri una nuova questione nel file questioni.md del progetto corrente.

## 1. Trova questioni.md

Cerca `questioni.md` nella directory corrente e nelle sottodirectory immediate
(es. `documenti/`, `project/`).

Se non esiste, chiedi all'utente dove crearlo prima di procedere.

## 2. Determina i parametri

Se il contesto del messaggio non fornisce tutte le informazioni necessarie,
usa AskUserQuestion per raccogliere:

- **Tipo**: `rilievo` (conoscenza nuova emersa), `revisione` (correzione artefatto esistente) o `anomalia` (comportamento difforme da quanto atteso)
- **Titolo**: breve e descrittivo
- **Descrizione**: il problema, il rilievo, la revisione o l'anomalia

Se il tipo e' `rilievo`, verifica con l'operatore:

> Stai aprendo un rilievo — conoscenza nuova emersa, soluzione non ancora definita.
> Se sai gia' cosa fare e sei pronto ad agire, apri una revisione invece.
> Confermi rilievo?

Se l'operatore corregge in revisione, procedi con `revisione`. Il tipo e'
immutabile dopo l'apertura: scegliere bene ora evita di dover chiudere e
riaprire la questione.

## 3. Determina l'ID

Leggi il file per identificare tutti gli ID esistenti (formato `QUESTIONE-NNN`).
Assegna il prossimo ID disponibile. La numerazione non deve essere progressiva
senza buchi, ma ogni ID deve essere univoco.

## 4. Scrivi la questione

Inserisci la nuova questione in cima al file, dopo la sezione Indice, usando
questo formato:

```markdown
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

**Commenti** (opzionale — ometti se assente)

COMMENTO-NNN — YYYY-MM-DD
[testo]

---
```

## 5. Aggiorna l'indice

Aggiungi una riga in cima alla tabella dell'indice:

```markdown
| QUESTIONE-{ID} | {Titolo} | open |
```

Aggiorna la nota:

```
> Ultima questione inserita: QUESTIONE-{ID} — {YYYY-MM-DD}.
```

## Regole

- Una questione aperta non contiene mai la soluzione, solo il problema
- La motivazione nella Storia deve rispondere al "perche'" non al "cosa"
- Se le domande aperte non sono ancora note, ometti la sezione o lasciala vuota
