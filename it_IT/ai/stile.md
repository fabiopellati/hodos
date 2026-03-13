---
tipo-artefatto: guida
documento: stile
descrizione: istruzioni di stile redazionale per l'agente AI che scrive o revisiona artefatti Hodos
autorita: operativa
---

# Istruzioni di Stile Redazionale — Hodos

Questo documento e' indirizzato all'agente AI che scrive o revisiona artefatti
Hodos. Definisce la persona di riferimento e coppie di esempi prima/dopo per
ciascun tipo di documento. Gli estensori umani non sono il destinatario: si
presuppone che sappiano gia' come redigere un documento tecnico in italiano.

---

## Livello primario — `protocollo.md`, `principi.md`

**Audience**: chi valuta o adotta la metodologia. Non necessariamente tecnico.
Potrebbe essere un responsabile di progetto, un cliente, un collaboratore
esterno che vuole capire come funziona il processo prima di adottarlo.

**Persona**: scrivi come un esperto che convincerebbe un collega scettico.
Non basta dire cosa prescrive il protocollo — ogni regola porta con se' la
ragione che l'ha prodotta e il problema che risolve. Il lettore deve poter
valutare, non solo applicare.

**Esempi**

Regola senza motivazione (da evitare):
> Un rilievo con impatto non vuoto richiede almeno una questione di revisione
> collegata aperta.

Regola con motivazione (corretto):
> Un rilievo che ha gia' modificato artefatti non si chiude senza una questione
> di revisione aperta: il processo deve poter tracciare se le modifiche eseguite
> sono state valutate e, se necessario, corrette. Senza questo vincolo, un
> impatto eseguito potrebbe restare privo di verifica.

Pattern: la regola risponde prima alla domanda "perche'" e poi alla domanda
"cosa". La struttura argomentativa precede la prescrizione.

---

## Livello secondario — `guide/`

**Audience**: chi applica il processo nel lavoro quotidiano. Conosce la
metodologia ma ha bisogno di riferimenti operativi chiari e rapidi.

**Persona**: scrivi come un tecnico italiano che spiega a un collega operativo.
Le frasi sono complete e le relazioni tra concetti sono dichiarate, non lasciate
all'inferenza del lettore. L'italiano ha strutture sintattiche piu' esplicite
dell'inglese: non comprimere la frase per inseguire la concisione di una
traduzione letterale.

**Esempi**

Colon senza framing (da evitare):
> Il knowledge-provider rende la knowledge base intercambiabile senza modificare
> il core del server: lettura da filesystem locale o da repository git per tag.

Relazione dichiarata (corretto):
> Il knowledge-provider rende la knowledge base intercambiabile senza modificare
> il core del server. Le sorgenti supportate sono due: il filesystem locale e il
> repository git, con accesso per tag.

Pattern: prima del colon deve comparire una parola che nomina la categoria di
cio' che segue (sorgenti, opzioni, modalita', casi). Se quella parola manca, il
colon e' prematuro.

---

## Livello terziario — `skills/`

**Audience**: agente AI esecutore. Il documento viene letto e interpretato
da un modello linguistico, non da un umano.

**Persona**: scrivi come un ingegnere che produce una specifica di macchina.
Ogni passo e' eseguibile senza contesto esterno, senza narrativa, senza
spiegazioni rivolte a un umano. L'agente esegue: non ha bisogno di capire il
perche', ha bisogno di sapere esattamente cosa fare in ogni caso.

**Esempi**

Istruzione ambigua (da evitare):
> Identifica la questione da chiudere nel contesto.

Istruzione specifica (corretto):
> Leggi l'ID della questione dagli argomenti dello skill. Se non e' presente
> negli argomenti, mostra l'indice di questioni.md tramite AskUserQuestion e
> chiedi quale questione chiudere.

Pattern: ogni passo specifica sia il caso normale sia il caso alternativo.
Un agente non improvvisa: ogni deviazione dal percorso atteso deve avere un
ramo esplicito.

---

## Documenti di analisi — `documenti/analisi/`

**Audience**: analisti, architetti, decision-maker tecnici. Lettori con
competenza tecnica e familiarita' con il dominio del progetto.

**Persona**: scrivi come un analista che produce un documento formale
consegnabile. Ogni affermazione e' verificabile o motivata esplicitamente.
I concetti simili sono distinti, le ambiguita' terminologiche sono risolte
prima di usare il termine.

**Esempi**

Affermazione vaga (da evitare):
> Il sistema deve essere performante e scalabile.

Affermazione verificabile (corretto):
> Il sistema deve rispondere a una query standard entro 200ms con un carico
> di 100 richieste concorrenti (RF-007).

Pattern: ogni requisito o vincolo porta un criterio di verifica o un
riferimento. Termini come "buono", "veloce", "semplice" non sono requisiti.

---

## Istruzione operativa

Identifica il tipo di documento dal percorso e dalla struttura del file,
poi applica la persona del livello corrispondente. In caso di dubbio,
chiedi prima di procedere.

Questo documento e' candidato a diventare una risorsa MCP accessibile
tramite `get_protocol_rules(context="style")` (QUESTIONE-048).
