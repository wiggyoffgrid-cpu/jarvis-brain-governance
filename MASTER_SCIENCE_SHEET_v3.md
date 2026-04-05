# MASTER SCIENCE SHEET — PROJECT JARVIS
**Version 3.1 | April 5, 2026 | Operational Reference**
*Consolidated from v1 (March 30) + v2 (April 3) + lineage lab logs v19, v20, APPEND.*
*v3.1 patch: removed deleted models (Qwen3.5-27B, Qwen3-8B F16, llama.cpp.backup); confirmed 309/113 client dedup; renumbered NEEDS_VERIFICATION (14 → 12 open items).*
*This document contains ONLY operational science — measurements, lab findings, locked parameters, working pipelines, failure modes. Family data, personality content, and governance structure live elsewhere (D-Series, Ideas Vault).*

---

## PART 1 — HARDWARE BASELINE

### WIGGYS-BEAST
| Component | Specification |
|---|---|
| Model | Acer Predator Helios 18 AI PH18-73-90A6 |
| Motherboard | ARL Vantage_ARX |
| CPU | Intel Core Ultra 9 |
| GPU | NVIDIA RTX 5080, 16 GB VRAM |
| RAM | 32 GB DDR5 |
| Storage | 2× NVMe (1 TB SK Hynix stock + 4 TB Samsung 990 EVO Plus); 3rd M.2 slot empty |

### Gigabyte Secondary
- Hostname: DESKTOP-E0HN73M
- Domain: PILEDRIVING\ericl
- Connected to Beast network

---

## PART 2 — MODEL ROSTER

