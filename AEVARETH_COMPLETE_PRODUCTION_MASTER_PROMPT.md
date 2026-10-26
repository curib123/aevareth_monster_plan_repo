# Aevareth: Monster Realm — Complete Production Master Prompt

> **For Codex + Unity MCP:** Read this entire file before acting. Perform the repository-wide and native Unity audit first, then implement the verified tasks in order. Use available planning, test-driven development, debugging and review workflows; when installed, use `superpowers:executing-plans` or `superpowers:subagent-driven-development`. Tool availability must be verified, not assumed.

**Goal:** Safely improve the existing game through Editor-first prefab authoring, original medieval music and complete sound design, cinematic visual polishing, and verified Android APK publication to GitHub Releases.

**Architecture:** Retain the current Unity/uGUI game and its gameplay/save authorities. Use authored scenes and prefabs for visual structure, runtime binding for changing data, a single audio presentation authority, and existing skill prefabs with improved original audio/visual presentation. Validate reversible changes against a pinned baseline.

**Tech stack:** The inspected project uses Unity `6000.5.6f1`, URP `17.6.0`, uGUI `2.5.0`, and a local `com.coplaydev.unity-mcp-10.3.0.tgz` package. Preserve these versions unless a separately justified, authorized compatibility change is necessary.

**Repository:** `https://github.com/curib123/aevareth_monster.git`  
**Branch policy:** `main` only, subject to the current `AGENTS.md` and repository protections.  
**Target:** Existing portrait Android ARM64 game; final deliverable is a signed APK, checksum and release evidence uploaded to a published GitHub Release.  
**Specification:** This file is self-contained. It consolidates the earlier Editor-first migration plan, medieval music/non-skill SFX plan, and the user's final approval to improve skill SFX and publish the APK. Older attachments are not required to execute it.  
**Document date:** 26 October 2026.  
**Repository snapshot rechecked for this handoff:** `9c067d29cde664061853f3a41a647fb237cebde3`, committed 25 October 2026 at 22:54:32 UTC / 26 October 2026 at 06:54:32 Manila time. Recheck HEAD before execution.  
**Status:** Finalized execution specification, not a claim that implementation, audio creation, Unity tests, Android tests or publication have happened.

---

## Contents

1. Execution authority and conflict resolution
2. Repository analysis and evidence limits
3. Global preservation and change-management rules
4. Stage 0 — Full repository/native audit and baseline
5. Stage 1 — Editor-first prefab migration
6. Stage 2 — Medieval soundtrack, ambience and non-skill SFX
7. Stage 3 — Graphics, animation, VFX and cinematic skill SFX
8. Stage 4 — Production QA, Android build and GitHub publication
9. Acceptance tests and release gates
10. Resume, reporting and final deliverables
11. Source register and engineering references
12. Copy-and-paste execution prompt

## 1. Execution authority and conflict resolution

Act as a coordinated Unity engineering, technical-art, UI/UX, composition, sound-design and QA team. This role describes responsibilities, not a claim that separate people or tools exist. Use separate agents only when supported, with explicit file ownership; never allow concurrent agents to edit the same Unity scene or prefab.

### Authorized scope when this prompt is invoked

Implement the work, create original assets, run tests, build the APK, make scoped commits, push through the normal permitted repository workflow, create a new release tag on the exact tested commit, and publish the verified APK and checksum to the existing repository. The final publication is authorized; do not ask for routine permission after every passing task.

This authorization does **not** permit deleting unrelated work, force-pushing, changing repository visibility, bypassing branch protections, exposing secrets, replacing the established signing identity, adding monetization or online services, purchasing tools/assets/subscriptions without an agreed budget, or shipping a knowingly failing production build.

### Mandatory production order

`Stage 0: Audit and baseline → Stage 1: Prefab migration → Stage 2: Music and non-skill SFX → Stage 3: Visual polish and skill SFX/VFX → Stage 4: Production QA, Android APK and GitHub Release`.

The following resolves previous instructions explicitly:

- Earlier “proposal only,” “Phase 0–1 only,” and “separate approval to commit/publish” statements are superseded by this execution authorization when the user invokes this file.
- Stage 1 remains a **presentation-authoring migration with visual/audio parity**. Do not mix a redesign or new sound library into it.
- Stage 2 creates music, ambience and non-skill SFX, while preserving the current skill sound clips and phase timing.
- Stage 3 explicitly authorizes **original, improved skill SFX and controlled VFX/presentation changes**. Thus, the old permanent exclusion of `Audio/Skills/` no longer applies to this stage. Preserve skill identities, gameplay rules and recoverable originals.
- The earlier migration plan's final regression/build checks become the Stage 1 migration checkpoint and the Stage 4 final release qualification. Do not publish an intermediate migration APK as the completed enhancement release.
- Later audio/visual enhancements are intentional differences from the migrated baseline, not migration regressions. Record them in an approved-scope change manifest and compare gameplay separately from presentation.
- Ordinary prefab instances, temporary VFX and data-generated lists may still appear only during Play Mode. Their **authored template assets and safe previews** must be editable while stopped. Do not promise to persist arbitrary Play Mode edits automatically.
- “Best quality” means demonstrable readability, original and appropriate sound, musical development, audiovisual synchronization, stable performance and tested behavior—not maximal loudness, particle count, long cut-ins or unnecessary rewrites.

### Safe completion boundary

Continue while prerequisites exist and gates pass. If an essential capability, signing identity, audio production/audition capability, physical-device test or permission is missing, stop the affected gate, retain verified progress and record the exact next action. Do not fabricate assets, waive mandatory tests, label a blocked phase complete or publish an unqualified production release to satisfy the final objective.

## 2. Repository analysis and evidence limits

### 2.1 What this handoff actually inspected

The current `main` SHA was rechecked through the connected GitHub repository. Repository-tree inspection and the earlier static inventories at this **same SHA** were reconciled with fresh reads of project rules, package/build configuration, current Unity context, UI construction/layout, battle state, skill presentation/audio, Android packaging and release metadata. Both supplied master plans were reviewed.

This is a **repository-wide structural and cross-subsystem static audit**, not a claim of a new line-by-line review of every source file or of native deserialization of every asset. The large Home and World Map scenes, imported binary/LFS asset contents, audio waveforms, live Unity state, every test and physical Android behavior still require Stage 0 verification. No Unity Editor session or listening/device tests were performed while producing this document. Never treat historical tests or file inventory as proof that the current candidate runs.

### 2.2 Verified or source-reported baseline

| Area | Evidence and meaning | Execution consequence |
|---|---|---|
| Source identity | Current `main` rechecked as `9c067d2…`; same snapshot as supplied plans | Preserve input SHA; re-audit changed files if HEAD has advanced |
| Inventory | Earlier complete tree inventory at this SHA reports 5,722 entries, 367 C# files, eight scenes and 139 prefabs | Recompute from the actual checkout; numbers are baseline observations, not hard-coded future limits |
| Prefabs | Reported split: 120 skill effects, 16 UI, two Resources UI and one AppRoot | Reuse working assets; do not rebuild the 139 prefabs indiscriminately |
| Build scenes | `EditorBuildSettings.asset` enables Bootstrap, Onboarding, Character Creation, Starter Selection, Home, World Map, Battle in that order | Preserve their paths, GUIDs and indices; retained Monster Codex scene is not automatically a new destination |
| UI factories | `CommerceHost.Prepare/BuildChrome` construct overlays/pages/chrome; the supplied audit identifies Inventory, Settings and Adventure sheets using `CommerceUi` factories | Convert fixed structures and bind dynamic rows without moving commerce/domain authority |
| Skill-card fallback | `SkillCardPanel.Attach/EnsureVisuals` can disable children and create missing art/labels; `Show/Layout` also writes visual properties | Migrate both construction and layout/style ownership, not just GameObject creation |
| Layout authority | `GildedLayout` is `ExecuteAlways` and repositions targets from `_placements`, using a 941 × 1672 reference | Supply Inspector/Scene editing of the authoritative placements; do not disable responsiveness merely to permit dragging |
| Audio baseline | The supplied audio audit reports 17 named UI WAV cues and no identified dedicated BGM library in inspected paths | Verify all assets and callbacks, including uncommitted assets, before adding/replacing audio |
| UI playback | `AevarethUiAudio` owns one source and calls `Stop()` before each cue | Preserve compatibility but prevent ordinary clicks from chopping off meaningful result sounds after enhancement |
| Skill timing | `BattleSkillPresentation` stores four cues in order `[charge, release, impact, block]` plus separate recovery; duration is clamped to 1–1.6 seconds | Preserve this contract or provide a tested compatibility adapter; do not substitute a generic five-attack-phase array |
| Cinematic lifecycle | `BattleCinematicPlayer` caches up to 12 cast instances, uses generation-based cancellation, and resets/stops cast presentation | Preserve cache/cancellation safety; persistent statuses need independent lifetime ownership |
| Combat status | `BattleState` exposes shield strength, shield turns, status turns, and actual shield absorption | Never impose an invented universal “four blocks” rule or count frame updates as turns |
| Save side effects | `HomeScreen.RefreshParty` already calls `TryRecordHomeRest` | Test **no additional unintended domain changes**, allowing existing authorized recovery/homecoming behavior under controlled time |
| Current story flow | Unity context says fresh profiles begin Character → Starter → loading → first story inside World Map → tutorial; intro defaults to 47.2 seconds | Do not select music solely from scene names or assume Title always appears first |
| Gameplay/content | Current context reports 10 worlds, 50 species, 120 skills, world schema 13, profile schema 3, 1,337 nodes, 95 quests, 785 activities and 225 puzzles | Preserve actual catalogs/rules; do not turn activity totals into claims of 785 separate quests |
| Historical tests | Current context reports 1,449 EditMode passes; PlayMode coverage is a full 169/171 run followed by scoped corrections, not one fresh full green run here | Run current complete suites; identify every failure, skipped case and actual evidence file |
| Release history | GitHub returned published `v1.0.0`; repository docs describe an unpublished/local `1.0.1`, code 2 | Determine the next version from releases, tags, settings and documented/local builds; do not blindly pick an old example tag |
| Android builder | Existing builder requires isolated batch identity, seven scenes, ARM64 IL2CPP, package `com.curib123.aevarethmonster`, API 26 minimum and target 36 | Reuse the pipeline and verify exact build inputs; no unrelated engine/toolchain upgrade |
| Signing hazard | PowerShell runner can create a key when absent; the editor build requires an existing key | Add a fail-closed established-key preflight **before** the runner can generate anything |
| Native validation | Existing release docs explicitly lack physical phone validation | Final release gate must obtain actual device evidence; old APK metadata is not a phone test |

