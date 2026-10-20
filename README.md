# ANIRBAN-1: IoT Mesh for Autonomous Aircraft Safety

Integrated Technical Concept Report — Cooperative Trajectory Sharing, Conflict Prediction, and Advisory-Layer Engineering.

[📄 Download the ANIRBAN-1 Technical Concept Report (PDF)](docs/ANIRBAN-1-Integrated-Technical-Concept-Report.pdf)

**Contributors:** Abu Kayes Huda, Jaidul Islam Alvi, MD Sakib Hasan

**Report Date:** 15 October 2026  
**Revision:** 1.0  
**Document Type:** Concept / Research Architecture  
**System Boundary:** Advisory-only, simulation-first

---

## Status: Research Concept — Not for Operational Use

ANIRBAN-1 is a research architecture and concept report.

It is not an installation manual, a certified design, an operational flight procedure, or evidence of compliance with any standard named in the report.

ANIRBAN-1 does not command flight controls and does not replace, disable, suppress, or contradict existing aviation safety systems, including TCAS/ACAS, ADS-B, ATC, or established operating procedures.

Any real-aircraft modification must be independently designed and approved by qualified aviation specialists and the responsible authority.

---

## Project Overview

ANIRBAN-1 proposes a **cooperative, advisory-only aircraft safety overlay**.

The concept explores whether participating aircraft can exchange state and planned-trajectory intent, predict potential conflicts over a declared horizon, evaluate candidate resolutions against explicit constraints, and present an explainable recommendation to a pilot or operator.

Existing collision-avoidance and air-traffic functions remain independent and unmodified throughout the Version 0.1 concept.

The report defines the research problem as **fault-aware peer coordination under uncertainty, disagreement, stale information, missing messages, and network partition conditions**.

The current research status is:

> **Unproven but testable.**

The concept has not yet demonstrated a measurable safety improvement.

---

# 1. Document Status and Scope

This repository represents Revision 1.0 of the ANIRBAN-1 integrated technical concept report.

The report consolidates the technical substance of the supplied concept material and its accompanying research-and-technology comparison into a single research architecture.

The report deliberately maintains an engineering boundary around Version 0.1:

- Simulation-first
- Advisory-only
- No flight-control commands
- No replacement of existing aviation safety systems
- No certification claim
- No demonstrated safety improvement claim

The report also records corrections and revisions made to the original concept, including removal or postponement of unsupported assumptions and unverified numerical claims.

---

# 2. Executive Summary

ANIRBAN-1 proposes a cooperative, advisory-only aircraft safety overlay.

Participating aircraft would:

1. Exchange aircraft state and planned-trajectory intent.
2. Predict potential conflicts over a declared prediction horizon.
3. Evaluate candidate resolutions against explicit constraints.
4. Apply independent safety monitoring.
5. Account for uncertainty, stale information, disagreement, loss, and network partition.
6. Present advisory information to a pilot or operator.
7. Keep existing collision-avoidance and air-traffic functions independent.

The research question is not whether existing aviation safety systems should be replaced.

Instead, the research question is whether a carefully engineered, fault-aware cooperative trajectory-sharing and conflict-prediction layer can demonstrate measurable benefits beyond existing aviation surveillance, collision avoidance, and trajectory-management approaches.

Any claimed benefit must be:

- Defined using pre-declared metrics.
- Measured against named baselines.
- Attributed using ablation experiments.
- Demonstrated through staged validation.

---

# 3. Introduction, Motivation, Problem Statement, and Research Question

## 3.1 Motivation

The concept is motivated by the potential value of peer-to-peer exchange of aircraft intent in addition to existing surveillance and collision-avoidance functions.

The report distinguishes between:

- Current aircraft state.
- Planned future intent.
- Conflict prediction.
- Candidate advisory resolution.
- Existing operational safety functions.

The proposed contribution is therefore not simply another collision-avoidance algorithm.

It focuses on whether aircraft can share intent and coordinate under fault, uncertainty, and disagreement without making their existing safety functions dependent on the cooperative layer.

## 3.2 Existing Collision Avoidance

ANIRBAN-1 is explicitly positioned as complementary to existing aviation systems.

The report does not characterize TCAS/ACAS as obsolete or replaceable.

Existing collision-avoidance functions remain independent and must not be contradicted by the advisory layer.

## 3.3 Related Technology

The report considers related work and technology including:

