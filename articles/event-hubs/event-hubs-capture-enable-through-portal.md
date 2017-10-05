---
title: Habilitar a Captura de Hubs de Eventos do Azure por meio do portal | Microsoft Docs
description: Habilite o recurso Captura de Hubs de Eventos usando o portal do Azure.
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
ms.openlocfilehash: 0cbf45dce922647f2996f929d2c7cf885a2f4db4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-event-hubs-capture-using-the-azure-portal"></a><span data-ttu-id="695aa-103">Habilitar a Captura de Hubs de Evento usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="695aa-103">Enable Event Hubs Capture using the Azure portal</span></span>

<span data-ttu-id="695aa-104">Você pode configurar Captura na hora da criação do hub de eventos usando o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="695aa-104">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="695aa-105">Ou pode capturar os dados em um contêiner do [Armazenamento de Blobs](https://azure.microsoft.com/services/storage/blobs/) do Azure ou em uma conta do [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="695aa-105">You can either capture the data to an Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or to an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-to-an-azure-storage-account"></a><span data-ttu-id="695aa-106">Capturar dados em uma conta do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="695aa-106">Capture data to an Azure Storage account</span></span>  

<span data-ttu-id="695aa-107">Quando você cria um hub de eventos, você pode habilitar a captura clicando o **em** no botão de **criar Hub de eventos** folha portal.</span><span class="sxs-lookup"><span data-stu-id="695aa-107">When you create an event hub, you can enable Capture by clicking the **On** button in the **Create Event Hub** portal blade.</span></span> <span data-ttu-id="695aa-108">Em seguida, especifique uma Conta de Armazenamento e um contêiner clicando em **Armazenamento do Azure** na caixa **Provedor da Captura**.</span><span class="sxs-lookup"><span data-stu-id="695aa-108">You then specify a Storage Account and container by clicking **Azure Storage** in the **Capture Provider** box.</span></span> <span data-ttu-id="695aa-109">Já que a Captura dos Hubs de Eventos usa a autenticação de serviços com o armazenamento, você não precisa especificar uma cadeia de conexão de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="695aa-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need to specify a storage connection string.</span></span> <span data-ttu-id="695aa-110">O seletor de recurso seleciona automaticamente o URI do recurso para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="695aa-110">The resource picker selects the resource URI for your storage account automatically.</span></span> <span data-ttu-id="695aa-111">Se você usar o Azure Resource Manager, deverá fornecer esse URI explicitamente como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="695aa-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="695aa-112">A janela de tempo padrão é de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="695aa-112">The default time window is 5 minutes.</span></span> <span data-ttu-id="695aa-113">O valor mínimo é 1, o máximo é 15.</span><span class="sxs-lookup"><span data-stu-id="695aa-113">The minimum value is 1, the maximum 15.</span></span> <span data-ttu-id="695aa-114">A janela **Tamanho** tem um intervalo de 10 a 500 MB.</span><span class="sxs-lookup"><span data-stu-id="695aa-114">The **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-to-an-azure-data-lake-store-account"></a><span data-ttu-id="695aa-115">Capturar dados em uma conta do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="695aa-115">Capture data to an Azure Data Lake Store account</span></span>

<span data-ttu-id="695aa-116">Para capturar dados em um Azure Data Lake Store, você pode criar uma conta do Data Lake Store e um hub de eventos:</span><span class="sxs-lookup"><span data-stu-id="695aa-116">To capture data to Azure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="695aa-117">Criar uma conta e pastas do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="695aa-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="695aa-118">Crie uma conta do Data Lake Store seguindo as instruções em [Introdução ao Azure Data Lake Store usando o portal do Azure](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="695aa-118">Create a Data Lake Store account, following the instructions in [Get started with Azure Data Lake Store using the Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="695aa-119">Crie uma pasta nessa conta seguindo as instruções na seção [Criar pastas na conta do Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md#createfolder).</span><span class="sxs-lookup"><span data-stu-id="695aa-119">Create a folder under this account, following the instructions in the [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="695aa-120">Na folha de conta do repositório Data Lake, clique em **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="695aa-120">In the Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="695aa-121">Clique em **Acessar**.</span><span class="sxs-lookup"><span data-stu-id="695aa-121">Click **Access**.</span></span>
5. <span data-ttu-id="695aa-122">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="695aa-122">Click **Add**.</span></span>
6. <span data-ttu-id="695aa-123">Na caixa **Pesquisar por nome ou email**, digite **Microsoft.EventHubs** e selecione essa opção.</span><span class="sxs-lookup"><span data-stu-id="695aa-123">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="695aa-124">A guia **Permissões** aparecerá.</span><span class="sxs-lookup"><span data-stu-id="695aa-124">The **Permissions** tab appears.</span></span> <span data-ttu-id="695aa-125">Defina as permissões conforme mostrado na figura abaixo:</span><span class="sxs-lookup"><span data-stu-id="695aa-125">Set the permissions as shown in the following figure:</span></span>

    ![][6]

8. <span data-ttu-id="695aa-126">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="695aa-126">Click **OK**.</span></span>
9. <span data-ttu-id="695aa-127">Agora, crie uma pasta na pasta raiz navegando até a pasta de destino e clicando em seu nome.</span><span class="sxs-lookup"><span data-stu-id="695aa-127">Now, create a folder in the root folder by browsing to the target folder and clicking on the folder name.</span></span>
10. <span data-ttu-id="695aa-128">Clique em **Acessar**.</span><span class="sxs-lookup"><span data-stu-id="695aa-128">Click **Access**.</span></span>
11. <span data-ttu-id="695aa-129">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="695aa-129">Click **Add**.</span></span>
12. <span data-ttu-id="695aa-130">Na caixa **Pesquisar por nome ou email**, digite **Microsoft.EventHubs** e selecione essa opção.</span><span class="sxs-lookup"><span data-stu-id="695aa-130">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="695aa-131">A guia **Permissões** é exibida novamente.</span><span class="sxs-lookup"><span data-stu-id="695aa-131">The **Permissions** tab appears again.</span></span> <span data-ttu-id="695aa-132">Defina as permissões conforme mostrado na figura abaixo:</span><span class="sxs-lookup"><span data-stu-id="695aa-132">Set the permissions as shown in the following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="695aa-133">Criar um Hub de Evento</span><span class="sxs-lookup"><span data-stu-id="695aa-133">Create an event hub</span></span>

1. <span data-ttu-id="695aa-134">Observe que o hub de eventos deve estar na mesma assinatura do Azure que o Azure Data Lake Store recém-criado.</span><span class="sxs-lookup"><span data-stu-id="695aa-134">Note that the event hub must be in the same Azure subscription as the Azure Data Lake Store you just created.</span></span> <span data-ttu-id="695aa-135">Criar o hub de eventos, clicando no **na** botão em **capturar** no **criar Hub de eventos** portal folha.</span><span class="sxs-lookup"><span data-stu-id="695aa-135">Create the event hub, clicking the **On** button under **Capture** in the **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="695aa-136">No **criar Hub de eventos** portal folha, selecione **repositório Azure Data Lake** do **provedor capturar** caixa.</span><span class="sxs-lookup"><span data-stu-id="695aa-136">In the **Create Event Hub** portal blade, select **Azure Data Lake Store** from the **Capture Provider** box.</span></span>
3. <span data-ttu-id="695aa-137">Em **Azure Data Lake Store**, especifique a conta do Data Lake Store criada anteriormente e, no campo **Caminho do Data Lake**, digite o caminho para a pasta de dados criada.</span><span class="sxs-lookup"><span data-stu-id="695aa-137">In **Select Data Lake Store**, specify the Data Lake Store account you created previously, and in the **Data Lake Path** field, enter the path to the data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="695aa-138">Adicionar ou configurar a Captura em um hub de eventos existente</span><span class="sxs-lookup"><span data-stu-id="695aa-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="695aa-139">Você pode configurar a Captura em hubs de eventos existentes que estejam em namespaces dos Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="695aa-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="695aa-140">Para habilitar a Captura em um hub de eventos existente ou alterar as configurações da Captura, clique no namespace para carregar a folha **Essentials** e clique no Hub de Eventos para o qual você deseja habilitar ou alterar a configuração da Captura.</span><span class="sxs-lookup"><span data-stu-id="695aa-140">To enable Capture on an existing event hub, or to change your Capture settings, click the namespace to load the **Essentials** blade, then click the event hub for which you want to enable or change the Capture setting.</span></span> <span data-ttu-id="695aa-141">Por fim, clique no **propriedades** seção da folha de abrir e editar as configurações de captura, conforme as figuras a seguir:</span><span class="sxs-lookup"><span data-stu-id="695aa-141">Finally, click the **Properties** section of the open blade and then edit the Capture settings, as shown in the following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="695aa-142">Armazenamento do Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="695aa-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="695aa-143">Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="695aa-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="695aa-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="695aa-144">Next steps</span></span>

<span data-ttu-id="695aa-145">Você também pode configurar a Captura dos Hubs de Eventos usando modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="695aa-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="695aa-146">Para saber mais, confira [Habilitar Captura usando um modelo do Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span><span class="sxs-lookup"><span data-stu-id="695aa-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
