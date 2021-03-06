---
title: AttributeUsage (C#) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 22c45568-9a6a-4c2f-8480-f38c1caa0a99
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6f6c72c8152cc0f76085efbaa99ec63e50d1b676
ms.lasthandoff: 03/13/2017

---
# <a name="attributeusage-c"></a>AttributeUsage (C#)
Determina cómo se puede usar una clase de atributo personalizado. `AttributeUsage` es un atributo que se puede aplicar a definiciones de atributos personalizados para controlar cómo se aplica el nuevo atributo. La configuración predeterminada presenta este aspecto cuando se aplica explícitamente:  
  
```csharp  
[System.AttributeUsage(System.AttributeTargets.All,  
                   AllowMultiple = false,  
                   Inherited = true)]  
class NewAttribute : System.Attribute { }  
```  
  
 En este ejemplo, la clase `NewAttribute` se puede aplicar a cualquier entidad de código atribuible, pero solo se puede aplicar una vez a cada entidad. Las clases derivadas la heredan cuando se aplica a una clase base.  
  
 Los argumentos `AllowMultiple` y `Inherited` son opcionales, por lo que este código tiene el mismo efecto:  
  
```csharp  
[System.AttributeUsage(System.AttributeTargets.All)]  
class NewAttribute : System.Attribute { }  
```  
  
 El primer argumento `AttributeUsage` debe ser uno o varios elementos de la enumeración <xref:System.AttributeTargets>. Se pueden vincular diversos tipos de destino con el operador OR, de esta forma:  
  
```csharp  
using System;  
```  
  
```csharp  
[AttributeUsage(AttributeTargets.Property | AttributeTargets.Field)]  
class NewPropertyOrFieldAttribute : Attribute { }  
```  
  
 Si el argumento `AllowMultiple` se establece en `true`, el atributo resultante se puede aplicar más de una vez a cada una de las entidades, del siguiente modo:  
  
```csharp  
using System;  
```  
  
```csharp  
[AttributeUsage(AttributeTargets.Class, AllowMultiple = true)]  
class MultiUseAttr : Attribute { }  
  
[MultiUseAttr]  
[MultiUseAttr]  
class Class1 { }  
  
[MultiUseAttr, MultiUseAttr]  
class Class2 { }  
```  
  
 En este caso, `MultiUseAttr` se puede aplicar varias veces porque `AllowMultiple` está establecido en `true`. Los dos formatos mostrados para aplicar varios atributos son válidos.  
  
 Si `Inherited` se establece en `false`, las clases que se derivan de una clase con atributos no heredan el atributo. Por ejemplo:  
  
```csharp  
using System;  
```  
  
```csharp  
[AttributeUsage(AttributeTargets.Class, Inherited = false)]  
class Attr1 : Attribute { }  
  
[Attr1]  
class BClass { }  
  
class DClass : BClass { }  
```  
  
 En este caso, `Attr1` no se aplica a `DClass` a través de la herencia.  
  
## <a name="remarks"></a>Comentarios  
 `AttributeUsage` es un atributo de uso único; no se puede aplicar más de una vez a la misma clase. `AttributeUsage` es un alias para <xref:System.AttributeUsageAttribute>.  
  
 Para obtener más información, consulte [Acceder a atributos mediante reflexión (C#)](../../../../csharp/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra el efecto de los argumentos `Inherited` y `AllowMultiple` en el atributo `AttributeUsage` y cómo se pueden enumerar los atributos personalizados aplicados a una clase.  
  
```csharp  
using System;  
```  
  
```csharp  
// Create some custom attributes:  
[AttributeUsage(System.AttributeTargets.Class, Inherited = false)]  
class A1 : System.Attribute { }  
  
[AttributeUsage(System.AttributeTargets.Class)]  
class A2 : System.Attribute { }  
  
[AttributeUsage(System.AttributeTargets.Class, AllowMultiple = true)]  
class A3 : System.Attribute { }  
  
// Apply custom attributes to classes:  
[A1, A2]  
class BaseClass { }  
  
[A3, A3]  
class DerivedClass : BaseClass { }  
  
public class TestAttributeUsage  
{  
    static void Main()  
    {  
        BaseClass b = new BaseClass();  
        DerivedClass d = new DerivedClass();  
  
        // Display custom attributes for each class.  
        Console.WriteLine("Attributes on Base Class:");  
        object[] attrs = b.GetType().GetCustomAttributes(true);  
        foreach (Attribute attr in attrs)  
        {  
            Console.WriteLine(attr);  
        }  
  
        Console.WriteLine("Attributes on Derived Class:");  
        attrs = d.GetType().GetCustomAttributes(true);  
        foreach (Attribute attr in attrs)  
        {  
            Console.WriteLine(attr);  
        }  
    }  
}  
```  
  
## <a name="sample-output"></a>Resultados del ejemplo  
  
```  
Attributes on Base Class:  
A1  
A2  
Attributes on Derived Class:  
A3  
A3  
A2  
```  
  
## <a name="see-also"></a>Vea también  
 <xref:System.Attribute>   
 <xref:System.Reflection>   
 [Guía de programación de C#](../../../../csharp/programming-guide/index.md)   
 [Attributes](https://msdn.microsoft.com/library/5x6cd29c)  (Atributos)  
 [Reflection (C#)](../../../../csharp/programming-guide/concepts/reflection.md)  (Reflexión [C#])  
 [Attributes](../../../../csharp/programming-guide/concepts/attributes/index.md)  (Atributos)  
 [Crear atributos personalizados (C#)](../../../../csharp/programming-guide/concepts/attributes/creating-custom-attributes.md)   
 [Acceder a atributos mediante reflexión (C#)](../../../../csharp/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)
