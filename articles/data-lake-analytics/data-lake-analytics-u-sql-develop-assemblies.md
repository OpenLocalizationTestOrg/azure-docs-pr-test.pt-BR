---
title: "assemblies aaaDevelop U-SQL para trabalhos de análise do Azure Data Lake | Microsoft Docs"
description: "Saiba como toodevelop assemblies toobe usado e reutilizado em análise Data Lake trabalhos. "
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: 86dd17b25e0967306ed36bb5b7f3178d9409d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="b6257-103">Desenvolver assemblies do U-SQL para trabalhos do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b6257-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="b6257-104">Saiba como tooturn por trás do código em assemblies toobe usado e reutilizado em trabalhos da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="b6257-104">Learn how tooturn code-behind into assemblies toobe used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="b6257-105">U-SQL torna fácil tooadd próprios e personalizados de código em linguagens .net, como c#, VB.Net ou F #.</span><span class="sxs-lookup"><span data-stu-id="b6257-105">U-SQL makes it easy tooadd your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="b6257-106">Você ainda pode implantar sua própria toosupport de tempo de execução outras linguagens.</span><span class="sxs-lookup"><span data-stu-id="b6257-106">You can even deploy your own runtime toosupport other languages.</span></span>

<span data-ttu-id="b6257-107">Olá mais fácil maneira toouse código personalizado é toouse Olá Data Lake Tools para recursos de por trás do código do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6257-107">hello easiest way toouse custom code is toouse hello Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="b6257-108">Para obter mais informações, consulte o [Tutorial: desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b6257-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="b6257-109">Há algumas desvantagens em usar code-behind:</span><span class="sxs-lookup"><span data-stu-id="b6257-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="b6257-110">código-fonte Olá é carregado para o envio de cada script.</span><span class="sxs-lookup"><span data-stu-id="b6257-110">hello source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="b6257-111">O code-behind não pode ser compartilhado com outros trabalhos.</span><span class="sxs-lookup"><span data-stu-id="b6257-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="b6257-112">tooaddress essas desvantagens, você pode transformar por trás do código em assemblies e registrar o catálogo do hello assemblies toohello análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="b6257-112">tooaddress these drawbacks, you can turn code-behind into assemblies, and register hello assemblies toohello Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6257-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b6257-113">Prerequisites</span></span>
* <span data-ttu-id="b6257-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 atualização 4 ou Visual Studio 2012 com Visual C++ instalado</span><span class="sxs-lookup"><span data-stu-id="b6257-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="b6257-115">SDK do Microsoft Azure para .NET versão 2.5 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b6257-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="b6257-116">Instale-o usando o instalador de plataforma da Web hello ou o instalador do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b6257-116">Install it using hello Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="b6257-117">Uma conta da Análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="b6257-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="b6257-118">Confira [Introdução ao Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b6257-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="b6257-119">Passar Olá [Introdução ao Azure Data Lake análise U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="b6257-119">Go through hello [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="b6257-120">Conecte-se tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b6257-120">Connect tooAzure.</span></span>
* <span data-ttu-id="b6257-121">Carregar dados de origem hello, consulte [Introdução ao Azure Data Lake análise U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b6257-121">Upload hello source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="b6257-122">Desenvolver assemblies para U-SQL</span><span class="sxs-lookup"><span data-stu-id="b6257-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="b6257-123">**toocreate e enviar um trabalho de U-SQL**</span><span class="sxs-lookup"><span data-stu-id="b6257-123">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="b6257-124">De saudação **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="b6257-124">From hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="b6257-125">Expanda **instalado**, **modelos**, **Azure Data Lake**, **U-SQL(ADLA)**, selecione Olá **biblioteca de classes (para U-SQL Aplicativo)** modelo e depois clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b6257-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select hello **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="b6257-126">Escreva seu código em Class1.cs.</span><span class="sxs-lookup"><span data-stu-id="b6257-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="b6257-127">a seguir Olá é um exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="b6257-127">hello following is a code sample.</span></span>

        using Microsoft.Analytics.Interfaces;

        namespace USQLApplication_codebehind
        {
            [SqlUserDefinedProcessor]
            public class MyProcessor : IProcessor
            {
                public override IRow Process(IRow input, IUpdatableRow output)
                {
                    output.Set(0, input.Get<string>(0));
                    output.Set(0, input.Get<string>(0));
                    return output.AsReadOnly();
                }
            }
        }
4. <span data-ttu-id="b6257-128">Clique em Olá **criar** menu e clique **compilar solução** toocreate Olá dll.</span><span class="sxs-lookup"><span data-stu-id="b6257-128">Click hello **Build** menu, and then click **Build Solution** toocreate hello dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="b6257-129">Registrar assemblies</span><span class="sxs-lookup"><span data-stu-id="b6257-129">Register assemblies</span></span>

<span data-ttu-id="b6257-130">Veja [Usar o catálogo do Data Lake Analytics (U-SQL)](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="b6257-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-hello-assemblies"></a><span data-ttu-id="b6257-131">Usar assemblies Olá</span><span class="sxs-lookup"><span data-stu-id="b6257-131">Use hello assemblies</span></span>

<span data-ttu-id="b6257-132">Consulte [usar hello Azure Data Lake Tools para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="b6257-132">See [Use hello Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b6257-133">Consulte também</span><span class="sxs-lookup"><span data-stu-id="b6257-133">See also</span></span>
* [<span data-ttu-id="b6257-134">Introdução à Análise Data Lake usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6257-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="b6257-135">Introdução à análise Data Lake usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b6257-135">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="b6257-136">Usar as Ferramentas do Data Lake para Visual Studio para desenvolver aplicativos do U-SQL</span><span class="sxs-lookup"><span data-stu-id="b6257-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="b6257-137">Usar o catálogo do Data Lake Analytics (U-SQL)</span><span class="sxs-lookup"><span data-stu-id="b6257-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="b6257-138">Use hello Azure Data Lake Tools para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b6257-138">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
