# **AI Architectural Skill**

The Laravel API Tool Kit ships with a built-in **AI Architectural Skill** — 21 rule files and 8 guided workflows that teach your AI coding assistant to follow the same standards you do.

When you use an AI coding assistant (like **Claude Code**, **Cursor**, **GitHub Copilot**, or **Antigravity**), these rules ensure every generated file matches your architecture from the first draft instead of requiring manual corrections.

---

## **Installation**

Run the following command in your project:

```bash
php artisan api-skill:install [tool]
```

The installer will ask which AI tool you are using (if not provided as an argument) and automatically copy the skill to the correct location. Supported values for `[tool]`: `claude`, `cursor`, `copilot`, `antigravity`.

Add `--force` to overwrite an existing installation without a prompt:

```bash
php artisan api-skill:install --force
```

---

## **Supported AI Tools**

### **Claude Code**

- Rules → `.claude/rules/laravel-api/` — auto-loaded by Claude Code on every session, no manual setup
- Workflows → `.claude/skills/<name>/SKILL.md` — become native slash commands: `/code-review`, `/investigate`, `/new-endpoint`, etc.
- A reference is appended to your `CLAUDE.md` automatically

### **Cursor**

Rules are installed as `.mdc` files into `.cursor/rules/laravel-api/` with the correct frontmatter for each type:

| Rule type | Cursor behaviour |
|-----------|-----------------|
| Core rules (SKILL, anti-patterns, code-quality) | **Always Apply** — injected in every session |
| Component rules (models, controllers, actions, etc.) | **Auto Attached** — activates automatically when `.php` files are open |
| Workflows & knowledge | **Manual** — reference with `@workflow-name` when needed |

### **GitHub Copilot**

- `.github/copilot-instructions.md` — always-on rules (SKILL overview + core rules)
- `.github/instructions/laravel-api.instructions.md` — PHP-specific rules, auto-attached to `**/*.php` files via `applyTo:` frontmatter

### **Antigravity**

- Rules compiled → `AGENTS.md` at project root (cross-tool standard, auto-loaded)
- Workflows → `.agent/skills/<name>/SKILL.md` — native slash commands
- Requires Antigravity v1.20.3+

---

## **Included Rules**

21 rule files covering every layer of a Laravel API:

### General Laravel Best Practices

| Rule file | Covers |
|-----------|--------|
| `code-quality` | `strict_types`, types, naming, no hardcoded values, CacheKeys pattern, early return, match over ternary |
| `dependency-injection` | Constructor injection, `private readonly`, never `new` for services or actions |
| `events` | Event classes, queued listeners, dispatch timing, domain ServiceProviders |
| `authorization` | Policies, `$this->authorize()`, all 5 policy methods (`viewAny`, `view`, `create`, `update`, `delete`) |
| `exceptions` | Route model binding, `UnprocessableEntityHttpException`, no `abort()` for business logic |
| `testing` | Feature tests, factories, failure paths, time-freezing, faking external services |
| `database` | Transactions (events outside transactions), bulk ops, eager loading, ULID/auto-increment convention |
| `services` | External 3rd-party integrations — Interface / Concrete / Mock / ServiceProvider pattern |
| `ddd` | Domain structure, cross-domain boundaries, App-Level Merging, Shadow Models, audience splitting |
| `anti-patterns` | 26+ wrong/correct code pairs covering the most common mistakes |

### Package-Specific Patterns

| Rule file | Covers |
|-----------|--------|
| `responses` | `ApiResponse` trait methods, status codes, `Resource::collection()` for index endpoints |
| `filters` | `QueryFilters`, `Filterable`, `useFilters()`, `$allowedIncludes` vs hardcoded `with()` |
| `actions` | `final readonly` Action classes, `execute()` method, when to use vs controller |
| `dtos` | `final readonly class` DTOs, getters, `fromRequest()` factory, when arrays must become DTOs |
| `controllers` | Thin controllers, `$request->validated()`, route-level middleware (Laravel 12) |
| `requests` | Separate create/update requests, `sometimes` for partial updates |
| `resources` | `whenLoaded()`, `$this->when()`, `dateTimeFormat()`, no DB calls inside `toArray()` |
| `models` | Fat model boundary, `HasUlids`, `shouldBeStrict()` via config, `Filterable`, package traits |
| `repositories` | Complex read queries, typed returns, `useFilters()` without array params |
| `enums` | Backed enums, `EnumHelpers`, `Rule::in(Enum::values())`, AI rule to extract magic values |
| `pagination` | `dynamicPaginate()`, client parameters, package max per_page cap |

