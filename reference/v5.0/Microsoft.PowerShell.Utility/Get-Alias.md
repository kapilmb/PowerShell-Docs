---
external help file: PSITPro5_Utility.xml
online version: http://go.microsoft.com/fwlink/p/?linkid=293964
schema: 2.0.0
---

# Get-Alias
## SYNOPSIS
Gets the aliases for the current session.

## SYNTAX

### UNNAMED_PARAMETER_SET_1
```
Get-Alias [[-Name] <String[]>] [-Exclude <String[]>] [-Scope <String>]
```

### UNNAMED_PARAMETER_SET_2
```
Get-Alias [-Definition <String[]>] [-Exclude <String[]>] [-Scope <String>]
```

## DESCRIPTION
The Get-Alias cmdlet gets the aliases (alternate names for commands and executable files) in the current session.
This includes built-in aliases, aliases that you have set or imported, and aliases that you have added to your Windows PowerShell profile.

By default, Get-Alias takes an alias and returns the command name.
When you use the Definition parameter, Get-Alias takes a command name and returns its aliases.

Beginning in Windows PowerShell 3.0, Get-Alias displays non-hyphenated alias names in an \<alias\> -\> \<definition\> format to make it even easier to find the information that you need.

## EXAMPLES

### Example 1: Get all aliases in the current session
```
PS C:\>Get-Alias
CommandType     Name

-----------     ----

Alias           % -> ForEach-Object

Alias           ? -> Where-Object

Alias           ac -> Add-Content

Alias           asnp -> Add-PSSnapin

Alias           cat -> Get-Content

Alias           cd -> Set-Location

Alias           chdir -> Set-Location

Alias           clc -> Clear-Content

Alias           clear -> Clear-Host

Alias           clhy -> Clear-History …
```

This command gets all aliases in the current session.

The output shows the \<alias\> -\> \<definition\> format that was introduced in Windows PowerShell 3.0.
This format is used only for aliases that do not include hyphens, because aliases with hyphens are typically preferred names for cmdlets and functions, rather than nicknames.

### Example 2: Get aliases by name
```
PS C:\>Get-Alias -Name g*, s* -Exclude Get-*
```

This command gets all aliases that begin with g or s, except for aliases that begin with Get-.

### Example 3: Get aliases for a cmdlet
```
PS C:\>Get-Alias -Definition Get-ChildItem
```

This command gets the aliases for the Get-ChildItem cmdlet.

By default, the Get-Alias cmdlet gets the item name when you know the alias.
The Definition parameter gets the alias when you know the item name.

### Example 4: Get aliases by property
```
PS C:\>Get-Alias | Where-Object {$_.Options -Match "ReadOnly"}
```

This command gets all aliases in which the value of the Options property is ReadOnly.
This command provides a quick way to find the aliases that are built into Windows PowerShell, because they have the ReadOnly option.

Options is just one property of the AliasInfo objects that Get-Alias gets.
To find all properties and methods of AliasInfo objects, type Get-Alias | get-member.

### Example 5: Get aliases by name and filter by beginning letter
```
PS C:\>Get-Alias -Definition "*-PSSession" -Exclude e* -Scope Global
```

This example gets aliases for commands that have names that end in -PSSession, except for those that begin with e.

The command uses the Scope parameter to apply the command in the global scope.
This is useful in scripts when you want to get the aliases in the session.

## PARAMETERS

### -Definition
Gets the aliases for the specified item.
Enter the name of a cmdlet, function, script, file, or executable file.

This parameter is called Definition, because it searches for the item name in the Definition property of the alias object.

```yaml
Type: String[]
Parameter Sets: UNNAMED_PARAMETER_SET_2
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Exclude
Omits the specified items.
The value of this parameter qualifies the Name and Definition parameters.
Enter a name, a definition, or a pattern, such as s*.
Wildcards are permitted.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name
Specifies the aliases to retrieve.
Wildcards are permitted.
By default, Get-Alias retrieves all aliases defined for the current session.
The parameter name Name is optional.
You can also pipe alias names to Get-Alias.

```yaml
Type: String[]
Parameter Sets: UNNAMED_PARAMETER_SET_1
Aliases: 

Required: False
Position: 1
Default value: None
Accept pipeline input: True (ByValue, ByPropertyName)
Accept wildcard characters: False
```

### -Scope
Gets only the aliases in the specified scope.
The acceptable values for this parameter are:

- Global
- Local
- Script
- A number relative to the current scope (0 through the number of scopes, where 0 is the current scope and 1 is its parent)

Local is the default.
For more information, see about_Scopes.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## INPUTS

### System.String
You can pipe alias names to Get-Alias.

## OUTPUTS

### System.Management.Automation.AliasInfo
Get-Alias returns an object that represents each alias.
Get-Alias returns the same object for every alias, but Windows PowerShell uses an arrow-based format to display the names of non-hyphenated aliases.

## NOTES
* To create a new alias, use Set-Alias or New-Alias. To delete an alias, use Remove-Item.
* The arrow-based alias name format is not used for aliases that include a hyphen. These are likely to be preferred substitute names for cmdlets and functions, instead of typical abbreviations or nicknames.

## RELATED LINKS

[About Aliases](https://technet.microsoft.com/en-us/library/hh847830.aspx)

[Export-Alias](f2ebfdac-0af9-4bf1-bef9-2b612381f3e6)

[Import-Alias](c4368ff1-c02a-47aa-b5c0-80503a20b4da)

[New-Alias](e77672bd-900b-4267-a07d-dab0d7957208)

[Set-Alias](b77236fb-e34f-4ac9-b8f7-9682dcb08593)

[Alias Provider](dce3f872-aeff-4eb2-8b38-876cd612fc29)
