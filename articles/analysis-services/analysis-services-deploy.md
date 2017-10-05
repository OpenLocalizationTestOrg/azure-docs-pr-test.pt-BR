---
title: Implantar no Azure Analysis Services usando o SSDT | Microsoft Docs
description: Saiba como implantar um modelo de tabela em um servidor do Azure Analysis Services usando SSDT.
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
ms.openlocfilehash: e9a3aedfb6e55696e1525e226fada1062fd5eda8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="9c3b4-103">Implantar um modelo a partir do SSDT</span><span class="sxs-lookup"><span data-stu-id="9c3b4-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="9c3b4-104">Depois de criar um servidor em sua assinatura do Azure, você estará pronto para implantar nele um banco de dados de modelo de tabela.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-104">Once you've created a server in your Azure subscription, you're ready to deploy a tabular model database to it.</span></span> <span data-ttu-id="9c3b4-105">Você pode usar o SSDT (SQL Server Data Tools) para criar e implantar um projeto de modelo de tabela no qual você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-105">You can use SQL Server Data Tools (SSDT) to build and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9c3b4-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9c3b4-106">Prerequisites</span></span>
<span data-ttu-id="9c3b4-107">Para começar, você precisa do seguinte:</span><span class="sxs-lookup"><span data-stu-id="9c3b4-107">To get started, you need:</span></span>

* <span data-ttu-id="9c3b4-108">**Servidor do Analysis Services** no Azure.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="9c3b4-109">Para saber mais, veja [Criar um servidor do Azure Analysis Services](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="9c3b4-109">To learn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="9c3b4-110">**Projeto de modelo de tabela** no SSDT ou em um modelo de tabela existente no nível de compatibilidade 1200 ou superior.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-110">**Tabular model project** in SSDT or an existing tabular model at the 1200 or higher compatibility level.</span></span> <span data-ttu-id="9c3b4-111">Nunca criou um?</span><span class="sxs-lookup"><span data-stu-id="9c3b4-111">Never created one?</span></span> <span data-ttu-id="9c3b4-112">Experimente o [tutorial de modelagem de tabela de vendas na Internet do Adventure Works](https://msdn.microsoft.com/library/hh231691.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c3b4-112">Try the [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="9c3b4-113">**Gateway local** - se uma ou mais fontes de dados estiverem no local na rede de sua organização, você precisará instalar um [Gateway de dados local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="9c3b4-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need to install an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="9c3b4-114">O gateway é necessário para que seu servidor na nuvem conecte-se às suas fontes de dados locais, a fim de processar e atualizar os dados no modelo.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-114">The gateway is necessary for your server in the cloud connect to your on-premises data sources to process and refresh data in the model.</span></span>

> [!TIP]
> <span data-ttu-id="9c3b4-115">Antes de implantar, verifique se que você pode processar os dados nas tabelas.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-115">Before you deploy, make sure you can process the data in your tables.</span></span> <span data-ttu-id="9c3b4-116">No SSDT, clique em **Modelo** > **Processo** > **Processar Tudo**.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="9c3b4-117">Se houver falha no processamento, você não poderá implantar com êxito.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="to-deploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="9c3b4-118">Para implantar um modelo de tabela do SSDT</span><span class="sxs-lookup"><span data-stu-id="9c3b4-118">To deploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="9c3b4-119">Antes de implantar, você precisa obter o nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-119">Before you deploy, you need to get the server name.</span></span> <span data-ttu-id="9c3b4-120">No **Portal do Azure** > servidor > **Visão geral** > **Nome do servidor**, copie o nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-120">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Obter o nome do servidor no Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="9c3b4-122">No SSDT > **Gerenciador de Solução**, clique com o botão direito do mouse no projeto > **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-122">In SSDT > **Solution Explorer**, right-click the project > **Properties**.</span></span> <span data-ttu-id="9c3b4-123">Em seguida, em **Implantação** > **Servidor**, cole o nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-123">Then in **Deployment** > **Server** paste the server name.</span></span>   
   
    ![Colar o nome do servidor na propriedade do servidor de implantação](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="9c3b4-125">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Propriedades** e clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="9c3b4-126">Talvez você receba uma solicitação para entrar no Azure.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-126">You may be prompted to sign in to Azure.</span></span>
   
    ![Implantar no servidor](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="9c3b4-128">O status da implantação aparecerá na janela Saída e em Implantar.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-128">Deployment status appears in both the Output window and in Deploy.</span></span>
   
    ![Status da Implantação](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="9c3b4-130">Isso é tudo!</span><span class="sxs-lookup"><span data-stu-id="9c3b4-130">That's all there is to it!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="9c3b4-131">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="9c3b4-131">Troubleshooting</span></span>
<span data-ttu-id="9c3b4-132">Se a implantação falhar durante a implantação dos metadados, provavelmente o SSDT não conseguiu se conectar ao servidor.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect to your server.</span></span> <span data-ttu-id="9c3b4-133">Verifique se você consegue se conectar ao servidor usando o SSMS.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-133">Make sure you can connect to your server using SSMS.</span></span> <span data-ttu-id="9c3b4-134">Em seguida, verifique se a propriedade do Servidor de Implantação do projeto está correta.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-134">Then make sure the Deployment Server property for the project is correct.</span></span>

<span data-ttu-id="9c3b4-135">Se a implantação falhar em uma tabela, provavelmente o servidor não conseguiu se conectar a uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-135">If deployment fails on a table, it's likely because your server couldn't connect to a data source.</span></span> <span data-ttu-id="9c3b4-136">Se a sua fonte de dados for local, na rede da sua organização, instale um [Gateway de dados local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="9c3b4-136">If your data source is on-premises in your organization's network, be sure to install an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c3b4-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9c3b4-137">Next steps</span></span>
<span data-ttu-id="9c3b4-138">Agora que seu modelo de tabela foi implantado em seu servidor, você está pronto para se conectar a ele.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-138">Now that you have your tabular model deployed to your server, you're ready to connect to it.</span></span> <span data-ttu-id="9c3b4-139">Você pode [conectar-se a ele com SSMS](analysis-services-manage.md) para gerenciá-lo.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-139">You can [connect to it with SSMS](analysis-services-manage.md) to manage it.</span></span> <span data-ttu-id="9c3b4-140">E, você pode [conectar-se a ele usando uma ferramenta de cliente](analysis-services-connect.md) como o Power BI, o Power BI Desktop ou o Excel, e começar a criar relatórios.</span><span class="sxs-lookup"><span data-stu-id="9c3b4-140">And, you can [connect to it using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

