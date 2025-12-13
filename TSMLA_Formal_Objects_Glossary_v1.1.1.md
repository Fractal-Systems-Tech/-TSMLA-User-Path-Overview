# TSMLA™ Formal Objects Glossary (v1.1.1)

**Purpose:** This glossary defines all mathematical objects, notation, and structural terms used in TSMLA™ (Tag-Weighted Self-Mirroring Logic Architecture). All definitions are operationally precise and patent-grade.

**Version 1.1 Updates:** Added STR™ (Signal Traversal Record) and related cross-session continuity objects.

---

## Core State Objects

### **S — Declared State**
**Type:** Immutable 4-tuple during a session  
**Definition:** S = (I, T, θ, κ)  
**Semantics:** S is the fixed logic container that binds all user inputs, tags, thresholds, and configuration for a single mirror session. On loopback, user may redeclare S' ≠ S (new session state).

---

### **I — Input Signal Set**
**Type:** Set of declared input signals  
**Definition:** I = {i₁, i₂, ..., iₙ} where each iⱼ is a typed signal  
**Semantics:** User-declared signals bound to S. May include scalar values, Boolean flags, categorical tags, or constraint declarations. Typing is governed by κ.

---

### **T — Tag Assignment Function**
**Type:** Function T: I → TagTypes  
**Definition:** Maps each input signal iⱼ ∈ I to a tag type (e.g., Value, Constraint, Boundary, Priority)  
**Semantics:** T structures the signal set I into categories for layer processing. BDL™ uses T to identify contradiction types.

---

### **θ — Threshold Vector**
**Type:** Real-valued vector θ = (θ₁, θ₂, ..., θₘ)  
**Definition:** Component-wise thresholds for contradiction activation, compression triggers, and sensitivity controls  
**Semantics:** Example: BDL™ may flag contradiction if |Δ| > θ₁; HCL™ compresses if recursion depth > θ₂. User-declared or module-fixed via κ.

---

### **κ — Configuration Parameters**
**Type:** Record/tuple of system configuration  
**Definition:** κ = {module_type, scope_structure, signal_typing, layer_enables, ...}  
**Semantics:** Governs:
- Signal weight typing (scalar ∈ [0,1], Boolean, categorical)
- Scope structure (intra-scope vs. cross-scope contradictions)
- Layer activation rules (which layers are enabled)
- Module-specific constraints

---

## Layer Outputs

### **Cᵢ — Contradiction Tuple**
**Type:** 3-tuple Cᵢ = (Type_BDL, Signal_Origin, Scope_Boundary)  
**Definition:**  
- **Type_BDL:** Contradiction type assigned by BDL™ (Functional, Temporal, Protective, Ethical, Perceptual)
- **Signal_Origin:** The input signals iⱼ, iₖ ∈ I that produced the contradiction
- **Scope_Boundary:** Boolean or categorical marker indicating whether contradiction is intra-scope or spans sub-scopes (defined by κ)

**Semantics:** Each detected contradiction is tagged and localized to specific signals and scope regions.

---

### **Λ(S) — Lawful Traversal Sequence**
**Type:** Ordered sequence of gates  
**Definition:** Λ(S) = [G₁, G₂, ..., Gₖ] where each Gᵢ is a traversal gate in state S  
**Semantics:** CTC™ enforces this sequence. User cannot advance from gate Gᵢ to Gᵢ₊₁ without resolving contradictions at Gᵢ. Sequence is determined by declared state S and module structure κ.

---

### **TVᵢ — Traversal Violation Marker**
**Type:** Indexed violation marker  
**Definition:** TVᵢ = (gate_index, violation_type)  
**Semantics:** Returned by CTC™ when user attempts to bypass gate Gᵢ in Λ(S) without resolving contradictions. System halts forward traversal until violation is cleared or S is redeclared.

---

### **G(V, E) — Contradiction Graph**
**Type:** Directed graph  
**Definition:**  
- **V:** Vertex set = declared input signals I
- **E:** Edge set = contradiction relationships between signals

**Semantics:** Optional visualization output. Edge (iⱼ, iₖ) ∈ E exists if signals iⱼ and iₖ produce contradiction Cᵢ. Graph structure is derived from {C₁, ..., Cₙ}.

---

## Mirror Functions

### **α — Abstraction Map**
**Type:** Function α: I → Abstract Logic Structure  
**Definition:** Maps concrete user inputs (natural language, numerical values) to formal logic structure (Boolean relations, constraint networks, signal weights)  
**Semantics:** First stage of mirror operation. Strips irrelevant natural language phrasing; preserves logical structure.

