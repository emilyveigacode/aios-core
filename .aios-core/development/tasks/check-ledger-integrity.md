# Check Ledger Integrity

> Task ID: juno-check-ledger-integrity  
> Agent: Juno (AI Governance Officer)  
> Version: 1.0.0

## Description

Verify SHA256 chain integrity of policy ledger to detect tampering.

## Workflow

1. Read `antigravity/logs/policy_ledger.yml`
2. Verify each entry has `entry_hash` field
3. Recalculate SHA256(entry + previous_hash)
4. Compare with stored hash
5. Report any breaks in chain

## Output

```json
{
  "ledger_path": "antigravity/logs/policy_ledger.yml",
  "total_entries": 47,
  "integrity_verified": true,
  "broken_chain_at": null
}
```

## Success Criteria

- [ ] Ledger readable
- [ ] All hashes verified
- [ ] Report generated
