# Roadmap

## Core Concept

**1 Session = 1 Issue = 1 Branch = 1 Branch Metadata File**

Sessions persist work context across conversation resets, branch switches, and team handoffs.

## Directory Structure

```
.claude/
├── sessions/           # Session files (rich, detailed markdown)
│   ├── 123-add-auth.md
│   ├── fix-456-login-bug.md
│   └── chore-update-deps.md
├── branches/           # Branch metadata (compact mapping)
│   ├── issue-feature-123-add-auth
│   ├── fix-456-login-bug
│   └── chore-update-deps
└── tools/              # Session management tools (JavaScript)
    ├── session.js          # Core module (shared utilities)
    ├── create-session.js   # Create branch metadata + session file
    ├── get-session.js      # Find session from current branch
    └── update-session.js   # Add log entries, decisions, learnings
```

## Tools

### create-session.js
Create branch metadata and session file from current git branch.

```bash
# After creating a branch
git checkout -b issue/feature-123/add-authentication
.claude/tools/create-session.js

# Creates:
# - .claude/branches/issue-feature-123-add-authentication
# - .claude/sessions/123-add-authentication.md
```

### get-session.js
Find and display session info for current branch.

```bash
.claude/tools/get-session.js
# Output:
# Branch: issue/feature-123/add-authentication
# Session: .claude/sessions/123-add-authentication.md
# Status: in-progress
```

### update-session.js
Update session with log entries, decisions, learnings, status changes.

```bash
# Add a log entry
.claude/tools/update-session.js --log "Implemented JWT validation"

# Add a decision with rationale
.claude/tools/update-session.js --decision "Use HTTP-only cookies" --rationale "XSS protection"

# Add a learning
.claude/tools/update-session.js --learning "bcrypt auto-handles salt generation"

# Update status
.claude/tools/update-session.js --status "pr-created"

# Add next step
.claude/tools/update-session.js --next "Create PR for review"

# Add blocker
.claude/tools/update-session.js --blocker "Waiting for API spec from backend team"
```

---

## Phase 1: Foundation

- [ ] Create directory structure (sessions/, branches/, tools/)
- [ ] Define session file schema (markdown with structured sections)
- [ ] Create session templates (feature, chore, bug)
- [ ] Define branch metadata file format
- [ ] Implement `session.js` core module
  - [ ] Git branch detection
  - [ ] Branch name parsing (issue/feature-N/desc, chore/desc, fix/N/desc)
  - [ ] Path utilities
  - [ ] Template loading

## Phase 2: Core Tools

- [ ] Implement `create-session.js`
  - [ ] Parse current branch name
  - [ ] Detect session type (feature, chore, bug)
  - [ ] Create branch metadata file
  - [ ] Create session file from template
  - [ ] Handle existing files (prompt or error)
- [ ] Implement `get-session.js`
  - [ ] Read current branch
  - [ ] Find branch metadata
  - [ ] Return session file path and status
  - [ ] Fallback: guess session from branch name pattern
- [ ] Implement `update-session.js`
  - [ ] --log: Add timestamped log entry
  - [ ] --decision: Add decision with rationale
  - [ ] --learning: Add learning entry
  - [ ] --status: Update session status
  - [ ] --next: Add/update next steps
  - [ ] --blocker: Document blocker
  - [ ] --files: Add files changed

## Phase 3: Content Sections

- [ ] Session log with timestamps
- [ ] Decisions log with rationale
- [ ] Learnings capture
- [ ] Blockers documentation
- [ ] Files changed inventory
- [ ] Next steps tracking

## Phase 4: Integration

- [ ] Hook: Auto-load session on conversation start
- [ ] Hook: "What's next?" query handler
- [ ] Session file validation
- [ ] Git commit integration (session + code atomicity)
- [ ] Pre-commit hook to remind session update

## Phase 5: Polish

- [ ] Session templates customization
- [ ] Session archival on branch merge
- [ ] Session diff/history viewing
- [ ] Documentation and examples
- [ ] Interactive mode for update-session.js
