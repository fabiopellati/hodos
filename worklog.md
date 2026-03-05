Aggiorna il work log per questa sessione di lavoro.

## Procedura

### 1. Verifica dati /cost

**Se l'utente ha incollato l'output di `/cost` nel messaggio**: usa quei dati
per compilare la sezione Tokens & Metriche (piano API).

**In tutti gli altri casi**: procedi senza dati di costo (piano Max o dati non
disponibili). La sezione Tokens & Metriche verra' compilata con la variante
piano Max (vedi step 5).

Non chiedere `/cost` e non bloccare l'esecuzione.

### 2. Recupera il git log (se in un repository)

Esegui `git log --oneline -30` nella working directory corrente.
Usa l'output come riferimento per identificare le attivita' committate durante
la sessione, in particolare se il contesto e' stato compattato e parte della
conversazione e' andata persa.

Il git log e' un aiuto per ricostruire il *cosa*, non la base per stimare
l'effort (che richiede contesto qualitativo sulla complessita' del lavoro).

Se non sei in un repository git, salta questo step.

### 3. Identifica il contesto

Analizza la conversazione (e il git log se disponibile) per estrarre:

- **Progetto**: nome repository o progetto modificato
- **Epic**: tema o obiettivo generale della sessione (decidilo autonomamente
  analizzando commit, file modificati, conversazione)
- **Conto**: estratto dalla primary working directory secondo questi pattern:
  - `/home/fabio/_Sources/[conto]/[progetto]/` → conto = `[conto]`
  - `/home/fabio/_Project/[conto]/[progetto]/` → conto = `[conto]`
  - Se la path non corrisponde: `MANUAL`
  - Per configurazioni globali (`~/.claude/`): `GLOBAL`
- **Attivita'**: descrizione aggregata delle operazioni svolte.
  Raggruppa le operazioni correlate — non loggare ogni modifica atomica.

### 4. Breakdown effort

Stima le ore equivalenti che sarebbero servite per completare lo stesso
lavoro **manualmente senza Claude**, ripartite per dominio.

**Escludi dal conteggio** (sono meta-lavoro):
- Inizializzazione progetti tramite `/init`
- Aggiornamento file in `~/.claude/projects/*/memory/`
- Aggiornamento `~/.claude/CLAUDE.md`

**Tassonomia** (usa i valori esatti — sono le chiavi del CSV):

| Dominio | Profilo | Riferimento per la stima |
|---|---|---|
| Analisi requisiti | Analyst | ampiezza e profondita' dei documenti prodotti |
| Architettura | Senior Architect | complessita' del sistema progettato, numero decisioni |
| Implementazione algoritmica | Senior Dev | complessita' logica, pattern usati, numero componenti |
| Implementazione CRUD | Mid Dev | numero entita', operazioni standard, file generati |
| Configurazione | DevOps Engineer | numero servizi configurati, complessita' infrastruttura |
| Documentazione | Analyst | quantita' e qualita' dei documenti |
| Test | Tester | numero casi, copertura, complessita' scenari |
| Troubleshooting | Senior Dev | profondita' del problema, numero tentativi, impatto |
| Project Management | Project Manager | numero issue gestiti, documenti redatti, verifiche compliance svolte, cicli di revisione |

Arrotonda a valori ragionevoli: 0.5h, 1h, 1.5h, 2h, 3h, 4h...
Sii conservativo: in caso di dubbio usa il valore piu' basso.

### 5. Scrivi il file giornaliero

File: `~/work-log/YYYY-MM-DD.md` (usa la data odierna).
Crea il file con header `# Work Log - YYYY-MM-DD` se non esiste.
Aggiungi la voce in append se il file esiste gia'.

Se nella stessa giornata esiste gia' una voce per lo stesso progetto,
aggiungi `(sessione 2)`, `(sessione 3)`, ecc. al titolo della sezione.

Formato della voce:

```markdown
## [Nome Progetto]

- **Epic**: [tema/obiettivo generale]
- **Conto**: [conto estratto dalla path]
- **Attivita'**: [descrizione aggregata]
- **Effort**:
  | Dominio | Profilo | Ore equivalenti |
  |---|---|---|
  | [dominio] | [profilo] | ~[N]h |
  | **Totale** | | **~[N]h** |
- **Tokens & Metriche**:
  - **Sonnet 4.6**: [N] in / [N] out | cache: [N] read, [N] write | $[N]
  - **Haiku 4.5**: [N] in / [N] out | cache: [N] read, [N] write | $[N]
  - **Totale**: $[N] | API: [Xm Xs] | Wall: [Xh Xm Xs] | Code: +[N] / -[N] lines
- **Note**: [opzionale]
```

**Variante per piano Max** (quando `/cost` non e' disponibile):
```markdown
- **Tokens & Metriche**:
  - **Piano**: Max (flat rate)
  - **Modello**: [modello principale usato, es. Opus 4.6]
  - **Wall**: ~[Xh Xm] (stima) | Code: +[N] / -[N] lines
```

La wall duration si stima dal contesto della conversazione (ora primo/ultimo
messaggio se visibili, altrimenti stima approssimativa).
Le code lines si calcolano da `git diff --stat` se disponibile.

Ometti la riga Haiku 4.5 se non presente nell'output `/cost`.
Ometti la riga Note se non ci sono informazioni rilevanti da aggiungere.

### 6. Aggiorna il CSV

File: `~/work-log/work-log.csv`

Se il file non esiste, crealo con questo header:
```
data,conto,progetto,epic,dominio,profilo,ore_equivalenti,costo_usd,api_duration,wall_duration,code_added,code_removed
```

Aggiungi una riga per ogni voce Dominio/Profilo della sessione.
I dati di sessione (costo, durate, codice) si ripetono su ogni riga.
Racchiudi tra virgolette doppie i campi che contengono virgole o spazi.

**Piano Max**: usa `Max` come valore per `costo_usd`, `0` per `api_duration`,
e la wall duration stimata. Code lines da `git diff --stat` se disponibile.
