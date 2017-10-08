---
title: "aaaCreate uma função que se conecta a serviços tooAzure | Microsoft Docs"
description: "Use as funções do Azure toocreate um aplicativo sem servidor que conecta tooother do Azure services."
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: "azure functions, functions, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a><span data-ttu-id="7a0ff-104">Use as funções do Azure toocreate uma função que se conecta tooother do Azure services</span><span class="sxs-lookup"><span data-stu-id="7a0ff-104">Use Azure Functions toocreate a function that connects tooother Azure services</span></span>

<span data-ttu-id="7a0ff-105">Este tópico mostra como toocreate uma função em funções do Azure que escuta toomessages em uma saudação de fila e cópias do armazenamento do Azure mensagens toorows em uma tabela de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-105">This topic shows you how toocreate a function in Azure Functions that listens toomessages on an Azure Storage queue and copies hello messages toorows in an Azure Storage table.</span></span> <span data-ttu-id="7a0ff-106">Uma função de temporizador disparado é usado tooload mensagens na fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-106">A timer triggered function is used tooload messages into hello queue.</span></span> <span data-ttu-id="7a0ff-107">Uma segunda função lê da fila de saudação e grava a tabela de toohello de mensagens.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-107">A second function reads from hello queue and writes messages toohello table.</span></span> <span data-ttu-id="7a0ff-108">Fila hello e tabela Olá são criadas para você por funções do Azure com base nas definições de associação de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-108">Both hello queue and hello table are created for you by Azure Functions based on hello binding definitions.</span></span> 

<span data-ttu-id="7a0ff-109">coisas toomake mais interessantes, uma função é escrita em JavaScript e outros Olá é gravado no script c#.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-109">toomake things more interesting, one function is written in JavaScript and hello other is written in C# script.</span></span> <span data-ttu-id="7a0ff-110">Isso demonstra como um aplicativo de funções pode ter funções em várias linguagens.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="7a0ff-111">Você pode ver esse cenário demonstrado em um [vídeo no Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span><span class="sxs-lookup"><span data-stu-id="7a0ff-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-toohello-queue"></a><span data-ttu-id="7a0ff-112">Crie uma função que grava toohello fila</span><span class="sxs-lookup"><span data-stu-id="7a0ff-112">Create a function that writes toohello queue</span></span>