### 2.3 Source families to inspect completely before modifying them

All paths below are relative to `Assets/_Aevareth_Monster_Realm/` unless noted.

| Subsystem | Source/asset families | Required audit |
|---|---|---|
| Startup and saves | `Runtime/Core/*`, `Runtime/Adventure/WorldSession*`, `WorldProgress*`, `CombatRuleSnapshot`, `GameBalance`, `JourneyProfile*` | Startup routing, persistence ownership, legacy compatibility, deterministic commands |
| Fixed and dynamic UI | `Runtime/UI/Commerce*`, `InventoryShopView`, `SharedSettingsView`, `RealmAdventureHost`, `RealmPanel`, `Adventure*View`, `SkillCardPanel`, `SkillArtworkView` | Created hierarchy, serialized references, semantic events, modal ownership |
| Already-authored UI | `HomeHubScreen*`, `MonsterCodexView*`, `CompanionCollectionView`, `CompanionTrainingView*`, `MonsterRest*`, `ChoiceSelection*`, `Prefabs/UI/*` | Preserve working templates and separate static shell from dynamic data |
| Layout and style | `GildedLayout`, `PortraitFrame`, `HomeLayout`, `WorldMapLayout`, `BattleStageLayout`, `Runtime/UI/Theme/*` | Competing transform/font/color writers, safe areas, style authority, input feedback |
| World presentation | `WorldMapScreen*`, `WorldSelectionView*`, `AdventureFieldView*`, `MapNodeView`, `FieldNodeView`, `MapRoute*`, camera/avatar classes | Atlas vs field, stable node IDs/routes, return focus, travel and procedural geometry |
| Cinematics | `FirstJourneyFlow`, `JourneyIntroductionView`, `GildedLoadingScreen`, `WorldUnlockReveal`, `ProgressionSequenceController` | Actual clocks, blocked states, success events, pause/resume and cleanup |
| Skill presentation | `BattleScreen*`, `BattleCinematicPlayer`, `BattleSkillPresentation*`, `BattleSoundMix`, `SkillVfxLayer`, `SkillVfxRecipe`, `BattleSkillGraphic*`, `Prefabs/Skills/*`, `Audio/Skills/*` | Per-skill phases, target semantics, existing voice ownership and performance |
| Authoring | `Editor/*`, especially `RealmValidationPipeline`, `CommerceSceneBuilder`, `GildedSceneBuilder*`, `NativeSkillVfxSceneBuilder`, `NativeSkillSoundBuilder` | Destructive write paths, hard-coded validation guards and allowed targeted upgrades |
| Tooling and release | Root `tools/*`, `Packages/*`, `ProjectSettings/*`, `.gitattributes`, `.gitignore`, `docs/android-release.md` | LFS, ignored evidence, test commands, packaging, signing/version policy |
| Tests | All `Tests/EditMode/*`, `Tests/PlayMode/*`, root `tools/tests/*` | Existing coverage, obsolete test assumptions and new regression requirements |

## 3. Global preservation and change-management rules

### Immutable gameplay/product contracts

Preserve original monster production artwork, all intentional variants and metadata, species/form IDs, world/node IDs and positions, route connectivity, enum numeric values including `Grass` displayed as Land, quests/story flags, capture restrictions, skill rules and uses, growth/evolution, currency/inventory transactions, first-bond permanence, saved progress and supported legacy-save behavior.

Retain seven enabled scene identities/order, original Resources keys, Android application identity and established signing certificate. Preserve the legacy eighth scene unless the user explicitly approves its removal. Do not add UI Toolkit, a new networking stack, a different render pipeline, Cinemachine/VFX Graph, new monetization, new monsters/worlds or a new combat system merely for this work.

### Editable scope and baseline rules

- Stage 1 may modify presentation code, serialized scenes/prefabs and tests, but must preserve current rendering and sound.
- Stage 2 may add original music/ambience and improve non-skill SFX/settings, with preserved legacy preference semantics.
- Stage 3 may enhance existing UI/environment presentation and skill VFX/SFX in place. These authorized assets become a documented changed allowlist; their old hashes are not incorrectly required to stay identical.
- Original monster images, gameplay data and save rules stay protected. A proven presentation-only read adapter is permissible if narrowly necessary, with deterministic tests and no schema change.
- Preserve existing asset GUIDs. Where extracting a prefab necessarily changes local object IDs, explicitly map and verify every affected serialized reference and persistent event; do not claim local IDs remained identical when they did not.
- Never delete old audio/art before complete replacement verification. Retain Git history and external backups. Do not ship every backup copy in `Resources` and inflate the APK.

### Operating procedure for every task

1. Record current input SHA, local changes and exact planned file/hierarchy edits. Preserve unrelated dirty files and unsaved Unity scenes; never use blanket `reset --hard`, `clean`, force-add, force-push or automatic stashing to obtain a clean baseline.
2. Work in the required disposable filesystem validation copy. The current Commerce builder checks a specific validation path and the `CodexValidation` / `AevarethExplorationValidated` identity. Do not bypass the guard or edit the player's active project to satisfy it. Use safe targeted Unity APIs/tools instead of running broad generators.
3. Write a focused failing regression test where suitable; run it, make the smallest scoped change, rerun it, then run affected integration checks. Maintain real visual/audio inspection separately.
4. Author scene/prefab structures through Unity Editor/Prefab APIs using Undo, serialized properties and proper dirty/save handling. Do not hand-rebuild large YAML scenes or bulk-reserialize the project. Do not auto-author on import or `OnValidate`.
5. Diff changed paths, GUIDs, references and protected hashes. Apply only validated changes to intended source paths, without copying validation company/product settings or fixture saves into production.
6. Record evidence and a scoped rollback checkpoint. Restore only task-owned changes if necessary; never erase later or unrelated work. Commit only coherent verified changes under the repository's `main` policy.
7. Revalidate the actual integrated candidate, not only the separate authoring copy. If remote main changes, reconcile safely and rerun affected checks; never force the old snapshot over new work.

All AI plans/checklists/execution ledgers belong in ignored `docs/gpt-plans/`, per `AGENTS.md`; never force-add them. Keep raw evidence in ignored `Logs/ProductionUpgrade/`, build artifacts in ignored `Builds/`, and durable architecture/art-license/test summaries in their existing tracked documentation homes. Preserve unrelated active plans.

### Five high-risk review cases

- Edit-time previews accidentally load/save the real player or mutate a prefab asset on selection.
- A migrated layout looks correct once but runtime skinning or layout writes erase Inspector edits.
- A presentation-only change consumes combat RNG, repeats a saved transaction, or removes an existing recovery update.
- Old cast cleanup stops a new cast or leaves persistent shield/buff sounds attached to a recycled actor.
- A release tag, APK, source commit or signing certificate does not match the validated candidate.

Each case has a required test in Section 9. A missing tool is not permission to waive a test.

## 4. Stage 0 — Full repository/native audit and baseline

**Deliverable:** A complete machine-readable inventory and a reproducible protected baseline. Do this before production changes.

### Task 0.1 — Verify the execution environment

- [ ] Verify local Git remote, branch, actual HEAD, dirty files, submodules if any, LFS objects and untracked production assets. Read current `AGENTS.md` and newest Unity context sections before older records.
- [ ] Verify Unity version from `ProjectVersion.txt`, packages/lock, license/toolchain availability and a clean import/compile result. Do not auto-upgrade packages.
- [ ] Use a read-only MCP call to identify **project path, active scene, Unity instance and editor state**. Before every mutation, confirm it targets the validation instance, not the player's editor. Inventory actual MCP tool capabilities; don't invent tool names.
- [ ] Verify screenshot capture, native tests, Android SDK/NDK/JDK, build entry point, audio creation/editing/export and actual audition capabilities, GPU/device profiling, Git authentication and release-upload access.
- [ ] Verify original signing files are present/readable under the appropriate Windows identity without printing secrets. Record only the certificate fingerprint. No key generation.
- [ ] Separate available capabilities, missing prerequisites and human-only checks. Do not claim Codex/MCP alone can produce or judge professional music without a real audio workflow.

### Task 0.2 — Inventory the whole project

- [ ] Scan every source/assembly, enabled and retained scene, prefab, material/shader, animation, imported asset, map/monster/catalog, audio clip, test, tool, package and release instruction. Record paths, hashes and references; classify unrelated assets as protected rather than deleting them.
- [ ] Use Unity to enumerate scene roots, inactive modals, prefab instances, missing scripts, persistent event targets, Resources lookups and runtime-created objects. Visit each relevant UI state and compare before/after Play hierarchies.
- [ ] Emit a UI ownership manifest: scene → hierarchy → view/presenter → construction method → prefab → layout/style owner → domain command → open/close/focus behavior → migration task.
- [ ] Emit an audio manifest: cue ID → clip/GUID → creator/provenance → source/mixer group → callback → gain/pitch → concurrency → loop/phase → lifecycle cleanup. Audition all existing UI cues and representative/all skill cues according to the later coverage plan.
- [ ] Emit a per-skill presentation manifest for **every actual skill**: stable ID, element, kind/behavior, legal target, existing phases/duration, VFX objects, sound clips and status semantics. Reconcile all catalogs with prefab/audio references.
- [ ] Emit save compatibility, route/encounter classification, asset rights, build/signing and release-history inventories. Read actual postgame IDs rather than guessing from display names or rarity.

### Task 0.3 — Establish evidence and recovery