- ACAS / TCAS
- ADS-B
- DAIDALUS
- Trajectory-Based Operations
- Four-dimensional trajectory conflict detection and resolution
- Air-to-air ad hoc networking
- Cooperative surveillance
- Non-cooperative sensing
- Human-factors research
- Aviation cybersecurity

These technologies provide baselines, context, or related evidence rather than proof of ANIRBAN-1 performance.

## 3.4 Problem Statement

The central problem is:

> What happens when a peer's intent message is stale, missing, contradictory, expired, or adversarial?

Additional concerns include:

- Network partitions.
- Message delay and loss.
- Uncertainty.
- Disagreement between peers.
- Insufficient information.
- Human interpretation of system state.

## Research Question

**Can a carefully engineered, fault-aware cooperative trajectory-sharing and conflict-prediction layer demonstrate measurable benefits beyond existing aviation surveillance, collision avoidance, and trajectory-management approaches — where “benefits” are defined by pre-declared metrics, measured against named baselines, and attributed by ablation?**

At the current concept stage, the answer remains unproven but testable.

---

# 4. System Scope, Objectives, Assumptions, and Non-Goals

## 4.1 Version 0.1 Scope

Version 0.1 operates primarily in simulation.

It processes simulated or appropriately available aircraft-state and traffic information and:

- Maintains a local representation of nearby traffic.
- Represents uncertainty.
- Predicts potential conflicts.
- Evaluates alternative trajectories.
- Exchanges simulated aircraft intent.
- Handles stale messages and communication loss.
- Handles disagreement and invalid inputs.
- Produces advisory recommendations.
- Remains isolated from flight-control commands.
- Keeps existing ACAS/TCAS functions independent.

## 4.2 Explicit Non-Goals

Version 0.1 does not aim to:

- Replace TCAS/ACAS.
- Replace ADS-B, radar, ATC, the flight-management system, or operating procedures.
- Automatically steer, climb, descend, slow, or send commands to an autopilot or flight-control computer.
- Assume every aircraft participates.
- Claim universal LiDAR or camera detection capability.
- Require live 6G or cloud connectivity.
- Require blockchain consensus for local conflict detection.
- Claim certification compliance based on the concept report.

## 4.3 Standing Assumptions

The report identifies several important assumptions:

- Unequipped traffic exists.
- Intent is a claim about planned behaviour, not a guarantee.
- Networks can fail.
- Authentication does not establish sensor truth.
- Access is permission-bound.
- Conflict criteria must be explicitly declared.

---

# 5. System Architecture and Requirements

## 5.1 Layered Architecture

Version 0.1 uses a layered architecture from aircraft/scenario sources through advisory output.

The conceptual layers are:

- **L0 — Aircraft / Scenario Sources**
- **L1 — Input Boundary**
- **L2 — State Estimation**
- **L3 — Prediction**
- **L4 — Planning / Coordination**
- **L5 — Safety Monitor**
- **L6 — Human Interface / Advisory**

The architecture separates:

- External data acquisition.
- Local airspace state.
- Prediction.
- Planning and coordination.
- Independent proposal checking.
- Human interaction.
- Evidence and health logging.

A central architectural rule is that the advisory layer must never create a path to flight-control authority.

## 5.2 Operating States

The advisory-only prototype defines six states:

- `BOOT`
- `PASSIVE_MONITORING`
- `ADVISORY_AVAILABLE`
- `DEGRADED`
- `SUGGESTION_SUPPRESSED`
- `DISABLED`

State transitions are explicitly defined and logged.

Degraded or disabled conditions must remain visible rather than silently disappearing.

## 5.3 System Requirements

Version 0.1 defines ten system-level requirements:

- **SYS-001:** Accept timestamped ownership and traffic-state records from a simulator or authorized data adapter.
- **SYS-002:** Every track carries source, age, quality status, and uncertainty representation or unknown status.
- **SYS-003:** The predictor produces future-position estimates over a configurable study horizon.
- **SYS-004:** The conflict detector evaluates tracks against a declared criterion.
- **SYS-005:** Every proposed alternative is checked against represented traffic and stated constraints before display.
- **SYS-006:** No valid recommendation is shown when essential inputs are stale, inconsistent, or insufficient.
- **SYS-007:** The prototype outputs no flight-control commands and does not modify TCAS/ACAS behaviour.
- **SYS-008:** Loss, delay, duplication, replay-like input, and network partition are observable and logged.
- **SYS-009:** Every advisory state exposes conflict cue, prediction horizon, data-quality indicator, and candidate-check status.
- **SYS-010:** Every experiment records configuration, algorithm version, inputs, outputs, and metrics.

