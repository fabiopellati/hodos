---
tipo-artefatto: template
documento: mastro-file
descrizione: struttura canonica del file mastro.md vuoto per un'opera Hodos
fase: trasversale
autorita: operativa
---

# Template — File mastro.md

Il file `mastro.md` è il registro immutabile delle decisioni prese nell'opera.
Viene creato durante l'inizializzazione e vive nella directory di processo.
Le entry vengono aggiunte in cima (prepend-only) e non vengono mai modificate.

## Struttura

```markdown
# Mastro — {Nome Opera}

---
```

## Regole

- Il mastro è prepend-only: ogni nuova entry va inserita in cima, dopo il titolo e prima del primo separatore `---`.
- Le entry sono immutabili: non modificarle mai dopo la scrittura.
- Per la struttura di una singola entry, consultare il template `mastro-entry`.
