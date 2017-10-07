---
title: "notificações de alerta de email de toosend de ações de dimensionamento automático aaaUse e webhook. | Microsoft Docs"
description: "Consulte como toocall de ações de dimensionamento automático toouse web URLs ou enviar notificações por email no Monitor do Azure. "
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="dc1b8-104">Usar o dimensionamento automático ações toosend email e webhook notificações de alerta no Monitor do Azure</span><span class="sxs-lookup"><span data-stu-id="dc1b8-104">Use autoscale actions toosend email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="dc1b8-105">Este artigo mostra como configurar gatilhos para que você possa chamar URLs da web específicas ou enviar emails com base em ações de escala automática no Azure.</span><span class="sxs-lookup"><span data-stu-id="dc1b8-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="dc1b8-106">Webhooks</span><span class="sxs-lookup"><span data-stu-id="dc1b8-106">Webhooks</span></span>
<span data-ttu-id="dc1b8-107">Webhooks permitem que você tenha sistemas de tooother de notificações de alerta do Azure tooroute Olá para notificações de pós-processamento ou personalizados.</span><span class="sxs-lookup"><span data-stu-id="dc1b8-107">Webhooks allow you tooroute hello Azure alert notifications tooother systems for post-processing or custom notifications.</span></span> <span data-ttu-id="dc1b8-108">Por exemplo, o roteamento tooservices alerta Olá que pode lidar com uma entrada da web solicitação toosend SMS, bugs de log, notificar uma equipe usando bate-papo ou serviços de mensagens, etc. Olá webhook URI deve ser um ponto de extremidade HTTP ou HTTPS válido.</span><span class="sxs-lookup"><span data-stu-id="dc1b8-108">For example, routing hello alert tooservices that can handle an incoming web request toosend SMS, log bugs, notify a team using chat or messaging services, etc. hello webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="dc1b8-109">Email</span><span class="sxs-lookup"><span data-stu-id="dc1b8-109">Email</span></span>
<span data-ttu-id="dc1b8-110">É possível enviar emails tooany endereço de email válido.</span><span class="sxs-lookup"><span data-stu-id="dc1b8-110">Email can be sent tooany valid email address.</span></span> <span data-ttu-id="dc1b8-111">Os administradores e coadministradores de assinatura de saudação onde regra hello está sendo executado também serão notificados.</span><span class="sxs-lookup"><span data-stu-id="dc1b8-111">Administrators and co-administrators of hello subscription where hello rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="dc1b8-112">Serviços de nuvem e aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="dc1b8-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="dc1b8-113">Você pode aceitar de saudação portal do Azure para serviços de nuvem e Farms de servidores (aplicativos da Web).</span><span class="sxs-lookup"><span data-stu-id="dc1b8-113">You can opt-in from hello Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="dc1b8-114">Escolha Olá **o dimensionamento por** métrica.</span><span class="sxs-lookup"><span data-stu-id="dc1b8-114">Choose hello **scale by** metric.</span></span>

