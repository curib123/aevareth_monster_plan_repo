# Aevareth: Monster Realm — Editor-First, Prefab-Based UI Migration Master Plan

**Plan status:** Proposal only; no code, scene, asset, commit, tag, or save changes made.  
**Source repository:** `curib123/aevareth_monster` (`main`)  
**Baseline inspected:** `9c067d29cde664061853f3a41a647fb237cebde3` (commit time 2026-10-25 22:54:32 UTC; 2026-10-26 in Manila)  
**Editor baseline:** Unity `6000.5.6f1`, URP `17.6.0`, uGUI `2.5.0`.

## Executive decision

Migrate **presentation authoring, not gameplay ownership**. Save persistent and reusable visual structures into existing `.unity` scenes or `.prefab` assets, referencing them through serialized, Inspector-visible fields. Keep runtime instantiation only for legitimately variable data (owned monsters, quests, map markers, item entries, skill effects, notifications), created **from authored template prefabs**, never by rebuilding the complete visual hierarchy from procedural C# every time.

The desired results are: (a) permanent layout visible and editable in Scene and Prefab modes while not playing; (b) usable mock previews for dynamic states without touching player saves; (c) existing game looks and plays the same; (d) all persistence, asset identities, and gameplay semantics remain intact; (e) retained native and mobile validation evidence passes.

**No zero-risk guarantee:** treat any untested conversion as incomplete. Perform the migration as a succession of reversible slices, with baseline tests and screenshots, not a one-shot rewrite. Do not publish a release until acceptance gates are satisfied.

## 1. Observed repository architecture and limits

A recursive GitHub tree of this exact commit contains **5,722 tree entries**, including **367 `.cs` files**, **eight `.unity` scenes**, and **139 `.prefab` files**: **120 existing skill-effect prefabs**, **16 UI prefabs**, **two Resources UI prefabs**, and **one AppRoot prefab**. `ProjectSettings/EditorBuildSettings.asset` enables seven scenes in order: Bootstrap, Onboarding, Character Creation, Starter Selection, Home, World Map, Battle. `Scenes/Monster Codex/Monster Codex.unity` exists but is not in the enabled build list: treat as legacy/retained until runtime routing is verified; do not delete or re-enable reflexively.

Relevant authoring/data roots:

- `Assets/_Aevareth_Monster_Realm/Scenes/` — canonical serialized scenes; Home and World Map YAML files are especially large (~9.9 MB and ~10.8 MB). **Do not wholesale regenerate them.**
- `Assets/_Aevareth_Monster_Realm/Prefabs/UI/Components/` — editable card, panel, button, slot, tab and modal prefab templates.
- `Assets/_Aevareth_Monster_Realm/Prefabs/Skills/` — 120 authored skill prefabs with phases, VFX and sound wiring; **preserve, do not recreate**.
- `Assets/_Aevareth_Monster_Realm/Resources/Aevareth/UI/` — `AevarethUiTheme.asset`, `CommerceUiTheme.asset`, `FirstJourneyExperience.prefab`, `GildedLoading.prefab`; retain resource paths.
- `Assets/_Aevareth_Monster_Realm/Resources/Aevareth/` — `SkillRunes.asset`, `Adventure/GameBalance.asset`, `Adventure/RealmAdventureCatalog.asset`, `Commerce/CommerceCatalog.asset`; runtime data source must not change as a side effect of presentation refactoring.
- `Assets/_Aevareth_Monster_Realm/Data/Adventure/Maps/` — ten serialized map assets; `Data/Adventure/Monsters/` — fifty species assets. Keep all stable IDs/positions, original enum values, and canonical monster art/GUIDs.
- `Assets/_Aevareth_Monster_Realm/Runtime/Core/` — player profile/startup/save setup; `Runtime/Adventure/` — combat/world/save/domain logic. No modifications planned unless a proven binding-only compatibility shim is strictly required.
- `Assets/_Aevareth_Monster_Realm/Tests/EditMode/` and `/PlayMode/` — existing tests, augment instead of replacing.
- `Assets/_Aevareth_Monster_Realm/Editor/` — numerous explicit authors/builders. Their protections require isolated validation identity and must **not** be bypassed or run in the working project.

**Specific source findings** (static inspection):

