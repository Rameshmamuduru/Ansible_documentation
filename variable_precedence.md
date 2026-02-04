```
| Order | Source                               | Real Usage |
| ----- | ------------------------------------ | ---------- |
| 1     | Role defaults (`roles/.../defaults`) | fallback   |
| 2     | Inventory vars                       | small labs |
| 3     | group_vars                           | MAIN PROD  |
| 4     | host_vars                            | per-host   |
| 5     | vars_files                           | secrets    |
| 6     | playbook vars                        | rare       |
| 7     | extra vars (`-e`)                    | CI/CD      |
```
