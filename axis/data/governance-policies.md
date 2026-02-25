# Governance Policies

> Version: 1.0.0  
> Type: Knowledge Base  
> Agent: Juno (AI Governance Officer)

## Active Policies

### ADR-013: Build vs Integrate vs Ignore Policy

**Status**: Active  
**Location**: `antigravity/config/build-vs-integrate-policy.yml`

**Summary**:
- **BUILD**: Lucidity logic, governance logic, decision loops, shadow mode core
- **INTEGRATE**: Observability visuals, dashboards, BI analytics, commodity logging
- **IGNORE**: Non-decisional UX, redundant scaffolding, vanity metrics

**Prohibited Builds**: dashboards, time_series_db, custom_tracing_ui, bi_tools

**Enforcement**: Auto-block commodity build attempts

---

### HITL (Human-in-the-Loop) Policy

**Status**: Active  
**Source**: `governance_authority_contract_v1.yaml`

**Rules**:
- **Always HITL**: create_agent, modify_governance_policy, delete_core_component, access_identity_zone
- **Never HITL**: read_logs, generate_reports, query_metrics, flag_violations
- **Conditional HITL**: Based on ImpactLevel (LOW/MEDIUM/HIGH)

**MEDIUM Split**:
- **security_adjacent** → HITL required, no timeout
- **non_security** → HITL required, 1h timeout fallback to ADVISORY_ONLY

---

### Budget Policy

**Status**: Active  
**Baseline**: Session-based budget tracking  
**Threshold**: 10x multiplier triggers HITL

**Enforcement**:
- Budget exceeded → AUTO_BLOCK (LOW impact)
- 10x exceeded → HITL required

**Source**: `telemetry.policy.budget_tracker`

---

### Ledger Integrity Policy

**Status**: Active  
**Method**: Append-only with SHA256 chain  
**Validation**: Required before policy changes

**Rules**:
- All governance actions logged with `correlation_id`
- Each entry chained via `entry_hash = SHA256(entry + previous_hash)`
- Tampering detection via chain validation
- Write path: Single (Juno only)

---

### Conflict Resolution Policy

**Status**: Active  
**Precedence**: Founder > Juno > GovernanceEngine > Other Agents

**Founder Override**:
- Requires: explicit_command + reason
- Logging: Mandatory (with lesson_learned)
- Destination: `policy_ledger.yml`

---

## Policy Updates

All policy changes require:
1. HITL approval
2. Policy version increment
3. Update to this knowledge base
4. Notification to all agents via shadow log

## References

- ADR-013: [build-vs-integrate-policy.yml](file:///Users/emilyveiga/Documents/AXIS/antigravity/config/build-vs-integrate-policy.yml)
- Authority Contract: [governance_authority_contract_v1.yaml](file:///Users/emilyveiga/Documents/AXIS/antigravity/config/contracts/governance_authority_contract_v1.yaml)
