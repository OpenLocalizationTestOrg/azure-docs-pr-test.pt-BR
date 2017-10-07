---
title: aaaDeploy tooAzure Analysis Services usando o SSDT | Microsoft Docs
description: Saiba como toodeploy tooan um modelo de tabela do Azure Analysis Services server usando o SSDT.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="3954c-103">Implantar um modelo a partir do SSDT</span><span class="sxs-lookup"><span data-stu-id="3954c-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="3954c-104">Depois de criar um servidor na sua assinatura do Azure, você está pronto toodeploy um tooit de banco de dados de modelo de tabela.</span><span class="sxs-lookup"><span data-stu-id="3954c-104">Once you've created a server in your Azure subscription, you're ready toodeploy a tabular model database tooit.</span></span> <span data-ttu-id="3954c-105">Você pode usar o SQL Server Data Tools (SSDT) toobuild e implantar um projeto de modelo de tabela que você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="3954c-105">You can use SQL Server Data Tools (SSDT) toobuild and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3954c-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3954c-106">Prerequisites</span></span>
<span data-ttu-id="3954c-107">tooget iniciado, você precisa:</span><span class="sxs-lookup"><span data-stu-id="3954c-107">tooget started, you need:</span></span>

* <span data-ttu-id="3954c-108">**Servidor do Analysis Services** no Azure.</span><span class="sxs-lookup"><span data-stu-id="3954c-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="3954c-109">mais, consulte toolearn [criar um servidor do Azure Analysis Services](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="3954c-109">toolearn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="3954c-110">**Projeto de modelo tabular** no SSDT ou um modelo tabular existente em Olá 1200 ou maior nível de compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="3954c-110">**Tabular model project** in SSDT or an existing tabular model at hello 1200 or higher compatibility level.</span></span> <span data-ttu-id="3954c-111">Nunca criou um?</span><span class="sxs-lookup"><span data-stu-id="3954c-111">Never created one?</span></span> <span data-ttu-id="3954c-112">Tente Olá [tutorial de modelagem de tabela de vendas do Adventure Works Internet](https://msdn.microsoft.com/library/hh231691.aspx).</span><span class="sxs-lookup"><span data-stu-id="3954c-112">Try hello [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="3954c-113">**Gateway local** -se uma ou mais fontes de dados local na rede da sua organização, você precisa tooinstall um [gateway de dados no local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="3954c-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="3954c-114">gateway de saudação é necessário para o servidor na nuvem Olá conectar tooyour local fontes tooprocess e a atualização de dados no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3954c-114">hello gateway is necessary for your server in hello cloud connect tooyour on-premises data sources tooprocess and refresh data in hello model.</span></span>

> [!TIP]
> <span data-ttu-id="3954c-115">Antes de implantar, verifique se que você pode processar dados saudação nas tabelas.</span><span class="sxs-lookup"><span data-stu-id="3954c-115">Before you deploy, make sure you can process hello data in your tables.</span></span> <span data-ttu-id="3954c-116">No SSDT, clique em **Modelo** > **Processo** > **Processar Tudo**.</span><span class="sxs-lookup"><span data-stu-id="3954c-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="3954c-117">Se houver falha no processamento, você não poderá implantar com êxito.</span><span class="sxs-lookup"><span data-stu-id="3954c-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="3954c-118">toodeploy um modelo de tabela do SSDT</span><span class="sxs-lookup"><span data-stu-id="3954c-118">toodeploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="3954c-119">Antes de implantar, é necessário o nome do servidor de saudação tooget.</span><span class="sxs-lookup"><span data-stu-id="3954c-119">Before you deploy, you need tooget hello server name.</span></span> <span data-ttu-id="3954c-120">Em **portal do Azure** > servidor > **visão geral** > **nome do servidor**, nome do servidor de saudação de cópia.</span><span class="sxs-lookup"><span data-stu-id="3954c-120">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Obter o nome do servidor no Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="3954c-122">No SSDT > **Solution Explorer**, projeto de saudação do botão direito do mouse > **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="3954c-122">In SSDT > **Solution Explorer**, right-click hello project > **Properties**.</span></span> <span data-ttu-id="3954c-123">Em seguida, em **implantação** > **Server** colar o nome do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="3954c-123">Then in **Deployment** > **Server** paste hello server name.</span></span>   
   
    ![Colar o nome do servidor na propriedade do servidor de implantação](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="3954c-125">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Propriedades** e clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="3954c-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="3954c-126">Você pode ser solicitado toosign em tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3954c-126">You may be prompted toosign in tooAzure.</span></span>
   
    ![Implantar tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="3954c-128">Status da implantação é exibida na janela Saída hello e na implantação.</span><span class="sxs-lookup"><span data-stu-id="3954c-128">Deployment status appears in both hello Output window and in Deploy.</span></span>
   
    ![Status da Implantação](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="3954c-130">Isso é tudo que há tooit!</span><span class="sxs-lookup"><span data-stu-id="3954c-130">That's all there is tooit!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="3954c-131">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="3954c-131">Troubleshooting</span></span>
<span data-ttu-id="3954c-132">Se a implantação falhar durante a implantação de metadados, é provável porque SSDT não foi possível conectar o servidor tooyour.</span><span class="sxs-lookup"><span data-stu-id="3954c-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect tooyour server.</span></span> <span data-ttu-id="3954c-133">Verifique se que você pode conectar o servidor tooyour usando o SSMS.</span><span class="sxs-lookup"><span data-stu-id="3954c-133">Make sure you can connect tooyour server using SSMS.</span></span> <span data-ttu-id="3954c-134">Em seguida, certifique-se de Olá propriedade de servidor de implantação de projeto hello está correto.</span><span class="sxs-lookup"><span data-stu-id="3954c-134">Then make sure hello Deployment Server property for hello project is correct.</span></span>

<span data-ttu-id="3954c-135">Se a implantação falhar em uma tabela, é provável porque o servidor não pôde se conectar à fonte de dados tooa.</span><span class="sxs-lookup"><span data-stu-id="3954c-135">If deployment fails on a table, it's likely because your server couldn't connect tooa data source.</span></span> <span data-ttu-id="3954c-136">Se sua fonte de dados é o local na rede da sua organização, ser tooinstall se um [gateway de dados no local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="3954c-136">If your data source is on-premises in your organization's network, be sure tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3954c-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3954c-137">Next steps</span></span>
<span data-ttu-id="3954c-138">Agora que você tem o servidor de tooyour implantado do modelo de tabela, você está pronto tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="3954c-138">Now that you have your tabular model deployed tooyour server, you're ready tooconnect tooit.</span></span> <span data-ttu-id="3954c-139">Você pode [conectar tooit com SSMS](analysis-services-manage.md) toomanage-lo.</span><span class="sxs-lookup"><span data-stu-id="3954c-139">You can [connect tooit with SSMS](analysis-services-manage.md) toomanage it.</span></span> <span data-ttu-id="3954c-140">E, você pode [tooit usando uma ferramenta de cliente de conectar](analysis-services-connect.md) como o Power BI, o Power BI Desktop, ou o Excel e começar a criar relatórios.</span><span class="sxs-lookup"><span data-stu-id="3954c-140">And, you can [connect tooit using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

