# claude-memento

> "Remember Sammy Jankis."

Like Leonard in *Memento*, Claude can't form long-term memories. claude-memento gives Claude its tattoos—session files that persist decisions, progress, and context across conversation resets.

## The Problem

In Christopher Nolan's *Memento* (2000), Leonard Shelby suffers from anterograde amnesia—he can't form new memories. Every few minutes, his slate wipes clean. To function, he tattoos critical facts on his body and leaves himself Polaroids and notes.

Claude has the same problem. Context window fills up, conversation resets, and everything learned—decisions made, approaches tried, dead ends discovered—vanishes.

## The Solution

claude-memento is Leonard's system for Claude: persistent session files that survive the reset, letting Claude wake up, read its own notes, and pick up exactly where it left off.

## Key Concepts

- **1 Session = 1 Issue = 1 Branch** - Clean mapping between work units
- **Atomic commits** - Session file versions WITH the code it describes
- **Progress checkpointing** - Update throughout work, not just at the end

## Features

- **Branch metadata files** - Compact lookup to find session from current branch
- **Session templates** - Standardized structure for feature vs chore sessions
- **Automatic context restoration** - Branch → session → next steps lookup
- **Session log** - Chronological record of what was done, when, and why
- **Key decisions documentation** - Captures WHY, not just WHAT
- **Learnings capture** - What surprised you, what would you do differently
- **Files changed tracking** - Inventory of modified files for handoff
- **Blockers documentation** - Capture what's blocking before stepping away

## Use Cases

- **Survives conversation resets** - Context window fills up, start new chat, read session, continue
- **Survives context compaction** - When Claude summarizes, session file has the real details
- **Team handoffs** - Teammate checks out branch, reads session, has full context

## Requirements

- Node.js (required by Claude CLI)
- All tools written in JavaScript

## License

MIT