- [ ] Snapshot source inputs, metadata and uncommitted work outside the checkout. Never upload player saves, credentials or signing material to the audit package.
- [ ] Use deterministic disposable profiles, isolated saves and controlled time for regression tests. Confirm tests cannot write the real `Application.persistentDataPath`.
- [ ] Capture native UI fixtures, music/sound behavior, representative combat recordings and baseline device performance. Separate current evidence from historical records.
- [ ] Run repository tooling, complete EditMode/PlayMode suites and a baseline player build. Android/native tests that cannot run remain blocked; document them before making production claims.
- [ ] Define protected files, authorized change categories, checkpoint locations and a resumable task ledger.

**Gate G0:** Verified input identity, complete ownership maps, working recovery path, actual Unity inspection capability and classified baseline failures. No hidden mutation of source/player data. If exhaustive coverage is unfinished, say exactly what remains; do not label the whole audit complete.

## 5. Stage 1 — Editor-first prefab migration

**Objective:** Change authoring, not the game. Existing UI, audio and gameplay remain equivalent at this stage.

### Authoring contract

Fixed visual structure belongs in original scenes or reusable prefab assets. Repeated content is instantiated from templates and bound to live data. Procedural route/element geometry may remain procedural on an editable serialized host. Modals need not all be active in the same scene: Prefab Mode and non-destructive preview fixtures must expose them while stopped.

Use typed serialized references, `Bind/Refresh/Open/Close` separation and balanced event subscription. Prevent duplicate hierarchies and callbacks. Missing required references fail validation with an actionable error; migrated production screens must not silently reconstruct a different fallback UI.

### Tasks in dependency order

| Task | Existing owners / scope | Required result and test |
|---|---|---|
| M01: Preview/layout foundation | `GildedLayout`, `PortraitFrame`, `HomeLayout`, `WorldMapLayout`, `BattleStageLayout`, theme/skin writers | One editable source of truth; Scene handles/Inspector update that source; Undo/Redo, save/reopen and Play/Stop preserve edits |
| M02: Shared template binding | Existing Button/Panel/Modal/ItemSlot/QuestCard/MonsterCard/SkillCard prefabs | Reuse and validate templates; no gratuitous library replacement; no duplicate persistent events |
| M03: Battle skill-card pilot | `SkillCardPanel`, `SkillArtworkView`, `BattleSkillPanel`, `BattleSkillCardView`, Battle scene | Existing 2×2 slots serialized or prefab-backed; actual use/cooldown/disabled state remains data-driven; no construction of missing permanent labels in normal play |
| M04: Battle sheets/results | `BattleItemView`, `PrismIconGraphic`, `PostBattleProgression`, related presenters | Editable item/Prism drawer and row templates; all ten Prisms; cancel costs nothing; results/evolution retain existing behavior |
| M05: Commerce and settings | `CommerceHost`, `InventoryShopView`, `SharedSettingsView`, active settings owners | Authored shell/header/dock/details/quantity/slider wiring; dynamic product rows; real wallet/receipts and readonly identity unchanged |
| M06: Adventure sheets | `RealmAdventureHost`, `RealmPanel`, `AdventureJournalView`, `AdventureActivityView` | Editable Journal/activity/evidence/rest forms and choice templates; same quest rules, hints, free rest and bounded resupply |
| M07: Home and Codex | `HomeHubScreen*`, `MonsterCodexView*`, collection/training/rest presenters | Preserve working scene/templates; preview unknown/owned/sleeping/forms/skills; no resurrected Farm/Companions routes |
| M08: World/atlas/field | `WorldMapScreen*`, `WorldSelectionView*`, `AdventureFieldView*`, node/route/camera views | Fixed HUD editable; data-driven maps/nodes preserved; marker/route templates and selected-map preview; no baking all nodes into scenes |
| M09: Startup and loading | Bootstrap/Onboarding/Character/Starter scenes; existing Resources loading/intro prefabs | Preserve fresh/returning routing, permanent selections, first-story/tutorial checkpoints, loading progress and retries |
| M10: Targeted cleanup/integration | Remaining fixed-layout factories and authoring callers | Retire only replaced construction paths; retain procedural graphics, dynamic rows and all compatibility references; reimport integrated source and run migration regression |

### Required implementation details

For M01, do not require direct RectTransform coordinates to override an active layout group. Instead make **layout settings themselves** authorable. Preserve responsive reflow from stored values. Inspect font, color, sprite, active-state and transform writers, not only positions. Use serialized compact/full skill-card variants where needed, not hard-coded resets that undo customization.

For M02–M03, update in-use prefab contents in place where possible. Existing `AevarethCelestialSkillCard.prefab` already has child art; prefer using it over creating another incompatible card. Separate temporary Editor migration helpers from runtime assemblies without breaking existing callers or tests. Do not move still-required static utility methods into Editor code prematurely.

For all previews, use preview scenes or isolated hosts, deterministic fake data and disposable saves. Preview must not instantiate a production `AppRoot` against real storage, run transactions, dirty original assets unexpectedly, autoplay audio, or leak into player builds. Do not add `ExecuteAlways` to gameplay components as a shortcut.

Preserve native input ownership, raycast targets, focus restoration, close-frame guards, selection, scroll positions and disabled states. Validate open/close/open and scene reloads, including disabled domain reload where supported.

### Per-screen migration acceptance

- [ ] Stop Play; open the scene/prefab or approved preview; select and edit a fixed control.
- [ ] Save, reopen Unity/scene/prefab, exercise Undo/Redo, enter/exit Play and verify the authored value remains authoritative.
- [ ] Confirm preview values never become real save data and runtime values replace previews normally.
- [ ] Compare deterministic screenshots and event/gameplay traces with the baseline across required resolutions.
- [ ] Reopen a migrated modal 100 times; no growing child/listener counts or hidden raycast blockers.
- [ ] Validate missing-reference scans, all affected tests, then complete migration regression and player-build smoke checks.

**Gate G1:** All existing fixed UI is authorable through scenes/prefabs/previews; gameplay, saves, sound and appearance retain baseline behavior; no unresolved migration regressions. Record a new **migration-stable baseline** before audio or visual improvements. Physical final-release qualification remains G4, not an excuse to skip migration-level native checks.

## 6. Stage 2 — Medieval soundtrack, ambience and non-skill SFX

**Objective:** Create real, original, usable music and non-skill sound assets, then integrate them into the stabilized presentation. Do not replace skill phase sounds yet; that is Stage 3.

### 6.1 Art direction and production workflow

Aevareth should sound like an intimate medieval-fantasy adventure: expressive wooden flute/recorder, lute, harp, dulcimer, warm strings, restrained horns, frame drums, ancient bells, subtle choirs and magical textures. Avoid constant trailer percussion, harsh synthetic beeps, overwhelming choir or modern dance rhythms during ordinary exploration.

Use an original five-note **Lantern Motif**, provisionally scale degrees `1–2–mode-dependent 3–5–4`, as a recurring identity. This is a creative brief, not an existing game asset. Each realm needs its own melody, instrumentation and emotional arc; changing only pitch/instrument on the same loop is insufficient.

Start with Home, Verdant Reach and Wild Battle prototypes plus a small UI click/confirm set. Listen in the real game on headphones and a phone speaker, document the quality review, refine, then produce the full catalog. The user's authorization allows professional creative decisions without repeated approval requests, but does not permit pretending a listening review occurred. Record who/what actually auditioned each asset; an unavailable audition capability is a quality gate blocker.

Compose using tools and source instruments genuinely available and permitted. Retain editable sessions/MIDI/stems where the production method supports them; otherwise document actual source materials and reproducible settings. Record provenance, licenses and commercial-distribution permissions. Do not extract or sample existing game/anime soundtracks or treat an unlicensed sample library as cleared. External paid generation/purchases need an agreed budget.

### 6.2 Ten elemental exploration themes

All following titles, tempos and modes are **proposed composition directions**. Produce seamless, developed loops around 1:45–3:00, with contrasting phrases, breathing room and clean tails. Adjust the exact tempo/length when needed for musical quality, recording the final values. Music follows the active field's stable map ID, not a hovered or locked atlas destination.

| Map ID / world | Cue ID and proposed title | Palette and musical direction | Separate ambience |
|---|---|---|---|
| `verdant-reach` — Land | `bgm_world_verdant_reach` — Lanterns Through the Green | About 78 BPM, D Dorian; wooden flute, lute, harp, warm viola; safe first adventure | Leaves, distant birds, soft forest air |
| `tideglass-coast` — Water | `bgm_world_tideglass_coast` — The Pearl Lantern Tide | About 72 BPM, D Mixolydian; flowing harp, oboe, bell harmonics; gentle coastal mystery | Surf, rope/rigging, distant harbor |
| `emberfall-peaks` — Fire | `bgm_world_emberfall_peaks` — Heart of the Ember Forge | About 94 BPM, E minor/modal; cello, dulcimer, restrained frame drum; courage and artisanship | Quiet forge, embers, volcanic wind |
| `zephyr-heights` — Air | `bgm_world_zephyr_heights` — Steps Above the Clouds | About 82 BPM, G Lydian; recorder, harp, bowed texture, soft bells; open sky and monasteries | Wind, ropes, distant bells |
| `stormforge-reach` — Electric | `bgm_world_stormforge_reach` — Sparks of the Old Relay | About 96 BPM, B Dorian; interlocking plucks, dulcimer, viola pulse; magical ingenuity, not EDM | Workshop movement, distant thunder |
| `frostveil-expanse` — Ice | `bgm_world_frostveil_expanse` — Snow Beneath the Aurora | About 62 BPM, F minor/Dorian color; strings, glassy harp, restrained choir; loneliness and shelter | Snow, cold air, distant ice resonance |
| `dawnspire-sanctuary` — Light | `bgm_world_dawnspire_sanctuary` — Hymn of the Open Gate | About 74 BPM, C Lydian; chamber choir, harp, gentle organ; dignity and hope | Sanctuary air, sparse soft chimes |
| `umbral-hollow` — Dark | `bgm_world_umbral_hollow` — The Unfinished Choir | About 66 BPM, A Aeolian; low viol, sparse lute, wordless choir; memory and melancholy, not horror spam | Cavern air and distant resonance |
| `venomfen-marsh` — Poison | `bgm_world_venomfen_marsh` — Reeds of the Wounded Fen | About 72 BPM, C Dorian; reed flute, pizzicato, light percussion; fragile beauty and uncertainty | Reeds, insects, occasional bubbles |
| `astral-reverie` — Psychic | `bgm_world_astral_reverie` — Dreams Beyond the Lantern | About 70 BPM, E Lydian; harp, glass bells, floating choir; dreamlike discovery | Subtle ethereal air |

