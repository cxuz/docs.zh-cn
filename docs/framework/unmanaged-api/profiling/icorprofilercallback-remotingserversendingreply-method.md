---
title: "ICorProfilerCallback::RemotingServerSendingReply 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerCallback.RemotingServerSendingReply
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerCallback::RemotingServerSendingReply
helpviewer_keywords:
- RemotingServerSendingReply method [.NET Framework profiling]
- ICorProfilerCallback::RemotingServerSendingReply method [.NET Framework profiling]
ms.assetid: dfe84a19-2e03-4be2-8b25-f02bad38e4a9
topic_type: apiref
caps.latest.revision: "12"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: b99b2de235634b715a6f5ba9fee9ee49ab34063a
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2017
---
# <a name="icorprofilercallbackremotingserversendingreply-method"></a><span data-ttu-id="2f30f-102">ICorProfilerCallback::RemotingServerSendingReply 方法</span><span class="sxs-lookup"><span data-stu-id="2f30f-102">ICorProfilerCallback::RemotingServerSendingReply Method</span></span>
<span data-ttu-id="2f30f-103">通知探查器，该过程已完成处理远程方法调用请求，即将传输通过通道答复。</span><span class="sxs-lookup"><span data-stu-id="2f30f-103">Notifies the profiler that the process has finished processing a remote method invocation request and is about to transmit the reply through a channel.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2f30f-104">语法</span><span class="sxs-lookup"><span data-stu-id="2f30f-104">Syntax</span></span>  
  
```  
HRESULT RemotingServerSendingReply(  
    [in] GUID *pCookie,  
    [in] BOOL fIsAsync);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="2f30f-105">参数</span><span class="sxs-lookup"><span data-stu-id="2f30f-105">Parameters</span></span>  
 `pCookie`  
 <span data-ttu-id="2f30f-106">[in]指向将与中提供的值相对应的 GUID 的指针[icorprofilercallback:: Remotingclientreceivingreply](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-remotingclientreceivingreply-method.md)在这些情况下：</span><span class="sxs-lookup"><span data-stu-id="2f30f-106">[in] A pointer to a GUID that will correspond with the value provided in [ICorProfilerCallback::RemotingClientReceivingReply](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-remotingclientreceivingreply-method.md) under these conditions:</span></span>  
  
-   <span data-ttu-id="2f30f-107">远程处理 GUID cookie 处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="2f30f-107">Remoting GUID cookies are active.</span></span>  
  
-   <span data-ttu-id="2f30f-108">通道成功传输消息。</span><span class="sxs-lookup"><span data-stu-id="2f30f-108">The channel succeeds in transmitting the message.</span></span>  
  
-   <span data-ttu-id="2f30f-109">GUID cookie 上处于活动状态的客户端过程。</span><span class="sxs-lookup"><span data-stu-id="2f30f-109">GUID cookies are active on the client-side process.</span></span>  
  
 <span data-ttu-id="2f30f-110">这样的远程处理调用和逻辑调用堆栈的创建轻松配对。</span><span class="sxs-lookup"><span data-stu-id="2f30f-110">This allows easy pairing of remoting calls and the creation of a logical call stack.</span></span>  
  
 `fIsAsync`  
 <span data-ttu-id="2f30f-111">[in]一个值，是`true`如果调用的是异步的; 否则为`false`。</span><span class="sxs-lookup"><span data-stu-id="2f30f-111">[in] A value that is `true` if the call is asynchronous; otherwise, `false`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2f30f-112">要求</span><span class="sxs-lookup"><span data-stu-id="2f30f-112">Requirements</span></span>  
 <span data-ttu-id="2f30f-113">**平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="2f30f-113">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2f30f-114">**头文件：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="2f30f-114">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="2f30f-115">**库：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="2f30f-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="2f30f-116">**.NET framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="2f30f-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2f30f-117">另请参阅</span><span class="sxs-lookup"><span data-stu-id="2f30f-117">See Also</span></span>  
 [<span data-ttu-id="2f30f-118">ICorProfilerCallback 接口</span><span class="sxs-lookup"><span data-stu-id="2f30f-118">ICorProfilerCallback Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)