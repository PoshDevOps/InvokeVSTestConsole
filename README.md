####What is it?

A [PoshDevOps](https://github.com/PoshDevOps/PoshDevOps) task that invokes [VSTest.Console.exe](https://msdn.microsoft.com/en-us/library/jj155796.aspx)

####How do I install it?

```PowerShell
Add-PoshDevOpsTask -Name "YOUR-CISTEP-NAME" -PackageId "InvokeVSTestConsole"
```

####What parameters are available?

#####IncludeDllPath
A String[] representing included .dll file paths. Either literal or wildcard paths are supported; default is all .dlls 
within your project root dir @ any depth containing `test` in their name not within a `packages` or `bin` directory (case insensitive)
```PowerShell
[String[]]
[ValidateCount(1,[Int]::MaxValue)]
[Parameter(
    ValueFromPipelineByPropertyName = $true)]
$IncludeDllPath = @(gci -Path $PoshDevOpsProjectRootDirPath -File -Recurse -Filter '*test*.dll' | ?{$_.FullName -notmatch '.*[/\\]packages|obj[/\\].*'}|%{$_.FullName})
```

#####ExcludeDllNameLike
A String[] representing .dll file names to exclude. Either literal or wildcard names are supported.
```PowerShell
[String[]]
[Parameter(
    ValueFromPipelineByPropertyName = $true)]
$ExcludeDllNameLike
```

#####Recurse
A Switch representing whether to recursively search directories below $IncludeDllPath.
```PowerShell
[Switch]
[Parameter(
    ValueFromPipelineByPropertyName = $true)]
$Recurse
```

#####TestCaseFilter
A String representing the `/TestCaseFilter` option of VSTest.Console.exe
```PowerShell
[String]
[Parameter(
    ValueFromPipelineByPropertyName = $true)]
$TestCaseFilter
```

#####Logger
A String representing the `/Logger` option of VSTest.Console.exe
```PowerShell
[String]
[Parameter(
    ValueFromPipelineByPropertyName = $true)]
$Logger
```

#####UseVsixExtensions
A Switch representing whether to pass the `/UseVsixExtensions` option to VSTest.Console.exe
```PowerShell
[String]
[Parameter(
    ValueFromPipelineByPropertyName = $true)]
$UseVsixExtensions
```

#####PathToVSTestConsoleExe
A String representing the path to VSTest.Console.exe
```PowerShell
[String]
[ValidateNotNullOrEmpty()]
[Parameter(
    ValueFromPipelineByPropertyName=$true)]
$PathToVSTestConsoleExe = 'C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\CommonExtensions\Microsoft\TestWindow\vstest.console.exe'
```

####What's the build status?
![](https://ci.appveyor.com/api/projects/status/qcsvd9rs60tb3lpt?svg=true)