---

# 6. Surveillance Inputs, Sensors, and Non-Cooperative Object Detection

The report distinguishes cooperative surveillance from non-cooperative sensing.

## Cooperative Surveillance

ADS-B provides cooperative aircraft-state information when aircraft are equipped and coverage is available.

However, the report explicitly identifies limitations involving:

- Coverage.
- Equipment dependency.
- Authentication and integrity.
- Current state versus negotiated future intent.

## Non-Cooperative Sensing

The report considers:

- LiDAR
- EO / IR cameras
- Airborne radar

These are treated as research modules rather than universal detection solutions.

The report explicitly avoids unsupported claims that a sensor suite can detect every bird, balloon, drone, glider, or non-cooperative aircraft.

Detection claims require measured target envelopes and false-alarm characteristics.

---

# 7. Communications, Message Formats, Coordination, and Failure Behaviour

## 7.1 Communication Options

Version 0.1 uses a **simulated / virtual network** as the primary research environment.

The report also discusses:

- IEEE 1920.1-class airborne ad hoc networking.
- Existing aviation links.
- Laboratory software-defined radios.
- Future dedicated aviation 6G research.

A dedicated 6G aviation mesh is treated as **future research, not a Version 0.1 prerequisite**.

## 7.2 Conceptual Message Schema

Five conceptual message types define the safety-relevant exchange:

### STATE

Contains concepts such as:

- Protocol version.
- Sender identity.
- Sequence.
- Generation timestamp.
- Expiry.
- Position.
- Altitude.
- Velocity.
- Track or heading.
- Vertical rate.
- Uncertainty.
- Source quality.
- Integrity and authentication metadata.

### INTENT

Represents:

- Sender identity.
- Intent version.
- Validity period.
- Path segments or waypoints.
- Expected speed and altitude profile.
- Uncertainty/confidence.
- Source information.

Intent is a claim about planned behaviour, not a guarantee.

### PROPOSAL

Represents a candidate advisory proposal and includes:

- Proposal identity.
- Participants and tracks.
- Candidate identifier.
- Intended trajectory structure.
- Safety assumptions.
- Creation and expiry.
- Safety-check status.
- Version.

A proposal is not a command or clearance.

### ACK / REJECT

Represents:

- Proposal identity.
- Sender identity.
- Outcome.
- Reason.
- Timestamp.
- Expiry.

Missing, late, or conflicting acknowledgement does not mean confirmed agreement.

### HEALTH

Represents:

- Component status.
- Degraded reason.
- Link state.
- Current software/configuration version.

Health information is diagnostic and must not block the prediction loop.

## 7.3 Coordination

The revised architecture removes blockchain-inspired consensus from the time-critical safety loop.

Version 0.1 adopts:

**Timeout-bounded proposal / acknowledgement with deterministic tie-break and explicit disagreement states.**

The design emphasizes:

- Bounded timing.
- Deterministic behaviour.
- Explicit disagreement.
- Local operation during network partition.
- Observable degradation.

## 7.4 Loss, Partition, Disagreement, and Degradation

The local safety loop must not depend on continuous peer connectivity.

The prototype considers:

- Invalid source data.
- Stale tracks.
- Expired intent.
- Intent-version changes.
- No network response.
- Conflicting proposals.
- Safety-monitor rejection.
- Processor overload.
- Active TCAS/ACAS resolution advisories.

The expected behaviour is to degrade safely and visibly.

---

# 8. Onboard Software Modules and Processing Workflow

The software boundary contains eleven conceptual modules:

- **M1 — Source adapters**
- **M2 — Validation and time**
- **M3 — Track manager**
- **M4 — Intent manager**
- **M5 — Prediction engine**
- **M6 — Conflict detector**
- **M7 — Candidate generator**
- **M8 — Coordination service**
- **M9 — Independent proposal monitor**
- **M10 — Advisory manager**
- **M11 — Health and logging**

The architecture uses deterministic core processing for safety-relevant state transitions, timing, validation, and gating.

Machine-learning components, where considered, remain behind explicit deterministic interfaces and checks.

Technology selection is driven by verification tractability rather than novelty.

