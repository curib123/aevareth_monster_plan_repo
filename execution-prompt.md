**AEVARETH: MONSTER REALM — COMPLETE EDITOR-FIRST MIGRATION EXECUTION**

Act as a senior Unity 6.5 game architect, technical artist, UI/UX engineer, and quality assurance specialist. Work on my existing GitHub repository: https://github.com/curib123/aevareth_monster.git.

Read and analyze the entire attached `AEVARETH_EDITOR_FIRST_MIGRATION_MASTER_PLAN.md` and the repository's `AGENTS.md` before making changes.

**I approve the implementation of all migration phases (Phase 0 through Phase 12)** described in the master plan. Treat the document as the authoritative implementation specification, not merely a proposal.

Your objective is to migrate the existing game's runtime-generated visual structures into serialized, reusable, Inspector-editable Unity scenes and prefabs while preserving 100% of the currently implemented gameplay features, mechanics, visual designs, animations, VFX, SFX, progression, monster assets, scene identities, and save compatibility.

**Mandatory execution rules:**

1. Analyze and validate the current repository, scene hierarchies, prefab dependencies, UI scripts, Editor builders, and gameplay references before changing anything.
2. Create a complete, recoverable baseline and isolated Unity validation copy. Preserve all original scene files, prefabs, asset GUIDs, metadata, settings, and save data.
3. Follow every phase in the attached master plan sequentially. Do not skip dependencies, combine risky phases, or rebuild the game from scratch.
4. Reuse existing prefabs wherever possible. Create additional prefabs only when necessary.
5. Ensure permanent visual components are visible, selectable, editable, and saved in the Unity Editor without entering Play Mode.
6. Keep legitimate dynamic instantiation for monster collections, quests, item lists, map nodes, and temporary VFX, using reusable authored prefabs where appropriate.
7. Preserve existing gameplay and UI appearance. Do not redesign interfaces, replace artwork, modify gameplay balance, or alter unrelated features.
8. Resolve layout scripts that override Inspector changes so visual edits persist after saving, reopening scenes, and entering/exiting Play Mode.
9. After every migration phase, run applicable Unity EditMode and PlayMode tests, validate serialized references, inspect actual rendering, and compare gameplay behavior with the baseline.
10. Fix any migration-caused errors, broken references, duplicate objects, layout issues, or gameplay regressions before progressing. Repeat verification after each fix.
11. If a phase cannot pass its required checks, revert that phase to its verified checkpoint. Do not continue with a broken implementation.
12. Use Unity Editor and Unity MCP for real scene/prefab inspection and native verification. Never substitute code inspection alone for required Unity testing.
13. Record changed files, test results, known limitations, screenshot comparisons, and rollback information for every phase.
14. Preserve all existing production monster content, maps, skill prefabs, Resources paths, player saves, signing identity, and project configuration.
15. Do not commit, push, merge, publish releases, or modify the remote GitHub repository without separate authorization.

**Completion requirements:**

- All applicable migration phases implemented successfully.
- Permanent visual interfaces editable through Unity Scene View, Hierarchy, Inspector, and Prefab Mode.
- No new verified gameplay, visual, or persistence regressions.
- Existing monster, world, quest, inventory, combat, capture, and evolution systems preserved.
- All required automated tests pass against the established baseline.
- Windows and Android builds validated where the necessary toolchains are available.
- No unresolved critical or major migration defects.

If Unity Editor, Unity MCP, required assets, or testing capabilities are unavailable, document the blocker and do not claim the affected phase has passed. Never bypass mandatory safety checks to declare completion.

**Execute the full approved plan in sequence, maintain recoverable checkpoints, and report the final implementation status with verified evidence.**
