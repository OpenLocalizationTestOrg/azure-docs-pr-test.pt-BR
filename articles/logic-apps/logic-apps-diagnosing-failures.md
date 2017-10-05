---
title: "Diagnosticar Falhas – Aplicativo Lógico do Azure | Microsoft Docs"
description: "Maneiras comuns de entender onde os aplicativos lógicos estão falhando"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 814e6f93088cdd96b0a663d2a7494b5a11470d99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="3297a-103">Diagnosticar falhas nos aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="3297a-103">Diagnose logic app failures</span></span>
<span data-ttu-id="3297a-104">Se você tiver problemas ou falhas com os aplicativos lógicos, há algumas abordagens que poderão ajudar a entender melhor a origem das falhas.</span><span class="sxs-lookup"><span data-stu-id="3297a-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where the failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="3297a-105">Ferramentas do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3297a-105">Azure portal tools</span></span>
<span data-ttu-id="3297a-106">O Portal do Azure fornece várias ferramentas para diagnosticar cada aplicativo lógico em cada etapa.</span><span class="sxs-lookup"><span data-stu-id="3297a-106">The Azure portal provides many tools to diagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="3297a-107">Histórico de gatilho</span><span class="sxs-lookup"><span data-stu-id="3297a-107">Trigger history</span></span>

<span data-ttu-id="3297a-108">Cada aplicativo lógico tem pelo menos um gatilho.</span><span class="sxs-lookup"><span data-stu-id="3297a-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="3297a-109">Se você perceber que os aplicativos não estão sendo acionados, procure mais informações no histórico de gatilho.</span><span class="sxs-lookup"><span data-stu-id="3297a-109">If you notice that apps aren't firing, look first at the trigger history for more information.</span></span> <span data-ttu-id="3297a-110">Você pode acessar o histórico de gatilhos na folha principal do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="3297a-110">You can access the trigger history on the logic app'ss main blade.</span></span>

![Exibir o histórico de gatilho][1]

<span data-ttu-id="3297a-112">O histórico de gatilho lista todas as tentativas de gatilho feitas pelo seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="3297a-112">The trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="3297a-113">Você pode clicar em cada tentativa de gatilho para ver os detalhes, mais especificamente, entradas ou saídas geradas pela tentativa de gatilho.</span><span class="sxs-lookup"><span data-stu-id="3297a-113">You can click each trigger attempt to drill into the details, specifically, any inputs or outputs that the trigger attempt generated.</span></span> <span data-ttu-id="3297a-114">Se você encontrar gatilhos com falha, selecione a tentativa de gatilho e escolha o link **Saídas** para examinar mensagens de erro geradas, por exemplo, para credenciais FTP que não são válidas.</span><span class="sxs-lookup"><span data-stu-id="3297a-114">If you find failed triggers, select the trigger attempt and choose the **Outputs** link to review any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="3297a-115">Os diferentes status que você pode ver são:</span><span class="sxs-lookup"><span data-stu-id="3297a-115">The different statuses you might see are:</span></span>

* <span data-ttu-id="3297a-116">**Ignorado**.</span><span class="sxs-lookup"><span data-stu-id="3297a-116">**Skipped**.</span></span> <span data-ttu-id="3297a-117">O ponto de extremidade foi sondado para procurar por dados e recebeu uma resposta de que nenhum dado estava disponível.</span><span class="sxs-lookup"><span data-stu-id="3297a-117">The endpoint was polled to check for data and received a response that no data was available.</span></span>
* <span data-ttu-id="3297a-118">**Êxito**.</span><span class="sxs-lookup"><span data-stu-id="3297a-118">**Succeeded**.</span></span> <span data-ttu-id="3297a-119">O gatilho recebeu uma resposta de que havia dados disponíveis.</span><span class="sxs-lookup"><span data-stu-id="3297a-119">The trigger received a response that data was available.</span></span> <span data-ttu-id="3297a-120">Esse status pode ser resultado de um gatilho manual, um gatilho de recorrência ou um gatilho de sondagem.</span><span class="sxs-lookup"><span data-stu-id="3297a-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="3297a-121">Esse status geralmente está acompanhado pelo status **Disparado**, mas poderá não estar se você tiver uma condição ou um comando SplitOn no modo de exibição de código que não foi atendido.</span><span class="sxs-lookup"><span data-stu-id="3297a-121">This status is usually accompanied by the **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="3297a-122">**Falha**.</span><span class="sxs-lookup"><span data-stu-id="3297a-122">**Failed**.</span></span> <span data-ttu-id="3297a-123">Um erro foi gerado.</span><span class="sxs-lookup"><span data-stu-id="3297a-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="3297a-124">Iniciar um gatilho manualmente</span><span class="sxs-lookup"><span data-stu-id="3297a-124">Start a trigger manually</span></span>

