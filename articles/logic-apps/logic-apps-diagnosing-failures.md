---
title: "falhas de aaaDiagnose - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Toounderstand de maneiras comuns onde estão os aplicativos lógicos"
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
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="91714-103">Diagnosticar falhas nos aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="91714-103">Diagnose logic app failures</span></span>
<span data-ttu-id="91714-104">Se você enfrentar falhas ou problemas com seus aplicativos lógicos, existem algumas abordagens podem ajudá-lo a entender melhor onde falhas Olá são provenientes.</span><span class="sxs-lookup"><span data-stu-id="91714-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where hello failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="91714-105">Ferramentas do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="91714-105">Azure portal tools</span></span>
<span data-ttu-id="91714-106">Olá portal do Azure fornece muitos toodiagnose de ferramentas cada aplicativo lógica em cada etapa.</span><span class="sxs-lookup"><span data-stu-id="91714-106">hello Azure portal provides many tools toodiagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="91714-107">Histórico de gatilho</span><span class="sxs-lookup"><span data-stu-id="91714-107">Trigger history</span></span>

<span data-ttu-id="91714-108">Cada aplicativo lógico tem pelo menos um gatilho.</span><span class="sxs-lookup"><span data-stu-id="91714-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="91714-109">Se você perceber que os aplicativos não são acionados, procure primeiro no histórico de gatilho Olá para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="91714-109">If you notice that apps aren't firing, look first at hello trigger history for more information.</span></span> <span data-ttu-id="91714-110">Você pode acessar o histórico de gatilho Olá na folha principal da saudação lógica app'ss.</span><span class="sxs-lookup"><span data-stu-id="91714-110">You can access hello trigger history on hello logic app'ss main blade.</span></span>

![Localizando o histórico de gatilho Olá][1]

<span data-ttu-id="91714-112">histórico de gatilho Olá lista todas as tentativas de gatilho que seu aplicativo lógico feito.</span><span class="sxs-lookup"><span data-stu-id="91714-112">hello trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="91714-113">Você pode clicar em cada toodrill de tentativa de gatilho detalhes hello, especificamente, quaisquer entradas ou saídas que Olá tentativa de gatilho é gerado.</span><span class="sxs-lookup"><span data-stu-id="91714-113">You can click each trigger attempt toodrill into hello details, specifically, any inputs or outputs that hello trigger attempt generated.</span></span> <span data-ttu-id="91714-114">Se você encontrar gatilhos com falha, selecione tentativa de gatilho hello e escolha Olá **saídas** link tooreview quaisquer gerado mensagens de erro, por exemplo, as credenciais de FTP que não são válidos.</span><span class="sxs-lookup"><span data-stu-id="91714-114">If you find failed triggers, select hello trigger attempt and choose hello **Outputs** link tooreview any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="91714-115">Olá talvez você veja os status diferentes são:</span><span class="sxs-lookup"><span data-stu-id="91714-115">hello different statuses you might see are:</span></span>

* <span data-ttu-id="91714-116">**Ignorado**.</span><span class="sxs-lookup"><span data-stu-id="91714-116">**Skipped**.</span></span> <span data-ttu-id="91714-117">ponto de extremidade de saudação foi toocheck poll de dados e recebeu uma resposta que não havia dados disponíveis.</span><span class="sxs-lookup"><span data-stu-id="91714-117">hello endpoint was polled toocheck for data and received a response that no data was available.</span></span>
* <span data-ttu-id="91714-118">**Êxito**.</span><span class="sxs-lookup"><span data-stu-id="91714-118">**Succeeded**.</span></span> <span data-ttu-id="91714-119">gatilho Olá recebeu uma resposta que os dados estavam disponíveis.</span><span class="sxs-lookup"><span data-stu-id="91714-119">hello trigger received a response that data was available.</span></span> <span data-ttu-id="91714-120">Esse status pode ser resultado de um gatilho manual, um gatilho de recorrência ou um gatilho de sondagem.</span><span class="sxs-lookup"><span data-stu-id="91714-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="91714-121">Geralmente, esse status é acompanhado por Olá **acionado** status, mas não pode ser se você tiver uma condição ou um comando de SplitOn no modo de exibição de código que não foi atendido.</span><span class="sxs-lookup"><span data-stu-id="91714-121">This status is usually accompanied by hello **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="91714-122">**Falha**.</span><span class="sxs-lookup"><span data-stu-id="91714-122">**Failed**.</span></span> <span data-ttu-id="91714-123">Um erro foi gerado.</span><span class="sxs-lookup"><span data-stu-id="91714-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="91714-124">Iniciar um gatilho manualmente</span><span class="sxs-lookup"><span data-stu-id="91714-124">Start a trigger manually</span></span>

