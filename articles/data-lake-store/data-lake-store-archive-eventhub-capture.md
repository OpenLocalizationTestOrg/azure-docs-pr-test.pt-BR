---
title: Capturar dados de Hubs de Eventos no Azure Data Lake Store | Microsoft Docs
description: Use o Azure Data Lake Store Use para capturar dados de Hubs de Eventos
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: a9e69576958ae96d22a4eb03d0df429f0b307298
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-store-to-capture-data-from-event-hubs"></a><span data-ttu-id="ddf83-103">Use o Azure Data Lake Store Use para capturar dados de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="ddf83-103">Use Azure Data Lake Store to capture data from Event Hubs</span></span>

<span data-ttu-id="ddf83-104">Saiba como usar o Azure Data Lake Store para capturar dados recebidos pelos Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ddf83-104">Learn how to use Azure Data Lake Store to capture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddf83-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ddf83-105">Prerequisites</span></span>

* <span data-ttu-id="ddf83-106">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-106">**An Azure subscription**.</span></span> <span data-ttu-id="ddf83-107">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ddf83-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="ddf83-108">**Uma conta do repositório Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="ddf83-109">Para obter instruções sobre como criar uma, consulte [Introdução ao Azure Data Lake Store](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ddf83-109">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="ddf83-110">**Um namespace dos Hubs de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="ddf83-111">Para obter instruções, confira [Criar um namespace dos Hubs de Eventos](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="ddf83-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="ddf83-112">Verifique se a conta do Data Lake Store e o namespace dos Hubs de Eventos estão na mesma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ddf83-112">Make sure the Data Lake Store account and the Event Hubs namespace are in the same Azure subscription.</span></span>


## <a name="assign-permissions-to-event-hubs"></a><span data-ttu-id="ddf83-113">Atribuir permissões aos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="ddf83-113">Assign permissions to Event Hubs</span></span>

<span data-ttu-id="ddf83-114">Nesta seção, você criará uma pasta dentro da conta na qual você deseja capturar os dados dos Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="ddf83-114">In this section, you create a folder within the account where you want to capture the data from Event Hubs.</span></span> <span data-ttu-id="ddf83-115">Você também atribui permissões aos Hubs de Eventos para que eles possam gravar dados em uma conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ddf83-115">You also assign permissions to Event Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="ddf83-116">Abra a conta do Data Lake Store onde você deseja capturar dados dos Hubs de Eventos e, em seguida, clique em **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-116">Open the Data Lake Store account where you want to capture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="ddf83-117">![Data explorer do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data explorer do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="ddf83-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="ddf83-118">Clique em **Nova Pasta** e digite um nome para a pasta onde você deseja capturar os dados.</span><span class="sxs-lookup"><span data-stu-id="ddf83-118">Click **New Folder** and then enter a name for folder where you want to capture the data.</span></span>

    <span data-ttu-id="ddf83-119">![Criar uma nova pasta no Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Criar uma nova pasta no Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="ddf83-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="ddf83-120">Atribua permissões na raiz do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ddf83-120">Assign permissions at the root of the Data Lake Store.</span></span> 

    <span data-ttu-id="ddf83-121">a.</span><span class="sxs-lookup"><span data-stu-id="ddf83-121">a.</span></span> <span data-ttu-id="ddf83-122">Clique em **Data Explorer**, selecione a raiz da conta do Data Lake Store e, em seguida, clique em **Acesso**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-122">Click **Data Explorer**, select the root of the Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="ddf83-123">![Atribuir permissões para a raiz do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Atribuir permissões para a raiz do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="ddf83-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="ddf83-124">b.</span><span class="sxs-lookup"><span data-stu-id="ddf83-124">b.</span></span> <span data-ttu-id="ddf83-125">Em **Acesso**, clique em **Adicionar**, clique em **Selecionar Usuário ou Grupo** e procure por `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="ddf83-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="ddf83-126">![Atribuir permissões para a raiz do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Atribuir permissões para a raiz do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="ddf83-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="ddf83-127">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-127">Click **Select**.</span></span>

    <span data-ttu-id="ddf83-128">c.</span><span class="sxs-lookup"><span data-stu-id="ddf83-128">c.</span></span> <span data-ttu-id="ddf83-129">Em **Atribuir Permissões**, clique em **Selecionar Permissões**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="ddf83-130">Defina **Permissões** como **Executar**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-130">Set **Permissions** to **Execute**.</span></span> <span data-ttu-id="ddf83-131">Defina **Adicionar a** como **Esta pasta e todas as filhas**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-131">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="ddf83-132">Defina **Adicionar como** como **Uma entrada de permissão de acesso e uma entrada de permissão predefinida**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-132">Set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="ddf83-133">![Atribuir permissões para a raiz do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Atribuir permissões para a raiz do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="ddf83-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="ddf83-134">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-134">Click **OK**.</span></span>

4. <span data-ttu-id="ddf83-135">Atribua permissões para a pasta na conta do Data Lake Store onde você deseja capturar dados.</span><span class="sxs-lookup"><span data-stu-id="ddf83-135">Assign permissions for the folder under Data Lake Store account where you want to capture data.</span></span>

    <span data-ttu-id="ddf83-136">a.</span><span class="sxs-lookup"><span data-stu-id="ddf83-136">a.</span></span> <span data-ttu-id="ddf83-137">Clique em **Data Explorer**, selecione a pasta na conta do Data Lake Store e, em seguida, clique em **Acesso**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-137">Click **Data Explorer**, select the folder in the Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="ddf83-138">![Atribuir permissões para a pasta do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Atribuir permissões para a pasta do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="ddf83-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="ddf83-139">b.</span><span class="sxs-lookup"><span data-stu-id="ddf83-139">b.</span></span> <span data-ttu-id="ddf83-140">Em **Acesso**, clique em **Adicionar**, clique em **Selecionar Usuário ou Grupo** e procure por `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="ddf83-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="ddf83-141">![Atribuir permissões para a pasta do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Atribuir permissões para a pasta do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="ddf83-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="ddf83-142">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-142">Click **Select**.</span></span>

    <span data-ttu-id="ddf83-143">c.</span><span class="sxs-lookup"><span data-stu-id="ddf83-143">c.</span></span> <span data-ttu-id="ddf83-144">Em **Atribuir Permissões**, clique em **Selecionar Permissões**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="ddf83-145">Defina **Permissões** como **Ler, Gravar** e **Executar**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-145">Set **Permissions** to **Read, Write,** and **Execute**.</span></span> <span data-ttu-id="ddf83-146">Defina **Adicionar a** como **Esta pasta e todas as filhas**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-146">Set **Add to** to **This folder and all children**.</span></span> <span data-ttu-id="ddf83-147">Por fim, defina **Adicionar como** como **Uma entrada de permissão de acesso e uma entrada de permissão predefinida**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-147">Finally, set **Add as** to **An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="ddf83-148">![Atribuir permissões para a pasta do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Atribuir permissões para a pasta do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="ddf83-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="ddf83-149">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-to-capture-data-to-data-lake-store"></a><span data-ttu-id="ddf83-150">Configurar os Hubs de Eventos para capturar dados no Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ddf83-150">Configure Event Hubs to capture data to Data Lake Store</span></span>

<span data-ttu-id="ddf83-151">Nesta seção, você criará um Hub de Eventos dentro de um namespace de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="ddf83-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="ddf83-152">Também configurará o Hub de Eventos para capturar os dados em uma conta do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ddf83-152">You also configure the Event Hub to capture data to an Azure Data Lake Store account.</span></span> <span data-ttu-id="ddf83-153">Esta seção pressupõe que você já criou um namespace dos Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="ddf83-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="ddf83-154">No painel **Visão Geral** do namespace de Hubs de Eventos, clique em **+ Hub de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-154">From the **Overview** pane of the Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="ddf83-155">![Criar Hub de Eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Criar Hub de Eventos")</span><span class="sxs-lookup"><span data-stu-id="ddf83-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="ddf83-156">Forneça os valores a seguir para configurar os Hubs de Eventos a fim de capturar dados no Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ddf83-156">Provide the following values to configure Event Hubs to capture data to Data Lake Store.</span></span>

    <span data-ttu-id="ddf83-157">![Criar Hub de Eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Criar Hub de Eventos")</span><span class="sxs-lookup"><span data-stu-id="ddf83-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="ddf83-158">a.</span><span class="sxs-lookup"><span data-stu-id="ddf83-158">a.</span></span> <span data-ttu-id="ddf83-159">Forneça um nome para o Hub de Eventos.</span><span class="sxs-lookup"><span data-stu-id="ddf83-159">Provide a name for the Event Hub.</span></span>
    
    <span data-ttu-id="ddf83-160">b.</span><span class="sxs-lookup"><span data-stu-id="ddf83-160">b.</span></span> <span data-ttu-id="ddf83-161">Para este tutorial, defina **Contagem de Partições** e **Retenção de Mensagem** com os valores padrão.</span><span class="sxs-lookup"><span data-stu-id="ddf83-161">For this tutorial, set **Partition Count** and **Message Retention** to the default values.</span></span>
    
    <span data-ttu-id="ddf83-162">c.</span><span class="sxs-lookup"><span data-stu-id="ddf83-162">c.</span></span> <span data-ttu-id="ddf83-163">Defina **Capturar** como **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-163">Set **Capture** to **On**.</span></span> <span data-ttu-id="ddf83-164">Defina a **Janela de Tempo** (a frequência de captura) e **Janela de Tamanho** (tamanho dos dados para captura).</span><span class="sxs-lookup"><span data-stu-id="ddf83-164">Set the **Time Window** (how frequently to capture) and **Size Window** (data size to capture).</span></span> 
    
    <span data-ttu-id="ddf83-165">d.</span><span class="sxs-lookup"><span data-stu-id="ddf83-165">d.</span></span> <span data-ttu-id="ddf83-166">Para **Provedor de Captura**, selecione **Azure Data Lake Store** e selecione o Data Lake Store criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ddf83-166">For **Capture Provider**, select **Azure Data Lake Store** and the select the Data Lake Store you created earlier.</span></span> <span data-ttu-id="ddf83-167">Para **Caminho do Data Lake**, digite o nome da pasta que você criou na conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ddf83-167">For **Data Lake Path**, enter the name of the folder you created in the Data Lake Store account.</span></span> <span data-ttu-id="ddf83-168">Você só precisa fornecer o caminho relativo para a pasta.</span><span class="sxs-lookup"><span data-stu-id="ddf83-168">You only need to provide the relative path to the folder.</span></span>

    <span data-ttu-id="ddf83-169">e.</span><span class="sxs-lookup"><span data-stu-id="ddf83-169">e.</span></span> <span data-ttu-id="ddf83-170">Deixe os **Formatos de nome de arquivo de captura de exemplo** como o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="ddf83-170">Leave the **Sample capture file name formats** to the default value.</span></span> <span data-ttu-id="ddf83-171">Essa opção controla a estrutura de pastas criada sob a pasta de captura.</span><span class="sxs-lookup"><span data-stu-id="ddf83-171">This option governs the folder structure that is created under the capture folder.</span></span>

    <span data-ttu-id="ddf83-172">f.</span><span class="sxs-lookup"><span data-stu-id="ddf83-172">f.</span></span> <span data-ttu-id="ddf83-173">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ddf83-173">Click **Create**.</span></span>

## <a name="test-the-setup"></a><span data-ttu-id="ddf83-174">Testar a configuração</span><span class="sxs-lookup"><span data-stu-id="ddf83-174">Test the setup</span></span>

<span data-ttu-id="ddf83-175">Agora, você pode testar a solução enviando dados para o Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ddf83-175">You can now test the solution by sending data to the Azure Event Hub.</span></span> <span data-ttu-id="ddf83-176">Siga as instruções em [Enviar eventos aos Hubs de Eventos do Azure](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="ddf83-176">Follow the instructions at [Send events to Azure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="ddf83-177">Quando você começar a enviar os dados, verá os dados refletidos no Data Lake Store usando a estrutura de pastas que você especificou.</span><span class="sxs-lookup"><span data-stu-id="ddf83-177">Once you start sending the data, you see the data reflected in Data Lake Store using the folder structure you specified.</span></span> <span data-ttu-id="ddf83-178">Por exemplo, você verá uma estrutura de pastas, conforme mostra a seguinte captura de tela, em seu Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ddf83-178">For example, you see a folder structure, as shown in the following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="ddf83-179">![Exemplo de dados do Hub de Eventos no Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Exemplo de dados do Hub de Eventos no Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="ddf83-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="ddf83-180">Mesmo se não houver mensagens chegando aos Hubs de Eventos, os Hubs de Eventos gravarão os arquivos vazios apenas com os cabeçalhos na conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ddf83-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just the headers into the Data Lake Store account.</span></span> <span data-ttu-id="ddf83-181">Os arquivos são gravados no mesmo intervalo de tempo fornecido durante a criação dos Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="ddf83-181">The files are written at the same time interval that you provided while creating the Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="ddf83-182">Analisar dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="ddf83-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="ddf83-183">Quando os dados estiverem no Data Lake Store, você poderá executar trabalhos de análise para processar e juntar os dados.</span><span class="sxs-lookup"><span data-stu-id="ddf83-183">Once the data is in Data Lake Store, you can run analytical jobs to process and crunch the data.</span></span> <span data-ttu-id="ddf83-184">Confira [Exemplo de USQL Avro](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) sobre como fazer isso usando o Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ddf83-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how to do this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="ddf83-185">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ddf83-185">See also</span></span>
* [<span data-ttu-id="ddf83-186">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="ddf83-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="ddf83-187">Copiar dados de Blobs do Armazenamento do Azure para o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="ddf83-187">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
