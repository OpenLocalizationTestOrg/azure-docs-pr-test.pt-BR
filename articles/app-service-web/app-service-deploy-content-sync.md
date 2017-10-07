---
title: "aaaSync conteúdo de uma pasta de nuvem tooAzure do serviço de aplicativo"
description: "Saiba como toodeploy seu tooAzure de aplicativo do serviço de aplicativo por meio do conteúdo de sincronização de uma pasta de nuvem."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a><span data-ttu-id="67bc7-103">Sincronizar o conteúdo de uma pasta de nuvem tooAzure do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="67bc7-103">Sync content from a cloud folder tooAzure App Service</span></span>
<span data-ttu-id="67bc7-104">Este tutorial mostra como toodeploy muito[do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) por sincronizando o conteúdo dos serviços de armazenamento de nuvem populares como o Dropbox e OneDrive.</span><span class="sxs-lookup"><span data-stu-id="67bc7-104">This tutorial shows you how toodeploy too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="67bc7-105"><a name="overview"></a>Visão geral da implantação de sincronização de conteúdo</span><span class="sxs-lookup"><span data-stu-id="67bc7-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="67bc7-106">implantação de sincronização de conteúdo sob demanda de saudação é alimentada por Olá [mecanismo de implantação Kudu](https://github.com/projectkudu/kudu/wiki) integrado com o serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="67bc7-106">hello on-demand content sync deployment is powered by hello [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="67bc7-107">Em Olá [Portal do Azure](https://portal.azure.com), você pode designar uma pasta no seu armazenamento em nuvem, com o código do aplicativo e o conteúdo na pasta de trabalho e sincronização tooApp serviço com hello clique de um botão.</span><span class="sxs-lookup"><span data-stu-id="67bc7-107">In hello [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync tooApp Service with hello click of a button.</span></span> <span data-ttu-id="67bc7-108">Sincronização de conteúdo utiliza o processo de Kudu Olá para compilação e implantação.</span><span class="sxs-lookup"><span data-stu-id="67bc7-108">Content sync utilizes hello Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="67bc7-109"><a name="contentsync"></a>Como o conteúdo de tooenable sincronizar implantação</span><span class="sxs-lookup"><span data-stu-id="67bc7-109"><a name="contentsync"></a>How tooenable content sync deployment</span></span>
<span data-ttu-id="67bc7-110">sincronização de conteúdo de tooenable de saudação [Portal do Azure](https://portal.azure.com), siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="67bc7-110">tooenable content sync from hello [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="67bc7-111">Na folha do seu aplicativo em Olá Portal do Azure, clique em **configurações** > **origem de implantação**.</span><span class="sxs-lookup"><span data-stu-id="67bc7-111">In your app's blade in hello Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="67bc7-112">Clique em **Escolher fonte**, em seguida, selecione **OneDrive** ou **Dropbox** como origem Olá para implantação.</span><span class="sxs-lookup"><span data-stu-id="67bc7-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as hello source for deployment.</span></span> 
   
    ![Sincronização de conteúdo](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="67bc7-114">Devido a diferenças subjacentes no hello APIs, **OneDrive para empresas** não tem suporte no momento.</span><span class="sxs-lookup"><span data-stu-id="67bc7-114">Because of underlying differences in hello APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="67bc7-115">Tooenable de fluxo de trabalho de autorização Olá completa tooaccess do serviço de aplicativo um determinado pré-definidas caminho designado para OneDrive ou Dropbox onde todo o conteúdo do serviço de aplicativo serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="67bc7-115">Complete hello authorization workflow tooenable App Service tooaccess a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="67bc7-116">Após a saudação de autorização plataforma do serviço de aplicativo dará a você Olá opção toocreate uma pasta de conteúdo em hello designada caminho de conteúdo ou toochoose uma pasta de conteúdo existente nesse caminho de conteúdo designado.</span><span class="sxs-lookup"><span data-stu-id="67bc7-116">After authorization hello App Service platform will give you hello option toocreate a content folder under hello designated content path, or toochoose an existing content folder under this designated content path.</span></span> <span data-ttu-id="67bc7-117">caminhos de conteúdo Olá designado em suas contas de armazenamento de nuvem usados para sincronização do serviço de aplicativo são seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="67bc7-117">hello designated content paths under your cloud storage accounts used for App Service sync are hello following:</span></span>  
   
   * <span data-ttu-id="67bc7-118">**OneDrive**: `Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="67bc7-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="67bc7-119">**Dropbox**: `Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="67bc7-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="67bc7-120">Depois de saudação sincronização de conteúdo de saudação inicial de sincronização de conteúdo pode ser iniciada sob demanda de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="67bc7-120">After hello initial content sync hello content sync can be initiated on demand from hello Azure portal.</span></span> <span data-ttu-id="67bc7-121">Histórico de implantação está disponível com hello **implantações** folha.</span><span class="sxs-lookup"><span data-stu-id="67bc7-121">Deployment history is available with hello **Deployments** blade.</span></span>
   
    ![Histórico de implantação](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="67bc7-123">Mais informações para a implantação do Dropbox estão disponíveis em [Implantar por meio do Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="67bc7-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

