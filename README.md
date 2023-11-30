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

Here is an example of accessing the elements of the atomic from inside the hook:

```powershell
function Invoke-ARTPreAtomicHook ($atomic,$inputArgs){
    Write-Host -fore cyan $atomic.name.trim
    Write-Host -fore cyan $atomic.auto_generated_guid
    Write-Host -fore cyan $atomic.executor.cleanup_command
    Write-Host -fore cyan $atomic.executor.name
    Write-Host -fore cyan $atomic.executor.command 
    Write-Host -fore cyan $atomic.input_arguments
    Write-Host -fore cyan $atomic.executor.elevation_required 
    Write-Host -fore cyan $atomic.supported_platforms
    foreach ($dep in $atomic.dependencies) {
        Write-Host -fore yellow $dep.description
        Write-Host -fore yellow $dep.prereq_command
        Write-Host -fore yellow $dep.get_prereq_command
    }
    foreach ($key in $inputArgs.Keys) {
        Write-Host -fore red $key
        Write-Host -fore red $inputArgs[$key]
    }
    Write-Host -fore cyan $atomic.executor.cleanup_command
 }
 ```