1. `Runtime/UI/CommerceUi.cs`: common `Rect`, `Art`, `Text`, `Surface`, `Button`, `Scroll` helpers directly create `new GameObject`, `AddComponent`, and children. This is the root of several uneditable modal layouts.
2. `CommerceHost.cs`: `Prepare()` creates `Commerce Overlay`, portrait frame and page dynamically. `BuildChrome()` creates header/avatar/wallet/bag/gear/dock dynamically. Identity and Settings view content are created on open.
3. `InventoryShopView.cs`: builds inventory/shop page, tabs, scrolling products, details and checkout with dynamic helper calls. Convert permanent panel hierarchy and product-row templates; keep list data dynamic.
4. `BattleItemView.cs`: creates Battle Items/Prism drawer and item rows on open. Convert fixed drawer/controls and introduce serialized item/prism row prefab.
5. `RealmAdventureHost.cs`: `OpenJournal`, `OpenActivity`, and `OpenRest` instantiate new modal roots and their content. `AdventureJournalView.cs`, `AdventureActivityView.cs`, `RealmPanel.cs` create the internal UI programmatically. Convert fixed forms and event bindings while retaining branching activity data.
6. `SharedSettingsView.cs`: builds page, help screen, volume Slider and labels dynamically. Convert reusable, authored settings and identity screen prefabs.
7. `SkillCardPanel.cs`: `Attach` can disable existing child objects, then `EnsureVisuals` creates skill art and labels. `SkillArtworkView.Create` creates rings/discs/icons. **Existing `AevarethCelestialSkillCard.prefab` already serializes these elements**; make serialized prefab the standard binding source and use fallback only for intentional migration/Editor tooling.
8. `CompanionCollectionView.cs` and `CompanionTrainingView.cs`: already instantiate serialized row/skill templates. **Retain** this pattern, improve missing Inspector references and previews rather than freezing the entire collection into the scene.
9. `AdventureFieldView.cs`: instantiates existing stop templates but also constructs some connection trails/captions programmatically. Keep data-driven 1,337 map nodes in catalog, add Inspector-visible marker/trail templates and authoring previews; never place all nodes as permanent scene objects.
10. `PrismIconGraphic.cs` contains procedural element drawing/child generation. Preserve distinct ten-element appearance, create a fully serialized glyph hierarchy or edit-friendly glyph prefab where practical; retain procedural shape rendering only if template controls are exposed and previews work.
11. `GildedLoadingScreen.cs` already loads and instantiates an existing editable prefab from Resources; **leave architecture unchanged**.
12. `NativeSkillVfxSceneBuilder.cs` modifies existing skill prefabs in place and `SkillVfxLayer.cs` applies skill effects. **Do not flatten 120 skills into scene objects**; their Prefab Mode is already editable.
13. Layout scripts such as `GildedLayout.cs`, `PortraitFrame.cs`, `HomeLayout.cs`, `WorldMapLayout.cs`, `OnboardingLayout.cs`, and `HomeHubScreen.cs` use `[ExecuteAlways]` or write RectTransforms in editor/runtime. **Inspector edits can be overridden** by `_placements` arrays and reflow code; layout authority must be resolved before visual migration.
14. `Editor/RealmAdventureSceneBuilder.cs` and `Editor/CommerceSceneBuilder.cs` explicitly save scenes and author UI in a validation copy; they are guarded against execution in the main project. `RealmValidationPipeline.AuthorAll` cascades multiple authoring operations. Never run broad authoring to refresh a single screen.
15. Source documentation indicates the latest world save schema is 13 and profile schema 3, and all ten worlds preserve existing IDs, their order and historic progression. Treat as invariants; verify by running tests, not by trusting documents alone.

**Scope limit:** This is a repository-tree plus targeted code/docs/prefab static audit. Complete Unity object graph deserialization, all asset import results, current EditMode visual states, runtime behavior and physical Android performance **have not been directly verified** in this environment. The first phase below performs that missing native inventory. Large scene files were not fully deserialized here.

## 2. Non-negotiable invariants

**Repository and source:** no destructive cleanup; do not replace scenes wholesale; no unrelated code refactoring; never silently delete/rename `.meta`, source GUIDs, prefabs, generated art, or preserved historical content. Never force-push. Do not create branches/worktrees contrary to `AGENTS.md`. Preserve or recreate temporary isolated validation **filesystem copies** and revalidate the exact candidate commit before integrating.

