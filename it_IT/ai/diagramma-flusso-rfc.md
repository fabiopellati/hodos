---
tipo-artefatto: guida
documento: diagramma-flusso-rfc
descrizione: diagramma e riferimento visivo del flusso RFC outbound e inbound
autorita: informativa
---

# Flusso RFC

Riferimento visivo: `../diagrams/flusso-rfc.puml`

Una RFC viene emessa quando una questione richiede intervento nell'ambito di
competenza di un attore esterno. È autocontenuta: leggibile senza conoscere
la storia interna dell'opera richiedente. La RFC è bidirezionale: l'attore
ricevente compila la sezione Response RFC e restituisce il documento.

---

## RFC Outbound

| Passo | Chi | Azione | Stato questione |
|---|---|---|---|
| 1 | Team-A | questione richiede intervento esterno | in-progress |
| 2 | Team-A | genera RFC e consegna a Team-B | pending-rfc |
| 3 | Team-B | compila Response RFC e restituisce | pending-rfc |
| 4 | Team-A | avvia verifica | in-verification |
| 5a | Team-A | verifica soddisfatta | closed |
| 5b | Team-A | verifica non soddisfatta | in-progress |

La questione rimane `pending-rfc` fino all'avvio effettivo del lavoro da parte
di Team-B. Ricevere la risposta non è sufficiente per passare a in-verification:
è necessario che il lavoro sia iniziato.

Il completamento del lavoro da parte di Team-B sblocca la verifica, ma non chiude
la questione. La responsabilità della verifica resta in capo a Team-A.

---

## RFC Inbound

| Passo | Chi | Azione |
|---|---|---|
| 1 | Team-B | riceve RFC da Team-A |
| 2 | Team-B | valuta RFC prima di aprire questioni |
| 3 | Team-B | apre le questioni necessarie |
| 4 | Team-B | segue il normale ciclo Hodos per ciascuna questione |
| 5 | Team-B | compila sezione Response RFC |
| 6 | Team-B | consegna Response a Team-A |
| 7 | Team-B | chiude le questioni aperte |

Il passo 7 (chiusura questioni) non può avvenire prima del passo 6 (consegna Response).
La chiusura è il completamento del ciclo RFC nella sua interezza, inclusa la restituzione.

---

## Regole

- La sezione di richiesta di una RFC è immutabile dopo la generazione. I contributi successivi avvengono solo tramite Response RFC e commenti.
- La RFC deve essere autocontenuta: Team-B non deve conoscere il progetto richiedente per capire cosa gli viene chiesto.
- I Criteri di Accettazione descrivono il punto di vista di Team-A, non le istruzioni realizzative per Team-B.
- La questione resta `pending-rfc` fino all'avvio effettivo del lavoro (semantica estesa: copre l'intero ciclo RFC).
- Le questioni inbound non possono essere chiuse prima che la Response RFC sia compilata, committata e consegnata.
