---
title: "aaaCreate uma função no Azure acionado por um webhook GitHub | Microsoft Docs"
description: "Use funções do Azure toocreate uma função sem servidor que é invocada por um webhook GitHub."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a>Criar uma função disparada pelo webhook do GitHub

Saiba como toocreate uma função que é disparada por uma solicitação de webhook HTTP com uma carga específica do GitHub.

![GitHub Webhook disparado função hello portal do Azure](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Pré-requisitos

+ Uma conta do GitHub com pelo menos um projeto.
+ Uma assinatura do Azure. Se você não tiver uma, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Criar um Aplicativo de funções do Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Aplicativo de funções criado com êxito.](./media/functions-create-first-azure-function/function-app-create-success.png)

Em seguida, crie uma função no novo aplicativo de função hello.

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a>Criar uma função disparada pelo webhook do GitHub

1. Expanda seu aplicativo de função e clique em Olá  **+**  botão Avançar muito**funções**. Se esta for a primeira função hello em seu aplicativo de função, selecione **função personalizada**. Isso exibe o conjunto completo de saudação de modelos de função.

    ![Página de início rápido de funções no hello portal do Azure](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. Selecione Olá **GitHub WebHook** modelo para o idioma desejado. **Nomeie sua função** e então selecione **Criar**.

     ![Criar uma função de webhook disparado GitHub em Olá portal do Azure](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. Em sua nova função, clique em **<> / Get função URL**, em seguida, copiar e salvar valores hello. Olá para a mesma coisa **<> / obter GitHub segredo**. Você pode usar essas webhook de saudação tooconfigure valores no GitHub.

    ![Examine o código de função hello](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

Em seguida, você cria o webhook no repositório GitHub.

## <a name="configure-hello-webhook"></a>Configurar Olá webhook

1. No GitHub, navegue tooa repositório que você possui. Você também pode usar qualquer repositório que você tenha bifurcado. Se você precisar toofork um repositório, use <https://github.com/Azure-Samples/functions-quickstart>.

1. Clique em **Configurações**, em seguida, clique em **Webhooks**, e **Adicionar webhook**.

    ![Adicionar um webhook do GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. Use as configurações conforme especificado na tabela Olá, e clique em **adicionar webhook**.

    ![Definir a URL do webhook hello e o segredo](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| Configuração | Valor sugerido | Descrição |
|---|---|---|
| **URL do conteúdo** | Valor copiado | Usar valor Olá retornado pela **<> / Get função URL**. |
| **Segredo**   | Valor copiado | Usar valor Olá retornado pela **<> / obter GitHub segredo**. |
| **Tipo de conteúdo** | aplicativo/json | função Hello espera uma carga JSON. |
| Gatilhos de evento | Deixe-me selecionar eventos individuais | Como só queremos tootrigger em eventos de comentário do problema.  |
| | Comentário do problema |  |

Agora, Olá webhook é configurado tootrigger sua função quando um novo comentário de problema é adicionado.

## <a name="test-hello-function"></a>Função de saudação do teste

1. No seu repositório GitHub, abra Olá **problemas** guia em uma nova janela do navegador.

1. Na nova janela de hello, clique em **novo problema**, digite um título e, em seguida, clique em **enviar novo problema**.

1. Edição de hello, digite um comentário e clique em **comentário**.

    ![Adicione um comentário de problema do GitHub.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. Voltar toohello portal e exibir logs de saudação. Você deve ver uma entrada de rastreamento com o novo texto de comentário hello.

     ![Exibir o texto de comentário hello nos logs de saudação.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a>Limpar recursos

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Próximas etapas

Você criou uma função que é executada quando uma solicitação é recebida de um webhook do GitHub.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para saber mais sobre gatilhos do webhook, veja [Associações HTTP e de webhook do Azure Functions](functions-bindings-http-webhook.md).
