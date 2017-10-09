---
title: "aaaCustom controle esquemas para B2B monitoramento - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Crie esquemas de acompanhamento personalizado toomonitor B2B mensagens de transações em sua conta de integração do Azure."
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
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="3a49c-103">Habilitar o acompanhamento toomonitor seu fluxo de trabalho completo, ponta a ponta</span><span class="sxs-lookup"><span data-stu-id="3a49c-103">Enable tracking toomonitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="3a49c-104">Há um acompanhamento interno que você pode habilitar para diferentes partes do fluxo de trabalho entre empresas, como acompanhamento de mensagens AS2 ou X12.</span><span class="sxs-lookup"><span data-stu-id="3a49c-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="3a49c-105">Quando você criar fluxos de trabalho que inclui um lógica de aplicativo, BizTalk Server, SQL Server ou qualquer outra camada, você pode habilitar o controle personalizado que registra eventos de saudação início toohello final do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3a49c-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from hello beginning toohello end of your workflow.</span></span> 

<span data-ttu-id="3a49c-106">Este tópico fornece código personalizado que você pode usar em camadas Olá fora de seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="3a49c-106">This topic provides custom code that you can use in hello layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="3a49c-107">Esquema de controle personalizado</span><span class="sxs-lookup"><span data-stu-id="3a49c-107">Custom tracking schema</span></span>
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

