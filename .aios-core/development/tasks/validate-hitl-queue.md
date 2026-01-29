# Validate HITL Queue

> Task ID: juno-validate-hitl-queue  
> Agent: Juno (AI Governance Officer)  
> Version: 1.0.0

## Description

Validate HITL queue integrity, process expired entries, and generate status report.

## Workflow

1. Read `antigravity/logs/hitl_queue.yml`
2. Check for malformed entries
3. Identify expired entries (timeout exceeded)
4. Update state to "expired" for timed-out entries
5. Generate queue status report

## Output

Console report showing:
- Total pending
- Total approved
- Total rejected
- Total expired
- Oldest pending entry (if any)

## Success Criteria

- [ ] Queue file readable
- [ ] All entries validated
- [ ] Expired entries updated
