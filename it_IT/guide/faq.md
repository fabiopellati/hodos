# FAQ — Hodos

Domande operative frequenti e disambiguazioni per chi usa Hodos.

Formato: domanda e risposta diretta. Per il testo normativo completo, consulta
`protocollo.md` e le guide in `guide/`.

---

## Questioni

**Cos'è una questione?**

Una questione è qualcosa di cui ci si deve occupare, tracciato
formalmente. Ha un tipo (rilievo, revisione o anomalia), uno stato che
evolve nel corso del ciclo e una storia immutabile che registra ogni evento
significativo. Quando è risolta, viene rimossa da `questioni.md` e la sua
risoluzione viene registrata nel mastro.

**Quando apro un rilievo invece di una revisione?**

Apri un rilievo se hai identificato qualcosa ma non sei ancora pronto ad agire.
Apri una revisione se sai già cosa fare e sei pronto a farlo. Il criterio è
l'intenzione al momento dell'apertura: il rilievo registra conoscenza, la
revisione esegue un cambiamento.

**Posso cambiare il tipo di una questione dopo l'apertura?**

No. Il tipo è immutabile. Se la classificazione si rivela errata, chiudi la
questione e riaprila con il tipo corretto.

**Un rilievo può modificare artefatti nel corso del suo ciclo?**

No. Il rilievo registra conoscenza e identifica cosa vale la pena fare, non lo
fa. Se durante l'analisi emerge una soluzione chiara e sei pronto ad agire, apri
una revisione e agisci tramite essa.

**Posso modificare la descrizione di una questione dopo l'apertura?**

No. Il corpo della questione (Descrizione, Domande aperte, Impatto) è immutabile.
Per aggiungere una rettifica o un'integrazione, usa la sezione Commenti
(COMMENTO-NNN, numerazione locale alla questione).

**La motivazione nella Storia deve dire cosa ho fatto o perché?**

Deve rispondere al "perché". Esempio non corretto: "aggiornato il protocollo".
Esempio corretto: "il testo precedente non distingueva i due casi, generando
ambiguità operative".

**Chi porta una questione a pending-approval?**

Chi realizza. È il segnale protocollare di consegna verso chi governa.
Il ciclo completo: chi governa apre e assegna, chi realizza porta a in-progress,
chi realizza porta a pending-approval, chi governa chiude e scrive nel mastro.

**Come chiudo un rilievo che ha il campo Impatto non vuoto?**

Prima di chiudere, verifica che esista almeno una questione di tipo revisione
aperta nel campo Questioni collegate. La revisione non deve essere completata,
ma deve esistere a testimonianza che il lavoro di applicazione è stato preso
in carico.

**Come chiudo un rilievo se la decisione è "non adottare"?**

Se la decisione è di non adottare il rilievo, non compilare il campo Impatto.
Con Impatto vuoto, la precondizione sulla revisione collegata non si applica
e il rilievo può essere chiuso direttamente.

**Posso chiudere una questione senza passare per pending-approval?**

Sì, se la decisione è stata diretta e non richiede approvazione esplicita.
Il passaggio per pending-approval è obbligatorio quando chi realizza e chi
governa sono persone diverse, o quando il processo lo richiede.

**Posso aggiungere voci al campo Impatto dopo l'apertura?**

Sì. Il campo Impatto è mutabile per addizione: durante l'esecuzione possono
emergere dipendenze non previste. Si possono aggiungere nuove voci in qualsiasi
momento documentando il motivo. Una voce esistente non si cancella, ma si può
dichiarare inattuata con motivazione esplicita inline:

```
- artefatto — descrizione — inattuata: motivazione
```

**Cosa faccio se una questione ha domande aperte al momento della chiusura?**

L'operatore viene avvisato prima di procedere. La presenza di domande aperte
non blocca meccanicamente la chiusura, ma richiede conferma esplicita.

---

## Ciclo degli stati

**Cos'è il ciclo degli stati?**

Il ciclo degli stati descrive il percorso che una questione compie
dall'apertura alla chiusura. Ogni transizione è accompagnata da una
motivazione nella Storia. Gli stati possibili sono: `open`, `in-progress`,
`pending-approval`, `pending-rfc`, `in-verification`, `deferred`, `closed`.

**Quale stato indica che l'esecuzione ha preso in carico la questione?**

Lo stato `in-progress`. È il segnale che l'esecuzione ha avviato il lavoro.
Solo l'esecuzione porta una questione a `in-progress`.

**Dopo in-verification, a quale stato torna la questione?**

Torna a `open`. Quando chi governa completa la verifica della risposta RFC,
la questione torna a `open` in modo che chi realizza possa riprenderla
autonomamente con il proprio `in-progress`. La firma di presa in carico
rimane di chi realizza.

