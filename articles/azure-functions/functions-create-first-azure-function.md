---
title: "aaaCreate sua primeira função da saudação Portal do Azure | Microsoft Docs"
description: "Saiba como toocreate do Azure a primeira função para a execução sem servidor usando Olá portal do Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a>Criar sua primeira função em Olá portal do Azure

As funções do Azure permite que você execute seu código em um ambiente sem servidor sem ter que toofirst criar uma VM ou publicar um aplicativo web. Neste tópico, Aprenda como toouse funções toocreate uma função de "hello world" hello portal do Azure.

![Criar aplicativo de função em Olá portal do Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a>Faça logon no tooAzure

Faça logon no toohello [portal do Azure](https://portal.azure.com/).

## <a name="create-a-function-app"></a>Criar um aplicativo de funções

Você deve ter uma função aplicativo toohost Olá a execução das funções. Um aplicativo de funções permite a você agrupar funções como uma unidade lógica para facilitar o gerenciamento, implantação e compartilhamento de recursos. 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

Em seguida, crie uma função no novo aplicativo de função hello.

## <a name="create-function"></a>Criar uma função disparada por HTTP

1. Expanda seu novo aplicativo de função, clique em Olá  **+**  botão Avançar muito**funções**.

2.  Em Olá **começar rapidamente** página, selecione **WebHook + API**, **escolher um idioma** para sua função e clique em **criar esta função** . 
   
    ![Início rápido de funções em Olá portal do Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

Uma função é criada no seu idioma escolhido usando o modelo de saudação para uma função HTTP disparado. Você pode executar uma nova função de saudação enviando uma solicitação HTTP.

## <a name="test-hello-function"></a>Função de saudação do teste

1. Em sua nova função, clique em **</> Obter URL da função**, selecione **padrão (Tecla de função)** e clique em **Copiar**. 

    ![Copiar URL da função de saudação do hello portal do Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. Cole Olá função URL na barra de endereços do navegador. Acrescente a cadeia de caracteres de consulta de saudação `&name=<yourname>` Olá de URL e pressione toothis `Enter` chave em sua solicitação de saudação do teclado tooexecute. a seguir Olá é um exemplo de resposta Olá retornado pela função hello no navegador de borda hello:

    ![Resposta de função no navegador de saudação.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    solicitação de saudação URL inclui uma chave que é necessário, por padrão, tooaccess sua função via HTTP.   

3. Quando a função é executada, informações de rastreamento são gravadas toohello logs. saída de rastreamento de saudação toosee de execução anterior do hello, retornar tooyour função no portal de saudação e clique em Olá a seta na parte inferior de saudação do hello tela tooexpand **Logs**. 

   ![Visualizador de log de funções no portal do Azure de saudação.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a>Limpar recursos

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Próximas etapas

Você criou um aplicativo de funções com uma função simples disparada por HTTP.  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para obter mais informações, consulte [Associações HTTP e de webhook do Azure Functions](functions-bindings-http-webhook.md).



