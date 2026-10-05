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
CLAUDE.md), quale questione è in corso e quale stato ha. Non chiude questioni
senza approvazione.

**Ogni artefatto rilevante passa per una questione.** La redazione di un documento,
la creazione di diagrammi, la scrittura di skill: ogni attività non banale
viene tracciata con una questione aperta prima di iniziare e portata a
`pending-approval` al completamento. L'umano approva esplicitamente.

**L'umano approva le approvazioni.** L'agente non avanza da una fase alla
successiva autonomamente. Il superamento di un'approvazione richiede sempre
conferma esplicita dell'umano.

**I file di processo si aggiornano in tempo reale.** Quando una questione cambia
stato, quando viene chiusa, quando una voce va nel mastro: l'agente aggiorna
i file immediatamente, non a fine sessione. Dopo aver modificato un file-elemento
in `questioni/`, `note/` o `mastro/`, l'agente rigenera l'indice corrispondente.

---

## Norme del protocollo che l'agente applica

L'agente osserva anche norme che hanno sede nel protocollo o nei template, e che qui non si ripetono.
Vanno lette nella loro sede, che è la sola autorevole:

- la forma segregata, gli indici derivati e il doppio regime del mastro: `protocollo.md`, Art. 3, Art. 6 e Art. 10;
- la mutabilità del corpo della questione aperta e il suo consolidamento: `protocollo.md`, Art. 4 commi 6, 7 e 8;
- il Percorso nella voce del mastro: `protocollo.md`, Art. 6 commi 5 e 6.

---

## Retrieval obbligatorio del template

Prima di redigere qualsiasi artefatto protocollare
(questione, nota, commento, entry del mastro, RFC,
voce di attività), l'agente deve consultare il template
corrispondente con `get_template` nella sessione
corrente. Non è sufficiente basarsi sulla struttura
ricordata da sessioni precedenti o dal contesto già
caricato: il knowledge base potrebbe essere stato
aggiornato e la struttura ricordata potrebbe essere
incompleta o non conforme.

Il costo del retrieval è trascurabile rispetto al costo
della correzione manuale di un artefatto non conforme.

---

## Limiti dell'autonomia dell'agente

L'agente non decide autonomamente:

- Quale stato assegnare a un'approvazione (approvato / da rivedere)
- Se una questione può essere chiusa con domande ancora aperte
- Se avanzare alla fase successiva
- Se una RFC inbound va accettata, rifiutata o rimandata
