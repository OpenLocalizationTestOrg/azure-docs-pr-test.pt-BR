---
title: "um serviço de Web do aprendizado de máquina do Excel de aaaConsume | Microsoft Docs"
description: "Consumir um serviço Web de Azure Machine Learning do Excel"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="a2b7d-103">Consumindo um Serviço Web de Azure Machine Learning do Excel</span><span class="sxs-lookup"><span data-stu-id="a2b7d-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="a2b7d-104">O estúdio de aprendizado de máquina do Azure torna fácil toocall os serviços da web diretamente do Excel sem Olá necessidade toowrite qualquer código.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-104">Azure Machine Learning Studio makes it easy toocall web services directly from Excel without hello need toowrite any code.</span></span>

<span data-ttu-id="a2b7d-105">Se você estiver usando o Excel 2013 (ou posterior) ou o Excel Online, recomendamos que você use Olá Excel [suplemento Excel](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="a2b7d-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use hello Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="a2b7d-106">Etapas</span><span class="sxs-lookup"><span data-stu-id="a2b7d-106">Steps</span></span>
<span data-ttu-id="a2b7d-107">Publicar um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-107">Publish a web service.</span></span> <span data-ttu-id="a2b7d-108">[Esta página](machine-learning-walkthrough-5-publish-web-service.md) explica como toodo-lo.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how toodo it.</span></span> <span data-ttu-id="a2b7d-109">Atualmente o recurso de pasta de trabalho do Excel Olá só tem suporte para serviços de solicitação/resposta que têm uma única saída (ou seja, uma pontuação rótulo único).</span><span class="sxs-lookup"><span data-stu-id="a2b7d-109">Currently hello Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="a2b7d-110">Uma vez que um serviço web, clique em Olá **serviços WEB** seção esquerda de saudação do studio hello e selecione Olá web serviço tooconsume do Excel.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-110">Once you have a web service, click on hello **WEB SERVICES** section on hello left of hello studio, and then select hello web service tooconsume from Excel.</span></span>

<span data-ttu-id="a2b7d-111">**Serviço Web Clássico**</span><span class="sxs-lookup"><span data-stu-id="a2b7d-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="a2b7d-112">Em Olá **painel** guia para o serviço web de saudação é uma linha para Olá **solicitação/resposta** serviço.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-112">On hello **DASHBOARD** tab for hello web service is a row for hello **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="a2b7d-113">Se esse serviço tinha uma única saída, você deve ver Olá **baixar pasta de trabalho do Excel** link nessa linha.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-113">If this service had a single output, you should see hello **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="a2b7d-114">Clique em **Baixar Pasta de Trabalho do Excel**.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="a2b7d-115">**Novo serviço Web**</span><span class="sxs-lookup"><span data-stu-id="a2b7d-115">**New Web Service**</span></span>

1. <span data-ttu-id="a2b7d-116">No portal de serviço de Web de aprendizado de máquina do Azure hello, selecione **consumir**.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-116">In hello Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="a2b7d-117">Na página de consumir hello, em Olá **opções de consumo do serviço da Web** seção, clique no ícone do Excel hello.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-117">On hello Consume page, in hello **Web service consumption options** section, click hello Excel icon.</span></span>

<span data-ttu-id="a2b7d-118">**Usando a pasta de trabalho Olá**</span><span class="sxs-lookup"><span data-stu-id="a2b7d-118">**Using hello workbook**</span></span>

1. <span data-ttu-id="a2b7d-119">Pasta de trabalho aberta hello.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-119">Open hello workbook.</span></span>
2. <span data-ttu-id="a2b7d-120">É exibido um aviso de segurança; Clique em Olá **habilitar edição** botão.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-120">A Security Warning appears; click on hello **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="a2b7d-121">Será exibido um Aviso de Segurança.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-121">A Security Warning appears.</span></span> <span data-ttu-id="a2b7d-122">Clique em Olá **Habilitar conteúdo** botão toorun macros na planilha.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-122">Click on hello **Enable Content** button toorun macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="a2b7d-123">Depois que as macros estiverem habilitadas, uma tabela será gerada.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="a2b7d-124">Colunas em azul tem como entrada no hello RRS web serviço necessário, ou **parâmetros**.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-124">Columns in blue are required as input into hello RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="a2b7d-125">Observe a saída Olá Olá serviço RRS, **valores previstos** em verde.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-125">Note hello output of hello RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="a2b7d-126">Quando todas as colunas para uma determinada linha são preenchidas, pasta de trabalho do hello automaticamente chama Olá API de pontuação e exibe o saudação resultados classificada.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-126">When all columns for a given row are filled, hello workbook automatically calls hello scoring API, and displays hello scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="a2b7d-127">tooscore mais de uma linha, preenchimento Olá segunda linha com dados e hello prevista valores são gerados.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-127">tooscore more than one row, fill hello second row with data and hello predicted values are produced.</span></span> <span data-ttu-id="a2b7d-128">Você pode até mesmo colar várias linhas ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="a2b7d-129">Você pode usar qualquer um dos recursos do Excel hello (gráficos, mapa de energia, condicional, formatação, etc.) com hello previsto valores toohelp visualizar dados saudação.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-129">You can use any of hello Excel features (graphs, power map, conditional formatting, etc.) with hello predicted values toohelp visualize hello data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="a2b7d-130">Compartilhar sua pasta de trabalho</span><span class="sxs-lookup"><span data-stu-id="a2b7d-130">Sharing your workbook</span></span>
<span data-ttu-id="a2b7d-131">Para Olá macros toowork, sua chave de API deve ser parte da planilha de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-131">For hello macros toowork, your API Key must be part of hello spreadsheet.</span></span> <span data-ttu-id="a2b7d-132">Isso significa que você deve compartilhar pasta de trabalho de saudação apenas com entidades/pessoas que confiáveis.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-132">That means that you should share hello workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="a2b7d-133">Atualizações automáticas</span><span class="sxs-lookup"><span data-stu-id="a2b7d-133">Automatic updates</span></span>
<span data-ttu-id="a2b7d-134">É feita uma chamada RRS nessas duas situações:</span><span class="sxs-lookup"><span data-stu-id="a2b7d-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="a2b7d-135">Olá a primeira vez que uma linha tem o conteúdo em todas as suas **parâmetros**</span><span class="sxs-lookup"><span data-stu-id="a2b7d-135">hello first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="a2b7d-136">Sempre que qualquer Olá **parâmetros** alterações em uma linha que tenha todos os seus **parâmetros** inserido.</span><span class="sxs-lookup"><span data-stu-id="a2b7d-136">Any time any of hello **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
