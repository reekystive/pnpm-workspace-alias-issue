# pnpm Workspace Alias Issue

This repository is a minimal reproduction of an issue [pnpm/pnpm#9683](https://github.com/pnpm/pnpm/issues/9683) with pnpm workspace aliases.

## Setup

- pnpm version: 10.12.1
- Workspace structure:

```plain
packages/
├── pkg-a/           # non-scoped package (pkg-a)
└── scoped-pkg-b/    # scoped package (@scoped/pkg-b)
```

## Issue

In the root package.json, the following dependencies are defined:

```json
{
  "dependencies": {
    "aliased-pkg-a": "npm:pkg-a@workspace:1.0.0",
    "aliased-pkg-b": "npm:@scoped/pkg-b@workspace:1.0.0"
  }
}
```

## Expected Behavior

Both aliases should resolve correctly to their respective workspace packages.

## Actual Behavior

- ✅ aliased-pkg-b (scoped package) works correctly
- ❌ aliased-pkg-a (non-scoped package) fails to resolve

## Environment

- pnpm version: 10.12.1
- Node.js version: 22.15.0
- OS: macOS 26.0

## Additional Context

This issue specifically affects non-scoped packages when using the `npm:package@workspace:version`
alias syntax in pnpm workspaces.
