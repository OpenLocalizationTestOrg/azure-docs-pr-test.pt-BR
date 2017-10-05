---
title: "Criar uma função que se conecta aos serviços do Azure | Microsoft Docs"
description: "Usar Azure Functions para criar um aplicativo sem servidor que se conecta a outros serviços do Azure."
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
ms.openlocfilehash: 65964a322f0adab4f648fb350bedb77b46bf9054
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-functions-to-create-a-function-that-connects-to-other-azure-services"></a><span data-ttu-id="d23ad-104">Use as Azure Functions para criar uma função que se conecta a outros serviços do Azure</span><span class="sxs-lookup"><span data-stu-id="d23ad-104">Use Azure Functions to create a function that connects to other Azure services</span></span>

<span data-ttu-id="d23ad-105">Este tópico mostra como você pode criar uma função nas Azure Functions que escuta mensagens em uma fila do Armazenamento do Azure e copia as mensagens para linhas em uma tabela do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d23ad-105">This topic shows you how to create a function in Azure Functions that listens to messages on an Azure Storage queue and copies the messages to rows in an Azure Storage table.</span></span> <span data-ttu-id="d23ad-106">Uma função disparada por temporizador é usada para carregar as mensagens na fila.</span><span class="sxs-lookup"><span data-stu-id="d23ad-106">A timer triggered function is used to load messages into the queue.</span></span> <span data-ttu-id="d23ad-107">Uma segunda função lê da fila e grava as mensagens na tabela.</span><span class="sxs-lookup"><span data-stu-id="d23ad-107">A second function reads from the queue and writes messages to the table.</span></span> <span data-ttu-id="d23ad-108">Ambas a fila e a tabela são criadas para você por Azure Functions com base nas definições de associação.</span><span class="sxs-lookup"><span data-stu-id="d23ad-108">Both the queue and the table are created for you by Azure Functions based on the binding definitions.</span></span> 

<span data-ttu-id="d23ad-109">Para tornar as coisas mais interessantes, uma função é escrita em JavaScript e a outra é escrita em script C#.</span><span class="sxs-lookup"><span data-stu-id="d23ad-109">To make things more interesting, one function is written in JavaScript and the other is written in C# script.</span></span> <span data-ttu-id="d23ad-110">Isso demonstra como um aplicativo de funções pode ter funções em várias linguagens.</span><span class="sxs-lookup"><span data-stu-id="d23ad-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="d23ad-111">Você pode ver esse cenário demonstrado em um [vídeo no Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span><span class="sxs-lookup"><span data-stu-id="d23ad-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-to-the-queue"></a><span data-ttu-id="d23ad-112">Criar uma função que grava na fila</span><span class="sxs-lookup"><span data-stu-id="d23ad-112">Create a function that writes to the queue</span></span>