**Gameplay:** world `WorldSession`/`WorldProgress` save authority, all 10 world IDs and node maps, the numeric `Grass` enum identity shown as Land, all battle/damage/turn/RNG semantics, skills (120), uses, shield duration/charges, capture Prisms, inventory receipts and transactional saves, monster growth/evolution, first-time intro, quests/puzzles/journal, world/map guards, camera, audio and reduced-motion/flash preferences must be identical.

**Data:** world save versions 1–13 supported as before; profile 1–3 supported as before; preserve active, legacy, incomplete and corrupt-save recovery. No migration schema/version bump for a view-only conversion. Do not read/write real `Application.persistentDataPath` saves while testing. Do not replace original signing key outside repo.

**Unity asset and scene identity:** unchanged seven enabled scene paths, indices and GUIDs; preserve eight existing scene files, all 50 monster definitions, ten maps, 1,278 canonical monster art files (per repo delivery record), skill prefab GUIDs, local file IDs where referenced, Resources paths and sprite/theme keys. New prefabs may receive new GUIDs but existing identities may not change unintentionally.

**Visuals and input:** same Gilded Sigil/Celestial visual direction and sprites, same functional labels and 2×2 skill selection with actual use counts; original particle/sound/cut-ins retained; preserve portrait scaling/safe areas, active button focus, Escape/Back handling, gamepad/keyboard/touch actions, modals and screen ordering. Preserve screen reader/accessibility and reduced-motion behavior where implemented.

## 3. Architecture target and authoring contracts

| UI kind | Edit-mode source of truth | Runtime responsibility | Example |
|---|---|---|---|
| Fixed scene structure | Serialized GameObjects/components in original `.unity` file | Set values, visibility, focus and animations | Battle HUD, Home framing, world HUD, common header/dock |
| Reusable screen/modal | Authored prefab with component script and serialized child references | Instantiate/open one prefab, pass session/view-model; close/reuse | Shop, Inventory, Settings, Journal, Activity, Rest, Prisms |
| Repeated data item | Authored **template prefab** | Instantiate/pool N instances and bind their models | Owned monsters, skill slots, shop products, quests, map nodes |
| Skill VFX | Existing 120 skill prefabs | Play effect and parameters via existing presentation code | Charge, release, contact, aftermath, passive/shield effects |
| Truly procedural graphics | Serialized host/component and exposed Inspector parameters | Update geometry/drawing when state changes | Routes, particle arcs, element glyphs where needed |
| Preview fixtures | **Editor-only tools** and deterministic mock data | Never load/save actual player progress | Unlocked quest, captured monster, purchase confirmation, skill 3/5 uses |

For each presenter, serialize typed references using `[SerializeField]`, preserve component public behavior/API, avoid `GetComponentInChildren` by name as routine binding, and separate `Bind(data)` / `Refresh()` / `Open()` / `Close()` from hierarchy creation. Existing fallback factory methods may exist during a short compatibility stage but must not execute for migrated production screens. Fail visibly with a useful missing-reference error rather than silently creating a different UI. Never leave two overlapping hierarchies alive.

**Layout ownership rule:** each component has one authoritative editable layout representation. Prefer existing serialized `GildedLayout` placement pairs where already used, with a custom Inspector/Scene handle that edits those positions; or migrate a scoped component to serialized anchors, LayoutGroups and RectTransforms if equivalence is verified. `ExecuteAlways` may perform preview reflow but must not overwrite user-entered layout values or create/destroy children from `OnValidate`/import. Test changing position while stopped, saving, reopening, pressing Play and stopping, and comparing persistence across all steps.

## 4. Exact implementation sequence and exit gates

### Phase 0 — Baseline freeze, backups and source inspection

**Do:** Verify clean latest `main` checkout, actual Git LFS object availability, Unity version, package import and Console. Record exact commit SHA, worktree status, scene GUID/index hashes, all `.meta` identities, all protected asset SHA-256s, enabled scenes, UI prefab dependency graph and canonical save fixture backups. Snapshot entire project outside working copy; keep original `Assets`, `Packages`, `ProjectSettings`, signing keystore and real saves untouched. Build isolated test filesystem copy with CodexValidation/AevarethExplorationValidated identity and a safe external screenshot/evidence directory. Capture baseline Unity Editor hierarchy and inspector layouts, before/after Play Mode screenshots, native UI navigation, EditMode+PlayMode test results, Windows-player build and Android baseline if toolchain available. Confirm reported prior 1,449 EditMode and 171 distinct PlayMode cases by actual re-runs; do not assume they still pass.

