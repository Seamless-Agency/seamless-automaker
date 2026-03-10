# Context Notes

## Dependency graph worktree filter

- The dependency graph previously filtered `features` to the selected worktree inside `apps/ui/src/components/views/graph-view/graph-view.tsx` before graph-specific filtering ran.
- Because of that early filter, the graph could not support an `All Worktrees` view even though each feature already exposes `branchName`.
- The correct change surface was the graph view stack:
  - `graph-view.tsx` to stop pre-filtering features
  - `hooks/use-graph-filter.ts` to add project-aware worktree filtering and a stable `Main` label
  - `graph-canvas.tsx` to own `selectedWorktrees` state and reset it with other filters
  - `components/graph-filter-controls.tsx` to render a worktree multi-select next to category and status filters
  - `graph-view-page.tsx` to aggregate running auto-mode tasks across project worktrees so status filters remain accurate when cross-worktree cards are visible