## Prediction-to-Advisory Workflow

The conceptual workflow is:

1. Read timestamped source records.
2. Validate events, age, schema, and plausibility.
3. Update tracks.
4. Update versioned intent.
5. Predict future positions with uncertainty.
6. Detect conflicts against a declared criterion.
7. Generate bounded candidate alternatives.
8. Coordinate candidate proposals.
9. Independently re-check candidates.
10. Show accepted advisory information or an explicit no-reliable-recommendation state.
11. Record inputs, versions, outputs, and timing.

---

# 9. Human Factors and the Advisory Interface

The report treats human factors as a core validation requirement.

The interface must make visible:

- Conflict cue.
- Involved tracks.
- Predicted time window.
- Reason for concern.
- Data age.
- Source status.
- Uncertainty.
- Candidate path.
- Expiry and version.
- Coordination status.
- System mode.
- Existing alerts.

The interface must avoid:

- Presenting a proposal as an ATC clearance.
- Presenting a proposal as a guaranteed safe trajectory.
- False precision from stale data.
- Hiding degraded states.
- Suppressing ACAS/TCAS information.

The original augmented-reality "ghost path" concept is postponed.

Version 0.1 begins with a conventional advisory display.

---

# 10. Preliminary Hazard Analysis, Safety Considerations, and Cybersecurity

## 10.1 Preliminary Hazard Register

The report identifies fourteen preliminary hazards covering:

- Data and sensing quality.
- System integrity and security.
- Coordination and network behaviour.
- Safety monitoring and authority.
- Human interface.

Examples include:

- Stale or invalid aircraft-state information.
- Unsafe candidate trajectory.
- Communication failure or network partition.
- Malicious or misleading messages.
- Prediction overconfidence.
- Contradictory advisory information.
- Timing or processor failure.
- Faulty sensor fusion.
- Misleading cockpit presentation.
- Unauthorized data write paths.
- Missed conflicts.
- False alarms.
- Loss of navigation or timing information.
- Conflicting peer proposals.

These hazards are preliminary and are not a substitute for a formal certification-based functional hazard assessment.

## 10.2 Cybersecurity and Traffic-Data Integrity

The cooperative communication layer is treated as an attackable part of the architecture.

Threats considered include:

- Spoofed sensors or forged messages.
- Replay or stale messages.
- Corrupted or malformed data.
- Network partition or jamming.
- Compromised processes.
- Unsafe configuration or updates.

Design controls include:

- Identity and key management.
- Message authentication where suitable.
- Sequence numbers.
- Timestamps.
- Expiry.
- Anti-replay checks.
- Clock-quality status.
- Schema validation.
- Range checks.
- Fail-closed handling.
- Timeouts.
- Link health.
- Bounded retries.
- Degraded mode.
- Process isolation.
- Least privilege.
- Signed builds and updates.
- Logging.
- Watchdogs.
- Configuration integrity.

The report explicitly distinguishes authentication/integrity from truth.

A correctly authenticated message does not prove that the sender's navigation solution or intent is truthful.

## 10.3 Authority Boundaries

The pilot and air traffic control retain authority.

ANIRBAN-1 output is advisory-only and does not change the legal or operational authority structure.

---

# 11. Applicable Standards and Potential Certification Pathway

The report maps the concept to relevant aviation development, safety, cybersecurity, environmental, and human-factors guidance.

The report discusses:

- **DO-178C / ED-12C** — airborne software.
- **DO-254 / ED-80** — airborne electronic hardware.
- **ARP4754A / ARP4754B** — aircraft/system development.
- **ARP4761 / ARP4761A** — safety assessment.
- **DO-160-class** — environmental and EMC qualification.
- **DO-326A / DO-356A-class** — aviation cybersecurity processes.
- **ARP5365A** — cockpit traffic-display human-interface considerations.
- FAA/EASA modification approval pathways where applicable.

These references establish a potential development and assurance pathway.

They do **not** establish that ANIRBAN-1 is certified or compliant.

No assurance level is assigned in this concept report.

Certification applicability remains project-, aircraft-, authority-, and intended-function-specific.

---

# 12. Validation Methodology, Baselines, Metrics, and Acceptance Criteria

## 12.1 Validation Stages

The report defines staged validation from V0 to V6.

### V0 — Model Review

Environment:

- Requirements review.
- Code review.

Focus:

