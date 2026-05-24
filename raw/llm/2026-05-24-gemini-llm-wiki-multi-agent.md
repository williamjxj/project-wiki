---
type: llm-chat
source: gemini
topic: "LLM-Wiki pattern in multi-agent dev"
date: 2026-05-24
status: ingested
question: "Comprehensive evaluation of LLM-Wiki pattern for multi-agent software development"
url: "https://gemini.google.com/share/ad57a239d2d5"
---
## Comprehensive Evaluation and Implementation Framework for the LLM-Wiki Pattern in Multi-Agent Software Development

The transition from stateless prompt-response loops to stateful, compounding knowledge architectures represents a major milestone in software engineering methodology. Standard Retrieval-Augmented Generation (RAG) systems operate on an ephemeral, run-time basis, requiring models to segment, vectorize, and rediscover the same source documents repeatedly with every query. This repetitive processing incurs significant token overhead, introduces context dilution, and fails to retain any analytical progress across separate chat sessions.

The developer's proposed six-step workflow directly addresses this bottleneck by establishing an intermediate, compiled, and compounding knowledge layer: the LLM-Wiki. Rather than forcing downstream development agents to directly parse raw, contradictory brainstorming transcripts from multiple models, the proposed workflow compiles these diverse inputs into a structured markdown database first. This architecture organizes, cross-references, and refines the conceptual domain, creating a single, coherent technical baseline before initiating code generation.

## Architectural Validation of the Proposed Six-Step Developer Loop

The proposed methodology is highly practical and aligns with the current shift toward agent-guided software engineering. By separating the initial research phase from the active code implementation phase, the developer establishes a clear division of labor between exploratory knowledge gathering and deterministic code output.

```markdown
+--------------------------------------------------------------------------------------------------+
|                                  PHASE I: EXPLORATION & HARVESTING                               |
|                                                                                                  |
|  +--------------------+      +--------------------+      +--------------------+                  |
|  |    Claude Chat     |      |    ChatGPT Chat    |      |    Gemini Chat     |                  |
|  +---------+----------+      +---------+----------+      +---------+----------+                  |
|            |                           |                           |                             |
|            +---------------------------+---------------------------+                             |
|                                        |                                                         |
|                                        v                                                         |
|                          +---------------------------+                                           |
|                          |   Multi-Model Transcripts |                                           |
|                          +-------------+-------------+                                           |
|                                        |                                                         |
+----------------------------------------|---------------------------------------------------------+
                                         |
+----------------------------------------|---------------------------------------------------------+
|                                  PHASE II: KNOWLEDGE COMPILATION                                 |
|                                        v                                                         |
|                          +---------------------------+                                           |
|                          |    Two-Stage Compiler     | <---+ Directed by:                        |
|                          |   (Analysis & Ingestion)  |     | - schema.md [2]                  |
|                          +-------------+-------------+     | - purpose.md                  |
|                                        |                   +                                     |
|                                        v                                                         |
|                          +---------------------------+                                           |
|                          |    Compounded LLM-Wiki    | <---+ Structured as:                      |
|                          |     (Obsidian Vault)      |     | - concepts/ [2]                  |
|                          +-------------+-------------+     | - entities/ [2]                  |
|                                        |                   | - index.md [2]                   |
|                                        |                   +                                     |
+----------------------------------------|---------------------------------------------------------+
                                         |
+----------------------------------------|---------------------------------------------------------+
|                                  PHASE III: ACTIVE DEVELOPMENT                                   |
|                                        v                                                         |
|                          +---------------------------+                                           |
|                          |    Standardized Exports   |                                           |
|                          |   (llms.txt, Skills, MCP) | [10, 11, 12]                     |
|                          +-------------+-------------+                                           |
|                                        |                                                         |
|                                        v                                                         |
|                          +---------------------------+                                           |
|                          |    Developer IDE Agents   |                                           |
|                          | (Cursor, Claude Code, VS) |                             |
|                          +---------------------------+                                           |
|                                                                                                  |
+--------------------------------------------------------------------------------------------------+
```

### Deconstructing the Seven Architectural Phases of the Compiled Loop

The execution of this workflow is structured around seven distinct phases, moving from initial multi-model exploration to the final closed-loop log harvest.