| <span data-ttu-id="3a49c-108">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3a49c-108">Property</span></span> | <span data-ttu-id="3a49c-109">Tipo</span><span class="sxs-lookup"><span data-stu-id="3a49c-109">Type</span></span> | <span data-ttu-id="3a49c-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="3a49c-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a49c-111">sourceType</span><span class="sxs-lookup"><span data-stu-id="3a49c-111">sourceType</span></span> |   | <span data-ttu-id="3a49c-112">Tipo de origem Olá executar.</span><span class="sxs-lookup"><span data-stu-id="3a49c-112">Type of hello run source.</span></span> <span data-ttu-id="3a49c-113">Os valores permitidos são **Microsoft.Logic/workflows** e **personalizado**.</span><span class="sxs-lookup"><span data-stu-id="3a49c-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="3a49c-114">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="3a49c-114">(Mandatory)</span></span> |
| <span data-ttu-id="3a49c-115">Fonte</span><span class="sxs-lookup"><span data-stu-id="3a49c-115">Source</span></span> |   | <span data-ttu-id="3a49c-116">Se o tipo de origem de saudação é **Microsoft.Logic/workflows**, informações de fonte de saudação precisa toofollow desse esquema.</span><span class="sxs-lookup"><span data-stu-id="3a49c-116">If hello source type is **Microsoft.Logic/workflows**, hello source information needs toofollow this schema.</span></span> <span data-ttu-id="3a49c-117">Se o tipo de origem de saudação é **personalizado**, esquema de saudação é um JToken.</span><span class="sxs-lookup"><span data-stu-id="3a49c-117">If hello source type is **custom**, hello schema is a JToken.</span></span> <span data-ttu-id="3a49c-118">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="3a49c-118">(Mandatory)</span></span> |
| <span data-ttu-id="3a49c-119">systemId</span><span class="sxs-lookup"><span data-stu-id="3a49c-119">systemId</span></span> | <span data-ttu-id="3a49c-120">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3a49c-120">String</span></span> | <span data-ttu-id="3a49c-121">ID do sistema de aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="3a49c-121">Logic app system ID.</span></span> <span data-ttu-id="3a49c-122">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="3a49c-122">(Mandatory)</span></span> |
| <span data-ttu-id="3a49c-123">runId</span><span class="sxs-lookup"><span data-stu-id="3a49c-123">runId</span></span> | <span data-ttu-id="3a49c-124">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3a49c-124">String</span></span> | <span data-ttu-id="3a49c-125">ID de execução do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="3a49c-125">Logic app run ID.</span></span> <span data-ttu-id="3a49c-126">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="3a49c-126">(Mandatory)</span></span> |
| <span data-ttu-id="3a49c-127">operationName</span><span class="sxs-lookup"><span data-stu-id="3a49c-127">operationName</span></span> | <span data-ttu-id="3a49c-128">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3a49c-128">String</span></span> | <span data-ttu-id="3a49c-129">Nome da operação de saudação (por exemplo, ações ou gatilho).</span><span class="sxs-lookup"><span data-stu-id="3a49c-129">Name of hello operation (for example, action or trigger).</span></span> <span data-ttu-id="3a49c-130">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="3a49c-130">(Mandatory)</span></span> |
| <span data-ttu-id="3a49c-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="3a49c-131">repeatItemScopeName</span></span> | <span data-ttu-id="3a49c-132">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3a49c-132">String</span></span> | <span data-ttu-id="3a49c-133">Repita o nome do item se ação hello está dentro de um `foreach` / `until` loop.</span><span class="sxs-lookup"><span data-stu-id="3a49c-133">Repeat item name if hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="3a49c-134">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="3a49c-134">(Mandatory)</span></span> |
| <span data-ttu-id="3a49c-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="3a49c-135">repeatItemIndex</span></span> | <span data-ttu-id="3a49c-136">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="3a49c-136">Integer</span></span> | <span data-ttu-id="3a49c-137">Se a ação hello está dentro de um `foreach` / `until` loop.</span><span class="sxs-lookup"><span data-stu-id="3a49c-137">Whether hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="3a49c-138">Indica o índice do item repetido hello.</span><span class="sxs-lookup"><span data-stu-id="3a49c-138">Indicates hello repeated item index.</span></span> <span data-ttu-id="3a49c-139">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="3a49c-139">(Mandatory)</span></span> |
| <span data-ttu-id="3a49c-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="3a49c-140">trackingId</span></span> | <span data-ttu-id="3a49c-141">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3a49c-141">String</span></span> | <span data-ttu-id="3a49c-142">ID de rastreamento, mensagens de saudação do toocorrelate.</span><span class="sxs-lookup"><span data-stu-id="3a49c-142">Tracking ID, toocorrelate hello messages.</span></span> <span data-ttu-id="3a49c-143">(Opcional)</span><span class="sxs-lookup"><span data-stu-id="3a49c-143">(Optional)</span></span> |
| <span data-ttu-id="3a49c-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="3a49c-144">correlationId</span></span> | <span data-ttu-id="3a49c-145">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3a49c-145">String</span></span> | <span data-ttu-id="3a49c-146">ID de correlação, mensagens de saudação do toocorrelate.</span><span class="sxs-lookup"><span data-stu-id="3a49c-146">Correlation ID, toocorrelate hello messages.</span></span> <span data-ttu-id="3a49c-147">(Opcional)</span><span class="sxs-lookup"><span data-stu-id="3a49c-147">(Optional)</span></span> |
| <span data-ttu-id="3a49c-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="3a49c-148">clientRequestId</span></span> | <span data-ttu-id="3a49c-149">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3a49c-149">String</span></span> | <span data-ttu-id="3a49c-150">Cliente pode preenchê-la toocorrelate mensagens.</span><span class="sxs-lookup"><span data-stu-id="3a49c-150">Client can populate it toocorrelate messages.</span></span> <span data-ttu-id="3a49c-151">(Opcional)</span><span class="sxs-lookup"><span data-stu-id="3a49c-151">(Optional)</span></span> |
| <span data-ttu-id="3a49c-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="3a49c-152">eventLevel</span></span> |   | <span data-ttu-id="3a49c-153">Nível de evento hello.</span><span class="sxs-lookup"><span data-stu-id="3a49c-153">Level of hello event.</span></span> <span data-ttu-id="3a49c-154">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="3a49c-154">(Mandatory)</span></span> |
| <span data-ttu-id="3a49c-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="3a49c-155">eventTime</span></span> |   | <span data-ttu-id="3a49c-156">Hora do evento hello, no formato AAAA-MM-DDTHH:MM:SS.00000Z do UTC.</span><span class="sxs-lookup"><span data-stu-id="3a49c-156">Time of hello event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="3a49c-157">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="3a49c-157">(Mandatory)</span></span> |
| <span data-ttu-id="3a49c-158">recordType</span><span class="sxs-lookup"><span data-stu-id="3a49c-158">recordType</span></span> |   | <span data-ttu-id="3a49c-159">Tipo de registro de controle de saudação.</span><span class="sxs-lookup"><span data-stu-id="3a49c-159">Type of hello track record.</span></span> <span data-ttu-id="3a49c-160">O valor permitido é **personalizado**.</span><span class="sxs-lookup"><span data-stu-id="3a49c-160">Allowed value is **custom**.</span></span> <span data-ttu-id="3a49c-161">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="3a49c-161">(Mandatory)</span></span> |
| <span data-ttu-id="3a49c-162">record</span><span class="sxs-lookup"><span data-stu-id="3a49c-162">record</span></span> |   | <span data-ttu-id="3a49c-163">Tipo de registro personalizado.</span><span class="sxs-lookup"><span data-stu-id="3a49c-163">Custom record type.</span></span> <span data-ttu-id="3a49c-164">O formato permitido é JToken.</span><span class="sxs-lookup"><span data-stu-id="3a49c-164">Allowed format is JToken.</span></span> <span data-ttu-id="3a49c-165">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="3a49c-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="3a49c-166">Esquemas de acompanhamento do protocolo B2B</span><span class="sxs-lookup"><span data-stu-id="3a49c-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="3a49c-167">Para obter informações sobre esquemas de acompanhamento do protocolo B2B, veja:</span><span class="sxs-lookup"><span data-stu-id="3a49c-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="3a49c-168">Esquemas de acompanhamento de AS2</span><span class="sxs-lookup"><span data-stu-id="3a49c-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="3a49c-169">Esquemas de acompanhamento de X12</span><span class="sxs-lookup"><span data-stu-id="3a49c-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="3a49c-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3a49c-170">Next steps</span></span>
* <span data-ttu-id="3a49c-171">Saiba mais sobre o [monitoramento de mensagens de B2B](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="3a49c-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="3a49c-172">Saiba mais sobre [acompanhamento de mensagens B2B no portal do Operations Management Suite Olá](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="3a49c-172">Learn about [tracking B2B messages in hello Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="3a49c-173">Saiba mais sobre Olá [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3a49c-173">Learn more about hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
