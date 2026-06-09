# Audio → Trasparenza foto/video Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Far sì che foto e video diventino più trasparenti al crescere del volume del microfono.

**Architecture:** Una riga di CSS per la transizione fluida + una riga JS nel loop `draw()` che imposta `opacity` sul canvas della foto in base all'energia audio.

**Tech Stack:** HTML/CSS/JS, tutto già presente nel progetto.

---

### Task 1: Aggiungere transizione CSS e logica opacità

**Files:**
- Modify: `1-POSTER.html` (stile `#photo-canvas` + loop `draw()`)

- [ ] **Step 1: Aggiungere `transition` al CSS di `#photo-canvas`**

Nel blocco stile esistente per `#photo-canvas`, aggiungere la proprietà `transition` per rendere fluido il cambio di opacità:

```css
#photo-canvas {
  position: fixed;
  inset: 0;
  z-index: 1;
  width: 100%;
  height: 100%;
  image-rendering: pixelated;
  pointer-events: none;
  mix-blend-mode: multiply;
  transition: opacity 0.15s ease;
}
```

- [ ] **Step 2: Aggiungere la riga che collega volume → opacità nel loop `draw()`**

Dentro la funzione `draw()`, dopo `const energy = getAudioEnergy();` (riga ~459), aggiungere:

```js
  photoCanvas.style.opacity = 1 - Math.min(1, energy * 1.2) * 0.75;
```

`Math.min(1, energy * 1.2)` amplifica leggermente l'energia per arrivare a opacità 0.25 anche con voci non fortissime.

- [ ] **Step 3: Verifica**
Aprire `1-POSTER.html` nel browser, caricare una foto, parlare nel microfono — la foto diventa più trasparente con la voce e torna visibile in silenzio.

- [ ] **Step 4: Commit**

```bash
git add 1-POSTER.html
git commit -m "feat: audio-reactive transparency on photo/video"
```
