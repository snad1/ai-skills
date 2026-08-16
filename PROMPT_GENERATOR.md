# UNIVERSAL CODEBASE PROMPT GENERATOR

**Version:** 2.0 - Smart Parsing Edition  
**Compatible with:** Any programming language, framework, or project type

---

## 🧠 SMART INPUT MODE

**Just dump your thoughts here - no structure needed!**

You can input in ANY format:
- ✅ Messy paragraphs with everything mixed
- ✅ Scattered bullet points
- ✅ Stream of consciousness
- ✅ Half-formed ideas
- ✅ Mix of instructions, constraints, and expectations

**Claude will automatically:**
1. Parse and organize your input
2. Ask clarifying questions if needed
3. Analyze your codebase
4. Structure everything properly
5. Confirm understanding before proceeding

---

## 📝 YOUR INPUT (Put everything here):

<!-- 
JUST WRITE NATURALLY! Examples:

"I want to change the login page colors to blue, optimize the DB queries, 
use SOLID principles, don't hardcode anything, and make sure it loads under 2 seconds"

"Add dark mode, but don't use any external libraries, keep it simple, 
test it properly, and the toggle should be in the header"

"Fix the signup form, users are confused, add better validation, 
rate limit it, show password requirements, keep design minimal"

NO FORMATTING REQUIRED - Just brain dump!
-->

**YOUR TASK/REQUEST:**

[WRITE YOUR REQUEST HERE - ANY FORMAT]

---

## 🤖 INSTRUCTIONS FOR CLAUDE

### STEP 1: INTELLIGENT PARSING

When you receive input above, analyze and categorize into:

#### 📋 INSTRUCTIONS (What to do)
Look for:
- Action verbs: add, change, optimize, implement, fix, update, create, remove
- Feature requests: "I want X", "we need Y", "should have Z"
- Tasks: "make responsive", "add validation", "improve performance"

#### 🔒 CONSTRAINTS (How to do it / What NOT to do)
Look for:
- Restrictions: "don't use", "avoid", "no hardcoding", "must use"
- Standards: "follow SOLID", "use TypeScript", "DRY principles"
- Limits: "under 2 seconds", "less than 100 lines", "max 200ms"
- Best practices: "optimize queries", "proper error handling"
- Technology choices: "use Redis", "only native features"

