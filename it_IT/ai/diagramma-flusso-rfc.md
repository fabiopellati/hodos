---
tipo-artefatto: guida
documento: diagramma-flusso-rfc
descrizione: flusso RFC outbound, inbound e informativa — tipi, cicli e regole operative
autorita: informativa
---

# Flusso RFC

Riferimento visivo: `../diagrams/flusso-rfc.puml`

Una RFC viene emessa quando una questione richiede intervento nell'ambito di
competenza di un attore esterno. È autocontenuta: leggibile senza conoscere
la storia interna dell'opera richiedente.

Esistono tre tipi di RFC, distinti per direzione e attesa di risposta:

- RFC Outbound — bidirezionale: Team-A emette, Team-B risponde.
- RFC Inbound — bidirezionale: Team-B riceve, compila la risposta e
  restituisce.
- RFC Informativa — unidirezionale: comunicazione senza attesa di
  risposta.

---

## RFC Outbound

1. Team-A — questione richiede intervento esterno (`in-progress`)
2. Team-A — genera RFC e consegna a Team-B (`pending-rfc`)
3. Team-B — compila Response RFC e restituisce (`pending-rfc`)
4. Team-A — avvia verifica (`in-verification`)
5. Team-A — esito verifica:
   - soddisfatta → `closed`
   - non soddisfatta → `in-progress`

La questione rimane `pending-rfc` fino all'avvio effettivo del lavoro da parte
di Team-B. Ricevere la risposta non è sufficiente per passare a in-verification:
è necessario che il lavoro sia iniziato.

Il completamento del lavoro da parte di Team-B sblocca la verifica, ma non chiude
la questione. La responsabilità della verifica resta in capo a Team-A.

---

## RFC Inbound

1. Team-B — riceve RFC da Team-A
2. Team-B — valuta RFC prima di aprire questioni
3. Team-B — apre le questioni necessarie
4. Team-B — segue il normale ciclo Hodos per ciascuna questione
5. Team-B — compila sezione Response RFC
6. Team-B — consegna Response a Team-A
7. Team-B — chiude le questioni aperte

Il passo 7 (chiusura questioni) non può avvenire prima del passo 6 (consegna Response).
La chiusura è il completamento del ciclo RFC nella sua interezza, inclusa la restituzione.

---

## RFC Informativa

1. Team-A — decide di emettere una comunicazione unidirezionale verso
   un attore esterno, senza richiedere risposta.
2. Team-A — genera la RFC con `Tipo: informativa` nell'intestazione e
   la consegna all'attore esterno.
3. La questione di origine **non transita** a `pending-rfc`: il suo
   ciclo prosegue indipendentemente dall'invio.

La RFC Informativa non ha sezione Response RFC e non genera attesa.
Non è previsto un ciclo di verifica: l'atto di consegna chiude
il coordinamento esterno.

---

## Regole

- La sezione di richiesta di una RFC è immutabile dopo la generazione. I contributi successivi avvengono solo tramite Response RFC e commenti.
- La RFC deve essere autocontenuta: Team-B non deve conoscere il progetto richiedente per capire cosa gli viene chiesto.
- I Criteri di Accettazione descrivono il punto di vista di Team-A, non le istruzioni realizzative per Team-B.
- La questione resta `pending-rfc` fino all'avvio effettivo del lavoro (semantica estesa: copre l'intero ciclo RFC).
- Le questioni inbound non possono essere chiuse prima che la Response RFC sia compilata, committata e consegnata.