**Exit:** recoverable baseline, all protected hashes/IDs recorded; baseline test failures explicitly classified; no dirty/unsaved active scenes and no player-save contamination.

### Phase 1 — Classify every visual owner (UI manifest)

**Do:** For **all seven build scenes** and the retained eighth Codex scene, inventory Canvas roots, prefab instances, runtime helpers and event handlers; classify every UI element as `authored fixed`, `prefab repeated`, `runtime-built fixed`, `procedural visual`, `editor preview`, or `legacy retained`. Capture `scene path > hierarchy path > serialized component > creator/presenter script > prefab owner > styling/layout authority > runtime data owner > dismissal behavior > editability`. Check 120 skill prefab asset references and compare against catalog skills and existing runtime scene usage. Record screenshot fixture for each state and ownership decision. Include UI generated under modal open and when battle, map or onboarding state changes.

**Exit:** no screen or dynamic modal lacks an assigned owner; new prefab inventory and migration order reviewed; no proposed migration of intentionally procedural or variable gameplay data.

### Phase 2 — Editor preview + layout authority infrastructure (no visible redesign)

**Do:** Provide safe Editor-only preview menu/actions and deterministic fake sessions, driven by Editor scripts, for Home, Codex detail/unknown, starter, combat (including 0/5 and 5/5 skills), Inventory, Shop, Profile/Settings, Adventure Journal/Activity/Rest, Prisms, world selection/field and first-time loading. Preview never writes to real saves or auto-imports assets. Create safe Inspector feedback for missing serialized binding refs and a read-only validator for missing prefab dependencies. Normalize `[ExecuteAlways]` scripts to only reflow existing objects, not reconstruct children. Add a Scene View layout-editing workflow for serialized `GildedLayout` reference rectangles, avoiding hard-coded pixel positions for features that should be draggable.

**Exit:** change/saving/reopening a control's layout works while Play is off; pressing Play and stopping cannot erase the edit; preview starts and cleans up deterministically; existing screenshots remain visually unchanged.

### Phase 3 — Shared UI templates/binding layer

**Do:** Reuse existing `AevarethButton`, `AevarethPanel`, `AevarethModal`, `AevarethItemSlot`, `AevarethQuestCard`, `AevarethCelestialSkillCard`, `AevarethGildedMonsterCard` and related components. Add new prefabs only for uncovered screens/rows. Introduce serialized optional `UiReferences`/presenter bindings and design-time placeholder values, without changing domain model ownership. `SkillCardPanel.EnsureVisuals()` and `SkillArtworkView.Create()` become Editor migration/validation helpers for authored prefabs; production uses existing children instead. Move visual factory construction out of normal opening paths after prefab-backed replacement passes. Version new prefabs deterministically, retaining existing GUIDs/serialized local object IDs for in-use templates. Avoid incidental font/icon redesign.

**Exit:** standard skills/items/quest/monster templates open in Prefab Mode with editable artwork/labels/layout; no duplicate generated visual children on repeated opening/reinitialization; old binding APIs still pass tests.

### Phase 4 — Pilot: Battle skill cards (smallest complete vertical slice)

**Do:** Serialize the existing battle 2×2 card roots into the Battle scene, or attach existing authored skill card prefab instances to the existing card Buttons. Bind `BattleSkillPanel`, `BattleSkillCardView`, `SkillCardPanel`, `SkillArtworkView`, `BattleScreen`, `BattleStageLayout` and `GildedBattleView` to serialized objects. Preserve skill descriptions, charges (actual x/y), depleted/disabled states, cooldown, shield/buff/debuff status, priority and selection. Preserve action ordering and keyboard/controller/touch routes. Never replace current `BattleScreen` or battle model. Fix layout authority so Inspector positioning wins in editor and authored responsiveness still works in play.

**Exit:** 2×2 cards and backing art visible/editable out of Play Mode; all four slots, depleted states, cooldowns, attack/defense and skill-to-effect VFX/SFX pass identical before/after interactions and screenshots. Editor-tested `SkillCardPanel` prefab is used; no runtime rebuilding of permanent child labels.

### Phase 5 — Battle Prism/item drawer, results and cinematic surfaces

