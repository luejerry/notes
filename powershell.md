# Notes on Powershell

## Unix equivalents

### Identical aliases
* `ls`
* `mv`
* `cp`
* `pwd`
* `rm`
* `cat`
* `echo`

### Commonly used mappings

| Unix | Powershell | Notes |
|------|------------|-------|
| `which` | `get-command` | |
| `more` | `oh -paging` | Space to page down, q to quit, no backwards paging |
| `man` | `man` | Use `man -examples` to view examples, and `man -online` to view online help |
| `find . -name "query"` | `gci -recurse -include "*query*"` | |
| `grep regexquery` | `sls regexquery` | |
| `head 10` | `select -first 10` | Does not stream when piped |
| `tail 10` | `select -last 10` | Does not stream when piped |
| `open` | `start` | |
| `~/.bashrc` | `$PROFILE` | |

## Using variables
* Create: `$var=0`
* Reference: `$var`

## Elevated shell
`Start-Process powershell -Verb runAs`

## Using and saving aliases
* Create: `New-Alias -Name grep -Description 'grep to select-string' Select-String`
* Save all aliases to file: `Export-Alias -Path "alias.csv"`
* Import aliases from file: `Import-Alias alias.csv`


## Enumerate properties of objects
Powershell cmdlets return PS objects, not strings as in Unix. By default, not
every property of the object is displayed to the terminal. To enumerate all
object properties, pipe a command output into `Format-List *`:

`Get-Command man | Format-List *`
