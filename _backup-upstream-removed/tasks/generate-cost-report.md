# Generate Cost Report

> Task ID: juno-generate-cost-report  
> Agent: Juno (AI Governance Officer)  
> Version: 1.0.0

## Description

Generate comprehensive token/API cost report from telemetry data.

## Workflow

1. Query telemetry for token usage per session
2. Calculate costs (tokens * model pricing)
3. Group by agent, model, session
4. Identify top cost drivers
5. Generate report with recommendations

## Output

```json
{
  "period": "last_7_days",
  "total_tokens": 1247893,
  "estimated_cost_usd": 4.72,
  "by_agent": {
    "dev": {"tokens": 647231, "cost": 2.45},
    "architect": {"tokens": 392847, "cost": 1.49}
  },
  "budget_status": "68% of monthly limit"
}
```

## Success Criteria

- [ ] Telemetry queried
- [ ] Costs calculated
- [ ] Report generated
