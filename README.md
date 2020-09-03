﻿# The Unity Style Guide

for projects on Unity Engine and C #

Our overarching goals are **conciseness**, **readability** and **simplicity**. Also, this guide is written to keep **Unity** in mind. 
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
  + [Line Length](#line-length)
  + [Vertical Spacing](#vertical-spacing)
- [Brace Style](#brace-style)
- [Switch Statements](#switch-statements)
- [Scriptable Objects](#scriptable-objects)
- [LifeCycle](#monobehaviour-lifecycle)
- [Structure of Folders](#structure-of-the-folders)
- [Additional Materials](#additional-material)

## Nomenclature

- On the whole, naming should follow C# standards.
- Use only English for names 

### Namespaces

Namespaces are all **PascalCase**, multiple words concatenated together, without hyphens ( - ) or underscores ( \_ ). The exception to this rule are acronyms like GUI or HUD, which can be uppercase:

**Try to AVOID**:

```csharp
com.green-blood.rtsgame.hud.manabar
```

**Try to USE**:

```csharp
Green-Blood.RTSGame.HUD.Manabar
```

### Classes & Interfaces

Classes and interfaces are written in **PascalCase**. For example `Cube`. 

### Methods

Methods are written in **PascalCase**. For example `DoSomething()`. 
The name of the method should describe its **behavior, purpose**. 

If you need a name
using And / Or / If is a bad method, split it up into parts.


For the Methods which call or change data use the construction action verb such as DoSomething () and ShowSomething ()

For the Methods which returns data use Get-an object such as GetSomething () or GetInfo () 

If the method explicitly changes the internal state,
and it must change from outside, use the Set-object construction, for example
SetSomething (objectSomeThing) and SetInfo (Info info).

### Fields

All public or serialized fields are written in **camelCase**. 

Names should say what is happening in code. don't use abbreviations, use **number** not **num**.


For example:

```csharp
public class MyClass 
{
    public int publicField;
    [SerializeField] int serializedField
    protected int myProtected;
}
```
All private fields are written in **camelCase** with **_** prefix. 

For example:
```csharp
public class MyClass 
{
    private int _privateField;
}
```

**Try to AVOID:**

```csharp
private int myPrivateVariable
```

**Try to Use:**

```csharp
private int _myPrivateVariable
```

For boolean fields try to use is, can, has, may prefix. 

For example:
```csharp
public class MyClass 
{
    private bool hasKey;
}
```




Static fields are the exception and should be written in **PascalCase**:

```csharp
public static int TheStaticField = 0;
```
### Properties

All properties are written in **PascalCase**. For example:

```csharp
public int Proprety 
{
    get { return propertValue; }
    set { propertValue = value; }
}
```

### Parameters

Parameters are written in **camelCase**.

**Try to AVOID:**

```csharp
void DoSomething(Vector3 Location)
```

**Try to Use:**

```csharp
void DoSomething(Vector3 location)
```

### Actions

Actions are written in **PascalCase**. For example:

```csharp
public event Action<int> ActionDone;
```

### Misc

In code, acronyms should be treated as words. For example:

**Try to AVOID:**

```csharp
HTTPRequest
String URL
findPostByID
```  

**Try to USE:**

```csharp
HttpRequest
String url
findPostById
```

## Declarations

### Access Level Modifiers

Access level modifiers should be explicitly defined for classes, methods and member variables.

### Fields & Variables

Prefer single declaration per line.

**Try to AVOID:**

```csharp
string username, twitterHandle;
```

**Try to USE:**

```csharp
string username;
string twitterHandle;
```

### Classes

Exactly one class per source file, although inner classes are encouraged where scoping appropriate.

### Interfaces

All interfaces should be prefaced with the letter **I**. 

**Try to AVOID:**

```csharp
RadialSlider
```

**Try to USE:**

```csharp
IRadialSlider
```

## Spacing

Spacing is important for readability 

#### Blocks

Indentation for blocks uses **4 spaces** for optimal readability:

**Try to AVOID:**

```csharp
for (int y = 0; y < 10; y++) 
{
  Debug.Log(y);
}
```

**PREFER:**

```csharp
for (int y = 0; y < 10; y++) 
{
    Debug.Log(y);
}
```

#### Line Wraps

It doesn't really matter, but try to use **8 spaces(2 tabs)**;
Most IDE's do it for you.  
 
### Line Length

Lines should be no longer than **100** characters long.

### Vertical Spacing

There should be exactly one blank line between methods to aid in visual clarity 
and organization. Whitespace within methods should separate functionality, but 
having too many sections in a method often means you should refactor into
several methods.


## Brace Style

All braces get their own line as it is a C# convention:

**Try to AVOID:**

```csharp
class MyClass {
    void DoSomething() {
        if (something) {
          // ...
        } else {
          // ...
        }
    }
}
```

**Try to USE:**

```csharp
class MyClass
{
    void DoSomething()
    {
        if (something)
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
irrespective of the number of lines required. Use **switch** if you are having more then 3 **if**'s. If you are having more than 5 cases, try to think about polymorphism. 

**Try to AVOID:**

```csharp
if (someTest)
    doSomething();  

if (someTest) doSomethingElse();
```

**Try to USE:**

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

**Try to AVOID:**  
  
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

**Try to USE:**  
  
```csharp
switch (variable) 
{
    case 1:
        break;
    case 2:
        break;
}
```
## Scriptable Objects
Try to use them, a lot. However, If Scriptable Object implements the behavior, it is wrong. Only the functionality of managing your data can be in it.
Because mostly it represent data. You should name it with postfixData
 
## MonoBehaviour LifeCycle
1. Awake is designed to initialize the internal default state of a component,
 with its default behavior. There should not be any dependencies in this method,
  for the simple reason that the objects themselves with dependency components may
   not yet exist.
2. OnEnable is used in most cases to subscribe to events.
 Remember that if you subscribe to an event, you always need to unsubscribe from it.
3. Start is designed to get dependencies. When all components are ready 
(awake has initialized their default state), 
you can get dependencies in Start. But it is better to inject them through the field marked with SerializeField, by specifying the dependency in the scene or prefab. 
4. OnDisable is used in most cases to unsubscribe from events that were subscribed to in OnEnable.
5. OnDestroy is needed only if the component grabs any resources.

## Structure of the Folders

Because we like to create big trash, **Try** to delete everything which is not needed anymore and add something new in strict accordance with the directory hierarchy

#### Directory names 
- *_Scenes* - the prefix dash is used to never lose scenes in a pile of directories
- *Prefabs* - for prefabs
- *Resources* - for prefabs which should initialized directly from code, like Resources.Load
- *Scripts* - for scripts, never forget to put classes into namespaces and in the corresponding directories.
- *Sprites* - for sprites, never forget to put Sprites in the corresponding directories. Try not to make a dump, putting everything into one folder. Try to split them, and use Sprite sheets.  
- *Reusables* - for Reusable content from project to project(Can be changed to Utils)
- *Animations* - for Animators and Animations 
- *Localisations* - for Localisations(I'm pron to use Unity's official localizer, but most of the people pron to use L2 )
- *Audios* - for audios
- *Custom Assets(optional)* - for storing third-party solutions(Plugins, Assets and etc.)

## Additional Material
- Custom exception class names always end with the "Exception" postfix
- Custom attribute names always end with the "Attribute" postfix
- Extension class names always end with the Extension postfix
- For a class that uses Prefs in itself and is an intermediary for storing data, the Prefs postfix should be used.(Actually, Try to use EasySave, or something else)
- Remove unused namespaces from using, taking into account that there is no use in excluded blocks by the #IF preprocessor
- Each class must be placed in the appropriate namespace
- There should be a line break after #region, just like before #endregion
- Define names must be capitalized, with a separator instead of an underscore problem. For example, #define MY_DEFINE.
- If you are having class with more than 100-200 lines, or method with more than 50 lines, think about refactoring  
- Use comment only if the method is to hard to understand by it's name. If you are having methods like that, you must comment it, so that you won't have problems in future.
- If you want to name component with postfix Manager, Controller, System, this means that your logic is wrong, and you should think about SOLID principles. Exceptions are MVC pattern(Model, View, Controller), ECS (ENTITY COMPONENT SYSTEM)  
- Use LINQ only in Awake or Start in other cases fps will drop, so it's better not to use it, this also applies to GetComponent, FinObjectOfType, and etc. Try to reference them, if possible.

 

 