<span data-ttu-id="91714-125">Olá lógica aplicativo toocheck para um gatilho disponível imediatamente sem aguardar a próxima recorrência de saudação, clique em **Selecionar disparador** em Olá folha principal tooforce uma verificação.</span><span class="sxs-lookup"><span data-stu-id="91714-125">If you want hello logic app toocheck for an available trigger immediately without waiting for hello next recurrence, click **Select Trigger** on hello main blade tooforce a check.</span></span> <span data-ttu-id="91714-126">Por exemplo, clicar nesse link com um gatilho Dropbox faz sondagem tooimmediately de fluxo de trabalho Olá Dropbox para novos arquivos.</span><span class="sxs-lookup"><span data-stu-id="91714-126">For example, clicking this link with a Dropbox trigger causes hello workflow tooimmediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="91714-127">Histórico da execução</span><span class="sxs-lookup"><span data-stu-id="91714-127">Run history</span></span>

<span data-ttu-id="91714-128">Cada gatilho acionado resulta em uma execução.</span><span class="sxs-lookup"><span data-stu-id="91714-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="91714-129">Você pode acessar informações de execução da folha principal hello, que contém muitos detalhes que podem ajudá-lo a entender o que aconteceu durante o fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="91714-129">You can access run information from hello main blade, which contains many details that can help you understand what happened during hello workflow.</span></span>

![Localizando Olá histórico de execução][2]

<span data-ttu-id="91714-131">Uma execução exibe uma saudação status a seguir:</span><span class="sxs-lookup"><span data-stu-id="91714-131">A run displays one of hello following statuses:</span></span>

