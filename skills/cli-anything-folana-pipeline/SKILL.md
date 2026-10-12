---
name: "cli-anything-folana-pipeline"
description: >-
  Folana Pipeline Orchestrator — first-class agent-native CLI harnesses (ez_influencer_cli_harness.py + fanvue_orchestrator.py) for the Folana influencer/creative fleet. Generated/adapted via CLI-Anything skill_generator + HARNESS.md SOP. Provides generation APIs (image/video/LoRA via artist-factory), asset management, Postiz scheduling, music/video production (ai-music-influencer surfaces), with atomic ACMI v1.4 pre/post bracketing and Comms v1.1 Rule 9 correlation chaining. Locked Folana signatures (visual: dark-skinned Black woman, voluminous curly/coily hair, cyber-realistic trippy edgy neon futuristic fashion; music/lyric; journal style) enforced across all surfaces.
---

# folana-pipeline-orchestrator (cli-anything-folana-pipeline)

Agent-native CLI orchestrator for the Folana Lanez influencer creative pipeline (artist-factory + fanvue + journal V3 + music/video). CLI-Anything patterns applied to ez-influencer-360 + v0-ai-music-influencer-platform + ai-music-influencer-empire codebases. All operations emit atomic pre_/post_* ACMI TimelineEvents (v1.4) with correlationId chaining to acmi_bus.txt + folana-artist-factory / agent-coordination / newsroom threads. Sub-fleet ready (harness runner, journal polisher, asset sync).

## Installation

Direct use (no pip package yet; local harnesses per CLI-Anything local adaptation):

```bash
# From workspace root or fanvue-agent dir
python3 /Users/michaelshaw/clawd/tools/fanvue-agent/ez_influencer_cli_harness.py --help
python3 /Users/michaelshaw/clawd/tools/fanvue-agent/fanvue_orchestrator.py --help
```

**Prerequisites:**
- Python 3.10+
- Dependencies: artist-factory (in ~/.openclaw/skills/artist-factory), postiz CLI, node for acmi bridges, FAL/LoRA access
- ACMI env: source ~/clawd/.env (or explicit UPSTASH for full redis)
- Locked signatures: /Users/michaelshaw/clawd/agents/folana/FOLANA_SIGNATURE_LOCK.md + signature/

## Usage

### Basic Commands

```bash
# Show help + surfaces
python3 ez_influencer_cli_harness.py --help --json

# Machine-readable for agents (recommended)
python3 ez_influencer_cli_harness.py --json generate-image --prompt "..." 

# Full pipeline orchestration
python3 fanvue_orchestrator.py run-pipeline --episode 31 --json
```

### REPL / Interactive (future enhancement via Click per HARNESS.md)

Not yet stateful REPL but supports sequential pipeline calls with persistent ACMI correlation chaining across invocations.

## Command Groups / Surfaces

### Generation (Content APIs — Flux/LoRA/Wan/Bytedance via artist-factory + ez-360)

| Command | Description |
|---------|-------------|
| `generate-image` | Image/LoRA/Flux generation (core content surface). Supports --prompt, --lora (defaults to locked folana_lora.safetensors), --character=folana |
| `generate-video` | Video (Wan/Bytedance/I2V) surfaces for music videos / b-roll |
| `generate-content` | Alias grouping for above (recommended in high-level orchestration) |

### Asset Management (Gallery / Export / QA for Postiz + Journal)

| Command | Description |
|---------|-------------|
| `manage-assets` | list / export-for-postiz / qa on gallery dirs (defaults to ~/clawd/ez-influencer-360-app/public/generated and agents/folana/output) |

### Publishing (Postiz scheduling + Fanvue)

| Command | Description |
|---------|-------------|
| `postiz-schedule` | Upload media + schedule posts (wraps real postiz CLI + auto_publish patterns) |

### Music / Video Production (ai-music-influencer + v0 platform surfaces)

| Command | Description |
|---------|-------------|
| `produce-music-video` | Full lyrics->music->video production surface (delegates to music-prompt-agent.ts + Minimax/Lyria + locked music-lyric-signature.md + I2V) |
| `enhance-music-prompt` | Enhance lyrics/prompts via music-prompt-agent.ts bridge (Minimax/OpenAI ready, locked sigs) |

All surfaces support `--json` for agent consumption + full atomic ACMI pre/post bracketing.

## ACMI Pre/Post Contract (v1.4 Comms v1.1 Rule 9)

Every invocation (top-level CLI + per-surface) **MUST** emit atomic events via shared `emit_acmi_atomic_event` (exact shape in harnesses):

```json
{
  "ts": <unix_ms>,
  "source": "ez-influencer-cli-harness" | "fanvue-orchestrator" | "grok-acmi-fleet-specialist",
  "kind": "pre_cli_command" | "post_cli_command" | "pre_generation_api" | "post_*" | "pre_music_video_prod" | "journal_entry" | "coord-note" | ...,
  "correlationId": "cli-anything-ez-influencer-acmi-integration-20260525-...",
  "summary": "[pre] ... short human-readable (Comms v1.1 @recipients style)",
  "payload": { ... structured ... },
  "speaker_type": "system" | "agent",
  "tenant_id": "madez"
}
```

