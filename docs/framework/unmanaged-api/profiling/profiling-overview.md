---
title: "分析概述"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- managed code, profiling API support
- unmanaged code, combining with managed code in profiling
- notification threads [.NET Framework profiling]
- unmanaged code, profiling
- profiling API [.NET Framework], and COM
- profiling API [.NET Framework], unmanaged code profiling
- profilers, writing
- profiling API [.NET Framework], call stacks
- code profilers, writing
- profiling API [.NET Framework], security considerations
- profiling API [.NET Framework], managed code support
- common language runtime, profiling
- profiling API [.NET Framework], notification threads
- call stacks [.NET Framework profiling]
- profiling API [.NET Framework], stack depth
- common language runtime, writing a profiler
- profiling API [.NET Framework], information retrieval interfaces
- shadow stacks [.NET Framework profiling]
- COM, using in the profiling API
- stack snapshots [.NET Framework profiling]
- profiling API [.NET Framework], supported features
- profiling API [.NET Framework], overview
- security, profiling API considerations
- stack depth [.NET Framework profiling]
ms.assetid: 864c2344-71dc-46f9-96b2-ed59fb6427a8
caps.latest.revision: "27"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 6d7918a369b5a5656fa2e059bdaaf6c211bd022c
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2017
---
# <a name="profiling-overview"></a><span data-ttu-id="77c2f-102">分析概述</span><span class="sxs-lookup"><span data-stu-id="77c2f-102">Profiling Overview</span></span>
<span data-ttu-id="77c2f-103"><a name="top"></a>探查器是一种工具，监视另一个应用程序的执行。</span><span class="sxs-lookup"><span data-stu-id="77c2f-103"><a name="top"></a> A profiler is a tool that monitors the execution of another application.</span></span> <span data-ttu-id="77c2f-104">公共语言运行时 (CLR) 探查器是一个动态链接库 (DLL)，具有使用分析 API 从 CLR 中接收消息以及向 CLR 发送消息的功能。</span><span class="sxs-lookup"><span data-stu-id="77c2f-104">A common language runtime (CLR) profiler is a dynamic link library (DLL) that consists of functions that receive messages from, and send messages to, the CLR by using the profiling API.</span></span> <span data-ttu-id="77c2f-105">CLR 在运行时加载探查器 DLL。</span><span class="sxs-lookup"><span data-stu-id="77c2f-105">The profiler DLL is loaded by the CLR at run time.</span></span>  
  
 <span data-ttu-id="77c2f-106">传统的分析工具专注于测量应用程序的执行情况。</span><span class="sxs-lookup"><span data-stu-id="77c2f-106">Traditional profiling tools focus on measuring the execution of the application.</span></span> <span data-ttu-id="77c2f-107">即测量随着时间的推移应用程序使用每个功能或内存所花费的时间。</span><span class="sxs-lookup"><span data-stu-id="77c2f-107">That is, they measure the time that is spent in each function or the memory usage of the application over time.</span></span> <span data-ttu-id="77c2f-108">而分析 API 则针对更广泛的诊断工具，如代码覆盖率实用程序，甚至高级的调试辅助工具。</span><span class="sxs-lookup"><span data-stu-id="77c2f-108">The profiling API targets a broader class of diagnostic tools such as code-coverage utilities and even advanced debugging aids.</span></span> <span data-ttu-id="77c2f-109">实际上，它们全都用于诊断用途。</span><span class="sxs-lookup"><span data-stu-id="77c2f-109">These uses are all diagnostic in nature.</span></span> <span data-ttu-id="77c2f-110">分析 API 不仅测量而且还监视应用程序的执行情况。</span><span class="sxs-lookup"><span data-stu-id="77c2f-110">The profiling API not only measures but also monitors the execution of an application.</span></span> <span data-ttu-id="77c2f-111">基于此原因，应用程序本身始终不应使用分析 API 并且应用程序的执行情况不应依赖于探查器或受探查器影响。</span><span class="sxs-lookup"><span data-stu-id="77c2f-111">For this reason, the profiling API should never be used by the application itself, and the application’s execution should not depend on (or be affected by) the profiler.</span></span>  
  
 <span data-ttu-id="77c2f-112">与分析常规编译的机器代码相比，分析 CLR 应用程序需要更多支持。</span><span class="sxs-lookup"><span data-stu-id="77c2f-112">Profiling a CLR application requires more support than profiling conventionally compiled machine code.</span></span> <span data-ttu-id="77c2f-113">这是因为 CLR 引进了诸如应用程序域、垃圾回收、托管异常处理、实时 (JIT) 代码编译（将 Microsoft 中间语言、MSIL 或代码转换为本机代码）以及类似功能的概念。</span><span class="sxs-lookup"><span data-stu-id="77c2f-113">This is because the CLR introduces concepts such as application domains, garbage collection, managed exception handling, just-in-time (JIT) compilation of code (converting Microsoft intermediate language, or MSIL, code into native machine code), and similar features.</span></span> <span data-ttu-id="77c2f-114">常规的分析机制无法识别或提供关于这些功能的有用信息。</span><span class="sxs-lookup"><span data-stu-id="77c2f-114">Conventional profiling mechanisms cannot identify or provide useful information about these features.</span></span> <span data-ttu-id="77c2f-115">分析 API 则有效地提供缺少的信息，并对 CLR 和分析的应用程序的性能产生最小的影响。</span><span class="sxs-lookup"><span data-stu-id="77c2f-115">The profiling API provides this missing information efficiently, with minimal effect on the performance of the CLR and the profiled application.</span></span>  
  
 <span data-ttu-id="77c2f-116">运行时的 JIT 编译可以很好地进行分析。</span><span class="sxs-lookup"><span data-stu-id="77c2f-116">JIT compilation at run time provides good opportunities for profiling.</span></span> <span data-ttu-id="77c2f-117">分析 API 允许探查器在对某一例程进行 JIT 编译之前更改该例程的内存中 MSIL 代码流。</span><span class="sxs-lookup"><span data-stu-id="77c2f-117">The profiling API enables a profiler to change the in-memory MSIL code stream for a routine before it is JIT-compiled.</span></span> <span data-ttu-id="77c2f-118">探查器可以利用这种方式向需要深入调查的特定例程动态添加检测代码。</span><span class="sxs-lookup"><span data-stu-id="77c2f-118">In this manner, the profiler can dynamically add instrumentation code to particular routines that need deeper investigation.</span></span> <span data-ttu-id="77c2f-119">尽管此种方法在常规方案中可用，但是通过使用分析 API 可以更轻松地实现 CLR。</span><span class="sxs-lookup"><span data-stu-id="77c2f-119">Although this approach is possible in conventional scenarios, it is much easier to implement for the CLR by using the profiling API.</span></span>  
  
 <span data-ttu-id="77c2f-120">本概述包含以下几节：</span><span class="sxs-lookup"><span data-stu-id="77c2f-120">This overview consists of the following sections:</span></span>  
  