- System boundary.
- Definitions.
- Assumptions.
- Data contracts.
- Threat model.

### V1 — Software Simulation

Environment:

- Multi-aircraft simulator or scenario engine.

Focus:

- Crossing.
- Converging.
- Overtaking.
- Intent changes.
- Uncertainty.
- Multiple traffic.

### V2 — Network Simulation

Environment:

- Virtual network.

Focus:

- Loss.
- Latency.
- Reordering.
- Duplication.
- Partition.
- Replay-like cases.

### V3 — Hardware-in-the-Loop

Environment:

- Bench computer.
- Simulated I/O.
- Optional laboratory sensors or radios.

Focus:

- Timing.
- Restart.
- Resource exhaustion.
- Interface faults.

### V4 — Human Factors

Environment:

- Mock display.
- Controlled operator study.

Focus:

- Comprehension.
- Response.
- Workload.
- Alert interpretation.
- Trust calibration.
- Rejection of incorrect advice.

### V5 — Aircraft Feasibility Study

Environment:

- Aircraft-specific design and safety review.

Focus:

- Interfaces.
- Power.
- EMC.
- Environmental conditions.
- Airworthiness.
- Certification route.

### V6 — Approved Ground and Flight Trials

Only under appropriate authorization and approved test plans.

The progression is evidence-gated rather than calendar-driven.

---

## 12.2 Baselines and Ablation

Three baselines are defined:

### Baseline A

Constant-velocity extrapolation with a geometric proximity test.

### Baseline B

DAIDALUS-style detect-and-avoid implementation.

### Baseline C

A published four-dimensional trajectory conflict-detection and resolution method.

The ANIRBAN-1 variant adds:

- Intent sharing.
- Uncertainty handling.
- Fault-aware coordination.

Ablation runs disable one feature at a time so that measured improvements can be attributed rather than assumed.

---

## 12.3 Metric Families

### Detection

- Conflict detection rate.
- Missed-conflict rate.
- False-alarm rate.
- Warning lead-time distribution.

### Prediction

- Position prediction error by horizon.
- Uncertainty calibration.
- Behaviour under intent change.

### Resolution

- Feasibility rate.
- Constraint violations.
- Path deviation.
- Manoeuvre feasibility.
- Oscillation.
- Repeated replanning.

### Network

- Message age.
- End-to-end delay distribution.
- Packet loss.
- Stale-message rejection.
- Recovery after partition.

### Runtime

- Processing-time distribution.
- Deadline misses.
- Processor and memory use.
- Restart time.
- Event-log completeness.

### Human Factors

- Time to understand an advisory.
- Correct manoeuvre selection.
- Workload.
- Trust calibration.
- Inappropriate acceptance or rejection rates.

---

# 12.4 Research Questions That Define Success

1. Does sharing a planned trajectory improve prediction lead time over current-state-only traffic, measured against Baselines A to C?
2. Under what message-loss conditions does distributed coordination stop adding value?
3. Does uncertainty-aware sensing reduce missed detections without creating unacceptable false alerts?
4. Does the interface help operators correctly distinguish safe from unsafe proposals?
5. What measurable benefit survives after accounting for false alarms and legacy or unequipped aircraft?

---

# 13. Development Roadmap and Evidence Gates

The development roadmap is evidence-driven rather than based on a fixed certification schedule.

The conceptual phases include:

- **Phase 0 — Concept baseline**
- **Phase 1 — Simulation MVP**
- **Phase 2 — Robustness and network**
- **Phase 3 — HIL prototype**
- **Phase 4 — Research aviation study**
- **Phase 5 — Authorized trials**
- **Phase 6 — Operationalization study**

Progression depends on evidence gates.

No phase is considered complete without the evidence required by its gate.

Aircraft integration, operational trials, and certification-related activity remain conditional on:

- Selected platform.
- Defined intended function.
- Manufacturer/design-organization involvement where required.
- Responsible authority.
- Required approval.
- Evidence from earlier stages.

---

# 14. Discussion, Research Gap, Proposed Contributions, and Limitations

## 14.1 Research Position

The report maps ANIRBAN-1 against existing areas including:

- Trajectory mathematics.
- Conflict screening and detection.
- Manoeuvre optimization.
- Alerting and guidance.
- Intent sharing.
- Trajectory-Based Operations.
- ADS-B.
- Air-to-air ad hoc networking.

The report does not claim that these areas are unexplored.

