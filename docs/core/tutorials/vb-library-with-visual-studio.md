---
title: "使用 Visual Studio 2017 生成 Visual Basic .NET Core 类库"
description: "了解如何使用 Visual Studio 2017 生成 Visual Basic 类库"
keywords: ".NET Core, .NET Standard 类库, Visual Studio 2017, Visual Basic"
author: rpetrusha
ms.author: ronpet
ms.date: 08/07/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-vb
dev_langs: vb
ms.openlocfilehash: 6572f35b1e2b652c9f2ff5448165ece104f0bdf6
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2017
---
# <a name="building-a-class-library-with-visual-basic-and-net-core-in-visual-studio-2017"></a><span data-ttu-id="7ce49-104">使用 Visual Studio 2017 生成 Visual Basic .NET Core 类库</span><span class="sxs-lookup"><span data-stu-id="7ce49-104">Building a class library with Visual Basic and .NET Core in Visual Studio 2017</span></span>

<span data-ttu-id="7ce49-105">类库定义的是可以由应用程序调用的类型和方法。</span><span class="sxs-lookup"><span data-stu-id="7ce49-105">A *class library* defines types and methods that are called by an application.</span></span> <span data-ttu-id="7ce49-106">借助定目标到 .NET Standard 2.0 的类库，任何支持相应版本 .NET Standard 的 .NET 实现都可以调用库。</span><span class="sxs-lookup"><span data-stu-id="7ce49-106">A class library that targets the .NET Standard 2.0 allows your library to be called by any .NET implementation that supports that version of the .NET Standard.</span></span> <span data-ttu-id="7ce49-107">完成类库时，可以决定是要将其作为第三方组件进行分布，还是要将其作为与一个或多个应用程序捆绑在一起的组件进行添加。</span><span class="sxs-lookup"><span data-stu-id="7ce49-107">When you finish your class library, you can decide whether you want to distribute it as a third-party component or whether you want to include it as a bundled component with one or more applications.</span></span>

> [!NOTE]
> <span data-ttu-id="7ce49-108">有关 .NET Standard 版本及其支持的平台列表，请参阅 [.NET Standard](../../standard/net-standard.md)。</span><span class="sxs-lookup"><span data-stu-id="7ce49-108">For a list of the .NET Standard versions and the platforms they support, see [.NET Standard](../../standard/net-standard.md).</span></span>

<span data-ttu-id="7ce49-109">在本主题中，将创建包含一个字符串处理方法的简单实用工具库。</span><span class="sxs-lookup"><span data-stu-id="7ce49-109">In this topic, you'll create a simple utility library that contains a single string-handling method.</span></span> <span data-ttu-id="7ce49-110">我们将把它作为[扩展方法](../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)进行实现，这样就可以把它作为 <xref:System.String> 类成员进行调用。</span><span class="sxs-lookup"><span data-stu-id="7ce49-110">You'll implement it as an [extension method](../../visual-basic/programming-guide/language-features/procedures/extension-methods.md) so that you can call it as if it were a member of the <xref:System.String> class.</span></span>

## <a name="creating-a-class-library-solution"></a><span data-ttu-id="7ce49-111">创建类库解决方案</span><span class="sxs-lookup"><span data-stu-id="7ce49-111">Creating a class library solution</span></span>

<span data-ttu-id="7ce49-112">首先为类库项目及其相关项目创建解决方案。</span><span class="sxs-lookup"><span data-stu-id="7ce49-112">Start by creating a solution for your class library project and its related projects.</span></span> <span data-ttu-id="7ce49-113">Visual Studio 解决方案只用作一个或多个项目的容器。</span><span class="sxs-lookup"><span data-stu-id="7ce49-113">A Visual Studio Solution just serves as a container for one or more projects.</span></span> <span data-ttu-id="7ce49-114">若要创建解决方案，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="7ce49-114">To create the solution:</span></span>

