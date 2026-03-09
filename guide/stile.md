# Guida allo Stile Redazionale — Hodos

Gli artefatti di Hodos hanno audience e tono distinti per livello. Questo
documento definisce le aspettative redazionali per ciascun tipo. E' destinato
sia agli estensori umani sia agli agenti AI che scrivono o revisionano documenti
nel contesto di un'opera Hodos.

---

## Livello primario — `protocollo.md`, `principi.md`

**Audience**: chi valuta o adotta la metodologia. Non necessariamente tecnico.
Potrebbe essere un responsabile di progetto, un cliente, un collaboratore
esterno che vuole capire come funziona il processo prima di adottarlo.

**Tono**: valutativo e motivazionale. Ogni regola ha una ragione esplicita.
Il lettore deve capire non solo *cosa* prescrive il protocollo, ma *perche'*
quella scelta e' stata fatta e quale problema risolve.

**Stile**:
- Frasi complete, linguaggio accessibile
- Motivazioni prima delle regole, non dopo
- Struttura argomentativa, non operativa

**Evita**:
- Checklist e istruzioni step-by-step
- Formulazioni algoritmiche ("se X allora Y")
- Tono da manuale tecnico o da specifica software
- Regole senza motivazione

---

## Livello secondario — `guide/`

**Audience**: chi applica il processo nel lavoro quotidiano. Conosce la
metodologia ma ha bisogno di riferimenti operativi chiari e rapidi.

**Tono**: operativo e diretto. Orientato all'azione, senza prolissita'.

**Stile**:
- Conciso, esempi pratici dove utili
- Rimandi mirati e poco frequenti
- L'italiano ha regole sintattiche che producono frasi piu' verbose delle
  equivalenti in inglese: non comprimere eccessivamente. Una traduzione
  letterale dall'inglese suona spesso sintetica al punto da risultare
  rigida o meccanica. Preferire la costruzione naturale della frase italiana.

**Evita**:
- Motivazioni verbose (appartengono al livello primario)
- Ripetizioni del contenuto del protocollo
- Rimandi a catena che costringono il lettore a navigare piu' documenti
- Costruzioni sintetiche che sacrificano la leggibilita'

---

## Livello terziario — `skills/`

**Audience**: agente AI esecutore. Il documento viene letto e interpretato
da un modello linguistico, non da un umano.

**Tono**: procedurale e compatto.

**Stile**:
- Autocontenuto: ogni passo e' eseguibile senza contesto esterno
- Formulato per efficienza del modello: istruzioni dirette, senza narrativa
- Struttura a passi numerati o con titoli chiari

**Evita**:
- Tono narrativo o descrittivo
- Ridondanza e ripetizioni
- Spiegazioni destinate a un lettore umano
- Motivazioni esplicite (l'agente esegue, non valuta)

---

## Documenti di analisi — `documenti/analisi/`

**Audience**: analisti, architetti, decision-maker tecnici. Lettori con
competenza tecnica e familiarita' con il dominio del progetto.

**Tono**: analitico e strutturato.

**Stile**:
- Vocabolario di dominio usato in modo coerente
- Distinzioni esplicite tra concetti simili
- Rigore descrittivo: ogni affermazione e' verificabile o motivata

**Evita**:
- Opinioni implicite presentate come fatti
- Affermazioni vaghe o non fondate
- Ambiguita' terminologica
- Mistura di livelli di astrazione diversi nello stesso paragrafo

---

## Nota per gli agenti AI

Quando scrivi o revisioni un documento, identifica il tipo dal percorso e
dalla struttura del file, poi applica le regole del livello corrispondente.
In caso di dubbio sul tipo, chiedi prima di procedere.

Questo documento e' candidato a diventare una risorsa MCP accessibile
tramite `get_protocol_rules(context="style")` quando il server Hodos MCP
sara' disponibile (QUESTIONE-048).
