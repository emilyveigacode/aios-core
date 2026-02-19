# Audit Agent Decisions

> Task ID: juno-audit-agent  
> Agent: Juno (AI Governance Officer)  
> Version: 1.0.0

## Task Definition

```yaml
task: auditAgent(agent_id)
responsável: Juno (Guardian)
atomic_layer: Governance

**Entrada:**
- campo: agent_id
  tipo: string
  origem: User Input
  obrigatório: true
  validação: Valid agent ID from AXIS ecosystem

**Saída:**
- campo: audit_report
  tipo: object
  destino: File (antigravity/logs/audit_reports/{agent_id}_{timestamp}.json)
  persistido: true
```

## Description

Audit all decisions and actions taken by a specific agent by querying shadow logs, analyzing compliance with governance policies, and generating detailed audit report.

## Workflow

### Steps

1. **Validate Agent ID**
   - Check agent exists in `.antigravity/agents/{agent_id}.md`
   - Validation: Agent file exists

2. **Query Shadow Logs**
   - Read `antigravity/logs/shadow_mode_log.jsonl`
   - Filter by `agent_id`
   - Extract all decision entries
   - Validation: At least one log entry found (or empty report if none)

3. **Analyze Compliance**
   - Check each decision against `governance_authority_contract_v1.yaml`
   - Verify HITL requirements were met
   - Verify impact_level classification was correct
   - Flag any policy violations

4. **Generate Audit Report**
   - Create JSON report with:
     - Total decisions made
     - HITL compliance rate
     - Policy violations (if any)
     - Recommendations
   - Save to `antigravity/logs/audit_reports/`

## Output Format

```json
{
  "agent_id": "dev",
  "audit_timestamp": "2026-01-15T22:00:00-03:00",
  "period": "all_time",
  "total_decisions": 127,
  "hitl_compliance": {
    "required": 14,
    "obtained": 14,
    "rate": 1.0
  },
  "violations": [],
  "recommendations": ["Consider reducing MEDIUM impact operations"]
}
```

## Success Criteria

- [ ] Agent ID validated
- [ ] Shadow logs queried successfully
- [ ] Audit report generated
- [ ] No critical errors
