# Check Compliance

> Task ID: juno-compliance-check  
> Agent: Juno (AI Governance Officer)  
> Version: 1.0.0

## Task Definition

```yaml
task: checkCompliance(scope)
responsável: Juno (Guardian)
atomic_layer: Governance

**Entrada:**
- campo: scope
  tipo: string
  origem: User Input
  obrigatório: true
  validação: One of: policy|security|cost|all

**Saída:**
- campo: compliance_report
  tipo: object
  destino: Memory
  persistido: false
```

## Description

Check compliance across specified scope (policy, security, cost, or all) and generate report with violations and recommendations.

## Workflow

### Scope: policy
1. Verify all agents comply with `governance_authority_contract_v1.yaml`
2. Check `policy_ledger.yml` for unauthorized modifications
3. Validate ADR-013 compliance (Build vs Integrate)

### Scope: security
1. Check for hardcoded secrets in recent commits
2. Verify shadow logging is active
3. Check for unauthorized privilege escalations

### Scope: cost
1. Query telemetry for token usage by session
2. Compare against budget limits
3. Flag sessions exceeding 10x baseline

### Scope: all
Run all checks above and generate consolidated report.

## Output Format

```json
{
  "scope": "all",
  "timestamp": "2026-01-15T22:00:00-03:00",
  "policy_compliance": {"status": "pass", "violations": []},
  "security_compliance": {"status": "pass", "violations": []},
  "cost_compliance": {"status": "warning", "budget_usage": "68%"},
  "overall_status": "warning"
}
```

## Success Criteria

- [ ] Scope validated
- [ ] All checks completed
- [ ] Report generated
