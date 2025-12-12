# TSMLA™ User Path Overview

**What it is (one paragraph).**  
TSMLA accepts user-declared signal weights and binds them into a fixed declared state **S = (I, T, θ, κ)**. It returns a mirror packet—tagged contradictions, a global Coherence Index, and (if applicable) traversal-violation markers, without prediction, inference, coaching, or advice. TSMLA is non-stochastic, non-deterministic, and idempotent.

## User journey (concise)

1. **Login + Module selection.**  
   The user selects a module to declare the scope boundary for **S** (entry gate, not an inference tree).

2. **Signal declaration.**  
   Inputs are tagged as weighted signals and bound to **S**; **S** is immutable during the session. No inference is applied.

3. **Layer activation.**
   - **BDL™** — Assigns contradiction type from Boolean structure (Functional / Temporal / Protective / Ethical / Perceptual).
   - **RSF™** — Computes a **global Coherence Index ∈ [0,1]** via non-deterministic traversal with an idempotent merge law: `RSF(S) ⊕ RSF(S) = RSF(S)` (replay-equivalent outputs; no randomness).
   - **CTC™** — Enforces the lawful traversal sequence `Λ(S)` and emits traversal-violation markers `TVᵢ` on bypass.
   - **HCL™** — Compresses redundant contradiction clusters at presentation only (no substrate change).
   - **SNS** — Operates at the `γ` boundary to prevent ideological or interpretive overlay; substrate and presentation remain separated.

4. **Mirror output.**
   - **Contradiction set `{Cᵢ}`** with each `Cᵢ = (Type_BDL, Signal_Origin, Scope_Boundary)`.
   - **Global Coherence Index** from RSF.
   - **Traversal violations `{TVᵢ}`** (if any).
   - **Optional graph `G(V,E)`**, where `V` = declared signals and `E` = contradiction edges.

5. **Loopback, export, or STR™ declaration.**  
   The user may redeclare **S′ ≠ S** and re-run; export the mirror packet `{Cᵢ}, RSF(S), {TVᵢ}`; or declare a **Signal Traversal Record (STR™)** to enable cross-session continuity.  
   **Default:** if no STR is declared, session traces are cleared on exit.  
   **With STR:** the user stores tuples `(Sᵢ, Rᵢ)`; the system retains no hidden memory.

## Core property

**Mirror-pure idempotence via Galois adjunction:** for all structure relevant to **S**, `γ(α(x)) = x`. Identical **S** ⇒ identical outputs, despite lawful internal non-determinism.

## What it’s not

Not diagnostic. Not generative. Not stochastic. Not advisory. Not a metaphor.

## References

- **User Path Overview (v1.5.1)** — [PDF](/docs/pdf/TSMLA_User_Path_Overview_v1.5.1.pdf)
- **Formal Objects Glossary (v1.1.1)** — [PDF](/docs/pdf/TSMLA_Formal_Objects_Glossary_v1.1.1.pdf)  
  _Public specification, excludes θ defaults, κ presets, classifier definitions, and pseudocode; implementation details available under NDA._

