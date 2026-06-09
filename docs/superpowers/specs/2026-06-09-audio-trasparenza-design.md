# Audio → Trasparenza foto/video

## Obiettivo
La foto o il video caricato diventano progressivamente trasparenti in base all'intensità della voce captata dal microfono: più voce = più trasparenza.

## Mappa volume → visibilità
- Silenzio (energia ~0) → visibile 100%
- Voce normale (energia ~0.33) → visibile 75%
- Voce alta (energia ~0.66) → visibile 50%
- Urlo (energia ~1.0) → visibile 25%

Formula: `opacità = 1.0 - (energia × 0.75)`, con transizione fluida.

## Implementazione
- Metodo: CSS `opacity` sul `#photo-canvas`
- `transition: opacity 0.15s ease` per smoothness
- Una riga nel loop `draw()`: `photoCanvas.style.opacity = 1 - energy * 0.75`
- Nessuna nuova libreria o file

## File modificato
Solo `1-POSTER.html`:
1. Aggiungere `transition: opacity 0.15s ease` allo stile `#photo-canvas`
2. Aggiungere `photoCanvas.style.opacity = 1 - Math.min(1, energy * 1.2) * 0.75;` nel loop `draw()`