<span data-ttu-id="3297a-125">Se você quiser que o aplicativo lógico verifique imediatamente se há um gatilho disponível (sem aguardar a próxima recorrência), clique no botão **Selecionar Gatilho** na folha principal para forçar uma verificação.</span><span class="sxs-lookup"><span data-stu-id="3297a-125">If you want the logic app to check for an available trigger immediately without waiting for the next recurrence, click **Select Trigger** on the main blade to force a check.</span></span> <span data-ttu-id="3297a-126">Por exemplo, clicar nesse link com um gatilho Dropbox fará com que o fluxo de trabalho sonde o Dropbox imediatamente em busca de novos arquivos.</span><span class="sxs-lookup"><span data-stu-id="3297a-126">For example, clicking this link with a Dropbox trigger causes the workflow to immediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="3297a-127">Histórico da execução</span><span class="sxs-lookup"><span data-stu-id="3297a-127">Run history</span></span>

<span data-ttu-id="3297a-128">Cada gatilho acionado resulta em uma execução.</span><span class="sxs-lookup"><span data-stu-id="3297a-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="3297a-129">Você pode acessar informações de execução da folha principal, que contém muitos detalhes que podem ajudá-lo a entender o que aconteceu durante o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3297a-129">You can access run information from the main blade, which contains many details that can help you understand what happened during the workflow.</span></span>

![Localizando o histórico da execução][2]

<span data-ttu-id="3297a-131">Uma execução exibe um dos seguintes status:</span><span class="sxs-lookup"><span data-stu-id="3297a-131">A run displays one of the following statuses:</span></span>

