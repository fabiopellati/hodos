---
tipo-artefatto: guida
documento: regole-ingaggio
descrizione: regole di comportamento dell'agente AI di fronte a prompt ambigui in un'opera Hodos
autorita: normativa
---

# Regole di Ingaggio — Comportamento dell'Agente con Prompt Ambigui

Queste regole governano il comportamento dell'agente AI quando riceve un
prompt dall'operatore in un'opera Hodos. L'obiettivo e' evitare che l'agente
agisca sui file di processo (questioni.md, mastro.md, notes.md) senza che
l'operatore abbia espresso un'intenzione chiara e confermata.

---

## Principio fondante

In caso di ambiguita', chiedere e non agire. Un'azione non richiesta sui file
di processo e' sempre peggiore di una domanda in piu'. L'agente non deve mai
presumere l'intenzione dell'operatore quando il prompt ammette piu' di
un'interpretazione.

---

## Livelli di riconoscimento

### Livello 1 — Intenzione esplicita

L'operatore usa un termine del protocollo o un'espressione che corrisponde
univocamente a un'operazione Hodos (vedi glossario-operativo.md).

Esempio: "apri una questione di rilievo sulla gestione degli errori"

Comportamento dell'agente: chiede conferma dei parametri (tipo, titolo,
descrizione) e procede solo dopo l'approvazione dell'operatore.

### Livello 2 — Intenzione probabile

L'operatore usa un'espressione che suggerisce un'operazione Hodos ma non
la identifica univocamente, oppure il tipo di operazione non e' chiaro.

Esempio: "registra questo: il formato del file non supporta caratteri unicode"

Comportamento dell'agente: segnala le operazioni possibili e chiede quale
intende l'operatore. Non opera sui file di processo.

Modello di risposta: "Vuoi che apra una questione (di rilievo, revisione
o anomalia), che aggiunga una nota, o e' un'osservazione nel contesto
della conversazione?"

### Livello 3 — Nessun riconoscimento

L'operatore non usa termini riconducibili a operazioni Hodos. Il prompt e'
una domanda, un'istruzione generica, o una conversazione.

Esempio: "come funziona la gestione degli errori nel protocollo?"

Comportamento dell'agente: risponde normalmente senza toccare i file di
processo. Non suggerisce di aprire questioni o note a meno che non emerga
un motivo concreto durante la risposta.

---

## Regole vincolanti

1. **Mai operare sui file di processo senza conferma esplicita.** Nessuna
   eccezione. Anche quando l'intenzione sembra chiara (livello 1), l'agente
   chiede conferma dei parametri prima di scrivere.

2. **Mai interpretare un prompt ambiguo come istruzione di operare.** Se
   l'agente non e' sicuro che l'operatore voglia modificare un file di
   processo, non lo modifica. Chiedere e' sempre lecito; agire senza
   conferma non lo e' mai.

3. **Mai suggerire operazioni non richieste.** L'agente non propone di aprire
   questioni, aggiungere note o aggiornare stati se l'operatore non ha
   espresso l'intenzione di farlo. Il suggerimento proattivo e' una forma
   di pressione che l'operatore non ha chiesto.

4. **Distinguere il tipo prima di operare.** Se l'operatore chiede di
   aprire una questione ma non specifica il tipo (rilievo, revisione,
   anomalia), l'agente lo chiede. Se il contesto rende il tipo evidente,
   l'agente lo propone e chiede conferma.

5. **Non confondere nota e questione.** Se l'operatore descrive un problema
   con un termine generico ("registra", "segna", "documenta"), l'agente
   chiede se intende una nota (informazione senza decisione) o una
   questione (problema che richiede risoluzione). Non scegliere per lui.

6. **Rispettare il silenzio.** Se l'operatore non menziona Hodos ne' usa
   termini del protocollo, l'agente non introduce il protocollo nella
   conversazione. L'operatore potrebbe voler semplicemente conversare,
   chiedere aiuto tecnico, o ragionare ad alta voce.

---

## Sequenza decisionale

Quando l'agente riceve un prompt, segue questa sequenza:

1. Il prompt contiene un termine riconoscibile del protocollo Hodos?
   - No: rispondi normalmente (livello 3)
   - Si': prosegui

2. Il termine identifica univocamente un'operazione?
   - No: chiedi chiarimento (livello 2)
   - Si': prosegui

3. I parametri dell'operazione sono completi (tipo, target, contenuto)?
   - No: chiedi i parametri mancanti
   - Si': chiedi conferma e, ottenuta, esegui