## 14.2 Surviving Research Gap

The remaining research gap is:

> A coherent, testable specification of fault-aware peer coordination covering message expiry and staleness semantics, deterministic disagreement and tie-break outcomes, explicit unconfirmed states when peers do not respond, partition behaviour that preserves local detection, and an advisory interface that exposes these conditions to a human.

The report treats these primarily as protocol-and-evidence problems rather than simply algorithm problems.

---

## 14.3 Candidate Contributions

The report defines four candidate contributions as hypotheses requiring evidence.

### C1 — Fault-Aware State and Intent Exchange

A state and intent exchange schema with:

- Uncertainty.
- Time validity.
- Explicit degradation rules.

Evidence required:

- Schema specification.
- V2 results showing correct expiry and staleness behaviour.
- Comparison against an ADS-B-style state-only feed.

### C2 — Predictable Coordination Under Disagreement

A coordination protocol with deterministic behaviour under:

- Disagreement.
- Message loss.
- Peer non-response.

Evidence required:

- Deterministic tie-break specification.
- Adversarial multi-peer runs.
- V1/V2 results.
- No undefined states in the state machine.

### C3 — Reproducible Evaluation

A combined evaluation of:

- Trajectory sharing.
- Sensing uncertainty.
- Advisory quality.

Across:

- Simulation.
- Hardware-in-the-loop.

Evidence required:

- Open scenario corpus.
- Baseline comparison.
- Ablation attribution.

### C4 — Advisory Presentation of Uncertainty

An advisory presentation that exposes:

- Uncertainty.
- Data freshness.
- Coordination status.

Instead of presenting a falsely confident path.

Evidence required:

- V4 human-factors study.
- Calibrated trust and correction-rejection measures.
- Comparison against relevant published ACAS display research.

---

# 14.4 Limitations

The report explicitly identifies the following limitations:

- No measurements exist.
- No simulation campaign has yet been run.
- Unverified source numbers are flagged rather than corrected through invented estimates.
- The project has no established public research footprint.
- Standards status is as-reported and project-specific applicability remains to be determined.
- Cost and schedule information is qualitative.
- No verified vendor, weight, power, or approval-duration data is asserted.

Therefore, ANIRBAN-1 should be understood as a research hypothesis and technical concept rather than a demonstrated aviation safety improvement.

---

# 15. Decisions Made During Revision of the Original Concept

The revised Version 0.1 retains, revises, postpones, or removes elements of the original concept based on evidence and research scope.

## Retained

- Aircraft-state and planned-trajectory sharing.
- Forward-looking conflict prediction.
- Independent safety monitor.

## Revised

- Aircraft networking architecture.
- Multi-aircraft coordination.
- Ground and ATC integration.
- Certification-pathway presentation.

## Postponed

- Automatic trajectory execution.
- Augmented-reality windshield "ghost path".
- LiDAR / optical / radar non-cooperative sensing as an offline research module.
- Dedicated 6G aviation mesh.

## Removed

- Blockchain/PBFT-style consensus from the time-critical safety loop.

The revised architecture focuses on a smaller, testable research question.

---

# 16. Conclusions and Next Steps

## 16.1 Conclusion

ANIRBAN-1 is positioned as a well-posed research hypothesis with a credible, low-cost test path.

The open research question is whether aircraft can share intent and coordinate under:

- Fault.
- Uncertainty.
- Disagreement.
- Communication loss.
- Stale information.

The correct current status is:

> **A well-posed research hypothesis with a credible, low-cost test path — not a demonstrated safety improvement and not a replacement for any existing system.**

---

## 16.2 Open Decisions

The report identifies seven major open questions:

1. What is the first target: airliner, research aircraft, or unmanned aircraft?
2. Which separation or well-clear criterion governs?
3. Which traffic and intent data are exchanged?
4. How are uncertainty and unknown data represented?
5. What is the safest coordination outcome under disagreement?
6. Which sensor target envelope is in scope?
7. Which authority and certification basis applies?

These decisions gate further implementation and validation.

---

## 16.3 Immediate Next Steps

The report defines the following immediate action set:

1. Freeze Version 0.1 requirements and message schema.
2. Establish Baseline A and B simulation harnesses with the ablation mechanism.
3. Run the V2 fault-injection catalogue against the deterministic coordination protocol.
4. Document the threat model and authentication limits.
5. Draft the V4 human-factors protocol.
6. Open decision records Q1–Q7 and complete contributor statements.

