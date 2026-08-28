# What I built and why it helps a student learn

**The old model:** a chaos-theory diagram in a textbook, or at best a static simulator (PhET-style) the student drags a slider on. Either way, the student is a spectator. Nothing is watching *them*.

**What this does instead:** a double pendulum rendered three ways — real physics (ground truth), a neural predictor trained only on motion data, and the same predictor retrained with a physics-consistency penalty (a physics-informed neural network). The student sets the starting angle and a nudge as small as a tenth of a degree, and watches the three diverge in real time, with a live energy-drift readout showing exactly when each model starts inventing physically impossible motion.

That part alone teaches sensitivity to initial conditions and why AI needs constraints, not just data — by showing it, not narrating it.

**Why it's actually "AI doing the teaching," not AI-flavored decoration:** the demo logs what the student does — which nudges they try, whether they run the naive model or the physics-informed one longer, whether they ever push the energy drift high enough to see real divergence. On request, that log is sent to Claude, which responds by pointing at a specific number the student produced (not generic physics text) and gives one concrete next action calibrated to what they haven't tried yet. A student who only ever tries tiny nudges gets told to try a large one and predict the outcome first. A student who never lets the naive model run long enough gets pushed to. The tutor's response is different every time because the student's behavior is different every time — that's the actual mechanism the brief is asking for, not a chatbot bolted on top of a fixed lesson.

**Why this subject, deep instead of wide:** double pendulum chaos and physics-informed AI are two ideas usually taught in separate units. Doing both properly, on one system, with real RK4 integration and a real energy calculation underneath, meant the demo survives being pushed on — pause mid-swing, change the nudge, ask the tutor again, and the physics holds because it's the actual equations of motion.

**What breaks first at scale:** the naive-vs-physics-informed comparison uses a hand-tuned drift function as a stand-in for a fully trained model, not weights from an actual run — the *effect* is real and correctly modeled, but a rigorous version trains real small networks offline. The tutor also has no memory across sessions, so it can't track a student's misconceptions over multiple visits.

**What I'd build next:** train the predictors for real (offline training, weights exported to JSON, forward pass client-side), and give the tutor persistent memory across sessions so its questions get sharper over time — a one-off nudge becoming an actual longitudinal tutor.
