# Post-Mortem Template

> Blameless. Within 48 hours of incident. Action items tracked.

---

## Incident Summary
- **Title:**
- **Severity:** (SEV-1 / SEV-2 / SEV-3)
- **Date:**
- **Duration:**
- **Author:**
- **Stakeholders:**

## Impact
- User-visible symptoms:
- Number of users affected:
- Revenue / data impact:
- SLA / SLO violation:

## Timeline (UTC)
| Time | Event |
|---|---|
| 00:00 | Alert fired |
| 00:05 | On-call ack |
| 00:10 | Mitigation applied |
| 00:30 | Resolved |

## Root Cause
What actually went wrong. Technical. Specific.

## Contributing Factors
- What made it worse?
- What failed to catch it?
- What delayed recovery?

## What went well
- Be specific. Praise good calls.

## What went poorly
- Be specific. No blame.

## Action Items
| Action | Owner | Due | Priority |
|---|---|---|---|
| Add alert for X | @alice | 1 week | P0 |
| Add runbook for Y | @bob | 2 weeks | P1 |
| Fix code in Z | @carol | 1 week | P0 |

## Lessons Learned
- Process improvements.
- Tooling improvements.
- Communication improvements.

## Appendix
- Logs.
- Metrics screenshots.
- Slack thread link.
- PagerDuty incident link.

---

## Rules

1. **Blameless.** No finger-pointing. Focus on systems, not people.
2. **Within 48 hours.** While memories are fresh.
3. **Action items tracked.** With owners and dates.
4. **Shared widely.** Post in #incidents. Discuss in next team meeting.
5. **Follow up.** Review action items weekly until closed.

---

**Back to:** [Checklists/](README.md) · [Monitoring/](../Monitoring/)
