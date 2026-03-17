<p align="center">
  <a href="https://agentos.sh"><img src="https://raw.githubusercontent.com/manicinc/voice-chat-assistant/master/logos/agentos-primary-no-tagline-transparent-2x.png" alt="AgentOS" height="56" /></a>
  &nbsp;&nbsp;&nbsp;
  <a href="https://frame.dev"><img src="https://raw.githubusercontent.com/manicinc/voice-chat-assistant/master/logos/frame-logo-green-no-tagline.svg" alt="Frame.dev" height="36" /></a>
</p>

# @framers/agentos-skills

Skills runtime for the [AgentOS](https://github.com/framersai/agentos) ecosystem -- loads, parses, and manages SKILL.md prompt modules.

[![npm](https://img.shields.io/npm/v/@framers/agentos-skills?logo=npm&color=cb3837)](https://www.npmjs.com/package/@framers/agentos-skills)

```bash
npm install @framers/agentos-skills
```

## What's Inside

This package is the **runtime** for the AgentOS skills system. It provides:

| Module              | Description                                                              |
| ------------------- | ------------------------------------------------------------------------ |
| `SkillLoader`       | Loads and parses SKILL.md files with YAML frontmatter                    |
| `SkillRegistry`     | Runtime registry for managing, querying, and filtering loaded skills     |
| `paths`             | Path resolution utilities for discovering default skill directories      |
| `types`             | Full TypeScript type definitions for skills, metadata, and configuration |

## Usage

```typescript
import {
  SkillRegistry,
  loadSkillFromDir,
  loadSkillsFromDir,
  resolveDefaultSkillsDirs,
} from '@framers/agentos-skills';

// Discover default skill directories
const dirs = resolveDefaultSkillsDirs();

// Create a registry and load skills
const registry = new SkillRegistry();
await registry.loadFromDirs(dirs);

console.log(`Loaded ${registry.size} skills`);

// Build a snapshot for LLM context
const snapshot = registry.buildSnapshot({ platform: 'darwin', strict: true });
console.log(snapshot.prompt);
```

## Relationship to Other Packages

```
@framers/agentos-skills              <-- You are here (runtime: SkillLoader, SkillRegistry, types)
@framers/agentos-skills-registry     (catalog: 40+ curated SKILL.md files + JSON index)
@framers/agentos                     (full cognitive runtime, re-exports skills from here)
```

| Package                              | What                                      | Runtime Code | Dependencies    |
| ------------------------------------ | ----------------------------------------- | :----------: | --------------- |
| **@framers/agentos-skills**          | SkillLoader, SkillRegistry, path utils    |     Yes      | `yaml`          |
| **@framers/agentos-skills-registry** | 40+ SKILL.md files + JSON index + catalog |      No      | `yaml`          |
| **@framers/agentos**                 | Full cognitive runtime                    |     Yes      | Many            |

## API

### SkillLoader

- `parseSkillFrontmatter(content)` -- Parse YAML frontmatter from SKILL.md content
- `extractMetadata(frontmatter)` -- Extract typed SkillMetadata from parsed frontmatter
- `loadSkillFromDir(dir)` -- Load a single skill from a directory containing SKILL.md
- `loadSkillsFromDir(dir)` -- Load all skills from a parent directory
- `filterByPlatform(entries, platform)` -- Filter skill entries by OS platform
- `filterByEligibility(entries, context)` -- Filter by full eligibility context
- `checkBinaryRequirements(entry, hasBin)` -- Check if binary requirements are met

### SkillRegistry

- `register(entry)` / `unregister(name)` -- Add/remove skills
- `loadFromDir(dir)` / `loadFromDirs(dirs)` / `reload(options)` -- Bulk loading
- `getByName(name)` / `listAll()` / `has(name)` / `size` -- Queries
- `filterByPlatform(platform)` / `filterByEligibility(context)` -- Filtering
- `getUserInvocableSkills()` / `getModelInvocableSkills()` -- Invocation filtering
- `buildSnapshot(options)` -- Build LLM context snapshot
- `buildPrompt(entries)` -- Format skills into prompt text
- `buildCommandSpecs(options)` -- Generate CLI command specs

### Path Utilities

- `resolveDefaultSkillsDirs(options)` -- Resolve default skill directories to scan

## License

MIT

