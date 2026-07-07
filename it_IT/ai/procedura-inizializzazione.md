---
tipo-artefatto: guida
documento: procedura-inizializzazione
descrizione: procedura operativa per inizializzare un'opera Hodos — creazione dei file di processo
autorita: operativa
---

# Procedura — Inizializzazione Opera Hodos

Quando l'operatore chiede di inizializzare Hodos, l'agente deve creare la
struttura di processo dell'opera nella forma segregata. Questa procedura si
applica quando la directory contiene un CLAUDE.md con `**protocollo**: Hodos`
ma manca uno o più elementi di processo.

Nella forma segregata gli strumenti di governo sono collezioni: una cartella
per famiglia (`questioni/`, `note/`, `mastro/`), un file per elemento, più un
indice (`questioni.md`, `note.md`, `mastro.md`) che è proiezione derivata dei
frontmatter e viene rigenerato, non scritto a mano.

## Passi

1. Recupera i template con `get_template`:
   - `questioni-file` — struttura dell'indice questioni.md
   - `mastro-file` — struttura dell'indice mastro.md
   - `notes-file` — struttura dell'indice note.md
   - `claude-md` — struttura completa del CLAUDE.md

2. Leggi il CLAUDE.md esistente per determinare il nome dell'opera.

3. Crea le cartelle di collezione mancanti, vuote: `questioni/`, `note/`,
   `mastro/`. All'inizializzazione non contengono ancora elementi.

4. Crea gli indici mancanti usando i template recuperati, sostituendo
   `{Nome Opera}` con il nome dell'opera e includendo il marcatore di file
   generato:
   - `questioni.md` — indice vuoto delle questioni
   - `mastro.md` — indice vuoto del mastro
   - `note.md` — indice vuoto delle note

5. Aggiorna il CLAUDE.md con le sezioni mancanti dal template `claude-md`:
   - `File di progetto` — le cartelle di collezione e i rispettivi indici
   - `Stato corrente` — questioni aperte
   - `Arricchimenti abilitati` — nessuno per default

6. Non creare elementi o indici che esistono già. Non modificare il contenuto
   di file esistenti diversi dal CLAUDE.md.

7. La generazione e la rigenerazione degli indici a partire dai frontmatter è
   realizzata da uno strumento dell'opera, secondo lo stack scelto dal
   progetto: il protocollo prescrive la forma, non l'implementazione.

## Cosa non fare

- Non usare `get_protocol_rules` per l'inizializzazione: le regole operative
  servono durante il lavoro, non durante la creazione dei file.
- Non stampare riepiloghi delle norme o dei propri comportamenti: l'operatore
  vuole che i file vengano creati, non una dichiarazione di intenti.
- Non proporre commit automaticamente dopo la creazione.