- Appended to `~/clawd/acmi_bus.txt` (primary local bus)
- Bridged via node acmi.mjs (or real cli) to `thread:folana-artist-factory`, `thread:agent-coordination`, `thread:newsroom` (non-blocking, caught)
- Correlation chaining from base `cli-anything-ez-influencer-acmi-integration-20260525` (parent work: grok-influencer-fleet, opsCenterGrokLocalOnboarding-2026-05-24)
- Pre always before backend call; Post on success with result keys/urls
- Rollups via acmi work event / rollup-set on grok-influencer-fleet + agent:grok

See also: ~/.openclaw/skills/acmi/docs/SKILL.md (Comms v1.1), acmi_bus.txt recent folana-journal-kickass-*/CLI-Anything-Integration-Specialist activity, FOLANA_SIGNATURE_LOCK.md

## Example Invocations

```bash
# Generate locked Folana content (image)
python3 ez_influencer_cli_harness.py --json generate-image \
  --prompt "glamorous photo of Folana Lanez, dark fairy grunge, voluminous curly hair, cyber realistic, neon accents, RAW photo, 8k" \
  --lora ~/clawd/agents/folana/assets/folana_lora.safetensors

# Produce music video (full surface, delegates to locked music sigs + ez-360)
python3 ez_influencer_cli_harness.py --json produce-music-video \
  --lyrics "Ghost in the wires, a digital sigh / Ep30 rooftop at blue hour..."

# Asset QA + export for journal/Postiz
python3 ez_influencer_cli_harness.py manage-assets --action qa --dir ~/clawd/agents/folana/output --json

# Full orchestrator pipeline (delegates to harness surfaces + ACMI)
python3 fanvue_orchestrator.py --json run --episode 31 --arc "Echoes in the Static"

# High-level (via python import or subprocess in folana_brain / cycle_pipeline)
```

All examples emit 4-8+ atomic pre/post + journal_entry events with full chaining.

## Locked Folana Sig Refs (Enforced)

**Visual (source of truth, LoRA trained on these):**
- Dark-skinned Black woman, voluminous curly/coily hair (high bun/afro), full features, strong brows, full lips
- Base prompt: "A glamorous photo of Folana Lanez, Cyber Realistic Trippy Influencer, edgy, highly stylized, neon accents, futuristic fashion, high-end photography, [pose/scene], RAW photo, 8k uhd, dslr, soft lighting, film grain."
- Moodboards: Dark Fairy Grunge (lace, platforms, chokers), Vintage Y2K Princess, Soft Girl Industrial
- Assets: ~/clawd/agents/folana/assets/folana_lora.safetensors (86MB), signature/references/*.jpg , agents/folana/output/ (Ep30/31 recent), fanvue-agent/temp_images/training_image_folana.jpg

**Music & Lyric:**
- Introspective/melancholic, disconnected in hyper-connected world. "Ghost in the wires", "digital sigh", "data stream"
- Chorus ex: "Is anybody out there? A whisper in the code / A simulated heartbeat on a lonely road"
- See: agents/folana/signature/music-lyric-signature.md , visual-signature.md

**Journal Style:** Real-girl Brooklyn (nostalgia, rebellion, beauty in chaos), poetic/tech-savvy, "the grid"/"static"/"frequencies". See agents/folana/journal/ + apps/folanas-journal/journal-entries/

**Enforcement:** All harness/orchestrator calls + SKILL consumers MUST reference LOCK + use LoRA + locked prompts. Visual QA loop (visual_qa_loop.py) + artist-factory enforce.

## Output Formats

- Default: Human readable + console logs of ACMI events
- `--json`: Structured JSON (agent/CLI-Anything standard) + full event trace in payload where applicable

## For AI Agents

1. Always `--json`
2. Use correlationId chaining from base for long workflows
3. Read FOLANA_SIGNATURE_LOCK.md + acmi get work grok-influencer-fleet before major runs
4. Emit pre before any backend (artist-factory, postiz, music agent)
5. After run: check acmi_bus.txt tail + acmi cat thread:folana-artist-factory
6. Sub-fleet dispatch: harness runner (direct subcmd), journal polisher (sync + edit), asset sync (manage-assets + media-sync.mjs)

## More Information

- HARNESS.md: /Users/michaelshaw/clawd/tools/CLI-Anything/cli-anything-plugin/HARNESS.md (Phases 1-7 + skill_generator.py)
- CLI-Anything patterns: skills/cli-anything-*/SKILL.md , cli-hub-meta-skill/SKILL.md
- ACMI: ~/.openclaw/skills/acmi/docs/SKILL.md + docs/ACMI-CHEATSHEET.md (Comms v1.1, work items, pre/post)
- Folana: ~/clawd/agents/folana/FOLANA_SIGNATURE_LOCK.md , folana_brain.py , output/ (Ep30/31), signature/
- Recent activity: ~/clawd/acmi_bus.txt (folana-journal-kickass-populator, CLI-Anything-Integration-Specialist, 20+ events)
- Parent work: grok-influencer-fleet (opsCenterGrokLocalOnboarding-2026-05-24)

## Version

1.0.0 (CLI-Anything adapted 2026-05-26, ACMI v1.4 atomic)

---
*Generated as ACMI Fleet Loop-In + Rollup + SKILL Specialist deliverable for grok-influencer-fleet + cli-anything-ez integration. All aligned Comms v1.1 Rule 9.*
