# Session: Issue #2 - Session Helper Tools

## Details
- **Issue**: [#2](https://github.com/flexion/claude-memento/issues/2)
- **Branch**: issue/feature-2/session-tools
- **Created**: 2025-12-07
- **Status**: in-progress

## Objective
Build JavaScript tools for session creation, tracking, and updating. These tools give Claude persistent memory across conversation resets.

## Implementation Plan

### Directory Structure
```
.claude/
├── sessions/           # Session files (rich, detailed markdown)
├── branches/           # Branch metadata (compact, mapping)
└── tools/              # Session management tools (JavaScript)
    ├── session.js          # Core module (shared utilities)
    ├── create-session.js   # Create branch metadata + session file
    ├── get-session.js      # Find session from current branch
    └── update-session.js   # Add log entries, decisions, learnings
```

### Tools to Build

1. **session.js** - Core module
   - Git branch detection
   - Branch name parsing (feature/X, chore/X, fix/X, issue/feature-N/X)
   - Path utilities
   - Template loading

2. **create-session.js** - Session initialization
   - Parse current branch name
   - Detect session type (feature, chore, bug)
   - Create branch metadata file
   - Create session file from template

3. **get-session.js** - Session discovery
   - Read current branch
   - Find branch metadata
   - Return session file path and status

4. **update-session.js** - Session updates (NEW - not in reference impl)
   - --log: Add timestamped log entry
   - --decision: Add decision with rationale
   - --learning: Add learning entry
   - --status: Update session status
   - --next: Add/update next steps
   - --blocker: Document blocker

## Session Log

### 2025-12-07 - Session Started
- Created GitHub issue #2
- Created branch: issue/feature-2/session-tools
- Reviewed reference implementation in claude-domestique
- Identified gap: no update-session tool exists
- Created directory structure: sessions/, branches/, tools/
- Updated ROADMAP.md with tool specifications

## Key Decisions

### 1. Multi-platform support for issue trackers
**Decision**: Support GitHub, Jira, and Azure DevOps with auto-detection
**Rationale**: Different teams use different issue trackers; tool should be flexible

### 2. Branch naming patterns by platform
| Platform | Pattern | Identifier | Session File |
|----------|---------|------------|--------------|
| GitHub | `issue/feature-N/desc` | `#N` | `N-desc.md` |
| Jira | `feature/PROJ-123/desc` | `PROJ-123` | `PROJ-123-desc.md` |
| Azure DevOps | `feature/456/desc` | `#456` | `456-desc.md` |
| No issue | `chore/desc` | none | `chore-desc.md` |

### 3. Auto-detection logic
- `PROJ-123` pattern → Jira
- Numeric only → GitHub or Azure DevOps
- No number → Non-issue work (chore, feature)

### 4. Fallback behavior
If branch pattern doesn't match, use sanitized branch name as session filename

## Learnings
- Reference scripts are bash; we need JavaScript for Claude CLI compatibility
- update-session.js is new functionality not in reference implementation
- claude-domestique has work-items.yml with full platform config spec

## Files Changed
- .claude/sessions/2-session-tools.md (this file)
- .claude/branches/issue-feature-2-session-tools
- ROADMAP.md

## Next Steps
1. ~~Update ROADMAP.md with detailed tool specifications~~ ✓
2. Implement session.js core module
3. Implement create-session.js
4. Implement get-session.js
5. Implement update-session.js
