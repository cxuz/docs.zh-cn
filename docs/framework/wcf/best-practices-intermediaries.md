---
title: 最佳做法：中介
ms.date: 03/30/2017
ms.assetid: 2d41b337-8132-4ac2-bea2-6e9ae2f00f8d
ms.openlocfilehash: d69baae9b4f5851f60d8d1336c40e0d18db8e77d
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33458414"
---
# <a name="best-practices-intermediaries"></a>最佳做法：中介
当调用中介时务必谨慎，以便正确地处理故障，从而确保中介上的服务端通道正确关闭。  
  
 请考虑以下方案。 客户端调用中介，然后中介调用后端服务。  后端服务没有定义故障协定，因此，从该服务引发的任何故障都将被视为非类型化的故障。  后端服务引发<xref:System.ApplicationException>和 WCF 正确地中止服务端通道。 然后，<xref:System.ApplicationException> 显示为一个要向中介引发的 <xref:System.ServiceModel.FaultException>。 中介重新引发 <xref:System.ApplicationException>。 WCF 将此解释为来自中介的非类型化故障，并将其转发到客户端。 收到故障后，中介和客户端会同时使其客户端通道出现故障。 但中介的客户端通道保持打开，因为 WCF 不知道故障是严重故障。  
  
 这种方案的最佳实践是检测来自服务的故障是否为严重故障，如果是，中介将使其服务端通道出现故障，如下面的代码段所示。  
  
```csharp  
catch (Exception e)  
{  
    bool faulted = service.State == CommunicationState.Faulted;  
    service.Abort();  
    if (faulted)  
    {  
        throw new ApplicationException(e.Message);  
    }  
    Else  
    {  
        throw;  
    }  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [WCF 错误处理](../../../docs/framework/wcf/wcf-error-handling.md)  
 [在协定和服务中指定并处理错误](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)
