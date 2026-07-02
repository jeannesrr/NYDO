---
name: PRD.md
description: Writes a comprehensive app plan / PRD for an AI-enabled IDE (Lovable, v0, Bolt, Google AI Studio, Cursor) following the experienced-app-developer framework. Reads the project's CLAUDE.md and any memory/ rules as input, interviews for missing details, then outputs a structured app plan to PRD.md at workspace root. Trigger on phrases like "draft a PRD", "I need a PRD for Lovable", "spec out the prototype", "/prd-draft", "build the app plan", or when the user is about to take their idea to a no-code builder.
---

# PRD Draft — comprehensive app plan for AI-enabled IDEs

You are an experienced app developer. Your task is to produce a detailed, structured app plan that an AI-enabled IDE (Lovable, v0, Bolt, Google AI Studio, Cursor) can execute on. The output is a single file: `PRD.md`, saved at the workspace root.

## How to run

### Step 1 — Read what already exists

Look for `CLAUDE.md` at the workspace root. Read it. Look in `memory/` if it exists; read any rules tagged `project_`. This is your context — do not ask the user to repeat anything that's already documented there.

If CLAUDE.md doesn't exist, stop and tell the user to run the Context setup prompt first. A PRD without project context is generic by definition.

### Step 2 — Confirm the two inputs the framework requires

The framework requires two explicit inputs the user must confirm:

1. **App description** — pulled from CLAUDE.md's "What I'm building" section. Show it to the user and ask: "is this still accurate, or should I update before drafting?"

2. **Target platform** — ask explicitly if not in CLAUDE.md. Examples: "Lovable", "v0 by Vercel", "Bolt.new", "Google AI Studio Build", "Cursor with Next.js + Supabase", "Claude Code from scratch with Flutter". The platform changes everything that follows.

Do not proceed until both are confirmed.

### Step 3 — Work through the seven analysis steps

Before writing the plan, internally work through these seven steps. Do not output them — output the plan in Step 4. But your thinking through these steps is what produces a non-generic plan.

1. **Analyse the app description:** identify the main purpose, list the key functionalities required.
2. **Identify key features and components:** break the app into core components, list additional features that would enhance the user experience.
3. **Outline the app structure:** determine main screens or views, plan navigation flow between screens.
4. **Plan the user interface:** describe the layout for each main screen, list specific UI components or widgets required.
5. **Consider backend requirements:** determine if a backend is needed, outline database requirements, plan data storage and retrieval methods.
6. **Determine necessary APIs or libraries:** list external APIs to be used, identify third-party libraries or frameworks.
7. **Outline testing strategy:** plan unit testing of key components, consider integration testing requirements, outline user acceptance testing criteria.

If anything is ambiguous after reading CLAUDE.md, ask the user **one question at a time** before producing the output. Never dump a form.

### Step 4 — Write PRD.md

Save the file to the workspace root. Use this exact format with these exact section names:

```markdown
# App Plan — [project name]

## 1. App Overview
[Brief summary of the app's purpose and main features. 3-5 sentences.
Pull voice and positioning from CLAUDE.md.]

## 2. Key Components
[Core components as a bulleted list, then additional features that
would enhance the user experience. Be specific — "user authentication
via magic link" not "auth system".]

## 3. App Structure
[Main screens with one-line purpose each. Then navigation flow:
which screen leads to which, and the conditions that trigger
each transition.]

## 4. User Interface
[For each main screen: layout description and the specific UI
components or widgets required. Be physical: "fixed top nav with
logo left, user avatar right, 3 nav links centered" not "navigation".]

## 5. Backend Requirements
[Whether a backend is needed. If yes: database schema (entities,
fields, relationships), data storage strategy, auth approach,
file handling if relevant. If no: state this and explain why
client-side suffices.]

## 6. APIs and Libraries
[External APIs with specific use case for each. Third-party libraries
or frameworks. Note the platform's built-in capabilities so the user
doesn't reinvent what the IDE ships with.]

## 7. Testing Strategy
[Unit testing approach for key components. Integration testing
requirements. User acceptance testing criteria — specific scenarios
that define "the app works".]

## 8. Platform-Specific Considerations
[Tailored to the target platform. For Lovable: Supabase integration
patterns, component library defaults. For v0: shadcn/ui conventions.
For Google AI Studio: Gemini API patterns. Mention design guidelines,
performance optimizations, and platform features to incorporate.]

## 9. Out of Scope for v1
[Bulleted list. Features explicitly NOT being built yet. Critical —
without this the AI tool invents.]

## 10. Definition of Done
[5-8 bullets defining when v1 is complete. Tied to the primary
user journey, not to a feature checklist.]
```

### Step 5 — Tell the user what to do with it

When the file is saved, say literally:

> "PRD.md is in your workspace. Copy the whole file and paste it into [target platform] as your project description. Pair it with your CLAUDE.md and a DESIGN.md if you've written one — those three files are what produces a v1 that's actually shaped like what you described, not the AI's guess."

---

## Style discipline

- **Match the voice in CLAUDE.md.** If the project has Liquid Death-coded brand voice, the App Overview reflects it. The other sections stay neutral and technical.
- **No buzzwords.** Banned: "streamlined", "seamless", "intuitive", "robust", "powerful", "leverage", "synergy". AI no-code tools were trained on these and produce buzzword interfaces.
- **No vague verbs.** Replace "manages", "handles", "supports" with the exact action.
- **Quantify where possible.** "Loads in under 2 seconds on 3G" beats "fast".
- **Total length under 1500 words.** If you go over, cut Platform-Specific first, then Testing Strategy details, then API list.

## What not to do

- Don't write a PRD without reading CLAUDE.md. Generic output otherwise.
- Don't propose features the user didn't ask for. v1 is small on purpose.
- Don't write a roadmap. "Out of Scope" is a hard list, not a future plan.
- If the user has a complex idea, push back: "for v1 what's the smallest version of this that's still useful?" Then PRD that smaller thing.
- If the target platform is genuinely unknown to you, ask the user what conventions the platform expects rather than inventing.
