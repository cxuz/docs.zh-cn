---
title: 与 ASP.NET Web 服务的互操作性
ms.date: 03/30/2017
ms.assetid: 622422f8-6651-442f-b8be-e654a4aabcac
ms.openlocfilehash: 8a0737a36989dd8bc6f5d5670555c7b2218798bb
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33494291"
---
# <a name="interoperability-with-aspnet-web-services"></a>与 ASP.NET Web 服务的互操作性
之间的互操作性[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]Web 服务和 Windows Communication Foundation (WCF) Web 服务可以通过确保使用这两种技术实现的服务符合 WS-基本配置文件 1.1 规范。 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Web 服务符合 WS-Basic Profile 1.1 进行互操作与 WCF 客户端通过使用 WCF 系统提供的绑定， <xref:System.ServiceModel.BasicHttpBinding>。  
  
 使用 [!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)] 选项，即将 <xref:System.Web.Services.WebService> 和 <xref:System.Web.Services.WebMethodAttribute> 属性添加到接口而不是添加到类，并编写实现该接口的类，如下面的示例代码所示。  
  
```  
[WebService]  
public interface IEcho  
{  
    [WebMethod]  
    string Echo(string input);  
}  
  
public class Service : IEcho  
{  
  
   public string Echo(string input)  
   {  
        return input;  
    }  
}  
```  
  
 使用此选项是首选方法，因为具有 <xref:System.Web.Services.WebService> 属性的接口为服务所执行的操作构成了一个协定，在以不同方式实现该协定的各个类中，都可重用该协定。  
  
 避免使用 <xref:System.Web.Services.Protocols.SoapDocumentServiceAttribute> 特性依据 SOAP 消息正文元素的完全限定名称将消息路由到方法，而应使用 `SOAPAction` 标头。 WCF 使用`SOAPAction`HTTP 标头来路由消息。  
  
 只要为 XML 显式定义了命名空间，则在默认情况下，<xref:System.Xml.Serialization.XmlSerializer> 将类型序列化为的 XML 与 <xref:System.Runtime.Serialization.DataContractSerializer> 将类型序列化为的 XML 在语义上完全相同。 定义与一起使用的数据类型时[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]Web 并且预期采用 WCF 的服务，请执行以下操作：  
  
-   使用 .NET Framework 类而不是 XML 架构来定义该类型。  
  
-   仅将 <xref:System.SerializableAttribute> 和 <xref:System.Xml.Serialization.XmlRootAttribute> 添加到该类，使用后者显式定义类型的命名空间。 不要添加 <xref:System.Xml.Serialization> 命名空间中的其他属性来控制如何将 .NET Framework 类转换为 XML。  
  
-   通过采用此方法，以后可将 .NET 类转换为附加了 <xref:System.Runtime.Serialization.DataContractAttribute> 和 <xref:System.Runtime.Serialization.DataMemberAttribute> 的数据协定，而无需为了传输而对类序列化成的 XML 进行重大更改。 通过消息中使用的类型[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]Web 服务可以作为数据协定由 WCF 应用程序，以生成其他优点，更好的性能 WCF 应用程序中处理。  
  
 避免使用 Internet Information Services (IIS) 提供的身份验证选项。 WCF 客户端不支持这些选项。 如果必须保护服务，使用 WCF 提供的因为这些选项是可靠的基于标准协议的选项。  
  
## <a name="performance-impact-caused-by-loading-the-servicemodel-httpmodule"></a>由加载 ServiceModel HttpModule 而导致的性能影响  
 在 .NET Framework 3.0 中，WCF `HttpModule` 安装在根 Web.config 文件中，因此，每个 ASP.NET 应用程序都启用了 WCF。 这可能会影响性能，因此，可以移除 Web.config 文件的 `ServiceModel`，如下面的示例所示。  
  
```xml  
<httpModules>  
    <remove name="ServiceModel" />  
<httpModules/>  
```  
  
## <a name="see-also"></a>请参阅  
 [如何：配置 WCF 服务以便与 ASP.NET Web 服务客户端进行互操作](../../../../docs/framework/wcf/feature-details/config-wcf-service-with-aspnet-web-service.md)
