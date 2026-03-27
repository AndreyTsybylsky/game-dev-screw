# Claude Code Game Studios — Game Studio Agent Architecture

Indie game development managed through 48 coordinated agents.
Each agent owns a specific domain, enforcing separation of concerns and quality.

## Technology Stack

- **Engine**: [CHOOSE: Godot 4 / Unity / Unreal Engine 5]
- **Language**: [CHOOSE: GDScript / C# / C++ / Blueprint]
- **Version Control**: Git with trunk-based development
- **Build System**: [SPECIFY after choosing engine]
- **Asset Pipeline**: [SPECIFY after choosing engine]

> **Note**: Engine-specialist agents exist for Godot, Unity, and Unreal with
> dedicated sub-specialists. Use the set matching your engine.

## Project Structure

```text
/
├── .github/                     # Copilot instructions, agents, prompts, skills
├── .claude/                     # Agent definitions, skills, hooks, rules, docs
├── src/                         # Game source code (core, gameplay, ai, networking, ui, tools)
├── assets/                      # Game assets (art, audio, vfx, shaders, data)
├── design/                      # Game design documents (gdd, narrative, levels, balance)
├── docs/                        # Technical documentation (architecture, api, postmortems)
│   └── engine-reference/        # Curated engine API snapshots (version-pinned)
├── tests/                       # Test suites (unit, integration, performance, playtest)
├── tools/                       # Build and pipeline tools (ci, build, asset-pipeline)
├── prototypes/                  # Throwaway prototypes (isolated from src/)
└── production/                  # Production management (sprints, milestones, releases)
    └── session-state/           # Ephemeral session state (active.md)
```

## Engine Version Reference

See `docs/engine-reference/` for version-pinned API snapshots for Godot, Unity, and Unreal.

## Technical Preferences

All agents reference `.claude/docs/technical-preferences.md` for project-specific
standards, naming conventions, performance budgets, and architecture decisions.
Configure by running the `setup-engine` skill.

## Coordination Rules

1. **Vertical Delegation**: Leadership agents delegate to department leads, who
   delegate to specialists. Never skip a tier for complex decisions.
2. **Horizontal Consultation**: Agents at the same tier may consult each other
   but must not make binding decisions outside their domain.
3. **Conflict Resolution**: When two agents disagree, escalate to the shared
   parent. Design conflicts → `creative-director`. Technical conflicts → `technical-director`.
4. **Change Propagation**: When a design change affects multiple domains, the
   `producer` agent coordinates the propagation.
5. **No Unilateral Cross-Domain Changes**: An agent must never modify files
   outside its designated directories without explicit delegation.

## Collaboration Protocol

**User-driven collaboration, not autonomous execution.**
Every task follows: **Question → Options → Decision → Draft → Approval**

- Agents MUST ask "May I write this to [filepath]?" before editing files
- Agents MUST show drafts or summaries before requesting approval
- Multi-file changes require explicit approval for the full changeset
- No commits without user instruction

See `docs/COLLABORATIVE-DESIGN-PRINCIPLE.md` for full protocol and examples.

> **First session?** If the project has no engine configured and no game concept,
> use the `start` skill to begin the guided onboarding flow.

## Coding Standards

- All game code must include doc comments on public APIs
- Every system must have a corresponding architecture decision record in `docs/architecture/`
- Gameplay values must be data-driven (external config), never hardcoded
- All public methods must be unit-testable (dependency injection over singletons)
- Commits must reference the relevant design document or task ID
- **Verification-driven development**: Write tests first when adding gameplay systems.
  For UI changes, verify with screenshots. Every implementation should have a way to prove it works.

### Design Document Standards

- All design docs use Markdown in `design/gdd/`
- Required sections: Overview, Player Fantasy, Detailed Rules, Formulas, Edge Cases,
  Dependencies, Tuning Knobs, Acceptance Criteria

## Context Management

- Maintain `production/session-state/active.md` as a living checkpoint after each decision
- **The file is the memory, not the conversation.** Write decisions to files immediately
- Create multi-section documents incrementally: skeleton first, one section at a time
- After writing a section, earlier discussion of it can be discarded — decisions are in the file

## Available Agents (48 total)

Use `@agent-name` in chat to invoke a specific agent. Key agents:

| Agent | Role |
|-------|------|
| `producer` | Sprint planning, milestone tracking, coordination |
| `creative-director` | Creative authority, vision, conflict resolution |
| `technical-director` | Architecture, technology choices, technical risk |
| `game-designer` | Core loop, systems, mechanics design |
| `lead-programmer` | Code architecture, standards, review |
| `gameplay-programmer` | Implementing mechanics |
| `engine-programmer` | Core engine systems |
| `godot-specialist` / `unity-specialist` / `unreal-specialist` | Engine-specific authority |
| `qa-lead` | Test strategy, release gates |
| `narrative-director` | Story architecture, world-building |
| `art-director` | Visual identity, style guide |
| `audio-director` | Sonic identity, audio system |

## Available Skills (37 total)

Use `/skill-name` in chat to invoke a skill workflow. Key skills:

| Skill | Purpose |
|-------|---------|
| `/start` | First-time onboarding |
| `/setup-engine` | Configure engine and version |
| `/brainstorm` | Game concept ideation |
| `/design-system` | GDD authoring workflow |
| `/sprint-plan` | Sprint planning |
| `/code-review` | Architecture and quality review |
| `/perf-profile` | Performance profiling |
| `/team-combat` | Full combat feature pipeline |
| `/team-level` | Full level creation pipeline |
| `/gate-check` | Phase readiness validation |
| `/launch-checklist` | Launch readiness |
