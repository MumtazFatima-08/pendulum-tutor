# chaos-honest-ai

**Rebuild the Classroom Hackathon — Round 1 Submission**

A double pendulum, shown three ways at once — real physics, a data-only neural predictor, and a physics-informed neural predictor (PINN) — so a student can *watch* chaos and AI-hallucination happen instead of reading about them. An adaptive tutor (real Claude API call, not scripted text) watches what the student explores and responds to their specific actions.

## Run it

No build step, no install. Either:

- **Open directly:** download `index.html` and open it in any modern browser, or
- **Live link:** https://mumtazfatima-08.github.io/pendulum-tutor/

**To use the adaptive tutor:** paste a free Gemini API key into the field above the tutor panel — get one at [aistudio.google.com/apikey](https://aistudio.google.com/apikey) (Google account only, no credit card, no payment ever required for the free tier). The key is used only in your browser for that session — never stored, never sent anywhere but Google's API. The pendulum simulation itself works with no key at all; the key is only needed for the live "Ask the tutor" responses.

## What it does

- **Ground truth panel:** real double-pendulum physics, integrated with RK4.
- **Naive net panel:** a stand-in for a model trained only on motion data — drifts into physically impossible states (energy climbs) the longer it runs.
- **Physics-informed panel:** the same predictor, but corrected to respect energy conservation at every step — stays physically honest even under uncertainty.
- Student sets the starting angle and a nudge as small as 0.1°, and watches how fast the three diverge — chaos theory, observed rather than described.
- **Adaptive tutor:** logs every interaction (angle changes, nudge size, run/pause, how far the energy drift got). On request, that log is sent to Claude, which responds with a specific observation about *this* student's exploration and one concrete next thing to try — not a generic explanation.

## Why this subject

Chaos theory and AI reliability are usually taught in separate units, both as abstractions. This demo makes both visible on one system: nudge sensitivity, and why unconstrained AI predictions can't be trusted the same way physics-constrained ones can.

## Known limitations (see submission note for full detail)

- The naive-vs-PINN comparison uses a hand-tuned drift/correction function as a stand-in for a fully trained model — the effect is real and correctly modeled, not a trained network yet.
- The tutor has no memory across sessions.

## Stack

Vanilla HTML/CSS/JS, canvas rendering, RK4 physics integration, Google Gemini API (`gemini-2.5-flash`, free tier) for the adaptive tutor. No backend, no dependencies.

## Files

- `index.html` — the whole prototype
- `submission_note.md` — round 1 written note
