# powershell

## Get-Help

```bash
Get-Help *COMMAND [-Verb Start|Stop|XXX ][-Full] [-Examples] [-Parameter *] [| more]
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