---
name: portage
description: Keeps working context lean across long tasks. Before each step, loads only the tools, skills, and files that step needs — never the full catalogue. When recall of earlier decisions degrades, writes a handoff document and restarts in a clean agent. Use for long refactors, multi-file edits, or "losing the thread." Never hand off silently; never carry history across the boundary.
---

# portage

Long tasks fail quietly. The agent keeps working, but stops recalling why it chose
what it chose forty messages ago — and starts contradicting itself. Reading more
does not fix this; it is the cause. One rule above all:

**Carry only what the current step needs, and when you can no longer recall
without rereading, put it in writing and start clean.**

## Golden rules

1. **Load for the step, not for the task.** A tool you might need later is a tool
   you are not loading now. Preloading "just in case" is how catalogues get read
   into context whole — the single largest source of avoidable drift.
2. **Re-run discovery at every phase change.** Writing code and running tests need
   different tools. Discovery done once at kickoff is discovery done for a task
   that no longer exists.
3. **Recall failure is the trigger, not token counts.** No environment reports
   remaining budget reliably or uniformly. The honest signal is behavioural: you
   cannot restate a decision, constraint or file state from >15 messages back
   without rereading. That is the threshold. Everything else is corroboration.
4. **Finish the atomic unit first.** Never hand off mid-migration or mid-refactor
   while the tree is inconsistent. A clean agent inheriting a broken state is
   worse than a tired agent finishing the edit.
5. **The document is the only channel.** The successor gets the handoff and
   nothing else — no history, no transcript, no "and also remember". If a fact
   matters, it is written down; if it is not written down, it does not survive.
   This is what makes the boundary real rather than cosmetic.
6. **Next action or nothing.** A handoff without a specific, immediately executable
   next step is a summary, and summaries do not resume work. Write the instruction
   someone could act on cold.
7. **Announce the boundary.** State in one line why you are handing off and where
   the document lives. A silent restart looks to the user like the agent forgot.

## Discovery

Before acting:

1. Enumerate what is available — tools, skills, connected servers.
2. Keep the minimum set. Test: remove it; if the step still runs, it was not needed.
3. Use and name only that set. Do not narrate the full catalogue to the user.
4. Need something unforeseen? Add it at that moment. Not before.

## Drift signals

| signal | weight |
|---|---|
| Cannot recall a decision/constraint from >15 messages back without rereading | decisive |
| More than ~8-10 files read or modified this session | corroborating |
| Beyond ~40-50 turns | corroborating |

Corroborating signals never fire alone. The decisive one always does.

## Handoff protocol

1. Fill the structure in `assets/handoff-template.md` with concrete, checkable
   facts. Generic summary defeats the purpose.
2. Save as `HANDOFF_<task-id>_<timestamp>.md` inside the project, so it outlives
   the context that produced it.
3. Hand over:
   - **If the environment can spawn an isolated agent** — start one with the
     document as its sole input, then stop working in the current context. Your
     part of the task is over.
   - **If it cannot** — present the document in full and tell the user to open a
     new session with it as the first message.
4. Tell the user, in one line, why and where.

Describe the spawn by capability, not by API name: environments differ, and a
skill naming one vendor's mechanism breaks on the other.

## Safety

Handing off discards working state. Constraints:

- Never hand off before the document is written **and saved to disk**. The write
  precedes the discard; nothing is destroyed on the promise of a later write.
- Never hand off from an inconsistent tree (rule 4).
- Never hand off silently — the user must always be able to see the boundary and
  the document behind it.
- If saving fails, do not hand off. Report the failure and continue in the
  current context: degraded recall beats lost work.

## When to use

- Starting anything spanning multiple tools, files or phases.
- Mid-task, when recall of earlier decisions has visibly degraded.
- On request: handoff, context reduction, fresh session, "start over clean".
- Many servers connected, few relevant to the task at hand.

## When NOT to use

- **Short, single-file, few-turn work.** Discovery on a two-step task is overhead.
- **Filtering or reducing a data payload** — that is a transformation on content,
  not on the agent's working set. → use `sieve`.
- **Summarising a conversation for a human reader.** A handoff targets an executor
  with no context; a summary targets someone who was there. Different artefacts.
- **Recovering from an error or a failed run.** Handing off carries the failure
  forward with less context to diagnose it. Fix first, hand off after.
- **Reducing context volume without restarting**: If the context window is crowded or noisy but you do not need a fresh sandbox/session restart → use `chisel` instead.
- **Filesystem checkpointing/rolling back**: For filesystem-level snapshotting rather than conversational handoffs → use `chronicle-session-memory` instead.
- **Reducing context volume without restarting**: If the context window is crowded or noisy but you do not need a fresh sandbox/session restart → use `chisel` instead.
- **Filesystem checkpointing/rolling back**: For filesystem-level snapshotting rather than conversational handoffs → use `chronicle-session-memory` instead.