Deliver each realm ambience as a separate approximately 35–80 second seamless bed when it improves the scene. Do not bake birds/thunder into every repetition of a musical phrase. Ten ambience candidates are in scope; integrate each only after its acoustic/performance review. Quiet/tension stems are optional later refinements, not a reason to delay the required ten excellent base themes.

### 6.3 Complete music catalog and playback policy

Produce the **31-item music slate** below: the ten realm loops above plus 16 other loop beds, one timed score and four stingers. Conditional tracks may be delivered as reserved soundtrack assets, but never invent new scenes/features just to claim all tracks have an in-game trigger. Identify each item as integrated, conditional/reserved, or blocked.

| Additional loop cue | Target duration | Where/when it plays |
|---|---|---|
| `bgm_title_lanterns_at_dawn` | 1:45–2:20 | Actual Onboarding/Title view only; recognizable gentle main theme |
| `bgm_character_oath` | 1:30–2:15 | Character Creation; intimate anticipation |
| `bgm_starter_first_bond` | 1:45–2:20 | Starter Selection; warmth and friendship |
| `bgm_home_lanternrest` | 2:00–3:00 | Home, collection and routine rest; a calming sanctuary |
| `bgm_atlas_ten_seals` | 1:45–2:30 | Atlas/world chooser; not the currently open exploration field |
| `bgm_codex_pages_of_concord` | 1:30–2:00 | Sustained Codex browsing when a dedicated theme improves it; short overlays retain the previous bed |
| `bgm_battle_wild` | 1:35–2:20 | Ordinary wild encounters; agile strings/lute, modest drums |
| `bgm_battle_trainer` | 1:40–2:30 | Trainer/story trials; tactical momentum |
| `bgm_battle_guardian` | 2:00–2:50 | Verified guardian/boss contexts; heroic but readable |
| `bgm_battle_legendary` | 2:00–3:00 | Actual legendary encounter context; mystical rarity |
| `bgm_battle_concord_tower` | 1:50–2:40 | Verified Tower/designated elite challenges; determined escalation |
| `bgm_battle_unanswered_star` | 2:30–3:15 | The actual Unanswered Star encounter only; full thematic culmination |
| `bgm_concord_tower_hall` | 1:45–2:30 | Tower preparation only if an actual distinct state exists; otherwise reserved, retain atlas/world bed |
| `bgm_epilogue_concord_homecoming` | 2:00–2:40 | Actual accepted epilogue presentation, not routine Home entry |
| `bgm_credits_lanterns_return` | 2:00–3:00 | Existing credits presentation if present; otherwise soundtrack bonus, no new credits scene required |
| `bgm_loading_lantern_hum` | 0:25–0:45 | Fallback for genuinely long loading; short transitions preserve prior music |

**Timed score:** `score_first_journey` follows the actual `JourneyIntroductionView` duration, currently 4 seconds of title + 42 seconds of crawl + 1.2 seconds of fade. Compose a 47.2-second version: ancient seal/title → fading lantern mystery → first-bond hope → resolution into Verdant Reach. Follow `PlaybackSeconds`, blocked states, loading, pause, retry and reduced-motion presentation. The view caps elapsed-time increments: playing a wall-clock track for 47.2 seconds is not sufficient synchronization during a stall. Do not change story timing/checkpoints to fit the music.

**Stingers:** `stinger_battle_entry`, `stinger_battle_victory`, `stinger_battle_defeat`, `stinger_realm_unlock`. Entry is optional when a battle intro already supplies the accent. Victory/defeat/unlock must replace or coordinate with existing semantic result cues, never blindly double them. Capture, level-up and quest success generally remain short SFX instead of changing the entire BGM.

### 6.4 State resolution and transitions

Implement a read-only music-context resolver. Observe current scene **and** actual UI/encounter/story state; never change gameplay/save flags to select a song.

| Condition | Required behavior |
|---|---|
| Bootstrap destination not established | Silence/retain pending state; never force Title music |
| New profile skips Title | Character theme follows the actual startup destination |
| Atlas → active field | Crossfade to active `MapDefinition.Id`; locked selections cannot change exploration music |
| Journal, inventory, ordinary settings, NPC/puzzle overlay | Preserve underlying bed; optionally duck about 3–6 dB; no restart per page |
| Home → collection/details → Home | Continuous Home music unless an intentional long Codex context takes over |
| Battle entry | Resolve actual encounter once; special IDs override generic classifications |
| Battle precedence | Verified superboss → verified Tower/elite → actual legendary → ordinary Boss/guardian → Trainer → Wild |
| Battle result | Use accepted/committed result and existing presenter ordering; one outcome cue; fade combat music appropriately |
| Return from battle | Restore current valid world/atlas/Home context, not an obsolete queued request |
| First story/epilogue | Explicit cinematic context; timeline-aligned score; no accidental replay on ordinary World Map load |
| World reveal | Coordinate with existing 4.2-second reveal/skip/interruption; music cannot acknowledge the reveal |
| Fast loading | Continue/soften previous bed; use loading fallback only after a measured delay, approximately 1.5–2 seconds initially |
| Mute, music volume zero, app background | Immediate correct silence/pause; no source may bypass master mute |
| App resume/audio-device interruption | Revalidate current context and restore safely; never resume a stale battle cue |

Use approximately 1–2.5 second normal crossfades, 250–500 ms dialogue-duck attack and 400–900 ms release as starting values, not immutable requirements. Identical music requests are no-ops. Cancel obsolete transitions with a generation/token. Preserve context through overlays without retaining an unlimited stack of clips. Use DSP scheduling when sample/beat-accurate stitching is required; don't impose beat waits on gameplay input. Validate all seams in the imported Android build. [T1–T2]

### 6.5 Non-skill SFX coverage

Retain the existing 17 public cue IDs for compatibility, audition them and explicitly keep/revise/replace each:

`ui_cancel`, `ui_capture_failure`, `ui_capture_success`, `ui_click`, `ui_close`, `ui_confirm`, `ui_defeat`, `ui_error`, `ui_item`, `ui_levelup`, `ui_locked`, `ui_notification`, `ui_open`, `ui_purchase`, `ui_quest`, `ui_skill`, `ui_victory`.

`ui_skill` is the existing learning/equipping confirmation, not an attack sound. Inspect `ProgressionSequenceController` level/evolution clips, `WorldUnlockReveal._chime`, `BattleScreen` outcomes and dynamic UI feedback before adding another owner.

Create/reconcile these **33 additional semantic cue families**. An existing equivalent may be reused through an explicit alias instead of adding redundant events/files. Supply subtle 2–4 variants for frequently repeated tactile cues where helpful.

| Family | Proposed IDs | Trigger rule |
|---|---|---|
| Controls/navigation — 10 | `sfx_ui_focus`, `sfx_ui_tab_switch`, `sfx_ui_scroll_tick`, `sfx_ui_toggle_on`, `sfx_ui_toggle_off`, `sfx_ui_slider_release`, `sfx_ui_modal_open`, `sfx_ui_modal_close`, `sfx_ui_page_turn`, `sfx_ui_long_confirm` | Actual user interaction/state change; no sound from initial data binding, automatic focus restoration or every drag pixel |
| World/quests — 10 | `sfx_world_step_soft`, `sfx_world_node_select`, `sfx_world_route_confirm`, `sfx_world_blocked_path`, `sfx_world_treasure_open`, `sfx_world_portal`, `sfx_world_npc_dialogue_open`, `sfx_world_dialogue_advance`, `sfx_world_puzzle_success`, `sfx_world_puzzle_incorrect` | Actual travel beat/accepted interaction; quiet wrong-answer cue; no fake rewards or footstep per frame |
| Collection/commerce — 8 | `sfx_codex_discovery`, `sfx_monster_card_select`, `sfx_inventory_pickup`, `sfx_inventory_use`, `sfx_coin_gain`, `sfx_quest_claim`, `sfx_shop_buy_reject`, `sfx_rest_camp` | Committed outcome for inventory/rewards/rest; selection is a separate cosmetic event |
| Narrative/progression — 5 | `sfx_intro_lantern_ignite`, `sfx_realm_seal_glow`, `sfx_story_choice_commit`, `sfx_postgame_floor_clear`, `sfx_epilogue_resolution` | Corresponding real presentation/accepted event; deduplicate against stingers and existing outcome sounds |

Use antique brass, soft wood, parchment, coins, cloth, glass and restrained magical chimes. Frequent clicks should be short and quiet. Avoid error alarms for harmless unavailable actions. One accepted interaction gets one intentional semantic response, not a generic click plus multiple independent success sounds.

### 6.6 Unity audio architecture and concrete responsibilities

Reuse the existing persistent presentation ownership where practical; implement **one** authoritative audio service instantiated from an editable prefab, with no extra AudioListener. Proposed new names below are implementation targets, not claims these files already exist. Adapt names to avoid duplicates discovered in Stage 0.

```text
Assets/_Aevareth_Monster_Realm/
  Audio/Music/                       # Production music clips
  Audio/Ambience/                    # Reviewed realm beds
  Audio/UI/                          # Compatible existing/new UI and world-feedback cues
  Audio/Mixers/AevarethAudio.mixer
  Prefabs/Audio/AevarethAudioDirector.prefab
  Resources/Aevareth/Audio/
    MusicCatalog.asset
    NonSkillSfxCatalog.asset
  Runtime/UI/Audio/
    AevarethAudioDirector.cs          # Persistent playback and transitions
    MusicContextResolver.cs          # Read-only state -> cue mapping
    NonSkillSfxPlayer.cs              # Bounded semantic voices and deduplication
    AudioSettingsBridge.cs           # Legacy keys and new mixer controls
  Editor/Audio/                      # Guarded audition, binding and import validators
```

Use stable cue IDs and a single catalog of clip references, gains, priorities, loop metadata, cooldowns, allowed contexts and duck policy. Retain `AevarethUiRuntime.PlayCue(id)` as a compatibility facade where viable. Do not keep two competing services responding to the same event.

