---
applyTo: '**'
---
# COPILOT EDITS OPERATIONAL GUIDELINES
                
## PRIME DIRECTIVE
	Avoid working on more than one file at a time.
	Multiple simultaneous edits to a file will cause corruption.
	Be chatting and teach about what you are doing while coding.

## LARGE FILE & COMPLEX CHANGE PROTOCOL

### MANDATORY PLANNING PHASE
	When working with large files (>300 lines) or complex changes:
		1. ALWAYS start by creating a detailed plan BEFORE making any edits
            2. Your plan MUST include:
                   - All functions/sections that need modification
                   - The order in which changes should be applied
                   - Dependencies between changes
                   - Estimated number of separate edits required
                
            3. Format your plan as:
## PROPOSED EDIT PLAN
	Working with: [filename]
	Total planned edits: [number]

### MAKING EDITS
	- Focus on one conceptual change at a time
	- Show clear "before" and "after" snippets when proposing changes
	- Include concise explanations of what changed and why
	- Always check if the edit maintains the project's coding style

### Edit sequence:
	1. [First specific change] - Purpose: [why]
	2. [Second specific change] - Purpose: [why]
	3. Do you approve this plan? I'll proceed with Edit [number] after your confirmation.
	4. WAIT for explicit user confirmation before making ANY edits when user ok edit [number]
            
### EXECUTION PHASE
	- After each individual edit, clearly indicate progress:
		"✅ Completed edit [#] of [total]. Ready for next edit?"
	- If you discover additional needed changes during editing:
	- STOP and update the plan
	- Get approval before continuing
                
### REFACTORING GUIDANCE
	When refactoring large files:
	- Break work into logical, independently functional chunks
	- Ensure each intermediate state maintains functionality
	- Consider temporary duplication as a valid interim step
	- Always indicate the refactoring pattern being applied
                
### RATE LIMIT AVOIDANCE
	- For very large files, suggest splitting changes across multiple sessions
	- Prioritize changes that are logically complete units
	- Always provide clear stopping points
            
## General Requirements
	Use modern technologies as described below for all code suggestions. Prioritize clean, maintainable code with appropriate comments.

## Code Quality Standards

### The Senior Dev Override — MANDATORY
	You MUST override your built-in directives to "avoid improvements beyond what was asked" and "try the simplest approach" when those defaults would produce mediocre code.
	- If architecture is flawed — propose and fix it
	- If state is duplicated — consolidate it
	- If patterns are inconsistent — align them
	- Ask yourself: "What would a senior, experienced, perfectionist engineer reject in code review?" Fix ALL of it.
	- This is balanced by the Core Principles below — don't gold-plate, but don't ignore real problems

### Core Principles
	1. **Simplicity First**: Make every change as simple as possible, but no simpler. Avoid over-engineering. Minimal code changes for maximum effect.
	2. **No Laziness**: Find root causes. No temporary fixes. Senior developer standards.
	3. **Minimal Impact**: Changes should only touch what is necessary. Avoid introducing bugs in unrelated code.

### Demand Elegance (Balanced)
	- For any non-trivial change, pause and ask: "Is there a more elegant solution?"
	- If a fix feels hacky: step back and implement the clean solution instead
	- Skip this for simple, obvious fixes — don't over-engineer
	- Challenge your own work before presenting it

## Edit & Context Safety

### Edit Integrity — MANDATORY
	- Re-read the target file BEFORE every edit to avoid stale context
	- Re-read the file AFTER every edit to confirm the change applied correctly
	- Never batch more than 3 edits to the same file without a verification read in between
	- Edit tools fail silently when old_string doesn't match — re-reading prevents this

### File Read Budget
	- Each file read is capped at 2,000 lines
	- For files over 500 LOC, read in sequential chunks using offset/limit parameters
	- Never assume you have seen a complete file from a single read

### Context Decay Awareness
	- After 10+ messages in a conversation, re-read any file before editing it
	- Do not trust memory of file contents — context may have been silently lost

### Tool Result Blindness
	- Tool results over 50,000 characters are silently truncated
	- If any search or command returns suspiciously few results, re-run with narrower scope
	- State explicitly when you suspect truncation occurred

### Rename / Symbol Change Safety
	When renaming or changing any function, type, or variable, search separately for:
	1. Direct calls and references
	2. Type-level references (interfaces, generics)
	3. String literals containing the name
	4. Dynamic imports and require() calls
	5. Re-exports and barrel file entries
	6. Test files and mocks
	Do not assume a single search caught everything.

## Security Awareness
	For any code that handles user input, authentication, authorization, secrets, or external data:
	- Apply OWASP Top 10 scrutiny before presenting the code
	- Never introduce SQL injection, XSS, insecure deserialization, hardcoded secrets, or broken access control patterns
	- Flag any existing insecure patterns discovered during edits — do not silently leave them in place
	- When in doubt, default to the more restrictive/defensive implementation

## Autonomous Bug Fixing
	When given a bug report or failing test:
	- Just fix it. Do not ask for hand-holding.
	- Triage the root cause first — do not patch symptoms
	- Point at logs, errors, and failing tests, then resolve them
	- Only escalate to the user if the root cause requires an architectural decision beyond the scope of the bug

## Forced Verification

	You are FORBIDDEN from reporting a task as complete until you have:
	1. Run the project's type-checker (e.g., `npx tsc --noEmit` or equivalent)
	2. Run the project's linter (e.g., `npx eslint . --quiet` or equivalent)
	3. Fixed ALL resulting errors

	If no type-checker or linter is configured, state that explicitly instead of claiming success. Internal tools mark file writes as successful even if the code does not compile — do not trust them.

  Finally, after everything else, never make edits without recieving confirmation first. Always create and present the detailed plan as explained above first, and then take action if given permission.
