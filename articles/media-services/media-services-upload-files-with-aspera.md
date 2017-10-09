---
title: "arquivos de aaaUpload em uma conta de serviços de mídia do Azure usando Aspera | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação de carregamento de arquivos em uma conta de armazenamento que está associada a uma conta de serviços de mídia usando hello * * Aspera Server na demanda * * o serviço no Azure."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="c05f3-103">Carregar arquivos em uma conta de serviços de mídia usando Olá serviço servidor sob demanda Aspera no Azure</span><span class="sxs-lookup"><span data-stu-id="c05f3-103">Upload files into a Media Services account using hello Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="c05f3-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c05f3-104">Overview</span></span>

<span data-ttu-id="c05f3-105">**Aspera** é um software de transferência de arquivos de alta velocidade.</span><span class="sxs-lookup"><span data-stu-id="c05f3-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="c05f3-106">O **Servidor Aspera sob demanda** para o Azure permite um carregamento de alta velocidade e download de arquivos grandes diretamente no armazenamento do objeto de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="c05f3-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="c05f3-107">Para obter informações sobre **Aspera On Demand**, consulte Olá [Aspera nuvem](http://cloud.asperasoft.com/) site.</span><span class="sxs-lookup"><span data-stu-id="c05f3-107">For information about **Aspera On Demand**, see hello [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="c05f3-108">**Servidor sob demanda Aspera** para Azure está disponível para compra Olá [do Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span><span class="sxs-lookup"><span data-stu-id="c05f3-108">**Aspera Server On Demand** for Azure is available for purchase from hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="c05f3-109">Em ordem toocomplete uma compra de **servidor sob demanda Aspera** do Azure, faça logon no Azure Marketplace com seu Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="c05f3-109">In order toocomplete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="c05f3-110">Este tutorial orienta você pelas etapas de saudação de carregamento de arquivos em uma conta de armazenamento que está associada a uma conta de serviços de mídia usando Olá **servidor sob demanda Aspera** serviço no Azure.</span><span class="sxs-lookup"><span data-stu-id="c05f3-110">This tutorial walks you through hello steps of uploading files into a storage account that is associated with a Media Services account using hello **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="c05f3-111">Você pode encontrar um exemplo que mostra como toouse Azure funciona com os serviços de mídia e Aspera [aqui](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span><span class="sxs-lookup"><span data-stu-id="c05f3-111">You can find an example that shows how toouse Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="c05f3-112">Há um limite toohello tamanho máximo com suporte para processadores de mídia (MPs) de processamento com os serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="c05f3-112">There is a limit toohello maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="c05f3-113">Consulte [isso](media-services-quotas-and-limitations.md) tópico para obter detalhes sobre a limitação de tamanho de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="c05f3-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="c05f3-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c05f3-114">Prerequisites</span></span> 

<span data-ttu-id="c05f3-115">toocomplete neste tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="c05f3-115">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="c05f3-116">Uma ID do Windows Live</span><span class="sxs-lookup"><span data-stu-id="c05f3-116">A Windows Live ID</span></span>
* <span data-ttu-id="c05f3-117">Uma [conta do Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c05f3-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="c05f3-118">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c05f3-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="c05f3-119">Uma [conta de Serviços de Mídia do Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="c05f3-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="c05f3-120">Comprar Aspera sob demanda para Azure</span><span class="sxs-lookup"><span data-stu-id="c05f3-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="c05f3-121">Depois de fazer logon no Azure Marketplace, siga essas toocomplete etapas básicas a compra do Aspera On Demand for Azure.</span><span class="sxs-lookup"><span data-stu-id="c05f3-121">Once you have logged into Azure Marketplace,  follow these basic steps toocomplete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="c05f3-122">Pesquise por Aspera e selecione 'Servidor sob demanda'.</span><span class="sxs-lookup"><span data-stu-id="c05f3-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="c05f3-124">Examine os planos de assinatura hello e clique em 'Inscrever-se'</span><span class="sxs-lookup"><span data-stu-id="c05f3-124">Review hello subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="c05f3-126">Preencha as especificidades de saudação para seu servidor na assinatura de demanda.</span><span class="sxs-lookup"><span data-stu-id="c05f3-126">Fill in hello specifics for your Server on Demand subscription.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="c05f3-128">Clique em Olá **preço** e selecione o volume mensal desejado no painel de sub hello.</span><span class="sxs-lookup"><span data-stu-id="c05f3-128">Click on hello **Pricing Tier** and select your desired monthly volume in hello sub panel.</span></span> <span data-ttu-id="c05f3-129">Em Olá **planejar detalhes** painel, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="c05f3-129">In hello **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="c05f3-130">Em seguida, no hello **escolha sua camada de preços** do painel, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="c05f3-130">Then, in hello **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="c05f3-132">Clique em **termos legais** tooview e aceitar os termos legais de saudação no painel de sub Olá.</span><span class="sxs-lookup"><span data-stu-id="c05f3-132">Click on **Legal terms** tooview and accept hello legal terms in hello sub panel.</span></span> <span data-ttu-id="c05f3-133">Depois de revisar os termos legais hello, clique em **compra**.</span><span class="sxs-lookup"><span data-stu-id="c05f3-133">Once you have reviewed hello legal terms, click **Purchase**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="c05f3-135">Concluir a compra de saudação clicando **criar**.</span><span class="sxs-lookup"><span data-stu-id="c05f3-135">Complete hello purchase by clicking **Create**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="c05f3-137">saudação do painel do Azure anunciará que ele é o provisionamento de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="c05f3-137">hello Azure dashboard will announce that it is provisioning hello service.</span></span>  <span data-ttu-id="c05f3-138">Depois de concluído com o provisionamento, você pode encontrar a nova assinatura de saudação pesquisando em seus recursos de nome de saudação do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="c05f3-138">Once it is completed with provisioning, you can find hello new subscription by searching in your resources for hello name of hello service.</span></span> <span data-ttu-id="c05f3-139">Após localizar serviço hello, clique duas vezes nele toolaunch portal de gerenciamento de serviços de saudação.</span><span class="sxs-lookup"><span data-stu-id="c05f3-139">Once you have found hello service, double click on it toolaunch hello service management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="c05f3-141">Inicie o portal de gerenciamento Aspera hello.</span><span class="sxs-lookup"><span data-stu-id="c05f3-141">Launch hello Aspera management portal.</span></span> <span data-ttu-id="c05f3-142">Após localizar o novo serviço Aspera, você pode obter o portal de gerenciamento do acesso toohello, clicando-se no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="c05f3-142">Once you have found your new Aspera service, you can gain access toohello management portal, by clicking on hello service.</span></span>  <span data-ttu-id="c05f3-143">Um novo painel será iniciado.</span><span class="sxs-lookup"><span data-stu-id="c05f3-143">A new panel will be launched.</span></span> <span data-ttu-id="c05f3-144">De dentro desse painel novo, você precisa tooclick em Olá **nome do recurso** do seu novo serviço.</span><span class="sxs-lookup"><span data-stu-id="c05f3-144">From within that new panel, you need tooclick on hello **Resource Name** of your new service.</span></span>  <span data-ttu-id="c05f3-145">No hello captura de tela a seguir, o nome do recurso de saudação é 'AsperaTransferDemo'.</span><span class="sxs-lookup"><span data-stu-id="c05f3-145">In hello following screenshot, hello resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="c05f3-146">Quando você clicar no nome do recurso hello, outro painel é iniciado.</span><span class="sxs-lookup"><span data-stu-id="c05f3-146">Once you click on hello resource name, another panel is launched.</span></span> <span data-ttu-id="c05f3-147">Nesse painel recém-lançado, você verá um link 'Gerenciar'.</span><span class="sxs-lookup"><span data-stu-id="c05f3-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="c05f3-148">Clique em Olá portal de gerenciamento 'Gerenciar' link toolaunch Olá Aspera.</span><span class="sxs-lookup"><span data-stu-id="c05f3-148">Click on hello 'Manage' link toolaunch hello Aspera management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="c05f3-150">Clicando em Olá gerenciar link, você obterá a página de registro de toohello, que é necessária tooaccess Olá serviço.</span><span class="sxs-lookup"><span data-stu-id="c05f3-150">By clicking on hello manage link, you will get toohello registration page, which is required tooaccess hello service.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="c05f3-152">Neste ponto, você deve ter acesso toohello Aspera service portal de gerenciamento, onde você pode criar chaves de acesso, baixar licenças e clientes Aspera, exiba o uso e saiba mais sobre Olá APIs.</span><span class="sxs-lookup"><span data-stu-id="c05f3-152">At this point, you should have access toohello Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about hello APIs.</span></span>

    <span data-ttu-id="c05f3-153">Olá seguinte captura de tela mostra a criação de acesso hello.</span><span class="sxs-lookup"><span data-stu-id="c05f3-153">hello following screenshot shows hello access creation.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="c05f3-155">Olá seguinte captura de tela mostra o uso de saudação interfaces no portal de saudação de emissão de relatórios.</span><span class="sxs-lookup"><span data-stu-id="c05f3-155">hello following screenshot shows hello usage reporting interfaces in hello portal.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="c05f3-157">Carregar arquivos com o Aspera</span><span class="sxs-lookup"><span data-stu-id="c05f3-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="c05f3-158">Baixe e instale o software de cliente Aspera hello:</span><span class="sxs-lookup"><span data-stu-id="c05f3-158">Download and install hello Aspera client software:</span></span>
    
    * [<span data-ttu-id="c05f3-159">Plug-in de navegador</span><span class="sxs-lookup"><span data-stu-id="c05f3-159">Browser plugin</span></span>](http://downloads.asperasoft.com/connect2/)
    * [<span data-ttu-id="c05f3-160">Cliente avançado</span><span class="sxs-lookup"><span data-stu-id="c05f3-160">Rich client</span></span>](http://downloads.asperasoft.com/en/downloads/2)

2. <span data-ttu-id="c05f3-161">Faça sua primeira transferência.</span><span class="sxs-lookup"><span data-stu-id="c05f3-161">Make your first transfer.</span></span> <span data-ttu-id="c05f3-162">Em ordem toouse Olá Aspera cliente tootransfer com hello Aspera serviço de transferência, você precisa fazer toocomplete Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="c05f3-162">In order toouse hello Aspera client tootransfer with hello Aspera transfer service, you need toocomplete hello following:</span></span> 

    1. <span data-ttu-id="c05f3-163">Crie uma chave de acesso, usando o portal de Aspera hello.</span><span class="sxs-lookup"><span data-stu-id="c05f3-163">Create an access key, using hello Aspera portal.</span></span>  
    2. <span data-ttu-id="c05f3-164">Download, a instalação e o cliente de Aspera de saudação de licença (o software pode ser encontrado no portal de Aspera de saudação).</span><span class="sxs-lookup"><span data-stu-id="c05f3-164">Download, install, and license hello Aspera client (software can be found in hello Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="c05f3-165">Leia Olá Aspera cliente guia para obter informações de configuração.</span><span class="sxs-lookup"><span data-stu-id="c05f3-165">Please read hello Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="c05f3-166">Recuperar algumas informações de sua conta de armazenamento que está associada com sua conta de mídia do Azure usando Olá [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c05f3-166">Retrieve some information of your storage account that is associated with your Azure Media Account using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="c05f3-167">Especificamente, o nome e chave e nome do contêiner de blob de armazenamento de saudação em toowhich deseja tooplace seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="c05f3-167">Specifically, name and key, and hello storage blob container name in toowhich you want tooplace your content.</span></span> 

        * <span data-ttu-id="c05f3-168">informações de armazenamento Olá tooget do portal de saudação: localizar sua conta de armazenamento, clique nas teclas de acesso do hello e cópia Olá nome e Olá a chave da sua conta.</span><span class="sxs-lookup"><span data-stu-id="c05f3-168">tooget hello storage info from hello portal: find your storage account, click on hello Access keys and copy hello name and hello key of your account.</span></span>
        * <span data-ttu-id="c05f3-169">nome do contêiner Olá tooget: localizar sua conta de armazenamento, selecione **Blobs**, selecione nome de saudação do contêiner de saudação deseja tooupload Olá conteúdo em.</span><span class="sxs-lookup"><span data-stu-id="c05f3-169">tooget hello container name: find your storage account, select **Blobs**, select hello name of hello container you want tooupload hello content into.</span></span> 

    <span data-ttu-id="c05f3-170">Abaixo está a captura de tela de saudação do cliente do hello Aspera **Gerenciador de Conexão** onde você deve especificar o tipo de armazenamento 'Do Azure' hello e credenciais, bem como o contêiner de blob hello.</span><span class="sxs-lookup"><span data-stu-id="c05f3-170">Below is hello screenshot of hello Aspera client **Connection Manager** where you must specify hello 'Azure' storage type and credentials as well as hello blob container.</span></span>

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="c05f3-172">Recursos</span><span class="sxs-lookup"><span data-stu-id="c05f3-172">Resources</span></span>

<span data-ttu-id="c05f3-173">Olá recursos a seguir foram mencionada neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c05f3-173">hello following resources were mentioned in this article.</span></span> 

* [<span data-ttu-id="c05f3-174">Plug-in Connect Browser</span><span class="sxs-lookup"><span data-stu-id="c05f3-174">Connect Browser Plugin</span></span>](http://downloads.asperasoft.com/connect2/)
* [<span data-ttu-id="c05f3-175">Guia do Connect</span><span class="sxs-lookup"><span data-stu-id="c05f3-175">Connect Guide</span></span>](http://downloads.asperasoft.com/en/documentation/8)
* [<span data-ttu-id="c05f3-176">Aspera Client</span><span class="sxs-lookup"><span data-stu-id="c05f3-176">Aspera Client</span></span>](http://downloads.asperasoft.com/en/downloads/2)
* [<span data-ttu-id="c05f3-177">Guia do Client</span><span class="sxs-lookup"><span data-stu-id="c05f3-177">Client Guide</span></span>](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a><span data-ttu-id="c05f3-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c05f3-178">Next steps</span></span>

<span data-ttu-id="c05f3-179">Agora você pode [copiar blobs de uma conta de armazenamento para uma conta do AMS ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span><span class="sxs-lookup"><span data-stu-id="c05f3-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c05f3-180">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="c05f3-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c05f3-181">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="c05f3-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

