---
title: "aaaCreate uma função que é executada em um agendamento no Azure | Microsoft Docs"
description: "Saiba como toocreate uma função no Azure que é executado com base em uma agenda que você definir."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a>Criar uma função no Azure que é disparada por um temporizador

Saiba como toouse funções do Azure toocreate uma função que é executada com base em uma agenda que você definir.

![Criar aplicativo de função em Olá portal do Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este tutorial:

+ Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Criar um Aplicativo de funções do Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Aplicativo de funções criado com êxito.](./media/functions-create-first-azure-function/function-app-create-success.png)

Em seguida, crie uma função no novo aplicativo de função hello.

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a>Criar uma função disparada por temporizador

1. Expanda seu aplicativo de função e clique em Olá  **+**  botão Avançar muito**funções**. Se esta for a primeira função hello em seu aplicativo de função, selecione **função personalizada**. Isso exibe o conjunto completo de saudação de modelos de função.

    ![Página de início rápido de funções no hello portal do Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. Selecione Olá **TimerTrigger** modelo para o idioma desejado. Use configurações de saudação conforme especificado na tabela de saudação:

    ![Crie uma função de temporizador disparado no Olá portal do Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | Configuração | Valor sugerido | Descrição |
    |---|---|---|
    | **Nomeie sua função** | TimerTriggerCSharp1 | Define o nome de saudação da sua função timer disparado. |
    | **[Agendamento](http://en.wikipedia.org/wiki/Cron#CRON_expression)** | 0 \*/1 \* \* \* \* | Um campo de seis [expressão CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) que agenda a cada minuto toorun sua função. |

2. Clique em **Criar**. Uma nova função na linguagem de programação escolhida por você e que é executada a cada minuto é criada.

3. Exibindo informações de rastreamento gravadas toohello logs, verifique se a execução.

    ![Visualizador de log de funções no portal do Azure de saudação.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

Agora, você pode alterar o agendamento da função Olá para que ele seja executado com menos frequência, como uma vez a cada hora. 

## <a name="update-hello-timer-schedule"></a>Agendamento de atualização de temporizador hello

1. Expanda sua função e clique em **Integrar**. Isso é onde você define a entrada e associações de saída de sua função e também definir a agenda de saudação. 

2. Insira um novo valor de **Agendamento** de `0 0 */1 * * *` e, em seguida, clique em **Salvar**.  

![Funções de atualizar a agenda de timer no hello portal do Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

Agora você tem uma função que é executada uma vez a cada hora. 

## <a name="clean-up-resources"></a>Limpar recursos

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Próximas etapas

Você criou uma função que é executada segundo um agendamento.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para obter mais informações sobre gatilhos de temporizador, consulte [Agendar a execução de código com o Azure Functions](functions-bindings-timer.md).