<span data-ttu-id="7a0ff-113">Antes de poder conectar tooa fila de armazenamento, você precisa toocreate uma função que carrega a fila de mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-113">Before you can connect tooa storage queue, you need toocreate a function that loads hello message queue.</span></span> <span data-ttu-id="7a0ff-114">Essa função de JavaScript usa um gatilho de timer que grava uma fila de mensagens toohello cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-114">This JavaScript function uses a timer trigger that writes a message toohello queue every 10 seconds.</span></span> <span data-ttu-id="7a0ff-115">Se você ainda não tiver uma conta do Azure, confira Olá [funções do Azure tente](https://functions.azure.com/try) experiência, ou [criar sua conta gratuita do Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7a0ff-115">If you don't already have an Azure account, check out hello [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="7a0ff-116">Vá toohello portal do Azure e localize seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-116">Go toohello Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="7a0ff-117">Clique em **Nova Função** > **TimerTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="7a0ff-118">Nome de função hello **FunctionsBindingsDemo1**, digite um valor de expressão cron de `0/10 * * * * *` para **agenda**e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-118">Name hello function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Adicionar uma função disparada por temporizador](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="7a0ff-120">Você criou uma função disparada por temporizador que é executada a cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="7a0ff-121">Em Olá **desenvolver** , clique em **Logs** e exibir a atividade de Olá no log de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-121">On hello **Develop** tab, click **Logs** and view hello activity in hello log.</span></span> <span data-ttu-id="7a0ff-122">Você vê uma entrada de log gravada a cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-122">You see a log entry written every 10 seconds.</span></span>
   
    ![Exibir hello log tooverify Olá função funciona](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="7a0ff-124">Adicionar uma associação de saída de fila de mensagens</span><span class="sxs-lookup"><span data-stu-id="7a0ff-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="7a0ff-125">Em Olá **integrar** guia, escolha **nova saída** > **armazenamento de fila do Azure** > **selecione**.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-125">On hello **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Adicionar uma função de temporizador de gatilho](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="7a0ff-127">Digite `myQueueItem` para **nome de parâmetro de mensagem** e `functions-bindings` para **nome de fila**, selecione uma existente **conexão da conta de armazenamento** ou clique em **novo** toocreate um armazenamento de conta de conexão e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** toocreate a storage account connection, and then click **Save**.</span></span>  

    ![Criar fila de armazenamento Olá saída associação toohello](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="7a0ff-129">Em Olá **desenvolver** guia, acrescentar Olá função toohello de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a0ff-129">Back in hello **Develop** tab, append hello following code toohello function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="7a0ff-130">Localizar Olá *se* em torno de instrução linha 9 da função hello e de código a seguir de saudação insert após essa instrução.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-130">Locate hello *if* statement around line 9 of hello function, and insert hello following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="7a0ff-131">Esse código cria um **myQueueItem** e define seu **tempo** toohello propriedade carimbo de hora atual.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-131">This code creates a **myQueueItem** and sets its **time** property toohello current timeStamp.</span></span> <span data-ttu-id="7a0ff-132">Em seguida, adiciona Olá nova fila item toohello do contexto **myQueueItem** associação.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-132">It then adds hello new queue item toohello context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="7a0ff-133">Clique em **Salvar e Executar**.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="7a0ff-134">Exibir atualizações de armazenamento usando o Gerenciador de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="7a0ff-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="7a0ff-135">Você pode verificar se a função está funcionando, exibindo mensagens na fila Olá que você criou.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-135">You can verify that your function is working by viewing messages in hello queue you created.</span></span>  <span data-ttu-id="7a0ff-136">Você pode se conectar a fila de armazenamento tooyour usando o Pesquisador de objetos de nuvem no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-136">You can connect tooyour storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="7a0ff-137">No entanto, portal Olá torna fácil tooconnect conta de armazenamento de tooyour usando o Microsoft Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-137">However, hello portal makes it easy tooconnect tooyour storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="7a0ff-138">Em Olá **integrar** , clique em sua fila de associação de saída > **documentação**, reexibir hello cadeia de caracteres de Conexão para sua conta de armazenamento e copie o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-138">In hello **Integrate** tab, click your queue output binding > **Documentation**, then unhide hello Connection String for your storage account and copy hello value.</span></span> <span data-ttu-id="7a0ff-139">Você usar essa conta de armazenamento do valor tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-139">You use this value tooconnect tooyour storage account.</span></span>

    ![Baixar o Gerenciador de Armazenamento do Azure](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="7a0ff-141">Se você ainda não fez isso, baixe e instale o [Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="7a0ff-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="7a0ff-142">No Gerenciador de armazenamento, clique em Olá tooAzure armazenamento ícone connect, cole a cadeia de caracteres de conexão de Olá no campo hello e conclua o Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-142">In Storage Explorer, click hello connect tooAzure Storage icon, paste hello connection string in hello field, and complete hello wizard.</span></span>

    ![Gerenciador de Armazenamento – adicionar uma conexão](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="7a0ff-144">Em **Local e anexado**, expanda **contas de armazenamento** > sua conta de armazenamento > **filas** > **deassociaçõesdefunções**e verifique se que as mensagens são escritas toohello fila.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written toohello queue.</span></span>

    ![Exibição de mensagens na fila de saudação](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="7a0ff-146">Se a fila de saudação não existe ou está vazia, provavelmente há um problema com sua associação de função ou o código.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-146">If hello queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-hello-queue"></a><span data-ttu-id="7a0ff-147">Criar uma função que lê da fila de saudação</span><span class="sxs-lookup"><span data-stu-id="7a0ff-147">Create a function that reads from hello queue</span></span>

<span data-ttu-id="7a0ff-148">Agora que você tem que está sendo adicionadas toohello fila de mensagens, você pode criar outra função que lê da fila de saudação e gravações Olá permanentemente mensagens tooan tabela de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-148">Now that you have messages being added toohello queue, you can create another function that reads from hello queue and writes hello messages permanently tooan Azure Storage table.</span></span>

1. <span data-ttu-id="7a0ff-149">Clique em **Nova Função** > **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="7a0ff-150">Nome de função hello `FunctionsBindingsDemo2`, digite **associações a funções** em Olá **nome da fila** campo, selecione uma conta de armazenamento existente ou crie um e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-150">Name hello function `FunctionsBindingsDemo2`, enter **functions-bindings** in hello **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Adicionar uma função de temporizador de fila de saída](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="7a0ff-152">(Opcional) Você pode verificar que nova função de saudação funciona exibindo a nova fila de saudação no Gerenciador de armazenamento como antes.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-152">(Optional) You can verify that hello new function works by viewing hello new queue in Storage Explorer as before.</span></span> <span data-ttu-id="7a0ff-153">Você também pode usar o Cloud Explorer no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="7a0ff-154">(Opcional) Atualizar Olá **associações a funções** fila e observe que os itens foram removidos da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-154">(Optional) Refresh hello **functions-bindings** queue and notice that items have been removed from hello queue.</span></span> <span data-ttu-id="7a0ff-155">Hello remoção ocorre porque a função hello é toohello associado **associações a funções** como uma função de gatilho e hello entrada lê a fila de saudação da fila.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-155">hello removal occurs because hello function is bound toohello **functions-bindings** queue as an input trigger and hello function reads hello queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="7a0ff-156">Adicionar uma associação de saída da tabela</span><span class="sxs-lookup"><span data-stu-id="7a0ff-156">Add a table output binding</span></span>

1. <span data-ttu-id="7a0ff-157">Em FunctionsBindingsDemo2, clique em **Integrar** > **Nova Saída** > **Armazenamento de Tabela do Azure** > **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Adicionar uma tabela de armazenamento do Azure associação tooan](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="7a0ff-159">Insira `functionbindings` para **Nome de tabela** e `myTable` para **Nome de parâmetro de tabela**, escolha uma **Conexão da conta de armazenamento** ou crie uma nova e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Configurar a associação de tabela de armazenamento Olá](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="7a0ff-161">Em Olá **desenvolver** guia, substitua o código de função existente Olá pela seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="7a0ff-161">In hello **Develop** tab, replace hello existing function code with hello following:</span></span>
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add hello item toohello table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    <span data-ttu-id="7a0ff-162">Olá **TableItem** classe representa uma linha na tabela de armazenamento hello e adicionar Olá item toohello `myTable` coleção de **TableItem** objetos.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-162">hello **TableItem** class represents a row in hello storage table, and you add hello item toohello `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="7a0ff-163">Você deve definir Olá **PartitionKey** e **RowKey** propriedades toobe capaz de tooinsert na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-163">You must set hello **PartitionKey** and **RowKey** properties toobe able tooinsert into hello table.</span></span>

4. <span data-ttu-id="7a0ff-164">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-164">Click **Save**.</span></span>  <span data-ttu-id="7a0ff-165">Por fim, você pode verificar Olá função funciona exibindo tabela de saudação no Gerenciador de armazenamento ou o Gerenciador de nuvem do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-165">Finally, you can verify hello function works by viewing hello table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="7a0ff-166">(Opcional) Na sua conta de armazenamento no Gerenciador de armazenamento, expanda **tabelas** > **functionsbindings** e verifique se que linhas são adicionadas toohello tabela.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added toohello table.</span></span> <span data-ttu-id="7a0ff-167">Você pode fazer Olá mesmo no Gerenciador de nuvem no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-167">You can do hello same in Cloud Explorer in Visual Studio.</span></span>

    ![Exibição de linhas na tabela de saudação](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="7a0ff-169">Se a tabela de saudação não existe ou está vazia, provavelmente há um problema com sua associação de função ou o código.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-169">If hello table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="7a0ff-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7a0ff-170">Next steps</span></span>
<span data-ttu-id="7a0ff-171">Para obter mais informações sobre as funções do Azure, consulte Olá seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="7a0ff-171">For more information about Azure Functions, see hello following topics:</span></span>

* [<span data-ttu-id="7a0ff-172">Referência do desenvolvedor do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="7a0ff-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="7a0ff-173">Referência do programador para codificação de funções e definição de gatilhos e de associações.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="7a0ff-174">Testando o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="7a0ff-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="7a0ff-175">Descreve várias ferramentas e técnicas para testar suas funções.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="7a0ff-176">Como tooscale funções do Azure</span><span class="sxs-lookup"><span data-stu-id="7a0ff-176">How tooscale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="7a0ff-177">Discute os planos de serviço disponíveis com as funções do Azure, incluindo o plano de hospedagem de consumo hello e como toochoose Olá plano à direita.</span><span class="sxs-lookup"><span data-stu-id="7a0ff-177">Discusses service plans available with Azure Functions, including hello Consumption hosting plan, and how toochoose hello right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

