---
title: "Lição 13 do tutorial do Azure Analysis Services: implantar | Microsoft Docs"
description: Descreve como implantar o projeto do tutorial do Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/17/2017
ms.author: owend
ms.openlocfilehash: 70dbf5786262f75199270aa8009e03b9b48b8559
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="56661-103">Lição 13: implantar</span><span class="sxs-lookup"><span data-stu-id="56661-103">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="56661-104">Nesta lição, você configura as propriedades de implantação especificando um servidor do Azure Analysis Services para implantar e um nome para o modelo.</span><span class="sxs-lookup"><span data-stu-id="56661-104">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server to deploy to and a name for the model.</span></span> <span data-ttu-id="56661-105">Em seguida, você implanta o modelo para essa instância.</span><span class="sxs-lookup"><span data-stu-id="56661-105">You then deploy the model to that instance.</span></span> <span data-ttu-id="56661-106">Após o modelo ser implantado, os usuários podem se conectar a ele usando um aplicativo cliente de relatório.</span><span class="sxs-lookup"><span data-stu-id="56661-106">After your model is deployed, users can connect to it by using a reporting client application.</span></span> <span data-ttu-id="56661-107">Para saber mais, confira [Implantar no Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span><span class="sxs-lookup"><span data-stu-id="56661-107">To learn more, see [Deploy to Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="56661-108">Tempo estimado para conclusão desta lição: **5 minutos**</span><span class="sxs-lookup"><span data-stu-id="56661-108">Estimated time to complete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="56661-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="56661-109">Prerequisites</span></span>  
<span data-ttu-id="56661-110">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="56661-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="56661-111">Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 12: analisar no Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="56661-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="56661-112">Você deve ter [permissões de Administrador](../analysis-services-server-admins.md) no servidor remoto do Analysis Services para poder implantar nele.</span><span class="sxs-lookup"><span data-stu-id="56661-112">You must have [Administrator permissions](../analysis-services-server-admins.md) on the remote Analysis Services server in-order to deploy to it.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="56661-113">Se você instalou o banco de dados de exemplo AdventureWorksDW2014 em um SQL Server local e está implantando seu modelo em um servidor do Azure Analysis Services, um [Gateway de dados local](../analysis-services-gateway.md) é necessário.</span><span class="sxs-lookup"><span data-stu-id="56661-113">If you installed the AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model to an Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-the-model"></a><span data-ttu-id="56661-114">Implantar o modelo</span><span class="sxs-lookup"><span data-stu-id="56661-114">Deploy the model</span></span>  
  
#### <a name="to-configure-deployment-properties"></a><span data-ttu-id="56661-115">Para configurar propriedades de implantação</span><span class="sxs-lookup"><span data-stu-id="56661-115">To configure deployment properties</span></span>  

  
1.  <span data-ttu-id="56661-116">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **Vendas pela Internet da AW** e depois clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="56661-116">In **Solution Explorer**, right-click the **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="56661-117">Na caixa de diálogo **Páginas de Propriedades de Vendas pela Internet da AW**, no **Servidor de Implantação**, na propriedade **Servidor**, digite o servidor completo.</span><span class="sxs-lookup"><span data-stu-id="56661-117">In the **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in the **Server** property, enter the full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="56661-119">Na propriedade **Banco de Dados**, digite **Vendas pela Internet da Adventure Works**.</span><span class="sxs-lookup"><span data-stu-id="56661-119">In the **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="56661-120">Na propriedade **Nome do Modelo**, digite **Modelo de Vendas pela Internet da Adventure Works**.</span><span class="sxs-lookup"><span data-stu-id="56661-120">In the **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="56661-121">Verifique suas seleções e então clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="56661-121">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a><span data-ttu-id="56661-122">Para implantar as Vendas pela Internet da Adventure Works</span><span class="sxs-lookup"><span data-stu-id="56661-122">To deploy the Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="56661-123">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **Vendas pela Internet da AW** > **Compilar**.</span><span class="sxs-lookup"><span data-stu-id="56661-123">In **Solution Explorer**, right-click the **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="56661-124">Clique com o botão direito do mouse no projeto **Vendas pela Internet da AW** > **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="56661-124">Right-click the **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="56661-125">Ao implantar para os Azure Analysis Services, pode ser solicitado que você insira sua conta.</span><span class="sxs-lookup"><span data-stu-id="56661-125">When deploying to Azure Analysis Services, you may be prompted to enter your account.</span></span> <span data-ttu-id="56661-126">Insira sua conta e senha organizacionais, por exemplo, nancy@adventureworks.com. Esta conta deve constar na lista Admins no servidor.</span><span class="sxs-lookup"><span data-stu-id="56661-126">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on the server.</span></span>
  
    <span data-ttu-id="56661-127">A caixa de diálogo Implantar aparece e exibe o status da implantação dos metadados e cada tabela incluída no modelo.</span><span class="sxs-lookup"><span data-stu-id="56661-127">The Deploy dialog box appears and displays the deployment status of the metadata and each table included in the model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="56661-129">Quando a implantação for concluída com êxito, vá em frente e clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="56661-129">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="56661-130">Conclusão</span><span class="sxs-lookup"><span data-stu-id="56661-130">Conclusion</span></span>  
<span data-ttu-id="56661-131">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="56661-131">Congratulations!</span></span> <span data-ttu-id="56661-132">Você terminou de criar e implantar seu primeiro modelo tabular do Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="56661-132">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="56661-133">Este tutorial ajudou a orientá-lo a concluir as tarefas mais comuns na criação de um modelo tabular.</span><span class="sxs-lookup"><span data-stu-id="56661-133">This tutorial has helped guide you through completing the most common tasks in creating a tabular model.</span></span> <span data-ttu-id="56661-134">Agora que seu modelo de vendas de Internet da Adventure Works está implantado, você pode usar o SQL Server Management Studio para gerenciar o modelo; crie scripts de processo e um plano de backup.</span><span class="sxs-lookup"><span data-stu-id="56661-134">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio to manage the model; create process scripts and a backup plan.</span></span> <span data-ttu-id="56661-135">Os usuários agora também podem se conectar ao modelo usando um aplicativo cliente de relatório, como o Microsoft Excel ou o Power BI.</span><span class="sxs-lookup"><span data-stu-id="56661-135">Users can also now connect to the model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="56661-137">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="56661-137">What's next?</span></span>
<span data-ttu-id="56661-138">[Conecte-se com o Power BI Desktop](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="56661-138">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="56661-139">[Lição suplementar - Segurança dinâmica](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="56661-139">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="56661-140">[Lição suplementar - Linhas de detalhes](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="56661-140">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="56661-141">Lição Suplementar – hierarquias desbalanceadas</span><span class="sxs-lookup"><span data-stu-id="56661-141">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
