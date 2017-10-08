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
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a>Use as funções do Azure toocreate uma função que se conecta tooother do Azure services

Este tópico mostra como toocreate uma função em funções do Azure que escuta toomessages em uma saudação de fila e cópias do armazenamento do Azure mensagens toorows em uma tabela de armazenamento do Azure. Uma função de temporizador disparado é usado tooload mensagens na fila de saudação. Uma segunda função lê da fila de saudação e grava a tabela de toohello de mensagens. Fila hello e tabela Olá são criadas para você por funções do Azure com base nas definições de associação de saudação. 

coisas toomake mais interessantes, uma função é escrita em JavaScript e outros Olá é gravado no script c#. Isso demonstra como um aplicativo de funções pode ter funções em várias linguagens. 

Você pode ver esse cenário demonstrado em um [vídeo no Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).

## <a name="create-a-function-that-writes-toohello-queue"></a>Crie uma função que grava toohello fila

Antes de poder conectar tooa fila de armazenamento, você precisa toocreate uma função que carrega a fila de mensagens de saudação. Essa função de JavaScript usa um gatilho de timer que grava uma fila de mensagens toohello cada 10 segundos. Se você ainda não tiver uma conta do Azure, confira Olá [funções do Azure tente](https://functions.azure.com/try) experiência, ou [criar sua conta gratuita do Azure](https://azure.microsoft.com/free/).

1. Vá toohello portal do Azure e localize seu aplicativo de função.

2. Clique em **Nova Função** > **TimerTrigger-JavaScript**. 

3. Nome de função hello **FunctionsBindingsDemo1**, digite um valor de expressão cron de `0/10 * * * * *` para **agenda**e, em seguida, clique em **criar**.
   
    ![Adicionar uma função disparada por temporizador](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    Você criou uma função disparada por temporizador que é executada a cada 10 segundos.

5. Em Olá **desenvolver** , clique em **Logs** e exibir a atividade de Olá no log de saudação. Você vê uma entrada de log gravada a cada 10 segundos.
   
    ![Exibir hello log tooverify Olá função funciona](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a>Adicionar uma associação de saída de fila de mensagens

1. Em Olá **integrar** guia, escolha **nova saída** > **armazenamento de fila do Azure** > **selecione**.

    ![Adicionar uma função de temporizador de gatilho](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. Digite `myQueueItem` para **nome de parâmetro de mensagem** e `functions-bindings` para **nome de fila**, selecione uma existente **conexão da conta de armazenamento** ou clique em **novo** toocreate um armazenamento de conta de conexão e, em seguida, clique em **salvar**.  

    ![Criar fila de armazenamento Olá saída associação toohello](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. Em Olá **desenvolver** guia, acrescentar Olá função toohello de código a seguir:
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. Localizar Olá *se* em torno de instrução linha 9 da função hello e de código a seguir de saudação insert após essa instrução.
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    Esse código cria um **myQueueItem** e define seu **tempo** toohello propriedade carimbo de hora atual. Em seguida, adiciona Olá nova fila item toohello do contexto **myQueueItem** associação.

3. Clique em **Salvar e Executar**.

## <a name="view-storage-updates-by-using-storage-explorer"></a>Exibir atualizações de armazenamento usando o Gerenciador de Armazenamento
Você pode verificar se a função está funcionando, exibindo mensagens na fila Olá que você criou.  Você pode se conectar a fila de armazenamento tooyour usando o Pesquisador de objetos de nuvem no Visual Studio. No entanto, portal Olá torna fácil tooconnect conta de armazenamento de tooyour usando o Microsoft Azure Storage Explorer.

1. Em Olá **integrar** , clique em sua fila de associação de saída > **documentação**, reexibir hello cadeia de caracteres de Conexão para sua conta de armazenamento e copie o valor de saudação. Você usar essa conta de armazenamento do valor tooconnect tooyour.

    ![Baixar o Gerenciador de Armazenamento do Azure](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. Se você ainda não fez isso, baixe e instale o [Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com). 
 
3. No Gerenciador de armazenamento, clique em Olá tooAzure armazenamento ícone connect, cole a cadeia de caracteres de conexão de Olá no campo hello e conclua o Assistente de saudação.

    ![Gerenciador de Armazenamento – adicionar uma conexão](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. Em **Local e anexado**, expanda **contas de armazenamento** > sua conta de armazenamento > **filas** > **deassociaçõesdefunções**e verifique se que as mensagens são escritas toohello fila.

    ![Exibição de mensagens na fila de saudação](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    Se a fila de saudação não existe ou está vazia, provavelmente há um problema com sua associação de função ou o código.

## <a name="create-a-function-that-reads-from-hello-queue"></a>Criar uma função que lê da fila de saudação

Agora que você tem que está sendo adicionadas toohello fila de mensagens, você pode criar outra função que lê da fila de saudação e gravações Olá permanentemente mensagens tooan tabela de armazenamento do Azure.

1. Clique em **Nova Função** > **QueueTrigger-CSharp**. 
 
2. Nome de função hello `FunctionsBindingsDemo2`, digite **associações a funções** em Olá **nome da fila** campo, selecione uma conta de armazenamento existente ou crie um e, em seguida, clique em **criar**.

    ![Adicionar uma função de temporizador de fila de saída](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. (Opcional) Você pode verificar que nova função de saudação funciona exibindo a nova fila de saudação no Gerenciador de armazenamento como antes. Você também pode usar o Cloud Explorer no Visual Studio.  

4. (Opcional) Atualizar Olá **associações a funções** fila e observe que os itens foram removidos da fila de saudação. Hello remoção ocorre porque a função hello é toohello associado **associações a funções** como uma função de gatilho e hello entrada lê a fila de saudação da fila. 
 
## <a name="add-a-table-output-binding"></a>Adicionar uma associação de saída da tabela

1. Em FunctionsBindingsDemo2, clique em **Integrar** > **Nova Saída** > **Armazenamento de Tabela do Azure** > **Selecionar**.

    ![Adicionar uma tabela de armazenamento do Azure associação tooan](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. Insira `functionbindings` para **Nome de tabela** e `myTable` para **Nome de parâmetro de tabela**, escolha uma **Conexão da conta de armazenamento** ou crie uma nova e, em seguida, clique em **Salvar**.

    ![Configurar a associação de tabela de armazenamento Olá](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. Em Olá **desenvolver** guia, substitua o código de função existente Olá pela seguinte hello:
   
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
    Olá **TableItem** classe representa uma linha na tabela de armazenamento hello e adicionar Olá item toohello `myTable` coleção de **TableItem** objetos. Você deve definir Olá **PartitionKey** e **RowKey** propriedades toobe capaz de tooinsert na tabela de saudação.

4. Clique em **Salvar**.  Por fim, você pode verificar Olá função funciona exibindo tabela de saudação no Gerenciador de armazenamento ou o Gerenciador de nuvem do Visual Studio.

5. (Opcional) Na sua conta de armazenamento no Gerenciador de armazenamento, expanda **tabelas** > **functionsbindings** e verifique se que linhas são adicionadas toohello tabela. Você pode fazer Olá mesmo no Gerenciador de nuvem no Visual Studio.

    ![Exibição de linhas na tabela de saudação](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    Se a tabela de saudação não existe ou está vazia, provavelmente há um problema com sua associação de função ou o código. 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre as funções do Azure, consulte Olá seguintes tópicos:

* [Referência do desenvolvedor do Azure Functions](functions-reference.md)  
  Referência do programador para codificação de funções e definição de gatilhos e de associações.
* [Testando o Azure Functions](functions-test-a-function.md)  
  Descreve várias ferramentas e técnicas para testar suas funções.
* [Como tooscale funções do Azure](functions-scale.md)  
  Discute os planos de serviço disponíveis com as funções do Azure, incluindo o plano de hospedagem de consumo hello e como toochoose Olá plano à direita. 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