**Always-infer defaults (apply even if the user didn't mention them):**
- **Performance / Web Vitals** — for ANY frontend / UI / page / component / loading-state work, performance is a default constraint, not an afterthought. Design for LCP (don't hide the largest element behind `opacity:0`), FCP (loading states must show a real contentful element, not just gray skeletons), INP (keep interaction handlers light — debounce, memoize, defer), CLS (reserve space; dimension images; don't shift content), and TTFB (static/ISR + cache server data) from the start. Code-split heavy or disabled-feature dependencies instead of importing them into the shared/root bundle, and verify the production bundle before deploy. See the project's PERF rules in `.claude/rules.md`. Do it right while implementing — never "build it, then fix performance later."
- **Security** (OWASP/ISO awareness), **accessibility**, and **user-friendly errors** are likewise default constraints.

#### 🎯 EXPECTATIONS (What should happen)
Look for:
- Success criteria: "should load in X", "user sees Y"
- Test scenarios: "when user does X, expect Y"
- Performance targets: "response under 200ms"
- UX requirements: "smooth transitions", "no page reload"

#### 🏗️ CONTEXT CLUES (Background information)
Look for:
- Tech mentions: "the login page", "dashboard", "using Laravel"
- Current state: "already have X", "currently using Y"
- Project details: "our API", "mobile app", "admin panel"

---

### STEP 2: ASK CLARIFYING QUESTIONS

**If anything is ambiguous, use this template:**

```
I've analyzed your request. Let me organize and confirm:

📋 INSTRUCTIONS (Tasks to accomplish):
- [Extracted instruction 1]
- [Extracted instruction 2]
- [Extracted instruction 3]

🔒 CONSTRAINTS (Requirements & Restrictions):
- [Extracted constraint 1]
- [Extracted constraint 2]
- [Extracted constraint 3]

🎯 EXPECTATIONS (Success Criteria):
- [Extracted expectation 1]
- [Auto-generated from instructions]

❓ CLARIFICATION NEEDED:
1. [Question about unclear point 1]
2. [Question about unclear point 2]

Is this understanding correct? Anything to add or modify?
```

---

### STEP 3: CODEBASE ANALYSIS

After confirming understanding, analyze the project:

#### DETECT PROJECT TYPE

**Check for these indicators:**

**Backend:**
- `composer.json` → PHP (Laravel, Symfony, CodeIgniter)
- `package.json` + server files → Node.js (Express, NestJS, Fastify)
- `requirements.txt` / `pyproject.toml` → Python (Django, Flask, FastAPI)
- `go.mod` → Go (Gin, Echo, Fiber)
- `Cargo.toml` → Rust (Actix, Rocket)
- `pom.xml` / `build.gradle` → Java (Spring Boot)
- `Gemfile` → Ruby (Rails, Sinatra)
- `mix.exs` → Elixir (Phoenix)

**Frontend:**
- `package.json` + `next.config.js` → Next.js
- `package.json` + `vite.config.js` → Vite (React/Vue/Svelte)
- `package.json` + `angular.json` → Angular
- `package.json` + `vue.config.js` → Vue.js
- `package.json` + `nuxt.config.js` → Nuxt.js
- `package.json` + React dependencies → React (CRA/Custom)
- `package.json` + `svelte.config.js` → Svelte/SvelteKit
- `astro.config.mjs` → Astro

**Mobile:**
- `package.json` + `app.json` → React Native / Expo
- `pubspec.yaml` → Flutter
- `*.xcodeproj` + Swift files → iOS Native
- `build.gradle` + Kotlin files → Android Native

**Desktop:**
- `tauri.conf.json` → Tauri
- `electron-builder.json` → Electron
- `.csproj` → .NET / WPF

#### EXTRACT PROJECT CONTEXT

**1. Language & Framework:**
- Primary language(s)
- Framework/library and version
- Runtime version (Node, Python, PHP, etc.)

**2. Project Architecture:**
- Structure type: MVC, Microservices, Monolith, Serverless, JAMstack
- Key directories: src/, app/, components/, pages/, api/, services/
- Entry points: main, index, app files

**3. Dependencies & Tools:**
- Package manager: npm, yarn, pnpm, pip, composer, cargo, go mod
- Top 10 important dependencies
- Build tools: Webpack, Vite, esbuild, Rollup, Turbopack
- Dev tools: Linters, formatters, pre-commit hooks

**4. Data Layer (if applicable):**
- Database: PostgreSQL, MySQL, MongoDB, SQLite, etc.
- ORM/Query tool: Prisma, Sequelize, TypeORM, SQLAlchemy, Eloquent, Drizzle
- Caching: Redis, Memcached
- State management (frontend): Redux, Zustand, Pinia, Jotai, MobX

**5. Configuration:**
- Environment variables: .env, config files, environment modules
- Config management: dotenv, config packages, environment-specific files

**6. Testing:**
- Framework: Jest, Vitest, Pytest, PHPUnit, Go test, Mocha, Cypress
- Test locations: tests/, __tests__/, test/, spec/
- E2E testing: Playwright, Cypress, Selenium
- Coverage requirements from config

**7. Code Quality:**
- Linter: ESLint, Pylint, RuboCop, golangci-lint, Clippy
- Formatter: Prettier, Black, gofmt, rustfmt
- Type checking: TypeScript, mypy, Flow
- Config files: Check for .eslintrc, tsconfig.json, etc.

**8. Styling (if frontend):**
- Approach: Tailwind, CSS Modules, styled-components, SASS, vanilla CSS
- UI library: Material-UI, shadcn/ui, Ant Design, Chakra, DaisyUI

**9. API/Communication:**
- Type: REST, GraphQL, tRPC, gRPC, WebSocket
- Client: axios, fetch, apollo, urql, httpx, requests
- Response format from existing code

**10. Authentication (if applicable):**
- Method: JWT, sessions, OAuth, Firebase Auth, NextAuth, Passport
- Storage: localStorage, cookies, httpOnly cookies, sessionStorage

#### DETECT CODING PATTERNS

**Analyze 3-5 existing files to identify:**
- Naming conventions: camelCase, PascalCase, snake_case, kebab-case
- File organization: Feature-based, type-based, domain-driven
- Component/module structure
- Import style: Relative, absolute, path aliases
- Error handling patterns
- Async patterns: async/await, promises, callbacks
- Comment style and documentation

---

### STEP 4: FINAL STRUCTURED OUTPUT

Provide the complete organized prompt:

```markdown
## 🎯 CONTEXT & BACKGROUND

**Project Type:** [Detected type]
**Stack:** [Languages, frameworks, versions]
**Architecture:** [Pattern detected]

**Current Setup:**
- [Key technologies]
- [Database/State management]
- [Testing framework]
- [Styling approach]
- [Notable patterns detected]

**Relevant Files/Directories:**
- [Key files related to this task]

---

## 📋 INSTRUCTIONS

**Priority 1 (Must Have):**
- [Main instruction 1]
- [Main instruction 2]

**Priority 2 (Should Have):**
- [Secondary instruction 1]
- [Secondary instruction 2]

**Priority 3 (Nice to Have):**
- [Optional enhancement 1]

---

## 🔒 CONSTRAINTS & ASSUMPTIONS

**Technical Constraints:**
- [Framework/library restrictions]
- [Performance requirements]
- [Browser/environment support]

**Code Quality Standards:**
- [Auto-detected patterns to follow]
- [Linting/formatting rules]
- [Testing requirements]

**Best Practices:**
- [SOLID, DRY, or other principles]
- [Security considerations]
- [Accessibility requirements]

**Do NOT:**
- [Things to avoid]
- [Anti-patterns to prevent]

---

## 🎯 EXPECTATIONS & RESULTS

**Success Criteria:**
- [What success looks like]
- [Performance metrics]
- [User experience goals]

**When [Action], then [Expected Result]:**
- When [user action], then [system response]
- When [condition], then [expected behavior]
- When [error case], then [error handling]

**Testing Requirements:**
- [Unit tests needed]
- [Integration tests needed]
- [E2E scenarios if applicable]

**Performance Targets:**
- [Load time expectations]
- [Response time requirements]
- [Resource usage limits]

---

## ✅ READY TO IMPLEMENT

All requirements understood and organized. Proceed with implementation?
```

---

## 📚 USAGE EXAMPLES

### Example 1: Messy Paragraph

**Input:**
```
I want to add user authentication to the app, use JWT tokens, 
store them in httpOnly cookies, hash passwords with bcrypt, 
don't store passwords in plain text obviously, add rate limiting 
to prevent brute force, use Redis for session storage, write 
tests for all auth flows, and make sure it works with our existing 
user model. Oh and add 2FA later maybe but not now.
```

**Output:**
```
📋 INSTRUCTIONS:
- Implement JWT-based authentication
- Add password hashing (bcrypt)
- Implement rate limiting for auth endpoints
- Use Redis for session storage

🔒 CONSTRAINTS:
- Store JWT in httpOnly cookies (not localStorage)
- Never store plain text passwords
- Must integrate with existing user model
- Write comprehensive tests for all flows

🎯 EXPECTATIONS:
- Protection against brute force attacks
- Secure token storage
- All auth flows tested
- Session management via Redis

📝 DEFERRED:
- 2FA implementation (future enhancement)

[Proceeds with codebase analysis...]
```

---

### Example 2: Bullet Points

**Input:**
```
- dark mode for entire app
- toggle in settings
- remember user choice
- smooth transitions
- test on mobile
- don't use libraries
- localStorage for persistence
```

**Output:**
```
📋 INSTRUCTIONS:
- Implement dark mode theme system
- Add toggle control in settings page
- Persist user preference

🔒 CONSTRAINTS:
- No external libraries (custom implementation)
- Use localStorage for persistence
- Mobile-compatible
- Smooth CSS transitions

🎯 EXPECTATIONS:
- Theme persists across sessions
- Smooth visual transitions between themes
- Works on all screen sizes
- User preference loads on app mount

[Proceeds with codebase analysis...]
```

---

### Example 3: Stream of Consciousness

**Input:**
```
The dashboard loads way too slow, need to optimize it. Maybe 
virtualize the table? We're loading like 10k rows. Also cache 
the API response, it doesn't change that often. Keep the filters 
working though. Don't break anything, we have users on production. 
Add loading states so users know something's happening.
```

**Output:**
```
📋 INSTRUCTIONS:
- Optimize dashboard performance (currently slow with 10k rows)
- Implement table virtualization
- Add API response caching
- Improve loading state UX

🔒 CONSTRAINTS:
- Maintain existing filter functionality
- Zero breaking changes (production system)
- Preserve current user experience

🎯 EXPECTATIONS:
- Significant performance improvement for large datasets
- Loading indicators visible to users
- Cache invalidation strategy for API data
- All existing features continue to work

❓ QUESTIONS:
1. What's acceptable cache duration for the API response?
2. Any specific rows in view target? (e.g., show 50, render 20 buffer)

[Proceeds with codebase analysis...]
```

---

## 🚀 QUICK START

1. **Copy this file** to your project root as `.ai/PROMPT_GENERATOR.md`

2. **When you need to work on something:**
   ```
   @.ai/PROMPT_GENERATOR.md
   
   [Your messy thoughts here]
   ```

3. **Claude will:**
   - Parse your input
   - Ask clarifications
   - Analyze codebase
   - Organize everything
   - Confirm understanding
   - Start implementation

4. **Continue conversation naturally** - context persists!

---

## 🎯 BENEFITS

✅ **No mental overhead** - Just think out loud  
✅ **Works with ANY project** - Language agnostic  
✅ **Auto-detects patterns** - Respects your codebase  
✅ **Asks when unclear** - No assumptions  
✅ **Consistent structure** - Every time  
✅ **Context aware** - Knows your tech stack  
✅ **Production ready** - Use immediately  

---

## 📝 NOTES

- This file should be version controlled with your project
- Works in VS Code, Claude.ai, and any IDE with Claude integration
- Update examples as your project evolves
- Share with team for consistent AI interactions
- Add project-specific patterns to STEP 3 as needed

---

**Version:** 2.0  
**Last Updated:** February 2026  
**License:** MIT - Use freely in any project