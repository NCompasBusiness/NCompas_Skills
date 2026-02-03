# Meeting to Actions

Extract action items from meeting notes or transcripts and generate a structured action items document.

## Usage

```
/meeting-to-actions <path-to-meeting-file>
```

Or paste meeting content directly after the command.

## Instructions

When the user invokes this skill, follow these steps:

1. **Read the input**: Accept meeting notes or transcript from either:
   - A file path provided by the user
   - Text pasted directly in the conversation

2. **Analyze the content**: Identify all action items by looking for:
   - Explicit assignments ("John will...", "Sarah to handle...")
   - Tasks with deadlines ("by Friday", "due next week")
   - Follow-up items ("need to", "should", "must", "action required")
   - Decisions that require implementation
   - Commitments made during the meeting

3. **Extract metadata for each action item**:
   - **Task**: Clear, actionable description of what needs to be done
   - **Owner**: Person responsible (use "TBD" if not specified)
   - **Deadline**: Due date if mentioned (use "TBD" if not specified)
   - **Priority**: Infer from context (High/Medium/Low)
   - **Notes**: Additional context, dependencies, or related discussion points

4. **Generate the output file**: Create `action_items.md` in the current directory with:

```markdown
# Action Items from Meeting

**Meeting Date:** [extracted or today's date]
**Generated:** [current date/time]

## Action Items

| Task | Owner | Deadline | Priority | Notes |
|------|-------|----------|----------|-------|
| [task description] | [owner] | [deadline] | [priority] | [notes] |

## Summary

- **Total Action Items:** [count]
- **High Priority:** [count]
- **Medium Priority:** [count]
- **Low Priority:** [count]
- **Unassigned Items:** [count of items with TBD owner]

## Next Steps

[Brief summary of immediate next steps and any blockers or dependencies identified]
```

5. **Confirm completion**: Tell the user the file was created and provide a brief summary of what was extracted.

## Examples

**Input (meeting notes):**
```
Team sync - Jan 15
Attendees: Alice, Bob, Carol

- Alice will update the API documentation by Friday
- Bob needs to review the PR #234 - high priority
- Carol to schedule follow-up meeting with stakeholders next week
- Decision: We'll use PostgreSQL for the new service
- Need someone to set up the CI pipeline
```

**Output highlights:**
- 4 action items extracted
- 1 unassigned item (CI pipeline setup)
- Priorities inferred from context