### Active Models
| Model | File | Size | Idle VRAM | Max Context | Role |
|---|---|---|---|---|---|
| Qwen2.5-14B Q6_K | `qwen2.5-14b-instruct-q6_k.gguf` | 11.29 GB | 14,947 MiB (92%) | **16,384 confirmed stable** | Everyday fast brain |
| Qwen3.5-9B Claude-Opus Distilled Q6_K | `Qwen3.5-9B.Q6_K.gguf` | 7.36 GB | 9,552 MiB (59%) | **65,536 confirmed stable** | CRM powerhouse, WEAP analyst, deep reasoning |
| Gemma 4 E4B | — | ~8,206 MiB | — | — | Champion efficiency model (deployment path NEEDS VERIFICATION) |
| GLM-Z1-9B | — | — | — | — | Math specialist (status NEEDS VERIFICATION) |
| DeepSeek R1 14B | — | — | — | — | Present on disk at `D:\Jarvis\qlora\models\DeepSeek-R1-14B\` |

### LoRA Adapter
- **Current:** `jarvis_7b_lora_v13`
- **Parameters:** r=16, lora_alpha=32, dropout=0.1, lr=8e-5, 7 epochs, 104 training records
- **Role:** Personality layer only — NOT facts
- **Status:** Stable; do not retrain without significant personality shift need

### Retired (deleted from disk)
- Qwen3.5-27B Claude-4.6-Opus-Reasoning-Distilled Q4_K_S — 15.6 GB, 97% VRAM, no inference headroom — **deleted April 5, 2026**
- Qwen3-8B F16 base — **deleted April 5, 2026**
- GPT-OSS 20B — retired
- All Ollama models — Ollama itself deleted March 30 (12.44 GB reclaimed)

---

## PART 3 — LOCKED INFERENCE PARAMETERS

```
--top-k 20              # Keep only top 20 tokens
--repeat-penalty 1.25   # DO NOT go below 1.25 on 14B — causes degenerate loops
--mirostat 1            # Deterministic sampling for consistent personality
-ngl 99                 # Offload all layers to GPU
num_keep 24             # Preserve system prompt tokens
```

### Context Sizes (measured, not default)
- **14B:** `num_ctx 16384` — confirmed stable under normal inference load. 8192 is no longer the ceiling.
- **9B:** `num_ctx 65536` — confirmed stable with full CRM payload (76 people + 309 clients).

### Extraction Task Parameters (9B only)
```
temperature 0.1
top_k 40
top_p 0.9
repeat_penalty 1.25 – 1.4
```

### Quantization Standard
**Q6_K with imatrix calibration, always.** Proven stable, ~80% accuracy vs f16, preserves LoRA personality. No other quant level is sanctioned for production on this machine.

---

## PART 4 — QUANTIZATION SCIENCE (HARD-WON)

### Core Finding — Quantization Destroys QLoRA Below a Threshold

**14B models:** q8_0 is the minimum that preserves LoRA fine-tuned weights. q4_k_m and q5_k_m completely scramble trained knowledge.

**7B / 8B models:** Even q8_0 destroys the subtle LoRA adjustments. 7B QLoRA requires **f16 deployment, Q6_K with imatrix protection, or runtime LoRA via llama-server** — never naive q8_0.

### Proof Matrix (identical model, different pipeline stages)
| Method | Siblings test | Grand Canyon test | Accuracy |
|---|---|---|---|
| Python direct (no GGUF) | CORRECT | CLEAN | ~80% |
| f16 merged GGUF | CORRECT | CLEAN | ~80% |
| q8_0 quantized (7B) | SCRAMBLED | CONTAMINATED ("Tammy's wedding venue") | ~20% |
| q4_k_m / q5_k_m (14B) | RANDOM hallucinated names (French-Canadian, even Chinese) | — | 0% |
| Q6_K + imatrix | CORRECT | CLEAN | ~80% |
| llama-server runtime LoRA | CORRECT | CLEAN | ~80% |
| System prompt only (no LoRA) | CORRECT | CLEAN | 100% |

### Root Cause of the Merge-Quant Failure
Base GGUF extracted from Ollama was Q4_K quantized. The merge pipeline was:
1. Dequantize Q4_K base → F32
2. Add LoRA weights at F32
3. Output as F16
4. Requantize to Q8_0

The dequant→merge→requant chain introduces cumulative rounding errors. Tiny LoRA weight adjustments get rounded away at the Q8 stage because they were already degraded by the Q4 base dequantization.

### Diagnostic Rule
If a model answers correctly in Python (Unsloth direct inference) but hallucinates through Ollama/quantized GGUF, the problem is the **pipeline, not the training**. Always test with Python direct inference before retraining.

---

## PART 5 — WORKING QLoRA → GGUF → DEPLOYMENT PIPELINE

### One-Time Base Preparation
```powershell
# 1. Convert HF safetensors base to F16 GGUF
python convert_hf_to_gguf.py D:\Jarvis\qlora\models\Qwen3-8B\ `
  --outfile qwen3-8b-f16.gguf --outtype f16

# 2. Generate imatrix from calibration text (training JSONL + 50–100 lines general text to prevent overfit)
.\llama-imatrix.exe -m qwen3-8b-f16.gguf -f calibration.txt -o jarvis_imatrix.dat

# 3. Quantize with imatrix protection
.\llama-quantize.exe --imatrix jarvis_imatrix.dat qwen3-8b-f16.gguf qwen3-8b-Q6_K.gguf Q6_K
```

### Per-Training-Run
```powershell
# 1. STOP Docker — it holds GPU memory and will cause "No or negligible GPU memory available for fused cross entropy"
docker stop ollama openwebui searxng 2>$null
Stop-Process -Name "Docker Desktop" -Force -ErrorAction SilentlyContinue

# 2. Activate venv and train (always from clean base — training on top of an existing LoRA does NOT override; old weights dominate)
D:\Jarvis\qlora\venv\Scripts\Activate.ps1
python D:\Jarvis\qlora\train_jarvis_7b_v[N].py

# 3. Convert LoRA to GGUF
python C:\Users\ericl\.unsloth\llama.cpp\convert_lora_to_gguf.py `
  --base D:\Jarvis\qlora\models\Qwen3-8B `
  --outtype f16 `
  D:\Jarvis\qlora\output\jarvis_7b_lora_v[N]
```

### Deployment — Runtime LoRA via llama-server (CLEANEST PATH)
```powershell
.\llama-server.exe `
  -m qwen3-8b-Q6_K.gguf `
  --lora jarvis_7b_lora_v[N]-F16-LoRA.gguf `
  --port 8080 -c 8192 -ngl 99
```
No merge, no requantization of trained weights. This is the canonical deployment.

