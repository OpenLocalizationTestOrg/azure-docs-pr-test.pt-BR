---
title: "condições de aaaAdd e iniciar os fluxos de trabalho - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Controle como os fluxos de trabalho são executados em Aplicativos Lógicos do Azure adicionando parâmetros, gatilhos, ações e lógica condicional."
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="47205-103">Usar recursos de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="47205-103">Use Logic Apps features</span></span>

<span data-ttu-id="47205-104">Em um [tópico anterior](../logic-apps/logic-apps-create-a-logic-app.md), você criou seu primeiro aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="47205-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="47205-105">toocontrol fluxo de trabalho lógica do aplicativo, você pode especificar um caminho diferente para o toorun do aplicativo de lógica e muito como processar dados em lotes, coleções e matrizes.</span><span class="sxs-lookup"><span data-stu-id="47205-105">toocontrol your logic app's workflow, you can specify different paths for your logic app toorun and how too process data in arrays, collections, and batches.</span></span> <span data-ttu-id="47205-106">Você pode incluir esses elementos no fluxo de trabalho do aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="47205-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="47205-107">Condições e [instruções switch](../logic-apps/logic-apps-switch-case.md) permitem que seu aplicativo lógico execute ações diferentes com base em se condições específicas são atendidas.</span><span class="sxs-lookup"><span data-stu-id="47205-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="47205-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) permitem que seu aplicativo lógico execute etapas repetidamente.</span><span class="sxs-lookup"><span data-stu-id="47205-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="47205-109">Por exemplo, você pode repetir ações em uma matriz quando usa um loop **For_each**.</span><span class="sxs-lookup"><span data-stu-id="47205-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="47205-110">Ou você pode repetir ações até que uma condição seja atendida quando usa um loop **Until**.</span><span class="sxs-lookup"><span data-stu-id="47205-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="47205-111">[Escopos](../logic-apps/logic-apps-loops-and-scopes.md) permitem agrupar série de ações, por exemplo, tooimplement tratamento de exceção.</span><span class="sxs-lookup"><span data-stu-id="47205-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, tooimplement exception handling.</span></span>

* <span data-ttu-id="47205-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) permite que seu aplicativo lógico iniciar fluxos de trabalho separados para itens em uma matriz ao usar Olá **SplitOn** comando.</span><span class="sxs-lookup"><span data-stu-id="47205-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use hello **SplitOn** command.</span></span>

<span data-ttu-id="47205-113">Este tópico apresenta outros conceitos para a criação de seu aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="47205-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="47205-114">Exibição tooedit um aplicativo existente da lógica de código</span><span class="sxs-lookup"><span data-stu-id="47205-114">Code view tooedit an existing logic app</span></span>
* <span data-ttu-id="47205-115">Opções para iniciar um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="47205-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="47205-116">Condições: executar etapas somente depois de atender a uma condição</span><span class="sxs-lookup"><span data-stu-id="47205-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="47205-117">toohave seu aplicativo lógico executar etapas somente quando os dados atendem a critérios específicos, você pode adicionar uma condição que compara dados no fluxo de trabalho de saudação em campos específicos ou valores.</span><span class="sxs-lookup"><span data-stu-id="47205-117">toohave your logic app run steps only when data meets specific criteria, you can add a condition that compares data in hello workflow against specific fields or values.</span></span>

<span data-ttu-id="47205-118">Por exemplo, suponha que você tem um aplicativo lógico que envia muitos emails para postagens no feed RSS de um site.</span><span class="sxs-lookup"><span data-stu-id="47205-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="47205-119">Você pode adicionar uma condição para que seu aplicativo lógico envia email somente quando lançar Olá nova categoria específica de tooa pertence.</span><span class="sxs-lookup"><span data-stu-id="47205-119">You can add a condition so that your logic app sends email only when hello new post belongs tooa specific category.</span></span>

