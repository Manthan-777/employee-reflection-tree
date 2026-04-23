# Design Rationale: Employee Reflection Tree

## Overview
This project is a deterministic reflection tool that guides an employee through an end-of-day reflection using a decision tree. The goal is to help users gain clarity about how they approached their day—without using any LLM at runtime. Every path is predefined and traceable.

The design is based on three psychological axes:
1. Locus of Control (Axis 1)
2. Contribution vs Expectation (Axis 2)
3. Perspective: Self vs Team (Axis 3)

The tree progresses sequentially across these axes to build a coherent reflection.

---

## Axis 1: Locus of Control (Internal vs External)

This axis explores how the user interprets outcomes.

- Internal locus: The user focuses on their own actions and responses.
- External locus: The user attributes outcomes to external factors.

### Design choices:
- Questions ask how the user interpreted their performance and responded to challenges.
- Options are balanced between internal (e.g., "I took steps to adjust and improve the situation") and external (e.g., "I felt the outcome was influenced by factors outside my control").
- For example, options like "I identified areas for improvement" and "I actively worked on correcting the issue" indicate internal ownership, while options such as "I felt the outcome depended on others' contribution" or "I felt external factors affected how things turned out" reflect an external locus.
- The goal is not to judge but to surface awareness of where control is perceived.

---

## Axis 2: Contribution vs Expectation

This axis explores how the user engaged with others.

- Contribution: The user actively supports or contributes to the team.
- Entitlement/Expectation: The user expects others to contribute or support them.

### Design choices:
- Questions focus on responsibility and collaboration.
- Options reflect both proactive contribution and expectation from others.
- For example, "I actively supported others to help the team succeed" and "I collaborated beyond my own tasks" represent contribution, whereas options like "I expected others to support me when needed" and "I felt others should have contributed more" reflect expectation or entitlement.
- This helps the user reflect on their role within a team dynamic.

---

## Axis 3: Perspective (Self vs Team)

This axis captures how the user evaluates progress.

- Self-focused: Emphasis on personal growth and performance.
- Team-focused: Emphasis on collective outcomes and team progress.

### Design choices:
- Questions ask what the user focused on while evaluating improvements and achievements.
- Options distinguish between individual and team perspectives.
- For example, options like "I focused on improving my own performance" and "I recognized growth in my own skills" indicate a self-focused perspective, while "I focused on the team's overall performance" and "I saw success as a collective team effort" reflect a team-oriented view.
- This completes the reflection by framing how success is interpreted.

---

## Deterministic Structure

The tree is fully deterministic:
- Each question has fixed options (no free text).
- Each option leads to a predefined next node.
- Decision nodes route based on selected answers.
- No ambiguity or runtime inference is used.

This ensures:
- Predictable behavior
- Easy traceability of all paths
- Consistent experience for all users

---

## Signals and State

Each answer contributes to a signal:
- Axis 1 → internal / external
- Axis 2 → contribution / entitlement
- Axis 3 → self / team

These signals are accumulated and used in the final summary using:
- `{axis1.dominant}`
- `{axis2.dominant}`
- `{axis3.dominant}`

This allows a small number of summary nodes to represent many possible paths.

---

## Reflections

Reflection nodes provide insight without judgment:
- They reframe the user's responses
- They do not assign scores or labels
- The tone is neutral and supportive

This aligns with the requirement of:
> guiding reflection, not evaluating performance

---

## Why This Design Works

- Covers all three required axes in sequence
- Uses balanced, non-leading options
- Maintains a natural conversational flow
- Fully deterministic and easy to audit
- Scalable through signal-based summaries instead of duplicating paths

---

## Conclusion

This tree transforms a structured set of questions into a meaningful reflection experience. By combining deterministic logic with psychological framing, it helps users better understand their actions, interactions, and perspective at the end of the day.