### Legacy Merge Path (only if runtime LoRA unavailable — DO NOT use for 7B)
```powershell
# Merge LoRA into base
& llama-export-lora.exe -m base.gguf -o merged.gguf --lora lora-F16-LoRA.gguf

# Quantize merged file — --allow-requantize flag MANDATORY
# (merged file has mixed tensor types f32/f16/q4_K/q6_K from the base)
& llama-quantize.exe --allow-requantize merged.gguf out-q8.gguf q8_0
```

### Tool Paths
| Tool | Path |
|---|---|
| llama-server.exe | `D:\Jarvis\llama.cpp\llama-server.exe` (NOT `D:\llama.cpp\`) |
| llama-quantize.exe | `C:\Users\ericl\.unsloth\llama.cpp\build\bin\Release\` |
| llama-export-lora.exe | `C:\Users\ericl\.unsloth\llama.cpp\build\bin\Release\` |
| llama-imatrix.exe | `C:\Users\ericl\.unsloth\llama.cpp\build\bin\Release\` |
| convert_hf_to_gguf.py | `C:\Users\ericl\.unsloth\llama.cpp\` |
| convert_lora_to_gguf.py | `C:\Users\ericl\.unsloth\llama.cpp\` |

### Build Versions
- **llama.cpp current build:** b8639 (updated April 3, 2026)
- CMake required to build llama-export-lora (`winget install Kitware.CMake`)

---

## PART 6 — TRAINING LINEAGE & LESSONS

### 14B Training Rounds (Round 1 → Round 3)
| Round | Data | Params | Loss | Result |
|---|---|---|---|---|
| R1 | 3,318 records (83% emails) | r=16, 3 epoch | 3.458 → 0.061 | Learned email voice, not facts — email data dominated |
| R2 | 67 brain records *trained on top of R1* | r=16, 3 epoch | Dropped | Still hallucinated — R1 weights dominated |
| R2-Clean | 67 records from fresh base | r=16, 5 epoch, 85 steps | 4.47 → 0.72 | Still hallucinated at q4 (quant was culprit) |
| **R3 (winner)** | 67 records, fresh | **r=64, 10 epoch, 170 steps** | 4.47 → 0.598 | All 4 siblings correct at q8; APE and cabin flawless |

**14B lesson:** rank 16 (0.43% of parameters) insufficient. rank 64 (1.7% of parameters) with 10 epochs required to make knowledge survive quantization.

### 7B Training Rounds (v1 → v11) — 11 Failures Before System-Prompt Pivot
| Ver | Records | Key Change | Loss | Result |
|---|---|---|---|---|
| v1 | 67 | Single Q&A flashcards | 0.052 | Scrambled. Invented "Maurice" |
| v2 | 117 | Anti-scrambling pairs | 0.064 | Direct Q correct, read rules aloud |
| v3 | 118 | Natural tone (BEST HAND DATA) | 0.064 | 5/5 direct, cross-ref failed |
| v4 | 105 | Prose format | 0.056 | Cross-ref still failed |
| v5 | 356 | Multi-turn auto-gen ($1 via Claude API) | 0.076 | Catastrophic forgetting — Grand Canyon became "Route 66" |
| v6 | 118 | r=32, lr=1e-4 | 0.73 | Grand Canyon became "wedding venue" |
| v7 | 158 | Q/V only + 40-record replay buffer | 2.134 | Too weak — invented Patrick/Jean |
| v8 | 158 | QKVO 4 modules | ~1.8 | Middle ground, still contaminated |
| v9 | 191 | Grossmann method | 0.72 | Denika = Randy's daughter correct; kids still swapped |
| v10 | 201 | Sibling sorter + count anchors | ~0.7 | Randy correct; Elissa/Denika copied everywhere |
| v11 | ~200 | Rule of 5, dropout 0.1, fresh LoRA | ~0.7 | Still swapping kids between siblings |
| **SP** | N/A | **System prompt with family table** | N/A | **6/6 PERFECT** |

### Core Architectural Finding
**Relational knowledge (family trees, parent→child) CANNOT be reliably baked into 7B weights.** After 11 runs using every known technique, the model consistently cross-wires relationships. The winning architecture separates layers:
- **System prompt** = facts (100% accurate, always in context)
- **LoRA** = personality (tone, humor, phrasing, movie references)
- **Jigsaw XML injection** = structured relational data retrieved on demand
- **RAG (future)** = scalable document retrieval for 50+ clients, manuals, soil reports

### Catastrophic Forgetting — Research Findings
- Forgetting increases as a shifted power law in parameters fine-tuned × update steps
- CANNOT be avoided by early stopping or parameter count alone
- Replay buffer (mixing general knowledge into training data) is the proven mitigation
- **Recommended ratio: 70–75% domain data, 25–30% general knowledge**
- Targeted adapters (Q/V only or QKVO) disrupt base knowledge less than all 7 modules
- Model merging (SLERP) is an option for future work

### Training Rules — Hard-Won
1. Always train from a CLEAN base — never resume on an existing LoRA (old weights dominate).
2. ALWAYS stop Docker before training — Ollama container grabs GPU memory.
3. Docker Desktop must be running before any `docker` command (otherwise "failed to connect to docker API") — use `Start-Process` + `Start-Sleep 45`.
4. ChatML TEMPLATE in Modelfile is mandatory — without `im_start`/`im_end` the model loops infinitely generating garbage.
5. `repeat_penalty 1.8` needed on Modelfiles (without it model repeats phrases endlessly).
6. All three stop tokens required: `<|im_end|>`, `<|im_start|>`, `<|endoftext|>`.
7. `--allow-requantize` flag MANDATORY when quantizing a merged file (mixed tensor types).
8. Ollama 0.18.0 does NOT support runtime LoRA — `ADAPTER` directive with safetensors has a known bug (`adapter_config.json` not found regardless of file location); `ADAPTER` with GGUF LoRA returns "loras are not yet implemented." Use llama-server instead.

---

## PART 7 — GROSSMANN TRAINING PLAYBOOK (Relational Data)

### The 10 Commandments
1. **Rule of 5** — equal weight per entity (5 mirrored records each)
2. **Full-name anchoring** — "Denika Legault" always, never just "Denika"
3. **Third-person records** — 30–40% without first-person perspective
4. **Count anchors** — "father of TWO" vs "father of FOUR"
5. **Entity isolation** — never mention Entity A in Entity B's records
6. **CoT think tokens** — Qwen3 native thought blocks for collision points
7. **Variable phrasing** — same fact, different words (prevents wallpaper effect)
8. **Dropout 0.1** — forces robust neural pathways
9. **Lower learning rate** — 8e-5 for relational data
10. **Shuffle everything** — random distribution, never cluster

### Anti-Patterns — NEVER DO
- Negative denial ("X is NOT Y's daughter") — fires wrong neurons together
- Anti-scrambling pairs ("Is X related to Y? No") — builds bridges not fences
- Unbalanced representation — dominant branch becomes default
- Master table of all entities — positional encoding blur
- 100% first-person data — ego-centric bias
- Auto-generation without replay buffer — catastrophic forgetting

### Key Concepts
- **Ego-centric bias** — single-perspective data anchors everything to primary subject
- **Symmetric collision** — similar entities (both brothers, both same surname) overlap in semantic space
- **Pink Elephant effect** — denying an association trains the association
- **Hebbian learning** — neurons that fire together wire together (applies to artificial networks)
- **Semantic gravity** — pattern extraction requires reasoning capacity that exceeds 14B latent space for certain tasks

### WEAP Guardrail (Grossmann)
Exact N-values only. No averaging. UNDEFINED for missing data. No inference beyond data.

---

## PART 8 — MODEL BEHAVIOR LAB RESULTS

### 14B vs 9B Comparison (April 2, 2026 — measured)
| Test | 14B Q6_K | 9B Claude-Distilled Q6_K |
|---|---|---|
| VRAM headroom | 1,356 MiB | 6,751 MiB |
| 76 people cards @ 16K ctx | PASS — 25 sec | PASS — 37 sec |
| 76 people + 316 clients payload | FAIL (overflow) | PASS — 100 sec |
| Family relationship accuracy | 5/7 (fast) | 5.5/7 (slower) |
| Inference beyond data | No (safer for CRM) | Yes (inferred "half-brothers") |

**Decision:** 14B = everyday fast hat for small queries. 9B = CRM powerhouse for full dataset. Hat-swap on port 8080.

### 14B Context Behavior
- **16,384 confirmed stable** for normal inference load (April 2 retest)
- **WARNING:** Do NOT run extraction-heavy prompts at 16,384 on 14B — headroom is only 1,356 MiB. March 31 test crashed GPU driver and forced reboot at this setting. Safe for inference, unsafe for extraction.
- 8192 is no longer the ceiling; document any older references as superseded.

### 14B Extraction Ceiling (Queen Finding)
- 14B cannot identify value shifts or strategic overrules in conversational text
- Pattern-count ceiling: sees storage/file ops, misses architecture decisions
- Schema Priming (XML pattern injection) did NOT overcome this ceiling
- Confirmed by Grossmann as "semantic gravity exceeds 14B latent space"
- **14B safe zone: Janitor-class tasks only** (storage, file moves, deletions, archiving)
- Deep-extraction tasks must route to 9B or higher

### Gordon Extraction Failure (March 31)
- Gordon (Docker Haiku) created 32 empty .md files — template generation, not extraction
- Gordon admission: "This wasn't extraction, it was template generation with your filenames attached"
- Gordon later crashed, looped "I understand the project" 13 times without executing
- **Verdict:** Gordon (Haiku) cannot perform deep-reading extraction. Restrict to infrastructure, containers, file ops.

### Opus vs Sonnet Extraction Benchmark (April 1)
Controlled test: 406 KB session file split into two ~203 KB chunks.
| Test | Worker | Chunk | Entries Found | Session Cost | Time |
|---|---|---|---|---|---|
| 1 | Opus | Chunk 1 | 118 | 8% | 7m51s (hit turn limit once) |
| 2 | Sonnet | Chunk 2 | 99 | 3% | 7m00s |
| 3 | Sonnet | Same chunk 1 | 87 | 4% | — |

**Verdict:** Sonnet costs ~half the tokens and finds ~74% of entries. Sonnet is The Analyzer. Opus reserved for War Room and deep architecture only.

### War Room Reading Cost
Reading a 4 KB extraction report = ~1% session.

---

## PART 9 — INFRASTRUCTURE & BOOT

### Ports
| Service | Port | Type | Notes |
|---|---|---|---|
| Flask app | 5001 | Host Python | Jigsaw injection, web UI |
| llama-server | 8080 | Host .exe | Inference engine |
| Chatterbox TTS | 8004 | Docker container | Adrian voice output |

### Docker Boot Sequence (19-Second Auto-Start)
**Script:** `D:\Jarvis\DockerBootSequence.ps1`
**Scheduled task:** `DockerBootSequence` at system startup

Proven sequence — resolves the Docker/WSL2 race condition that plagued earlier builds:
1. Kill lingering Docker Desktop processes
2. `wsl --shutdown` — cleanly terminate WSL2 VM
3. Wait 5 seconds for WSL to fully die
4. Kill `vmmem` to confirm VHDX released
5. Wait 3 seconds for file handle release
6. Launch Docker Desktop (`C:\Program Files\Docker\Docker\Docker Desktop.exe`)
7. Poll `vmmem` death up to 30 seconds (every 2 seconds)
8. Poll `docker ps` every 5 seconds up to 120 seconds until engine responds
9. Auto-start llama-server and Flask as hidden background processes
10. Log to `D:\Jarvis\logs\boot_sequence.log`

**Docker Desktop removed from HKCU Run registry key** (March 30) — scheduled task handles startup deterministically.

**Known issues:**
- Recovery boot once had empty PID at Step 7 for llama-server — needed manual launch. Reliability on cold boot flagged for verification.
- Smart App Control (Windows Security) can block `llama-server.exe` — disable under App & Browser Control if service fails to start.

**Full manual recovery:** `D:\Jarvis\JARVIS_FULL_STARTUP.ps1` (needs path update — chatterbox container name and llama-server path require verification).

### Active Components
| Component | Type | Details |
|---|---|---|
| chatterbox-tts-server:cu128 | Docker container | Adrian voice, port 8004, auto-starts with Docker |
| llama-server.exe | Host .exe | Port 8080, `D:\Jarvis\llama.cpp\llama-server.exe` |
| jarvis_flask.py | Host Python | Port 5001, 531 lines, `D:\Jarvis\jarvis_flask.py` |

### VHDX Compaction Result (March 30)
Docker virtual disk: **318 GB → 10.8 GB** — 307 GB reclaimed. Chatterbox TTS image wiped during compact; rebuilt from `Dockerfile.cu128`. Golden Images backed up to `H:\Golden_Images\`.

Total D: reclaimed March 30: ~370 GB (VHDX 307 + Ollama 12.44 + OpenWebUI 3.28 + 54 GB dead databases moved to H:\Gordons Stable\).

---

## PART 10 — JIGSAW XML INJECTION SYSTEM

### Three-Layer Knowledge Architecture
- **Layer 1 — System Prompt (facts):** Family tree, de-conflation rules, `{{CURRENT_DATETIME}}` injection, domain-specific facts per instance. Compressed from 12,794 tokens → ~800 tokens via Jigsaw.
- **Layer 2 — LoRA Weights (personality):** Tone, humor, phrasing, movie references. Baked into v13. NOT facts.
- **Layer 3 — Jigsaw XML Injection (relationships):** Flask loads relevant cards BEFORE sending to llama-server.

**RAG: permanently retired.** Jigsaw XML injection is superior — structured, queryable, deterministic, instant reload, zero hallucination on relationships.

### Index Files
- **people_index.py:** 86 keyword entries, 3-layer retrieval
  - Layer 1: exact name match
  - Layer 2: relationship keyword match ("Randy's daughter")
  - Layer 3: full fallback XML scan
- **ape_index.py:** 155+ entries (expanded March 30 with 75 new entries) — equipment models, specifications, companies, techniques
- **Client index:** 309 cards across 113 company folders (confirmed April 3, 2026 — dedup complete)

### Card Counts (current — April 2, 2026)
| Domain | Count |
|---|---|
| People XML cards | 76 (was 73 — added bonnie_puhakka, pat_goulard, mikey_poirier) |
| Client XML cards | 309 (confirmed April 3, 2026 — dedup complete) |
| Client company folders | 113 (was 121 — 5 duplicate folders merged) |
| APE equipment folders | 71 |
| wiggy_equipment XMLs | 1,093 (dirty UTF-8 — future cleanup) |
| APE equipment chunked XMLs | 20 |

### XML Card Standards
```xml
<PERSON>
  <NAME>Full Name</NAME>
  <RELATIONSHIP>Primary-qualifier</RELATIONSHIP>
  <RELATION_TYPE>Primary</RELATION_TYPE>
  <RELATION_DETAIL>How connected</RELATION_DETAIL>
  <SIBLINGS>…</SIBLINGS>
  <PARENTS>…</PARENTS>
  <BIRTHDATE>YYYY-MM-DD</BIRTHDATE>
  <LOCATION>…</LOCATION>
  <CONTACT>…</CONTACT>
  <NOTES>…</NOTES>
</PERSON>
```

**Relationship format:** Primary first, qualifier after hyphen (`Uncle-maternal`, `Nephew-great`, `Nephew-in-law`).

**Inlaws folder structure:** Split into `parent_inlaws`, `sibling_inlaws`, `nephew_inlaws`, `future_inlaws`.

**Client card format:** `<CLIENT>` with `FULL_NAME` (uppercase), `ADDRESSED_AS`, `MOBILE_PHONE`, `CURRENT_COMPANY`, `JOB_TITLE`, `EMAIL`, and additional fields. Phone numbers standardized to dash format.

### Grossmann Jigsaw Decision (April 2)
Family grouping logic belongs in **people_index.py**, not the LLM. When user says "nephews," Jigsaw queries XML for all `RELATIONSHIP` containing `Nephew` and injects all matching cards. The model answers from what it sees — it does NOT reason family tree logic from `RELATIONSHIP` tags.

### Hat-Swap Architecture
Flask kills and reloads llama-server with different XML hat configs in 5–15 seconds. Same port (8080), different model/context. Dashboard becomes mission control with hat buttons; browser tab + header show which hat is loaded.

**Planned hats:** Everyday (14B), APE Worker, WEAP Analyst (9B), Mechanic, Provisioner, Client Comms (9B).

---

## PART 11 — TOKEN GOVERNANCE

### Measured Costs (April 1, 2026)
| Operation | Cost |
|---|---|
| Opus: 200 KB chunk extraction | ~8% session |
| Sonnet: 200 KB chunk extraction | ~3–4% session |
| War Room reading 4 KB report | ~1% session |

### Session Rules
- Session resets approximately every 5 hours
- Weekly reset: Saturday 9 PM
- Sonnet has a separate token pool from Opus (confirmed independent)
- **Never deploy Analyzer above 40% session meter**
- **Claude Code parallel agents: PERMANENTLY BANNED** — burned full daily token allowance in 12 minutes
- **Claude Code and Claude Web share the same token pool** — running Code starves Web access
- Claude Code: single file at a time, surgical strikes only

### Worker Model Assignments
- **Opus (Claude Web):** War Room, deep architecture, complex decisions — protect these tokens
- **Sonnet:** Analyzer extraction, bulk reading tasks — cheap and capable
- **Gordon (Docker Haiku, claude-haiku-4-5-20251001):** Infrastructure, Docker, file ops only — NOT extraction. Docker pays the bill (~$0.01/query)
- **Mason (Claude API via Queen.ps1):** Playbook execution, bulk work — Haiku recommended for cost
- **Claude Code:** Single-file surgical strikes from `H:\Koonie\`

### Multi-Session Workers
Gordon and Mason can each run multiple simultaneous Docker sessions, each with a role-specific handoff — pure focus, no confusion.

---

## PART 12 — POWERSHELL TRAPS

### Critical: curl Alias
PowerShell aliases `curl` to `Invoke-WebRequest`. It is NOT real curl — JSON POST bodies fail silently. Always use `Invoke-RestMethod`:
```powershell
# WRONG
curl http://localhost:8080/v1/models

# RIGHT
Invoke-RestMethod -Uri "http://localhost:8080/v1/models" -Method Get

# RIGHT with JSON body
Invoke-RestMethod -Uri "http://localhost:5001/chat" -Method Post `
  -ContentType "application/json" `
  -Body '{"message": "test"}'
```

### Other Traps
- `Join-Path` takes ONLY 2 arguments — multi-segment joins must chain or use `-ChildPath`
- `$var:` breaks in double-quoted strings — use `${var}` instead
- Claude Code on Windows: terminal paste unreliable; use `--dangerously-skip-permissions` flag for uninterrupted execution
- Smart App Control can block `llama-server.exe` and training scripts — disable in Windows Security if needed
- Gordon (Docker) and Claude Code cannot communicate directly (Docker isolation) — use file-based relay via `H:\Koonie\tasks\CLAUDE_CODE_TASK.md`

---

## PART 13 — CREDENTIALS & ENVIRONMENT

### HF_TOKEN
- Set at **Machine level** — confirmed working
- Token name: `Jarvis` (READ permissions)
- Required for full HuggingFace download speed (throttled to ~3 MB/s without it)
- Without token: HF downloads crawl; with token: full bandwidth

### API Keys
- Anthropic API key disabled in console (March 30) — Queen runs localhost llama-server
- API key saved at `D:\Jarvis\config\api_key.txt` from `ANTHROPIC_API_KEY` environment variable (Mason auto-start status NEEDS VERIFICATION)

---

## PART 14 — NETWORK LOCATIONS

| Location | Connection | Speed | Status |
|---|---|---|---|
| APE Office (Nisku) | Rogers fibre | 750 mbps | Live April 1, 2026 |
| Farm (Beaumont) | Xplore 5G | 500 mbps | Live April 2, 2026 |
| Ontario house | — | 300 mbps | Active |
| Northern Ontario property | Starlink | — | Active |
| Cabin | Off-grid PTO generator | — | Jarvis runs local, no internet |

### Deployment Principles
- All processing on WIGGYS-BEAST
- No cloud dependency (models fully local)
- No API keys for Jarvis runtime (local llama-server + local Flask)
- Off-grid capable — Jarvis works in the bush, northern Ontario
- Full privacy — conversations never leave the machine

---

## PART 15 — EXTRACTION PIPELINE LAB NOTES

### Working Extraction Stack
- **Analyzer:** Sonnet (cheap, thorough, 74% recall vs Opus at 50% the cost)
- **Output:** `D:\Jarvis\brain\knowledge\extracted\` (8 categories)
- **Patterns:** `D:\Jarvis\brain\knowledge\extraction_patterns.xml` (15 Grossmann pattern cards)
- **Task sheets:** Explicit instructions mandatory — "Do NOT produce a Science Sheet. No questions. Just results." Abbreviated task sheets fail; `ANALYZER_HANDOFF.md` works.

### Known Extraction Quality Failures
- Gordon Haiku: template generation, not extraction. Permanently removed from extraction duty.
- 14B Queen: cannot identify strategic/architectural shifts in conversational text. Janitor-class only.
- Claude Code parallel agents: burned daily tokens in 12 minutes. Banned.

---

## PART 16 — NEEDS VERIFICATION (Open Items)

Items flagged — do not delete, require Wiggy review or lab confirmation:

1. **Gemma 4 E4B** — Listed as champion model with ~8,206 MiB VRAM. File path, deployment status, hat assignment not documented. Verify current state.
2. **GLM-Z1-9B** — Listed as math specialist. File path not documented. Verify if downloaded and deployed.
3. **llama.cpp build number conflict** — v2 sheet says `b8639` (April 3); earlier lab notes reference `b4639`. Reconcile which is canonical.
4. **JARVIS_FULL_STARTUP.ps1 path update** — Referenced `D:\llama.cpp\` does not exist; correct path is `D:\Jarvis\llama.cpp\`. Chatterbox container name also needs verification.
5. **llama-server cold-boot reliability** — One recovery boot had empty PID at Step 7 (had to launch manually). Cold-boot all-services test required.
6. **Flask cold-boot reliability** — Same concern. Cold boot and confirm Chatterbox + llama-server + Flask all come up without manual intervention.
7. **people_index.py entry count** — Documented as 86 entries; 3 new cards added (Pat Goulard, Mikey Poirier, Bonnie Puhakka). Confirm index updated.
8. **wiggy_equipment UTF-8 cleanup** — 1,093 dirty UTF-8 XMLs. Future cleanup task.
9. **Docker Business / Gordon account** — Case #00202864 resolved per task sheet, but session log said "waiting for backend switch." Gordon currently on Personal account (wiggstar) while Business (wiggonator) syncs. Confirm current state.
10. **Extraction pipeline merge** — `extracted_claude_test\` 32 files: merged into main `extracted\` folder? 11 remaining Claude sessions + 4 ChatGPT JSONs still unprocessed.
11. **Mason auto-start / API key** — Current status of Mason deployment unclear.
12. **PST to MBOX conversion** — 18 GB inbox pending — needs converter tool identified.

---

*MASTER SCIENCE SHEET v3.1 — Operational Reference*
*Deduplicated against D-Series governance (D-00 Domains, D-02 Index, D-04 Spine, D-07 Folder Map, D-08 MCP, D-09 Quote Engine, D-MB Master Build). File paths that duplicate D-07 are omitted; governance content belongs to D-01/D-43.*
*Family data, personality quotes, standing-order tone rules, and Ideas Vault contents have been removed — those live in their respective canonical sources.*
