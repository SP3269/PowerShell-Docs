---
description: TypeName Element for EntrySelectedBy for CustomEntry for View
ms.date: 08/25/2021
title: TypeName Element for EntrySelectedBy for CustomEntry for View
---
# TypeName Element for EntrySelectedBy for CustomEntry for View

Specifies a .NET type that uses this definition of the custom control view. There is no limit to the
number of types that can be specified for a definition.

## Schema

- Configuration Element
- ViewDefinitions Element
- View Element
- CustomControl Element
- CustomEntries Element
- CustomEntry Element
- EntrySelectedBy Element
- TypeName Element

## Syntax

```xml
<TypeName>Nameof.NetType</TypeName>
```

## Attributes and Elements

The following sections describe attributes, child elements, and the parent element of the `TypeName`
element.

### Attributes

None.

### Child Elements

None.

### Parent Elements

|Element|Description|
|-------------|-----------------|
|[EntrySelectedBy Element for CustomEntry for View](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)|Defines the .NET types that use this custom control view definition or the condition that must exist for this definition to be used.|

## Text Value

Specify the fully qualified name of the .NET type, such as `System.IO.DirectoryInfo`.

## Remarks

Each custom control view definition must have at least one type name, selection set, or selection
condition defined.

For more information about the components of a custom control view, see [Creating Custom Controls](./creating-custom-controls.md).

## See Also

[Creating Custom Controls](./creating-custom-controls.md)

[EntrySelectedBy Element for CustomEntry for View](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)

[Writing a PowerShell Formatting File](./writing-a-powershell-formatting-file.md)
