---
title: "aaaSchema atualizações 1 2016 junho - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Criar definições de JSON para Aplicativos Lógicos do Azure com a versão de esquema 2016-06-01"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/25/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: b0347fbbd692a93b63a2f8b741402a225450b35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="87fd6-103">Atualizações de esquema para Aplicativos Lógicos do Azure - 1º de junho de 2016</span><span class="sxs-lookup"><span data-stu-id="87fd6-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="87fd6-104">Esse novo esquema e a API de versão para os aplicativos lógicos do Azure inclui aprimoramentos importantes que tornam os aplicativos lógicos mais toouse mais fácil e confiável:</span><span class="sxs-lookup"><span data-stu-id="87fd6-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

* <span data-ttu-id="87fd6-105">[Escopos](#scopes) permitem agrupar ou aninhar ações como uma coleção de ações.</span><span class="sxs-lookup"><span data-stu-id="87fd6-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="87fd6-106">[Condições e loops](#conditions-loops) agora são ações de primeira classe.</span><span class="sxs-lookup"><span data-stu-id="87fd6-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="87fd6-107">Ordenação mais precisa para executar ações com hello `runAfter` propriedade, substituindo`dependsOn`</span><span class="sxs-lookup"><span data-stu-id="87fd6-107">More precise ordering for running actions with hello `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="87fd6-108">tooupgrade seus aplicativos de lógica de Olá 1 de agosto de 2015 preview esquema toohello esquema de 1º de junho de 2016, [Confira a seção Atualizar Olá](##upgrade-your-schema).</span><span class="sxs-lookup"><span data-stu-id="87fd6-108">tooupgrade your logic apps from hello August 1, 2015 preview schema toohello June 1, 2016 schema, [check out hello upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="87fd6-109">Escopos</span><span class="sxs-lookup"><span data-stu-id="87fd6-109">Scopes</span></span>

<span data-ttu-id="87fd6-110">Esse esquema inclui escopos, que permitem agrupar ações ou aninhar ações umas dentro das outras.</span><span class="sxs-lookup"><span data-stu-id="87fd6-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="87fd6-111">Por exemplo, uma condição pode conter outra condição.</span><span class="sxs-lookup"><span data-stu-id="87fd6-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="87fd6-112">Saiba mais sobre a [sintaxe de escopo](../logic-apps/logic-apps-loops-and-scopes.md) ou examine este exemplo básico de escopo:</span><span class="sxs-lookup"><span data-stu-id="87fd6-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="87fd6-113">Alterações de condições e loops</span><span class="sxs-lookup"><span data-stu-id="87fd6-113">Conditions and loops changes</span></span>

<span data-ttu-id="87fd6-114">Em versões de esquema anteriores, condições e loops eram parâmetros associados a uma única ação.</span><span class="sxs-lookup"><span data-stu-id="87fd6-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="87fd6-115">Esse esquema remove essa limitação; portanto, condições e loops agora aparecem como tipos de ação.</span><span class="sxs-lookup"><span data-stu-id="87fd6-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="87fd6-116">Saiba mais sobre [loops e escopos](../logic-apps/logic-apps-loops-and-scopes.md) ou examine este exemplo básico de uma ação de condição:</span><span class="sxs-lookup"><span data-stu-id="87fd6-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>
## <a name="runafter-property"></a><span data-ttu-id="87fd6-117">Propriedade 'runAfter'</span><span class="sxs-lookup"><span data-stu-id="87fd6-117">'runAfter' property</span></span>

<span data-ttu-id="87fd6-118">Olá `runAfter` propriedade substitui `dependsOn`, fornecendo mais precisão quando você especifica a ordem Olá executar ações com base no status de saudação das ações anteriores.</span><span class="sxs-lookup"><span data-stu-id="87fd6-118">hello `runAfter` property replaces `dependsOn`, providing more precision when you specify hello run order for actions based on hello status of previous actions.</span></span>

<span data-ttu-id="87fd6-119">Olá `dependsOn` propriedade era sinônimo de "ação Olá foi executado e foi bem-sucedida", não importa quantas vezes desejar tooexecute uma ação com base em se a ação anterior Olá teve êxito, falha ou ignoradas.</span><span class="sxs-lookup"><span data-stu-id="87fd6-119">hello `dependsOn` property was synonymous with "hello action ran and was successful", no matter how many times you wanted tooexecute an action, based on whether hello previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="87fd6-120">Olá `runAfter` propriedade proporciona essa flexibilidade como um objeto que especifica todos os Olá nomes de ação após o qual hello objeto é executado.</span><span class="sxs-lookup"><span data-stu-id="87fd6-120">hello `runAfter` property provides that flexibility as an object that specifies all hello action names after which hello object runs.</span></span> <span data-ttu-id="87fd6-121">Essa propriedade também define uma matriz de status aceitável como disparadores.</span><span class="sxs-lookup"><span data-stu-id="87fd6-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="87fd6-122">Por exemplo, se você quisesse toorun depois de passo A passo é bem-sucedida e também depois B êxito ou falha, você construir isso `runAfter` propriedade:</span><span class="sxs-lookup"><span data-stu-id="87fd6-122">For example, if you wanted toorun after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="87fd6-123">Atualizar o esquema</span><span class="sxs-lookup"><span data-stu-id="87fd6-123">Upgrade your schema</span></span>

<span data-ttu-id="87fd6-124">Atualizando toohello novo esquema tem apenas algumas etapas.</span><span class="sxs-lookup"><span data-stu-id="87fd6-124">Upgrading toohello new schema only takes a few steps.</span></span> <span data-ttu-id="87fd6-125">Olá processo de atualização inclui a execução de script de atualização hello, salvar como um novo aplicativo de lógica e, se desejar, possivelmente substitui o aplicativo lógico anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="87fd6-125">hello upgrade process includes running hello upgrade script, saving as a new logic app, and if you want, possibly overwriting hello previous logic app.</span></span>

1. <span data-ttu-id="87fd6-126">No portal do Azure de Olá, abra o aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="87fd6-126">In hello Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="87fd6-127">Vá muito**visão geral**.</span><span class="sxs-lookup"><span data-stu-id="87fd6-127">Go too**Overview**.</span></span> <span data-ttu-id="87fd6-128">Na barra de ferramentas do hello lógica aplicativo, escolha **atualizar esquema**.</span><span class="sxs-lookup"><span data-stu-id="87fd6-128">On hello logic app toolbar, choose **Update Schema**.</span></span>
   
    ![Escolher o Esquema de Atualização][1]
   
    <span data-ttu-id="87fd6-130">Olá definição atualizada for retornada, que você pode copiar e colar em uma definição de recurso, se necessário.</span><span class="sxs-lookup"><span data-stu-id="87fd6-130">hello upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="87fd6-131">No entanto, podemos **altamente recomendável** você escolher **Salvar como** toomake-se de que todas as referências de conexão são válidas em Olá atualizado o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="87fd6-131">However, we **strongly recommend** you choose **Save As** toomake sure that all connection references are valid in hello upgraded logic app.</span></span>

3. <span data-ttu-id="87fd6-132">Na barra de ferramentas de atualização de folha hello, escolha **Salvar como**.</span><span class="sxs-lookup"><span data-stu-id="87fd6-132">In hello upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="87fd6-133">Insira o nome de lógica de saudação e status.</span><span class="sxs-lookup"><span data-stu-id="87fd6-133">Enter hello logic name and status.</span></span> <span data-ttu-id="87fd6-134">toodeploy seu aplicativo atualizado lógica, escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="87fd6-134">toodeploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="87fd6-135">Confirme se o aplicativo lógico atualizado funciona conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="87fd6-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="87fd6-136">Se você estiver usando um gatilho manual ou de solicitação, URL de retorno de chamada hello alterações em seu novo aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="87fd6-136">If you are using a manual or request trigger, hello callback URL changes in your new logic app.</span></span> <span data-ttu-id="87fd6-137">Teste Olá nova URL toomake se Olá-ponta a experiência funciona.</span><span class="sxs-lookup"><span data-stu-id="87fd6-137">Test hello new URL toomake sure hello end-to-end experience works.</span></span> <span data-ttu-id="87fd6-138">URLs do toopreserve anterior, você pode clonar sobre a lógica do aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="87fd6-138">toopreserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="87fd6-139">*Opcional* toooverwrite seu aplicativo lógico anterior com a nova versão de esquema hello, na barra de ferramentas hello, escolha **Clone**, Avançar muito**atualizar esquema**.</span><span class="sxs-lookup"><span data-stu-id="87fd6-139">*Optional* toooverwrite your previous logic app with hello new schema version, on hello toolbar, choose **Clone**, next too**Update Schema**.</span></span> <span data-ttu-id="87fd6-140">Essa etapa é necessária somente se você quiser tookeep Olá mesmo recurso ID ou a solicitação de URL do gatilho de seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="87fd6-140">This step is necessary only if you want tookeep hello same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="87fd6-141">Observações sobre a ferramenta de atualização</span><span class="sxs-lookup"><span data-stu-id="87fd6-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="87fd6-142">Condições de mapeamento</span><span class="sxs-lookup"><span data-stu-id="87fd6-142">Mapping conditions</span></span>

<span data-ttu-id="87fd6-143">Na definição de saudação atualizada, ferramenta de saudação se esforça em Agrupar ações de ramificação true e false como um escopo.</span><span class="sxs-lookup"><span data-stu-id="87fd6-143">In hello upgraded definition, hello tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="87fd6-144">Especificamente, Olá designer padrão de `@equals(actions('a').status, 'Skipped')` devem aparecer como um `else` ação.</span><span class="sxs-lookup"><span data-stu-id="87fd6-144">Specifically, hello designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="87fd6-145">No entanto, se a ferramenta Olá detectar padrões irreconhecíveis, ferramenta Olá pode criar condições separadas para true hello e a ramificação falsa hello.</span><span class="sxs-lookup"><span data-stu-id="87fd6-145">However, if hello tool detects unrecognizable patterns, hello tool might create separate conditions for both hello true and hello false branch.</span></span> <span data-ttu-id="87fd6-146">É possível remapear ações após a atualização, se necessário.</span><span class="sxs-lookup"><span data-stu-id="87fd6-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="87fd6-147">loop 'foreach' com condição</span><span class="sxs-lookup"><span data-stu-id="87fd6-147">'foreach' loop with condition</span></span>

<span data-ttu-id="87fd6-148">No novo esquema de saudação, você pode usar o padrão de Olá Olá filtro ação tooreplicate de um `foreach` loop com uma condição por item, mas essa alteração automaticamente deve acontecer quando você atualiza.</span><span class="sxs-lookup"><span data-stu-id="87fd6-148">In hello new schema, you can use hello filter action tooreplicate hello pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="87fd6-149">condição de saudação torna-se uma ação de filtro antes de loop de foreach Olá para retornar apenas uma matriz de itens que correspondem à condição de saudação e essa matriz é passada para a ação de foreach hello.</span><span class="sxs-lookup"><span data-stu-id="87fd6-149">hello condition becomes a filter action before hello foreach loop for returning only an array of items that match hello condition, and that array is passed into hello foreach action.</span></span> <span data-ttu-id="87fd6-150">Para obter um exemplo, confira [Loops e escopos](../logic-apps/logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="87fd6-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="87fd6-151">Marcações de recursos</span><span class="sxs-lookup"><span data-stu-id="87fd6-151">Resource tags</span></span>

<span data-ttu-id="87fd6-152">Depois de atualizar, marcas de recurso são removidas, portanto você deverá redefini-los para fluxo de trabalho Olá atualizado.</span><span class="sxs-lookup"><span data-stu-id="87fd6-152">After you upgrade, resource tags are removed, so you must reset them for hello upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="87fd6-153">Outras alterações</span><span class="sxs-lookup"><span data-stu-id="87fd6-153">Other changes</span></span>

### <a name="renamed-manual-trigger-toorequest-trigger"></a><span data-ttu-id="87fd6-154">Renomear o gatilho 'manual' too'request' gatilho</span><span class="sxs-lookup"><span data-stu-id="87fd6-154">Renamed 'manual' trigger too'request' trigger</span></span>

<span data-ttu-id="87fd6-155">Olá `manual` tipo de disparador foi preterido e renomeado muito`request` com tipo `http`.</span><span class="sxs-lookup"><span data-stu-id="87fd6-155">hello `manual` trigger type was deprecated and renamed too`request` with type `http`.</span></span> <span data-ttu-id="87fd6-156">Essa alteração cria mais consistência para o tipo de saudação do padrão que Olá gatilho é toobuild usado.</span><span class="sxs-lookup"><span data-stu-id="87fd6-156">This change creates more consistency for hello kind of pattern that hello trigger is used toobuild.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="87fd6-157">Nova ação 'filter'</span><span class="sxs-lookup"><span data-stu-id="87fd6-157">New 'filter' action</span></span>

<span data-ttu-id="87fd6-158">toofilter uma matriz grande conjunto de itens, Olá novo menor tooa `filter` tipo aceita uma matriz e uma condição, avalia a condição Olá para cada item e retorna uma matriz com itens que atendem a condição de saudação.</span><span class="sxs-lookup"><span data-stu-id="87fd6-158">toofilter a large array down tooa smaller set of items, hello new `filter` type accepts an array and a condition, evaluates hello condition for each item, and returns an array with items meeting hello condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="87fd6-159">Restrições às ações 'foreach' e 'until'</span><span class="sxs-lookup"><span data-stu-id="87fd6-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="87fd6-160">Olá `foreach` e `until` loop são restritos tooa única ação.</span><span class="sxs-lookup"><span data-stu-id="87fd6-160">hello `foreach` and `until` loop are restricted tooa single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="87fd6-161">Novo 'trackedProperties' para ações</span><span class="sxs-lookup"><span data-stu-id="87fd6-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="87fd6-162">Ações agora podem ter uma propriedade adicional chamada `trackedProperties`, que é irmão toohello `runAfter` e `type` propriedades.</span><span class="sxs-lookup"><span data-stu-id="87fd6-162">Actions can now have an additional property called `trackedProperties`, which is sibling toohello `runAfter` and `type` properties.</span></span> <span data-ttu-id="87fd6-163">Esse objeto especifica certas entradas de ação ou saídas que você deseja tooinclude na telemetria de diagnóstico do Azure hello, emitida como parte de um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="87fd6-163">This object specifies certain action inputs or outputs that you want tooinclude in hello Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="87fd6-164">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="87fd6-164">For example:</span></span>

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="87fd6-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="87fd6-165">Next Steps</span></span>
* [<span data-ttu-id="87fd6-166">Criar definições de fluxo de trabalho para aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="87fd6-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="87fd6-167">Criar modelos de implantação para aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="87fd6-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