1. <span data-ttu-id="47205-120">Em Olá [portal do Azure](https://portal.azure.com), localize e abra o aplicativo lógica no Designer de lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="47205-120">In hello [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="47205-121">Adicione um local de fluxo de trabalho toohello de condição que você deseja.</span><span class="sxs-lookup"><span data-stu-id="47205-121">Add a condition toohello workflow location that you want.</span></span> 

   <span data-ttu-id="47205-122">condição de saudação tooadd entre etapas existentes no fluxo de trabalho app de lógica Olá, mova o ponteiro de Olá sobre Seta Olá onde deseja que a condição de saudação tooadd.</span><span class="sxs-lookup"><span data-stu-id="47205-122">tooadd hello condition between existing steps in hello logic app workflow, move hello pointer over hello arrow where you want tooadd hello condition.</span></span> 
   <span data-ttu-id="47205-123">Escolha Olá **sinal** (**+**), em seguida, escolha **adicionar uma condição**.</span><span class="sxs-lookup"><span data-stu-id="47205-123">Choose hello **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="47205-124">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="47205-124">For example:</span></span>

   ![Adicionar condição toologic aplicativo](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="47205-126">Se você quiser tooadd uma condição no final de saudação do fluxo de trabalho atual, vá toohello inferior do seu aplicativo lógico e escolha **+ nova etapa**.</span><span class="sxs-lookup"><span data-stu-id="47205-126">If you want tooadd a condition at hello end of your current workflow, go toohello bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="47205-127">Defina condição de saudação.</span><span class="sxs-lookup"><span data-stu-id="47205-127">Now define hello condition.</span></span> <span data-ttu-id="47205-128">Especifique Olá campo de origem que você deseja tooevaluate, Olá operação tooperform e o valor de destino hello ou campo.</span><span class="sxs-lookup"><span data-stu-id="47205-128">Specify hello source field that you want tooevaluate, hello operation tooperform, and hello target value or field.</span></span> <span data-ttu-id="47205-129">tooadd existente campos tooyour condição, escolha Olá **Adicionar lista de conteúdo dinâmica**.</span><span class="sxs-lookup"><span data-stu-id="47205-129">tooadd existing fields tooyour condition, choose from hello **Add dynamic content list**.</span></span>

   <span data-ttu-id="47205-130">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="47205-130">For example:</span></span>

   ![Editar condição no modo básico](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="47205-132">Aqui está a condição completa hello:</span><span class="sxs-lookup"><span data-stu-id="47205-132">Here's hello complete condition:</span></span>

   ![Condição completa](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="47205-134">condição de saudação toodefine no código, escolha **Editar no modo avançado**.</span><span class="sxs-lookup"><span data-stu-id="47205-134">toodefine hello condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="47205-135">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="47205-135">For example:</span></span>
   > 
   > ![Editar condição no código](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="47205-137">Em **Sim se** e **não se**, adicionar Olá etapas tooperform com base em se Olá condição é atendida.</span><span class="sxs-lookup"><span data-stu-id="47205-137">Under **IF YES** and **IF NO**, add hello steps tooperform based on whether hello condition is met.</span></span>

   <span data-ttu-id="47205-138">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="47205-138">For example:</span></span>

   ![Condição com caminhos SIM e NÃO](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="47205-140">Você pode arrastar ações existentes para Olá **Sim se** e **não se** caminhos.</span><span class="sxs-lookup"><span data-stu-id="47205-140">You can drag existing actions into hello **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="47205-141">Quando terminar, salve o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="47205-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="47205-142">Agora você não receberá emails somente quando Olá postagens atendem a condição.</span><span class="sxs-lookup"><span data-stu-id="47205-142">Now you get emails only when hello posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="47205-143">Repita ações em uma lista com forEach</span><span class="sxs-lookup"><span data-stu-id="47205-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="47205-144">loop de forEach Olá Especifica uma matriz toorepeat uma ação.</span><span class="sxs-lookup"><span data-stu-id="47205-144">hello forEach loop specifies an array toorepeat an action over.</span></span> <span data-ttu-id="47205-145">Se não for uma matriz, fluxo Olá falhará.</span><span class="sxs-lookup"><span data-stu-id="47205-145">If it is not an array, hello flow fails.</span></span> <span data-ttu-id="47205-146">Por exemplo, se você tiver action1 que gera uma matriz de mensagens, e você quiser que cada mensagem toosend, você pode incluir essa instrução forEach nas propriedades de saudação da ação:`forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="47205-146">For example, if you have action1 that outputs an array of messages, and you want toosend each message, you can include this forEach statement in hello properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-hello-code-definition-for-a-logic-app"></a><span data-ttu-id="47205-147">Editar definição de código Olá para um aplicativo de lógica</span><span class="sxs-lookup"><span data-stu-id="47205-147">Edit hello code definition for a logic app</span></span>

<span data-ttu-id="47205-148">Embora você tenha Olá lógica de aplicativo Designer, você pode editar diretamente o código de saudação que define um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="47205-148">Although you have hello Logic App Designer, you can directly edit hello code that defines a logic app.</span></span>

1. <span data-ttu-id="47205-149">Na barra de comandos hello, escolha **exibição de código**.</span><span class="sxs-lookup"><span data-stu-id="47205-149">On hello command bar, choose **Code view**.</span></span>

    <span data-ttu-id="47205-150">Um editor completo é aberto e mostra a definição Olá editado.</span><span class="sxs-lookup"><span data-stu-id="47205-150">A full editor opens and shows hello definition you edited.</span></span>

    ![Visualização do código](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="47205-152">No editor de texto de saudação, você pode copiar e colar qualquer número de ações no hello mesmo aplicativo lógica ou entre aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="47205-152">In hello text editor, you can copy and paste any number of actions within hello same logic app or between logic apps.</span></span> 
    <span data-ttu-id="47205-153">Você pode facilmente adicionar ou remover seções inteiras da definição de saudação, e você também pode compartilhar definições com outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="47205-153">You can also easily add or remove entire sections from hello definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="47205-154">Escolha de suas edições, toosave **salvar**.</span><span class="sxs-lookup"><span data-stu-id="47205-154">toosave your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="47205-155">parâmetros</span><span class="sxs-lookup"><span data-stu-id="47205-155">Parameters</span></span>

<span data-ttu-id="47205-156">Alguns recursos de aplicativos lógicos como parâmetros estão disponíveis apenas na exibição de código.</span><span class="sxs-lookup"><span data-stu-id="47205-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="47205-157">Parâmetros tornam fácil tooreuse valores ao longo de seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="47205-157">Parameters make it easy tooreuse values throughout your logic app.</span></span> <span data-ttu-id="47205-158">Por exemplo, se você tiver um endereço de email que deseje usar em várias ações, deverá defini-lo como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="47205-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="47205-159">Parâmetros são bons para extrair os valores que são provavelmente toochange muito.</span><span class="sxs-lookup"><span data-stu-id="47205-159">Parameters are good for pulling out values that you are likely toochange a lot.</span></span> <span data-ttu-id="47205-160">Elas são especialmente úteis quando você precisar toooverride parâmetros em ambientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="47205-160">They are especially useful when you need toooverride parameters in different environments.</span></span> <span data-ttu-id="47205-161">toolearn como toooverride parâmetros com base no ambiente, consulte [criar definições de aplicativo lógica](../logic-apps/logic-apps-author-definitions.md) e [documentação da API REST](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="47205-161">toolearn how toooverride parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="47205-162">Este exemplo mostra como tooupdate seu aplicativo lógico existente para que você pode usar parâmetros para o termo de consulta hello.</span><span class="sxs-lookup"><span data-stu-id="47205-162">This example shows how tooupdate your existing logic app so that you can use parameters for hello query term.</span></span>

1. <span data-ttu-id="47205-163">No modo de exibição de código, localize Olá `parameters : {}` do objeto e, em seguida, adicione um `currentFeedUrl` objeto:</span><span class="sxs-lookup"><span data-stu-id="47205-163">In code view, find hello `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="47205-164">Vá toohello `When_a_feed-item_is_published` ação, localizar Olá `queries` seção e substitua o valor de consulta Olá com:`"feedUrl": "#@{parameters('currentFeedUrl')}"`</span><span class="sxs-lookup"><span data-stu-id="47205-164">Go toohello `When_a_feed-item_is_published` action, find hello `queries` section, and replace hello query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="47205-165">toojoin duas ou mais cadeias de caracteres, você também pode usar o hello `concat` função.</span><span class="sxs-lookup"><span data-stu-id="47205-165">toojoin two or more strings, you can also use hello `concat` function.</span></span> 
    <span data-ttu-id="47205-166">Por exemplo, `"@concat('#',parameters('currentFeedUrl'))"` funciona Olá mesmo como Olá acima.</span><span class="sxs-lookup"><span data-stu-id="47205-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works hello same as hello above.</span></span>

3.  <span data-ttu-id="47205-167">Quando terminar, escolha **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="47205-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="47205-168">Agora você pode alterar RSS do site Olá feed, passando uma URL diferente por meio de saudação `currentFeedURL` objeto.</span><span class="sxs-lookup"><span data-stu-id="47205-168">Now you can change hello website's RSS feed by passing a different URL through hello `currentFeedURL` object.</span></span>

<span data-ttu-id="47205-169">Saiba mais sobre [como definições de aplicativo de lógica de tooauthor](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="47205-169">Learn more about [how tooauthor logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="47205-170">Iniciar fluxos de trabalho de aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="47205-170">Start logic app workflows</span></span>

<span data-ttu-id="47205-171">Você tem opções diferentes para iniciar o fluxo de trabalho Olá definido no seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="47205-171">You have different options for starting hello workflow defined in your logic app.</span></span> <span data-ttu-id="47205-172">Você sempre pode iniciar uma fluxo de trabalho sob demanda no hello [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="47205-172">You can always start a workflow on-demand in hello [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="47205-173">Gatilhos de recorrência</span><span class="sxs-lookup"><span data-stu-id="47205-173">Recurrence triggers</span></span>

<span data-ttu-id="47205-174">Um gatilho de recorrência é executado em um intervalo especificado por você.</span><span class="sxs-lookup"><span data-stu-id="47205-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="47205-175">Quando o gatilho de saudação tem lógica condicional, gatilho Olá determina se o fluxo de trabalho de saudação deve toorun.</span><span class="sxs-lookup"><span data-stu-id="47205-175">When hello trigger has conditional logic, hello trigger determines whether hello workflow needs toorun.</span></span> <span data-ttu-id="47205-176">Um gatilho indica o fluxo de trabalho Olá deve ser executado, retornando um `200` código de status.</span><span class="sxs-lookup"><span data-stu-id="47205-176">A trigger indicates hello workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="47205-177">Quando o fluxo de trabalho de saudação não precisa toorun, gatilho Olá retorna um `202` código de status.</span><span class="sxs-lookup"><span data-stu-id="47205-177">When hello workflow doesn't need toorun, hello trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="47205-178">Retorno de chamada usando APIs REST</span><span class="sxs-lookup"><span data-stu-id="47205-178">Callback using REST APIs</span></span>

<span data-ttu-id="47205-179">toostart um fluxo de trabalho, serviços podem chamar um ponto de extremidade do aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="47205-179">toostart a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="47205-180">toostart esse tipo de lógica aplicativo sob demanda, escolha **executar agora** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="47205-180">toostart this kind of logic app on-demand, choose **Run now** on hello command bar.</span></span> <span data-ttu-id="47205-181">Consulte [Iniciar fluxos de trabalho chamando pontos de extremidade de aplicativo lógico como gatilhos](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="47205-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
[portal do Azure]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="47205-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="47205-183">Next steps</span></span>

* [<span data-ttu-id="47205-184">Instruções switch</span><span class="sxs-lookup"><span data-stu-id="47205-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="47205-185">Loops, escopos e debatching</span><span class="sxs-lookup"><span data-stu-id="47205-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="47205-186">Criar definições de aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="47205-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)