---

## RFC

**Cos'è una RFC?**

Una RFC è un documento formale generato quando una questione richiede
l'intervento di un team esterno (Team-B). È bidirezionale: Team-A descrive
la richiesta, Team-B compila la risposta nella sezione Response RFC. Il
documento è autocontenuto e leggibile senza conoscere il progetto richiedente.

**Quando genero una RFC?**

Quando una questione non può essere risolta senza intervento di un team
esterno (Team-B). La questione deve essere portata a `pending-rfc` prima di
generare il documento.

**La risposta RFC chiude la questione di origine?**

No. La risposta RFC sblocca la fase di verifica. Solo se la verifica ha esito
positivo la questione può progredire. Il "done" di Team-B non chiude la
questione: è Team-A che verifica e decide.

**Chi gestisce la ricezione di una risposta RFC?**

Chi governa. La questione pending-rfc è stata aperta da chi governa;
la risposta torna a chi governa, che la interpreta, valuta le implicazioni
e apre le questioni figlie se necessario. Chi realizza può materialmente
ricevere il documento, ma l'interpretazione e le decisioni di processo
appartengono a chi governa.

**Cosa faccio se la risposta RFC arriva parziale?**

La questione rimane in `pending-rfc`. Aggiungi voci di storia e commenti per
tracciare cosa è stato ricevuto e cosa manca. Il meccanismo storia e commenti
è sufficiente per la tracciabilità; non è necessaria una transizione di stato.

**Qual è il formato del nome file di una RFC?**

`rfc-[progetto]-YYYY-MM-DD-slug.md`. La tracciabilità verso la questione di
origine è garantita dal campo `**Questione di origine**` nell'intestazione
del documento, non dal nome file.

**Posso usare la RFC per una comunicazione senza attesa di risposta?**

La RFC è progettata per un ciclo bidirezionale con attesa della risposta.
Per comunicare qualcosa a un team esterno senza bloccare una questione, usa
una nota in `notes.md` che documenta cosa è stato comunicato e a chi: la
nota non entra in `pending-rfc` e non blocca nessuna questione. In alternativa,
alcuni team usano il formato RFC dichiarando il tipo nell'intestazione
(`Tipo: informativa`) senza portare la questione a `pending-rfc`; il ciclo
della questione di origine prosegue indipendentemente. Questa variante non è
regolamentata dal protocollo.

---

## Mastro

**Cos'è il mastro?**

Il mastro è il registro immutabile delle decisioni prese. Contiene solo
cicli chiusi: ogni voce descrive cosa è emerso, cosa è stato deciso e
perché. Le voci più recenti sono in cima e nessuna voce viene mai
modificata dopo la scrittura.

**Quando include la sezione Percorso?**

Quando il ciclo ha avuto complessità: stati multipli, ripensamenti, alternative
valutate o scartate. Se la questione è stata aperta e chiusa senza stati
intermedi significativi, la sezione si omette. In caso di dubbio, includila.

**Posso correggere un'entry nel mastro?**

No. Il mastro è immutabile. Le voci vengono aggiunte in cima e non vengono
mai modificate dopo la scrittura.

---

## Note

**Cos'è una nota?**

Una nota è un'osservazione, un memo o un'idea in incubazione che non
richiede ancora una decisione formale. Non ha stati, non produce una voce
nel mastro e non richiede approvazione. Il suo ciclo di vita è libero:
può essere eliminata, archiviata nel mastro quando ha esaurito il suo
scopo, oppure restare indefinitamente in `note.md`.

**Qual è la differenza tra una nota e una questione?**

Una nota non richiede una decisione formale: è un'osservazione, un memo, un'idea
in incubazione. Non ha stati, non produce una voce nel mastro, non richiede
approvazione. Una questione traccia qualcosa di cui ci si deve occupare e richiede
analisi, decisione e registrazione del risultato.

---

## Ruoli

**Cosa sono i ruoli in Hodos?**

Hodos distingue due ruoli fondamentali: chi governa (prende le decisioni,
approva, scrive nel mastro) e chi realizza (esegue, consegna tramite
`pending-approval`). Nella stessa persona i due ruoli coesistono senza
frizione. Hodos non prescrive chi assuma quale ruolo: è una scelta di
chi adotta Hodos.

**Chi può aprire una questione?**

Chiunque nel team (governance o esecuzione). L'apertura non è un atto
esclusivo della governance.

**Chi chiude una questione?**

Chi governa. La chiusura include la scrittura nel mastro ed è un atto di
approvazione e registrazione, non solo di completamento tecnico.
