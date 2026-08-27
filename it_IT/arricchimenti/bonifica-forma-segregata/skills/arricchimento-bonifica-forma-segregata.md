---
tipo-artefatto: skill
documento: arricchimento-bonifica-forma-segregata
descrizione: processo operativo con cui un'opera avviata sulla forma monolitica migra alla
  forma segregata degli strumenti di governo
skill: arricchimento-bonifica-forma-segregata
client: Claude Code CLI
invocazione: /hodos-arricchimento-bonifica-forma-segregata
tipo: operativo
locale: it_IT
---

# Skill — Bonifica verso la forma segregata

Questo skill descrive il processo operativo con cui un'opera Hodos avviata
sulla forma monolitica migra alla forma segregata introdotta dalla versione
1.0.0 del protocollo. È un processo che si esegue una volta sola per opera.

Prima di operare, l'agente deve aver recuperato i template della forma
segregata (`questioni-file`, `mastro-file`, `notes-file`, `questione`,
`mastro-entry`, `nota`) con `get_template`, per conoscere la forma di
destinazione esatta.

---

## Precondizioni

- L'opera possiede un corpus di processo nella forma monolitica: `questioni.md`,
  `mastro.md` e `note.md` (o `notes.md`) come file accumulanti.
- L'opera adotta la versione 1.0.0 o successiva del protocollo.
- Il working tree è pulito: la bonifica va eseguita in un commit isolato, senza
  altre modifiche pendenti che si mescolino al diff di riformattazione.

---

## Primo strato — split deterministico

Questo strato è meccanico e non introduce giudizio. Per ciascuno dei tre
strumenti monolitici:

1. Crea la cartella di collezione corrispondente (`questioni/`, `mastro/`,
   `note/`) se non esiste.

2. Separa il monolite nei singoli elementi individuando i confini di ciascun
   blocco (per le questioni e le voci del mastro l'intestazione `## `; per le
   note l'intestazione `## NOTA-...`).

3. Per ogni elemento crea un file con nome parlante:
   - `questioni/Q{NNN}-slug.md` per una questione aperta;
   - `mastro/Q{NNN}-slug.md` per una voce del mastro;
   - `note/NOTA-{NNN}-slug.md` per una nota.
   Lo `slug` è un kebab-case derivato dal titolo.

4. Trasferisci il **corpo verbatim**: il testo dell'elemento va copiato senza
   alcuna riscrittura. Per il mastro questo è vincolante, perché il corpo è
   immutabile e ne va preservata l'esatta forma storica.

5. Anteponi un **frontmatter minimo**, popolando solo i campi ricavabili
   meccanicamente dal contenuto e dalla posizione:
   - `id`, `titolo`, `tipo-elemento`;
   - per le questioni: `tipo`, `stato`, `aperta` (e `aggiornata` se ricavabile
     dalla storia);
   - per le voci del mastro: `tipo`, `stato: closed`, `chiusa` (dalla data di
     chiusura in intestazione);
   - per le note: `data`.
   I campi di giudizio (`decisioni`, `related`, `tag`, `file-toccati`) si
   lasciano vuoti o assenti in questo strato: verranno compilati nel secondo.

6. Rigenera gli indici `questioni.md`, `mastro.md` e `note.md` come proiezione
   dei frontmatter appena creati, includendo il marcatore di file generato.

Al termine di questo strato l'opera è già nella forma segregata e conforme
alla struttura; manca solo la ricchezza dei metadati di giudizio.

---

## Secondo strato — arricchimento progressivo

Questo strato richiede lettura e interpretazione, può avvenire in tempi
successivi e non blocca il primo. Per ciascun elemento, letto il corpo:

- compila `decisioni` distillando le decisioni prese (per le voci del mastro,
  dalla sezione `Decisioni prese`);
- compila `file-toccati` dagli artefatti citati nella sezione `Impatto`;
- compila `related` traducendo in lista di identificativi i legami che nel
  corpo erano scritti in prosa o nella vecchia sezione `Questioni collegate`;
- compila `tag` con i temi ricorrenti dell'elemento.

Trattandosi del mastro, l'arricchimento avviene sul **frontmatter**, che è
mutabile, mentre il corpo resta intatto: è esattamente il doppio regime
previsto dal protocollo.

---

## Invarianti di non-regressione

La bonifica non deve perdere né alterare contenuto. Prima di considerare
conclusa la migrazione, verifica che:

- il corpo di ogni elemento segregato coincida verbatim con il testo che aveva
  nel monolite, in particolare per il mastro;
- nessun elemento sia andato perso: il numero di elementi segregati eguaglia il
  numero di blocchi del monolite di partenza;
- ogni indice sia una proiezione fedele dei frontmatter e non contenga voci
  orfane o mancanti;
- i frontmatter siano coerenti con il corpo (il validatore dell'opera, se
  presente, non segnala discrepanze).

---

## Tooling

Lo split deterministico, la generazione degli indici e la validazione dei
frontmatter sono lavoro ripetitivo e a regola fissa: vanno automatizzati con
uno strumento dell'opera. L'arricchimento **promuove** questo strumento ma non
ne prescrive lo stack: Python o TypeScript sono le scelte tipiche, ma la
decisione spetta al progetto in base alla propria toolchain. Il protocollo
prescrive la forma e le invarianti, non l'implementazione.

Quando lo strumento non è ancora disponibile, il primo strato può essere
eseguito manualmente su un corpus piccolo; per corpus grandi l'automazione è di
fatto necessaria, ed è preferibile realizzarla prima di iniziare la migrazione.

---

## Commit isolato

La riformattazione di massa tocca l'intero corpus di processo e va eseguita in
un commit dedicato, che non contiene alcun'altra modifica sostanziale. Mescolare
la migrazione al lavoro di merito nasconderebbe il diff reale di quest'ultimo
dietro lo spostamento di righe della riformattazione. Il secondo strato, se
svolto in tempi successivi, produce i propri commit distinti.
