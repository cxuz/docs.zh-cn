---
title: "IHostThreadPoolManager 接口"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostThreadPoolManager
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostThreadPoolManager
helpviewer_keywords: IHostThreadPoolManager interface [.NET Framework hosting]
ms.assetid: c3a2cd90-7c4e-4374-bb87-b41befb8344f
topic_type: apiref
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 2773042c695320ab1e90d4c5d341e2df5f0f778f
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="ihostthreadpoolmanager-interface"></a><span data-ttu-id="265e3-102">IHostThreadPoolManager 接口</span><span class="sxs-lookup"><span data-stu-id="265e3-102">IHostThreadPoolManager Interface</span></span>
<span data-ttu-id="265e3-103">提供启用公共语言运行时 (CLR) 若要配置线程池以及排队到线程池工作项的方法。</span><span class="sxs-lookup"><span data-stu-id="265e3-103">Provides methods that enable the common language runtime (CLR) to configure the thread pool and to queue work items to the thread pool.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="265e3-104">方法</span><span class="sxs-lookup"><span data-stu-id="265e3-104">Methods</span></span>  
  
|<span data-ttu-id="265e3-105">方法</span><span class="sxs-lookup"><span data-stu-id="265e3-105">Method</span></span>|<span data-ttu-id="265e3-106">描述</span><span class="sxs-lookup"><span data-stu-id="265e3-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="265e3-107">GetAvailableThreads 方法</span><span class="sxs-lookup"><span data-stu-id="265e3-107">GetAvailableThreads Method</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-getavailablethreads-method.md)|<span data-ttu-id="265e3-108">获取在当前不在处理工作项的线程池中的线程数。</span><span class="sxs-lookup"><span data-stu-id="265e3-108">Gets the number of threads in the thread pool that are not currently processing work items.</span></span>|  
|[<span data-ttu-id="265e3-109">GetMaxThreads 方法</span><span class="sxs-lookup"><span data-stu-id="265e3-109">GetMaxThreads Method</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-getmaxthreads-method.md)|<span data-ttu-id="265e3-110">在线程池中同时获取最大主机维护的线程数。</span><span class="sxs-lookup"><span data-stu-id="265e3-110">Gets the maximum number of threads that the host maintains concurrently in the thread pool.</span></span>|  
|[<span data-ttu-id="265e3-111">GetMinThreads 方法</span><span class="sxs-lookup"><span data-stu-id="265e3-111">GetMinThreads Method</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-getminthreads-method.md)|<span data-ttu-id="265e3-112">预期的请求中获取的最小主机维护的空闲线程数。</span><span class="sxs-lookup"><span data-stu-id="265e3-112">Gets the minimum number of idle threads that the host maintains in anticipation of requests.</span></span>|  
|[<span data-ttu-id="265e3-113">QueueUserWorkItem 方法</span><span class="sxs-lookup"><span data-stu-id="265e3-113">QueueUserWorkItem Method</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-queueuserworkitem-method.md)|<span data-ttu-id="265e3-114">排队的执行，函数，并提供一个包含由该函数使用的数据的对象。</span><span class="sxs-lookup"><span data-stu-id="265e3-114">Queues a function for execution, and provides an object containing data to be used by the function.</span></span>|  
|[<span data-ttu-id="265e3-115">SetMaxThreads 方法</span><span class="sxs-lookup"><span data-stu-id="265e3-115">SetMaxThreads Method</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-setmaxthreads-method.md)|<span data-ttu-id="265e3-116">设置最大主机可以维护在线程池中的线程数。</span><span class="sxs-lookup"><span data-stu-id="265e3-116">Sets the maximum number of threads that the host can maintain in the thread pool.</span></span>|  
|[<span data-ttu-id="265e3-117">SetMinThreads 方法</span><span class="sxs-lookup"><span data-stu-id="265e3-117">SetMinThreads Method</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-setminthreads-method.md)|<span data-ttu-id="265e3-118">预期的请求中设置的最小主机必须维护的空闲线程数。</span><span class="sxs-lookup"><span data-stu-id="265e3-118">Sets the minimum number of idle threads that the host must maintain in anticipation of requests.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="265e3-119">备注</span><span class="sxs-lookup"><span data-stu-id="265e3-119">Remarks</span></span>  
 <span data-ttu-id="265e3-120">主机不需要使用对的调用中指定的值配置线程池`SetMaxThreads`和`SetMinThreads`方法。</span><span class="sxs-lookup"><span data-stu-id="265e3-120">The host is not required to configure the thread pool by using the values specified in calls to the `SetMaxThreads` and `SetMinThreads` methods.</span></span> <span data-ttu-id="265e3-121">在这种情况下，主机应从这些方法返回 E_NOTIMPL 的 HRESULT 值。</span><span class="sxs-lookup"><span data-stu-id="265e3-121">In this case, the host should return an HRESULT value of E_NOTIMPL from these methods.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="265e3-122">要求</span><span class="sxs-lookup"><span data-stu-id="265e3-122">Requirements</span></span>  
 <span data-ttu-id="265e3-123">**平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="265e3-123">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="265e3-124">**标头：** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="265e3-124">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="265e3-125">**库：**作为 MSCorEE.dll 中的资源</span><span class="sxs-lookup"><span data-stu-id="265e3-125">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="265e3-126">**.NET framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="265e3-126">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="265e3-127">另请参阅</span><span class="sxs-lookup"><span data-stu-id="265e3-127">See Also</span></span>  
 <xref:System.Threading>  
 <xref:System.Threading.ThreadPool>  
 [<span data-ttu-id="265e3-128">承载接口</span><span class="sxs-lookup"><span data-stu-id="265e3-128">Hosting Interfaces</span></span>](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)