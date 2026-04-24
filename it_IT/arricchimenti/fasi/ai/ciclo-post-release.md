---
tipo-artefatto: guida
autorita: operativa
documento: ciclo-post-release
descrizione: Ciclo iterativo post-release per opere Hodos in produzione
fase: trasversale
---

# Ciclo post-release

Dopo P4 approvato e prima release taggata su `main`, l'opera entra nel
regime iterativo post-release. Ogni release successiva è un ciclo compiuto,
non un regime indefinito.

**Modello**: il backlog alimenta ogni ciclo. Ogni ciclo produce una release.

---

## Condizione di ingresso

Il ciclo post-release si attiva quando:
- P4 è approvato
- La prima release è taggata su `main` con versione semantica

Prima di questa condizione, non esiste ancora un "in produzione" a cui riferirsi.

---

## Modello iterativo

Ogni ciclo post-release percorre quattro passi:

1. **Raccolta**: il backlog raccoglie richieste, bug segnalati, miglioramenti
   emersi post-consegna
2. **Prioritizzazione**: chi governa seleziona e ordina gli item per la
   release successiva
3. **Mini-ciclo P1-P2-P3**: l'insieme degli item selezionati percorre un
   ciclo ridotto di analisi, realizzazione e integrazione
4. **Release (P4)**: il ciclo si chiude con una nuova release approvata
   e taggata su `main`

La granularità del mini-ciclo è proporzionale alla complessità degli item.
Per fix minori, P1 può ridursi a pochi appunti di analisi. Per evoluzioni
significative, il percorso completo è appropriato.

---

## Tracciabilità

Il lavoro post-release si traccia con questioni nel normale ciclo Hodos:
- Una questione di revisione per ogni release (copre l'intero mini-ciclo)
- Questioni operative per item significativi

Non è necessaria una struttura di documenti separata: si estendono le
directory esistenti o se ne aggiungono di nuove nella stessa opera.

---

## Il ruolo del backlog

Il backlog è lo strumento di raccolta e prioritizzazione degli item
post-release. Non è un documento di fase: è trasversale al ciclo.

Negli arricchimenti che prevedono un file di backlog (`backlog.md`),
questo file persiste tra un ciclo e l'altro e raccoglie item in attesa
di essere inclusi in una release futura.

---

## Hotfix

Un hotfix è un caso speciale: un bug critico in produzione che non può
attendere il prossimo ciclo ordinario. Si realizza su un branch `hotfix/*`
(vedi `arricchimento-git`), bypassa il normale backlog, e produce una release
corretta direttamente su `main`.

La questione per un hotfix è distinta dalle questioni del ciclo ordinario
e si chiude con la release del fix.