- **Phase 1: Exploratory Gathering (Step 1):** The developer prompts multiple independent model architectures (Claude, ChatGPT, Gemini) to gather diverse perspectives, technical options, and edge cases for a given problem.
- **Phase 2: Immutable Logging (Step 2):** Raw chat logs and transcripts are saved as plain text files in a dedicated, read-only directory (`raw/`), preserving the original statements for future auditing.
- **Phase 3: Automated Ingestion & Distillation (Step 3 & 4):** A compiling model parses the raw folder. It filters out duplicate information, resolves structural conflicts, and organizes the unique material into markdown files with bidirectional links.
- **Phase 4: Synthesis & Verification:** The developer reviews the compiled database within Obsidian, examining the generated concepts, tracking structural relationships in the graph view, and running diagnostic checks to flag logical contradictions.
- **Phase 5: Context Export (Step 5):** The compiled repository is exported into highly dense, machine-readable formats like `llms-full.txt` or packaged as reusable agent skills.
- **Phase 6: IDE Execution (Step 6):** Developer tools (Cursor, VS Code, Claude Code) mount the compiled notes via the Model Context Protocol (MCP) or load the generated skill files. This ensures that all code-generation and planning tasks are guided by the pre-compiled architecture.
- **Phase 7: Closed-Loop Harvesting:** Interactive session transcripts from the active development tools are automatically exported and written back into the `raw/` directory, updating the wiki with real-world implementation logs.

By employing this pipeline, the developer avoids the common failure mode of feeding raw, unverified chat transcripts directly into coding agents, which often triggers hallucinated APIs and conflicting software patterns. Compiling the raw ideas into an organized intermediate database ensures that downstream code generators receive a single, verified technical reference.

## Optimizing the Ingestion and Distillation Phases

To prevent relationship hallucination, directory corruption, and information loss during ingestion, the compilation engine must use structured processing rules. Simple, single-pass prompts often fail when processing multi-megabyte transcripts. To ensure high-quality output, the system must split the ingestion phase into two distinct steps and apply dedicated intent-based steering.

| Operational Step | Executing Model Role | Processing Inputs | Concrete System Outputs |
| --- | --- | --- | --- |
| **Step 1: Structural Analysis** | Analytical Reviewer | Raw transcripts, existing wiki files, project roadmap (`purpose.md`). | Conceptual maps, detected architectural conflicts, and recommended wiki edits. |
| **Step 2: Generation & Integration** | Technical Writer | Analytical outputs from Step 1, structural guidelines (`schema.md`). | New and updated concept/entity markdown pages, bidirectional link updates, and log updates. |

### Implementing the Two-Stage Ingestion Pipeline

To protect the integrity of the database, the ingestion pipeline separates structural analysis from file generation.

- **Stage 1 (Structural Analysis):** The model analyzes the newly added raw sources alongside the current wiki index. It maps key conceptual entities, identifies technical overlaps, and notes any direct logical contradictions between the sources. No files are modified during this stage; the model outputs a structured blueprint of the required changes.
- **Stage 2 (Generation and Linkage):** The model executes the blueprint. It updates existing markdown documents, generates new concept and entity pages, establishes bidirectional links, and records the operations in `log.md`.

This separation ensures that file formatting and structural organization do not compete for model attention, preventing corrupted formatting and broken directories.

### Strategic Steering via purpose.md

Standard implementations of the LLM-Wiki rely on a behavioral schema file (typically `CLAUDE.md` or `schema.md`) to define file formats, folder conventions, and structural rules. However, to build a highly targeted technical solution, the system must also implement an intent-based guidance document, designated as `purpose.md`.

While the structural schema tells the agent *how* to build the wiki, `purpose.md` informs the agent *why* the wiki exists. It contains the overall thesis of the software project, the precise engineering goals, core architectural constraints, and the targeted research boundary. By forcing the compiling model to read `purpose.md` at the start of every ingestion cycle, the system prevents the knowledge graph from drifting into irrelevant topics, keeping the compiled data dense and focused.

## The Compounding Knowledge Layer

Traditional summaries are static, flat artifacts. They do not interact with other documents, cannot resolve contradictions, and quickly become obsolete as a project moves forward. In contrast, a compiling LLM-Wiki treats knowledge as a dynamic, interconnected graph where new information refines, validates, or updates existing concepts.

