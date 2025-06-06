---
description: Defines what a script block is and explains how to use script blocks in the PowerShell programming language.
Locale: en-US
ms.date: 11/28/2023
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.core/about/about_script_blocks?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Script_Blocks
---
# about_Script_Blocks

## Short description

Defines what a script block is and explains how to use script blocks in
the PowerShell programming language.

## Long description

In the PowerShell programming language, a script block is a collection of
statements or expressions that can be used as a single unit. The collection of
statements can be enclosed in braces (`{}`), defined as a function, or saved in
a script file. A script block can return values and accept parameters and
arguments.

Syntactically, a script block is a statement list in braces, as shown in
the following syntax:

```
{<statement list>}
```

A script block returns the output of all the commands in the script block,
either as a single object or as an array.

You can also specify a return value using the `return` keyword. The `return`
keyword doesn't affect or suppress other output returned from your script
block. However, the `return` keyword exits the script block at that line. For
more information, see [about_Return][04].

Like functions, a script block can include parameters. Use the `param`
keyword to assign named parameters, as shown in the following syntax:

```
{
    param ([type]$Parameter1 [,[type]$Parameter2])
    <statement list>
}
```

> [!NOTE]
> In a script block, unlike a function, you can't specify parameters outside
> the braces.

Like functions, script blocks can include the `dynamicparam`, `begin`,
`process`, and `end` keywords. For more information, see [about_Functions][02]
and [about_Functions_Advanced][01].

## Using Script Blocks

A script block is an instance of a Microsoft .NET Framework type
`System.Management.Automation.ScriptBlock`. Commands can have script
block parameter values. For example, the `Invoke-Command` cmdlet has a
`ScriptBlock` parameter that takes a script block value, as shown in this
example:

```powershell
Invoke-Command -ScriptBlock { Get-Process }
```

```Output
Handles  NPM(K)    PM(K)     WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----     ----- -----   ------     -- -----------
999          28    39100     45020   262    15.88   1844 communicator
721          28    32696     36536   222    20.84   4028 explorer
...
```

`Invoke-Command` can also execute script blocks that have parameter blocks.
Parameters are assigned by position using the **ArgumentList** parameter.

```powershell
Invoke-Command -ScriptBlock { param($p1, $p2)
"p1: $p1"
"p2: $p2"
} -ArgumentList "First", "Second"
```

```Output
p1: First
p2: Second
```

The script block in the preceding example uses the `param` keyword to
create a parameters `$p1` and `$p2`. The string "First" is bound to the
first parameter (`$p1`) and "Second" is bound to (`$p2`).

For more information about the behavior of **ArgumentList**, see
[about_Splatting][05].

You can use variables to store and execute script blocks. The example below
stores a script block in a variable and passes it to `Invoke-Command`.

```powershell
$a = { Get-Service BITS }
Invoke-Command -ScriptBlock $a
```

```Output
Status   Name               DisplayName
------   ----               -----------
Running  BITS               Background Intelligent Transfer Ser...
```

The call operator is another way to execute script blocks stored in a variable.
Like `Invoke-Command`, the call operator executes the script block in a child
scope. The call operator can make it easier for you to use parameters with your
script blocks.

```powershell
$a ={ param($p1, $p2)
"p1: $p1"
"p2: $p2"
}
&$a -p2 "First" -p1 "Second"
```

```Output
p1: Second
p2: First
```

You can store the output from your script blocks in a variable using
assignment.

```
PS>  $a = { 1 + 1}
PS>  $b = &$a
PS>  $b
2
```

```
PS>  $a = { 1 + 1}
PS>  $b = Invoke-Command $a
PS>  $b
2
```

For more information about the call operator, see [about_Operators][03].

## Using delay-bind script blocks with parameters

A typed parameter that accepts pipeline input enables use of _delay-bind_
script blocks on the parameter. You can use delay-bind script blocks as a
shorthand to define parameters for a pipelined cmdlet before executing it.

Within the delay-bind script block, you can reference the piped in object
using the pipeline variable `$_`.

```powershell
# Both examples rename config.log to old_config.log
# Without delay-binding
dir config.log | ForEach-Object -Process {
  Rename-Item -Path $_ -NewName "old_$($_.Name)"
}
# With delay-binding
dir config.log | Rename-Item -NewName { "old_$($_.Name)" }
```

In more complex cmdlets, delay-bind script blocks allow the reuse of one piped
in object to populate other parameters.

Notes on delay-bind script blocks as parameters:

- You must explicitly specify any parameter names you use with delay-bind
  script blocks.
- The parameter must not be untyped, and the parameter's type can't be
  `[scriptblock]` or `[Object]`.
- You receive an error if you use a delay-bind script block without providing
  pipeline input.

  ```powershell
  Rename-Item -NewName {$_.Name + ".old"}
  ```

  ```Output
  Rename-Item : Cannot evaluate parameter 'NewName' because its argument is
  specified as a script block and there is no input. A script block cannot
  be evaluated without input.
  At line:1 char:23
  +  Rename-Item -NewName {$_.Name + ".old"}
  +                       ~~~~~~~~~~~~~~~~~~
      + CategoryInfo          : MetadataError: (:) [Rename-Item],
        ParameterBindingException
      + FullyQualifiedErrorId : ScriptBlockArgumentNoInput,
        Microsoft.PowerShell.Commands.RenameItemCommand
  ```

## See also

- [about_Functions][02]
- [about_Functions_Advanced][01]
- [about_Operators][03]

<!-- link references -->
[01]: about_Functions_Advanced.md
[02]: about_Functions.md
[03]: about_Operators.md
[04]: about_Return.md
[05]: about_Splatting.md#splatting-with-arrays
