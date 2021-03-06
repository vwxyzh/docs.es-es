---
title: "Cómo: Publicar eventos que cumplan las directrices de .NET Framework (Guía de programación de C#)| Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- events [C#], implementation guidelines
ms.assetid: 9310ae16-8627-44a2-b08c-05e5976202b1
caps.latest.revision: 31
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
ms.openlocfilehash: 78d069249c8131a091a206703c475faaf641d17b
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-publish-events-that-conform-to-net-framework-guidelines-c-programming-guide"></a>Cómo: Publicar eventos que cumplan las directrices de .NET Framework (Guía de programación de C#)
En el siguiente procedimiento se muestra cómo agregar eventos que cumplan el patrón [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] estándar a las clases y structs. Todos los eventos de la biblioteca de clases [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] se basan en el delegado <xref:System.EventHandler>, que se define de la siguiente manera:  
  
```  
public delegate void EventHandler(object sender, EventArgs e);  
```  
  
> [!NOTE]
>  [!INCLUDE[dnprdnlong](../../../csharp/programming-guide/events/includes/dnprdnlong_md.md)] incluye una versión genérica de este delegado, <xref:System.EventHandler%601>. En los siguientes ejemplos se muestra cómo usar las dos versiones.  
  
 Aunque los eventos de las clases que defina se pueden basar en cualquier tipo de delegado válido, incluidos los delegados que devuelven un valor, por lo general se recomienda que base los eventos en el patrón [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] mediante <xref:System.EventHandler>, como se muestra en el ejemplo siguiente.  
  
### <a name="to-publish-events-based-on-the-eventhandler-pattern"></a>Para publicar eventos basados en el patrón EventHandler  
  
1.  (Omita este paso y vaya al paso 3a si no tiene que enviar datos personalizados con el evento). Declare la clase de los datos personalizados en un ámbito que sea visible para las clases de publicador y suscriptor. Luego, agregue los miembros necesarios para almacenar los datos de eventos personalizados. En este ejemplo se devuelve una cadena simple.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
2.  (Omita este paso si usa la versión genérica de <xref:System.EventHandler%601>). Declare un delegado en la clase de publicación. Asígnele un nombre que acabe por *EventHandler*. El segundo parámetro especifica el tipo EventArgs personalizado.  
  
    ```  
    public delegate void CustomEventHandler(object sender, CustomEventArgs a);  
    ```  
  
3.  Declare el evento en la clase de publicación llevando a cabo uno de los siguientes pasos.  
  
    1.  Si no tiene ninguna clase EventArgs personalizada, el tipo Event será el delegado EventHandler no genérico. No es necesario declarar el delegado, porque ya está declarado en el espacio de nombres <xref:System> que se incluye al crear el proyecto de C#. Agregue el código siguiente a la clase de publicador.  
  
        ```  
        public event EventHandler RaiseCustomEvent;  
        ```  
  
    2.  Si usa la versión no genérica de <xref:System.EventHandler> y tiene una clase personalizada derivada de <xref:System.EventArgs>, declare el evento dentro de la clase de publicación y use el delegado del paso 2 como tipo.  
  
        ```  
        public event CustomEventHandler RaiseCustomEvent;  
  
        ```  
  
    3.  Si usa la versión genérica, no necesita ningún delegado personalizado. En su lugar, en la clase de publicación, especifique el tipo de evento como `EventHandler<CustomEventArgs>`, sustituyendo el nombre de su propia clase que aparece entre corchetes angulares.  
  
        ```  
        public event EventHandler<CustomEventArgs> RaiseCustomEvent;  
        ```  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestran los pasos anteriores mediante el uso de una clase EventArgs personalizada y <xref:System.EventHandler%601> como tipo de evento.  
  
 [!code-cs[csProgGuideEvents#2](../../../csharp/programming-guide/events/codesnippet/CSharp/how-to-publish-events-that-conform-to-net-framework-guidelines_1.cs)]  
  
## <a name="see-also"></a>Vea también  
 <xref:System.Delegate>   
 [Guía de programación de C#](../../../csharp/programming-guide/index.md)   
 [Eventos](../../../csharp/programming-guide/events/index.md)   
 [Delegados](../../../csharp/programming-guide/delegates/index.md)