* <span data-ttu-id="3297a-132">**Êxito**.</span><span class="sxs-lookup"><span data-stu-id="3297a-132">**Succeeded**.</span></span> <span data-ttu-id="3297a-133">Todas as ações foram bem sucedidas.</span><span class="sxs-lookup"><span data-stu-id="3297a-133">All actions succeeded.</span></span> <span data-ttu-id="3297a-134">Se uma falha ocorreu, ela foi tratada por uma ação que ocorreu posteriormente no fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3297a-134">If a failure happened, that failure was handled by an action that occurred later in the workflow.</span></span> <span data-ttu-id="3297a-135">Ou seja, a falha foi tratada por uma ação definida para ser executada depois de uma ação com falha.</span><span class="sxs-lookup"><span data-stu-id="3297a-135">That is, the failure was handled by an action that was set to run after a failed action.</span></span>
* <span data-ttu-id="3297a-136">**Falha**.</span><span class="sxs-lookup"><span data-stu-id="3297a-136">**Failed**.</span></span> <span data-ttu-id="3297a-137">Pelo menos uma ação teve uma falha que não foi tratada por uma ação posterior no fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3297a-137">At least one action had a failure that was not handled by an action later in the workflow.</span></span>
* <span data-ttu-id="3297a-138">**Cancelado**.</span><span class="sxs-lookup"><span data-stu-id="3297a-138">**Cancelled**.</span></span> <span data-ttu-id="3297a-139">O fluxo de trabalho estava em execução, mas recebeu uma solicitação de cancelamento.</span><span class="sxs-lookup"><span data-stu-id="3297a-139">The workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="3297a-140">**Executando**.</span><span class="sxs-lookup"><span data-stu-id="3297a-140">**Running**.</span></span> <span data-ttu-id="3297a-141">O fluxo de trabalho está em execução atualmente.</span><span class="sxs-lookup"><span data-stu-id="3297a-141">The workflow is currently running.</span></span> <span data-ttu-id="3297a-142">Esse status pode ocorrer para fluxos de trabalho limitados ou por conta do plano de preços atual.</span><span class="sxs-lookup"><span data-stu-id="3297a-142">This status might occur for throttled workflows, or because of the current pricing plan.</span></span> <span data-ttu-id="3297a-143">Para ver mais detalhes, confira os [limites da ação na página de preços](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="3297a-143">For details, see [action limits on the pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="3297a-144">Configurar o diagnóstico (os gráficos que aparecem embaixo do histórico da execução) também podem fornecer informações sobre quaisquer eventos de restrição ocorridos.</span><span class="sxs-lookup"><span data-stu-id="3297a-144">Configuring diagnostics (the charts that appear under the run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="3297a-145">Quando você estiver observando um histórico da execução, você pode analisar para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="3297a-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="3297a-146">Saídas do gatilho</span><span class="sxs-lookup"><span data-stu-id="3297a-146">Trigger outputs</span></span>

<span data-ttu-id="3297a-147">As saídas do gatilho mostrarão os dados recebidos do gatilho.</span><span class="sxs-lookup"><span data-stu-id="3297a-147">Trigger outputs show the data that came from the trigger.</span></span> <span data-ttu-id="3297a-148">Essas saídas podem ajudá-lo a determinar se todas as propriedades retornaram conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="3297a-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="3297a-149">Se você vir algum conteúdo que não consegue compreender, aprenda como o Aplicativo Lógico do Azure [lida com diferentes tipos de conteúdo](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="3297a-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Exemplos de saída do gatilho][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="3297a-151">Entradas e saídas da ação</span><span class="sxs-lookup"><span data-stu-id="3297a-151">Action inputs and outputs</span></span>

<span data-ttu-id="3297a-152">Você pode analisar as entradas e saídas que uma ação recebeu.</span><span class="sxs-lookup"><span data-stu-id="3297a-152">You can drill into the inputs and outputs that an action received.</span></span> <span data-ttu-id="3297a-153">Esses dados são úteis para entender o tamanho e a forma das saídas e para encontrar todas as mensagens de erro que possam ter sido geradas.</span><span class="sxs-lookup"><span data-stu-id="3297a-153">This data is useful for understanding the size and shape of the outputs, and also for finding any error messages that might have been generated.</span></span>

![Entradas e saídas da ação][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="3297a-155">Tempo de execução do fluxo de trabalho de depuração</span><span class="sxs-lookup"><span data-stu-id="3297a-155">Debug workflow runtime</span></span>

<span data-ttu-id="3297a-156">Juntamente com o monitoramento de entradas, saídas e gatilhos de uma execução, você pode adicionar algumas etapas ao fluxo de trabalho para ajudar na depuração.</span><span class="sxs-lookup"><span data-stu-id="3297a-156">Along with monitoring the inputs, outputs, and triggers of a run, you could add some steps to a workflow that help with debugging.</span></span> 
<span data-ttu-id="3297a-157">[RequestBin](http://requestb.in) é uma ferramenta poderosa que você pode adicionar como uma etapa em um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3297a-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="3297a-158">Usando o RequestBin, você pode configurar um inspetor de solicitação HTTP para determinar exatamente o tamanho, forma e formato de uma solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="3297a-158">By using RequestBin, you can set up an HTTP request inspector to determine the exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="3297a-159">Você pode criar um RequestBin e colar a URL em uma Ação HTTP POST do aplicativo lógico com qualquer conteúdo do corpo que você deseje testar, por exemplo, uma expressão ou outra saída da etapa.</span><span class="sxs-lookup"><span data-stu-id="3297a-159">You can create a RequestBin and paste the URL in a logic app HTTP POST action with body content that you want to test, for example, an expression or another step output.</span></span> <span data-ttu-id="3297a-160">Depois de executar o aplicativo lógico, você poderá atualizar o RequestBin para ver como a solicitação foi formada quando gerada do mecanismo dos Aplicativos Lógicos.</span><span class="sxs-lookup"><span data-stu-id="3297a-160">After you run the logic app, you can refresh your RequestBin to see how the request was formed when generated from the Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