-   [<span data-ttu-id="77c2f-121">分析 API</span><span class="sxs-lookup"><span data-stu-id="77c2f-121">The Profiling API</span></span>](#profiling_api)  
  
-   [<span data-ttu-id="77c2f-122">支持的功能</span><span class="sxs-lookup"><span data-stu-id="77c2f-122">Supported Features</span></span>](#support)  
  
-   [<span data-ttu-id="77c2f-123">通知线程</span><span class="sxs-lookup"><span data-stu-id="77c2f-123">Notification Threads</span></span>](#notification_threads)  
  
-   [<span data-ttu-id="77c2f-124">安全性</span><span class="sxs-lookup"><span data-stu-id="77c2f-124">Security</span></span>](#security)  
  
-   [<span data-ttu-id="77c2f-125">组合托管和非托管代码在代码探查器</span><span class="sxs-lookup"><span data-stu-id="77c2f-125">Combining Managed and Unmanaged Code in a Code Profiler</span></span>](#combining_managed_unmanaged)  
  
-   [<span data-ttu-id="77c2f-126">分析非托管的代码</span><span class="sxs-lookup"><span data-stu-id="77c2f-126">Profiling Unmanaged Code</span></span>](#unmanaged)  
  
-   [<span data-ttu-id="77c2f-127">使用 COM</span><span class="sxs-lookup"><span data-stu-id="77c2f-127">Using COM</span></span>](#com)  
  
-   [<span data-ttu-id="77c2f-128">调用堆栈</span><span class="sxs-lookup"><span data-stu-id="77c2f-128">Call stacks</span></span>](#call_stacks)  
  
-   [<span data-ttu-id="77c2f-129">回调和堆栈深度</span><span class="sxs-lookup"><span data-stu-id="77c2f-129">Callbacks and Stack Depth</span></span>](#callbacks)  
  
-   [<span data-ttu-id="77c2f-130">相关主题</span><span class="sxs-lookup"><span data-stu-id="77c2f-130">Related Topics</span></span>](#related_topics)  
  
<a name="profiling_api"></a>   
## <a name="the-profiling-api"></a><span data-ttu-id="77c2f-131">分析 API</span><span class="sxs-lookup"><span data-stu-id="77c2f-131">The Profiling API</span></span>  
 <span data-ttu-id="77c2f-132">通常，分析 API 用于编写*代码探查器*，是一个程序，用于监视托管应用程序执行。</span><span class="sxs-lookup"><span data-stu-id="77c2f-132">Typically, the profiling API is used to write a *code profiler*, which is a program that monitors the execution of a managed application.</span></span>  
  
 <span data-ttu-id="77c2f-133">分析 API 由探查器 DLL 使用，加载到与所分析应用程序相同的进程中。</span><span class="sxs-lookup"><span data-stu-id="77c2f-133">The profiling API is used by a profiler DLL, which is loaded into the same process as the application that is being profiled.</span></span> <span data-ttu-id="77c2f-134">探查器 DLL 实现回调接口 ([ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) .NET framework 版本 1.0 和 1.1 中， [ICorProfilerCallback2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md)版本 2.0 及更高版本中)。</span><span class="sxs-lookup"><span data-stu-id="77c2f-134">The profiler DLL implements a callback interface ([ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) in the .NET Framework version 1.0 and 1.1, [ICorProfilerCallback2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md) in version 2.0 and later).</span></span> <span data-ttu-id="77c2f-135">CLR 调用该接口的方法，以通知探查器所分析进程中发生的事件。</span><span class="sxs-lookup"><span data-stu-id="77c2f-135">The CLR calls the methods in that interface to notify the profiler of events in the profiled process.</span></span> <span data-ttu-id="77c2f-136">探查器可以调回至运行时使用中的方法[ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)和[ICorProfilerInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)接口来获取有关所分析应用程序的状态信息。</span><span class="sxs-lookup"><span data-stu-id="77c2f-136">The profiler can call back into the runtime by using the methods in the [ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md) and [ICorProfilerInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md) interfaces to obtain information about the state of the profiled application.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="77c2f-137">只有探查器解决方案的数据收集部分才能在与所分析应用程序相同的进程中运行。</span><span class="sxs-lookup"><span data-stu-id="77c2f-137">Only the data-gathering part of the profiler solution should be running in the same process as the profiled application.</span></span> <span data-ttu-id="77c2f-138">所有用户界面和数据分析都应在单独的进程中执行。</span><span class="sxs-lookup"><span data-stu-id="77c2f-138">All user interface and data analysis should be performed in a separate process.</span></span>  
  
 <span data-ttu-id="77c2f-139">下图显示探查器 DLL 如何与所分析应用程序和 CLR 交互。</span><span class="sxs-lookup"><span data-stu-id="77c2f-139">The following illustration shows how the profiler DLL interacts with the application that is being profiled and the CLR.</span></span>  
  
 <span data-ttu-id="77c2f-140">![分析体系结构](../../../../docs/framework/unmanaged-api/profiling/media/profilingarch.png "ProfilingArch")</span><span class="sxs-lookup"><span data-stu-id="77c2f-140">![Profiling Architecture](../../../../docs/framework/unmanaged-api/profiling/media/profilingarch.png "ProfilingArch")</span></span>  
<span data-ttu-id="77c2f-141">分析体系结构</span><span class="sxs-lookup"><span data-stu-id="77c2f-141">Profiling architecture</span></span>  
  
### <a name="the-notification-interfaces"></a><span data-ttu-id="77c2f-142">通知接口</span><span class="sxs-lookup"><span data-stu-id="77c2f-142">The Notification Interfaces</span></span>  
 <span data-ttu-id="77c2f-143">[ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)和[ICorProfilerCallback2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md)可被视为通知接口。</span><span class="sxs-lookup"><span data-stu-id="77c2f-143">[ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) and [ICorProfilerCallback2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md) can be considered notification interfaces.</span></span> <span data-ttu-id="77c2f-144">这些接口方法组成如[ClassLoadStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-classloadstarted-method.md)， [ClassLoadFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-classloadfinished-method.md)，和[JITCompilationStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationstarted-method.md)。</span><span class="sxs-lookup"><span data-stu-id="77c2f-144">These interfaces consist of methods such as [ClassLoadStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-classloadstarted-method.md), [ClassLoadFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-classloadfinished-method.md), and [JITCompilationStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationstarted-method.md).</span></span> <span data-ttu-id="77c2f-145">每次 CLR 进行加载或卸载类、编译函数等操作时，都会调用探查器的 `ICorProfilerCallback` 或 `ICorProfilerCallback2` 接口中的相应方法。</span><span class="sxs-lookup"><span data-stu-id="77c2f-145">Each time the CLR loads or unloads a class, compiles a function, and so on, it calls the corresponding method in the profiler's `ICorProfilerCallback` or `ICorProfilerCallback2` interface.</span></span>  
  
 <span data-ttu-id="77c2f-146">例如，探查器可以测量代码性能通过两个通知函数： [FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)和[FunctionLeave2](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md)。</span><span class="sxs-lookup"><span data-stu-id="77c2f-146">For example, a profiler could measure code performance through two notification functions: [FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md) and [FunctionLeave2](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md).</span></span> <span data-ttu-id="77c2f-147">它会对每个通知添加时间戳、累积结果并输出一个列表指示在应用程序执行期间哪个函数占用的 CPU 最多或消耗的时钟时间最长。</span><span class="sxs-lookup"><span data-stu-id="77c2f-147">It just time-stamps each notification, accumulates results, and outputs a list that indicates which functions consumed the most CPU or wall-clock time during the execution of the application.</span></span>  
  
### <a name="the-information-retrieval-interfaces"></a><span data-ttu-id="77c2f-148">信息检索接口</span><span class="sxs-lookup"><span data-stu-id="77c2f-148">The Information Retrieval Interfaces</span></span>  
 <span data-ttu-id="77c2f-149">其他主要接口分析涉及为[ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)和[ICorProfilerInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)。</span><span class="sxs-lookup"><span data-stu-id="77c2f-149">The other main interfaces involved in profiling are [ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md) and [ICorProfilerInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md).</span></span> <span data-ttu-id="77c2f-150">探查器根据需要调用这些接口，以获取更多的信息来帮助进行分析。</span><span class="sxs-lookup"><span data-stu-id="77c2f-150">The profiler calls these interfaces as required to obtain more information to help its analysis.</span></span> <span data-ttu-id="77c2f-151">例如，每当 CLR 调用[FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)函数，它会提供函数标识符。</span><span class="sxs-lookup"><span data-stu-id="77c2f-151">For example, whenever the CLR calls the [FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md) function, it supplies a function identifier.</span></span> <span data-ttu-id="77c2f-152">探查器可以获取有关该函数的详细信息，通过调用[icorprofilerinfo2:: Getfunctioninfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctioninfo2-method.md)方法来发现该函数的父类、 其名称和等等。</span><span class="sxs-lookup"><span data-stu-id="77c2f-152">The profiler can get more information about that function by calling the [ICorProfilerInfo2::GetFunctionInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctioninfo2-method.md) method to discover the function's parent class, its name, and so on.</span></span>  
  
 [<span data-ttu-id="77c2f-153">返回页首</span><span class="sxs-lookup"><span data-stu-id="77c2f-153">Back to top</span></span>](#top)  
  
<a name="support"></a>   
## <a name="supported-features"></a><span data-ttu-id="77c2f-154">支持的功能</span><span class="sxs-lookup"><span data-stu-id="77c2f-154">Supported Features</span></span>  
 <span data-ttu-id="77c2f-155">分析 API 提供公共语言运行时中发生的各种事件和操作的相关信息。</span><span class="sxs-lookup"><span data-stu-id="77c2f-155">The profiling API provides information about a variety of events and actions that occur in the common language runtime.</span></span> <span data-ttu-id="77c2f-156">你可以使用此信息来监视进程的内部工作情况，也可分析 .NET Framework 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="77c2f-156">You can use this information to monitor the inner workings of processes and to analyze the performance of your .NET Framework application.</span></span>  
  
 <span data-ttu-id="77c2f-157">分析 API 检索 CLR 中发生的以下操作和事件的相关信息：</span><span class="sxs-lookup"><span data-stu-id="77c2f-157">The profiling API retrieves information about the following actions and events that occur in the CLR:</span></span>  
  
-   <span data-ttu-id="77c2f-158">CLR 启动和关闭事件。</span><span class="sxs-lookup"><span data-stu-id="77c2f-158">CLR startup and shutdown events.</span></span>  
  
-   <span data-ttu-id="77c2f-159">应用程序域创建和关闭事件。</span><span class="sxs-lookup"><span data-stu-id="77c2f-159">Application domain creation and shutdown events.</span></span>  
  
-   <span data-ttu-id="77c2f-160">程序集加载和卸载事件。</span><span class="sxs-lookup"><span data-stu-id="77c2f-160">Assembly loading and unloading events.</span></span>  
  
-   <span data-ttu-id="77c2f-161">模块加载和卸载事件。</span><span class="sxs-lookup"><span data-stu-id="77c2f-161">Module loading and unloading events.</span></span>  
  
-   <span data-ttu-id="77c2f-162">COM vtable 创建和析构事件。</span><span class="sxs-lookup"><span data-stu-id="77c2f-162">COM vtable creation and destruction events.</span></span>  
  
-   <span data-ttu-id="77c2f-163">实时 (JIT) 编译和代码间距调整事件。</span><span class="sxs-lookup"><span data-stu-id="77c2f-163">Just-in-time (JIT) compilation and code-pitching events.</span></span>  
  
-   <span data-ttu-id="77c2f-164">类加载和卸载事件。</span><span class="sxs-lookup"><span data-stu-id="77c2f-164">Class loading and unloading events.</span></span>  
  
-   <span data-ttu-id="77c2f-165">线程创建和析构事件。</span><span class="sxs-lookup"><span data-stu-id="77c2f-165">Thread creation and destruction events.</span></span>  
  
-   <span data-ttu-id="77c2f-166">函数入口和退出事件。</span><span class="sxs-lookup"><span data-stu-id="77c2f-166">Function entry and exit events.</span></span>  
  
-   <span data-ttu-id="77c2f-167">异常。</span><span class="sxs-lookup"><span data-stu-id="77c2f-167">Exceptions.</span></span>  
  
-   <span data-ttu-id="77c2f-168">托管和非托管代码执行之间的转换。</span><span class="sxs-lookup"><span data-stu-id="77c2f-168">Transitions between managed and unmanaged code execution.</span></span>  
  
-   <span data-ttu-id="77c2f-169">不同运行时上下文之间的转换。</span><span class="sxs-lookup"><span data-stu-id="77c2f-169">Transitions between different runtime contexts.</span></span>  
  
-   <span data-ttu-id="77c2f-170">有关运行时挂起的信息。</span><span class="sxs-lookup"><span data-stu-id="77c2f-170">Information about runtime suspensions.</span></span>  
  
-   <span data-ttu-id="77c2f-171">有关运行时内存堆和垃圾回收活动的信息。</span><span class="sxs-lookup"><span data-stu-id="77c2f-171">Information about the runtime memory heap and garbage collection activity.</span></span>  
  
 <span data-ttu-id="77c2f-172">分析 API 可从任何（非托管）COM 兼容语言调用。</span><span class="sxs-lookup"><span data-stu-id="77c2f-172">The profiling API can be called from any (non-managed) COM-compatible language.</span></span>  
  
 <span data-ttu-id="77c2f-173">API 可高效减少 CPU 和内存占用。</span><span class="sxs-lookup"><span data-stu-id="77c2f-173">The API is efficient with regard to CPU and memory consumption.</span></span> <span data-ttu-id="77c2f-174">分析不包括对所分析应用程序进行足以导致误导性结果的更改。</span><span class="sxs-lookup"><span data-stu-id="77c2f-174">Profiling does not involve changes to the profiled application that are significant enough to cause misleading results.</span></span>  
  
 <span data-ttu-id="77c2f-175">分析 API 有益于采样和非采样探查器。</span><span class="sxs-lookup"><span data-stu-id="77c2f-175">The profiling API is useful to both sampling and non-sampling profilers.</span></span> <span data-ttu-id="77c2f-176">A*采样探查器*检查常规时钟计时周期的配置文件说，每 5 毫秒分离。</span><span class="sxs-lookup"><span data-stu-id="77c2f-176">A *sampling profiler* inspects the profile at regular clock ticks, say, at 5 milliseconds apart.</span></span> <span data-ttu-id="77c2f-177">A*非采样探查器*同步使用的线程来导致该事件的事件通知。</span><span class="sxs-lookup"><span data-stu-id="77c2f-177">A *non-sampling profiler* is informed of an event synchronously with the thread that causes the event.</span></span>  
  
### <a name="unsupported-functionality"></a><span data-ttu-id="77c2f-178">不支持的功能</span><span class="sxs-lookup"><span data-stu-id="77c2f-178">Unsupported Functionality</span></span>  
 <span data-ttu-id="77c2f-179">分析 API 不支持以下功能：</span><span class="sxs-lookup"><span data-stu-id="77c2f-179">The profiling API does not support the following functionality:</span></span>  
  
-   <span data-ttu-id="77c2f-180">非托管代码，此类代码必须使用常规 Win32 方法进行分析。</span><span class="sxs-lookup"><span data-stu-id="77c2f-180">Unmanaged code, which must be profiled using conventional Win32 methods.</span></span> <span data-ttu-id="77c2f-181">然而，CLR 探查器包括过渡事件，以确定托管与非托管代码之间的边界。</span><span class="sxs-lookup"><span data-stu-id="77c2f-181">However, the CLR profiler includes transition events to determine the boundaries between managed and unmanaged code.</span></span>  
  
-   <span data-ttu-id="77c2f-182">自修改应用程序，即出于某种目的（如面向方面的编程）修改自己的代码。</span><span class="sxs-lookup"><span data-stu-id="77c2f-182">Self-modifying applications that modify their own code for purposes such as aspect-oriented programming.</span></span>  
  
-   <span data-ttu-id="77c2f-183">边界检查，原因是分析 API 不提供此信息。</span><span class="sxs-lookup"><span data-stu-id="77c2f-183">Bounds checking, because the profiling API does not provide this information.</span></span> <span data-ttu-id="77c2f-184">CLR 为所有托管代码的边界检查提供内部支持。</span><span class="sxs-lookup"><span data-stu-id="77c2f-184">The CLR provides intrinsic support for bounds checking of all managed code.</span></span>  
  
-   <span data-ttu-id="77c2f-185">远程分析，在以下情况不受支持：</span><span class="sxs-lookup"><span data-stu-id="77c2f-185">Remote profiling, which is not supported for the following reasons:</span></span>  
  
    -   <span data-ttu-id="77c2f-186">远程分析延长执行时间。</span><span class="sxs-lookup"><span data-stu-id="77c2f-186">Remote profiling extends execution time.</span></span> <span data-ttu-id="77c2f-187">当使用分析接口时，必须最大限度地缩短执行时间，确保分析结果不会受到不良影响。</span><span class="sxs-lookup"><span data-stu-id="77c2f-187">When you use the profiling interfaces, you must minimize execution time so that profiling results will not be unduly affected.</span></span> <span data-ttu-id="77c2f-188">在执行性能受到监视时尤为如此。</span><span class="sxs-lookup"><span data-stu-id="77c2f-188">This is especially true when execution performance is being monitored.</span></span> <span data-ttu-id="77c2f-189">然而，当分析接口用于监视内存使用情况或用于获取有关堆栈帧、对象等的运行时信息时，远程分析并不是一个限制。</span><span class="sxs-lookup"><span data-stu-id="77c2f-189">However, remote profiling is not a limitation when the profiling interfaces are used to monitor memory usage or to obtain run-time information about stack frames, objects, and so on.</span></span>  
  
    -   <span data-ttu-id="77c2f-190">CLR 代码探查器必须向运行所分析应用程序的本地计算机上的运行时注册一个或多个回调接口。</span><span class="sxs-lookup"><span data-stu-id="77c2f-190">The CLR code profiler must register one or more callback interfaces with the runtime on the local computer on which the profiled application is running.</span></span> <span data-ttu-id="77c2f-191">这便限制了创建远程代码探查器的功能。</span><span class="sxs-lookup"><span data-stu-id="77c2f-191">This limits the ability to create a remote code profiler.</span></span>  
  
-   <span data-ttu-id="77c2f-192">在具有高可用性要求的生产环境中进行分析。</span><span class="sxs-lookup"><span data-stu-id="77c2f-192">Profiling in production environments with high-availability requirements.</span></span> <span data-ttu-id="77c2f-193">为了支持开发时诊断，已经创建了分析 API。</span><span class="sxs-lookup"><span data-stu-id="77c2f-193">The profiling API was created to support development-time diagnostics.</span></span> <span data-ttu-id="77c2f-194">但尚未进行支持生产环境所需的严格测试。</span><span class="sxs-lookup"><span data-stu-id="77c2f-194">It has not undergone the rigorous testing required to support production environments.</span></span>  
  
 [<span data-ttu-id="77c2f-195">返回页首</span><span class="sxs-lookup"><span data-stu-id="77c2f-195">Back to top</span></span>](#top)  
  
<a name="notification_threads"></a>   
## <a name="notification-threads"></a><span data-ttu-id="77c2f-196">通知线程</span><span class="sxs-lookup"><span data-stu-id="77c2f-196">Notification Threads</span></span>  
 <span data-ttu-id="77c2f-197">在大多数情况下，生成事件的线程也会执行通知。</span><span class="sxs-lookup"><span data-stu-id="77c2f-197">In most cases, the thread that generates an event also executes notifications.</span></span> <span data-ttu-id="77c2f-198">此类通知 (例如， [FunctionEnter](../../../../docs/framework/unmanaged-api/profiling/functionenter-function.md)和[FunctionLeave](../../../../docs/framework/unmanaged-api/profiling/functionleave-function.md)) 无需提供显式`ThreadID`。</span><span class="sxs-lookup"><span data-stu-id="77c2f-198">Such notifications (for example, [FunctionEnter](../../../../docs/framework/unmanaged-api/profiling/functionenter-function.md) and [FunctionLeave](../../../../docs/framework/unmanaged-api/profiling/functionleave-function.md)) do not need to supply the explicit `ThreadID`.</span></span> <span data-ttu-id="77c2f-199">此外，探查器还可能决定使用线程本地存储来存储和更新其分析块，而不是基于受影响线程的 `ThreadID` 对全局存储中的分析块建立索引。</span><span class="sxs-lookup"><span data-stu-id="77c2f-199">Also, the profiler might decide to use thread-local storage to store and update its analysis blocks instead of indexing the analysis blocks in global storage, based on the `ThreadID` of the affected thread.</span></span>  
  
 <span data-ttu-id="77c2f-200">注意，这些回调未经过序列化。</span><span class="sxs-lookup"><span data-stu-id="77c2f-200">Note that these callbacks are not serialized.</span></span> <span data-ttu-id="77c2f-201">用户必须通过创建线程安全数据结构并在必要时锁定探查器代码以防止从多个线程并行访问的方式保护代码。</span><span class="sxs-lookup"><span data-stu-id="77c2f-201">Users must protect their code by creating thread-safe data structures and by locking the profiler code where necessary to prevent parallel access from multiple threads.</span></span> <span data-ttu-id="77c2f-202">因此，在某些情况下，会收到不正常的回调序列。</span><span class="sxs-lookup"><span data-stu-id="77c2f-202">Therefore, in certain cases you can receive an unusual sequence of callbacks.</span></span> <span data-ttu-id="77c2f-203">例如，假设托管应用程序正在生成执行相同代码的两个线程。</span><span class="sxs-lookup"><span data-stu-id="77c2f-203">For example, assume that a managed application is spawning two threads that are executing identical code.</span></span> <span data-ttu-id="77c2f-204">在这种情况下，就可以接收[icorprofilercallback:: Jitcompilationstarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationstarted-method.md)执行某项功能从一个线程的事件和一个`FunctionEnter`来自另一个线程才收到回调[Icorprofilercallback:: Jitcompilationfinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationfinished-method.md)回调。</span><span class="sxs-lookup"><span data-stu-id="77c2f-204">In this case, it is possible to receive a [ICorProfilerCallback::JITCompilationStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationstarted-method.md) event for some function from one thread and a `FunctionEnter` callback from the other thread before receiving the [ICorProfilerCallback::JITCompilationFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationfinished-method.md) callback.</span></span> <span data-ttu-id="77c2f-205">在这种情况下，用户将收到可能尚未完全实时 (JIT) 编译的函数的 `FunctionEnter` 回调。</span><span class="sxs-lookup"><span data-stu-id="77c2f-205">In this case, the user will receive a `FunctionEnter` callback for a function that may not have been fully just-in-time (JIT) compiled yet.</span></span>  
  
 [<span data-ttu-id="77c2f-206">返回页首</span><span class="sxs-lookup"><span data-stu-id="77c2f-206">Back to top</span></span>](#top)  
  
<a name="security"></a>   
## <a name="security"></a><span data-ttu-id="77c2f-207">安全性</span><span class="sxs-lookup"><span data-stu-id="77c2f-207">Security</span></span>  
 <span data-ttu-id="77c2f-208">探查器 DLL 是作为公共语言运行时执行引擎的一部分运行的非托管 DLL。</span><span class="sxs-lookup"><span data-stu-id="77c2f-208">A profiler DLL is an unmanaged DLL that runs as part of the common language runtime execution engine.</span></span> <span data-ttu-id="77c2f-209">因此，探查器 DLL 中的代码并不受到托管代码访问安全性的约束。</span><span class="sxs-lookup"><span data-stu-id="77c2f-209">As a result, the code in the profiler DLL is not subject to the restrictions of managed code access security.</span></span> <span data-ttu-id="77c2f-210">探查器 DLL 的唯一限制是操作系统强加在运行所分析应用程序的用户身上的限制。</span><span class="sxs-lookup"><span data-stu-id="77c2f-210">The only limitations on the profiler DLL are those imposed by the operating system on the user who is running the profiled application.</span></span>  
  
 <span data-ttu-id="77c2f-211">探查器作者应采取适当的预防措施以避免安全相关问题。</span><span class="sxs-lookup"><span data-stu-id="77c2f-211">Profiler authors should take appropriate precautions to avoid security-related issues.</span></span> <span data-ttu-id="77c2f-212">例如，在安装期间，应将探查器 DLL 添加到访问控制列表 (ACL)，以确保恶意用户无法对其进行修改。</span><span class="sxs-lookup"><span data-stu-id="77c2f-212">For example, during installation, a profiler DLL should be added to an access control list (ACL) so that a malicious user cannot modify it.</span></span>  
  
 [<span data-ttu-id="77c2f-213">返回页首</span><span class="sxs-lookup"><span data-stu-id="77c2f-213">Back to top</span></span>](#top)  
  
<a name="combining_managed_unmanaged"></a>   
## <a name="combining-managed-and-unmanaged-code-in-a-code-profiler"></a><span data-ttu-id="77c2f-214">在代码探查器中组合托管和非托管代码</span><span class="sxs-lookup"><span data-stu-id="77c2f-214">Combining Managed and Unmanaged Code in a Code Profiler</span></span>  
 <span data-ttu-id="77c2f-215">编写错误的探查器可能会引起自身的循环引用，从而导致不可预知的行为。</span><span class="sxs-lookup"><span data-stu-id="77c2f-215">An incorrectly written profiler can cause circular references to itself, resulting in unpredictable behavior.</span></span>  
  
 <span data-ttu-id="77c2f-216">审查 CLR 分析 API 可能会形成这样的印象：可以编写包含托管和非托管组件的探查器，在探查器中这些组件通过 COM 互操作或间接调用相互调用。</span><span class="sxs-lookup"><span data-stu-id="77c2f-216">A review of the CLR profiling API may create the impression that you can write a profiler that contains managed and unmanaged components that call each other through COM interop or indirect calls.</span></span>  
  
 <span data-ttu-id="77c2f-217">虽然从设计角度而言这是可行的，但分析 API 并不支持托管组件。</span><span class="sxs-lookup"><span data-stu-id="77c2f-217">Although this is possible from a design perspective, the profiling API does not support managed components.</span></span> <span data-ttu-id="77c2f-218">CLR 探查器必须完全处于非托管状态。</span><span class="sxs-lookup"><span data-stu-id="77c2f-218">A CLR profiler must be completely unmanaged.</span></span> <span data-ttu-id="77c2f-219">尝试在 CLR 探查器中组合托管和非托管代码可能会导致访问冲突、程序故障或死锁。</span><span class="sxs-lookup"><span data-stu-id="77c2f-219">Attempts to combine managed and unmanaged code in a CLR profiler may cause access violations, program failure, or deadlocks.</span></span> <span data-ttu-id="77c2f-220">探查器的托管组件将激发事件返回其非托管组件，随后将再次调用托管组件，从而导致循环引用。</span><span class="sxs-lookup"><span data-stu-id="77c2f-220">The managed components of the profiler will fire events back to their unmanaged components, which would subsequently call the managed components again, resulting in circular references.</span></span>  
  
 <span data-ttu-id="77c2f-221">CLR 探查器可以安全调用托管代码的唯一位置是方法的 Microsoft 中间语言 (MSIL) 体。</span><span class="sxs-lookup"><span data-stu-id="77c2f-221">The only location where a CLR profiler can call managed code safely is in the Microsoft intermediate language (MSIL) body of a method.</span></span> <span data-ttu-id="77c2f-222">修改 MSIL 体的建议的做法是使用中的 JIT 重新编译方法[ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md)接口。</span><span class="sxs-lookup"><span data-stu-id="77c2f-222">The recommended practice for modifying the MSIL body is to use the  JIT recompilation methods in the [ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md) interface.</span></span>  
  
 <span data-ttu-id="77c2f-223">还可以使用较早的检测方法修改 MSIL。</span><span class="sxs-lookup"><span data-stu-id="77c2f-223">It is also possible to use the older instrumentation methods to modify MSIL.</span></span> <span data-ttu-id="77c2f-224">在完成函数的实时 (JIT) 编译之前，探查器可以方法然后进行 JIT 编译的 MSIL 体中插入托管的调用它 (请参阅[icorprofilerinfo:: Getilfunctionbody](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getilfunctionbody-method.md)方法)。</span><span class="sxs-lookup"><span data-stu-id="77c2f-224">Before the just-in-time (JIT) compilation of a function is completed, the profiler can insert managed calls in the MSIL body of a method and then JIT-compile it (see the [ICorProfilerInfo::GetILFunctionBody](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getilfunctionbody-method.md) method).</span></span> <span data-ttu-id="77c2f-225">这种技术可成功用于托管代码的选择性检测，也可用于收集有关 JIT 的统计信息和性能数据。</span><span class="sxs-lookup"><span data-stu-id="77c2f-225">This technique can successfully be used for selective instrumentation of managed code, or to gather statistics and performance data about the JIT.</span></span>  
  
 <span data-ttu-id="77c2f-226">代码探查器也可以在调用到非托管代码的每个托管函数的 MSIL 体中插入本机挂钩。</span><span class="sxs-lookup"><span data-stu-id="77c2f-226">Alternatively, a code profiler can insert native hooks in the MSIL body of every managed function that calls into unmanaged code.</span></span> <span data-ttu-id="77c2f-227">这种技术可用于检测和覆盖。</span><span class="sxs-lookup"><span data-stu-id="77c2f-227">This technique can be used for instrumentation and coverage.</span></span> <span data-ttu-id="77c2f-228">例如，代码探查器可以在每个 MSIL 块后插入检测挂钩，以确保该块已执行。</span><span class="sxs-lookup"><span data-stu-id="77c2f-228">For example, a code profiler could insert instrumentation hooks after every MSIL block to ensure that the block has been executed.</span></span> <span data-ttu-id="77c2f-229">修改方法的 MSIL 体是一项非常细致的操作，因此必须将许多因素考虑在内。</span><span class="sxs-lookup"><span data-stu-id="77c2f-229">The modification of the MSIL body of a method is a very delicate operation, and there are many factors that should be taken into consideration.</span></span>  
  
 [<span data-ttu-id="77c2f-230">返回页首</span><span class="sxs-lookup"><span data-stu-id="77c2f-230">Back to top</span></span>](#top)  
  
<a name="unmanaged"></a>   
## <a name="profiling-unmanaged-code"></a><span data-ttu-id="77c2f-231">分析非托管代码</span><span class="sxs-lookup"><span data-stu-id="77c2f-231">Profiling Unmanaged Code</span></span>  
 <span data-ttu-id="77c2f-232">公共语言运行时 (CLR) 分析 API 为分析非托管代码提供最低支持。</span><span class="sxs-lookup"><span data-stu-id="77c2f-232">The common language runtime (CLR) profiling API provides minimal support for profiling unmanaged code.</span></span> <span data-ttu-id="77c2f-233">它具有以下功能：</span><span class="sxs-lookup"><span data-stu-id="77c2f-233">The following functionality is provided:</span></span>  
  
-   <span data-ttu-id="77c2f-234">堆栈链的枚举。</span><span class="sxs-lookup"><span data-stu-id="77c2f-234">Enumeration of stack chains.</span></span> <span data-ttu-id="77c2f-235">借助此功能，代码探查器能够确定托管代码与非托管代码之间的边界。</span><span class="sxs-lookup"><span data-stu-id="77c2f-235">This feature enables a code profiler to determine the boundary between managed code and unmanaged code.</span></span>  
  
-   <span data-ttu-id="77c2f-236">确定堆栈链是否与托管代码或本机代码对应。</span><span class="sxs-lookup"><span data-stu-id="77c2f-236">Determination whether a stack chain corresponds to managed code or native code.</span></span>  
  
 <span data-ttu-id="77c2f-237">在 .NET Framework 1.0 和 1.1 版中，可通过 CLR 调试 API 的进程内子集使用这些方法。</span><span class="sxs-lookup"><span data-stu-id="77c2f-237">In the .NET Framework versions 1.0 and 1.1, these methods are available through the in-process subset of the CLR debugging API.</span></span> <span data-ttu-id="77c2f-238">它们在 CorDebug.idl 文件中定义。</span><span class="sxs-lookup"><span data-stu-id="77c2f-238">They are defined in the CorDebug.idl file.</span></span>  
  
 <span data-ttu-id="77c2f-239">在.NET Framework 2.0 和更高版本，你可以使用[icorprofilerinfo2:: Dostacksnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)此功能的方法。</span><span class="sxs-lookup"><span data-stu-id="77c2f-239">In the .NET Framework 2.0 and later, you can use the [ICorProfilerInfo2::DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md) method for this functionality.</span></span>  
  
 [<span data-ttu-id="77c2f-240">返回页首</span><span class="sxs-lookup"><span data-stu-id="77c2f-240">Back to top</span></span>](#top)  
  
<a name="com"></a>   
## <a name="using-com"></a><span data-ttu-id="77c2f-241">使用 COM</span><span class="sxs-lookup"><span data-stu-id="77c2f-241">Using COM</span></span>  
 <span data-ttu-id="77c2f-242">尽管将分析接口定义为 COM 接口，但公共语言运行时 (CLR) 并不会实际初始化 COM 以使用这些接口。</span><span class="sxs-lookup"><span data-stu-id="77c2f-242">Although the profiling interfaces are defined as COM interfaces, the common language runtime (CLR) does not actually initialize COM to use these interfaces.</span></span> <span data-ttu-id="77c2f-243">原因是为了避免使用设置的线程模型[CoInitialize](http://msdn.microsoft.com/library/windows/desktop/ms678543\(v=vs.85\).aspx)函数在托管应用程序有机会指定其所需的线程处理模型之前。</span><span class="sxs-lookup"><span data-stu-id="77c2f-243">The reason is to avoid having to set the threading model by using the [CoInitialize](http://msdn.microsoft.com/library/windows/desktop/ms678543\(v=vs.85\).aspx) function before the managed application has had a chance to specify its desired threading model.</span></span> <span data-ttu-id="77c2f-244">同样，探查器本身不应调用 `CoInitialize`，因为它可能会选取与所分析应用程序不兼容的线程模型，并可能会导致应用程序失败。</span><span class="sxs-lookup"><span data-stu-id="77c2f-244">Similarly, the profiler itself should not call `CoInitialize`, because it may pick a threading model that is incompatible with the application being profiled and may cause the application to fail.</span></span>  
  
 [<span data-ttu-id="77c2f-245">返回页首</span><span class="sxs-lookup"><span data-stu-id="77c2f-245">Back to top</span></span>](#top)  
  
<a name="call_stacks"></a>   
## <a name="call-stacks"></a><span data-ttu-id="77c2f-246">调用堆栈</span><span class="sxs-lookup"><span data-stu-id="77c2f-246">Call Stacks</span></span>  
 <span data-ttu-id="77c2f-247">分析 API 提供两种方法来获取调用堆栈：堆栈快照方法和阴影堆栈方法，前者以分散方式收集调用堆栈，后者时刻跟踪调用堆栈。</span><span class="sxs-lookup"><span data-stu-id="77c2f-247">The profiling API provides two ways to obtain call stacks: a stack snapshot method, which enables sparse gathering of call stacks, and a shadow stack method, which tracks the call stack at every instant.</span></span>  
  
### <a name="stack-snapshot"></a><span data-ttu-id="77c2f-248">堆栈快照</span><span class="sxs-lookup"><span data-stu-id="77c2f-248">Stack Snapshot</span></span>  
 <span data-ttu-id="77c2f-249">堆栈快照是线程堆栈在某一时刻的跟踪。</span><span class="sxs-lookup"><span data-stu-id="77c2f-249">A stack snapshot is a trace of the stack of a thread at an instant in time.</span></span> <span data-ttu-id="77c2f-250">分析 API 支持在堆栈上跟踪托管函数，但它会将跟踪非托管函数的工作交给探查器自己的堆栈审核器来完成。</span><span class="sxs-lookup"><span data-stu-id="77c2f-250">The profiling API supports the tracing of managed functions on the stack, but it leaves the tracing of unmanaged functions to the profiler's own stack walker.</span></span>  
  
 <span data-ttu-id="77c2f-251">有关如何进行编程以审核托管的堆栈探查器的详细信息，请参阅[icorprofilerinfo2:: Dostacksnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)此文档集中的方法和[.NET Framework 2.0 中的探查器堆栈审核：基础知识和扩展](http://go.microsoft.com/fwlink/?LinkId=73638)。</span><span class="sxs-lookup"><span data-stu-id="77c2f-251">For more information about how to program the profiler to walk managed stacks, see the [ICorProfilerInfo2::DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md) method in this documentation set, and [Profiler Stack Walking in the .NET Framework 2.0: Basics and Beyond](http://go.microsoft.com/fwlink/?LinkId=73638).</span></span>
  
### <a name="shadow-stack"></a><span data-ttu-id="77c2f-252">阴影堆栈</span><span class="sxs-lookup"><span data-stu-id="77c2f-252">Shadow Stack</span></span>  
 <span data-ttu-id="77c2f-253">过度频繁使用快照方法很快就会产生性能问题。</span><span class="sxs-lookup"><span data-stu-id="77c2f-253">Using the snapshot method too frequently can quickly create a performance issue.</span></span> <span data-ttu-id="77c2f-254">如果你想要频繁进行堆栈跟踪，探查器而是应通过使用生成阴影堆栈[FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)， [FunctionLeave2](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md)， [FunctionTailcall2](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md)，和[ICorProfilerCallback2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md)异常回调。</span><span class="sxs-lookup"><span data-stu-id="77c2f-254">If you want to take stack traces frequently, your profiler should instead build a shadow stack by using the [FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md), [FunctionLeave2](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md), [FunctionTailcall2](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md), and [ICorProfilerCallback2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md) exception callbacks.</span></span> <span data-ttu-id="77c2f-255">阴影堆栈始终是最新的，并且在需要堆栈快照时可以快速复制到存储区。</span><span class="sxs-lookup"><span data-stu-id="77c2f-255">The shadow stack is always current and can quickly be copied to storage whenever a stack snapshot is needed.</span></span>  
  
 <span data-ttu-id="77c2f-256">阴影堆栈可以获取函数参数、返回值和有关泛型实例化的信息。</span><span class="sxs-lookup"><span data-stu-id="77c2f-256">A shadow stack may obtain function arguments, return values, and information about generic instantiations.</span></span> <span data-ttu-id="77c2f-257">泛型实例化信息只能通过阴影堆栈获取，并可能在将控件传递到函数时获取。</span><span class="sxs-lookup"><span data-stu-id="77c2f-257">This information is available only through the shadow stack and may be obtained when control is handed to a function.</span></span> <span data-ttu-id="77c2f-258">然而，后续运行此函数时，此信息可能不可用。</span><span class="sxs-lookup"><span data-stu-id="77c2f-258">However, this information may not be available later during the run of the function.</span></span>  
  
 [<span data-ttu-id="77c2f-259">返回页首</span><span class="sxs-lookup"><span data-stu-id="77c2f-259">Back to top</span></span>](#top)  
  
<a name="callbacks"></a>   
## <a name="callbacks-and-stack-depth"></a><span data-ttu-id="77c2f-260">回调和堆栈深度</span><span class="sxs-lookup"><span data-stu-id="77c2f-260">Callbacks and Stack Depth</span></span>  
 <span data-ttu-id="77c2f-261">在堆栈受到严重限制的情况下，可能会引发探查器回调；并且探查器回调中的堆栈溢出将导致进程立即退出。</span><span class="sxs-lookup"><span data-stu-id="77c2f-261">Profiler callbacks may be issued in very stack-constrained circumstances, and a stack overflow in a profiler callback will lead to an immediate process exit.</span></span> <span data-ttu-id="77c2f-262">探查器应确保尽可能少使用堆栈来响应回调。</span><span class="sxs-lookup"><span data-stu-id="77c2f-262">A profiler should make sure to use as little stack as possible in response to callbacks.</span></span> <span data-ttu-id="77c2f-263">如果希望将探查器用于抑制堆栈溢出的可靠进程中，那么探查器本身也应避免触发堆栈溢出。</span><span class="sxs-lookup"><span data-stu-id="77c2f-263">If the profiler is intended for use against processes that are robust against stack overflow, the profiler itself should also avoid triggering stack overflow.</span></span>  
  
 [<span data-ttu-id="77c2f-264">返回页首</span><span class="sxs-lookup"><span data-stu-id="77c2f-264">Back to top</span></span>](#top)  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a><span data-ttu-id="77c2f-265">相关主题</span><span class="sxs-lookup"><span data-stu-id="77c2f-265">Related Topics</span></span>  
  
|<span data-ttu-id="77c2f-266">标题</span><span class="sxs-lookup"><span data-stu-id="77c2f-266">Title</span></span>|<span data-ttu-id="77c2f-267">描述</span><span class="sxs-lookup"><span data-stu-id="77c2f-267">Description</span></span>|  
|-----------|-----------------|  
|[<span data-ttu-id="77c2f-268">设置分析环境</span><span class="sxs-lookup"><span data-stu-id="77c2f-268">Setting Up a Profiling Environment</span></span>](../../../../docs/framework/unmanaged-api/profiling/setting-up-a-profiling-environment.md)|<span data-ttu-id="77c2f-269">说明如何初始化探查器、设置事件通知和分析 Windows 服务。</span><span class="sxs-lookup"><span data-stu-id="77c2f-269">Explains how to initialize a profiler, set event notifications, and profile a Windows Service.</span></span>|  
|[<span data-ttu-id="77c2f-270">分析接口</span><span class="sxs-lookup"><span data-stu-id="77c2f-270">Profiling Interfaces</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)|<span data-ttu-id="77c2f-271">描述分析 API 使用的非托管接口。</span><span class="sxs-lookup"><span data-stu-id="77c2f-271">Describes the unmanaged interfaces that the profiling API uses.</span></span>|  
|[<span data-ttu-id="77c2f-272">分析全局静态函数</span><span class="sxs-lookup"><span data-stu-id="77c2f-272">Profiling Global Static Functions</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)|<span data-ttu-id="77c2f-273">描述分析 API 使用的非托管全局静态函数。</span><span class="sxs-lookup"><span data-stu-id="77c2f-273">Describes the unmanaged global static functions that the profiling API uses.</span></span>|  
|[<span data-ttu-id="77c2f-274">分析枚举</span><span class="sxs-lookup"><span data-stu-id="77c2f-274">Profiling Enumerations</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)|<span data-ttu-id="77c2f-275">描述分析 API 使用的非托管枚举。</span><span class="sxs-lookup"><span data-stu-id="77c2f-275">Describes the unmanaged enumerations that the profiling API uses.</span></span>|  
|[<span data-ttu-id="77c2f-276">分析结构</span><span class="sxs-lookup"><span data-stu-id="77c2f-276">Profiling Structures</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-structures.md)|<span data-ttu-id="77c2f-277">描述分析 API 使用的非托管结构。</span><span class="sxs-lookup"><span data-stu-id="77c2f-277">Describes the unmanaged structures that the profiling API uses.</span></span>|