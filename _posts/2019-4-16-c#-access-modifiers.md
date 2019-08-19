---
layout: post
title: C# Access Modifiers
category: DotNet
tags: [csharp, dotnet, access-modifiers]
---

This is a short hierarchy summary of the access modifiers in C#.NET, from most restricted to least restricted.

---

## `private`

- Only Accessible within a Class/Struct
- Not inherited by any deriving classes
- Boundaries:
  - **Same Assembly: Declared Class**

## `private protected`

- Since C# 7.2
- Accessible from within a Class/Struct
- Inherited by any deriving classes
- But only within the current assembly (Project/Namespace)
- Boundaries:
  - **Same Assembly: Declared Class**
  - **Same Assembly: Derived Classes**

## `internal`

- (Assembly-Project Priority)
- Accessible from anywhere within the current assembly (Project/Namespace)
- Boundaries:
  - **Same Assembly: Declared Class**
  - **Same Assembly: Derived Classes**
  - **Same Assembly: Other Classes**

## `protected`

- (Class-Inheritance Priority)
- Accessible from within a Class/Struct
- Inherited by any deriving classes
- Boundaries:
  - **Same Assembly: Declared Class**
  - **Same Assembly: Derived Classes**
  - **Other Assemblies: Derived Classes**

## `protected internal`

- (Class-Inheritance + Assembly-Project)
- Accessible from anywhere within the current assembly (Project/Namespace)
- Inherited from any deriving classes
- Boundaries:
  - **Same Assembly: Declared Class/Struct**
  - **Same Assembly: Derived Classes**
  - **Same Assembly: Other Classes**
  - **Other Assemblies: Derived Classes**

## `public`

- Accessible from everywhere
- Access is not restricted at all
- Boundaries:
  - **Same Assembly: Declared Class/Struct**
  - **Same Assembly: Derived Classes**
  - **Same Assembly: Other Classes**
  - **Other Assemblies: Derived Classes**
  - **Other Assemblies: Other Classes**
