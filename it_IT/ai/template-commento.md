---
tipo-artefatto: template
documento: commento
descrizione: struttura canonica di un commento in una questione o in una nota
fase: trasversale
autorita: operativa
---

# Template — Commento

Un commento è un'annotazione additiva e immutabile che si aggiunge a una
questione o a una nota per rettificare, integrare o documentare un'evoluzione
senza modificare il corpo originale.

Il commento nasce per i contenitori il cui corpo non si tocca: la nota, il cui
corpo è immutabile per l'Art. 5 comma 5, e tutto ciò che è entrato nel ciclo
chiuso. Su una questione ancora aperta il corpo è invece modificabile, quindi il
commento non è l'unica via disponibile e non è sempre la migliore: vedi la
sezione seguente.

## Struttura

```markdown
**Commenti**

COMMENTO-{NNN} — {YYYY-MM-DD}
{testo del commento}
```

## Il commento su una questione aperta

Su una questione aperta il commento va riservato a ciò che ha una data e un
autore che contano, cioè a un'**interazione realmente avvenuta**: una risposta
ricevuta da un interlocutore, una decisione presa dall'operatore, un fatto
accaduto in un momento preciso. Questi commenti restano dove sono: registrano
qualcosa che è successo, e la loro collocazione nel tempo è parte
dell'informazione.

Quando invece il commento sarebbe una **pura rettifica redazionale** del corpo —
correggere un passaggio sbagliato, precisare una formulazione ambigua, smentire
una deduzione che non era corretta nemmeno quando fu scritta — la strada giusta
è consolidare il corpo della questione, non aggiungere un commento. Un commento
di questo tipo già presente può essere riassorbito nel corpo e rimosso finché la
questione è aperta, con l'approvazione dell'operatore.

Questo non intacca l'immutabilità del commento, che riguarda il suo testo: un
commento non si riscrive mai in luogo. Riassorbire significa portare nel corpo il
contenuto valido e togliere l'annotazione diventata superflua, non riformularla
sul posto.

La ragione è la stessa che governa il consolidamento del corpo, ed è spiegata
nel template `questione`: una questione che alterna un'affermazione e la sua
successiva smentita è faticosa da leggere per una persona e induce in errore chi
la consulti per frammenti, perché nulla garantisce che l'affermazione e la sua
negazione vengano recuperate insieme. Vale anche qui il limite: riassorbire non
vuol dire abbreviare, e il contenuto valido va portato nel corpo per intero.

## Prima di scrivere

Non scrivere il commento senza conferma dell'operatore. Proponi il contenuto
e il contenitore di destinazione (quale questione o nota) e attendi
approvazione esplicita.

## Regole

- La numerazione (COMMENTO-NNN) è locale al contenitore (questione o nota).
- Il primo commento è COMMENTO-001. Leggere i commenti esistenti per determinare il prossimo numero.
- Il commento è immutabile dopo la scrittura: il suo testo non si riscrive mai in luogo.
- Il commento è additivo: si aggiunge in fondo alla sezione Commenti.
- Su una questione aperta, quando il commento sarebbe una pura rettifica redazionale del corpo, si consolida il corpo invece di commentare; un commento redazionale già presente può essere riassorbito nel corpo e rimosso, con l'approvazione dell'operatore. I commenti che registrano un'interazione datata non si riassorbono.
- La sezione **Commenti** si trova in fondo al contenitore, prima del separatore `---` finale. Se non esiste, crearla in quella posizione.
- In una questione, la sezione Commenti segue tutti i campi strutturati (Descrizione, Domande aperte, Impatto). Il legame con altre questioni non è più una sezione del corpo: vive nel campo `related` del frontmatter.
- Per rettificare un commento precedente, aggiungere un nuovo commento che lo riferisce esplicitamente (es. "Rettifica del COMMENTO-002").
