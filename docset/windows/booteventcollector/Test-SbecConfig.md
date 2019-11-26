---
ms.mktglfcycl: manage
ms.sitesec: library
ms.author: v-anbarr
author: andreabarr
description: Use this topic to help manage Windows and Windows Server technologies with Windows PowerShell.
external help file: BootEventCollector-help.xml
keywords: powershell, cmdlet
manager: jasgro
ms.date: 12/20/2016
ms.prod: w10
ms.technology: powershell-windows
ms.topic: reference
online version: 
schema: 2.0.0
title: Test-SbecConfig
ms.reviewer:
ms.assetid: 69A2C9E8-4FAD-4C40-883E-0EAE358175E8
---

# Test-SbecConfig

## SYNOPSIS
Validates a configuration.

## SYNTAX

```
Test-SbecConfig [-Content] <String[]> [-Continue] [[-ComputerName] <String[]>] [[-CimSession] <CimSession[]>]
 [<CommonParameters>]
```

## DESCRIPTION
The **Test-SbecConfig** cmdlet validates a configuration for the Setup and Boot Event Collector.

This cmdlet checks a configuration for validity without applying it.
This is similar to running the command `bevtcol.exe -checkOnly`, except that **Test-SbecConfig** uses the running service to perform the validation.

The values that **Test-SbecConfig** returns are a subset of those returned by **Set-SbecActiveConfig**, because **Test-SbecConfig** does not apply the configuration.

You must have the Builtin Administrator privilege to run this command.

This cmdlet is also available using the alias **Validate-SbecConfig**.

## EXAMPLES

### Example 1: Validate a configuration
```
PS C:\> $res = Test-SbecConfig -Content $NewConfig -Continue
```

This command validates the configuration in $NewConfig, and then stores the results in the $res variable.
Because the *Continue* parameter is specified, the command does not throw an error if any errors occur.

### Example 2: Validate a configuration using the pipeline
```
PS C:\> Get-Content MyConfig.xml | Test-SbecConfig -Continue | Format-List
```

This command validates the configuration from a file.
Format-List prints all the returned information without reducing it.

### Example 3: Validate a configuration and throw on error
```
PS C:\> $res = Test-SbecConfig -Content (Get-Content MyConfig.xml)
```

Validate the configuration from a file and throw on error.

## PARAMETERS

### -CimSession
Runs the cmdlet on the remote computers through a remote session.
Enter a session object, such as the output of a **New-CimSession** or **Get-CimSession** cmdlet or an array of these objects.
The default is to run the cmdlet on the local computer.
For more information, see About_CimSession.

```yaml
Type: CimSession[]
Parameter Sets: (All)
Aliases: 

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ComputerName
Specifies the names of the computers on which you want to perform the operation.
You can specify a fully qualified domain name (FQDN), a NetBIOS name, or an IP address for each computer.
For more information see [Invoke-CimMethod](http://go.microsoft.com/fwlink/?LinkId=808801) on MSDN.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases: 

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Content
Specifies the configuration to validate.
The acceptable values for this parameter are:

- A multiline string.
Use `\n` to indicate line breaks. 
- An array of one-line strings.
This cmdlet merges the array.
- A mix of multiline strings and string arrays.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases: 

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Continue
Indicates that this operation will not throw an exception if a failure occurs.
Instead the caller should examine the output of the cmdlet for the error information.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### string[]
The text of the configuration, same as in the *Content* parameter.

## OUTPUTS

### hash table
The hash table includes the following elements: 

- `<Success>`
- `<ErrorType>`
- `<ErrorString>`
- `<WarningString>`
- `<InfoString>`

The `<ErrorType>` element contains 0 on success.
If a failure occurs, `<ErrorType>` has a code that describes the error: 

- 1 (bad argument format) 
- 2 (bad argument value)

The `<Success>` element is $True on success, $False otherwise.

`<ErrorString>`, `<WarningString>`, and `<InfoString>` contain detailed error messages.
`<ErrorString>` contains information only if an error occurs.

## NOTES

## RELATED LINKS

[Get-SbecActiveConfig](./Get-SbecActiveConfig.md)

[Set-SbecActiveConfig](./Set-SbecActiveConfig.md)

[Test-SbecActiveConfig](./Test-SbecActiveConfig.md)