* <span data-ttu-id="91714-132">**Êxito**.</span><span class="sxs-lookup"><span data-stu-id="91714-132">**Succeeded**.</span></span> <span data-ttu-id="91714-133">Todas as ações foram bem sucedidas.</span><span class="sxs-lookup"><span data-stu-id="91714-133">All actions succeeded.</span></span> <span data-ttu-id="91714-134">Se ocorreu uma falha, essa falha era manipulada por uma ação que ocorreu posteriormente no fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="91714-134">If a failure happened, that failure was handled by an action that occurred later in hello workflow.</span></span> <span data-ttu-id="91714-135">Ou seja, falha de saudação foi tratada por uma ação que foi definida toorun depois de uma ação que falhou.</span><span class="sxs-lookup"><span data-stu-id="91714-135">That is, hello failure was handled by an action that was set toorun after a failed action.</span></span>
* <span data-ttu-id="91714-136">**Falha**.</span><span class="sxs-lookup"><span data-stu-id="91714-136">**Failed**.</span></span> <span data-ttu-id="91714-137">Pelo menos uma ação teve uma falha que não foi tratada por uma ação posteriormente no fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="91714-137">At least one action had a failure that was not handled by an action later in hello workflow.</span></span>
* <span data-ttu-id="91714-138">**Cancelado**.</span><span class="sxs-lookup"><span data-stu-id="91714-138">**Cancelled**.</span></span> <span data-ttu-id="91714-139">Olá estava em execução, mas recebeu uma solicitação de cancelamento.</span><span class="sxs-lookup"><span data-stu-id="91714-139">hello workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="91714-140">**Executando**.</span><span class="sxs-lookup"><span data-stu-id="91714-140">**Running**.</span></span> <span data-ttu-id="91714-141">fluxo de trabalho Hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="91714-141">hello workflow is currently running.</span></span> <span data-ttu-id="91714-142">Esse status pode ocorrer para fluxos de trabalho limitados ou devido a saudação atual plano de preços.</span><span class="sxs-lookup"><span data-stu-id="91714-142">This status might occur for throttled workflows, or because of hello current pricing plan.</span></span> <span data-ttu-id="91714-143">Para obter detalhes, consulte [limites de ação na página de preços de saudação](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="91714-143">For details, see [action limits on hello pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="91714-144">Configuração de diagnóstico (gráficos de saudação que apareçam no histórico de execução de saudação) também pode fornecer informações sobre os eventos de limitação acontecer.</span><span class="sxs-lookup"><span data-stu-id="91714-144">Configuring diagnostics (hello charts that appear under hello run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="91714-145">Quando você estiver observando um histórico da execução, você pode analisar para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="91714-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="91714-146">Saídas do gatilho</span><span class="sxs-lookup"><span data-stu-id="91714-146">Trigger outputs</span></span>

<span data-ttu-id="91714-147">Gatilho gera Mostrar dados Olá originários do gatilho de saudação.</span><span class="sxs-lookup"><span data-stu-id="91714-147">Trigger outputs show hello data that came from hello trigger.</span></span> <span data-ttu-id="91714-148">Essas saídas podem ajudá-lo a determinar se todas as propriedades retornaram conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="91714-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="91714-149">Se você vir algum conteúdo que não consegue compreender, aprenda como o Aplicativo Lógico do Azure [lida com diferentes tipos de conteúdo](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="91714-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Exemplos de saída do gatilho][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="91714-151">Entradas e saídas da ação</span><span class="sxs-lookup"><span data-stu-id="91714-151">Action inputs and outputs</span></span>

<span data-ttu-id="91714-152">Você pode analisar as entradas de saudação e saídas que recebeu uma ação.</span><span class="sxs-lookup"><span data-stu-id="91714-152">You can drill into hello inputs and outputs that an action received.</span></span> <span data-ttu-id="91714-153">Esses dados são úteis para entender o tamanho de saudação e a forma de saudação saídas e também para localizar qualquer mensagem de erro pode ter sido gerada.</span><span class="sxs-lookup"><span data-stu-id="91714-153">This data is useful for understanding hello size and shape of hello outputs, and also for finding any error messages that might have been generated.</span></span>

![Entradas e saídas da ação][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="91714-155">Tempo de execução do fluxo de trabalho de depuração</span><span class="sxs-lookup"><span data-stu-id="91714-155">Debug workflow runtime</span></span>

<span data-ttu-id="91714-156">Juntamente com hello entradas, saídas e gatilhos de uma execução de monitoramento, você pode adicionar etapas tooa fluxos de trabalho que ajudam com a depuração.</span><span class="sxs-lookup"><span data-stu-id="91714-156">Along with monitoring hello inputs, outputs, and triggers of a run, you could add some steps tooa workflow that help with debugging.</span></span> 
<span data-ttu-id="91714-157">[RequestBin](http://requestb.in) é uma ferramenta poderosa que você pode adicionar como uma etapa em um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="91714-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="91714-158">Usando RequestBin, você pode configurar um Inspetor toodetermine Olá exato tamanho da solicitação HTTP, forma e formato de uma solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="91714-158">By using RequestBin, you can set up an HTTP request inspector toodetermine hello exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="91714-159">Você pode criar um RequestBin e cole a URL de saudação em um aplicativo de lógica ação HTTP POST com conteúdo do corpo que você deseja tootest, por exemplo, uma expressão ou outra saída de etapa.</span><span class="sxs-lookup"><span data-stu-id="91714-159">You can create a RequestBin and paste hello URL in a logic app HTTP POST action with body content that you want tootest, for example, an expression or another step output.</span></span> <span data-ttu-id="91714-160">Após executar o aplicativo de lógica de saudação, você pode atualizar seu toosee RequestBin como solicitação Olá foi formada quando gerado do mecanismo de aplicativos lógicos hello.</span><span class="sxs-lookup"><span data-stu-id="91714-160">After you run hello logic app, you can refresh your RequestBin toosee how hello request was formed when generated from hello Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
