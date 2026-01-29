# Audit Procedures

> Version: 1.0.0  
> Type: Operational Procedures  
> Agent: Juno (AI Governance Officer)

## Pre-Audit Procedures

### 1. Verify Access
- Confirm read access to `antigravity/logs/shadow_mode_log.jsonl`
- Confirm read access to `antigravity/logs/policy_ledger.yml`
- Confirm read access to `.antigravity/agents/*.md`

### 2. Validate Contract
- Verify `governance_authority_contract_v1.yaml` is active
- Check contract version matches audit procedures version
- Review any recent contract amendments

---

## Audit Procedures by Type

### Agent Decision Audit

**Procedure**: `audit-agent.md`

1. Validate agent_id exists
2. Query shadow logs for agent decisions
3. For each decision:
   - Verify `impact_level` classification
   - Check HITL compliance if required
   - Flag policy violations
4. Generate audit report
5. Save to `antigravity/logs/audit_reports/`

**Frequency**: On-demand or quarterly

---

### Compliance Audit

**Procedure**: `compliance-check.md`

**Scope: Policy**
1. Verify ADR-013 compliance (no commodity builds)
2. Check `policy_ledger.yml` for unauthorized modifications
3. Validate all active policies are enforced

**Scope: Security**
1. Scan for hardcoded secrets in recent commits
2. Verify shadow logging is active
3. Check for privilege escalations without HITL

**Scope: Cost**
1. Query telemetry for token usage
2. Compare against budget baselines
3. Flag sessions exceeding 10x multiplier

**Frequency**: Weekly automated, on-demand manual

---

### HITL Queue Audit

**Procedure**: `validate-hitl-queue.md`

1. Read `antigravity/logs/hitl_queue.yml`
2. Validate schema compliance
3. Identify expired entries (timeout exceeded)
4. Update state to "expired"
5. Generate queue status summary

**Frequency**: Daily automated

---

### Ledger Integrity Audit

**Procedure**: `check-ledger-integrity.md`

1. Read `antigravity/logs/policy_ledger.yml`
2. Verify SHA256 chain:
   - For each entry: `entry_hash == SHA256(entry + previous_hash)`
3. Flag any breaks in chain
4. Generate integrity report

**Frequency**: Daily automated, before policy changes

---

## Post-Audit Procedures

### 1. Report Generation
- Save detailed report to `antigravity/logs/audit_reports/`
- Generate executive summary for founder
- Log audit completion to shadow log

### 2. Violation Escalation
- **INFO/WARNING**: Log only
- **VIOLATION**: Add to HITL queue
- **CRITICAL**: Immediate founder alert
- **EMERGENCY**: Kill switch activation

### 3. Recommendations
- Document improvement recommendations
- Propose policy updates if needed
- Track remediation via HITL queue

---

## Audit Evidence

All audits must collect:
- **Timestamp**: When audit was performed
- **Auditor**: Juno (ai-governance agent)
- **Scope**: What was audited
- **Evidence**: Raw data supporting findings
- **Correlation ID**: For end-to-end tracing

---

## Audit Retention

- **Audit reports**: 90 days
- **Shadow logs**: Indefinite (append-only)
- **Policy ledger**: Indefinite (append-only)
- **HITL queue**: 30 days after resolution

---

## Emergency Audit

If system integrity is compromised:
1. Halt all agent operations
2. Generate emergency audit across all scopes
3. Alert founder immediately
4. Document incident with full evidence
5. Await founder decision before resuming