<span data-ttu-id="d23ad-113">Antes de você se conectar a uma fila de armazenamento, você precisa criar uma função que carrega a fila de mensagens.</span><span class="sxs-lookup"><span data-stu-id="d23ad-113">Before you can connect to a storage queue, you need to create a function that loads the message queue.</span></span> <span data-ttu-id="d23ad-114">Essa função de JavaScript usa um gatilho de temporizador que grava uma mensagem na fila a cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="d23ad-114">This JavaScript function uses a timer trigger that writes a message to the queue every 10 seconds.</span></span> <span data-ttu-id="d23ad-115">Se você ainda não tiver uma conta do Azure, confira a experiência [Experimentar o Azure Functions](https://functions.azure.com/try) ou [crie sua conta gratuita do Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="d23ad-115">If you don't already have an Azure account, check out the [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="d23ad-116">Acesse o Portal do Azure e localize o aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="d23ad-116">Go to the Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="d23ad-117">Clique em **Nova Função** > **TimerTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="d23ad-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="d23ad-118">Nomeie a função como **FunctionsBindingsDemo1**, insira um valor da expressão cron `0/10 * * * * *` para **Schedule** e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d23ad-118">Name the function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Adicionar uma função disparada por temporizador](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="d23ad-120">Você criou uma função disparada por temporizador que é executada a cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="d23ad-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="d23ad-121">Na guia **Desenvolver**, clique em **Logs** e exiba a atividade do log.</span><span class="sxs-lookup"><span data-stu-id="d23ad-121">On the **Develop** tab, click **Logs** and view the activity in the log.</span></span> <span data-ttu-id="d23ad-122">Você vê uma entrada de log gravada a cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="d23ad-122">You see a log entry written every 10 seconds.</span></span>
   
    ![Exibir o log para verificar se a função funciona](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="d23ad-124">Adicionar uma associação de saída de fila de mensagens</span><span class="sxs-lookup"><span data-stu-id="d23ad-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="d23ad-125">Na guia **Integrar**, escolha **Nova Saída** > **Armazenamento de Filas do Azure** > **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="d23ad-125">On the **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Adicionar uma função de temporizador de gatilho](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="d23ad-127">Insira `myQueueItem` para **Nome de parâmetro de mensagem** e `functions-bindings` para **Nome da fila**, selecione uma **Conexão da conta de armazenamento** existente ou clique em **nova** para criar uma conexão de conta de armazenamento e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d23ad-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** to create a storage account connection, and then click **Save**.</span></span>  

    ![Criar a associação de saída para a fila de armazenamento](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="d23ad-129">De volta à função **Desenvolver**, acrescente o seguinte código à função:</span><span class="sxs-lookup"><span data-stu-id="d23ad-129">Back in the **Develop** tab, append the following code to the function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="d23ad-130">Localize a instrução *if* ao redor da linha 9 da função e insira o código a seguir após essa instrução.</span><span class="sxs-lookup"><span data-stu-id="d23ad-130">Locate the *if* statement around line 9 of the function, and insert the following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="d23ad-131">Esse código cria um **myQueueItem** e define sua propriedade **time** com o carimbo de data/hora atual.</span><span class="sxs-lookup"><span data-stu-id="d23ad-131">This code creates a **myQueueItem** and sets its **time** property to the current timeStamp.</span></span> <span data-ttu-id="d23ad-132">Em seguida, ele adiciona o novo item de fila à associação **myQueueItem** do contexto.</span><span class="sxs-lookup"><span data-stu-id="d23ad-132">It then adds the new queue item to the context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="d23ad-133">Clique em **Salvar e Executar**.</span><span class="sxs-lookup"><span data-stu-id="d23ad-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="d23ad-134">Exibir atualizações de armazenamento usando o Gerenciador de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="d23ad-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="d23ad-135">Você pode verificar se a função está funcionando por meio da exibição de mensagens na fila que você criou.</span><span class="sxs-lookup"><span data-stu-id="d23ad-135">You can verify that your function is working by viewing messages in the queue you created.</span></span>  <span data-ttu-id="d23ad-136">Você pode se conectar à sua fila de armazenamento usando o Cloud Explorer no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d23ad-136">You can connect to your storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="d23ad-137">No entanto, o portal torna fácil conectar-se à sua conta de armazenamento usando o Gerenciador de Armazenamento do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d23ad-137">However, the portal makes it easy to connect to your storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="d23ad-138">Na guia **Integrar**, clique em sua fila de associação de saída > **Documentação**, exiba novamente a cadeia de conexão para sua conta de armazenamento e copie o valor.</span><span class="sxs-lookup"><span data-stu-id="d23ad-138">In the **Integrate** tab, click your queue output binding > **Documentation**, then unhide the Connection String for your storage account and copy the value.</span></span> <span data-ttu-id="d23ad-139">Você pode usar esse valor para conectar-se à sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d23ad-139">You use this value to connect to your storage account.</span></span>

    ![Baixar o Gerenciador de Armazenamento do Azure](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="d23ad-141">Se você ainda não fez isso, baixe e instale o [Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="d23ad-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="d23ad-142">No Gerenciador de Armazenamento, clique em conectar ao ícone de Armazenamento do Azure, cole a cadeia de conexão no campo e conclua o assistente.</span><span class="sxs-lookup"><span data-stu-id="d23ad-142">In Storage Explorer, click the connect to Azure Storage icon, paste the connection string in the field, and complete the wizard.</span></span>

    ![Gerenciador de Armazenamento – adicionar uma conexão](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="d23ad-144">Em **Local e anexado**, expanda **Contas de Armazenamento** > sua conta de armazenamento > **Filas** > **funções-associações** e verifique se as mensagens são gravadas na fila.</span><span class="sxs-lookup"><span data-stu-id="d23ad-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written to the queue.</span></span>

    ![Modo de exibição de mensagens na fila](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="d23ad-146">Se a fila não existe ou está vazia, provavelmente há um problema com o código ou a associação de função.</span><span class="sxs-lookup"><span data-stu-id="d23ad-146">If the queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-the-queue"></a><span data-ttu-id="d23ad-147">Criar uma função que lê da fila</span><span class="sxs-lookup"><span data-stu-id="d23ad-147">Create a function that reads from the queue</span></span>

<span data-ttu-id="d23ad-148">Agora que você tem mensagens sendo adicionadas à fila, você pode criar outra função que lê da fila e grava as mensagens permanentemente uma tabela de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d23ad-148">Now that you have messages being added to the queue, you can create another function that reads from the queue and writes the messages permanently to an Azure Storage table.</span></span>

1. <span data-ttu-id="d23ad-149">Clique em **Nova Função** > **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="d23ad-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="d23ad-150">Nomeie a função `FunctionsBindingsDemo2`, insira **funções-associações** no campo **Nome da Fila**, selecione uma conta de armazenamento existente ou crie uma e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d23ad-150">Name the function `FunctionsBindingsDemo2`, enter **functions-bindings** in the **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Adicionar uma função de temporizador de fila de saída](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="d23ad-152">(Opcional) Você pode verificar se a nova função funciona exibindo a nova fila no Gerenciador de Armazenamento como antes.</span><span class="sxs-lookup"><span data-stu-id="d23ad-152">(Optional) You can verify that the new function works by viewing the new queue in Storage Explorer as before.</span></span> <span data-ttu-id="d23ad-153">Você também pode usar o Cloud Explorer no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d23ad-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="d23ad-154">(Opcional) Atualize a fila **funções-associações** e observe os itens que foram removidos da fila.</span><span class="sxs-lookup"><span data-stu-id="d23ad-154">(Optional) Refresh the **functions-bindings** queue and notice that items have been removed from the queue.</span></span> <span data-ttu-id="d23ad-155">A remoção ocorre porque a função está associada à fila **funções-associações** como um gatilho de entrada e a função lê a fila.</span><span class="sxs-lookup"><span data-stu-id="d23ad-155">The removal occurs because the function is bound to the **functions-bindings** queue as an input trigger and the function reads the queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="d23ad-156">Adicionar uma associação de saída da tabela</span><span class="sxs-lookup"><span data-stu-id="d23ad-156">Add a table output binding</span></span>

1. <span data-ttu-id="d23ad-157">Em FunctionsBindingsDemo2, clique em **Integrar** > **Nova Saída** > **Armazenamento de Tabela do Azure** > **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="d23ad-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Adicionar uma associação a uma tabela de Armazenamento do Azure](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="d23ad-159">Insira `functionbindings` para **Nome de tabela** e `myTable` para **Nome de parâmetro de tabela**, escolha uma **Conexão da conta de armazenamento** ou crie uma nova e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d23ad-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Configurar a Associação da tabela de armazenamento](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="d23ad-161">Na guia **Desenvolver**, substitua o código de função existente pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="d23ad-161">In the **Develop** tab, replace the existing function code with the following:</span></span>
   
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
        
        // Add the item to the table binding collection.
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
    <span data-ttu-id="d23ad-162">A classe **TableItem** representa uma linha na tabela de armazenamento e você adiciona o item à coleção `myTable` de objetos **TableItem**.</span><span class="sxs-lookup"><span data-stu-id="d23ad-162">The **TableItem** class represents a row in the storage table, and you add the item to the `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="d23ad-163">Você deve definir as Propriedades **PartitionKey** e **RowKey** para poder inserir na tabela.</span><span class="sxs-lookup"><span data-stu-id="d23ad-163">You must set the **PartitionKey** and **RowKey** properties to be able to insert into the table.</span></span>

4. <span data-ttu-id="d23ad-164">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d23ad-164">Click **Save**.</span></span>  <span data-ttu-id="d23ad-165">Por fim, você pode verificar se a função funciona exibindo a tabela no Gerenciador de Armazenamento ou Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="d23ad-165">Finally, you can verify the function works by viewing the table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="d23ad-166">(Opcional) Na sua conta de armazenamento no Gerenciador de Armazenamento, expanda **Tabelas** > **funções-associações** e verifique se as linhas são adicionadas à tabela.</span><span class="sxs-lookup"><span data-stu-id="d23ad-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added to the table.</span></span> <span data-ttu-id="d23ad-167">Você pode fazer o mesmo no Cloud Explorer no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d23ad-167">You can do the same in Cloud Explorer in Visual Studio.</span></span>

    ![Modo de exibição de linhas na tabela](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="d23ad-169">Se a tabela não existe ou está vazia, provavelmente há um problema com o código ou a associação de função.</span><span class="sxs-lookup"><span data-stu-id="d23ad-169">If the table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="d23ad-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d23ad-170">Next steps</span></span>
<span data-ttu-id="d23ad-171">Confira estes tópicos para obter mais informações sobre o Azure Functions:</span><span class="sxs-lookup"><span data-stu-id="d23ad-171">For more information about Azure Functions, see the following topics:</span></span>

* [<span data-ttu-id="d23ad-172">Referência do desenvolvedor do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="d23ad-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="d23ad-173">Referência do programador para codificação de funções e definição de gatilhos e de associações.</span><span class="sxs-lookup"><span data-stu-id="d23ad-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="d23ad-174">Testando o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="d23ad-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="d23ad-175">Descreve várias ferramentas e técnicas para testar suas funções.</span><span class="sxs-lookup"><span data-stu-id="d23ad-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="d23ad-176">Como escalar o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="d23ad-176">How to scale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="d23ad-177">Discute os planos de serviço disponíveis com o Azure Functions, incluindo o plano de hospedagem de consumo e como escolher o plano certo.</span><span class="sxs-lookup"><span data-stu-id="d23ad-177">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

