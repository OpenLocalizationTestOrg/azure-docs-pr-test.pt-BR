---
title: "Criar uma função executada segundo um agendamento no Azure | Microsoft Docs"
description: "Saiba como criar uma função no Azure que é executada com base em uma agendamento definido por você."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/03/2018
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 33f6cd9e10782bb8ff1b0ddf6d047aebc83f8008
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2018
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a>Criar uma função no Azure que é disparada por um temporizador

Saiba como usar o Azure Functions para criar uma função [sem servidor](https://azure.microsoft.com/overview/serverless-computing/) que é executada com base em um agendamento definido por você.

![Criar um aplicativo de funções no portal do Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>pré-requisitos

Para concluir este tutorial:

+ Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Criar um Aplicativo de funções do Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Aplicativo de funções criado com êxito.](./media/functions-create-first-azure-function/function-app-create-success.png)

Em seguida, crie uma nova função no novo aplicativo de funções.

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a>Criar uma função disparada por temporizador

1. Expanda seu aplicativo de funções e clique no botão **+** ao lado de **Functions**. Se essa for a primeira função em seu aplicativo de funções, selecione **Função personalizada**. Exibe o conjunto completo de modelos de função.

    ![Página de início rápido de funções no portal do Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. No campo de pesquisa, digite `timer` e depois escolha a linguagem desejada para o modelo de gatilho de temporizador. 

    ![Escolha o modelo de função disparada pelo temporizador.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

3. Configure o novo gatilho com as configurações conforme especificado na tabela abaixo da imagem.

    ![Criar uma função disparada pelo temporizador no portal do Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger-2.png)

    | Configuração | Valor sugerido | Descrição |
    |---|---|---|
    | **Nome** | Padrão | Define o nome da sua função disparada por temporizador. |
    | **[Agendamento](http://en.wikipedia.org/wiki/Cron#CRON_expression)** | 0 \*/1 \* \* \* \* | Uma [expressão CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) de seis campos que agenda sua função para ser executada a cada minuto. |

2. Clique em **Criar**. Uma nova função na linguagem de programação escolhida por você e que é executada a cada minuto é criada.

3. Verifique a execução, exibindo informações de rastreamento gravadas nos logs.

    ![Visualizador de log de função no Portal do Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

Agora você altera o agendamento da função para que ela seja executada uma vez por hora em vez de uma vez por minuto. 

## <a name="update-the-timer-schedule"></a>Atualizar o agendamento do temporizador

1. Expanda sua função e clique em **Integrar**. É aqui que você define as associações de entrada e saída de sua função e também define o agendamento. 

2. Insira um novo valor de **Agendamento** por hora de `0 0 */1 * * *` e depois clique em **Salvar**.  

![As funções atualizam o agendamento do temporizador no Portal do Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

Agora você tem uma função que é executada uma vez a cada hora. 

## <a name="clean-up-resources"></a>Limpar recursos

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Próximas etapas

Você criou uma função que é executada segundo um agendamento.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Para obter mais informações sobre gatilhos de temporizador, consulte [Agendar a execução de código com o Azure Functions](functions-bindings-timer.md).
