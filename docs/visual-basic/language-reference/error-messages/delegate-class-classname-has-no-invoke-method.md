---
title: В делегируемом классе <classname> отсутствует метод Invoke, поэтому выражение этого типа не может быть вызвано посредством метода
ms.date: 07/20/2015
f1_keywords:
- vbc30220
- bc30220
helpviewer_keywords:
- BC30220
ms.assetid: 6be0d61c-f2f9-4f9b-ab90-8871a0d7206d
ms.openlocfilehash: 3fe164d868ee7bde0e687e1d592f4d5a17565aea
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61803640"
---
# <a name="delegate-class-classname-has-no-invoke-method-so-an-expression-of-this-type-cannot-be-the-target-of-a-method-call"></a>Класс делегата\<имя_класса > "не содержит метода Invoke, поэтому выражение этого типа не может быть результатом вызова метода
Вызов `Invoke` через делегат не выполнено, поскольку `Invoke` не реализован в классе делегата.  
  
 **Идентификатор ошибки:** BC30220  
  
## <a name="to-correct-this-error"></a>Исправление ошибки  
  
1. Убедитесь, что создания экземпляра класса делегата с `Dim` инструкции и что процедура была назначена экземпляру делегата с `AddressOf` оператор.  
  
2. Найдите код, который реализует класс делегата и убедитесь, что он реализует `Invoke` процедуры.  
  
## <a name="see-also"></a>См. также

- [Делегаты](../../../visual-basic/programming-guide/language-features/delegates/index.md)
- [Оператор Delegate](../../../visual-basic/language-reference/statements/delegate-statement.md)
- [Оператор AddressOf](../../../visual-basic/language-reference/operators/addressof-operator.md)
- [Оператор Dim](../../../visual-basic/language-reference/statements/dim-statement.md)