Mixer groups: Master → Music, UI, World SFX, Skill SFX, Ambience. Add a separate Skill volume now without replacing the clips; route existing skill playback safely. Preserve `Aevareth.Presentation.Muted` and `Aevareth.Presentation.UiVolume` behavior, plus motion/flash preferences. New Master/Music/World/Skill/Ambience settings need independent keys, immediate application and safe defaults. Updating a slider or binding its value must not replay an event or unintentionally square the gain through two multipliers. Snapshot ducking and user volume need separate attenuation controls, so one does not overwrite the other.

Start with two BGM voices, one realm ambience voice (allow a second only during a bounded transition), a bounded 6–10 voice UI/world pool, and the existing three skill-phase voices. Important result cues outrank incidental clicks. Persistent skill loops later get their own low bounded budget. These are proposed initial limits; profile actual hardware before increasing them. Never use an unbounded AudioSource-per-click scheme. [T1]

Random variant selection must use **presentation-only randomness**, not consume or reseed battle RNG. Dynamic prefab rows must acquire feedback when bound; a scene-load skinning pass alone will miss controls created later. Subscribe/unsubscribe once; no repeated scene scans every frame. Missing clips yield a diagnostic and silence, never a gameplay exception or transaction retry.

### 6.7 Production, import and acoustic gates

- [ ] Export real lossless 48 kHz/24-bit masters, with final sample count, loop boundaries, tempo/meter, version, provenance and source/stem inventory. Avoid unnecessary lossy-to-lossy transcoding; let verified Unity platform settings produce the player format.
- [ ] Check waveform discontinuities, tails and encoder/import seams over at least ten consecutive loop repetitions. Do not normalize long music and tiny transient SFX using one arbitrary loudness rule.
- [ ] Set a recorded mix target and leave headroom. Starting music mastering range around −20 to −16 LUFS integrated and ≤ −1 dBTP may be auditioned; these are proposed targets, not a universal quality guarantee. Judge short SFX by peaks, envelope and in-game perception.
- [ ] Evaluate Streaming for long BGM and appropriate PCM/ADPCM/compressed settings for short cues. Measure decode CPU, loading delay and memory; don't preload every song. Unity's import modes have different costs. [T1]
- [ ] Keep an incremental audio-size budget, initially roughly 60–90 MB for music/non-skill audio as a planning target; report actual compressed build growth, not source-WAV size. Do not cut protected content just to meet this estimate.
- [ ] Test phone speaker, earbuds/headphones and mono compatibility; no harsh peaks, clipping, irritating repeated cues or low-end energy that masks speech-like UI cues/skill attacks.
- [ ] Store a cue-by-cue native integration/listening receipt. Reserved Tower-hall/credits cues must be labeled honestly rather than claimed as active features.

**Gate G2:** Required world/menu/battle/story music and reviewed non-skill cues are real, original, correctly routed and auditioned; settings/lifecycle tests pass; no skill-clip replacement or gameplay/save regression has occurred. Record the audio-stable baseline before Stage 3.

## 7. Stage 3 — Graphics, animation, VFX and cinematic skill SFX

**Objective:** Improve the migrated game substantially while retaining its identity, gameplay and performance. This stage explicitly includes the previously excluded skill sound library.

### 7.1 Visual direction and restraint

Keep the existing Gilded Sigil/Celestial-derived fantasy identity, original monster/character art, painted worlds and native uGUI composition. Do not reinterpret this project as a new fully 3D game or replace its artwork to demonstrate a new renderer. Improve the systems actually present.

Polish readability, spacing, alignment, typography, icon framing, focus/disabled states, panel transitions, depth cues, atmospheric layers, parallax where supported, camera settling, grounding, idle/breathing motion, travel feedback, discoveries, dialogue, progression and evolution. Preserve map geometry/routes and input timing. Keep backgrounds full-screen with safe-area-aware controls.

Use editable prefab parameters and reusable animation/material profiles. Add only effects that communicate place, action or status; avoid covering actors, HP, skill uses or touch controls. Retain reduced-motion and reduced-flash preferences throughout. Do not rescale protected sprites destructively or edit canonical image files to create motion; animate their existing presentation transforms instead.

### 7.2 Cinematic sound reference — original work only

Use the broad fantasy-anime qualities the user associates with **That Time I Got Reincarnated as a Slime**: precise attack transients, layered magical resonance, controlled pressure/energy swells, elemental movement, decisive contact and satisfying decay.

Create original sounds with their own identity. Do not rip, extract or sample identifiable anime audio, voices, catchphrases, music or proprietary sound libraries. Do not merely rename an existing show's audio or claim imitation is an original composition. Retain source and rights records for every ingredient.

Ordinary moves should feel tactile and decisive; support moves should feel protective or empowering; ultimates should gain scale through orchestration, contrast and timing rather than unsafe loudness. Phone-speaker clarity and repeated-play comfort take priority over inaudible sub-bass.

### 7.3 Skill-by-skill production manifest — no omissions

Reconcile the current authoritative skill catalog, all existing skill prefabs and their actual audio references. The inspected baseline contains 120 skills/prefabs; use the current count if it legitimately changed before execution. Every skill receives a reviewed, improved presentation profile and native playback evidence.

For each skill record:

`skillId; displayName; element; kind; behavior; actual target; unlock/rarity role; prefab path/GUID; duration; preparation/release/contact/recovery points; charge/release/impact/block/recovery clips; persistent-status association; legal variations; gain/pitch; voice/priority/cooldown; VFX anchor/layers; camera policy; reduced-motion/flash behavior; cancellation; source/provenance; test and audition evidence`.

An inapplicable phase must be explicitly documented as inapplicable, not hidden as a missing asset. Shared elemental layers are acceptable for cohesion, but each skill needs a meaningful unique envelope, rhythm, signature or construction. Do not create 120 identical renamed effects or indiscriminately require 600 unrelated new files merely to hit a count.

### 7.4 Preserve the real phase and timing contract

At the inspected baseline:

- `BattleSkillPresentation._cues[0]` = charge.
- `_cues[1]` = release.
- `_cues[2]` = impact.
- `_cues[3]` = block.
- `RecoveryCue` is separate.
- Presentation duration is clamped to 1–1.6 seconds; authored normalized landmarks govern release/contact/recovery.
- `BattleCinematicPlayer` already has a local impact hold and generation-safe reset/cached instances.

Design improved clips to these **existing** timings and actual playback order. Preserve phase-index semantics, target selection and normal encounter pacing. Do not add a multi-second intro to every action, alter global `Time.timeScale`, delay save commits or make a sound callback apply damage. A proposed longer cinematic must be separately justified and cannot silently bypass existing duration/tests.

Where an existing cut-in is applicable, improve it without blocking responsiveness or repeating an ultimate spectacle for every minor move. Keep brief ordinary casts and richer high-tier presentation. Preserve interruption, reduced-motion and already-supported skip policies; do not make the first story skippable as an unrelated convenience.

Synchronize animation, VFX emissions, projectile movement, impact transient, actor reaction and camera response from **one presentation timeline**. Do not trigger the same sound from both an Animator event and the cast controller. Validate low-frame-rate crossings so a phase fires once even when a frame skips over its threshold.

### 7.5 Elemental sound and VFX vocabulary

| Element | Original acoustic/visual materials | Avoid |
|---|---|---|
| Land | Roots, bark, earth pressure, stone grit, grounded rings, organic thumps | Giving every grass/root skill a rock explosion |
| Water | Fluid pressure, droplets, flowing resonance, ripples and smooth ribbons | Constant loud surf or identical splash on every action |
| Fire | Ignition, air intake, ember crackle, controlled flame burst and warm light | Harsh broadband noise covering the whole cast |
| Air | Pressure shifts, airy sweeps, spirals and sharp directional releases | Excessive hiss or camera movement that hides contact |
| Electric | Arc snaps, brief tonal tension, crackle, branching light and thunder body | Sustained piercing tones, uncontrolled strobing |
| Ice | Crystal growth, frost tension, glass-like fracture, restrained shards | A loud brittle shatter on every buff/heal |
| Light | Bell-like purity, radiant bloom, shimmering harmonics and luminous pulses | Thin, painfully bright chimes with no body |
| Dark | Shadow suction, low spectral resonance, subdued distortion and dark trails | Constant sub-bass or horror noise unrelated to the move |
| Poison | Viscosity, bubbling/corrosion, organic tension and readable toxic mist | Gross or noisy textures that overwhelm the game's tone |
| Psychic | Spatial displacement, tuned pulses, crystalline resonance and unusual arcs | Random pitch sweeps with no relation to target/contact |

Within each element, vary direct, ranged, tactical, support and ultimate signatures according to the existing skill metadata. Larger visual scope does not create area-of-effect mechanics where the game has only one target.

### 7.6 Skill classes and persistent effects

**Attacks:** Distinguish melee movement, projectile travel, piercing/slashing/crushing behavior, critical contact and actual blocking. Keep transient, body and tail layers controlled. Use `LastPlayerShieldAbsorbed` / `LastEnemyShieldAbsorbed` or an equivalent verified result, not simply zero HP damage, to decide that a shield actually absorbed an attack.

**Shield:** Play an activation cue, keep a subtle visible shield while the real shield state remains active, give a controlled block reaction when it absorbs an actual hit, and expire it when shield strength/turns reach the model's conditions. The current model has shield strength and shield turns. A hypothetical “four blocked attacks” effect is valid only if an actual current skill implements that rule; do not invent one.

**Buff/debuff:** Show correct actor/target, polarity and status lifetime. Read actual status duration/state through typed access, not parsing description/status-summary text. An ongoing effect must not re-trigger activation every refresh. Reapplication/refresh/stacking must match the model exactly.

**Healing, cleanse, drain, poison and other behaviors:** Use their actual definitions; do not fabricate a separate healing skill class if healing is represented by an existing behavior. Reflect confirmed healing/cleanse/status ticks without modifying their amounts or frequency.

**Passive:** Show activation when the real passive condition triggers. Do not add continuous audio just because a passive exists in the skill description. Limit sustained sonic layers to a low, intentional budget; multiple active statuses can be visually represented without several competing hums.

