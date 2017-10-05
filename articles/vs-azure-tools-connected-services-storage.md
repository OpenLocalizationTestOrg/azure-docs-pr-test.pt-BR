---
title: "Adicionar Armazenamento do Azure usando serviços conectados no Visual Studio | Microsoft Docs"
description: "Adicionar Armazenamento do Azure ao seu aplicativo usando a caixa de diálogo Adicionar Serviços Conectados do Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 35638083cd75e1b751d00a9c8163a3bc7480f0cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="128b2-103">Adicionando armazenamento do Azure usando os serviços conectados do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="128b2-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="128b2-104">Com o Visual Studio, você pode conectar qualquer um dos seguintes Armazenamentos do Azure usando a caixa de diálogo **Adicionar Serviços Conectados**:</span><span class="sxs-lookup"><span data-stu-id="128b2-104">With Visual Studio, you can connect any of the following to Azure Storage by using the **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="128b2-105">Serviço de nuvem do C#</span><span class="sxs-lookup"><span data-stu-id="128b2-105">C# cloud service</span></span>
- <span data-ttu-id="128b2-106">Serviço móvel de back-end .NET</span><span class="sxs-lookup"><span data-stu-id="128b2-106">.NET backend mobile service</span></span>
- <span data-ttu-id="128b2-107">Site ou serviço ASP.NET</span><span class="sxs-lookup"><span data-stu-id="128b2-107">ASP.NET website or service</span></span>
- <span data-ttu-id="128b2-108">Principais serviços ASP.NET</span><span class="sxs-lookup"><span data-stu-id="128b2-108">ASP.NET Core service</span></span>
- <span data-ttu-id="128b2-109">Serviço do Trabalho Web do Azure</span><span class="sxs-lookup"><span data-stu-id="128b2-109">Azure WebJob service</span></span> 

<span data-ttu-id="128b2-110">A funcionalidade do serviço conectado adiciona todas as referências necessárias e o código de conexão ao seu projeto, bem como modifica os arquivos de configuração adequadamente.</span><span class="sxs-lookup"><span data-stu-id="128b2-110">The connected service functionality adds all the needed references and connection code to your project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="128b2-111">Após a conclusão, a caixa de diálogo **Adicionar Serviços Conectados** exibe automaticamente a documentação detalhando as etapas necessárias para começar a trabalhar com armazenamento de blobs, filas e tabelas.</span><span class="sxs-lookup"><span data-stu-id="128b2-111">After completion, the **Add Connected Services** dialog automatically displays documentation detailing the steps required to start working with blob storage, queues, and tables.</span></span>

## <a name="connect-to-azure-storage-using-the-connected-services-dialog"></a><span data-ttu-id="128b2-112">Conectar-se ao Armazenamento do Azure usando a caixa de diálogo Serviços Conectados</span><span class="sxs-lookup"><span data-stu-id="128b2-112">Connect to Azure Storage using the Connected Services dialog</span></span>
1. <span data-ttu-id="128b2-113">Abra o projeto no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="128b2-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="128b2-114">No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó **Serviços Conectados** e, no menu de contexto, selecione **Adicionar Serviço Conectado**.</span><span class="sxs-lookup"><span data-stu-id="128b2-114">In **Solution Explorer**, right-click the **Connected Services** node, and, from the context menu, and select **Add Connected Service**.</span></span>
   
    ![Adicionar serviço conectado do Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="128b2-116">Na página **Serviços Conectados**, selecione **Armazenamento em Nuvem com o Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="128b2-116">In the **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Adicionar Armazenamento do Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="128b2-118">Na caixa de diálogo **Armazenamento do Azure**, selecione uma conta de armazenamento existente e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="128b2-118">In the **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="128b2-119">Se você precisar criar uma conta de armazenamento, passe para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="128b2-119">If you need to create a storage account, go to the next step.</span></span> <span data-ttu-id="128b2-120">Caso contrário, pule para a etapa 6.</span><span class="sxs-lookup"><span data-stu-id="128b2-120">Otherwise, skip to step 6.</span></span>
    
    ![Adicionar conta de armazenamento existente ao projeto](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="128b2-122">Para criar uma conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="128b2-122">To create a storage account:</span></span> 
   
   1. <span data-ttu-id="128b2-123">Selecione **Criar uma Nova Conta de Armazenamento** na parte inferior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="128b2-123">Select **Create a New Storage Account** at the bottom of the dialog.</span></span>

   1. <span data-ttu-id="128b2-124">Preencha o diálogo **Criar Conta de Armazenamento** e selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="128b2-124">Fill out the **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![Nova conta de armazenamento do Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="128b2-126">Quando a caixa de diálogo **Armazenamento do Azure** for exibida, a nova conta de armazenamento aparecerá na lista.</span><span class="sxs-lookup"><span data-stu-id="128b2-126">When the **Azure Storage** dialog is displayed, the new storage account appears in the list.</span></span> <span data-ttu-id="128b2-127">Selecione a nova conta de armazenamento na lista e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="128b2-127">Select the new storage account in the list, and select **Add**.</span></span>

1. <span data-ttu-id="128b2-128">O serviço conectado de armazenamento aparece sob o nó **Referências de Serviço** do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="128b2-128">The storage connected service appears under the **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="128b2-129">Como o projeto é modificado</span><span class="sxs-lookup"><span data-stu-id="128b2-129">How your project is modified</span></span>
<span data-ttu-id="128b2-130">Quando você acaba de fazer suas escolhas na caixa de diálogo, o Visual Studio adiciona referências e modifica determinados arquivos de configuração.</span><span class="sxs-lookup"><span data-stu-id="128b2-130">When you finish the dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="128b2-131">As alterações específicas dependem do tipo de projeto:</span><span class="sxs-lookup"><span data-stu-id="128b2-131">The specific changes depend on the project type:</span></span> 

- <span data-ttu-id="128b2-132">Projeto ASP.NET — [O que aconteceu — projetos ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="128b2-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="128b2-133">Projeto de Núcleo ASP.NET — [O que aconteceu — projetos ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="128b2-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="128b2-134">Projeto de serviço de nuvem (funções Web e funções de trabalho) — [O que aconteceu — projetos Serviço de Nuvem](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="128b2-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="128b2-135">Projetos de Trabalho Web — [O que aconteceu — projetos de Trabalho Web](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="128b2-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="128b2-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="128b2-136">Next steps</span></span>
- [<span data-ttu-id="128b2-137">Fórum do MSDN: Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="128b2-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="128b2-138">Blog da equipe do Armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="128b2-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="128b2-139">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="128b2-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
