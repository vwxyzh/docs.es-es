---
title: extern (Referencia de C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- extern_CSharpKeyword
- extern
dev_langs:
- CSharp
helpviewer_keywords:
- DllImport attribute
- extern keyword [C#]
ms.assetid: 9c3f02c4-51b8-4d80-9cb2-f2b6e1ae15c7
caps.latest.revision: 26
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 61cde8c8f6b3d255be5f6040141542e3e8d1e8c7
ms.lasthandoff: 03/13/2017

---
# <a name="extern-c-reference"></a>extern (Referencia de C#)
El modificador `extern` se usa para declarar un método que se implementa externamente. Un uso común del modificador `extern` es con el atributo `DllImport` al usar servicios de interoperabilidad para llamar a código no administrado. En este caso, el método se debe declarar también como `static`, como se muestra en el ejemplo siguiente:  
  
```  
[DllImport("avifil32.dll")]  
private static extern void AVIFileInit();  
```  
  
 La palabra clave `extern` también puede definir un alias del ensamblado externo, lo que permite hacer referencia a diferentes versiones del mismo componente desde un único ensamblado. Para obtener más información, vea [alias externo](../../../csharp/language-reference/keywords/extern-alias.md).  
  
 Es un error usar los modificadores [abstract](../../../csharp/language-reference/keywords/abstract.md) y `extern` juntos para modificar el mismo miembro. El uso del modificador `extern` significa que el método se implementa fuera del código de C#, mientras que el uso del modificador `abstract` significa que la implementación del método no se proporciona en la clase.  
  
 La palabra clave extern tiene usos más limitados en C# que en C++. Para comparar la palabra clave de C# con la de C++, consulte el tema sobre el uso de extern para especificar vinculación en la referencia del lenguaje C++.  
  
## <a name="example"></a>Ejemplo  
 **Ejemplo 1.** En este ejemplo, el programa recibe una cadena del usuario y la muestra en un cuadro de mensaje. El programa usa el método `MessageBox` importado de la biblioteca User32.dll.  
  
 [!code-cs[csrefKeywordsModifiers#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/extern_1.cs)]  
  
## <a name="example"></a>Ejemplo  
 **Ejemplo 2.** En este ejemplo se muestra un programa de C# que llama a una biblioteca de C (una DLL nativa).  
  
 1. Cree el archivo de C siguiente y denomínelo `cmdll.c`:  
  
```  
// cmdll.c  
// Compile with: /LD  
int __declspec(dllexport) SampleMethod(int i)  
{  
   return i*10;  
}  
```  
  
## <a name="example"></a>Ejemplo  
 2. Abra una ventana del símbolo del sistema de las herramientas nativas de Visual Studio x64 (o x32) del directorio de instalación de Visual Studio y compile el archivo `cmdll.c` escribiendo **cl /LD cmdll.c** en el símbolo del sistema.  
  
 3. En el mismo directorio, cree el siguiente archivo de C# y denomínelo `cm.cs`:  
  
```  
// cm.cs  
using System;  
using System.Runtime.InteropServices;  
public class MainClass   
{  
   [DllImport("Cmdll.dll")]  
   public static extern int SampleMethod(int x);  
  
   static void Main()   
   {  
      Console.WriteLine("SampleMethod() returns {0}.", SampleMethod(5));  
   }  
}  
```  
  
## <a name="example"></a>Ejemplo  
 3. Abra una ventana del símbolo del sistema de las herramientas nativas de Visual Studio x64 (o x32) del directorio de instalación de Visual Studio y compile el archivo `cm.cs` escribiendo:  
  
> **csc cm.cs** (para el símbolo del sistema x64)   
>  -O bien-  
> **csc /platform:x86 cm.cs** (para el símbolo del sistema x32)  
  
 De esta forma, se creará el archivo ejecutable `cm.exe`.  
  
 4. Ejecute `cm.exe`. El método `SampleMethod` pasa el valor 5 al archivo DLL, que devuelve el valor multiplicado por 10.  El programa produce el siguiente resultado:  
  
```  
SampleMethod() returns 50.  
```  
  
## <a name="c-language-specification"></a>Especificación del lenguaje C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vea también  
 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>   
 [Referencia de C#](../../../csharp/language-reference/index.md)   
 [Guía de programación de C#](../../../csharp/programming-guide/index.md)   
 [Palabras clave de C#](../../../csharp/language-reference/keywords/index.md)   
 [Modificadores](../../../csharp/language-reference/keywords/modifiers.md)
