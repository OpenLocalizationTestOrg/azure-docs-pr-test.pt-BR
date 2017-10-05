---
title: "Criar uma função executada segundo um agendamento no Azure | Microsoft Docs"
description: "Saiba como criar uma função no Azure que é executada com base em uma agendamento definido por você."
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
ms.openlocfilehash: 03cc5e71e8eb20002cf58e713fc0fc92a9129874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="28412-103">Criar uma função no Azure que é disparada por um temporizador</span><span class="sxs-lookup"><span data-stu-id="28412-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="28412-104">Saiba como usar o Azure Functions para criar uma função que é executada com base em uma agendamento definido por você.</span><span class="sxs-lookup"><span data-stu-id="28412-104">Learn how to use Azure Functions to create a function that runs based a schedule that you define.</span></span>

![Criar um aplicativo de funções no portal do Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="28412-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="28412-106">Prerequisites</span></span>

<span data-ttu-id="28412-107">Para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="28412-107">To complete this tutorial:</span></span>

+ <span data-ttu-id="28412-108">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="28412-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="28412-109">Criar um Aplicativo de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="28412-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Aplicativo de funções criado com êxito.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="28412-111">Em seguida, crie uma nova função no novo aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="28412-111">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="28412-112">Criar uma função disparada por temporizador</span><span class="sxs-lookup"><span data-stu-id="28412-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="28412-113">Expanda seu aplicativo de funções e clique no botão **+** ao lado de **Functions**.</span><span class="sxs-lookup"><span data-stu-id="28412-113">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="28412-114">Se essa for a primeira função em seu aplicativo de funções, selecione **Função personalizada**.</span><span class="sxs-lookup"><span data-stu-id="28412-114">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="28412-115">Exibe o conjunto completo de modelos de função.</span><span class="sxs-lookup"><span data-stu-id="28412-115">This displays the complete set of function templates.</span></span>

    ![Página de início rápido de funções no portal do Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="28412-117">Selecione o modelo **TimerTrigger** para o idioma desejado.</span><span class="sxs-lookup"><span data-stu-id="28412-117">Select the **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="28412-118">Em seguida, use as configurações conforme especificado na tabela:</span><span class="sxs-lookup"><span data-stu-id="28412-118">Then use the settings as specified in the table:</span></span>

    ![Criar uma função disparada pelo temporizador no portal do Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="28412-120">Configuração</span><span class="sxs-lookup"><span data-stu-id="28412-120">Setting</span></span> | <span data-ttu-id="28412-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="28412-121">Suggested value</span></span> | <span data-ttu-id="28412-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="28412-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="28412-123">**Nomeie sua função**</span><span class="sxs-lookup"><span data-stu-id="28412-123">**Name your function**</span></span> | <span data-ttu-id="28412-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="28412-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="28412-125">Define o nome da sua função disparada por temporizador.</span><span class="sxs-lookup"><span data-stu-id="28412-125">Defines the name of your timer triggered function.</span></span> |
    | <span data-ttu-id="28412-126">**[Agendamento](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="28412-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="28412-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="28412-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="28412-128">Uma [expressão CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) de seis campos que agenda sua função para ser executada a cada minuto.</span><span class="sxs-lookup"><span data-stu-id="28412-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function to run every minute.</span></span> |

2. <span data-ttu-id="28412-129">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="28412-129">Click **Create**.</span></span> <span data-ttu-id="28412-130">Uma nova função na linguagem de programação escolhida por você e que é executada a cada minuto é criada.</span><span class="sxs-lookup"><span data-stu-id="28412-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="28412-131">Verifique a execução, exibindo informações de rastreamento gravadas nos logs.</span><span class="sxs-lookup"><span data-stu-id="28412-131">Verify execution by viewing trace information written to the logs.</span></span>

    ![Visualizador de log de função no Portal do Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="28412-133">Agora, você pode alterar o agendamento da função para que ela seja executada com menos frequência, por exemplo, uma vez por hora.</span><span class="sxs-lookup"><span data-stu-id="28412-133">Now, you can change the function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-the-timer-schedule"></a><span data-ttu-id="28412-134">Atualizar o agendamento do temporizador</span><span class="sxs-lookup"><span data-stu-id="28412-134">Update the timer schedule</span></span>

1. <span data-ttu-id="28412-135">Expanda sua função e clique em **Integrar**.</span><span class="sxs-lookup"><span data-stu-id="28412-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="28412-136">É aqui que você define as associações de entrada e saída de sua função e também define o agendamento.</span><span class="sxs-lookup"><span data-stu-id="28412-136">This is where you define input and output bindings for your function and also set the schedule.</span></span> 

2. <span data-ttu-id="28412-137">Insira um novo valor de **Agendamento** de `0 0 */1 * * *` e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="28412-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![As funções atualizam o agendamento do temporizador no Portal do Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="28412-139">Agora você tem uma função que é executada uma vez a cada hora.</span><span class="sxs-lookup"><span data-stu-id="28412-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="28412-140">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="28412-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="28412-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="28412-141">Next steps</span></span>

<span data-ttu-id="28412-142">Você criou uma função que é executada segundo um agendamento.</span><span class="sxs-lookup"><span data-stu-id="28412-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="28412-143">Para obter mais informações sobre gatilhos de temporizador, consulte [Agendar a execução de código com o Azure Functions](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="28412-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>