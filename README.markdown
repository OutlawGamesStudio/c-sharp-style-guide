# The Official Outlaw Games Studio C# Styling Convention

This style is a fork of Ray Wenderlich's C# Code Style [Here](https://github.com/raywenderlich/c-sharp-style-guide).

Our overarching goals are **conciseness**, **readability** and **simplicity**. Also, this guide is written to keep **Unity** in mind. 

## Inspiration

This style guide is based on C# and Unity conventions. 

## Table of Contents

- [Nomenclature](#nomenclature)
  + [Namespaces](#namespaces)
  + [Classes & Interfaces](#classes--interfaces)
  + [Methods](#methods)
  + [Fields](#fields)
  + [Parameters](#parameters--parameters)
  + [Delegates](#delegates--delegates)
  + [Events](#events--events)
  + [Misc](#misc)
- [Declarations](#declarations)
  + [Access Level Modifiers](#access-level-modifiers)
  + [Fields & Variables](#fields--variables)
  + [Classes](#classes)
  + [Interfaces](#interfaces)
- [Spacing](#spacing)
  + [Indentation](#indentation)
  + [Line Length](#line-length)
  + [Vertical Spacing](#vertical-spacing)
- [Brace Style](#brace-style)
- [Switch Statements](#switch-statements)
- [Language](#language)
- [Copyright Statement](#copyright-statement)
- [Smiley Face](#smiley-face)
- [Credit](#credits)


## Nomenclature

On the whole, naming should follow C# standards, see [Here](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions).

### Namespaces

Namespaces are all **PascalCase**, multiple words concatenated together, without hyphens ( - ) or underscores ( \_ ). The exception to this rule are acronyms like GUI or HUD, which can be uppercase:

**BAD**:

```csharp
com.outlawgamesstudio.fpsgame.hud.healthbar
```

**GOOD**:

```csharp
OutlawGamesStudio.FPSGame.HUD.Healthbar
```

### Classes & Interfaces

Written in **PascalCase**. For example `RadialSlider`. 

### Methods

Methods are written in **PascalCase**. For example `DoSomething()`. 

### Fields

All private class member fields must be prefixed with `m_` and all function member variables must be prefixed with `_`.
All public class members must be encapsulated within a property and their public interface must be in **PascalCase**.

For example:

**BAD:**

```csharp
public class MyClass 
{
    public int publicField;
    int packagePrivate;
    private int myPrivate;
    protected int myProtected;
}
```

**GOOD:**

```csharp
public class MyClass 
{
    private int m_PublicField;
    public int PublicField
    {
        get
        {
            return m_PublicField;
        }
        set
        {
            m_PublicField = value;
        }
    }

    int m_PackagePrivate;
    private int m_MyPrivate;
    protected int m_MyProtected;
}
```

**BAD:**

```csharp
private int myPrivateVariable
```

**GOOD:**

```csharp
private int m_MyPrivateVariable
```

Static fields are the exception and should be written in **PascalCase** with *no* prefix:

```csharp
public static int TheAnswer = 42;
```

### Parameters

Parameters are written in **camelCase**.

Single character values are to be avoided except for temporary looping variables, paramaters must also be concise as to what they are used for.

**BAD:**

```csharp
void DoSomething(Vector3 Location)
void DoSomething(Vector3 xyz)
```
**GOOD:**

```csharp
void DoSomething(Vector3 location)
```

### Delegates

Delegates are written in **PascalCase**.

When declaring delegates, DO add the suffix **EventHandler** and prefix **On** to names of delegates that are used in events.

**BAD:**

```csharp
public delegate void Click()
```
**GOOD:**

```csharp
public delegate void OnClickEventHandler()
```  

DO add the suffix **Callback** to names of delegates other than those used as event handlers.

**BAD:**

```csharp
public delegate void Render()
```
**GOOD:**

```csharp
public delegate void RenderCallback()
```  

### Events

Events should be written in **PascalCase**. Never prefix events with a prefix like **On**.

**BAD:**

```csharp
public static event CloseCallback OnClose;
```  

**GOOD:**

```csharp
public static event CloseCallback Close;
```

### Misc

In code, acronyms should be treated as words. For example:

**BAD:**

```csharp
XMLHTTPRequest
String URL
findPostByID
```  

**GOOD:**

```csharp
XmlHttpRequest
String url
findPostById
```

## Declarations

### Access Level Modifiers

Access level modifiers should be explicitly defined for classes, methods and member variables.

### Fields & Variables

Prefer single declaration per line.

**BAD:**

```csharp
string m_Username, m_TwitterHandle;
```

**GOOD:**

```csharp
string m_Username;
string m_TwitterHandle;
```

### Classes

Exactly one class per source file, although inner classes are encouraged where scoping appropriate.

### Interfaces

All interfaces should be prefaced with the letter **I**. 

**BAD:**

```csharp
RadialSlider
```

**GOOD:**

```csharp
IRadialSlider
```

## Spacing

Spacing is especially important in all code, as code needs to be easily readable. 

### Indentation

Indentation should be done using **spaces** — never tabs. You may use tabs if the IDE will replace it with the appropriate number of spaces.

#### Blocks

Indentation for blocks uses **4 spaces** for optimal readability:

**BAD:**

```csharp
for (int i = 0; i < 10; i++) 
{
  Debug.Log("index=" + i);
}
```

**GOOD:**

```csharp
for (int i = 0; i < 10; i++) 
{
    Debug.Log("index=" + i);
}
```

#### Line Wraps

Indentation for line wraps should use **4 spaces** (not the default 8):

**BAD:**

```csharp
CoolUiWidget widget =
        someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```

**GOOD:**

```csharp
CoolUiWidget widget =
    someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line);
```

### Line Length

Lines should be no longer than **100** characters long.

### Vertical Spacing

There should be exactly one blank line between methods to aid in visual clarity 
and organization. Whitespace within methods should separate functionality, but 
having too many sections in a method often means you should refactor into
several methods.


## Brace Style

All braces get their own line as it is a C# convention:

**BAD:**

```csharp
class MyClass {
    void DoSomething() {
        if (someTest) {
          // ...
        } else {
          // ...
        }
    }
}
```

**GOOD:**

```csharp
class MyClass
{
    void DoSomething()
    {
        if (someTest)
        {
          // ...
        }
        else
        {
          // ...
        }
    }
}
```

Conditional statements are always required to be enclosed with braces,
irrespective of the number of lines required.

**BAD:**

```csharp
if (someTest)
    doSomething();  

if (someTest) doSomethingElse();
```

**GOOD:**

```csharp
if (someTest) 
{
    DoSomething();
}  

if (someTest)
{
    DoSomethingElse();
}
```
## Switch Statements

Switch-statements come with `default` case by default (heh). If the `default` case is never reached, be sure to remove it.

**DEFAULT GETS USED:**  
  
```csharp
switch (variable) 
{
    case 1:
        break;
    case 2:
        break;
    default:
        break;
}
```

**DEFAULT DOESN'T GET USED:**  
  
```csharp
switch (variable) 
{
    case 1:
        break;
    case 2:
        break;
}
```

## Language

Prefer the use of UK English spelling.

**BAD:**

```csharp
string color = "red";
```

**GOOD:**

```csharp
string colour = "red";
```

## Copyright Statement

The following copyright statement should be included at the top of every source file:

```csharp
//
//  Copyright (C) 2018 Outlaw Games Studio. All Rights Reserved.
//
//  This document is the property of Outlaw Games Studio.
//  It is considered confidential and proprietary.
//
//  This document may not be reproduced or transmitted in any form
//  without the consent of Outlaw Games Studio.
//
```

## Strings

Prefer the use of string interpolation.

**BAD**
```csharp
string m_DisplayName = m_FirstName + " " + m_LastName;
Debug.Log(m_FirstName + " " + m_LastName);
```

**GOOD**
```csharp
string m_DisplayName = $"{m_FirstName} {m_LastName}";
Debug.Log($"{m_FirstName} {m_LastName}");
```

## Credits

### RayWenderlich
- [Darryl Bayliss](https://github.com/DarrylBayliss)
- [Sam Davies](https://github.com/sammyd)
- [Mic Pringle](https://github.com/micpringle)
- [Brian Moakley](https://github.com/VegetarianZombie)
- [Ray Wenderlich](https://github.com/rwenderlich)
- [Eric Van de Kerckhove](https://github.com/BlackDragonBE)

### Outlaw Games Studio
- [Sean McElholm](https://github.com/BlackDragonBE)