### Structuring the Knowledge Lifecycle

In an active software project, knowledge has a distinct, decaying lifecycle. Architectural decisions made during initial brainstorming are frequently superseded by concrete implementation details; libraries are upgraded, and transient debugging patterns lose utility over time. A static wiki that treats all statements as eternally valid quickly degrades into high-noise clutter. To counteract this, three explicit memory management techniques must be enforced:

1. **Decay-Weighted Confidence Scoring:** Every assertion written by the model should carry metadata containing its confirmation sources, creation date, and a decay-weighted confidence score. A claim that has been reinforced across multiple distinct ingestion sessions gains strength, whereas unreferenced or unvisited assertions gradually decay according to an exponential curve modeled on Ebbinghaus's forgetting principles.
2. **Systematic Supersession:** When a newly ingested document contradicts an existing claim, the system must not simply append the contradiction. The compiling agent must systematically mark the older claim as stale, append a timestamped link to the modern, overriding assertion, and archive the older version for historical auditability.
3. **Graph-Layered Entity Extraction:** Rather than maintaining a flat hierarchy of markdown documents, the compiling model must extract typed entities (such as `Project`, `Library`, `API_Contract`, or `Developer_Decision`) and establish explicitly typed semantic relationships. A link should not merely state that File A is related to File B; it must specify that "File A *depends\_on* File B" or "API\_Contract X *supersedes* API\_Contract Y," allowing coding agents to execute graph-traversal queries to trace downstream dependencies prior to generating code.

### Hierarchical Tree Indexing for Long Documents

Multi-model brainstorming sessions often generate very large text files that can easily exceed context limits or degrade retrieval quality. To handle long documents, the pipeline should bypass flat chunking and apply a tree-indexing algorithm, such as PageIndex.

```markdown
+-----------------------+
                         |   Long Document PDF   |
                         |   (> 20 Pages Long)   |
                         +-----------+-----------+
                                     |
                                     v
                         +-----------------------+
                         | Hierarchical Parser   |
                         | (Tree-Style Indexing) |
                         +-----------+-----------+
                                     |
            +------------------------+------------------------+
            |                        |                        |
            v                        v                        v
+-----------------------+ +-----------------------+ +-----------------------+
|    Section A Node     | |    Section B Node     | |    Section C Node     |
|  (Executive Summary)  | |  (Database Schema)   | |  (API Specification) |
+-----------+-----------+ +-----------+-----------+ +-----------+-----------+
            |                         |                         |
            v                         v                         v
+-----------------------+ +-----------------------+ +-----------------------+
|  Leaf A1 / Leaf A2    | |  Leaf B1 / Leaf B2    | |  Leaf C1 / Leaf C2    |
|  (Detailed Subsections)| |  (Table Definitions)  | |  (Endpoint Payloads)  |
+-----------------------+ +-----------------------+ +-----------------------+
```

When a document exceeds a set threshold (typically 20 pages), the system builds a hierarchical index. This tree index summarizes the document at multiple structural levels, mapping sections like database schemas, API specs, and deployment requirements to specific nodes.

Instead of searching a large volume of flat text chunks, the compiling model reads the high-level tree index to find the exact sub-sections it needs. This approach bypasses vector database overhead, keeps context windows clean, and ensures highly accurate data extraction.

## Active Integration with Agentic Dev-Tools

