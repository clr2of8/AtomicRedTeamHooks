# AtomicRedTeamHooks

This is a module that defines empty functions for use with the [Invoke-AtomicRedTeam Execution Framework](https://github.com/redcanaryco/invoke-atomicredteam/wiki)

Copy the files from this repository into a folder called **AtomicRedTeamHooks** in your `$env:PSModulePath`

Put code that you want to run before and after atomic execution and/or before and after atomic cleanup command execution (see *AtomicRedTeamHooks.ps1*).

```powershell
function Invoke-ARTPreAtomicHook ($atomic,$inputArgs){ }
function Invoke-ARTPostAtomicHook ($atomic,$inputArgs){ }
function Invoke-ARTPreAtomicCleanupHook ($atomic,$inputArgs){ }
function Invoke-ARTPostAtomicCleanupHook ($atomic,$inputArgs){ }
```