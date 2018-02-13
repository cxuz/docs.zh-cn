---
title: "如何：使用 String.Split 分析字符串（C# 指南）"
description: "String.Split 返回从一组分隔符中拆分的字符串数组。 这是分析字符串的一种简单方法。"
ms.date: 01/03/2018
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- splitting strings [C#]
- Split method [C#]
- strings [C#], splitting
- parse strings
ms.assetid: 729c2923-4169-41c6-9c90-ef176c1e2953
author: BillWagner
ms.author: wiwagn
ms.custom: mvc
ms.openlocfilehash: 5143fed04148fb17697bd5d040ad23b762505db4
ms.sourcegitcommit: 099aa20d9b6450d1b7452d782a55771a6ad8ff35
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2018
---
# <a name="how-to-parse-strings-using-stringsplit-c-guide"></a><span data-ttu-id="25902-104">如何：使用 String.Split 分析字符串（C# 指南）</span><span class="sxs-lookup"><span data-stu-id="25902-104">How to: Parse Strings Using String.Split (C# Guide)</span></span>

<span data-ttu-id="25902-105"><xref:System.String.Split%2A?displayProperty=nameWithType> 方法通过基于一个或多个分隔符拆分输入字符串来创建子字符串数组。</span><span class="sxs-lookup"><span data-stu-id="25902-105">The <xref:System.String.Split%2A?displayProperty=nameWithType> method creates an array of substrings by splitting the input string based on one or more delimiters.</span></span> <span data-ttu-id="25902-106">最简单的方法通常是分隔字边界上的字符串。</span><span class="sxs-lookup"><span data-stu-id="25902-106">It is often the easiest way to separate a string on word boundaries.</span></span> <span data-ttu-id="25902-107">它也用于拆分其他特定字符或字符串上的字符串。</span><span class="sxs-lookup"><span data-stu-id="25902-107">It is also used to split strings on other specific characters or strings.</span></span>

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

<span data-ttu-id="25902-108">下方代码将一个常用短语拆分为一个由每个单词组成的字符串数组。</span><span class="sxs-lookup"><span data-stu-id="25902-108">The following code splits a common phrase into an array of strings for each word.</span></span>

[!code-csharp-interactive[split strings on word boundaries](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#1)]

<span data-ttu-id="25902-109">分隔符的每个实例都会在返回的数组中产生一个值。</span><span class="sxs-lookup"><span data-stu-id="25902-109">Every instance of a separator character produces a value in the returned array.</span></span> <span data-ttu-id="25902-110">连续的分隔符将生成空字符串作为返回的数组中的值。</span><span class="sxs-lookup"><span data-stu-id="25902-110">Consecutive separator characters produce the empty string as a value in the returned array.</span></span>  <span data-ttu-id="25902-111">在下方示例中可以看到上述情况，其中使用空格作为分隔符：</span><span class="sxs-lookup"><span data-stu-id="25902-111">You can see this in the following example, which uses space as a separator:</span></span>

[!code-csharp-interactive[split strings with repeated separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#2)]

<span data-ttu-id="25902-112">该行为可以更容易地用逗号分隔值 (CSV) 文件之类的格式表示表格数据。</span><span class="sxs-lookup"><span data-stu-id="25902-112">This behavior makes it easier for formats like comma separated values (CSV) files representing tabular data.</span></span> <span data-ttu-id="25902-113">连续的逗号表示空白列。</span><span class="sxs-lookup"><span data-stu-id="25902-113">Consecutive commas represent a blank column.</span></span>

<span data-ttu-id="25902-114">可传递可选 <xref:System.StringSplitOptions.RemoveEmptyEntries?displayProperty=nameWithType> 参数来排除返回数组中的任何空字符串。</span><span class="sxs-lookup"><span data-stu-id="25902-114">You can pass an optional <xref:System.StringSplitOptions.RemoveEmptyEntries?displayProperty=nameWithType> parameter to exclude any empty strings in the returned array.</span></span> <span data-ttu-id="25902-115">要对返回的集合进行更复杂的处理，可使用 [LINQ](../programming-guide/concepts/linq/index.md) 来处理结果序列。</span><span class="sxs-lookup"><span data-stu-id="25902-115">For more complicated processing of the returned collection, you can use [LINQ](../programming-guide/concepts/linq/index.md) to manipulate the result sequence.</span></span>    

<span data-ttu-id="25902-116"><xref:System.String.Split%2A?displayProperty=nameWithType> 可使用多个分隔符。</span><span class="sxs-lookup"><span data-stu-id="25902-116"><xref:System.String.Split%2A?displayProperty=nameWithType> can use multiple separator characters.</span></span> <span data-ttu-id="25902-117">以下示例使用空格、逗号、句点、冒号和制表符，所有内容均在包含这些分隔字符的数组中传递到 <xref:System.String.Split%2A>。</span><span class="sxs-lookup"><span data-stu-id="25902-117">The following example uses spaces, commas, periods, colons, and tabs, all passed in an array containing these separating characters, to <xref:System.String.Split%2A>.</span></span>  <span data-ttu-id="25902-118">代码底部的循环显示返回数组中的每个单词。</span><span class="sxs-lookup"><span data-stu-id="25902-118">The loop at the bottom of the code displays each of the words in the returned array.</span></span>  

[!code-csharp-interactive[split strings using multiple separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#3)]

<span data-ttu-id="25902-119">任何分隔符的连续实例都会在输出数组中生成空字符串：</span><span class="sxs-lookup"><span data-stu-id="25902-119">Consecutive instances of any separator produce the empty string in the output array:</span></span>

[!code-csharp-interactive[split strings using multiple consecutive separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#4)]

<span data-ttu-id="25902-120"><xref:System.String.Split%2A?displayProperty=nameWithType> 可采用字符串数组（充当用于分析目标字符串的分隔符的字符序列，而非单个字符）。</span><span class="sxs-lookup"><span data-stu-id="25902-120"><xref:System.String.Split%2A?displayProperty=nameWithType> can take an array of strings (character sequences that act as separators for parsing the target string, instead of single characters).</span></span>  
  
[!code-csharp-interactive[split strings using strings as separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#5)]

<span data-ttu-id="25902-121">可通过查看 [GitHub 存储库](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/how-to/strings)中的代码来尝试这些示例</span><span class="sxs-lookup"><span data-stu-id="25902-121">You can try these samples by looking at the code in our [GitHub repository](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/how-to/strings)</span></span>

## <a name="see-also"></a><span data-ttu-id="25902-122">请参阅</span><span class="sxs-lookup"><span data-stu-id="25902-122">See Also</span></span>  
 [<span data-ttu-id="25902-123">C# 编程指南</span><span class="sxs-lookup"><span data-stu-id="25902-123">C# Programming Guide</span></span>](../programming-guide/index.md)  
 [<span data-ttu-id="25902-124">字符串</span><span class="sxs-lookup"><span data-stu-id="25902-124">Strings</span></span>](../programming-guide/strings/index.md)  
 [<span data-ttu-id="25902-125">.NET Framework 正则表达式</span><span class="sxs-lookup"><span data-stu-id="25902-125">.NET Framework Regular Expressions</span></span>](https://msdn.microsoft.com/library/hs600312)