---
title: Desenvolver assemblies do U-SQL para trabalhos do Azure Data Lake Analytics | Microsoft Docs
description: 'Saiba como desenvolver assemblies para serem usados e reutilizados em trabalhos do Data Lake Analytics. '
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
ms.openlocfilehash: c49f80f8dcd330d7f46726241e7178351b9cc28f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="66043-103">Desenvolver assemblies do U-SQL para trabalhos do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="66043-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="66043-104">Saiba como transformar code-behind em assemblies a serem usados e reutilizados em trabalhos do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="66043-104">Learn how to turn code-behind into assemblies to be used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="66043-105">O U-SQL torna fácil a tarefa de adicionar seu próprio código personalizado em linguagens .Net, como C#, VB.Net ou F#.</span><span class="sxs-lookup"><span data-stu-id="66043-105">U-SQL makes it easy to add your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="66043-106">Você ainda pode implantar seu próprio tempo de execução para dar suporte a outras linguagens.</span><span class="sxs-lookup"><span data-stu-id="66043-106">You can even deploy your own runtime to support other languages.</span></span>

<span data-ttu-id="66043-107">A maneira mais fácil de usar código personalizado é por meio dos recursos code-behind das Ferramentas do Data Lake para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66043-107">The easiest way to use custom code is to use the Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="66043-108">Para obter mais informações, consulte o [Tutorial: desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="66043-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="66043-109">Há algumas desvantagens em usar code-behind:</span><span class="sxs-lookup"><span data-stu-id="66043-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="66043-110">O código-fonte é carregado em cada envio de script.</span><span class="sxs-lookup"><span data-stu-id="66043-110">The source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="66043-111">O code-behind não pode ser compartilhado com outros trabalhos.</span><span class="sxs-lookup"><span data-stu-id="66043-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="66043-112">Para lidar com essas desvantagens, você pode transformar o code-behind em assemblies e registrá-los no catálogo do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="66043-112">To address these drawbacks, you can turn code-behind into assemblies, and register the assemblies to the Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66043-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="66043-113">Prerequisites</span></span>
* <span data-ttu-id="66043-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 atualização 4 ou Visual Studio 2012 com Visual C++ instalado</span><span class="sxs-lookup"><span data-stu-id="66043-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="66043-115">SDK do Microsoft Azure para .NET versão 2.5 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="66043-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="66043-116">Instale-o usando o Web Platform Installer ou Instalador do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="66043-116">Install it using the Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="66043-117">Uma conta da Análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="66043-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="66043-118">Confira [Introdução ao Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="66043-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="66043-119">Acompanhe o tutorial [Introdução ao U-SQL Studio da Análise Azure Data Lake](data-lake-analytics-u-sql-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="66043-119">Go through the [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="66043-120">Conecte-se ao Azure.</span><span class="sxs-lookup"><span data-stu-id="66043-120">Connect to Azure.</span></span>
* <span data-ttu-id="66043-121">Carregar os dados de origem, consulte [Introdução ao U-SQL Studio do Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="66043-121">Upload the source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="66043-122">Desenvolver assemblies para U-SQL</span><span class="sxs-lookup"><span data-stu-id="66043-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="66043-123">**Para criar e enviar um trabalho do U-SQL**</span><span class="sxs-lookup"><span data-stu-id="66043-123">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="66043-124">No menu **Arquivo**, clique em **Novo** e em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="66043-124">From the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="66043-125">Expanda **Instalados**, **Modelos**, **Azure Data Lake**, **U-SQL(ADLA)**, selecione o modelo **Biblioteca de Classes (para aplicativos U-SQL)** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="66043-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select the **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="66043-126">Escreva seu código em Class1.cs.</span><span class="sxs-lookup"><span data-stu-id="66043-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="66043-127">Veja a seguir um exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="66043-127">The following is a code sample.</span></span>

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
4. <span data-ttu-id="66043-128">Clique no menu **Criar** e em **Compilar Solução** para criar a dll.</span><span class="sxs-lookup"><span data-stu-id="66043-128">Click the **Build** menu, and then click **Build Solution** to create the dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="66043-129">Registrar assemblies</span><span class="sxs-lookup"><span data-stu-id="66043-129">Register assemblies</span></span>

<span data-ttu-id="66043-130">Veja [Usar o catálogo do Data Lake Analytics (U-SQL)](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="66043-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-the-assemblies"></a><span data-ttu-id="66043-131">Usar os assemblies</span><span class="sxs-lookup"><span data-stu-id="66043-131">Use the assemblies</span></span>

<span data-ttu-id="66043-132">Veja [Usar as Ferramentas do Azure Data Lake para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="66043-132">See [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="66043-133">Consulte também</span><span class="sxs-lookup"><span data-stu-id="66043-133">See also</span></span>
* [<span data-ttu-id="66043-134">Introdução à Análise Data Lake usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="66043-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="66043-135">Introdução à Análise Data Lake usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="66043-135">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="66043-136">Usar as Ferramentas do Data Lake para Visual Studio para desenvolver aplicativos do U-SQL</span><span class="sxs-lookup"><span data-stu-id="66043-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="66043-137">Usar o catálogo do Data Lake Analytics (U-SQL)</span><span class="sxs-lookup"><span data-stu-id="66043-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="66043-138">Usar as Ferramentas do Azure Data Lake para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="66043-138">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)