**Do:** Convert `BattleItemView` fixed drawer header, scroll frame, status, close and selected-detail panel into a scene-linked modal prefab, and all item/Prism choices into authored row prefabs. Keep conditional list length and chance formula data-driven. Inspect `PostBattleProgression.prefab`, `ProgressionSequenceController`, battle cinematics and animation controllers; already-authored elements are retained, not cloned. Ensure overlays, touch focus, cancellation and layer order are identical.

**Exit:** all ten Prisms display unique icon and live capture chances, charge consumption is transactional/once-only, 0 stock behaves correctly, Escape/Back does not advance a turn, postbattle/evolution visuals still work.

### Phase 6 — Inventory, Shop, Profile and Settings

**Do:** Replace `CommerceHost.Prepare/BuildChrome` fixed hierarchy creation with serialized reusable `CommerceShell.prefab` (header, avatar, saved coin wallet, bag, gear, dock, overlay, safe-area frame). Move `InventoryShopView` stable page, tabs, selected detail/quantity, checkout, status and scrolling region into prefab(s); `ItemSlot` and monster offer rows remain template instances. Convert `SharedSettingsView` and identity/help pages into serialized prefabs (including slider track/fill/handle wiring). Preserve `CommerceUi` only as an explicit Editor authoring helper and migration fallback while remaining callers are converted. Do not reset saved wallet, purchase receipt or profile identity when modal opens/closes.

**Exit:** Inspector-editable full screens, double-open safe, no duplicate overlays, all navigation and purchases are exactly-once, Save/Load unchanged, selections/cancel/focus restored, all 50 species remain distinct/locked where intended.

### Phase 7 — Adventure Journal, activities, quests, free rest, and Prism resupply

**Do:** Convert `RealmPanel`, `AdventureJournalView`, `AdventureActivityView`, `RealmAdventureHost` permanent modal anatomy to editable prefabs; quest/activity/choice/evidence/camp/prism row elements become repeatable templates with bound data. Keep quest rule authority in `WorldSession` and `RealmAdventureCatalog`; no authored quest nodes become hard-coded UI objects. Preserve wrong-choice hints, progression gates, postgame pages, free camp rest and single resupply action, focus return and modal state guard logic.

**Exit:** each page inspectable out of Play; wrong/correct activity choice, no duplicate rewards, all postgame/legacy routes, failed save recovery and active-skill charges pass with unchanged progress.

### Phase 8 — Home, Codex, collection, training and starter selection

**Do:** Reuse already serialized Home hierarchy and current monster card prefabs; convert only remaining dynamically created fixed modal shells and runtime-only children. Keep `CompanionCollectionView` and `CompanionTrainingView` instantiating list row templates for live collections; bind their templates via serialized Inspector fields. Retain `GildedLayout` pairs or migrate them with measured geometry equivalence. Provide editor fixtures for discovered/unknown Codex entries, level/stats/skills, selection, sleep/HP, starter carousel and saved first bond. Preserve historical Codex scene asset even if unused.

**Exit:** home collection and codex visible at edit time with mock data, original real data at play time; no duplicate clicks, focus traps or unexpected starter reselection; all monster art and saved training unchanged.

### Phase 9 — World map, atlas, exploration and procedural overlays

**Do:** Retain the serialized World Map scene, scene cameras, travel paths and ten `MapDefinition` asset authorities. Turn fixed navigation/help/modal/map HUD structure into editable scene objects/prefabs. Keep the 1,337 catalog nodes/branches data-driven; use authored reusable `WorldNode`, `FieldNode`, `MapRoute`, `EncounterMarker`, `Dialogue` prefabs and a deterministic Editor preview for selected map, current node, unlocked route, discovery and interactions. For genuinely procedural paths/geometric icons, expose stable editable host objects and parameters, not millions of baked children. Preserve camera bounds, route connectivity and focus of next valid node.

**Exit:** editor preview accurately shows selected map in edit mode; node identity/routes/positions match baseline; no blocked progression or missing edges; traveling, returning, branch selection and save/load route pass unchanged.

### Phase 10 — Onboarding, first journey, loading, visual effects and polish of editability

