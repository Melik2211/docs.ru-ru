---
title: Добавление столбцов в элемент управления ListView
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ListView control [Windows Forms], adding column headers
- columns [Windows Forms], adding to ListView controls
- list views [Windows Forms], adding columns
ms.assetid: 79174274-12ee-4a5d-80db-6ec02976d010
ms.openlocfilehash: dd438ffbadddfc37ec9eb15e59a908bb58472a45
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2020
ms.locfileid: "76744587"
---
# <a name="how-to-add-columns-to-the-windows-forms-listview-control"></a>Практическое руководство. Добавление столбцов в элемент управления ListView в Windows Forms
В представлении Details элемент управления <xref:System.Windows.Forms.ListView> может отображать несколько столбцов для каждого элемента списка. Столбцы можно использовать для вывода нескольких типов сведений о каждом элементе списка. Например, список файлов может отображать имя файла, тип файла, размер и дату последнего изменения файла. Сведения о заполнении столбцов после их создания см. в разделе [инструкции. Отображение подэлементов в столбцах с помощью элемента управления ListView Windows Forms](how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md).  
  
### <a name="to-add-columns-programmatically"></a>Добавление столбцов программным способом  
  
1. Задайте для свойства <xref:System.Windows.Forms.ListView.View%2A> элемента управления значение <xref:System.Windows.Forms.View.Details>.  
  
2. Используйте метод <xref:System.Windows.Forms.ListView.ColumnHeaderCollection.Add%2A> свойства <xref:System.Windows.Forms.ListView.Columns%2A> представления списка.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#31)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#31)]  
  
## <a name="see-also"></a>См. также раздел

- <xref:System.Windows.Forms.ListView>
- [Элемент управления ListView](listview-control-windows-forms.md)
- [Общие сведения об элементе управления ListView](listview-control-overview-windows-forms.md)
