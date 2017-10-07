---
title: "aaaAdd de armazenamento do Azure usando os serviços conectados no Visual Studio | Microsoft Docs"
description: "Adicionar o aplicativo de tooyour de armazenamento do Azure usando a caixa de diálogo do Visual Studio adicionar conectado serviços Olá"
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
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="53ae3-103">Adicionando armazenamento do Azure usando os serviços conectados do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="53ae3-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="53ae3-104">Com o Visual Studio, você pode conectar qualquer Olá tooAzure armazenamento a seguir usando Olá **adicionar serviços conectados** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="53ae3-104">With Visual Studio, you can connect any of hello following tooAzure Storage by using hello **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="53ae3-105">Serviço de nuvem do C#</span><span class="sxs-lookup"><span data-stu-id="53ae3-105">C# cloud service</span></span>
- <span data-ttu-id="53ae3-106">Serviço móvel de back-end .NET</span><span class="sxs-lookup"><span data-stu-id="53ae3-106">.NET backend mobile service</span></span>
- <span data-ttu-id="53ae3-107">Site ou serviço ASP.NET</span><span class="sxs-lookup"><span data-stu-id="53ae3-107">ASP.NET website or service</span></span>
- <span data-ttu-id="53ae3-108">Principais serviços ASP.NET</span><span class="sxs-lookup"><span data-stu-id="53ae3-108">ASP.NET Core service</span></span>
- <span data-ttu-id="53ae3-109">Serviço do Trabalho Web do Azure</span><span class="sxs-lookup"><span data-stu-id="53ae3-109">Azure WebJob service</span></span> 

<span data-ttu-id="53ae3-110">Olá serviço conectado funcionalidade adiciona todas as referências de saudação necessário e projeto de tooyour de código de conexão e modifica os arquivos de configuração adequadamente.</span><span class="sxs-lookup"><span data-stu-id="53ae3-110">hello connected service functionality adds all hello needed references and connection code tooyour project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="53ae3-111">Após a conclusão, Olá **adicionar serviços conectados** caixa de diálogo exibe automaticamente documentação detalhando Olá etapas necessárias toostart, trabalhando com o armazenamento de BLOBs, filas e tabelas.</span><span class="sxs-lookup"><span data-stu-id="53ae3-111">After completion, hello **Add Connected Services** dialog automatically displays documentation detailing hello steps required toostart working with blob storage, queues, and tables.</span></span>

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a><span data-ttu-id="53ae3-112">Conecte-se tooAzure armazenamento usando os serviços conectados Olá caixa de diálogo</span><span class="sxs-lookup"><span data-stu-id="53ae3-112">Connect tooAzure Storage using hello Connected Services dialog</span></span>
1. <span data-ttu-id="53ae3-113">Abra o projeto no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="53ae3-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="53ae3-114">Em **Gerenciador de soluções**, Olá atalho **serviços conectados** nó e, no menu de contexto hello e selecione **Adicionar serviço conectado**.</span><span class="sxs-lookup"><span data-stu-id="53ae3-114">In **Solution Explorer**, right-click hello **Connected Services** node, and, from hello context menu, and select **Add Connected Service**.</span></span>
   
    ![Adicionar serviço conectado do Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="53ae3-116">Em Olá **serviços conectados** página, selecione **armazenamento em nuvem com o armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="53ae3-116">In hello **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Adicionar Armazenamento do Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="53ae3-118">Em Olá **armazenamento do Azure** caixa de diálogo, selecione uma conta de armazenamento existente e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="53ae3-118">In hello **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="53ae3-119">Se você precisar toocreate uma conta de armazenamento, vá toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="53ae3-119">If you need toocreate a storage account, go toohello next step.</span></span> <span data-ttu-id="53ae3-120">Caso contrário, pule toostep 6.</span><span class="sxs-lookup"><span data-stu-id="53ae3-120">Otherwise, skip toostep 6.</span></span>
    
    ![Adicionar tooproject de conta de armazenamento existente](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="53ae3-122">toocreate uma conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="53ae3-122">toocreate a storage account:</span></span> 
   
   1. <span data-ttu-id="53ae3-123">Selecione **criar uma nova conta de armazenamento** na parte inferior da saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="53ae3-123">Select **Create a New Storage Account** at hello bottom of hello dialog.</span></span>

   1. <span data-ttu-id="53ae3-124">Preencha Olá **criar conta de armazenamento** caixa de diálogo e selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="53ae3-124">Fill out hello **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![Nova conta de armazenamento do Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="53ae3-126">Olá quando **armazenamento do Azure** caixa de diálogo é exibida, a nova conta de armazenamento Olá aparece na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="53ae3-126">When hello **Azure Storage** dialog is displayed, hello new storage account appears in hello list.</span></span> <span data-ttu-id="53ae3-127">Selecione a nova conta de armazenamento Olá na lista de saudação e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="53ae3-127">Select hello new storage account in hello list, and select **Add**.</span></span>

1. <span data-ttu-id="53ae3-128">Olá armazenamento serviço conectado aparece sob Olá **referências de serviço** nó do projeto.</span><span class="sxs-lookup"><span data-stu-id="53ae3-128">hello storage connected service appears under hello **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="53ae3-129">Como o projeto é modificado</span><span class="sxs-lookup"><span data-stu-id="53ae3-129">How your project is modified</span></span>
<span data-ttu-id="53ae3-130">Quando você terminar de caixa de diálogo Olá, o Visual Studio adiciona referências e modifica alguns arquivos de configuração.</span><span class="sxs-lookup"><span data-stu-id="53ae3-130">When you finish hello dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="53ae3-131">alterações específicas Olá dependem do tipo de projeto hello:</span><span class="sxs-lookup"><span data-stu-id="53ae3-131">hello specific changes depend on hello project type:</span></span> 

- <span data-ttu-id="53ae3-132">Projeto ASP.NET — [O que aconteceu — projetos ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="53ae3-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="53ae3-133">Projeto de Núcleo ASP.NET — [O que aconteceu — projetos ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="53ae3-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="53ae3-134">Projeto de serviço de nuvem (funções Web e funções de trabalho) — [O que aconteceu — projetos Serviço de Nuvem](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="53ae3-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="53ae3-135">Projetos de Trabalho Web — [O que aconteceu — projetos de Trabalho Web](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="53ae3-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="53ae3-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="53ae3-136">Next steps</span></span>
- [<span data-ttu-id="53ae3-137">Fórum do MSDN: Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="53ae3-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="53ae3-138">Blog da equipe do Armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="53ae3-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="53ae3-139">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="53ae3-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
