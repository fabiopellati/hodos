# FAQ — Hodos

Domande operative frequenti e disambiguazioni per chi usa Hodos.

Formato: domanda e risposta diretta. Per il testo normativo completo, consulta
`protocollo.md` e le guide in `guide/`.

---

## Questioni

**Cos'e' una questione?**

Una questione e' qualcosa di cui ci si deve occupare, tracciato
formalmente. Ha un tipo (rilievo, revisione o anomalia), uno stato che
evolve nel corso del ciclo e una storia immutabile che registra ogni evento
significativo. Quando e' risolta, viene rimossa da `questioni.md` e la sua
risoluzione viene registrata nel mastro.

**Quando apro un rilievo invece di una revisione?**

Apri un rilievo se hai identificato qualcosa ma non sei ancora pronto ad agire.
Apri una revisione se sai gia' cosa fare e sei pronto a farlo. Il criterio e'
l'intenzione al momento dell'apertura: il rilievo registra conoscenza, la
revisione esegue un cambiamento.

**Posso cambiare il tipo di una questione dopo l'apertura?**

No. Il tipo e' immutabile. Se la classificazione si rivela errata, chiudi la
questione e riaprila con il tipo corretto.

**Un rilievo puo' modificare artefatti nel corso del suo ciclo?**

No. Il rilievo registra conoscenza e identifica cosa vale la pena fare, non lo
fa. Se durante l'analisi emerge una soluzione chiara e sei pronto ad agire, apri
una revisione e agisci tramite essa.

**Posso modificare la descrizione di una questione dopo l'apertura?**

No. Il corpo della questione (Descrizione, Domande aperte, Impatto) e' immutabile.
Per aggiungere una rettifica o un'integrazione, usa la sezione Commenti
(COMMENTO-NNN, numerazione locale alla questione).

**La motivazione nella Storia deve dire cosa ho fatto o perche'?**

Deve rispondere al "perche'". Esempio non corretto: "aggiornato il protocollo".
Esempio corretto: "il testo precedente non distingueva i due casi, generando
ambiguita' operative".

**Chi porta una questione a pending-approval?**

Chi realizza. E' il segnale protocollare di consegna verso chi governa.
Il ciclo completo: chi governa apre e assegna, chi realizza porta a in-progress,
chi realizza porta a pending-approval, chi governa chiude e scrive nel mastro.

**Come chiudo un rilievo che ha il campo Impatto non vuoto?**

Prima di chiudere, verifica che esista almeno una questione di tipo revisione
aperta nel campo Questioni collegate. La revisione non deve essere completata,
ma deve esistere a testimonianza che il lavoro di applicazione e' stato preso
in carico.

**Come chiudo un rilievo se la decisione e' "non adottare"?**

Se la decisione e' di non adottare il rilievo, non compilare il campo Impatto.
Con Impatto vuoto, la precondizione sulla revisione collegata non si applica
e il rilievo puo' essere chiuso direttamente.

**Posso chiudere una questione senza passare per pending-approval?**

Si', se la decisione e' stata diretta e non richiede approvazione esplicita.
Il passaggio per pending-approval e' obbligatorio quando chi realizza e chi
governa sono persone diverse, o quando il processo lo richiede.

**Posso aggiungere voci al campo Impatto dopo l'apertura?**

Si'. Il campo Impatto e' mutabile per addizione: durante l'esecuzione possono
emergere dipendenze non previste. Si possono aggiungere nuove voci in qualsiasi
momento documentando il motivo. Una voce esistente non si cancella, ma si puo'
dichiarare inattuata con motivazione esplicita inline:

```
- artefatto — descrizione — inattuata: motivazione
```

**Cosa faccio se una questione ha domande aperte al momento della chiusura?**

L'operatore viene avvisato prima di procedere. La presenza di domande aperte
non blocca meccanicamente la chiusura, ma richiede conferma esplicita.

---

## Ciclo degli stati

**Cos'e' il ciclo degli stati?**

Il ciclo degli stati descrive il percorso che una questione compie
dall'apertura alla chiusura. Ogni transizione e' accompagnata da una
motivazione nella Storia. Gli stati possibili sono: `open`, `in-progress`,
`pending-approval`, `pending-rfc`, `in-verification`, `deferred`, `closed`.

**Quale stato indica che l'esecuzione ha preso in carico la questione?**

