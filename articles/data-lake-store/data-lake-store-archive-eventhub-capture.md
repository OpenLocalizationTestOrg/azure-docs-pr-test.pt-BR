---
title: "dados aaaCapture dos Hubs de eventos no repositório Azure Data Lake | Microsoft Docs"
description: "Dados do repositório do uso do Azure Data Lake toocapture dos Hubs de eventos"
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
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a><span data-ttu-id="7ab6b-103">Dados do repositório do uso do Azure Data Lake toocapture dos Hubs de eventos</span><span class="sxs-lookup"><span data-stu-id="7ab6b-103">Use Azure Data Lake Store toocapture data from Event Hubs</span></span>

<span data-ttu-id="7ab6b-104">Saiba como toouse dados do repositório Azure Data Lake toocapture recebeu por Hubs de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-104">Learn how toouse Azure Data Lake Store toocapture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ab6b-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7ab6b-105">Prerequisites</span></span>

* <span data-ttu-id="7ab6b-106">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-106">**An Azure subscription**.</span></span> <span data-ttu-id="7ab6b-107">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ab6b-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="7ab6b-108">**Uma conta do repositório Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="7ab6b-109">Para obter instruções sobre como um, ver toocreate [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7ab6b-109">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="7ab6b-110">**Um namespace dos Hubs de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="7ab6b-111">Para obter instruções, confira [Criar um namespace dos Hubs de Eventos](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="7ab6b-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="7ab6b-112">Certifique-se de conta do repositório Data Lake hello e Olá Hubs de eventos namespace estão no hello mesma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-112">Make sure hello Data Lake Store account and hello Event Hubs namespace are in hello same Azure subscription.</span></span>


## <a name="assign-permissions-tooevent-hubs"></a><span data-ttu-id="7ab6b-113">Atribuir permissões tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="7ab6b-113">Assign permissions tooEvent Hubs</span></span>

<span data-ttu-id="7ab6b-114">Nesta seção, você criar uma pasta dentro de conta Olá onde você deseja toocapture Olá dados dos Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-114">In this section, you create a folder within hello account where you want toocapture hello data from Event Hubs.</span></span> <span data-ttu-id="7ab6b-115">Você também atribuir permissões Hubs tooEvent para que ele possa gravar dados em uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-115">You also assign permissions tooEvent Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="7ab6b-116">Abrir conta de repositório Data Lake Olá onde você deseja que os dados toocapture dos Hubs de eventos e, em seguida, clique em **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-116">Open hello Data Lake Store account where you want toocapture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="7ab6b-117">![Data explorer do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data explorer do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="7ab6b-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="7ab6b-118">Clique em **nova pasta** e, em seguida, digite um nome para a pasta onde você deseja toocapture Olá dados.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-118">Click **New Folder** and then enter a name for folder where you want toocapture hello data.</span></span>

    <span data-ttu-id="7ab6b-119">![Criar uma nova pasta no Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Criar uma nova pasta no Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="7ab6b-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="7ab6b-120">Atribua permissões na raiz de saudação do hello repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-120">Assign permissions at hello root of hello Data Lake Store.</span></span> 

    <span data-ttu-id="7ab6b-121">a.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-121">a.</span></span> <span data-ttu-id="7ab6b-122">Clique em **Data Explorer**, selecione a raiz de saudação do hello conta do repositório Data Lake e, em seguida, clique em **acesso**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-122">Click **Data Explorer**, select hello root of hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="7ab6b-123">![Atribuir permissões para a raiz do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Atribuir permissões para a raiz do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="7ab6b-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="7ab6b-124">b.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-124">b.</span></span> <span data-ttu-id="7ab6b-125">Em **Acesso**, clique em **Adicionar**, clique em **Selecionar Usuário ou Grupo** e procure por `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="7ab6b-126">![Atribuir permissões para a raiz do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Atribuir permissões para a raiz do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="7ab6b-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="7ab6b-127">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-127">Click **Select**.</span></span>

    <span data-ttu-id="7ab6b-128">c.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-128">c.</span></span> <span data-ttu-id="7ab6b-129">Em **Atribuir Permissões**, clique em **Selecionar Permissões**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="7ab6b-130">Definir **permissões** muito**Execute**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-130">Set **Permissions** too**Execute**.</span></span> <span data-ttu-id="7ab6b-131">Definir **adicionar a** muito**essa pasta e todos os filhos**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-131">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="7ab6b-132">Definir **adicionar como** muito**uma entrada de permissão de acesso e uma entrada de permissão padrão**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-132">Set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="7ab6b-133">![Atribuir permissões para a raiz do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Atribuir permissões para a raiz do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="7ab6b-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="7ab6b-134">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-134">Click **OK**.</span></span>

4. <span data-ttu-id="7ab6b-135">Atribua permissões para pasta Olá na conta do repositório Data Lake onde você deseja toocapture dados.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-135">Assign permissions for hello folder under Data Lake Store account where you want toocapture data.</span></span>

    <span data-ttu-id="7ab6b-136">a.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-136">a.</span></span> <span data-ttu-id="7ab6b-137">Clique em **Data Explorer**, selecione a pasta Olá na conta do repositório Data Lake do hello e, em seguida, clique em **acesso**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-137">Click **Data Explorer**, select hello folder in hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="7ab6b-138">![Atribuir permissões para a pasta do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Atribuir permissões para a pasta do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="7ab6b-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="7ab6b-139">b.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-139">b.</span></span> <span data-ttu-id="7ab6b-140">Em **Acesso**, clique em **Adicionar**, clique em **Selecionar Usuário ou Grupo** e procure por `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="7ab6b-141">![Atribuir permissões para a pasta do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Atribuir permissões para a pasta do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="7ab6b-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="7ab6b-142">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-142">Click **Select**.</span></span>

    <span data-ttu-id="7ab6b-143">c.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-143">c.</span></span> <span data-ttu-id="7ab6b-144">Em **Atribuir Permissões**, clique em **Selecionar Permissões**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="7ab6b-145">Definir **permissões** muito**leitura, gravação,** e **Execute**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-145">Set **Permissions** too**Read, Write,** and **Execute**.</span></span> <span data-ttu-id="7ab6b-146">Definir **adicionar a** muito**essa pasta e todos os filhos**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-146">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="7ab6b-147">Finalmente, defina **adicionar como** muito**uma entrada de permissão de acesso e uma entrada de permissão padrão**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-147">Finally, set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="7ab6b-148">![Atribuir permissões para a pasta do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Atribuir permissões para a pasta do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="7ab6b-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="7ab6b-149">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a><span data-ttu-id="7ab6b-150">Configurar o repositório Hubs de eventos toocapture data tooData Lake</span><span class="sxs-lookup"><span data-stu-id="7ab6b-150">Configure Event Hubs toocapture data tooData Lake Store</span></span>

<span data-ttu-id="7ab6b-151">Nesta seção, você criará um Hub de Eventos dentro de um namespace de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="7ab6b-152">Você também pode configurar Olá Hub de eventos toocapture dados tooan conta do repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-152">You also configure hello Event Hub toocapture data tooan Azure Data Lake Store account.</span></span> <span data-ttu-id="7ab6b-153">Esta seção pressupõe que você já criou um namespace dos Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="7ab6b-154">De saudação **visão geral** painel do namespace de Hubs de eventos de saudação, clique em **+ Hub de eventos**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-154">From hello **Overview** pane of hello Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="7ab6b-155">![Criar Hub de Eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Criar Hub de Eventos")</span><span class="sxs-lookup"><span data-stu-id="7ab6b-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="7ab6b-156">Forneça a seguinte Olá valores tooconfigure Hubs de eventos toocapture dados tooData Lake repositório.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-156">Provide hello following values tooconfigure Event Hubs toocapture data tooData Lake Store.</span></span>

    <span data-ttu-id="7ab6b-157">![Criar Hub de Eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Criar Hub de Eventos")</span><span class="sxs-lookup"><span data-stu-id="7ab6b-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="7ab6b-158">a.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-158">a.</span></span> <span data-ttu-id="7ab6b-159">Forneça um nome para Olá Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-159">Provide a name for hello Event Hub.</span></span>
    
    <span data-ttu-id="7ab6b-160">b.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-160">b.</span></span> <span data-ttu-id="7ab6b-161">Neste tutorial, defina **contagem de partições** e **retenção de mensagem** toohello os valores padrão.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-161">For this tutorial, set **Partition Count** and **Message Retention** toohello default values.</span></span>
    
    <span data-ttu-id="7ab6b-162">c.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-162">c.</span></span> <span data-ttu-id="7ab6b-163">Definir **capturar** muito**em**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-163">Set **Capture** too**On**.</span></span> <span data-ttu-id="7ab6b-164">Saudação de conjunto **janela de tempo** (frequência toocapture) e **janela de tamanho** (toocapture de tamanho de dados).</span><span class="sxs-lookup"><span data-stu-id="7ab6b-164">Set hello **Time Window** (how frequently toocapture) and **Size Window** (data size toocapture).</span></span> 
    
    <span data-ttu-id="7ab6b-165">d.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-165">d.</span></span> <span data-ttu-id="7ab6b-166">Para **provedor capturar**, selecione **repositório Azure Data Lake** e selecione Olá Olá repositório Data Lake criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-166">For **Capture Provider**, select **Azure Data Lake Store** and hello select hello Data Lake Store you created earlier.</span></span> <span data-ttu-id="7ab6b-167">Para **Data Lake caminho**, digite nome de saudação da pasta de saudação criada na conta do repositório Data Lake do hello.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-167">For **Data Lake Path**, enter hello name of hello folder you created in hello Data Lake Store account.</span></span> <span data-ttu-id="7ab6b-168">Você só precisa de pasta de toohello tooprovide Olá caminho relativo.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-168">You only need tooprovide hello relative path toohello folder.</span></span>

    <span data-ttu-id="7ab6b-169">e.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-169">e.</span></span> <span data-ttu-id="7ab6b-170">Deixe Olá **formatos de nome de arquivo de captura do exemplo** toohello valor de padrão.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-170">Leave hello **Sample capture file name formats** toohello default value.</span></span> <span data-ttu-id="7ab6b-171">Essa opção controla a estrutura de pasta de saudação que é criada na pasta de captura hello.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-171">This option governs hello folder structure that is created under hello capture folder.</span></span>

    <span data-ttu-id="7ab6b-172">f.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-172">f.</span></span> <span data-ttu-id="7ab6b-173">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-173">Click **Create**.</span></span>

## <a name="test-hello-setup"></a><span data-ttu-id="7ab6b-174">Configuração de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="7ab6b-174">Test hello setup</span></span>

<span data-ttu-id="7ab6b-175">Agora você pode testar a solução Olá enviando dados toohello Hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-175">You can now test hello solution by sending data toohello Azure Event Hub.</span></span> <span data-ttu-id="7ab6b-176">Siga as instruções de saudação em [enviar eventos de Hubs de eventos tooAzure](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="7ab6b-176">Follow hello instructions at [Send events tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="7ab6b-177">Quando você começa a enviar dados hello, você vê os dados de saudação refletidos no repositório Data Lake usando a estrutura de pastas de saudação especificado.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-177">Once you start sending hello data, you see hello data reflected in Data Lake Store using hello folder structure you specified.</span></span> <span data-ttu-id="7ab6b-178">Por exemplo, verá uma estrutura de pasta, conforme mostrado no hello seguinte captura de tela, em seu repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-178">For example, you see a folder structure, as shown in hello following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="7ab6b-179">![Exemplo de dados do Hub de Eventos no Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Exemplo de dados do Hub de Eventos no Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="7ab6b-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="7ab6b-180">Mesmo se você não tem mensagens recebidas para Hubs de eventos, Hubs de eventos grava arquivos vazios com apenas a cabeçalhos de saudação em Olá conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just hello headers into hello Data Lake Store account.</span></span> <span data-ttu-id="7ab6b-181">Olá arquivos são gravados no hello mesmo intervalo de tempo que você forneceu durante a criação de Hubs de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-181">hello files are written at hello same time interval that you provided while creating hello Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="7ab6b-182">Analisar dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="7ab6b-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="7ab6b-183">Quando dados saudação estiverem no repositório Data Lake, você pode executar trabalhos analíticos tooprocess e situação dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-183">Once hello data is in Data Lake Store, you can run analytical jobs tooprocess and crunch hello data.</span></span> <span data-ttu-id="7ab6b-184">Consulte [USQL Avro exemplo](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) sobre como toodo esse usando análise Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how toodo this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="7ab6b-185">Consulte também</span><span class="sxs-lookup"><span data-stu-id="7ab6b-185">See also</span></span>
* [<span data-ttu-id="7ab6b-186">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="7ab6b-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="7ab6b-187">Copiar dados do repositório Azure armazenamento de Blobs tooData Lake</span><span class="sxs-lookup"><span data-stu-id="7ab6b-187">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