**Do:** Inspect Bootstrap, Onboarding, Character Creation and Starter Selection scene trees and retain serialized foundations. Keep existing `FirstJourneyExperience.prefab` and `GildedLoading.prefab` Resources references; add safe Editor previews for loading percentage, title crawl, tutorial and failure/retry states. Review all 120 skill prefabs in Prefab Mode by phase (charge, release, hit, aftermath, defense, buffs, debuffs and passive persistences) and expose Inspector-editable tuning; **do not rebuild VFX** or change damage/turn logic. Preserve current audio routing/volumes, orientation, reduced motion and other accessibility safeguards.

**Exit:** all seven build scenes have editable fixed visuals; 120 skill assets remain valid and their GUIDs match baseline; first-time flow/restart/returning save routes unchanged.

### Phase 11 — Remove runtime *visual hierarchy construction* only after callers are migrated

**Do:** Audit uses of `CommerceUi.Rect/Text/Button/Surface/Scroll`, `new GameObject`, `AddComponent` in `Runtime/UI`, and `DestroyImmediate` in view code. Remove **only redundant fixed-layout creation paths**, not valid data-row instantiation, particle/trail effect creation, offscreen previews, procedural graphics or domain entities. Convert old broad scene builders to optional, narrowly scoped explicit migration tools or mark legacy-only; avoid re-running them over customized scenes. Preserve existing scenes, all prefabs, obsolete-compatible references and guardrails unless zero-use can be rigorously proven. Do not run any generic cleanup tool.

**Exit:** no runtime-generated full fixed screen reappears as an alternative to the authored screen; no hidden duplicate hierarchy, no unreferenced missing components or stale event listeners, and no release-only failures.

### Phase 12 — Whole-game regression, performance and guarded integration

**Do:** On an isolated validation copy, import Unity/URP assets cleanly, inspect Console (zero new errors or missing scripts), run complete EditMode and PlayMode suites; verify every scene, every UI state, script serializations and all prefab instances; run native preview captures for multiple screen sizes, safe-area/cutout samples, on/off editability lifecycle, keyboard/controller/touch. Rebuild Windows player and signed ARM64 Android using existing isolated runner/retained signing certificate; verify manifest, install, launch, pause/resume, touch interaction, sound, thermal/GC/frame-time, VFX and save upgrades on real Android device(s). Compare protected file hashes and source diff, reject unrelated changes. Carry only verified target changes into source `main` according to repository rules, preserving backups and only committing/pushing if authorized. GitHub Release is a **separate optional step**; never publish before install/QA acceptance.

**Exit:** every explicit gate in §5 is green or documented with an approved exception; release candidate is traceable to an exact commit/input manifest; in-scene authoring and editor preview both work after reopening Unity.

## 5. Mandatory acceptance matrix

| Area | Required pass condition |
|---|---|
| Source/asset integrity | No deleted/renamed protected files; original eight scene files, seven build indices, `.meta` identities, maps, all 50 species, all 120 skill prefab GUIDs, art and Resources lookup keys preserved. Diff every changed asset, scene and serialized reference. |
| Editability | For each fixed screen: stop Play, select objects in Hierarchy, modify visual layout via Inspector/Scene handle, save, reopen, Play/Stop, verify edit survives. Prefab Mode works for all new reusable components. |
| Screenshot fidelity | Deterministic fixture captures compared in identical Unity/editor rendering configuration and screen sizes; no unexplained design drift, clipping, occlusion, text overflow or lost art; all changes intentional and approved. |
| Tests | Complete EditMode, PlayMode and tooling suites run; zero **new** failures, skips or missing scripts. Any prior red tests must be distinguished from regressions and cannot be silently reclassified green. |
| Save compatibility | Save fixture matrix: fresh, legacy (versions 1–13), profile (1–3), partially onboarded, mid-battle, capture, defeated/recovery, before/after evolution, active quests/postgame, corrupt/future-version recovery. UI-only navigation does not write/mutate save files. |
| Input/navigation | Each modal opens/closes exactly once; Escape/Back, keyboard/controller/touch all work; selected focus restores correctly; no invisible raycast blockers or duplicate buttons. |
| Combat/effects | Damage/RNG/turns/defensive status/uses/Prism chance/stock/result identical; 120 skills still map to correct VFX, SFX and cut-ins; temporary VFX cleanup doesn't leak. |
| Responsiveness | Validate at least 320×568, 360×640, 390×844, 412×915, 768×1024, 1080×1920, 1080×2400 plus cutout/inset simulation. No overlapped touch targets, cropped controls or text truncation. |
| Performance | Compare same-hardware before/after cold load, steady frames, modal open/close, GC allocations, peak memory, UI rebuilds, long journeys and extended battle effects. No material regression; investigate any repeated hierarchy construction or allocations on idle. Set device-specific targets using measured baseline before approval. |
| Android release | Signed original-key ARM64 build, installation/upgrade and actual-device playtest succeed; APK package identity retained; no reliance on screenshots or simulated validation alone. |

