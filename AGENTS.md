# Agentic Coding Guidelines

This document provides context and rules for AI agents operating in the `airboost/front` repository.

## 1. Project Overview & Environment

- **Framework**: Astro 5 (Static Site Generation / Hybrid)
- **Language**: TypeScript (Strict mode enabled)
- **Runtime/Package Manager**: Bun (implied by `bun.lock`)
- **Structure**: Standard Astro directory structure
  - `src/pages/`: File-based routing
  - `src/components/`: UI components
  - `src/layouts/`: Page layouts
  - `src/assets/`: Static assets

## 2. Build & Execution Commands

Use `bun` for all script executions.

### Core Commands
- **Start Development Server**: `bun run dev`
- **Build for Production**: `bun run build`
- **Preview Production Build**: `bun run preview`
- **Astro CLI**: `bun x astro`

### Quality Checks
- **Type Checking**: `bun x astro check`
  - *Note*: Run this to verify TypeScript types in `.astro` files.
- **Testing**: *No test framework is currently configured.* 
  - If instructed to add tests, prefer **Vitest** for unit/component testing as it integrates natively with Vite/Astro.

## 3. Code Style & Conventions

### General
- **Indentation**: 2 spaces.
- **Semicolons**: Always use semicolons.
- **Quotes**: Single quotes preferred for JS/TS; Double quotes for HTML attributes.

### Astro Components (`.astro`)
- **Frontmatter**: Use the "Code Fence" (`---`) at the top of the file for component logic.
- **Imports**: Group imports at the top of the frontmatter.
  1. Astro/Framework imports
  2. Component imports
  3. Asset/Style imports
- **Props**: Define props using the `Props` interface.
  ```typescript
  ---
  interface Props {
    title: string;
    isActive?: boolean;
  }
  
  const { title, isActive = false } = Astro.props;
  ---
  ```
- **HTML**: Ensure semantic HTML usage.

### TypeScript
- **Strict Mode**: The project uses `astro/tsconfigs/strict`. Ensure all types are explicitly defined; avoid `any`.
- **Interfaces**: Use `interface` for object definitions over `type` where possible.
- **Naming**:
  - **Variables/Functions**: `camelCase`
  - **Types/Interfaces**: `PascalCase`
  - **Components**: `PascalCase` (e.g., `Welcome.astro`, `Layout.astro`)
  - **Files**:
    - Components: `PascalCase.astro`
    - Pages: `kebab-case.astro` (e.g., `about-us.astro`)
    - Utilities: `camelCase.ts`

### Styling
- **Scoped Styles**: Prefer `<style>` tags within `.astro` components for scoped CSS.
- **Global Styles**: Define global styles only when necessary in `Layout.astro` or a dedicated global CSS file.

### Error Handling
- Use `try/catch` blocks for async operations in the component frontmatter.
- Handle missing props gracefully with default values.

## 4. Workflow Rules for Agents

1. **Verify Context**: Before editing, read the relevant file and its neighbors to understand local patterns.
2. **Type Safety**: Run `bun x astro check` after significant TypeScript changes to ensure no regressions.
3. **No Assumptions**: Do not assume libraries (like Tailwind, React, etc.) are installed unless you see them in `package.json`.
4. **File Creation**: When creating new pages or components, follow the directory structure:
   - Pages go in `src/pages/`
   - Reusable UI goes in `src/components/`
   - Wrappers go in `src/layouts/`