1. <span data-ttu-id="7ce49-115">在 Visual Studio 菜单栏上，选择“文件” > “新建” > “项目”。</span><span class="sxs-lookup"><span data-stu-id="7ce49-115">On the Visual Studio menu bar, choose **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="7ce49-116">在“新建项目”对话框中，展开“其他项目类型”节点，然后选择“Visual Studio 解决方案”。</span><span class="sxs-lookup"><span data-stu-id="7ce49-116">In the **New Project** dialog, expand the **Other Project Types** node, and select **Visual Studio Solutions**.</span></span> <span data-ttu-id="7ce49-117">将解决方案命名为“ClassLibraryProjects”，然后选择“确定”按钮。</span><span class="sxs-lookup"><span data-stu-id="7ce49-117">Name the solution "ClassLibraryProjects" and select the **OK** button.</span></span>

   ![“新建项目”对话框](./media/library-with-visual-studio/newproject.png)

## <a name="creating-the-class-library-project"></a><span data-ttu-id="7ce49-119">创建类库项目</span><span class="sxs-lookup"><span data-stu-id="7ce49-119">Creating the class library project</span></span>

<span data-ttu-id="7ce49-120">创建类库项目：</span><span class="sxs-lookup"><span data-stu-id="7ce49-120">Create your class library project:</span></span>

1. <span data-ttu-id="7ce49-121">在“解决方案资源管理器”中，右键单击“ClassLibraryProjects”解决方案文件，然后从上下文菜单中选择“添加” > “新项目”。</span><span class="sxs-lookup"><span data-stu-id="7ce49-121">In **Solution Explorer**, right-click on the **ClassLibraryProjects** solution file and from the context menu, select **Add** > **New Project**.</span></span>

1. <span data-ttu-id="7ce49-122">在“添加新项目”对话框中，展开“Visual Basic”节点，并依次选择“.NET Standard”节点和“类库(.NET Standard)”项目模板。</span><span class="sxs-lookup"><span data-stu-id="7ce49-122">In the **Add New Project** dialog, expand the **Visual Basic** node, then select the **.NET Standard** node followed by the **Class Library (.NET Standard)** project template.</span></span> <span data-ttu-id="7ce49-123">在“名称”文本框中，输入项目名称“StringLibrary”。</span><span class="sxs-lookup"><span data-stu-id="7ce49-123">In the **Name** text box, enter "StringLibrary" as the name of the project.</span></span> <span data-ttu-id="7ce49-124">选择“确定”，创建类库项目。</span><span class="sxs-lookup"><span data-stu-id="7ce49-124">Select **OK** to create the class library project.</span></span>

   ![“添加新项目”对话框](./media/vb-library-with-visual-studio/libproject.png)

   <span data-ttu-id="7ce49-126">然后，代码窗口在 Visual Studio 开发环境中打开。</span><span class="sxs-lookup"><span data-stu-id="7ce49-126">The code window then opens in the Visual Studio development environment.</span></span> 
 
   ![显示默认类库模板代码的 Visual Studio 应用程序窗口](./media/vb-library-with-visual-studio/stringlibrary.png)

1. <span data-ttu-id="7ce49-128">请检查以确保库定目标到 .NET Standard 的正确版本。</span><span class="sxs-lookup"><span data-stu-id="7ce49-128">Check to make sure that the library targets the correct version of the .NET Standard.</span></span> <span data-ttu-id="7ce49-129">右键单击“解决方案资源管理器”窗口中的库项目，再选择“属性”。</span><span class="sxs-lookup"><span data-stu-id="7ce49-129">Right-click on the library project in the **Solution Explorer** windows, then select **Properties**.</span></span> <span data-ttu-id="7ce49-130">“目标框架”文本框显示定目标到 .NET Standard 2.0。</span><span class="sxs-lookup"><span data-stu-id="7ce49-130">The **Target Framework** text box shows that we're targeting .NET Standard 2.0.</span></span>

   ![类库的项目属性](./media/library-with-visual-studio/properties.png)

