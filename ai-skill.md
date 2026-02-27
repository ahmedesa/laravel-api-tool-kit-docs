# **AI Architectural Skill**

The Laravel API Tool Kit ships with a built-in **AI Architectural Skill** — 20 rule files and 5 guided workflows that teach your AI coding assistant to follow the same standards you do.

When you use an AI coding assistant (like **Claude Code**, **Cursor**, **GitHub Copilot**, or **Antigravity**), these rules ensure every generated file matches your architecture from the first draft instead of requiring manual corrections.

---

## **Installation**

Run the following command in your project:

```bash
php artisan api-skill:install
```

The installer will ask which AI tool you are using and automatically copy the skill to the correct location for that tool.

Add `--force` to overwrite an existing installation without a prompt:

```bash
php artisan api-skill:install --force
```

---

## **Supported AI Tools**

### **Cursor**
Copies rule files as `.mdc` into `.cursor/rules/laravel-api/`.
- **Core rules** (SKILL, anti-patterns, code-quality) are set to `alwaysApply: true` — always active.
- **Component rules** (actions, models, controllers, etc.) are loaded on demand by referencing them in chat (e.g. `@actions`).

### **Claude Code**
Copies the full skill to `.claude/skills/laravel-api/` and appends a reference to your `CLAUDE.md` file automatically.

### **GitHub Copilot**
Compiles all rules into a single `.github/copilot-instructions.md` file — the standard format Copilot reads automatically.

### **Antigravity**
Compiles all rules into `.agents/instructions.md` and copies the workflows to `.agents/workflows/` — matching Antigravity's expected structure.

---

## **Included Rules**

### General Laravel Best Practices

| Rule file | Covers |
|-----------|--------|
| `code-quality` | `strict_types`, types, naming, no hardcoded values, dependency injection, CacheKeys pattern |
| `events` | Event classes, queued listeners, dispatch timing |
| `authorization` | Policies, `$this->authorize()`, never inline auth |
| `exceptions` | Route model binding, `UnprocessableEntityHttpException`, no empty catch |
| `testing` | Feature tests, factories, failure paths |
| `media` | File uploads, deletions, base64 images |
| `database` | Transactions, bulk ops, eager loading, primary key convention |
| `services` | External 3rd-party integrations — Interface / Concrete / Mock / ServiceProvider pattern |
| `anti-patterns` | 26 wrong/correct code pairs covering the most common mistakes |

### Package-Specific Patterns

| Rule file | Covers |
|-----------|--------|
| `responses` | `ApiResponse` trait methods, status codes |
| `filters` | `QueryFilters`, `Filterable`, `useFilters()` |
| `actions` | `final` Action classes, `execute()` method, when to use vs. controller |
| `dtos` | `final readonly class` DTOs, getters, when arrays must become DTOs |
| `controllers` | Thin controllers, `$request->validated()`, `ApiResponse` usage |
| `requests` | Separate create/update requests, `sometimes` for partials |
| `resources` | `whenLoaded()`, `$this->when()`, `dateTimeFormat()` |
| `models` | Fat model boundary, `shouldBeStrict()`, `Filterable`, package traits |
| `repositories` | Complex read queries, typed returns, when to use vs. controller |
| `enums` | Backed enums, `EnumHelpers`, `Rule::in(Enum::values())` |
| `pagination` | `dynamicPaginate()`, client parameters |

---

## **Included Workflows**

Step-by-step guides the AI follows for common tasks:

| Workflow | What it does |
|----------|-------------|
| `scan-project` | Performs a **Deep Project Analysis** (structure, services, core abstractions, feature flags, base patterns) and populates Project Defaults |
| `new-endpoint` | Full CRUD from scratch — Model → Migration → Filter → Requests → Resource → Action → Controller → Route → Test |
| `add-filter` | Add filtering and sorting to an existing model's list endpoint |
| `code-review` | 17-section checklist covering every layer of the stack |
| `update-knowledge` | Saves learnings from the current session back into the skill files |

---

## **Deep Project Scan — The AI's First Task**

When you join a new project or start a fresh session, the first thing you should do is trigger the **Deep Project Scan** workflow. 

**Why it matters:** Standard rules only go so far. A real project has custom services, unique feature flag patterns, and specific base classes. The Deep Project Scan teaches the AI your project's specific "DNA" by scanning:

- **Services & Core**: Discovers your custom abstractions for SMS, Payments, and specialized domain logic.
- **Pattern DNA**: Finds your `BaseAction`, `BaseRepository`, or global traits like `HasTenant`.
- **Infrastructure**: Detects your feature flag package (e.g., Pennant), cache key pattern, and custom exception handling.
- **Auto-Config**: It automatically updates your `SKILL.md` file, ensuring the AI never "invents" a new way to do something you've already solved.

**Trigger Phrases**: "Scan project", "Deep scan", "Learn project conventions"

## **Project Defaults**

After installing, open the `SKILL.md` file and fill in your project's conventions under **Project Defaults**:

```
- Primary key type: ulid   ← change to `id` if using auto-increment
- Auth guard: sanctum      ← change if different
- Test class: Tests\TestCase
```

The AI reads this section before generating any code, so migrations, factories, and tests will always use the correct primary key type and guard without extra prompting.

---

## **DDD Support**

The skill works with both standard Laravel structure (`app/Models/`, `app/Actions/`) and Domain-Driven Design layouts (`app/Domain/{Domain}/Models/`). The AI is instructed to scan the project structure before creating files and adapt paths to match the existing conventions.

---

## **Customization**

The skill is a baseline. If your project has overrides (e.g. "we use `id` instead of `ulid`"), add them to the **Project Defaults** section of your installed `SKILL.md`. The AI is instructed to prioritize **Project Patterns > Global Skill Rules**.
