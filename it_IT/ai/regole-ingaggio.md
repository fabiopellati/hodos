---
tipo-artefatto: guida
documento: regole-ingaggio
descrizione: regole di comportamento dell'agente AI di fronte a prompt ambigui in un'opera Hodos
autorita: normativa
---

# Regole di Ingaggio — Comportamento dell'Agente con Prompt Ambigui

Queste regole governano il comportamento dell'agente AI quando riceve un
prompt dall'operatore in un'opera Hodos. L'obiettivo è evitare che l'agente
agisca sui file di processo (questioni.md, mastro.md, notes.md) senza che
l'operatore abbia espresso un'intenzione chiara e confermata.

---

## Principio fondante

In caso di ambiguità, chiedere e non agire. Un'azione non richiesta sui file
di processo è sempre peggiore di una domanda in più. L'agente non deve mai
presumere l'intenzione dell'operatore quando il prompt ammette più di
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
la identifica univocamente, oppure il tipo di operazione non è chiaro.

Esempio: "registra questo: il formato del file non supporta caratteri unicode"

Comportamento dell'agente: segnala le operazioni possibili e chiede quale
intende l'operatore. Non opera sui file di processo.

Modello di risposta: "Vuoi che apra una questione (di rilievo, revisione
o anomalia), che aggiunga una nota, o è un'osservazione nel contesto
della conversazione?"

### Livello 3 — Nessun riconoscimento

L'operatore non usa termini riconducibili a operazioni Hodos. Il prompt è
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
   l'agente non è sicuro che l'operatore voglia modificare un file di
   processo, non lo modifica. Chiedere è sempre lecito; agire senza
   conferma non lo è mai.

3. **Non esercitare pressione per formalizzare.** L'agente non propone
   ripetutamente di aprire questioni, aggiungere note o aggiornare stati.
   Se l'operatore non raccoglie una proposta, l'agente non la reitera.
   Una segnalazione puntuale e soggetta a conferma è lecita quando le
   condizioni della regola 8 sono soddisfatte; la pressione ricorrente
   non lo è mai.

4. **Distinguere il tipo prima di operare.** Se l'operatore chiede di
   aprire una questione ma non specifica il tipo (rilievo, revisione,
   anomalia), l'agente lo chiede. Se il contesto rende il tipo evidente,
   l'agente lo propone e chiede conferma.

5. **Non confondere nota e questione.** Se l'operatore descrive un problema
   con un termine generico ("registra", "segna", "documenta"), l'agente
   chiede se intende una nota (informazione senza decisione) o una
   questione (problema che richiede risoluzione). Non scegliere per lui.

6. **Rispettare il silenzio.** Se l'operatore non menziona Hodos né usa
   termini del protocollo, l'agente non introduce il protocollo nella
   conversazione. L'operatore potrebbe voler semplicemente conversare,
   chiedere aiuto tecnico, o ragionare ad alta voce.

7. **Verificare il contesto prima di creare.** Prima di proporre l'apertura
   di una nuova questione o nota, l'agente verifica se il contenuto del
   prompt è correlato a questioni già aperte. Se il prompt riguarda lo
   stesso tema di una questione esistente, l'agente include tra le opzioni
   proposte anche l'aggiunta di un commento alla questione correlata.
   Non aprire una seconda questione sullo stesso tema senza che l'operatore
   lo chieda esplicitamente.

8. **Soglia di cristallizzazione.** Quando una conversazione esplorativa
   — non avviata come operazione Hodos — ha prodotto conoscenza che
   modifica la comprensione del dominio, l'agente può segnalare
   all'operatore l'opportunità di cristallizzare la discussione in un
   rilievo. La segnalazione è lecita quando la conversazione ha raggiunto
   una soglia riconoscibile: confini del problema chiariti, implicazioni
   o impatti potenziali emersi, domande aperte identificate. La
   segnalazione è soggetta a tre vincoli:
   a) va proposta una sola volta per conversazione sullo stesso tema;
   b) non deve interrompere il flusso del ragionamento in corso;
   c) richiede conferma esplicita dell'operatore prima di qualsiasi
      azione sui file di processo.

---

## Sequenza decisionale

Quando l'agente riceve un prompt, segue questa sequenza:

1. Il prompt contiene un termine riconoscibile del protocollo Hodos?
   - No: rispondi normalmente (livello 3)
   - Sì: prosegui

2. Esistono questioni aperte correlate al contenuto del prompt?
   - Sì: includi tra le opzioni l'aggiunta di un commento alla questione
     correlata. Non presumere che l'operatore voglia una nuova entità.
   - No: prosegui

3. Il termine identifica univocamente un'operazione?
   - No: chiedi chiarimento (livello 2)
   - Sì: prosegui

4. I parametri dell'operazione sono completi (tipo, target, contenuto)?
   - No: chiedi i parametri mancanti
   - Sì: chiedi conferma e, ottenuta, esegui
