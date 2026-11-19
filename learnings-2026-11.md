## 2026-11-18 — Cold static-review seats WITHHOLD on large files within 600s

- **Type**: feedback
- **Classification**: ⚠️
- **Summary**: Two cold `/static-review` seats on worldarchitect.ai [#11233](https://github.com/jleechanorg/worldarchitect.ai/pull/11233) at `7d0f14d7dd49` WITHHELD because they could not finish large files such as `agent_prompts.py` inside the 600s deadline; prefer saved-material packets scoped to changed regions, and use `knowledgeWork` subagents for truly cold seats.
- **Bead**: none (no `br` on the Grok Scenes box; no existing open bead found)
- **Files**: `mvp_site/agent_prompts.py` and the rest of the #11233 diff at `7d0f14d7dd49`; seats must be rerun at current head `8c018bf7a299`
- **Nextsteps doc**: `nextsteps-2026-11-18.md` in `jleechanorg/worldarchitect-roadmap`
