---
title: 如何：裁剪图像
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- images [WPF], cropping
- cropping images [WPF]
ms.assetid: c6bba109-c6e7-4cf8-bfe6-9cf8d01bb4fc
ms.openlocfilehash: 189cb92d581ccc9209ebdb4de18487951d17818a
ms.sourcegitcommit: 15d99019aea4a5c3c91ddc9ba23692284a7f61f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2018
ms.locfileid: "49308274"
---
# <a name="how-to-crop-an-image"></a>如何：裁剪图像
此示例演示如何裁剪图像使用<xref:System.Windows.Media.Imaging.CroppedBitmap>。  
  
 <xref:System.Windows.Media.Imaging.CroppedBitmap> 主要用于裁剪后的映像版本进行编码时将查看保存到文件。 若要裁剪图像用于显示目的，请参阅[创建剪辑区域](https://msdn.microsoft.com/library/56e4bed6-78d7-4292-b917-d72d0b3e4376)主题。  
  
## <a name="example"></a>示例  
 以下[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]定义下面的示例中使用的资源。  
  
 [!code-xaml[imageelementexample#CroppedXAML1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml#croppedxaml1)]  
  
 下面的示例创建映像使用<xref:System.Windows.Media.Imaging.CroppedBitmap>作为其源。  
  
 [!code-xaml[imageelementexample#CroppedXAML2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml#croppedxaml2)]  
  
 [!code-csharp[imageelementexample#CroppedCSharp1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml.cs#croppedcsharp1)]
 [!code-vb[imageelementexample#CroppedCSharp1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample/VB/CroppedImageExample.xaml.vb#croppedcsharp1)]  
  
 <xref:System.Windows.Media.Imaging.CroppedBitmap>还可以用作另一个源<xref:System.Windows.Media.Imaging.CroppedBitmap>，链接裁剪。 请注意，<xref:System.Windows.Media.Imaging.CroppedBitmap.SourceRect%2A>使用相对于裁剪位图并不是初始的图像的源的值。  
  
 [!code-xaml[imageelementexample#CroppedXAML3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml#croppedxaml3)]  
  
 [!code-csharp[imageelementexample#CroppedCSharp2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/CroppedImageExample.xaml.cs#croppedcsharp2)]
 [!code-vb[imageelementexample#CroppedCSharp2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample/VB/CroppedImageExample.xaml.vb#croppedcsharp2)]  
  
## <a name="see-also"></a>请参阅  
 [创建剪辑区域](https://msdn.microsoft.com/library/56e4bed6-78d7-4292-b917-d72d0b3e4376)
