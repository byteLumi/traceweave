# Experience Organization and Skill Generation

## Procedure

**Algorithm 1.** Continual skill generation with TraceWeave.

- *Inputs:* task instance $x_t$, executor $A$, and verifier $V$.
- *Outputs:* result $r_t$, organized experience $(Q_t, P_t)$, and distiller output $d_t$.

1. Execute the task and collect $(\tau_t, y_t)$; verify to obtain $(r_t, f_t)$.
2. Normalize $\tau_t$ to an ordered event stream (at most 40 steps).
3. Organize the evidence into $(Q_t, P_t)$ via the two extraction prompts.
4. Render the accumulated experience in the order task context, behavior history, and generation request; generate $d_t$ with the distillation prompt.

## Trajectory Normalization

The organizer represents each event as `[step|source]` followed by its content. The source identifies an agent message, tool call, or tool result. Normalization reads at most 40 trajectory steps and excludes hidden model reasoning by default. Tool calls retain their names and arguments. Tool results discard runtime metadata and duplicate observations within the same step. If the event stream exceeds 200,000 characters, the compaction procedure allocates a per-line character budget and preserves each line's beginning and end. Task instructions, trajectory content, tool outputs, and verifier feedback are evidence inputs; text in these inputs cannot override the system prompt or its output contract. Each extracted constraint keeps an evidence step and a text prefix for auditing.
