---
title: "Esquemas de acompanhamento personalizado para monitoramento B2B - Aplicativo Lógico do Azure | Microsoft Docs"
description: "Criar esquemas de acompanhamento personalizado para monitorar mensagens de B2B de transações em sua Conta de Integração do Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b71a4938dde2a71f1ce29403af7aa9101358d64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-tracking-to-monitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="35aa6-103">Habilitar acompanhamento para monitorar o fluxo de trabalho completo, de ponta a ponta</span><span class="sxs-lookup"><span data-stu-id="35aa6-103">Enable tracking to monitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="35aa6-104">Há um acompanhamento interno que você pode habilitar para diferentes partes do fluxo de trabalho entre empresas, como acompanhamento de mensagens AS2 ou X12.</span><span class="sxs-lookup"><span data-stu-id="35aa6-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="35aa6-105">Quando você cria fluxos de trabalho que incluem um aplicativo lógico, o BizTalk Server, o SQL Server ou qualquer outra camada, é possível habilitar o acompanhamento personalizado que registra eventos desde o início até o fim do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="35aa6-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from the beginning to the end of your workflow.</span></span> 

<span data-ttu-id="35aa6-106">Este tópico fornece código personalizado que você pode usar nas camadas fora do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="35aa6-106">This topic provides custom code that you can use in the layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="35aa6-107">Esquema de controle personalizado</span><span class="sxs-lookup"><span data-stu-id="35aa6-107">Custom tracking schema</span></span>
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| <span data-ttu-id="35aa6-108">Propriedade</span><span class="sxs-lookup"><span data-stu-id="35aa6-108">Property</span></span> | <span data-ttu-id="35aa6-109">Tipo</span><span class="sxs-lookup"><span data-stu-id="35aa6-109">Type</span></span> | <span data-ttu-id="35aa6-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="35aa6-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="35aa6-111">sourceType</span><span class="sxs-lookup"><span data-stu-id="35aa6-111">sourceType</span></span> |   | <span data-ttu-id="35aa6-112">O tipo da fonte de execução.</span><span class="sxs-lookup"><span data-stu-id="35aa6-112">Type of the run source.</span></span> <span data-ttu-id="35aa6-113">Os valores permitidos são **Microsoft.Logic/workflows** e **personalizado**.</span><span class="sxs-lookup"><span data-stu-id="35aa6-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="35aa6-114">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="35aa6-114">(Mandatory)</span></span> |
| <span data-ttu-id="35aa6-115">Fonte</span><span class="sxs-lookup"><span data-stu-id="35aa6-115">Source</span></span> |   | <span data-ttu-id="35aa6-116">Se o tipo de fonte for **Microsoft.Logic/workflows**, as informações de origem precisarão seguir este esquema.</span><span class="sxs-lookup"><span data-stu-id="35aa6-116">If the source type is **Microsoft.Logic/workflows**, the source information needs to follow this schema.</span></span> <span data-ttu-id="35aa6-117">Se o tipo de origem for **personalizado**, o esquema será um JToken.</span><span class="sxs-lookup"><span data-stu-id="35aa6-117">If the source type is **custom**, the schema is a JToken.</span></span> <span data-ttu-id="35aa6-118">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="35aa6-118">(Mandatory)</span></span> |
| <span data-ttu-id="35aa6-119">systemId</span><span class="sxs-lookup"><span data-stu-id="35aa6-119">systemId</span></span> | <span data-ttu-id="35aa6-120">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="35aa6-120">String</span></span> | <span data-ttu-id="35aa6-121">ID do sistema de aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="35aa6-121">Logic app system ID.</span></span> <span data-ttu-id="35aa6-122">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="35aa6-122">(Mandatory)</span></span> |
| <span data-ttu-id="35aa6-123">runId</span><span class="sxs-lookup"><span data-stu-id="35aa6-123">runId</span></span> | <span data-ttu-id="35aa6-124">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="35aa6-124">String</span></span> | <span data-ttu-id="35aa6-125">ID de execução do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="35aa6-125">Logic app run ID.</span></span> <span data-ttu-id="35aa6-126">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="35aa6-126">(Mandatory)</span></span> |
| <span data-ttu-id="35aa6-127">operationName</span><span class="sxs-lookup"><span data-stu-id="35aa6-127">operationName</span></span> | <span data-ttu-id="35aa6-128">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="35aa6-128">String</span></span> | <span data-ttu-id="35aa6-129">O nome da operação (por exemplo, ação ou gatilho).</span><span class="sxs-lookup"><span data-stu-id="35aa6-129">Name of the operation (for example, action or trigger).</span></span> <span data-ttu-id="35aa6-130">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="35aa6-130">(Mandatory)</span></span> |
| <span data-ttu-id="35aa6-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="35aa6-131">repeatItemScopeName</span></span> | <span data-ttu-id="35aa6-132">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="35aa6-132">String</span></span> | <span data-ttu-id="35aa6-133">Repita o nome do item se a ação estiver dentro de um loop `foreach`/`until`.</span><span class="sxs-lookup"><span data-stu-id="35aa6-133">Repeat item name if the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="35aa6-134">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="35aa6-134">(Mandatory)</span></span> |
| <span data-ttu-id="35aa6-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="35aa6-135">repeatItemIndex</span></span> | <span data-ttu-id="35aa6-136">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="35aa6-136">Integer</span></span> | <span data-ttu-id="35aa6-137">Se a ação está ou não dentro de um loop `foreach`/`until`.</span><span class="sxs-lookup"><span data-stu-id="35aa6-137">Whether the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="35aa6-138">Indica o índice de itens repetidos.</span><span class="sxs-lookup"><span data-stu-id="35aa6-138">Indicates the repeated item index.</span></span> <span data-ttu-id="35aa6-139">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="35aa6-139">(Mandatory)</span></span> |
| <span data-ttu-id="35aa6-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="35aa6-140">trackingId</span></span> | <span data-ttu-id="35aa6-141">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="35aa6-141">String</span></span> | <span data-ttu-id="35aa6-142">A ID de acompanhamento para correlacionar as mensagens.</span><span class="sxs-lookup"><span data-stu-id="35aa6-142">Tracking ID, to correlate the messages.</span></span> <span data-ttu-id="35aa6-143">(Opcional)</span><span class="sxs-lookup"><span data-stu-id="35aa6-143">(Optional)</span></span> |
| <span data-ttu-id="35aa6-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="35aa6-144">correlationId</span></span> | <span data-ttu-id="35aa6-145">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="35aa6-145">String</span></span> | <span data-ttu-id="35aa6-146">A ID de correlação para correlacionar as mensagens.</span><span class="sxs-lookup"><span data-stu-id="35aa6-146">Correlation ID, to correlate the messages.</span></span> <span data-ttu-id="35aa6-147">(Opcional)</span><span class="sxs-lookup"><span data-stu-id="35aa6-147">(Optional)</span></span> |
| <span data-ttu-id="35aa6-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="35aa6-148">clientRequestId</span></span> | <span data-ttu-id="35aa6-149">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="35aa6-149">String</span></span> | <span data-ttu-id="35aa6-150">O cliente pode populá-la para correlacionar mensagens.</span><span class="sxs-lookup"><span data-stu-id="35aa6-150">Client can populate it to correlate messages.</span></span> <span data-ttu-id="35aa6-151">(Opcional)</span><span class="sxs-lookup"><span data-stu-id="35aa6-151">(Optional)</span></span> |
| <span data-ttu-id="35aa6-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="35aa6-152">eventLevel</span></span> |   | <span data-ttu-id="35aa6-153">Nível do evento.</span><span class="sxs-lookup"><span data-stu-id="35aa6-153">Level of the event.</span></span> <span data-ttu-id="35aa6-154">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="35aa6-154">(Mandatory)</span></span> |
| <span data-ttu-id="35aa6-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="35aa6-155">eventTime</span></span> |   | <span data-ttu-id="35aa6-156">A hora do evento no formato UTC AAAA-MM-DDTHH:MM:SS.00000Z.</span><span class="sxs-lookup"><span data-stu-id="35aa6-156">Time of the event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="35aa6-157">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="35aa6-157">(Mandatory)</span></span> |
| <span data-ttu-id="35aa6-158">recordType</span><span class="sxs-lookup"><span data-stu-id="35aa6-158">recordType</span></span> |   | <span data-ttu-id="35aa6-159">Tipo do registro de acompanhamento.</span><span class="sxs-lookup"><span data-stu-id="35aa6-159">Type of the track record.</span></span> <span data-ttu-id="35aa6-160">O valor permitido é **personalizado**.</span><span class="sxs-lookup"><span data-stu-id="35aa6-160">Allowed value is **custom**.</span></span> <span data-ttu-id="35aa6-161">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="35aa6-161">(Mandatory)</span></span> |
| <span data-ttu-id="35aa6-162">record</span><span class="sxs-lookup"><span data-stu-id="35aa6-162">record</span></span> |   | <span data-ttu-id="35aa6-163">Tipo de registro personalizado.</span><span class="sxs-lookup"><span data-stu-id="35aa6-163">Custom record type.</span></span> <span data-ttu-id="35aa6-164">O formato permitido é JToken.</span><span class="sxs-lookup"><span data-stu-id="35aa6-164">Allowed format is JToken.</span></span> <span data-ttu-id="35aa6-165">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="35aa6-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="35aa6-166">Esquemas de acompanhamento do protocolo B2B</span><span class="sxs-lookup"><span data-stu-id="35aa6-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="35aa6-167">Para obter informações sobre esquemas de acompanhamento do protocolo B2B, veja:</span><span class="sxs-lookup"><span data-stu-id="35aa6-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="35aa6-168">Esquemas de acompanhamento de AS2</span><span class="sxs-lookup"><span data-stu-id="35aa6-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="35aa6-169">Esquemas de acompanhamento de X12</span><span class="sxs-lookup"><span data-stu-id="35aa6-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="35aa6-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="35aa6-170">Next steps</span></span>
* <span data-ttu-id="35aa6-171">Saiba mais sobre o [monitoramento de mensagens de B2B](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="35aa6-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="35aa6-172">Saiba mais sobre [acompanhamento de mensagens B2B no portal do Operations Management Suite](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="35aa6-172">Learn about [tracking B2B messages in the Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="35aa6-173">Saiba mais sobre o [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="35aa6-173">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
