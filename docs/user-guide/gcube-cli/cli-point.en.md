# **gcube CLI — point**

Check your point balance and usage history.

---

## **Point Query**

```bash
gcube point status                           # Balance and cumulative usage
gcube point spending                         # Daily usage for the current month
gcube point spending --month 2026-03         # Query a specific month
gcube point spending --workload <SER>        # Filter by workload
```

`point status` output example:

```
Available Point:      50,000 P
Charged Point:       100,000 P
Spent Point:          50,000 P
Network Point:             0 P

Spending Summary:
  Total:             50,000 P
  Prev Month:        20,000 P
  This Month:        30,000 P
```

!!! note "Point Field Descriptions"

    | Field | Description |
    |---|---|
    | `Available Point` | Current usable balance |
    | `Charged Point` | Total cumulative charged amount |
    | `Spent Point` | Total cumulative spent amount |
    | `Network Point` | Points deducted based on network traffic usage |

    !!! question "Review Needed"
        The exact billing criteria for `Network Point` (traffic unit, applicable conditions, etc.) should be confirmed with the development team.

---

<div style="text-align: center;" markdown>
[Next: Registry Credentials →](cli-credential.en.md){ .md-button .md-button--primary }
</div>
