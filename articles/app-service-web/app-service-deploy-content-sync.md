---
title: "Sincronizar o conteúdo de uma pasta de nuvem para o Serviço de Aplicativo do Azure"
description: "Saiba como implantar seu aplicativo no Serviço de Aplicativo do Azure por meio da sincronização de conteúdo de uma pasta de nuvem."
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
ms.openlocfilehash: 010e7dc492abefaa3afe814c0322af9f6fe5acd2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="sync-content-from-a-cloud-folder-to-azure-app-service"></a><span data-ttu-id="52e4a-103">Sincronizar o conteúdo de uma pasta de nuvem para o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="52e4a-103">Sync content from a cloud folder to Azure App Service</span></span>
<span data-ttu-id="52e4a-104">Este tutorial mostra como implantar o [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) sincronizando o conteúdo de serviços populares de armazenamento em nuvem como o Dropbox e o OneDrive.</span><span class="sxs-lookup"><span data-stu-id="52e4a-104">This tutorial shows you how to deploy to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="52e4a-105"><a name="overview"></a>Visão geral da implantação de sincronização de conteúdo</span><span class="sxs-lookup"><span data-stu-id="52e4a-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="52e4a-106">A implantação de sincronização de conteúdo sob demanda é proveniente da plataforma do [mecanismo de implantação do Kudu](https://github.com/projectkudu/kudu/wiki) integrado ao Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="52e4a-106">The on-demand content sync deployment is powered by the [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="52e4a-107">No [Portal do Azure](https://portal.azure.com), é possível designar uma pasta em seu armazenamento em nuvem, trabalhar com o código e o conteúdo do aplicativo nessa pasta e sincronizá-la com o Serviço de Aplicativo com apenas um clique.</span><span class="sxs-lookup"><span data-stu-id="52e4a-107">In the [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync to App Service with the click of a button.</span></span> <span data-ttu-id="52e4a-108">A sincronização de conteúdo utiliza o processo do Kudu para build e implantação.</span><span class="sxs-lookup"><span data-stu-id="52e4a-108">Content sync utilizes the Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="52e4a-109"><a name="contentsync"></a>Como habilitar a implantação de sincronização de conteúdo</span><span class="sxs-lookup"><span data-stu-id="52e4a-109"><a name="contentsync"></a>How to enable content sync deployment</span></span>
<span data-ttu-id="52e4a-110">Para habilitar a sincronização de conteúdo por meio do [Portal do Azure](https://portal.azure.com), siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="52e4a-110">To enable content sync from the [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="52e4a-111">Na folha do aplicativo no Portal do Azure, clique em **Configurações** > **Origem da Implantação**.</span><span class="sxs-lookup"><span data-stu-id="52e4a-111">In your app's blade in the Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="52e4a-112">Clique em **Escolher Origem** e selecione **OneDrive** ou **Dropbox** como a origem da implantação.</span><span class="sxs-lookup"><span data-stu-id="52e4a-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as the source for deployment.</span></span> 
   
    ![Sincronização de conteúdo](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="52e4a-114">Devido a diferenças subjacentes nas APIs, o **OneDrive for Business** não tem suporte no momento.</span><span class="sxs-lookup"><span data-stu-id="52e4a-114">Because of underlying differences in the APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="52e4a-115">Conclua o fluxo de trabalho de autorização para permitir que o Serviço de Aplicativo acesse um caminho designado predefinido específico para o OneDrive ou Dropbox no qual todo o conteúdo do Serviço de Aplicativo será armazenado.</span><span class="sxs-lookup"><span data-stu-id="52e4a-115">Complete the authorization workflow to enable App Service to access a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="52e4a-116">Após a autorização, a plataforma do Serviço de Aplicativo lhe dará a opção de criar uma pasta de conteúdo no caminho de conteúdo designado ou escolher uma pasta de conteúdo existente nesse caminho de conteúdo designado.</span><span class="sxs-lookup"><span data-stu-id="52e4a-116">After authorization the App Service platform will give you the option to create a content folder under the designated content path, or to choose an existing content folder under this designated content path.</span></span> <span data-ttu-id="52e4a-117">Os caminhos de conteúdo designados em suas contas de armazenamento em nuvem usados para a sincronização do Serviço de Aplicativo são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="52e4a-117">The designated content paths under your cloud storage accounts used for App Service sync are the following:</span></span>  
   
   * <span data-ttu-id="52e4a-118">**OneDrive**: `Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="52e4a-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="52e4a-119">**Dropbox**: `Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="52e4a-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="52e4a-120">Após a sincronização inicial de conteúdo, a sincronização de conteúdo poderá ser iniciada sob demanda no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="52e4a-120">After the initial content sync the content sync can be initiated on demand from the Azure portal.</span></span> <span data-ttu-id="52e4a-121">O histórico de implantação está disponível na folha **Implantações** .</span><span class="sxs-lookup"><span data-stu-id="52e4a-121">Deployment history is available with the **Deployments** blade.</span></span>
   
    ![Histórico de implantação](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="52e4a-123">Mais informações para a implantação do Dropbox estão disponíveis em [Implantar por meio do Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="52e4a-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

