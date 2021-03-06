---
title: 如何：使用设计器将快捷菜单附加到 TreeNode
ms.date: 03/30/2017
helpviewer_keywords:
- shortcut menus [Windows Forms], attaching to TreeNodes
- TreeNode [Windows Forms], attaching a shortcut menu using Designer
ms.assetid: 8e45e184-1313-4f8f-90ff-2cd5789b2268
ms.openlocfilehash: 77c4b01100aec2df16d5eb844f73f7a2bfa115aa
ms.sourcegitcommit: a885cc8c3e444ca6471348893d5373c6e9e49a47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43864732"
---
# <a name="how-to-attach-a-shortcut-menu-to-a-treenode-using-the-designer"></a>如何：使用设计器将快捷菜单附加到 TreeNode
Windows 窗体<xref:System.Windows.Forms.TreeView>控件显示的节点，类似于文件和 Windows 操作系统中的 Windows 资源管理器功能的左窗格中显示的文件夹层次结构。 通过设置<xref:System.Windows.Forms.Control.ContextMenuStrip%2A>属性，您可以区分上下文的操作向用户提供他们右键单击时<xref:System.Windows.Forms.TreeView>控件。 通过将相关联<xref:System.Windows.Forms.ContextMenuStrip>组件与单个<xref:System.Windows.Forms.TreeNode>项，可以添加到快捷菜单上功能的自定义的级别应用<xref:System.Windows.Forms.TreeView>控件。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-associate-a-shortcut-menu-with-a-treenode-at-design-time"></a>要在设计时与树节点关联的快捷菜单  
  
1.  添加<xref:System.Windows.Forms.TreeView>控制对窗体中，以及如何将节点<xref:System.Windows.Forms.TreeView>根据需要。 有关详细信息，请参阅[如何： 添加和删除节点使用 Windows 窗体 TreeView 控件](../../../../docs/framework/winforms/controls/how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md)。  
  
2.  添加<xref:System.Windows.Forms.ContextMenuStrip>组件向窗体，然后将菜单项添加到表示你想要在运行时提供节点级别操作的快捷菜单。 有关详细信息，请参阅[如何： 向 ContextMenuStrip 添加菜单项](../../../../docs/framework/winforms/controls/how-to-add-menu-items-to-a-contextmenustrip.md)。  
  
3.  重新打开**TreeNodeEditor**对话框<xref:System.Windows.Forms.TreeView>控件中，选择节点以编辑，并设置其<xref:System.Windows.Forms.ContextMenuStrip>属性设置为您添加的快捷菜单。  
  
4.  当设置此属性时，右键单击节点时，将显示的快捷菜单。  
  
     此外，你将想要编写代码来处理<xref:System.Windows.Forms.ToolStripItem.Click>这些菜单项的事件。  
  
## <a name="see-also"></a>请参阅  
 [TreeView 控件](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)  
 [TreeView 控件概述](../../../../docs/framework/winforms/controls/treeview-control-overview-windows-forms.md)  
 [ContextMenuStrip 控件](../../../../docs/framework/winforms/controls/contextmenustrip-control.md)
