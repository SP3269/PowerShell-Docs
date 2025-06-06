---
description: ValidateRange Attribute Declaration
ms.date: 09/13/2016
title: ValidateRange Attribute Declaration
---
# ValidateRange Attribute Declaration

The ValidateRange attribute specifies the minimum and maximum values (the range) for the cmdlet parameter argument. This attribute can also be used by Windows PowerShell functions.

## Syntax

```csharp
[ValidateRange(object minRange, object maxRange)]
```

#### Parameters

`MinRange` ([System.Object](/dotnet/api/system.object))
Required. Specifies the minimum value allowed.

`MaxRange` ([System.Object](/dotnet/api/system.object))
Required. Specifies the maximum value allowed.

## Remarks

- The Windows PowerShell runtime throws a construction error when the value of the `MinRange` parameter is greater than the value of the `MaxRange` parameter.

- The Windows PowerShell runtime throws a validation error under the following conditions:

  - When the value of the argument is less than the `MinRange` limit or greater than the `MaxRange` limit.

  - When the argument is not of the same type as the `MinRange` and the `MaxRange` parameters.

- The ValidateRange attribute is defined by the [System.Management.Automation.ValidateRangeAttribute](/dotnet/api/System.Management.Automation.ValidateRangeAttribute) class.

## See Also

[System.Management.Automation.ValidateRangeAttribute](/dotnet/api/System.Management.Automation.ValidateRangeAttribute)

[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)
