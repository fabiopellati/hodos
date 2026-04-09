---
tipo-artefatto: guida
documento: procedura-inizializzazione
descrizione: procedura operativa per inizializzare un'opera Hodos — creazione dei file di processo
autorita: operativa
---

# Procedura — Inizializzazione Opera Hodos

Quando l'operatore chiede di inizializzare Hodos, l'agente deve creare i file
di processo dell'opera. Questa procedura si applica quando la directory contiene
un CLAUDE.md con `**protocollo**: Hodos` ma manca uno o più file di processo.

## Passi

1. Recupera i template con `get_template`:
   - `questioni-file` — struttura di questioni.md
   - `mastro-file` — struttura di mastro.md
   - `notes-file` — struttura di notes.md
   - `claude-md` — struttura completa del CLAUDE.md

2. Leggi il CLAUDE.md esistente per determinare il nome dell'opera.

3. Crea i file mancanti usando i template recuperati:
   - `questioni.md` — sostituisci `{Nome Opera}` con il nome dell'opera
   - `mastro.md` — sostituisci `{Nome Opera}` con il nome dell'opera
   - `notes.md` — sostituisci `{Nome Opera}` con il nome dell'opera

4. Aggiorna il CLAUDE.md con le sezioni mancanti dal template `claude-md`:
   - `File di progetto` — lista dei file creati
   - `Stato corrente` — questioni aperte
   - `Arricchimenti abilitati` — nessuno per default

5. Non creare file che esistono già. Non modificare il contenuto di file
   esistenti diversi dal CLAUDE.md.

## Cosa non fare

- Non usare `get_protocol_rules` per l'inizializzazione: le regole operative
  servono durante il lavoro, non durante la creazione dei file.
- Non stampare riepiloghi delle norme o dei propri comportamenti: l'operatore
  vuole che i file vengano creati, non una dichiarazione di intenti.
- Non proporre commit automaticamente dopo la creazione.