Persistent effects are **not owned by the transient cast reset**. Use separate actor/status-bound presentation handles, keyed to encounter generation, actor and status. They must survive a subsequent cast when the model says the status survives, and clear on expiry, cleansing, defeat, capture, retreat, encounter replacement, scene unload or disable. Rebuild the visible state from a resumed battle snapshot without replaying acquisition cues or consuming charges.

The game resolves accepted commands before playing their presentation. Follow verified player/enemy action-phase snapshots so persistent effects do not prematurely show the final end-of-turn state during an earlier animation. If required intermediate status data is unavailable, add a narrowly scoped read-only presentation snapshot adapter with tests; never change combat resolution or save schema to simplify a VFX timer.

### 7.7 Audio mixing, lifetime and replacement policy

Preserve the existing three independent phase voices or replace them only with a tested bounded equivalent. Never change the pitch of a shared source while another phase is playing. Keep result/UI voices independent from cast cleanup. A discarded old coroutine must not stop a newer cast, song or status loop.

On a major impact, briefly duck **music**, not every bus indiscriminately. Provide a configurable strength/duration; avoid pumping on every particle. Stop tails and loops intentionally at interruption boundaries, with short fades where safe. App pause, global mute, volume zero and device interruption must silence the appropriate sources immediately, including sources configured to ignore listener pause.

For revised clips, choose either in-place content replacement with stable GUID/import metadata and recoverable originals, or new versioned assets with explicit reference remapping. Do not delete legacy assets until reference coverage and rollback are verified. Guard old sound/VFX generators so a later broad builder cannot silently overwrite curated improvements. Preserve existing package dependencies unless a proven need is separately authorized.

Use subtle presentation-only randomization; never mutate combat RNG. Pool reusable effects and respect the current cache budget unless profiling justifies a change. No unbounded ParticleSystem/AudioSource creation, never-ending coroutines or persistent effects attached to a reused wrong monster.

### 7.8 Concrete Stage 3 tasks and gates

| Task | Work | Evidence |
|---|---|---|
| V01: Quality baseline and profiles | Record migrated screenshots/cast recordings and define editable camera/VFX/SFX profiles | Before/after reference set and parameter manifests |
| V02: Representative skill pilot | Improve one direct, one ranged, shield, buff, debuff/tactical, healing-like behavior if present, and ultimate | Actual audio audition, native captures, target/phase/cancellation tests |
| V03: Full skill library | Apply validated approach to every skill, preserve individual identity | Full skill matrix; every binding valid; no unreviewed placeholders |
| V04: Persistent status layer | Implement read-only actor/status presentation and bounded loops | Expiry, block, refresh, cleanse, death, scene change and save-resume tests |
| V05: Worlds and battle presentation | Polish ten worlds and existing arenas/cameras/actors | Same map IDs/routes; responsive readable compositions; device profiling |
| V06: UI/progression polish | Refine stable prefabs, buttons, transitions, XP and evolution presentation | Visual hierarchy/input checks; no doubled semantic sounds |
| V07: Combined audio/visual integration | Balance music/UI/world/skill buses, all accessibility modes | Phone/headphone mix recordings, frame-time/memory/thermal results |

The pilot sets a quality bar, not permission to leave the remaining library unchanged without review. Preserve an already-good layer when replacing it would worsen the skill, but improve and validate the complete profile rather than changing files merely for activity.

**Gate G3:** Every current skill has verified original suitable SFX and corresponding VFX/animation synchronization; all ten worlds and affected UI are polished without changing gameplay. Sustained statuses match actual state, cleanup is correct, accessibility remains usable, and device budgets are met or the phase is explicitly blocked.

## 8. Stage 4 — Production QA, Android build and GitHub publication

**Objective:** Qualify the integrated game and publish the exact tested signed APK—not an old artifact or an unverified rebuild.

### 8.1 Whole-game QA and bounded fixes

Audit all enabled scenes and gameplay systems, not only changed files. Cover fresh and returning users, irreversible character/starter selection, introduction/tutorial, Home/collection/rest, Codex/learning/equipment, every realm, branch travel, quests/puzzles, inventory/shop, all encounter types, capture, defeat/recovery, growth/evolution, guardian unlocks, legendary investigations, Tower, superboss, audio, graphics, settings and lifecycle behavior.

Classify findings as critical, major, moderate or minor, with reproduction, expected/actual result, source location, scope and evidence. Prioritize data loss, crashes, progression blockers, duplicate transactions, bad signing, broken navigation/audio and unacceptable performance. Fix new regressions and bounded reproducible bugs; do not use QA as a license to redesign balance or remove systems. A larger unrelated defect may block release and require a separately scoped decision.

Run complete EditMode, PlayMode and tooling suites on the **final integrated candidate**. Historical passes and focused reruns do not replace a fresh complete run. Never remove/disable tests to manufacture success. Update a test only when it asserts superseded presentation structure, explaining the reason while preserving its behavioral contract. Prior baseline failures remain failures; any release-critical failure blocks publication even if it predates this task.

Repair loop: reproduce → smallest scoped hypothesis/change → focused check → related regression → evidence review. After three unsuccessful attempts at the same blocker without measurable progress, stop that path, restore a verified state and report the diagnosis rather than cycling indefinitely. Stop immediately for possible data loss or integrity compromise.

### 8.2 Mobile performance and acoustic qualification

Identify actual test devices, Android versions, RAM/GPU, resolution, graphics API and thermal conditions. Do not certify an unknown “low-end” tier based only on an emulator or a desktop Unity window.

Proposed targets, to be recorded against named devices during Stage 0 and verified here:

- Sustained 30 FPS on the selected supported lower-end device; target 60 FPS on an appropriate midrange/higher device. Report frame-time percentiles and separately identify loading/transition spikes.
- No new crashes, ANRs, lost touches, broken resume, audible buffer underruns or repeated effect-induced stalls during a 30-minute mixed exploration/combat run.
- No avoidable per-frame managed allocations in warmed-up routing/stable UI/status-effect paths; report measured allocations rather than claiming the whole engine allocates zero bytes.
- Pools/caches remain bounded and memory reaches a stable plateau after repeated menus/casts; compare before/after 100 modal cycles and repeated encounter transitions.
- Investigate >10% unexplained frame-time or resident-memory regressions on comparable fixtures. Authorized extra assets may require a documented budget tradeoff; do not quietly weaken the acceptance criteria.
- Long music does not preload the entire soundtrack; all buses retain mix headroom; phone speaker and headphones reproduce important effects without clipping, harshness or masked gameplay cues.

Test cutouts/safe areas and at least 320×568, 360×640, 390×844, 412×915, 768×1024, 1080×1920 and 1080×2400. Preserve portrait behavior and validate graceful layout in wider Editor hosts where the existing project supports them.

### 8.3 Signing and version preflight — fail closed

Before invoking `tools/build-android.ps1`:

1. Re-read the current runner and `Editor/AndroidReleaseBuild.cs`. The baseline runner can create a new keystore; **do not allow that branch for this established application**. Use a preflight wrapper or reviewed narrow guard that fails before key creation if either retained signing file is absent.
2. Locate the established `%LOCALAPPDATA%/Aevareth/Signing/aevareth-release.jks`, alias `aevareth-release`, and its DPAPI password file under the authorized Windows identity. Never echo passwords, pass them visibly in command lines, commit them, bundle them or upload them. Do not include them in generic project backups delivered to GitHub.
3. Confirm the certificate against the last trusted published APK and retained release record. The inspected docs record SHA-256 `7fe2b9cf6560807cae2024d2118c22a345ac22ef1e2d0c62e61052ca2784aeb3`; verify the actual certificate rather than trusting only this text.
4. If the retained key cannot be recovered safely, report a release blocker. Do not substitute debug signing, a new key, a new package name or an uninstall/reinstall instruction as proof of update compatibility.
5. Query current releases/tags plus local/documented shipped builds. Choose a meaningful next unused version and a strictly increasing Android version code above every known release candidate intended for upgrade. The historical local `1.0.1` code 2 matters even though only `v1.0.0` was returned by the release API during this audit.
6. Preserve application ID `com.curib123.aevarethmonster`, existing save locations/production identity and portrait settings. Baseline target is API 26 minimum / target 36, ARM64 IL2CPP, non-development APK. Verify the installed supported toolchain; do not silently raise minimum requirements or produce only an AAB.

### 8.4 Exact-source candidate and build

- [ ] Prepare scoped tested changes, final version configuration and durable release documentation. Review `git diff` and stage explicit paths, not every local file. Keep AI plans, fixtures, credentials, logs and APKs out of source commits.
- [ ] Create the final local candidate commit under the permitted `main` workflow and record `RELEASE_SHA`. This commit, not the moving branch name, identifies the build source.
- [ ] Create a fresh isolated build/validation copy from that commit, with resolved LFS assets. Record SHA-256 inputs for `Assets`, `Packages`, relevant `ProjectSettings` and approved build-tool files.
- [ ] Apply only documented validation identity and release-build overrides in the isolated copy. The existing release builder then sets production company/product/package. Record these controlled overrides; do not claim byte-identical settings when they intentionally differ.
- [ ] Close that validation Unity instance before batch building. Do not run simultaneous editors/builders on the same project or destroy unsaved scenes to acquire the lock.
- [ ] Run the existing Android pipeline with explicit version/code and fresh output/evidence paths. Check native process exit status, `BuildReport`, error log, receipt and resulting file; an APK filename alone is not a successful build.
- [ ] Verify APK signature/certificate, package/version/min/target SDK, ARM64 native contents, development/debug flags, ZIP CRC, native-library and APK alignment, source input identity, assets and cue packaging. Test 16 KB compatibility as required for supported devices; APK ZIP alignment and ELF segment alignment are separate checks. [T3]
- [ ] Install on real supported devices and upgrade over the trusted prior release using disposable test profiles, without uninstalling to hide a signature/save problem. Verify save retention, startup, all key gameplay flows, audio, touch, pause/resume, screen lock, app interruption and performance.
- [ ] Calculate SHA-256 only after the final signed APK is fixed. Any change affecting build inputs creates a new candidate commit/build and invalidates prior affected acceptance evidence.

### 8.5 Source integration and release publication

