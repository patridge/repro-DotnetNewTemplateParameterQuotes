# Repro template attempt

Template attempting to reproduce an issue with spaces inside escaped quotes in parameters.

## Problem

When passing in a parameter value that needs matching quotation marks in it, the command fails when there is a space between the quotation marks and produces unexpected results when there is _not_ a space between the quotation marks (no quotation marks in result).

## Reproduction installation

1. Clone this repo.
1. Navigate to the cloned repo in PowerShell Core.
1. Install the template locally: `dotnet new --install repro-template`.
1. Run any of the commands below.

## Attempts that result in an error message

### Escaped via back tick with space

```PowerShell
dotnet new repro-quotes-spaces --someparameter="something needing `"escaped quotes`" in it."
```

Output (truncated to red error text):

```log
Invalid input switch:
  quotes in it.
```

### Escaped via backslash with space

```PowerShell
dotnet new repro-quotes-spaces --someparameter="something needing \"escaped quotes\" in it."
```

Output (truncated to red error text):

```log
Invalid input switch:
  quotes\ in it.
```

### Escaped via double quotes with space

```PowerShell
dotnet new repro-quotes-spaces --someparameter="something needing ""escaped quotes"" in it."
```

Output (truncated to red error text):

```log
Invalid input switch:
  quotes in it.
```

### Swapped single and double quotes with space

```PowerShell
dotnet new repro-quotes-spaces --someparameter='something needing "escaped quotes" in it.'
```

Output (truncated to red error text):

```log
Invalid input switch:
  quotes in it.
```

## Attempts that "work" but with invalid content

### Escaped via back tick (no space)

```PowerShell
dotnet new repro-quotes-spaces --someparameter="something needing `"escapedquotes`" (without spaces) in it."
```

Invalid replacement result:

```text
something needing escapedquotes (without spaces) in it.
```

### Escaped via backslash (no space)

```PowerShell
dotnet new repro-quotes-spaces --someparameter="something needing \"escapedquotes\" (without spaces) in it."
```

Invalid replacement result:

```text
something needing \escapedquotes\ (without spaces) in it.
```

### Escaped via double quotes (no space)

```PowerShell
dotnet new repro-quotes-spaces --someparameter="something needing ""escapedquotes"" (without spaces) in it."
```

Invalid replacement result:

```text
something needing escapedquotes (without spaces) in it.
```

### Swapped single and double quotes (no space)

```PowerShell
dotnet new repro-quotes-spaces --someparameter='something needing "escapedquotes" (without spaces) in it.'
```

Invalid replacement result:

```text
something needing escapedquotes (without spaces) in it.
```

## Templated content to replace

{someparameter}

## Platform

Windows 10 Pro 1803
.NET Core SDK: v2.1.500 (also tested on v2.1.302)
PowerShell Core: v6.1.0
