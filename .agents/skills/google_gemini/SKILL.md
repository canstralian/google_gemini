```markdown
# google_gemini Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill teaches you the core development patterns, conventions, and workflows used in the `google_gemini` TypeScript codebase. You'll learn how to structure files, write imports/exports, manage dependencies, and follow the project's testing and update workflows. This guide is ideal for onboarding new contributors or standardizing team practices.

## Coding Conventions

**File Naming**
- Use kebab-case for all filenames.
  - Example: `my-feature.ts`, `user-service.test.ts`

**Import Style**
- Use relative imports for internal modules.
  - Example:
    ```typescript
    import { myFunction } from './utils';
    ```

**Export Style**
- Prefer named exports.
  - Example:
    ```typescript
    // utils.ts
    export function myFunction() { ... }
    ```

**Commit Patterns**
- Commits are freeform, with no enforced prefix.
- Average commit message length: 64 characters.

## Workflows

### Bulk Dependency Update Across Multiple Packages
**Trigger:** When you need to upgrade one or more dependencies across several packages in a monorepo.
**Command:** `/update-dependencies`

1. **Identify outdated dependencies** in all relevant packages.
2. **Update `package.json`** (if present) and lockfiles (`package-lock.json`, `pnpm-lock.yaml`) in each affected package or directory.
3. **Regenerate lockfiles** to reflect the new dependency versions.
4. **Commit all updated files** (`package.json` and lockfiles) together in a single commit.

**Files Involved:**
- `**/package.json`
- `**/package-lock.json`
- `**/pnpm-lock.yaml`

**Example Workflow:**
```bash
# Check for outdated dependencies
npm outdated

# Update dependencies in all packages
npm update

# Regenerate lockfiles
npm install

# Commit changes
git add **/package.json **/package-lock.json **/pnpm-lock.yaml
git commit -m "chore: update dependencies across packages"
```

## Testing Patterns

- **Test File Naming:** Test files follow the `*.test.*` pattern (e.g., `user-service.test.ts`).
- **Testing Framework:** Not explicitly detected; refer to project documentation or `package.json` for specifics.
- **Test Example:**
  ```typescript
  // user-service.test.ts
  import { getUser } from './user-service';

  test('should fetch user by ID', () => {
    expect(getUser(1)).toEqual({ id: 1, name: 'Alice' });
  });
  ```

## Commands

| Command              | Purpose                                                    |
|----------------------|------------------------------------------------------------|
| /update-dependencies | Bulk update dependencies across multiple packages/directories |
```