Lo stato `in-progress`. E' il segnale che l'esecuzione ha avviato il lavoro.
Solo l'esecuzione porta una questione a `in-progress`.

**Dopo in-verification, a quale stato torna la questione?**

Torna a `open`. Quando chi governa completa la verifica della risposta RFC,
la questione torna a `open` in modo che chi realizza possa riprenderla
autonomamente con il proprio `in-progress`. La firma di presa in carico
rimane di chi realizza.

---

## RFC

**Cos'e' una RFC?**

Una RFC e' un documento formale generato quando una questione richiede
l'intervento di un team esterno (Team-B). E' bidirezionale: Team-A descrive
la richiesta, Team-B compila la risposta nella sezione Response RFC. Il
documento e' autocontenuto e leggibile senza conoscere il progetto richiedente.

**Quando genero una RFC?**

Quando una questione non puo' essere risolta senza intervento di un team
esterno (Team-B). La questione deve essere portata a `pending-rfc` prima di
generare il documento.

**La risposta RFC chiude la questione di origine?**

No. La risposta RFC sblocca la fase di verifica. Solo se la verifica ha esito
positivo la questione puo' progredire. Il "done" di Team-B non chiude la
questione: e' Team-A che verifica e decide.

**Chi gestisce la ricezione di una risposta RFC?**

Chi governa. La questione pending-rfc e' stata aperta da chi governa;
la risposta torna a chi governa, che la interpreta, valuta le implicazioni
e apre le questioni figlie se necessario. Chi realizza puo' materialmente
ricevere il documento, ma l'interpretazione e le decisioni di processo
appartengono a chi governa.

**Cosa faccio se la risposta RFC arriva parziale?**

La questione rimane in `pending-rfc`. Aggiungi voci di storia e commenti per
tracciare cosa e' stato ricevuto e cosa manca. Il meccanismo storia e commenti
e' sufficiente per la tracciabilita'; non e' necessaria una transizione di stato.

**Qual e' il formato del nome file di una RFC?**

`rfc-[progetto]-YYYY-MM-DD-slug.md`. La tracciabilita' verso la questione di
origine e' garantita dal campo `**Questione di origine**` nell'intestazione
del documento, non dal nome file.

---

## Mastro

**Cos'e' il mastro?**

Il mastro e' il registro immutabile delle decisioni prese. Contiene solo
cicli chiusi: ogni voce descrive cosa e' emerso, cosa e' stato deciso e
perche'. Le voci piu' recenti sono in cima e nessuna voce viene mai
modificata dopo la scrittura.

**Quando include la sezione Percorso?**

Quando il ciclo ha avuto complessita': stati multipli, ripensamenti, alternative
valutate o scartate. Se la questione e' stata aperta e chiusa senza stati
intermedi significativi, la sezione si omette. In caso di dubbio, includila.

**Posso correggere un'entry nel mastro?**

No. Il mastro e' immutabile. Le voci vengono aggiunte in cima e non vengono
mai modificate dopo la scrittura.

---

## Note

**Cos'e' una nota?**

Una nota e' un'osservazione, un memo o un'idea in incubazione che non
richiede ancora una decisione formale. Non ha stati, non produce una voce
nel mastro e non richiede approvazione. Il suo ciclo di vita e' libero:
puo' essere eliminata, archiviata nel mastro quando ha esaurito il suo
scopo, oppure restare indefinitamente in `note.md`.

**Qual e' la differenza tra una nota e una questione?**

Una nota non richiede una decisione formale: e' un'osservazione, un memo, un'idea
in incubazione. Non ha stati, non produce una voce nel mastro, non richiede
approvazione. Una questione traccia qualcosa di cui ci si deve occupare e richiede
analisi, decisione e registrazione del risultato.

---

## Ruoli

**Cosa sono i ruoli in Hodos?**

Hodos distingue due ruoli fondamentali: chi governa (prende le decisioni,
approva, scrive nel mastro) e chi realizza (esegue, consegna tramite
`pending-approval`). Nella stessa persona i due ruoli coesistono senza
frizione. Hodos non prescrive chi assuma quale ruolo: e' una scelta di
chi adotta Hodos.

**Chi puo' aprire una questione?**

Chiunque nel team (governance o esecuzione). L'apertura non e' un atto
esclusivo della governance.

**Chi chiude una questione?**

Chi governa. La chiusura include la scrittura nel mastro ed e' un atto di
approvazione e registrazione, non solo di completamento tecnico.