---

# 17. References

The integrated technical concept report contains the complete reference set covering:

- Collision avoidance and detect-and-avoid.
- TCAS / ACAS.
- ADS-B.
- DAIDALUS.
- Trajectory-Based Operations.
- Four-dimensional trajectory conflict detection and resolution.
- Airborne networking.
- Cybersecurity.
- Aviation IoT.
- 6G / IMT-2030.
- DO-178C / ED-12C.
- DO-254 / ED-80.
- ARP4754A / ARP4754B.
- ARP4761 / ARP4761A.
- DO-160-class environmental qualification.
- DO-326A / DO-356A-class cybersecurity.
- ARP5365A human factors.
- Aviation display and automation research.

For the complete reference list and source details, see the full technical concept report.

---

# 18. Glossary

### ACAS / TCAS
Airborne Collision Avoidance System / Traffic Collision Avoidance System.

### ADS-B
Automatic Dependent Surveillance–Broadcast.

### Advisory-only
Displays information and recommendations; outputs no flight-control command.

### AFDX
Avionics Full-Duplex Switched Ethernet.

### 4DT
Four-dimensional trajectory: latitude, longitude, altitude, and time.

### ATC
Air Traffic Control.

### CD&R
Conflict Detection and Resolution.

### CDTI
Cockpit Display of Traffic Information.

### DAIDALUS
NASA Detect and Avoid Alerting Logic for Unmanned Systems.

### Degraded State
A system state in which the system remains available for limited purposes but cannot support its normal confidence level.

### FMS
Flight Management System.

### HIL
Hardware-in-the-loop.

### ICD
Interface Control Document.

### Intent
A stated intended future trajectory; a claim about planned behaviour, not proof of what the aircraft will do.

### MVP / Version 0.1
Minimum viable prototype; here, a simulated, advisory-only research implementation.

### RA / TA
Resolution Advisory / Traffic Advisory.

### STC
Supplemental Type Certificate.

### TBO
Trajectory-Based Operations.

### Unconfirmed State
A declared coordination outcome when a peer does not respond by the deadline; never treated as acceptance.

### Well-Clear / Conflict Criterion
The declared mathematical threshold used to label potentially unsafe proximity; it must be defined for the research domain.

---

# 19. Contributor Statements

### Abu Kayes Huda

Conceived the entire concept and designed the full system.

Developed the IoT mesh architecture, node communication, real-time data routing, redundancy/failover, autonomous aircraft safety logic, and system integration.

### Jaidul Islam Alvi

Participated in early discussions and provided feedback on the idea and system architecture.

Reviewed draft material.

### MD Sakib Hasan

Participated in discussions and provided input on the system architecture and core concept.

Reviewed the final report and presentation.

---

# Full Technical Concept Report

The complete 41-page integrated technical concept report is available in this repository:

**[ANIRBAN-1 Integrated Technical Concept Report](./ANIRBAN-1-Integrated-Technical-Concept-Report.pdf)**

---

# Research Website

The project is also available through the GitHub Pages research website:

**[🌐 Open ANIRBAN-1 Research Website](https://mdsakibhasan-cs.github.io/ANIRBAN-1-Aircraft-Safety-Research/)**

The website provides:

- Project overview.
- Research focus.
- Validation methodology.
- Team contributions.
- Full technical concept report.
- Direct PDF viewing and download.

---

# Repository

**GitHub Repository:**

https://github.com/mdsakibhasan-cs/ANIRBAN-1-Aircraft-Safety-Research

---

# Project Classification

**Collaborative Research & Technical Concept Project**

This repository documents a research concept, technical architecture, proposed validation methodology, research gap, and candidate contributions.

It should not be interpreted as:

- A certified aviation system.
- A demonstrated safety improvement.
- A production flight-control system.
- A replacement for TCAS/ACAS.
- A completed certification programme.
- A published experimental result.

---

# Disclaimer

ANIRBAN-1 is a research concept and proposed validation framework.

The system is advisory-only and simulation-first.

It does not issue flight-control commands and does not replace existing aviation safety systems or operational authority.

All candidate contributions remain hypotheses until supported by appropriate experimental evidence.

Any future real-aircraft integration, operational testing, certification activity, or modification must follow applicable engineering, safety, human-factors, cybersecurity, airworthiness, and regulatory processes under the responsible authorities.