**Recommended repeatable checks:** count serialized view roots per scene; assert required field references non-null; execute `Open-Close-Open` 100 times on reused modal templates and check child count, listeners and scene object allocations remain stable; compare prefab GUID/fileID graph; compare anonymized fixture-save JSON before/after passive navigation and use deterministic gameplay trace comparison on actual commands.

## 6. Risk register and mitigations

- **Critical — 10 MB scene changes cause accidental unrelated serialization:** make surgical edits, inspect scene diffs for changed `fileID`/component references, back up YAML, never re-save all scenes indiscriminately.
- **Critical — layout scripts overwrite Inspector edits:** resolve serialized layout source of truth first; create edit-time move/resize integration for `GildedLayout`, `HomeLayout`, `WorldMapLayout`, `BattleStageLayout` and `PortraitFrame`; test edit/save/reopen/Play/Stop.
- **Critical — lost serialized refs/events after prefab replacement:** serialized ref audit, missing-script scan, PlayMode focus and action tests, per-scene ref diffs and rollback.
- **High — dynamic content mistaken for static assets:** keep collection/shop/quests/nodes data-driven and bind to prefab item templates; do not freeze 1,337 map nodes or any save-specific monster list into scenes.
- **High — dual rendering paths coexist:** add a migration feature switch only if needed during staging, but never show two views simultaneously; remove old fixed builder only after pilot passes.
- **High — business logic changes hidden inside UI callbacks:** preserve commands/transaction entry points and timing; maintain deterministic battle/save traces; avoid touching `Runtime/Adventure`.
- **High — editor builders destructively regenerate scenes/prefabs:** never run broad `RealmValidationPipeline.AuthorAll` during migration; use explicit, scoped and guarded authoring with diff and rollback; retain original `AGENTS.md` controls.
- **High — skill prefabs lose VFX/SFX metadata:** never recreate them; preserve prefab identity and serialized phase objects; replay each skill category and at least all skill binding manifests.
- **Medium — false visual parity due to mock state differences:** fixture data and screenshots keyed to exact world/profile/monster/skill state and Unity version.
- **Medium — Android visual/performance difference:** explicit phone/device acceptance, not just Windows or Editor screenshots.

## 7. Per-screen migration work register

| Target | Existing code/asset owner | Planned conversion | Keep dynamic |
|---|---|---|---|
| Battle main HUD | `BattleScreen`, `BattleStageLayout`, `GildedBattleView`; `Scenes/Battle` | In-place authored Canvas hierarchy, serialized field bindings | HP/energy/text/monster art positions, event states |
| 2×2 skills | `BattleSkillPanel`, `BattleSkillCardView`, `SkillCardPanel`, `SkillArtworkView`, `AevarethCelestialSkillCard.prefab` | Preserve prefab and permanently serialize slot visuals | Four equipped skills and remaining uses |
| Battle item/Prism menu | `BattleItemView`, `PrismIconGraphic` | Modal prefab + editable row/icon template | Ten-element inventory/percentage counts |
| Battle result/evolution | `PostBattleProgression.prefab`, controllers | Retain and expose preview modes, no rebuild | EXP/evolution data and effects |
| Commerce chrome | `CommerceHost`, `CommerceUi` | Common root/Header/Dock/Overlay prefabs | Player identity, coins, selected destination |
| Inventory/Shop | `InventoryShopView`, existing item slot | Serialized page/sheet prefab with row templates | Items, monsters, quantities, actions |
| Identity/settings/help | `CommerceHost`, `SharedSettingsView` | Prefab page with Slider serialization | Actual profile and preferences |
| Journal/activity/rest | `RealmAdventureHost`, `RealmPanel`, `AdventureJournalView`, `AdventureActivityView` | Modal roots and cards authored, serialized buttons | Activities, choices, quests, evidence, 10 Prisms |
| Home/collection/training | `HomeHubScreen`, `CompanionCollectionView`, `CompanionTrainingView`, `HomeLayout` | Keep scene; refactor only missing fixed visuals / binding | Owned monster list, stats, skills, rest |
| Codex | `MonsterCodexView*`, card prefabs | Retain serialized shell, add Editor fixture states | Discovered/unknown forms, detail, skill library |
| Starter/character/title | `ChoiceSelection*`, `OnboardingLayout`, existing scenes | Inspector-editable anchored layouts and preview | First-time progression and selection authority |
| World map and exploration | `WorldMapScreen*`, `WorldSelectionView*`, `AdventureFieldView`, `MapNodeView` | Fixed HUD and map-marker templates with Editor preview | Route nodes, branches, camera/travel/encounters |
| Intro/loading | `FirstJourneyExperience.prefab`, `GildedLoading.prefab` | Retain; authored preview states | Real async progress and tutorial checkpoints |
| 120 skill effects | `Prefabs/Skills`, `SkillVfxLayer`, `BattleSkillPresentation` | Retain all existing Prefab Mode compositions | Skill activation, timing, defensive effects |

