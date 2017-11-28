---
title: Habilitar aaaAzure capturar de Hubs de eventos por meio do portal | Microsoft Docs
description: "Habilite o recurso de captura de Hubs de evento de saudação usando Olá portal do Azure."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a><span data-ttu-id="e8421-103">Habilitar a captura de Hubs de evento usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e8421-103">Enable Event Hubs Capture using hello Azure portal</span></span>

<span data-ttu-id="e8421-104">Você pode configurar a captura no momento da criação Olá evento hub usando Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e8421-104">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e8421-105">Pode qualquer tooan de dados captura hello Azure [armazenamento de Blob](https://azure.microsoft.com/services/storage/blobs/) contêiner ou tooan [repositório Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) conta.</span><span class="sxs-lookup"><span data-stu-id="e8421-105">You can either capture hello data tooan Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-tooan-azure-storage-account"></a><span data-ttu-id="e8421-106">Capturar conta de armazenamento do Azure tooan dados</span><span class="sxs-lookup"><span data-stu-id="e8421-106">Capture data tooan Azure Storage account</span></span>  

<span data-ttu-id="e8421-107">Quando você cria um hub de eventos, você pode habilitar a captura clicando Olá **na** botão Olá **criar Hub de eventos** portal folha.</span><span class="sxs-lookup"><span data-stu-id="e8421-107">When you create an event hub, you can enable Capture by clicking hello **On** button in hello **Create Event Hub** portal blade.</span></span> <span data-ttu-id="e8421-108">Em seguida, especifique uma conta de armazenamento e contêiner clicando **armazenamento do Azure** em Olá **provedor capturar** caixa.</span><span class="sxs-lookup"><span data-stu-id="e8421-108">You then specify a Storage Account and container by clicking **Azure Storage** in hello **Capture Provider** box.</span></span> <span data-ttu-id="e8421-109">Como capturar de Hubs de evento usa a autenticação de serviço a serviço com o armazenamento, não é necessário toospecify uma cadeia de caracteres de conexão de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e8421-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need toospecify a storage connection string.</span></span> <span data-ttu-id="e8421-110">Selecionador de recurso Olá seleciona automaticamente o URI do recurso Olá para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e8421-110">hello resource picker selects hello resource URI for your storage account automatically.</span></span> <span data-ttu-id="e8421-111">Se você usar o Azure Resource Manager, deverá fornecer esse URI explicitamente como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="e8421-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="e8421-112">janela de tempo saudação padrão é 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="e8421-112">hello default time window is 5 minutes.</span></span> <span data-ttu-id="e8421-113">valor mínimo de saudação é 1, Olá máximo 15.</span><span class="sxs-lookup"><span data-stu-id="e8421-113">hello minimum value is 1, hello maximum 15.</span></span> <span data-ttu-id="e8421-114">Olá **tamanho** janela tem um intervalo de 10 a 500 MB.</span><span class="sxs-lookup"><span data-stu-id="e8421-114">hello **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a><span data-ttu-id="e8421-115">Capturar conta de repositório Azure Data Lake tooan dados</span><span class="sxs-lookup"><span data-stu-id="e8421-115">Capture data tooan Azure Data Lake Store account</span></span>

<span data-ttu-id="e8421-116">toocapture dados tooAzure repositório Data Lake, crie uma conta do repositório Data Lake e um hub de eventos:</span><span class="sxs-lookup"><span data-stu-id="e8421-116">toocapture data tooAzure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="e8421-117">Criar uma conta e pastas do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e8421-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="e8421-118">Criar uma conta do repositório Data Lake, seguindo as instruções de saudação do [Introdução ao repositório Azure Data Lake usando Olá portal do Azure](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e8421-118">Create a Data Lake Store account, following hello instructions in [Get started with Azure Data Lake Store using hello Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="e8421-119">Criar uma pasta sob esta conta, seguindo as instruções de Olá Olá [criar pastas na conta do repositório Azure Data Lake](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) seção.</span><span class="sxs-lookup"><span data-stu-id="e8421-119">Create a folder under this account, following hello instructions in hello [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="e8421-120">Na folha de conta do repositório Data Lake hello, clique em **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e8421-120">In hello Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="e8421-121">Clique em **Acessar**.</span><span class="sxs-lookup"><span data-stu-id="e8421-121">Click **Access**.</span></span>
5. <span data-ttu-id="e8421-122">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e8421-122">Click **Add**.</span></span>
6. <span data-ttu-id="e8421-123">Em Olá **pesquisar por nome ou email** caixa tipo **Microsoft.EventHubs** e, em seguida, selecione essa opção.</span><span class="sxs-lookup"><span data-stu-id="e8421-123">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="e8421-124">Olá **permissões** guia é exibida.</span><span class="sxs-lookup"><span data-stu-id="e8421-124">hello **Permissions** tab appears.</span></span> <span data-ttu-id="e8421-125">Definir permissões de hello, conforme mostrado na figura a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="e8421-125">Set hello permissions as shown in hello following figure:</span></span>

    ![][6]

8. <span data-ttu-id="e8421-126">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8421-126">Click **OK**.</span></span>
9. <span data-ttu-id="e8421-127">Agora, crie uma pasta na pasta raiz de saudação toohello pasta de destino de navegação e clicando no nome da pasta Olá.</span><span class="sxs-lookup"><span data-stu-id="e8421-127">Now, create a folder in hello root folder by browsing toohello target folder and clicking on hello folder name.</span></span>
10. <span data-ttu-id="e8421-128">Clique em **Acessar**.</span><span class="sxs-lookup"><span data-stu-id="e8421-128">Click **Access**.</span></span>
11. <span data-ttu-id="e8421-129">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e8421-129">Click **Add**.</span></span>
12. <span data-ttu-id="e8421-130">Em Olá **pesquisar por nome ou email** caixa tipo **Microsoft.EventHubs** e, em seguida, selecione essa opção.</span><span class="sxs-lookup"><span data-stu-id="e8421-130">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="e8421-131">Olá **permissões** guia é exibida novamente.</span><span class="sxs-lookup"><span data-stu-id="e8421-131">hello **Permissions** tab appears again.</span></span> <span data-ttu-id="e8421-132">Definir permissões de hello, conforme mostrado na figura a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="e8421-132">Set hello permissions as shown in hello following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="e8421-133">Criar um Hub de Evento</span><span class="sxs-lookup"><span data-stu-id="e8421-133">Create an event hub</span></span>

1. <span data-ttu-id="e8421-134">Observe a esse hub de eventos Olá deve estar no hello mesma assinatura do Azure como Olá repositório Azure Data Lake você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="e8421-134">Note that hello event hub must be in hello same Azure subscription as hello Azure Data Lake Store you just created.</span></span> <span data-ttu-id="e8421-135">Criar hub de eventos de hello, clicando em Olá **na** botão em **capturar** em Olá **criar Hub de eventos** portal folha.</span><span class="sxs-lookup"><span data-stu-id="e8421-135">Create hello event hub, clicking hello **On** button under **Capture** in hello **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="e8421-136">Em Olá **criar Hub de eventos** portal folha, selecione **repositório Azure Data Lake** de saudação **provedor capturar** caixa.</span><span class="sxs-lookup"><span data-stu-id="e8421-136">In hello **Create Event Hub** portal blade, select **Azure Data Lake Store** from hello **Capture Provider** box.</span></span>
3. <span data-ttu-id="e8421-137">Em **selecione repositório do Data Lake**, especifique Olá conta do repositório Data Lake criado anteriormente e Olá **Data Lake caminho** campo, digite a pasta de dados Olá caminho toohello criado por você.</span><span class="sxs-lookup"><span data-stu-id="e8421-137">In **Select Data Lake Store**, specify hello Data Lake Store account you created previously, and in hello **Data Lake Path** field, enter hello path toohello data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="e8421-138">Adicionar ou configurar a Captura em um hub de eventos existente</span><span class="sxs-lookup"><span data-stu-id="e8421-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="e8421-139">Você pode configurar a Captura em hubs de eventos existentes que estejam em namespaces dos Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="e8421-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="e8421-140">tooenable captura em um hub de eventos existente ou toochange as configurações de captura, clique em saudação do hello namespace tooload **Essentials** folha, em seguida, clique em hub de eventos Olá para o qual você deseja tooenable ou alterar a configuração de captura de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8421-140">tooenable Capture on an existing event hub, or toochange your Capture settings, click hello namespace tooload hello **Essentials** blade, then click hello event hub for which you want tooenable or change hello Capture setting.</span></span> <span data-ttu-id="e8421-141">Por fim, clique em Olá **propriedades** seção Olá abrir folha e, em seguida, edite as configurações de captura hello, conforme mostrado no hello figuras a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8421-141">Finally, click hello **Properties** section of hello open blade and then edit hello Capture settings, as shown in hello following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="e8421-142">Armazenamento do Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="e8421-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="e8421-143">Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="e8421-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="e8421-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e8421-144">Next steps</span></span>

<span data-ttu-id="e8421-145">Você também pode configurar a Captura dos Hubs de Eventos usando modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e8421-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="e8421-146">Para saber mais, confira [Habilitar Captura usando um modelo do Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span><span class="sxs-lookup"><span data-stu-id="e8421-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