1. <span data-ttu-id="7ce49-132">另外，在“属性”对话框中，清除“根命名空间”文本框中的文本。</span><span class="sxs-lookup"><span data-stu-id="7ce49-132">Also in the **Properties** dialog, clear the text in the **Root namespace** text box.</span></span> <span data-ttu-id="7ce49-133">对于每个项目，Visual Basic 会自动创建与项目名称对应的命名空间，在源代码文件中定义的任何命名空间都是相应命名空间的父级。</span><span class="sxs-lookup"><span data-stu-id="7ce49-133">For each project, Visual Basic automatically creates a namespace that corresponds to the project name, and any namespaces defined in source code files are parents of that namespace.</span></span> <span data-ttu-id="7ce49-134">我们要使用 [`namespace`](../../visual-basic/language-reference/statements/namespace-statement.md) 关键字来定义顶级命名空间。</span><span class="sxs-lookup"><span data-stu-id="7ce49-134">We want to define a top-level namespace by using the [`namespace`](../../visual-basic/language-reference/statements/namespace-statement.md) keyword.</span></span>
  
1. <span data-ttu-id="7ce49-135">将代码窗口中的代码替换为以下代码，并保存文件：</span><span class="sxs-lookup"><span data-stu-id="7ce49-135">Replace the code in the code window with the following code and save the file:</span></span>

  [!CODE-vb[ClassLib#1](../../../samples/snippets/core/tutorials/vb-library-with-visual-studio/stringlibrary.vb)]

   <span data-ttu-id="7ce49-136">类库 `UtilityLibraries.StringLibrary` 包含 `StartsWithUpper` 方法，此方法会返回 <xref:System.Boolean> 值，以指明当前字符串实例是否以大写字符开头。</span><span class="sxs-lookup"><span data-stu-id="7ce49-136">The class library, `UtilityLibraries.StringLibrary`, contains a method named `StartsWithUpper`, which returns a <xref:System.Boolean> value that indicates whether the current string instance begins with an uppercase character.</span></span> <span data-ttu-id="7ce49-137">Unicode 标准会区分大小写字符。</span><span class="sxs-lookup"><span data-stu-id="7ce49-137">The Unicode standard distinguishes uppercase characters from lowercase characters.</span></span> <span data-ttu-id="7ce49-138">如果为大写字符，<xref:System.Char.IsUpper(System.Char)?displayProperty=nameWithType> 方法返回 `true`。</span><span class="sxs-lookup"><span data-stu-id="7ce49-138">The <xref:System.Char.IsUpper(System.Char)?displayProperty=nameWithType> method returns `true` if a character is uppercase.</span></span>

1. <span data-ttu-id="7ce49-139">在菜单栏中，选择“生成” > “生成解决方案”。</span><span class="sxs-lookup"><span data-stu-id="7ce49-139">On the menu bar, select **Build** > **Build Solution**.</span></span> <span data-ttu-id="7ce49-140">此项目的编译应该没有错误。</span><span class="sxs-lookup"><span data-stu-id="7ce49-140">The project should compile without error.</span></span>

   ![显示生成成功的输出窗格](./media/library-with-visual-studio/buildsucceeds.png)



## <a name="next-step"></a><span data-ttu-id="7ce49-142">下一步</span><span class="sxs-lookup"><span data-stu-id="7ce49-142">Next step</span></span>

<span data-ttu-id="7ce49-143">已成功生成库。</span><span class="sxs-lookup"><span data-stu-id="7ce49-143">You've successfully built the library.</span></span> <span data-ttu-id="7ce49-144">由于尚未调用库的任何方法，因此还不知道它能否按预期运行。</span><span class="sxs-lookup"><span data-stu-id="7ce49-144">Because you haven't called any of its methods, you don't know whether it works as expected.</span></span> <span data-ttu-id="7ce49-145">开发库的下一步是使用[单元测试项目](testing-library-with-visual-studio.md)测试库。</span><span class="sxs-lookup"><span data-stu-id="7ce49-145">The next step in developing your library is to test it by using a [Unit Test Project](testing-library-with-visual-studio.md).</span></span>