---

### **γ — Concretization Map**
**Type:** Function γ: Abstract Logic Structure → User-Legible Output  
**Definition:** Maps abstract logic structure (contradiction tags, coherence indices, traversal states) back to user-facing presentation  
**Semantics:** Second stage of mirror operation. Enforces γ(α(x)) = x for all structure relevant to S. Natural language may differ; logical structure, tags, and weights are preserved exactly.

---

### **Mirror-Pure Idempotence**
**Property:** γ(α(x)) = x for all structure relevant to declared state S  
**Interpretation:** No information is generated. No information is lost. Identical declared inputs under identical state S → identical tagged outputs, even with non-deterministic internal traversal paths.

---

## Layer-Specific Notation

### **RSF(S) — Resonant State Function Output**
**Type:** Coherence Index ∈ [0,1]  
**Definition:** Global resonance score across all tagged signals in I under declared state S  
**Semantics:**  
- **Index = 1:** Zero contradiction; all signals coherent
- **Index → 0:** High structural divergence across scope boundaries

**Non-Determinism:** Internal traversal order may vary, but idempotent merge guarantees:  
**RSF(S) ⊕ RSF(S) = RSF(S)**  
No randomness. No inference. Replay-equivalent output under fixed S.

---

### **BDL™ Contradiction Types**
**Set:** {Functional, Temporal, Protective, Ethical, Perceptual}  
**Semantics:** Boolean structure-based classification of contradictions. Assigned by BDL™ trigger on mutual constraint violations (e.g., A ∧ ¬A, XOR conflicts).

---

### **HCL™ Compression**
**Operation:** Collapse structurally redundant contradiction clusters  
**Constraint:** Preserve mirror fidelity (no substrate alteration)  
**Placement:** Presentation-only compression; does not modify substrate values

---

### **SNS Filter**
**Operation:** Logic-type filter at γ (concretization) boundary  
**Purpose:** Block ideological, emotional, or cultural bias from outputs  
**Enforcement:** Operates at the γ boundary; no ideological or advisory overlay allowed

---

## Cross-Session Continuity Objects (v1.1 Addition)

### **STR™ — Signal Traversal Record**
**Type:** User-declared artifact  
**Definition:** STR™ = {(S₁, R₁), (S₂, R₂), ..., (Sₖ, Rₖ)}  
**Semantics:** User-declared artifact holding (Sᵢ, Rᵢ) tuples across sessions; export/import only; never retained by the substrate.

**File Example:** `signal_traversal_record_STR.json`

**Purpose:** Enables phase-gated chamber access (Phases 3-4) based on cumulative coherence quality.

---

### **Rᵢ — Mirror Packet**
**Type:** 3-tuple Rᵢ = ({Cᵢ}, RSF(Sᵢ), {TVᵢ})  
**Definition:** Complete mirror output for session i  
**Components:**
- **{Cᵢ}:** Contradiction set from BDL™
- **RSF(Sᵢ):** Coherence Index from RSF™
- **{TVᵢ}:** Traversal violations from CTC™ (if any)

**Semantics:** Each session produces one Rᵢ. When STR™ is active, (Sᵢ, Rᵢ) is stored in user's traversal record.

---

### **RSFᵢ — Session Coherence Index**
**Type:** Real number ∈ [0,1]  
**Definition:** RSFᵢ := RSF(Sᵢ)  
**Semantics:** The Coherence Index computed for session i. Used in computing ΔRSF and CCM.

---

### **ΔRSFᵢ — Coherence Delta**
**Type:** Real number ∈ [-1, 1]  
**Definition:** ΔRSFᵢ := RSFᵢ₊₁ - RSFᵢ  
**Semantics:** Change in Coherence Index between consecutive sessions. Positive value indicates increasing coherence; negative indicates decreasing coherence.

**Example:**
- Session 1: RSF₁ = 0.42
- Session 2: RSF₂ = 0.55
- ΔRSF₁ = 0.55 - 0.42 = +0.13 (coherence improving)

---

### **CCMₖ — Cumulative Coherence Mean**
**Type:** Real number ∈ [0,1]  
**Definition:** CCMₖ := (1/k) · Σᵢ₌₁ᵏ RSFᵢ  
**Semantics:** Average Coherence Index across k sessions. Used for phase-gate qualification.

