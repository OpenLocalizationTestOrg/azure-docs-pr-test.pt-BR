---
title: "uma função no Azure acionado por mensagens da fila de aaaCreate | Microsoft Docs"
description: "Use funções do Azure toocreate uma função sem servidor que é invocada por uma mensagem enviada tooan fila de armazenamento do Azure."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 0b609bc0-c264-4092-8e3e-0784dcc23b5d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/17/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 44db90fa80bf77e31bf53dddabd7136de5800b11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-messages-tooan-azure-storage-queue-using-functions"></a>Adicionar a fila mensagens tooan armazenamento do Azure usando funções

Em funções do Azure, as associações de entrada e saídas fornecem um forma declarativa tooconnect tooexternal serviço de dados de sua função. Neste tópico, Aprenda como tooupdate uma função existente, adicionando uma saída de associação que envia mensagens tooAzure armazenamento de fila.  

![Exibir mensagem nos logs de saudação.](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a>Pré-requisitos 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* Instalar Olá [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="add-binding"></a>Adicionar uma associação de saída
 
1. Expanda seu aplicativo de funções e sua função.

2. Selecione **Integrar** e **+ Nova saída**, escolha **Armazenamento de filas do Azure** e escolha **Selecionar**.
    
    ![Adicione uma função de tooa fila armazenamento saída associação em Olá portal do Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. Usar configurações de saudação conforme especificado na tabela de saudação: 

    ![Adicione uma função de tooa fila armazenamento saída associação em Olá portal do Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | Configuração      |  Valor sugerido   | Descrição                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nome da fila**   | myqueue-items    | nome de saudação do hello fila tooconnect tooin sua conta de armazenamento. |
    | **Conexão da conta de armazenamento** | AzureWebJobStorage | Você pode usar a conexão de conta de armazenamento Olá já está sendo usado pelo seu aplicativo de função ou criar um novo.  |
    | **Nome do parâmetro de mensagem** | outputQueueItem | nome de Olá Olá associação de parâmetro de saída. | 

4. Clique em **salvar** tooadd associação de saudação.
 
Agora que você tem uma associação de saída definida, você precisa tooupdate Olá código toouse Olá associação tooadd tooa fila de mensagens.  

## <a name="update-hello-function-code"></a>Atualizar o código de função hello

1. Selecione o código de função hello função toodisplay no editor de saudação. 

2. Para uma função c#, atualize sua definição de função, da seguinte maneira Olá tooadd **outputQueueItem** parâmetro de associação de armazenamento. Ignore esta etapa para uma função JavaScript.

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. Adicione Olá função toohello de código a seguir antes de método hello retorna. Use trecho apropriado Olá para o idioma de saudação da sua função.

    ```javascript
    context.bindings.outputQueueItem = "Name passed toohello function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed toohello function: " + name);     
    ```

4. Selecione **salvar** toosave alterações.

valor de saudação passado toohello gatilho HTTP é incluído em uma fila de mensagens toohello adicionado.
 
## <a name="test-hello-function"></a>Função de saudação do teste 

1. Depois que as alterações de código Olá são salvos, selecione **executar**. 

    ![Adicione uma função de tooa fila armazenamento saída associação em Olá portal do Azure.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. Verifique Olá logs toomake-se de que a função hello teve êxito. Uma nova fila denominada **outqueue** é criado na sua conta de armazenamento por Olá funções em tempo de execução quando a associação de saída de saudação é usado pela primeira vez.

Em seguida, você pode conectar tooyour armazenamento conta tooverify Olá nova fila e mensagem de saudação adicionado tooit. 

## <a name="connect-toohello-queue"></a>Conecte-se a fila de toohello

Ignorar Olá três primeiras etapas, se você já tiver instalado o Gerenciador de armazenamento e conectados a ele tooyour conta de armazenamento.    

1. Em sua função, escolha **integrar** e hello novo **armazenamento de fila do Azure** associação de saída, e então expanda **documentação**. Copie o **Nome da conta** e a **Chave de conta**. Você usar a conta de armazenamento essas credenciais tooconnect toohello.
 
    ![Obter credenciais de conexão de conta de armazenamento hello.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. Executar Olá [Microsoft Azure Storage Explorer](http://storageexplorer.com/) ferramenta, Olá selecione conectar ícone Olá esquerda, escolha **usar um nome de conta de armazenamento e chave**e selecione **próximo**.

    ![Execute a ferramenta de Gerenciador de conta de armazenamento de saudação.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. Saudação de colar **nome da conta** e **chave de conta** da etapa 1 para seus campos correspondentes, em seguida, selecione **próximo**, e **conectar**. 
  
    ![Cole as credenciais de armazenamento hello e conecte-se.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. Expanda a conta de armazenamento Olá anexado, **filas** e verifique se que uma fila denominada **myqueue itens** existe. Você também verá uma mensagem já na fila de saudação.  
 
    ![Crie uma fila de armazenamento.](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a>Limpar recursos

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Próximas etapas

Você adicionou uma função existente do tooan de associação de saída. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para obter mais informações sobre o armazenamento de tooQueue de associação, consulte [associações de fila de armazenamento do Azure funções](functions-bindings-storage-queue.md). 