Once the brainstorming data is compiled and organized within the LLM-Wiki, the next phase (Steps 5 and 6 of the developer's proposed model) requires feeding this knowledge cleanly into active developer tools like Cursor, VSCode, or Claude Code. To maximize the effectiveness of this transition, the pipeline must utilize automated integration mechanisms rather than manual copy-paste protocols.

### Generating Machine-Readable Interfaces

To make the compiled knowledge base easily consumable by downstream coding agents, the system must automatically export the markdown files into standardized formats.

- **Standardized `llms.txt` Index:** Compiled at the root of the exported directory, this file provides a clean, machine-readable index of all available topics and pages, following the standard specification.
- **Flattened Context Dumps (`llms-full.txt`):** The system packages the entire compiled database into a single plain-text file, capped at 5 MB. This file contains all conceptual definitions, entity tables, and structural relationships, allowing developers to paste the entire project context into any model window in a single action.
- **JSON-LD Schema Graphs (`graph.jsonld`):** An exported knowledge graph of the database using semantic web schemas. This allows agentic tools to traverse the project's architecture programmatically using graph-queries.

These machine-readable exports ensure that downstream coding tools do not have to parse raw directories or lose time traversing complex, unmapped folder paths.

### Packaging Portable Agent Skills

A highly efficient mechanism for bridging compiled knowledge with agentic coding environments is the automated distillation of the wiki into portable developer skills. Using frameworks like OpenKB, the system can parse the compiled markdown database and compress designated thematic subdirectories into structured packages known as Anthropic Skills.

The compiled output (such as a standardized `SKILL.md` document loaded with metadata and behavioral rules) is placed in a local directory (e.g., `~/.claude/skills/`), which makes it immediately discoverable by execution interfaces like Claude Code. Consequently, instead of consuming massive token budgets by constantly reading hundreds of raw markdown files, the coding agent loads a highly dense, pre-compiled capability package that allows it to execute specialized code generations natively.

### Real-Time Interfacing via Obsidian MCP Servers

To enable active, bi-directional communication between the development environment and the compiled wiki, the developer should mount the Obsidian workspace directly to the coding agent via the Model Context Protocol (MCP). This approach bypasses the limitations of traditional vector-based RAG by exposing the filesystem as a structured set of resources and tools directly inside the IDE.

By running an MCP server designed for Obsidian (such as `cyanheads/obsidian-mcp-server` or `mcp-obsidian`) and linking it to the Obsidian Local REST API, developer tools like Cursor, Claude Code, or Codex gain direct access to the compiled vault. Rather than requiring manual human lookup, the coding agent programmatically invokes specialized tools :

- `obsidian_get_note` to retrieve precise structural sections of a compiled decision.
- `obsidian_patch_note` to surgically update specific frontmatter fields or markdown blocks as code requirements evolve.
- `obsidian_search_notes` to execute BM25-ranked lexical or semantic queries directly across the vault's directories without loading the entire corpus into context.

This real-time connection transforms the static wiki into an active second brain, allowing the coding agent to maintain strict alignment with the pre-established architecture.

## Closed-Loop Dev-Log Harvesting

To prevent technical debt and keep documentation in sync with real-world code, the workflow must include a closed-loop transcript harvester. As development tools execute terminal commands, modify files, and debug run-time errors, they write chronological conversation logs to local project directories.

| Development Interface | Default Local JSONL Directory Path | Harvester Adapter | Extraction Targets |
| --- | --- | --- | --- |
| **Claude Code** | `~/.claude/projects/*/*.jsonl` | `llmwiki.adapters.claude_code` | Interactive bash histories, tool execution outputs, and user prompts. |
| **Cursor** | `~/Library/.../Cursor/workspaceS...` | `llmwiki.adapters.cursor` | Inline AI suggestions, chat sidebars, and workspace modifications. |
| **Gemini CLI** | `~/.gemini/` | `llmwiki.adapters.gemini_cli` | Terminal conversation traces and generation sessions. |

When the developer executes a synchronization script (e.g., `llmwiki sync`), the harvester scans these local workspace directories, extracts the conversation logs, and converts them into markdown files under `raw/sessions/`.

These implementation logs are then run through the ingestion pipeline. The compiling model reads the logs and updates the active database, flagging discrepancies where the generated code deviates from the planned architecture. This closed loop keeps the wiki evergreen, ensuring that the project's documentation remains in sync with the actual codebase.

## Framework and Tooling Selection Matrix

To implement this compounding knowledge pipeline, the local development workspace must be organized with rigorous directory separation and structured schema enforcement.

```markdown
llm-wiki-demo/
├──.env                 # Local secrets and API URLs [23]
├── CLAUDE.md            # Naming conventions, folder schemas, and rules [2]
├── purpose.md           # Goals, scope, and project thesis 
├── raw/                 # Read-only source directory 
│   ├── articles/        # Downloaded papers, essays, and articles [2]
│   └── sessions/        # Harvested developer chats and transcripts 
└── wiki/                # LLM-maintained markdown database 
    ├── concepts/        # Abstract architectural definitions [2, 18]
    ├── entities/        # Specific technical libraries and tools [2, 18]
    ├── index.md         # Auto-updated catalog of all pages [2, 3, 4]
    ├── log.md           # Append-only ledger of changes [2, 3, 18]
    └── sources/         # Granular summaries of parsed inputs [2, 9, 18]
```

Choosing the correct tools is critical to building a stable, long-term system. Developers can evaluate the leading open-source options using the matrix below:

| Technical Capabilities | OpenKB *(VectifyAI)* | llm\_wiki *(Nashsu)* | llm-wiki *(Pratiyush)* |
| --- | --- | --- | --- |
| **Primary Interface** | Command Line (CLI). | Desktop App (Sigma.js UI). | Command Line & Static Site. |
| **Ingestion Pipeline** | Microsoft MarkItDown; PageIndex for long files. | Local file parser with SHA256 caching. | Tool-specific sync adapters. |
| **Model Compatibility** | Multi-LLM support via LiteLLM. | Multi-LLM support via LiteLLM. | Multi-LLM support via LiteLLM. |
| **Knowledge Graph Logic** | Bidirectional inline linking. | 4-Signal Relevance Model with Louvain Clustered Cohesion. | Bidirectional linking and JSON-LD schema generation. |
| **Diagnostic Checks** | Folder structural audits. | Orphan and community-cohesion checks. | Content lint checks. |
| **Agent Export Pipelines** | Exports portable Anthropic Skills. | Syncs changes to Obsidian folder. | Formats for `llms.txt` and `llms-full.txt`. |
| **Best-Fit Developer Role** | Core infrastructure and backend orchestration. | Interactive visual analysis. | Automated sync from active CLI sessions. |

## Actionable Implementation Protocol

To deploy this compounding knowledge pipeline, developers should execute the following four-phase protocol:

### Phase 1: Local Vault Setup and Strategic Initialization

1. Create the project workspace directory (e.g., `mkdir my-software-project && cd my-software-project`) and construct the separate folder structures for raw inputs (`raw/`) and compiled output files (`wiki/`).
2. Open the Obsidian desktop application, select "Open folder as vault," and target the `wiki/` directory to enable real-time visual monitoring.
3. Create `CLAUDE.md` or `schema.md` at the root of the project to define the schema, naming criteria (e.g., lowercase kebab-case for filenames), frontmatter templates, and formatting rules.
4. Create `purpose.md` at the root of the project, detailing the software architecture goals, core platform boundaries, database targets, and API structures.

### Phase 2: Ingestion and Compilation

1. Save all initial brainstorming chat logs, multi-model outputs, and reference documents to the `raw/` directory.
2. Run the ingestion pipeline using OpenKB or the Nashsu desktop application. Set up a file watcher (such as `openkb watch`) to monitor changes and compile updates automatically as new files are saved to the source folder.
3. Ensure the compilation agent processes changes in two stages: running a structural analysis first to detect conflicts, and then updating the concept files, generating Obsidian-compatible bidirectional links, writing to `index.md`, and logging modifications to `log.md`.

### Phase 3: IDE Mounting and Tooling Integration

1. Install the Obsidian Local REST API community plugin in the Obsidian application and copy the generated local API key.
2. Set up the Obsidian MCP server (such as `mcp-obsidian` or `cyanheads/obsidian-mcp-server`). Add the server configurations and API key to the active environment settings file (such as `claude_desktop_config.json` or Cursor's MCP developer panel).
3. Verify that the coding agents (inside Cursor, VS Code, or Claude Code) can discover the mounted tools, allowing them to search, read, and write directly to the database during active programming tasks.

### Phase 4: Closed-Loop Harvesting and Maintenance

1. Prompt coding agents to query the compiled database before writing code, keeping the generated software aligned with the planned architecture.
2. Set up automated log harvesters (using the Pratiyush model) to parse interactive conversation logs from hidden local project files. Configure a recurring cron task or git hook to process these session logs and copy them back to `raw/sessions/`.
3. Run regular health checks (using `openkb lint` or the compiled linting pass). The system must scan the database to flag orphaned files, unresolved gaps, or logical contradictions where code modifications conflict with the planned design.
4. Resolve flagged design issues in `purpose.md` as they arise, allowing the compiled knowledge base to compound and self-heal automatically as development progresses.