Git publication is authorized **after gates pass**, using existing permissions and repository protections. It is not authorized to bypass them.

1. Recheck remote `main`. Push validated commits with a normal fast-forward workflow only. If concurrent remote work makes the candidate stale, reconcile without overwriting others and revalidate the resulting source before publishing. If branch protection prevents the authorized workflow, report the blocker; do not create unauthorized branches or bypass rules.
2. Verify `RELEASE_SHA` is the exact tested commit now present on the permitted remote history. Never tag moving `main` merely because it currently looks correct.
3. Confirm the release tag is unused. Create an annotated tag on `RELEASE_SHA` and push that exact tag, or use an equally verified API workflow. Never overwrite an existing tag or release asset silently.
4. Create a **draft** release in `curib123/aevareth_monster`, upload the signed APK, `SHA256SUMS.txt`, a redacted release manifest and QA summary, and add accurate release notes. Draft state is a staging step, not the final deliverable.
5. Download the draft asset using authorized access to a new verification location and compare SHA-256/size to the local qualified APK. Verify the remote tag resolves to `RELEASE_SHA`, including annotated-tag dereferencing.
6. Publish the release only after upload/integrity checks succeed. Query it again and verify it is no longer a draft, its assets are present, and the published APK can be downloaded and matches the checksum.
7. Preserve the repository's visibility. A private-repository release remains accessible only to authorized users; do not make the source public or create another public repository without explicit approval.
8. If upload or publication fails, report actual state and leave verified local artifacts/a safe draft for resume. Do not claim publication from the presence of a local APK or from a source tag alone.

**Illustrative PowerShell commands for the executing agent after all variables and gates are verified:**

```powershell
# $Repo, $ReleaseSha, $Tag, $Version, $Apk, $Checksums,
# $ReleaseManifest, $QaSummary and $ReleaseNotes must be resolved from
# the verified candidate and manifest, not guessed or left as placeholders.
# Check $LASTEXITCODE after EVERY native command; stop on nonzero.

git tag -a $Tag $ReleaseSha -m "Aevareth: Monster Realm $Version"
git push origin "refs/tags/$Tag"

gh release create $Tag $Apk $Checksums $ReleaseManifest $QaSummary `
  --repo $Repo --verify-tag --draft `
  --title "Aevareth: Monster Realm $Version" --notes-file $ReleaseNotes

# Verify remote tag, download draft assets to a fresh directory,
# compare checksums, then publish only on successful verification.
gh release edit $Tag --repo $Repo --draft=false

gh release view $Tag --repo $Repo `
  --json url,tagName,isDraft,isPrerelease,targetCommitish,assets