## 8. Practical safe change-management procedure for every phase

1. Verify main's input SHA and clean status; archive source and scene/prefab metadata to a path outside checkout; never alter real saved games or release signing key.
2. Enumerate exact files proposed to change and expected hierarchy diffs. Preserve non-target objects, scene GUID and prefab/meta identity.
3. Make change in **isolated guarded authoring/validation project** where Editor scripts require that identity. Use explicit Unity authoring actions only; do not auto-author/import or call broad cleanup.
4. Save authored Unity assets, compare serialized references and protected asset hashes against baseline. Fail on unexpected file changes; return to snapshot if invalid.
5. Run phase-level tests and before/after screenshots, then Play Mode interaction, safe-area and data/save traces.
6. On success, apply validated changes to intended source paths without modifying unrelated state; perform a fresh import/test from that exact target candidate; if tests fail, revert affected migration slice only.
7. Generate a simple evidence receipt: input SHA, paths changed, expected asset/scene GUIDs, hashes, tests, screenshots, Android results, known issues and rollback artifact.
8. Do not commit, push, merge, delete, force-update refs or publish a GitHub Release without the user's explicit scope/authorization. If authorized later, follow `AGENTS.md` for `main`-only development; keep AI planning Markdown only in ignored `docs/gpt-plans/` (this downloadable copy is outside the repository).

## 9. Suggested delivery checkpoints

- **Gate A — Baseline protected:** audits, snapshots and baseline tests/visuals exist.
- **Gate B — Inspector ownership proven:** no layout is overwritten after Play/Stop, one selected pilot control remains saved.
- **Gate C — Battle slice passes:** editable 2×2 skills + capture drawer, identical business rules and visuals.
- **Gate D — Commerce and Adventure UI pass:** all previously code-generated modal roots now prefab-backed; repeated opening leak-free.
- **Gate E — Full seven-scene editability:** all persistent layouts editable, dynamic lists still correct, skill prefabs unchanged.
- **Gate F — Full regression and Android device acceptance:** only then consider a release.

## 10. First executable development task after this proposal is approved

Perform **Phase 0 and Phase 1 only**, without changing gameplay code. Produce a machine-readable manifest mapping every permanent screen/modal, runtime-generated GameObject, current prefab template, presenter and serialized layout owner. Record exact before/after Play hierarchy and screenshots in isolated Unity with fake saves; supply a prioritized patch list with zero-change risk gates. Do not prematurely run `RealmValidationPipeline.AuthorAll`, rebuild 120 skill prefabs, alter world/save authority, clean Assets or publish an APK. Then implement the smallest pilot: serialized `AevarethCelestialSkillCard` visual references in the existing Battle `2×2` grid. Repeat all defined tests/gates before broader rollout.

---

**Evidence basis:** repository tree at `9c067d2`, `AGENTS.md`, `README.md`, `ProjectSettings/EditorBuildSettings.asset`, `Assets/_Aevareth_Monster_Realm/Docs/UnityProjectContext.md`, `docs/project-structure.md`, `docs/gilded-sigil-ui.md`, `docs/inventory-shop.md`, `docs/realm-adventure.md`, `docs/skill-vfx.md`, `docs/android-release.md`, source files explicitly named above, and examples from serialized UI/skill/Resources prefabs. Reported prior test passes are historical repository records, not tests re-run in this session.
