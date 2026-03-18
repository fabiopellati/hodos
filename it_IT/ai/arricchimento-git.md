---
tipo-artefatto: guida
autorita: operativa
documento: arricchimento-git
descrizione: Convenzioni git per progetti Hodos che usano un repository git
fase: trasversale
---

# Arricchimento — Convenzioni git per progetti Hodos

Questo arricchimento e' opzionale. Si attiva nei progetti che usano git e vogliono
una convenzione esplicita di nomenclatura branch legata alle questioni Hodos.

Hodos e' git-agnostico per principio. Questo arricchimento non fa parte del
protocollo base e non e' obbligatorio. I progetti che non lo attivano seguono
le convenzioni git proprie del loro contesto.

## Come attivare

Nel `CLAUDE.md` del progetto, sezione `Arricchimenti abilitati`:

```markdown
## Arricchimenti abilitati

- arricchimento-git: convenzioni branch git per questioni Hodos
```

---

## Convenzione di nomenclatura branch

Tre pattern coprono i casi d'uso tipici:

### Questione singola

Branch dedicato a una singola questione operativa:

```
<tipo-git>/q<NNN>-<descrizione-kebab>
```

Il `<tipo-git>` e' il tipo della modifica git — scelto liberamente dall'operatore
in base a cosa fa il branch, non derivato dal tipo della questione Hodos:

| Tipo git | Quando usarlo |
|---|---|
| `feat/` | nuova funzionalita' o capacita' |
| `fix/` | correzione di un comportamento errato |
| `docs/` | solo documentazione o artefatti |
| `chore/` | manutenzione, configurazione, dipendenze |
| `refactor/` | ristrutturazione senza cambiare comportamento |

Esempi:
- `feat/q055-configurazione-deploy`
- `fix/q061-correzione-formula-limite`
- `docs/q072-aggiornamento-scenari`
- `chore/q058-validazione-dispositivi`

### Batch di questioni

Branch che copre piu' questioni sequenziali della stessa fase o contesto:

```
<tipo-git>/<fase-o-contesto>-<descrizione>
```

Usare questo pattern quando si lavora su un insieme di questioni correlate
che condividono lo stesso branch. La scelta tra questione singola e batch
e' discrezionale: usare il batch quando le questioni sono strettamente
sequenziali e difficilmente separabili, la questione singola negli altri casi.

Esempi:
- `feat/p3-integrazione` (copre Q055..Q058)
- `docs/p1-analisi-requisiti`

### Governance

Branch per attivita' di revisione, approvazione e chiusura questioni:

```
docs/<fase-o-contesto>
```

Esempi:
- `docs/governance`
- `docs/p2-chiusura`

---

## Regola operativa alla transizione open -> in-progress

Prima di portare una questione in `in-progress`, verificare il branch git corrente:

1. Il branch corrente e' gia' coerente con il lavoro da fare? Proseguire.
2. Il branch e' `develop`, `main`, o un branch di un'altra attivita'? Creare un branch dedicato prima di toccare qualsiasi file.

```bash
git branch --show-current
# se non coerente:
git checkout develop && git pull
git checkout -b <tipo-git>/q<NNN>-<descrizione>
```

Non operare mai direttamente su `develop`, `main`, o branch di governance
di un'altra fase.

---

## Merge su develop

Al completamento della questione, fare merge con `--no-ff`:

```bash
git checkout develop
git merge --no-ff <tipo-git>/q<NNN>-<descrizione> -m "Merge <tipo>: descrizione"
```

Il `--no-ff` preserva la tracciabilita' del branch nella storia git.