---

## **Included Workflows**

8 workflows the AI follows for common tasks:

### Building

| Workflow | What it does |
|----------|-------------|
| `new-endpoint` | Full CRUD from scratch — detects Standard vs DDD structure, then: Model → Migration → Filter → Enum → Requests → Resource → Policy → Action → Controller → Language file → Route → Test |
| `add-filter` | Add filtering, sorting, search, and eager-load includes to an existing model's list endpoint |

### Reviewing

| Workflow | What it does |
|----------|-------------|
| `code-review` | Multi-phase defense-oriented review: gathers full git diff → validates acceptance criteria → structural checklists → defense review (race conditions, data source validation, consistency between methods, silent data loss) → scope discipline → final report with severity table |

### Debugging

| Workflow | What it does |
|----------|-------------|
| `investigate` | Data-before-code debugging: checks knowledge base → queries DB → cross-references API vs DB vs Tinker → 15-min hypothesis checkpoint → proves root cause with data → updates knowledge |
| `curl-test` | Builds curl command for an endpoint, parses the response, and cross-references it against the DB to pinpoint cache, resource, or transformation bugs |

### Knowledge Management

| Workflow | What it does |
|----------|-------------|
| `update-knowledge` | Saves learnings from the current session — architectural rules go into `rules/`, project-specific findings go into `knowledge/[feature].md` |
| `organize-knowledge` | Consolidates scattered investigation docs (`INVESTIGATION_*.md`, `FIX_*.md`) into the correct `knowledge/[feature].md` file — one file per feature |
| `create-workflow` | Captures a repeatable process discovered during a session into a new reusable workflow file |

---

## **Knowledge Base**

The skill installs a per-project knowledge directory. The location depends on your AI tool:

| Tool | Knowledge location |
|------|--------------------|
| Claude Code | `.claude/knowledge/` |
| Antigravity | `.agent/knowledge/` |
| Cursor / Copilot | `knowledge/` (project root) |

Each file covers one feature area and accumulates:

- Bug root causes with data evidence
- Reusable diagnostic SQL queries (with placeholder variables)
- DB / data gotchas specific to this project
- Lessons that don't fit into general rules

The `investigate` workflow checks this directory before starting any investigation. The `update-knowledge` workflow writes to it after confirming a root cause. A `_TEMPLATE.md` is copied into your project during installation.

One file per feature — never one file per investigation ticket.

---

## **Project Defaults**

After installing, open the installed `SKILL.md` (or `_overview.md` for Claude Code) and fill in your project's conventions:

```
- Primary key type: ulid   ← change to `id` if using auto-increment
- Auth guard: sanctum      ← change if different
- Test class: Tests\TestCase
```

The AI reads this section before generating any code — migrations, factories, and tests will always use the correct primary key type and guard without extra prompting.

---

## **DDD Support**

The skill works with both standard Laravel structure and Domain-Driven Design layouts. The `new-endpoint` workflow runs `ls app/` first, then provides an explicit path map for both structures:

| Component | Standard Laravel | DDD |
|---|---|---|
| Model | `app/Models/` | `app/Domain/{Name}/Models/` |
| Filter / Action / Enum | `app/Filters/`, `app/Actions/`, `app/Enums/` | `app/Domain/{Name}/Filters/` etc. |
| Controller / Request / Resource | `app/Http/...` | `app/Http/...` (always stays in Http) |

The `ddd` rule file covers cross-domain boundaries, the App-Level Merging pattern for multi-domain data, Shadow Models, and audience splitting (Application vs Dashboard resources).

---

## **Customization**

The skill is a baseline. If your project has overrides (e.g. "we use `id` instead of `ulid`"), add them to the **Project Defaults** section of your installed `SKILL.md`. The AI is instructed to prioritize **Project Patterns > Global Skill Rules**.

For project-specific accumulated knowledge (bugs, queries, gotchas), use the knowledge directory — not the rule files.