![escalar por](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="dc1b8-116">Conjuntos de escala de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="dc1b8-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="dc1b8-117">Para ver as Máquinas Virtuais mais novas criadas com o Gerenciador de Recursos (conjuntos de escala da Máquina Virtual), você pode configurar isso usando a API REST, modelos do Gerenciador de Recursos, PowerShell e CLI.</span><span class="sxs-lookup"><span data-stu-id="dc1b8-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="dc1b8-118">Uma interface de portal ainda não está disponível.</span><span class="sxs-lookup"><span data-stu-id="dc1b8-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="dc1b8-119">Ao usar o hello API REST ou o modelo do Gerenciador de recursos, inclua o elemento de notificações de saudação com hello as opções a seguir.</span><span class="sxs-lookup"><span data-stu-id="dc1b8-119">When using hello REST API or Resource Manager template, include hello notifications element with hello following options.</span></span>

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]
```
| <span data-ttu-id="dc1b8-120">Campo</span><span class="sxs-lookup"><span data-stu-id="dc1b8-120">Field</span></span> | <span data-ttu-id="dc1b8-121">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="dc1b8-121">Mandatory?</span></span> | <span data-ttu-id="dc1b8-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="dc1b8-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc1b8-123">operation</span><span class="sxs-lookup"><span data-stu-id="dc1b8-123">operation</span></span> |<span data-ttu-id="dc1b8-124">sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-124">yes</span></span> |<span data-ttu-id="dc1b8-125">o valor deve ser "Scale"</span><span class="sxs-lookup"><span data-stu-id="dc1b8-125">value must be "Scale"</span></span> |
| <span data-ttu-id="dc1b8-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="dc1b8-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="dc1b8-127">sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-127">yes</span></span> |<span data-ttu-id="dc1b8-128">o valor deve ser "true" ou "false"</span><span class="sxs-lookup"><span data-stu-id="dc1b8-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="dc1b8-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="dc1b8-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="dc1b8-130">sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-130">yes</span></span> |<span data-ttu-id="dc1b8-131">o valor deve ser "true" ou "false"</span><span class="sxs-lookup"><span data-stu-id="dc1b8-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="dc1b8-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="dc1b8-132">customEmails</span></span> |<span data-ttu-id="dc1b8-133">sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-133">yes</span></span> |<span data-ttu-id="dc1b8-134">o valor pode ser null [] ou uma matriz da cadeia de caracteres de emails</span><span class="sxs-lookup"><span data-stu-id="dc1b8-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="dc1b8-135">Webhooks</span><span class="sxs-lookup"><span data-stu-id="dc1b8-135">webhooks</span></span> |<span data-ttu-id="dc1b8-136">sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-136">yes</span></span> |<span data-ttu-id="dc1b8-137">o valor pode ser um Uri válido ou nulo</span><span class="sxs-lookup"><span data-stu-id="dc1b8-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="dc1b8-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="dc1b8-138">serviceUri</span></span> |<span data-ttu-id="dc1b8-139">sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-139">yes</span></span> |<span data-ttu-id="dc1b8-140">um Uri de https válido</span><span class="sxs-lookup"><span data-stu-id="dc1b8-140">a valid https Uri</span></span> |
| <span data-ttu-id="dc1b8-141">propriedades</span><span class="sxs-lookup"><span data-stu-id="dc1b8-141">properties</span></span> |<span data-ttu-id="dc1b8-142">sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-142">yes</span></span> |<span data-ttu-id="dc1b8-143">o valor deve ser vazio {} ou pode conter pares de chave-valor</span><span class="sxs-lookup"><span data-stu-id="dc1b8-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="dc1b8-144">Autenticação em webhooks</span><span class="sxs-lookup"><span data-stu-id="dc1b8-144">Authentication in webhooks</span></span>
<span data-ttu-id="dc1b8-145">Olá webhook pode autenticar usando autenticação baseada em token, onde salvar o webhook Olá URI com uma token de ID como um parâmetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="dc1b8-145">hello webhook can authenticate using token-based authentication, where you save hello webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="dc1b8-146">Por exemplo, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="dc1b8-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="dc1b8-147">Escala automática do esquema de carga útil do webhook de notificação</span><span class="sxs-lookup"><span data-stu-id="dc1b8-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="dc1b8-148">Quando a notificação de dimensionamento automático Olá é gerada, hello metadados a seguir estão incluídos na carga de webhook hello:</span><span class="sxs-lookup"><span data-stu-id="dc1b8-148">When hello autoscale notification is generated, hello following metadata is included in hello webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| <span data-ttu-id="dc1b8-149">Campo</span><span class="sxs-lookup"><span data-stu-id="dc1b8-149">Field</span></span> | <span data-ttu-id="dc1b8-150">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="dc1b8-150">Mandatory?</span></span> | <span data-ttu-id="dc1b8-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="dc1b8-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc1b8-152">status</span><span class="sxs-lookup"><span data-stu-id="dc1b8-152">status</span></span> |<span data-ttu-id="dc1b8-153">sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-153">yes</span></span> |<span data-ttu-id="dc1b8-154">status de saudação que indica que uma ação de dimensionamento automático foi gerada</span><span class="sxs-lookup"><span data-stu-id="dc1b8-154">hello status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="dc1b8-155">operation</span><span class="sxs-lookup"><span data-stu-id="dc1b8-155">operation</span></span> |<span data-ttu-id="dc1b8-156">sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-156">yes</span></span> |<span data-ttu-id="dc1b8-157">Para um aumento de instâncias, será "Escalar Horizontalmente" e para uma diminuição de instâncias, será "Reduzir Horizontalmente"</span><span class="sxs-lookup"><span data-stu-id="dc1b8-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="dc1b8-158">context</span><span class="sxs-lookup"><span data-stu-id="dc1b8-158">context</span></span> |<span data-ttu-id="dc1b8-159">sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-159">yes</span></span> |<span data-ttu-id="dc1b8-160">contexto de ação de dimensionamento automático Olá</span><span class="sxs-lookup"><span data-stu-id="dc1b8-160">hello autoscale action context</span></span> |
| <span data-ttu-id="dc1b8-161">timestamp</span><span class="sxs-lookup"><span data-stu-id="dc1b8-161">timestamp</span></span> |<span data-ttu-id="dc1b8-162">sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-162">yes</span></span> |<span data-ttu-id="dc1b8-163">Carimbo de hora quando a ação de dimensionamento automático Olá foi disparada</span><span class="sxs-lookup"><span data-stu-id="dc1b8-163">Time stamp when hello autoscale action was triggered</span></span> |
| <span data-ttu-id="dc1b8-164">ID</span><span class="sxs-lookup"><span data-stu-id="dc1b8-164">id</span></span> |<span data-ttu-id="dc1b8-165">Sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-165">Yes</span></span> |<span data-ttu-id="dc1b8-166">ID do Gerenciador de recursos de configuração de dimensionamento automático Olá</span><span class="sxs-lookup"><span data-stu-id="dc1b8-166">Resource Manager ID of hello autoscale setting</span></span> |
| <span data-ttu-id="dc1b8-167">name</span><span class="sxs-lookup"><span data-stu-id="dc1b8-167">name</span></span> |<span data-ttu-id="dc1b8-168">Sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-168">Yes</span></span> |<span data-ttu-id="dc1b8-169">nome de saudação da configuração de AutoEscala Olá</span><span class="sxs-lookup"><span data-stu-id="dc1b8-169">hello name of hello autoscale setting</span></span> |
| <span data-ttu-id="dc1b8-170">detalhes</span><span class="sxs-lookup"><span data-stu-id="dc1b8-170">details</span></span> |<span data-ttu-id="dc1b8-171">Sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-171">Yes</span></span> |<span data-ttu-id="dc1b8-172">Explicação da ação de saudação que levou o serviço de AutoEscala hello e Olá alterar na contagem de instâncias de saudação</span><span class="sxs-lookup"><span data-stu-id="dc1b8-172">Explanation of hello action that hello autoscale service took and hello change in hello instance count</span></span> |
| <span data-ttu-id="dc1b8-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="dc1b8-173">subscriptionId</span></span> |<span data-ttu-id="dc1b8-174">Sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-174">Yes</span></span> |<span data-ttu-id="dc1b8-175">ID de assinatura do recurso de destino de hello está sendo dimensionado</span><span class="sxs-lookup"><span data-stu-id="dc1b8-175">Subscription ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="dc1b8-176">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="dc1b8-176">resourceGroupName</span></span> |<span data-ttu-id="dc1b8-177">Sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-177">Yes</span></span> |<span data-ttu-id="dc1b8-178">Nome do grupo de recursos do recurso de destino de hello está sendo dimensionado</span><span class="sxs-lookup"><span data-stu-id="dc1b8-178">Resource Group name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="dc1b8-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="dc1b8-179">resourceName</span></span> |<span data-ttu-id="dc1b8-180">Sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-180">Yes</span></span> |<span data-ttu-id="dc1b8-181">Nome do recurso de destino de hello está sendo dimensionado</span><span class="sxs-lookup"><span data-stu-id="dc1b8-181">Name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="dc1b8-182">resourceType</span><span class="sxs-lookup"><span data-stu-id="dc1b8-182">resourceType</span></span> |<span data-ttu-id="dc1b8-183">Sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-183">Yes</span></span> |<span data-ttu-id="dc1b8-184">Olá três valores com suporte: "microsoft.classiccompute/domainnames/slots/roles" - funções de serviço de nuvem, "microsoft.compute/virtualmachinescalesets" - conjuntos de escala de máquina Virtual e "Web/serverfarms" - aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="dc1b8-184">hello three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="dc1b8-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="dc1b8-185">resourceId</span></span> |<span data-ttu-id="dc1b8-186">Sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-186">Yes</span></span> |<span data-ttu-id="dc1b8-187">ID do Gerenciador de recursos do recurso de destino de saudação que está sendo dimensionado</span><span class="sxs-lookup"><span data-stu-id="dc1b8-187">Resource Manager ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="dc1b8-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="dc1b8-188">portalLink</span></span> |<span data-ttu-id="dc1b8-189">Sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-189">Yes</span></span> |<span data-ttu-id="dc1b8-190">Página de resumo do link do portal do Azure toohello do recurso de destino Olá</span><span class="sxs-lookup"><span data-stu-id="dc1b8-190">Azure portal link toohello summary page of hello target resource</span></span> |
| <span data-ttu-id="dc1b8-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="dc1b8-191">oldCapacity</span></span> |<span data-ttu-id="dc1b8-192">Sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-192">Yes</span></span> |<span data-ttu-id="dc1b8-193">Olá atual (antigo) contagem de instâncias quando o dimensionamento automático levou a uma ação de escala</span><span class="sxs-lookup"><span data-stu-id="dc1b8-193">hello current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="dc1b8-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="dc1b8-194">newCapacity</span></span> |<span data-ttu-id="dc1b8-195">Sim</span><span class="sxs-lookup"><span data-stu-id="dc1b8-195">Yes</span></span> |<span data-ttu-id="dc1b8-196">Contagem de instâncias novo Olá que AutoEscala dimensionado recurso Olá muito</span><span class="sxs-lookup"><span data-stu-id="dc1b8-196">hello new instance count that Autoscale scaled hello resource too</span></span>|
| <span data-ttu-id="dc1b8-197">Propriedades</span><span class="sxs-lookup"><span data-stu-id="dc1b8-197">Properties</span></span> |<span data-ttu-id="dc1b8-198">Não</span><span class="sxs-lookup"><span data-stu-id="dc1b8-198">No</span></span> |<span data-ttu-id="dc1b8-199">Opcional.</span><span class="sxs-lookup"><span data-stu-id="dc1b8-199">Optional.</span></span> <span data-ttu-id="dc1b8-200">Conjunto de pares de <Chave, Valor> (por exemplo, Dicionário <Cadeia de caracteres, Cadeia de caracteres>).</span><span class="sxs-lookup"><span data-stu-id="dc1b8-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="dc1b8-201">Olá propriedades campo é opcional.</span><span class="sxs-lookup"><span data-stu-id="dc1b8-201">hello properties field is optional.</span></span> <span data-ttu-id="dc1b8-202">Em uma interface de usuário personalizada ou fluxo de trabalho de aplicativo com base em lógica, você pode inserir chaves e valores que podem ser passados usando a carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc1b8-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using hello payload.</span></span> <span data-ttu-id="dc1b8-203">Um modo alternativo de propriedades personalizadas toopass fazer a chamada de webhook saída toohello é toouse Olá webhook URI em si (como parâmetros de consulta)</span><span class="sxs-lookup"><span data-stu-id="dc1b8-203">An alternate way toopass custom properties back toohello outgoing webhook call is toouse hello webhook URI itself (as query parameters)</span></span> |