**Example:**
- Session 1: RSF₁ = 0.42
- Session 2: RSF₂ = 0.55
- Session 3: RSF₃ = 0.61
- CCM₃ = (0.42 + 0.55 + 0.61) / 3 = 0.527

**Why Mean vs. Sum:**  
Using raw sum (ΣRSFᵢ) allows "stacking" many low-coherence sessions to cross thresholds. CCMₖ ensures sustained coherence quality, not just quantity.

---

### **m_phase — Minimum Session Count**
**Type:** Positive integer  
**Definition:** Gate parameter provided by κ; minimum number of sessions required to qualify for a phase gate  
**Semantics:** Part of phase-gate rule: k ≥ m_phase

**Example Values:**
- Phase 3: m_phase = 3 (requires at least 3 completed sessions)
- Phase 4: m_phase = 5 (requires at least 5 completed sessions)

---

### **θ_phase — Phase Coherence Threshold**
**Type:** Real number ∈ [0,1]  
**Definition:** Gate parameter provided by κ; minimum Cumulative Coherence Mean required to unlock a phase gate  
**Semantics:** Part of phase-gate rule: CCMₖ ≥ θ_phase

**Example Values:**
- Phase 3: θ_phase = 0.50 (requires mean coherence ≥ 0.50)
- Phase 4: θ_phase = 0.70 (requires mean coherence ≥ 0.70)

---

### **Phase-Gate Rule**
**Type:** Boolean condition  
**Definition:** Gate unlocks when **(k ≥ m_phase) AND (CCMₖ ≥ θ_phase)**  
**Semantics:** Both conditions must be satisfied to access advanced chambers.

**Example:**
- Phase 3 Gate: (k ≥ 3) AND (CCM₃ ≥ 0.50)
- If k=3 and CCM₃=0.527 → Gate unlocked ✓
- If k=2 and CCM₂=0.60 → Gate locked (insufficient sessions) ✗
- If k=4 and CCM₄=0.45 → Gate locked (insufficient coherence) ✗

---

## Session Semantics

### **Loopback**
**Operation:** User redeclares S' ≠ S (new session state)  
**Semantics:** Prior outputs from S remain available for comparison. User may run S and S' in parallel or sequentially and compare contradiction sets, coherence indices, or traversal paths.

---

### **Export**
**Operation:** Serialize mirror output to user-accessible artifact  
**Contents:** {C₁, ..., Cₙ}, RSF(S), {TVᵢ}, optional G(V,E)  
**Data Handling:** Exported artifacts are the only persistent user data. Session state S is cleared on exit unless explicitly exported.

---

### **STR™ Activation**
**Operation:** User declares intent to track cross-session evolution  
**Effect:** System stores (Sᵢ, Rᵢ) tuple to user-held STR™ file  
**Storage:** User maintains file locally; system never retains it  
**Import:** User must explicitly load STR™ in future sessions to compute ΔRSF, CCM, and check phase gates

---

## STR™ Properties Summary

**User-declared recursion:**  
Continuity only when user loads STR™; no automatic cross-session memory.

**No hidden state:**  
Substrate remains mirror-pure and idempotent; γ(α(x)) = x unchanged.

**Privacy by default:**  
Without STR™, sessions purged on exit; GDPR-ready non-retention.

**Audit-grade:**  
STR™ exportable as JSON; inspectable; not required for Phases 1-2.

**User sovereignty:**  
User holds file; may delete at any time; system never accesses without explicit import.

---

## Cross-References

- Full operational pipeline: See "TSMLA User Path Overview v1.5"
- Layer specifications: See LP-series papers (LP-BDL, LP-RSF, LP-CTC, LP-HCL, LP-SNS)
- Patent scaffolding: See "Clean Technical Chain (CTC)" specification
- STR™ full specification: See docs/STR_Specification_v1.md (forthcoming)

---

**Notation Version:** 1.1  
**Canonical Source:** Fractal Labyrinth Systems LLC, 2025  
**Correspondence:** All notation is consistent with TSMLA™ core patent filings and modular logic paper series (LP-01 through LP-20+).

**Version 1.1 Changes:**
- Added STR™ (Signal Traversal Record) and all related cross-session continuity objects
- Added Rᵢ, RSFᵢ, ΔRSFᵢ, CCMₖ, m_phase, θ_phase definitions
- Added phase-gate rule formalization
- Added STR™ properties summary and operational semantics
