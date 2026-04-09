---
skill: arricchimento-versionamento-git
client: Claude Code CLI
invocazione: /hodos-arricchimento-versionamento-git
tipo: descrittivo
locale: it_IT
---

Arricchimento opzionale per opere che adottano git come sistema di versionamento.
Questo skill è descrittivo: non esegue azioni, non crea file. Fornisce il contesto
per integrare il workflow git con il percorso P0-P4 di Hodos.

Applicabile solo se il team usa git. Ignorabile altrimenti.

---

## Verifica preliminare

Prima di procedere, verifica se la directory corrente è un repo git:

```bash
git rev-parse --is-inside-work-tree 2>/dev/null
```

Se il comando fallisce o restituisce errore, la directory non è un repo git.
In questo caso, ricorda all'utente:

> La directory corrente non è un repo git. Esegui `git init` per inizializzare
> il repository prima di applicare le convenzioni di versionamento.

Dopo `git init`, è buona norma creare subito il branch `develop`:

```bash
git checkout -b develop
```

---

## Integrazione con P4 — Consegna

La fase P4 di Hodos è agnostica rispetto agli strumenti. Per team che usano git,
la consegna si materializza tipicamente così:

1. Crea il branch di release: `release/x.y.z`
2. Esegui le verifiche finali sul branch di release
3. Merge su `main` (o branch principale) e su `develop`
4. Apponi il tag di versione: `vx.y.z`

Il criterio di approvazione P4 in questo contesto è: merge su main approvato
e tag di versione applicato.

---

## Strategia di branching

Un modello di riferimento compatibile con Hodos:

| Branch | Scopo |
|---|---|
| `main` | Versioni stabili consegnate; ogni commit corrisponde a un tag |
| `develop` | Integrazione continua del lavoro in corso |
| `feat/nome` | Unità di realizzazione (P2); merge su develop al completamento |
| `fix/nome` | Correzioni; merge su develop |
| `release/x.y.z` | Preparazione consegna (P4); merge su main e develop |
| `hotfix/nome` | Correzione urgente su main; merge su main e develop |

---

## Versionamento semantico

Formato raccomandato: `MAJOR.MINOR.PATCH`

| Componente | Quando incrementare |
|---|---|
| `MAJOR` | Cambiamento incompatibile con versioni precedenti |
| `MINOR` | Nuova funzionalità retrocompatibile |
| `PATCH` | Correzione di difetti |

---

## Commit e merge

- Ogni commit descrive una modifica logica atomica
- Il messaggio di commit risponde al "perché", non al "cosa"
- Il merge di un branch di unità su develop usa `--no-ff` per preservare la storia
- Il merge di release su main usa `--no-ff` e produce un merge commit identificabile

---

## Nota

Questo arricchimento è un riferimento operativo, non un vincolo. Il team adatta
le convenzioni al proprio contesto. L'unico invariante di Hodos è l'approvazione
esplicita prima di procedere alla fase successiva: come si materializza
tecnicamente è una scelta implementativa.
