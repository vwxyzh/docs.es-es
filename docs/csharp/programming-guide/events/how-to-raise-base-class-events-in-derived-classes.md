---
title: "Cómo: Producir eventos de una clase base en clases derivadas (Guía de programación de C#) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- events [C#], in derived classes
ms.assetid: 2d20556a-0aad-46fc-845e-f85d86ea617a
caps.latest.revision: 24
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
ms.openlocfilehash: 4f3990959bb62676562dc21e1e5eabfb8ead20d5
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-raise-base-class-events-in-derived-classes-c-programming-guide"></a>Cómo: Producir eventos de una clase base en clases derivadas (Guía de programación de C#)
En el siguiente ejemplo sencillo se muestra la forma estándar de declarar eventos en una clase base para que también se puedan generar desde clases derivadas. Este patrón se usa mucho en las clases de Windows Forms de la biblioteca de clases de [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)].  
  
 Al crear una clase que se pueda usar como clase base para otras clases, debe considerar el hecho de que los eventos son un tipo especial de delegado que solo se pueden invocar desde la clase que los haya declarado. Las clases derivadas no pueden invocar directamente a eventos declarados en la clase base. Aunque a veces pueda querer un evento que solo la clase base pueda generar, en la mayoría de los casos debería habilitar la clase derivada para invocar a eventos de clase base. Para ello, puede crear un método de invocación protegido en la clase base que encapsula el evento. Al llamar o invalidar a este método de invocación, las clases derivadas pueden invocar directamente al evento.  
  
> [!NOTE]
>  No declare eventos virtuales en una clase base y los invalide en una clase derivada. El compilador de C# no los controla correctamente y no es posible decir si un suscriptor del evento derivado se está suscribiendo realmente al evento de clase base.  
  
## <a name="example"></a>Ejemplo  
 [!code-cs[csProgGuideEvents#1](../../../csharp/programming-guide/events/codesnippet/CSharp/how-to-raise-base-class-events-in-derived-classes_1.cs)]  
  
## <a name="see-also"></a>Vea también  
 [Guía de programación de C#](../../../csharp/programming-guide/index.md)   
 [Eventos](../../../csharp/programming-guide/events/index.md)   
 [Delegados](../../../csharp/programming-guide/delegates/index.md)   
 [Modificadores de acceso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [Creating Event Handlers in Windows Forms](https://msdn.microsoft.com/library/dacysss4.aspx)
