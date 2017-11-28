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
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="41ecc-103">Criar uma função no Azure que é disparada por um temporizador</span><span class="sxs-lookup"><span data-stu-id="41ecc-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="41ecc-104">Saiba como toouse funções do Azure toocreate uma função que é executada com base em uma agenda que você definir.</span><span class="sxs-lookup"><span data-stu-id="41ecc-104">Learn how toouse Azure Functions toocreate a function that runs based a schedule that you define.</span></span>

![Criar aplicativo de função em Olá portal do Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="41ecc-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="41ecc-106">Prerequisites</span></span>

<span data-ttu-id="41ecc-107">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="41ecc-107">toocomplete this tutorial:</span></span>

+ <span data-ttu-id="41ecc-108">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="41ecc-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="41ecc-109">Criar um Aplicativo de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="41ecc-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Aplicativo de funções criado com êxito.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="41ecc-111">Em seguida, crie uma função no novo aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="41ecc-111">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="41ecc-112">Criar uma função disparada por temporizador</span><span class="sxs-lookup"><span data-stu-id="41ecc-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="41ecc-113">Expanda seu aplicativo de função e clique em Olá  **+**  botão Avançar muito**funções**.</span><span class="sxs-lookup"><span data-stu-id="41ecc-113">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="41ecc-114">Se esta for a primeira função hello em seu aplicativo de função, selecione **função personalizada**.</span><span class="sxs-lookup"><span data-stu-id="41ecc-114">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="41ecc-115">Isso exibe o conjunto completo de saudação de modelos de função.</span><span class="sxs-lookup"><span data-stu-id="41ecc-115">This displays hello complete set of function templates.</span></span>

    ![Página de início rápido de funções no hello portal do Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="41ecc-117">Selecione Olá **TimerTrigger** modelo para o idioma desejado.</span><span class="sxs-lookup"><span data-stu-id="41ecc-117">Select hello **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="41ecc-118">Use configurações de saudação conforme especificado na tabela de saudação:</span><span class="sxs-lookup"><span data-stu-id="41ecc-118">Then use hello settings as specified in hello table:</span></span>

    ![Crie uma função de temporizador disparado no Olá portal do Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="41ecc-120">Configuração</span><span class="sxs-lookup"><span data-stu-id="41ecc-120">Setting</span></span> | <span data-ttu-id="41ecc-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="41ecc-121">Suggested value</span></span> | <span data-ttu-id="41ecc-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="41ecc-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="41ecc-123">**Nomeie sua função**</span><span class="sxs-lookup"><span data-stu-id="41ecc-123">**Name your function**</span></span> | <span data-ttu-id="41ecc-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="41ecc-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="41ecc-125">Define o nome de saudação da sua função timer disparado.</span><span class="sxs-lookup"><span data-stu-id="41ecc-125">Defines hello name of your timer triggered function.</span></span> |
    | <span data-ttu-id="41ecc-126">**[Agendamento](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="41ecc-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="41ecc-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="41ecc-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="41ecc-128">Um campo de seis [expressão CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) que agenda a cada minuto toorun sua função.</span><span class="sxs-lookup"><span data-stu-id="41ecc-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function toorun every minute.</span></span> |

2. <span data-ttu-id="41ecc-129">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="41ecc-129">Click **Create**.</span></span> <span data-ttu-id="41ecc-130">Uma nova função na linguagem de programação escolhida por você e que é executada a cada minuto é criada.</span><span class="sxs-lookup"><span data-stu-id="41ecc-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="41ecc-131">Exibindo informações de rastreamento gravadas toohello logs, verifique se a execução.</span><span class="sxs-lookup"><span data-stu-id="41ecc-131">Verify execution by viewing trace information written toohello logs.</span></span>

    ![Visualizador de log de funções no portal do Azure de saudação.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="41ecc-133">Agora, você pode alterar o agendamento da função Olá para que ele seja executado com menos frequência, como uma vez a cada hora.</span><span class="sxs-lookup"><span data-stu-id="41ecc-133">Now, you can change hello function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-hello-timer-schedule"></a><span data-ttu-id="41ecc-134">Agendamento de atualização de temporizador hello</span><span class="sxs-lookup"><span data-stu-id="41ecc-134">Update hello timer schedule</span></span>

1. <span data-ttu-id="41ecc-135">Expanda sua função e clique em **Integrar**.</span><span class="sxs-lookup"><span data-stu-id="41ecc-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="41ecc-136">Isso é onde você define a entrada e associações de saída de sua função e também definir a agenda de saudação.</span><span class="sxs-lookup"><span data-stu-id="41ecc-136">This is where you define input and output bindings for your function and also set hello schedule.</span></span> 

2. <span data-ttu-id="41ecc-137">Insira um novo valor de **Agendamento** de `0 0 */1 * * *` e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="41ecc-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![Funções de atualizar a agenda de timer no hello portal do Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="41ecc-139">Agora você tem uma função que é executada uma vez a cada hora.</span><span class="sxs-lookup"><span data-stu-id="41ecc-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="41ecc-140">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="41ecc-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="41ecc-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="41ecc-141">Next steps</span></span>

<span data-ttu-id="41ecc-142">Você criou uma função que é executada segundo um agendamento.</span><span class="sxs-lookup"><span data-stu-id="41ecc-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="41ecc-143">Para obter mais informações sobre gatilhos de temporizador, consulte [Agendar a execução de código com o Azure Functions](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="41ecc-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>