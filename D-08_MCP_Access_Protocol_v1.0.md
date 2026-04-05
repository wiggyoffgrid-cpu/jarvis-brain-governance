# D-08 — MCP Access Protocol

**Version:** 1.0
**Status:** Active
**Created:** April 4, 2026
**Authority:** Wiggy (Eric Legault)

---

## Purpose

This doctrine defines how AI workers connect to the Jarvis Brain. It establishes the three access paths, their permissions, and the tier-based security model. No AI accesses the brain outside these protocols.

---

## The Three Doors

The Jarvis Brain has three access methods. Each AI connects through exactly one door.

### Door 1: MCP Filesystem Server (Read/Write)

**Who uses it:** All Cowork projects (Director, Neurologist, Surgeon, Codex, Assistant), Dispatch (via Cowork proxy)

**How it works:**
- Node.js MCP filesystem server (@modelcontextprotocol/server-filesystem)
- Config file: %APPDATA%\Claude\claude_desktop_config.json
- Serves D:\Jarvis\brain\ with full subdirectory access
- Read AND write access — Cowork projects can create, edit, and read files

**What's exposed:**
- governance\ (D-Series, audit_logs, Command Library, Science Sheet, Strategic Planning)
- knowledge\ (APE clients, APE equipment, extracted, wiggy_equipment)
- mail_cart\ (inter-project relay)
- Ideas Vault\ (ideas and future plans)
- archive\ (D-45 with manifest)
- memory\ and training_data\ and Chat History\

**What's NOT exposed:**
- D:\Jarvis\brain\knowledge\people\ — NOT included in MCP server config (Tier 1 protection)
- C:\ drive — never, sacred
- E:\, F:\, G:\, H:\ drives — not served

### Door 2: Cloudflare Tunnel (Read Only)

**Who uses it:** Director Claude Web (browser), Grossmann (Google AI), any AI with web_fetch that Wiggy authorizes

**How it works:**
- Python HTTP server (jarvis_brain_server.py) on localhost:8009
- Cloudflare named tunnel "jarvis-brain" exposes it to the internet
- Permanent URL: https://brain.wiggyoffgrid.com
- Domain: wiggyoffgrid.com (registered April 4, 2026, expires April 4, 2036)

**Permissions:**
- GET only — PUT, POST, DELETE, PATCH all return 405
- Read-only access to all served paths
- Tier 1 protection: /knowledge/people/ returns 403 Forbidden

**Infrastructure:**
- Server script: D:\Jarvis\scripts\jarvis_brain_server.py
- Tunnel client: D:\Jarvis\scripts\cloudflared.exe
- Tunnel config: D:\Jarvis\scripts\config.yml
- Tunnel ID: 035f3d53-86ab-4a4f-a22e-dd8d87cc1be8
- Credentials: C:\Users\ericl\.cloudflared\035f3d53-86ab-4a4f-a22e-dd8d87cc1be8.json

### Door 3: Flask Jigsaw Injection (Read Only, Filtered)

**Who uses it:** Local models (Qwen, Gemma, GLM, DeepSeek) via llama-server

**How it works:**
- Flask app (jarvis_flask.py) on port 5001
- Reads question, routes to correct domain, loads only relevant XML cards
- Model gets focused context — not the whole brain
- Jigsaw XML injection — domain-aware card loading

**What's exposed:** Only the cards relevant to the current question, filtered by domain routing.

---

## Tier-Based Security Model

Access is governed by the D-00 Domain Structure tiers:

| Tier | Domains | MCP (Door 1) | Tunnel (Door 2) | Flask (Door 3) |
|------|---------|--------------|-----------------|----------------|
| Tier 1 (Wiggy Only) | D-10 People, D-11 Personal | BLOCKED | 403 Forbidden | Filtered by domain |
| Tier 2 (Trusted Workers) | D-00–D-07 Governance, D-20–D-21 Equipment | Full access | Read only | Filtered by domain |
| Tier 3 (Operational) | D-12 Clients, D-40–D-45 Ops | Full access | Read only | Filtered by domain |
| Tier 4 (Public/Shared) | D-50+ External | Full access | Read only | Filtered by domain |

**Tier 1 Enforcement:**
- MCP server config excludes D:\Jarvis\brain\knowledge\people\ entirely
- Brain server returns 403 for any request to /knowledge/people/
- Flask only loads people cards when the domain routing explicitly calls for them
- Only Wiggy reads and writes people cards directly

---

## Known Issue: web_fetch Cache and 401 Errors

**Discovered April 4, 2026.** Basic auth was tested on the brain server and then removed. However, web_fetch tools cache responses — so files that returned 401 during the auth test continued returning 401 after auth was removed from the server.

**How to diagnose:** If you get a 401 on a specific file, try fetching a different file you've never fetched before. If the new file loads fine, the server has no auth — your tool is serving a cached 401. Wait for the cache to clear (up to 15 minutes) or append a query string like `?v=2` to bust the cache.

**Do NOT:** Ask Wiggy to restart the server, modify the script, or change the tunnel config. If other files load, the server is fine. The problem is on your end.

**For the record:** Basic auth was removed because web_fetch tools (Claude Web, Grossmann) cannot send authentication headers. Path-based 403 blocking is the security layer instead.

---

## Standing Orders

1. **No AI modifies people cards.** Tier 1, D-10. Wiggy only. Always.
2. **No AI deletes files** without Wiggy's explicit approval.
3. **No AI modifies D-00 through D-07** governance documents. Read only.
4. **The tunnel is read-only.** No write path exists through brain.wiggyoffgrid.com.
5. **MCP write access** is granted to Cowork projects for operational files (mail_cart, Ideas Vault, etc.) but NOT for governance or people data.
6. **Credentials stay secret.** The tunnel credential JSON and config.yml are never shared, never committed to public repos, never exposed through the tunnel itself.
7. **Wiggy is the gatekeeper.** No new AI gets tunnel access without Wiggy's approval. No new MCP paths without Wiggy's approval.

---

## Phase 2 Planned Enhancements

- Basic authentication on brain.wiggyoffgrid.com (username/password)
- Path-based access control per AI worker (different AIs see different paths)
- Auto-start script for brain server + cloudflared on Beast boot
- Access logging — who fetched what and when
- Rate limiting to prevent abuse

---

## Relationship to Other Doctrines

- **D-00 Domain Structure:** Defines the tiers that D-08 enforces
- **D-01 Governance Charter:** Authority model that D-08 operates under
- **D-02 Operational Index:** D-08 must be registered here
- **D-05 File Architecture:** Naming rules for scripts and config files
- **D-07 Folder Map:** Physical truth of what D-08 serves

---

*"Care for what sustains you, and it will sustain you in return." — Wiggy*
*"Does Eatons tell Sears their business?" — Koonie*
*Go Leafs Go.*