```

These commands illustrate publication, not building or qualification. `--verify-tag` checks that a remote tag exists; it does not prove the APK was built from it. The manifest/tag/input audit establishes that relationship. GitHub CLI supports explicit draft creation and later publication; verify actual command availability in the installed CLI. [T4–T6]

### 8.6 Release package and notes

Upload `Aevareth-<version>-arm64.apk`, `SHA256SUMS.txt`, `release-manifest.json`, and a concise durable QA summary. Release notes must describe migration, music, non-skill SFX, original cinematic skill SFX, visual improvements, compatibility, minimum requirements, real tested devices and known limitations. List conditional/reserved music honestly; do not advertise an unimplemented credits screen.

Manifest fields: version/code, exact source SHA/tag, build-input manifest hash, APK name/bytes/SHA-256, signing certificate fingerprint, Unity/SDK/NDK/backend/architecture, build overrides, test-result file hashes, device IDs/models/OS in a privacy-safe form, audio/skill coverage totals, provenance summary and known issues. Exclude secrets, real player data and unredacted private logs.

**Gate G4:** Required tests and device/acoustic checks pass; no unresolved critical/major release defect; exact-source signed APK passes upgrade/integrity checks; protected assets/gameplay remain compatible. Missing device or listening evidence blocks a production-ready claim and production publication; do not silently downgrade to a prerelease. A different distribution standard needs an explicit user decision.

**Gate G5:** Authorized scoped source push, exact commit tag, published release, uploaded/download-verified APK and checksum all confirmed. Only then report the full task complete.

## 9. Acceptance tests and release gates

Extend the existing test assemblies and tooling; do not replace their coverage with a new superficial smoke suite. Existing relevant families include `RealmUiContractTests`, `RealmUiAuthoringAuditTests`, `PortraitResponsiveLayoutTests`, `AevarethUiBindingTests`, `Commerce*Tests`, `FirstJourney*Tests`, `RealmBattleStorageTests`, `NativeSkillAudioTests`, `NativeSkillVfxTests`, `SkillSequenceTests`, `BattleSoundMixTests` and native `AdventureFlowTests*`. Verify actual paths/names in the current checkout before running filters.

The following are **new required test contracts**, not assertions that these tests already exist or pass. Put them into focused EditMode/PlayMode classes under the established `Tests/` directories. Each implementation task should add its relevant failing test first where feasible, then record focused and integration results.

| Test contract | Required assertion |
|---|---|
| `Authoring_InspectorEditsSurviveLifecycle` | Edit authoritative layout/style, save/reopen, enter/exit Play; value and intended responsive behavior survive |
| `Authoring_PreviewNeverUsesProductionSave` | Preview opens with no production AppRoot/save writes, cleans up, and does not dirty original assets unexpectedly |
| `Authoring_RuntimeUsesSerializedHierarchy` | Migrated fixed views use valid authored refs; 100 reopen cycles do not construct duplicate shells/listeners |
| `Authoring_SkinDoesNotEraseAuthoredOverrides` | Runtime theme/skin/layout respects defined style ownership and expected states |
| `Assets_ProtectedIdentityGraphPreserved` | Scene indices/GUIDs, protected monster/data hashes and Resources paths match; intentional ref remaps are complete |
| `Music_AllTenActiveWorldIdsResolve` | One correct world cue for each actual active field; locked/hovered selection never switches it |
| `Music_ActualStartupAndOverlayRouting` | Character-first startup, returning journey, atlas/field, Home/Codex and modal inheritance match actual state |
| `Music_EncounterPrecedence` | Verified stable special IDs override legendary/Boss/Trainer/Wild without display-name guessing |
| `Music_IdenticalRequestsDoNotRestart` | Repeated same-context refresh leaves playback position and transition count stable |
| `Music_StaleTransitionCannotWin` | Rapid navigation cancels old requests; one selected context owns music after the fade |
| `Music_IntroUsesPresentationClock` | Intro audio follows real elapsed/blocked/pause/retry states; 47.2 seconds is the current default, not an assumed wall-clock deadline |
| `Audio_LegacySettingsAndImmediateMute` | Existing keys preserve semantics; every active bus responds immediately and resume cannot override user mute |
| `Audio_SemanticCueExactlyOnce` | Accepted purchase/capture/quest/result gets one intended cue; retries, failed saves and data rebinds do not double it |
| `Audio_PresentationDoesNotConsumeCombatRng` | Same deterministic actions/time fixtures produce the same domain results with audio on/off and variant randomization |
| `Audio_NoAdditionalSaveSideEffects` | Audio/preview adds no domain mutation; existing Home rest/recovery transactions remain equivalent under controlled time |
| `Skills_AllIdsHaveValidProfiles` | Every current skill ID resolves to the right prefab, phases, target, original audio assets and verified profile |
| `Skills_ExistingCueIndexContractRetained` | Charge/release/impact/block/recovery mapping remains correct; a support action is not given a fake enemy hit |
| `Skills_PhasesFireOnceAcrossFrameSkips` | Crossing thresholds at low frame rate triggers each applicable event once and in order |
| `Skills_ActualBlockAndStatusLifetime` | Actual absorption, shield strength/turns and status state drive visuals/audio; no invented four-hit or timer rule |
| `Skills_TransientResetDoesNotKillPersistentStatus` | Starting/ending a cast cannot incorrectly remove a surviving status; expiration/cleanse removes it correctly |
| `Skills_OldGenerationCannotStopNewCast` | Canceled iterator/cleanup cannot stop a newer cast or unrelated UI/music |
| `Skills_ResumeDoesNotReplayActivation` | Mid-battle restore reconstructs current presentation without consuming uses or replaying acquisition sounds |
| `Gameplay_SavesAndTransactionsUnchanged` | Fresh, all supported legacy versions, corrupt/future saves, interrupted battle, reward receipts, equipment and evolution behave as before |
| `Presentation_ResponsiveAndAccessible` | Safe areas, touch targets, focus, reduced motion/flash and critical readability remain correct |
| `Runtime_PoolsRemainBounded` | Warmed repeated menus/casts/transitions leave stable object/listener/source counts and no unbounded memory growth |
| `Release_KeyMustAlreadyExist` | Missing key/password/certificate mismatch fails before build-runner key generation; no debug/new-key fallback |
| `Release_BuiltInputMatchesTaggedCommit` | APK input manifest and controlled build overrides match exact tagged source; dirty/unrecorded source cannot pass |
| `Release_DownloadedApkMatchesQualifiedArtifact` | Downloaded published APK SHA-256 and size equal the final qualified local file |

### Required manual/native evidence

Automated checks supplement—not substitute for—actual rendered UI inspection, in-game audio listening, device installation/upgrade, touch/lifecycle testing and performance profiling. Record dates, input/candidate SHAs, commands/tool actions, exit codes, counts, logs/XML, screenshots, recordings, device details, and reviewer observations.

All skills need binding and native playback coverage; use a controlled harness for exhaustive skill presentations without rewriting gameplay. Device performance should include worst-case effects and representative direct/ranged/support/ultimate cases from all ten elements. A test harness recording is not falsely labeled a normal player journey.

### Gate summary

| Gate | Pass means | Blocking condition |
|---|---|---|
| G0 | Source, ownership, tools and baseline protected/verified | Incomplete native audit, unresolved asset access, unsafe save/editor target |
| G1 | Full prefab migration with parity and editable authoritative layouts | Broken refs, design drift, duplicate handlers or persistence changes |
| G2 | Original BGM/non-skill assets and routes integrated/auditioned | Placeholder/missing clips, no audition evidence, duplicate/incorrect music |
| G3 | Original improved skill SFX and visual polish with correct mechanics | Unreviewed skill profiles, stale statuses/audio, timing or performance regressions |
| G4 | Final source-qualified signed APK passes full release acceptance | Missing signing/device/audio evidence, wrong source/version, critical/major defect |
| G5 | Verified APK/checksum published to the exact-tag GitHub Release | Draft-only release, upload failure, hash mismatch or inaccessible asset for authorized account |

## 10. Resume, reporting and final deliverables

### Execution ledger

Maintain one active ledger under `docs/gpt-plans/` with task IDs `0.1–0.3`, `M01–M10`, audio subtasks, `V01–V07`, release subtasks and `G0–G5`. Use honest states:

`NOT_STARTED`, `IN_PROGRESS`, `IMPLEMENTED_UNVERIFIED`, `VERIFIED`, `BLOCKED`, `PUBLISHED_VERIFIED`.

For each task store input SHA, current candidate SHA, owned paths, baseline/checkpoint identifier, manifest diff, tests and evidence paths, asset-audition status, unresolved risks and exact next action. Never replace earlier failed evidence with a false green summary. A file existing or code compiling does not promote a task to `VERIFIED`.

Before resuming after interruption, re-read the ledger and current `AGENTS.md`, check HEAD/dirty files and MCP instance, confirm artifacts/checkpoints still exist, and revalidate changed assumptions. Resume at the first unverified dependency. Do not repeat expensive whole-project analysis when the input SHA and completed evidence are unchanged; do not skip it when they have changed.

At a session/tool limit, finish a safe bounded operation, leave a precise checkpoint and report the next action. Do not promise background work or future completion without an actual execution mechanism. Do not start a destructive operation just to appear to finish a stage.

### Deliverables

- Migrated, editable scenes/prefabs and preview tools, with unchanged game/domain contracts.
- Original music library: ten world themes, actual menu/Home/atlas/battle contexts, timed story score and stingers; conditional reserve cues clearly labeled.
- Reviewed 17 legacy UI cue IDs, new/reconciled non-skill families, ambience and backward-compatible volume controls.
- Complete per-skill manifest and improved original skill sound/visual profiles for every current skill, including actual persistent-status behavior.
- Reproducible source/provenance/rights inventory, loop metadata, audio masters/sources actually produced, and editable Unity profiles.
- Full test evidence, native screenshots/recordings, device/acoustic/performance reports, protected-input diffs and rollback records.
- Scoped verified commits pushed through the permitted workflow; no planning files, APKs or secrets committed accidentally.
- Signed production APK, checksum, redacted release manifest, QA summary and published GitHub Release tied to the exact tested commit.

### Final response from the executing agent

Report the real result, not a promotional summary. Include:

1. Gate/task status and remaining blockers or known limitations.
2. Final source SHA, pushed branch and release tag.
3. Release page and APK asset URLs, publication state, APK bytes and SHA-256.
4. Certificate fingerprint, package/version/code and actual tested Android requirements/devices.
5. New test results, not historical counts; links/paths to logs, captures and audible review evidence.
6. Actual integrated/conditional music counts, non-skill cue coverage and per-skill coverage.
7. A concise statement of preserved gameplay/save identities and intentional audio/visual changes.

Do not state “production-ready,” “all passed,” “fully tested,” “original audio created,” or “APK published” unless the corresponding evidence exists. When blocked, deliver verified artifacts/status without pretending the final release goal was reached.

## 11. Source register and engineering references

### Repository evidence

The repository paths below refer to the inspected commit, not an assumed future state. Pinned snapshot: [9c067d29cde664061853f3a41a647fb237cebde3](https://github.com/curib123/aevareth_monster/tree/9c067d29cde664061853f3a41a647fb237cebde3). The executing agent must inspect the current equivalents if HEAD changes. Earlier full tree/file-count observations and additional source-path findings came from the two supplied static plans at this same commit; they are not substituted for Stage 0 native coverage.

- **R1 — Repository rules:** `AGENTS.md`; `main`-only development, validation copies, canonical monster protection, ignored planning directory.
- **R2 — Current project context:** `Assets/_Aevareth_Monster_Realm/Docs/UnityProjectContext.md`; newest sections supersede historic Farm/title-first/free-capture notes.
- **R3 — Version/packages/scenes:** `ProjectSettings/ProjectVersion.txt`, `Packages/manifest.json`, `ProjectSettings/EditorBuildSettings.asset`.
- **R4 — Migration owners:** `Runtime/UI/CommerceHost.cs`, `SkillCardPanel.cs`, `GildedLayout.cs`; supplied migration audit additionally covers Inventory/Journal/Rest/World/collection owners named in this file.
- **R5 — UI audio:** `Runtime/UI/Theme/AevarethUiAudio.cs`, `AevarethUiRuntime.cs`, `AevarethUiPreferences.cs`, `AevarethButtonFeedback.cs`, `AevarethUiTheme.cs`, `Resources/Aevareth/UI/AevarethUiTheme.asset` and `Audio/UI/`.
- **R6 — Battle authority/presentation:** `Runtime/Adventure/BattleState.cs`, `BattleSkill.cs`, `WorldSession.BattleCommands.cs`, `Runtime/UI/BattleSkillPresentation.cs`, `BattleCinematicPlayer.cs`, `BattleSoundMix.cs` and `SkillVfxLayer.cs`.
- **R7 — Lifecycle and save behavior:** `Runtime/UI/HomeScreen.cs`, `JourneyIntroductionView.cs`, `FirstJourneyFlow.cs`, `WorldUnlockReveal.cs`, `ProgressionSequenceController.cs` and Core startup routes.
- **R8 — Guarded authoring:** `Editor/CommerceSceneBuilder.cs`, `RealmAdventureSceneBuilder.cs`, `RealmValidationPipeline.cs` and existing skill/audio builders.
- **R9 — Release pipeline:** Root `tools/build-android.ps1`, `Assets/_Aevareth_Monster_Realm/Editor/AndroidReleaseBuild.cs`, `docs/android-release.md`, current GitHub releases/tags.
- **P1 — Supplied migration specification:** `AEVARETH_EDITOR_FIRST_MIGRATION_MASTER_PLAN(3).md`, identical named copies also supplied. Its preservation/migration requirements are incorporated; obsolete limited-approval instructions are explicitly superseded.
- **P2 — Supplied music specification:** `AEVARETH_MEDIEVAL_MUSIC_AND_SFX_MASTER_PLAN.md`. Its original 31-cue slate, ten-world identity and non-skill coverage are incorporated. The former permanent skill-SFX exclusion is explicitly superseded for Stage 3.

### Technical references checked for this handoff

Use installed-version documentation and current distribution requirements during implementation; references are engineering support, not evidence that this game was tested.

- **T1:** Unity Audio Clip Import Settings: https://docs.unity3d.com/6000.0/Documentation/Manual/class-AudioClip.html
- **T2:** Unity `AudioSource.PlayScheduled`: https://docs.unity3d.com/6000.0/Documentation/ScriptReference/AudioSource.PlayScheduled.html
- **T3:** Android native page-size compatibility and testing: https://developer.android.com/guide/practices/page-sizes
- **T4:** GitHub CLI release creation/draft/verified-tag options: https://cli.github.com/manual/gh_release_create
- **T5:** GitHub CLI release editing/publication: https://cli.github.com/manual/gh_release_edit
- **T6:** GitHub CLI release download/metadata checks: https://cli.github.com/manual/gh_release_download and https://cli.github.com/manual/gh_release_view
- **T7:** OpenAI Codex MCP documentation entry point: https://developers.openai.com/codex/mcp — confirm the installed client's actual configuration/capabilities rather than assuming a connection.

## 12. Copy-and-paste execution prompt

Paste the following into the **local Codex session with the repository and running Unity MCP available**, and attach/provide this one Markdown file. This invokes the complete specification; no older planning attachment is necessary.

```text
Read AEVARETH_COMPLETE_PRODUCTION_MASTER_PROMPT.md completely and use it as the
single controlling specification for this Aevareth: Monster Realm task.

Repository: https://github.com/curib123/aevareth_monster.git

I authorize the full scoped implementation, original asset creation, testing,
normal main-branch source integration, signed Android build, and final GitHub
APK release described in the file. This supersedes the older planning-only,
Phase-0/1-only, permanent skill-SFX-exclusion and separate-publication-approval
instructions for this task. It does not waive safety or release gates.

First read current AGENTS.md, verify the real local/remote source state, Unity
version, LFS assets and correct Unity MCP validation instance, and perform the
full repository/native ownership audit. Do not rely on historical test passes.
Preserve unrelated dirty work, production saves, canonical monster assets,
scene/GUID identities, gameplay rules and the established signing certificate.

Execute in order:
0. Full audit, capability verification, protected baseline and checkpoints.
1. Complete Editor-first prefab migration with appearance/audio parity.
2. Original medieval music for all ten worlds and actual game states, ambience,
   Audio Director/mixer, and complete non-skill SFX integration.
3. Graphics/animation/camera/VFX polish and improved original cinematic skill
   SFX for every current skill, inspired by fantasy-anime impact and magic but
   never copied from existing anime. Bind persistent effects to real battle state.
4. Full QA, acoustic and physical Android validation, exact-source signed APK,
   scoped normal push/tag, and verified GitHub Release publication.

Continue after passing gates without asking for routine phase approval. Use
recoverable task-sized changes and real Unity/audio/device evidence. Never
force-push, bypass builder guards, generate a replacement signing key, invent
missing tools/assets or publish a failing/untested production APK. If a mandatory
prerequisite is unavailable, preserve verified work, mark the affected gate
blocked and report the precise next action; do not silently skip it.

Maintain the resumable ledger in ignored docs/gpt-plans/. Resume from verified
checkpoints rather than repeating completed work. Finish by reporting the real
release URL, source SHA/tag, APK SHA-256, test/device/audio evidence and remaining
limitations. Begin with Stage 0 now; do not stop at another generic proposal when
safe implementation can proceed.
```

---

**Definition of done:** The existing game is preserved and enhanced, the required evidence has passed, and the exact verified signed APK plus checksum is available from its confirmed published GitHub Release. Until then, report the precise partial/blocked state rather than asserting completion.
