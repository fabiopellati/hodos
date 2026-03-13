---
tipo-artefatto: guida
documento: norme-ai
descrizione: norme vincolanti per l'agente AI che opera in un'opera Hodos — derivate dal protocollo
autorita: normativa
---

# Norme AI — Vincoli protocollari per l'agente

Queste norme derivano dal protocollo Hodos e hanno valore vincolante. In caso
di conflitto con istruzioni operative o arricchimenti opzionali, queste norme
prevalgono.

---

## Principi operativi

**Il processo guida l'agente, non viceversa.** Prima di qualsiasi azione,
l'agente verifica lo stato corrente del progetto (questioni aperte, note attive,
CLAUDE.md), quale questione e' in corso e quale stato ha. Non chiude questioni
senza approvazione.

**Ogni artefatto rilevante passa per una questione.** La redazione di un documento,
la creazione di diagrammi, la scrittura di skill: ogni attivita' non banale
viene tracciata con una questione aperta prima di iniziare e portata a
`pending-approval` al completamento. L'umano approva esplicitamente.

**L'umano approva le approvazioni.** L'agente non avanza da una fase alla
successiva autonomamente. Il superamento di un'approvazione richiede sempre
conferma esplicita dell'umano.

**I file di processo si aggiornano in tempo reale.** Quando una questione cambia
stato, quando viene chiusa, quando una entry va nel mastro: l'agente aggiorna
i file immediatamente, non a fine sessione.

---

## Entry nel mastro — norma sul Percorso

Ogni entry deve includere la sezione Percorso quando il ciclo ha avuto qualsiasi
complessita': stati multipli, ripensamenti, blocchi, alternative esplorate. Il
bias corretto e' includere il Percorso. L'omissione e' legittima solo quando la
decisione e' stata diretta — apertura e chiusura senza stati intermedi
significativi. Ometterla per concisione vanifica il valore del registro.

---

## Limiti dell'autonomia dell'agente

L'agente non decide autonomamente:

- Quale stato assegnare a un'approvazione (approvato / da rivedere)
- Se una questione puo' essere chiusa con domande ancora aperte
- Se avanzare alla fase successiva
- Se una RFC inbound va accettata, rifiutata o rimandata
