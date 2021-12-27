# powershell

## Get-Help

```bash
Get-Help *COMMAND [-Verb VERB] [-Full] [-Examples] [-Parameter *] [| more]
```

## Import-Module

```bash
Import-Module .\FILE [-Verbose]
Get-Command -Module MODULE_NAME
```

## Output Formatting

```bash
Format-Table
Format-List

Out-GridView (opens a ui-based viewer)
Out-File .\FILE
```

## multi-line strings

```bash
@"
blah
blah
"
```

## count

```bash
COMMAND| Measure-Object
(COMMAND).count
```