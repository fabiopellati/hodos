---
tipo-artefatto: template
documento: commento
descrizione: struttura canonica di un commento in una questione o in una nota
fase: trasversale
autorita: operativa
---

# Template — Commento

Un commento è un'annotazione additiva che si aggiunge a una questione o a una
nota per rettificare, integrare o documentare un'evoluzione senza riscrivere il
corpo che la precede.

Il regime del suo testo è quello del contenitore. Nella nota il commento è
immutabile come il corpo che lo accoglie (Art. 5 comma 5). Nella questione
aperta il commento appartiene al corpo e ne segue il regime ordinario, sicché il
suo difetto di redazione si corregge nel testo del commento (Art. 4 comma 9).

Il commento nasce per i contenitori il cui corpo non si tocca: la nota e tutto
ciò che è entrato nel ciclo chiuso. Su una questione ancora aperta il corpo è
invece modificabile, quindi il commento non è l'unica via disponibile e non è
sempre la migliore: vedi le sezioni seguenti.

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
questione è aperta, con l'approvazione dell'operatore (Art. 4 comma 8, lettera d).

Riassorbire significa portare nel corpo il contenuto valido e togliere
l'annotazione diventata superflua. È un atto diverso dalla correzione di un
commento, descritta nella sezione seguente, che ne ripara il testo lasciandolo
dov'è.

La ragione è la stessa che governa il consolidamento del corpo, ed è stabilita
dall'Art. 4 comma 8: una questione che alterna un'affermazione e la sua
successiva smentita è faticosa da leggere per una persona e induce in errore chi
la consulti per frammenti, perché nulla garantisce che l'affermazione e la sua
negazione vengano recuperate insieme. Vale anche qui il limite: riassorbire non
vuol dire abbreviare, e il contenuto valido va portato nel corpo per intero.

## Correggere un commento

Su una questione aperta, quando l'operatore chiede di correggere un commento
già scritto, si corregge il testo di quel commento: non si aggiunge un commento
di rettifica, che lascerebbe agli atti il refuso accanto alla sua correzione
(Art. 4 comma 9).

La correzione ripara come il commento è scritto e non cambia ciò che
testimonia: data, autore e contenuto dell'interazione registrata restano quelli
che erano. Se invece il commento registrava qualcosa che l'opera ha davvero
creduto e poi ha appreso diversamente, la traccia si conserva e la rettifica è
un commento nuovo; nel dubbio decide l'operatore (Art. 4 comma 8, lettere a e b).

Nella nota il commento non si corregge in luogo: ogni rettifica è un commento
nuovo che riferisce il precedente (Art. 5 comma 5).

## Prima di scrivere

Non scrivere il commento senza conferma dell'operatore. Proponi il contenuto
e il contenitore di destinazione (quale questione o nota) e attendi
approvazione esplicita.

## Regole

- La numerazione (COMMENTO-NNN) è locale al contenitore (questione o nota).
- Il primo commento è COMMENTO-001. Leggere i commenti esistenti per determinare il prossimo numero.
- Il testo del commento segue il regime del contenitore: nella questione aperta si corregge in luogo (Art. 4 comma 9), nella nota è immutabile (Art. 5 comma 5).
- Il commento è additivo: si aggiunge in fondo alla sezione Commenti.
- Su una questione aperta, quando il commento sarebbe una pura rettifica redazionale del corpo, si consolida il corpo invece di commentare; un commento redazionale già presente può essere riassorbito nel corpo e rimosso, con l'approvazione dell'operatore. I commenti che registrano un'interazione datata non si riassorbono (Art. 4 comma 8).
- La sezione **Commenti** si trova in fondo al contenitore, prima del separatore `---` finale. Se non esiste, crearla in quella posizione.
- In una questione, la sezione Commenti segue tutti i campi strutturati (Descrizione, Domande aperte, Impatto). Il legame con altre questioni non è più una sezione del corpo: vive nel campo `related` del frontmatter.
- Il difetto di redazione di un commento di una questione aperta si corregge nel testo del commento, non con un commento di rettifica (Art. 4 comma 9).
- Per rettificare un commento di una nota, o un commento che registra ciò che l'opera ha davvero creduto, aggiungere un nuovo commento che lo riferisce esplicitamente (es. "Rettifica del COMMENTO-002").
