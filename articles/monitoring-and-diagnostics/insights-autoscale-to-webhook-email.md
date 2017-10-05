---
title: "Usar ações de dimensionamento automático para enviar notificações de alerta por email e webhook. | Microsoft Docs"
description: "Consulte como usar ações de escala automática para chamar URLs da web ou enviar notificações por email no Azure Monitor. "
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
ms.openlocfilehash: 16caf14028494800e9259f0296c292b606d0210a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-autoscale-actions-to-send-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="11ff9-104">Use ações de dimensionamento automático para enviar notificações de alerta por email e webhook no Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="11ff9-104">Use autoscale actions to send email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="11ff9-105">Este artigo mostra como configurar gatilhos para que você possa chamar URLs da web específicas ou enviar emails com base em ações de escala automática no Azure.</span><span class="sxs-lookup"><span data-stu-id="11ff9-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="11ff9-106">Webhooks</span><span class="sxs-lookup"><span data-stu-id="11ff9-106">Webhooks</span></span>
<span data-ttu-id="11ff9-107">Webhooks permitem rotear as notificações de alerta do Azure para outros sistemas para pós-processamento ou notificações personalizadas.</span><span class="sxs-lookup"><span data-stu-id="11ff9-107">Webhooks allow you to route the Azure alert notifications to other systems for post-processing or custom notifications.</span></span> <span data-ttu-id="11ff9-108">Por exemplo, rotear o alerta para serviços que podem lidar com uma solicitação da Web de entrada para enviar SMS, registrar bugs, notificar a equipe por meio de serviços de chat/mensagens etc. O URI do webhook deve ser um ponto de extremidade HTTP ou HTTPS válido.</span><span class="sxs-lookup"><span data-stu-id="11ff9-108">For example, routing the alert to services that can handle an incoming web request to send SMS, log bugs, notify a team using chat or messaging services, etc. The webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="11ff9-109">Email</span><span class="sxs-lookup"><span data-stu-id="11ff9-109">Email</span></span>
<span data-ttu-id="11ff9-110">O email pode ser enviado para qualquer endereço de email válido.</span><span class="sxs-lookup"><span data-stu-id="11ff9-110">Email can be sent to any valid email address.</span></span> <span data-ttu-id="11ff9-111">Os administradores e administradores da assinatura em que a regra está em execução também serão notificados.</span><span class="sxs-lookup"><span data-stu-id="11ff9-111">Administrators and co-administrators of the subscription where the rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="11ff9-112">Serviços de nuvem e aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="11ff9-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="11ff9-113">Você pode aderir no portal do Azure para Serviços de Nuvem e Farms de Servidores (aplicativos Web).</span><span class="sxs-lookup"><span data-stu-id="11ff9-113">You can opt-in from the Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="11ff9-114">Escolha a métrica **escalar por** .</span><span class="sxs-lookup"><span data-stu-id="11ff9-114">Choose the **scale by** metric.</span></span>

![escalar por](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="11ff9-116">Conjuntos de escala de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="11ff9-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="11ff9-117">Para ver as Máquinas Virtuais mais novas criadas com o Gerenciador de Recursos (conjuntos de escala da Máquina Virtual), você pode configurar isso usando a API REST, modelos do Gerenciador de Recursos, PowerShell e CLI.</span><span class="sxs-lookup"><span data-stu-id="11ff9-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="11ff9-118">Uma interface de portal ainda não está disponível.</span><span class="sxs-lookup"><span data-stu-id="11ff9-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="11ff9-119">Ao usar o modelo da API REST ou do Gerenciador de Recursos, inclua o elemento de notificações com as seguintes opções.</span><span class="sxs-lookup"><span data-stu-id="11ff9-119">When using the REST API or Resource Manager template, include the notifications element with the following options.</span></span>

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
| <span data-ttu-id="11ff9-120">Campo</span><span class="sxs-lookup"><span data-stu-id="11ff9-120">Field</span></span> | <span data-ttu-id="11ff9-121">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="11ff9-121">Mandatory?</span></span> | <span data-ttu-id="11ff9-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="11ff9-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11ff9-123">operation</span><span class="sxs-lookup"><span data-stu-id="11ff9-123">operation</span></span> |<span data-ttu-id="11ff9-124">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-124">yes</span></span> |<span data-ttu-id="11ff9-125">o valor deve ser "Scale"</span><span class="sxs-lookup"><span data-stu-id="11ff9-125">value must be "Scale"</span></span> |
| <span data-ttu-id="11ff9-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="11ff9-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="11ff9-127">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-127">yes</span></span> |<span data-ttu-id="11ff9-128">o valor deve ser "true" ou "false"</span><span class="sxs-lookup"><span data-stu-id="11ff9-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="11ff9-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="11ff9-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="11ff9-130">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-130">yes</span></span> |<span data-ttu-id="11ff9-131">o valor deve ser "true" ou "false"</span><span class="sxs-lookup"><span data-stu-id="11ff9-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="11ff9-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="11ff9-132">customEmails</span></span> |<span data-ttu-id="11ff9-133">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-133">yes</span></span> |<span data-ttu-id="11ff9-134">o valor pode ser null [] ou uma matriz da cadeia de caracteres de emails</span><span class="sxs-lookup"><span data-stu-id="11ff9-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="11ff9-135">Webhooks</span><span class="sxs-lookup"><span data-stu-id="11ff9-135">webhooks</span></span> |<span data-ttu-id="11ff9-136">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-136">yes</span></span> |<span data-ttu-id="11ff9-137">o valor pode ser um Uri válido ou nulo</span><span class="sxs-lookup"><span data-stu-id="11ff9-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="11ff9-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="11ff9-138">serviceUri</span></span> |<span data-ttu-id="11ff9-139">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-139">yes</span></span> |<span data-ttu-id="11ff9-140">um Uri de https válido</span><span class="sxs-lookup"><span data-stu-id="11ff9-140">a valid https Uri</span></span> |
| <span data-ttu-id="11ff9-141">propriedades</span><span class="sxs-lookup"><span data-stu-id="11ff9-141">properties</span></span> |<span data-ttu-id="11ff9-142">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-142">yes</span></span> |<span data-ttu-id="11ff9-143">o valor deve ser vazio {} ou pode conter pares de chave-valor</span><span class="sxs-lookup"><span data-stu-id="11ff9-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="11ff9-144">Autenticação em webhooks</span><span class="sxs-lookup"><span data-stu-id="11ff9-144">Authentication in webhooks</span></span>
<span data-ttu-id="11ff9-145">O webhook pode autenticar usando autenticação baseada em token, em que você salva o URI do webhook com uma ID de token como um parâmetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="11ff9-145">The webhook can authenticate using token-based authentication, where you save the webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="11ff9-146">Por exemplo, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="11ff9-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="11ff9-147">Escala automática do esquema de carga útil do webhook de notificação</span><span class="sxs-lookup"><span data-stu-id="11ff9-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="11ff9-148">Quando a notificação de escala automática é gerada, os metadados a seguir são incluídos na carga útil do webhook:</span><span class="sxs-lookup"><span data-stu-id="11ff9-148">When the autoscale notification is generated, the following metadata is included in the webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' to capacity '2'",
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


| <span data-ttu-id="11ff9-149">Campo</span><span class="sxs-lookup"><span data-stu-id="11ff9-149">Field</span></span> | <span data-ttu-id="11ff9-150">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="11ff9-150">Mandatory?</span></span> | <span data-ttu-id="11ff9-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="11ff9-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11ff9-152">status</span><span class="sxs-lookup"><span data-stu-id="11ff9-152">status</span></span> |<span data-ttu-id="11ff9-153">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-153">yes</span></span> |<span data-ttu-id="11ff9-154">O status que indica que uma ação de escala automática foi gerada</span><span class="sxs-lookup"><span data-stu-id="11ff9-154">The status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="11ff9-155">operation</span><span class="sxs-lookup"><span data-stu-id="11ff9-155">operation</span></span> |<span data-ttu-id="11ff9-156">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-156">yes</span></span> |<span data-ttu-id="11ff9-157">Para um aumento de instâncias, será "Escalar Horizontalmente" e para uma diminuição de instâncias, será "Reduzir Horizontalmente"</span><span class="sxs-lookup"><span data-stu-id="11ff9-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="11ff9-158">context</span><span class="sxs-lookup"><span data-stu-id="11ff9-158">context</span></span> |<span data-ttu-id="11ff9-159">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-159">yes</span></span> |<span data-ttu-id="11ff9-160">O contexto de ação de escala automática</span><span class="sxs-lookup"><span data-stu-id="11ff9-160">The autoscale action context</span></span> |
| <span data-ttu-id="11ff9-161">timestamp</span><span class="sxs-lookup"><span data-stu-id="11ff9-161">timestamp</span></span> |<span data-ttu-id="11ff9-162">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-162">yes</span></span> |<span data-ttu-id="11ff9-163">Carimbo de data/hora de quando a ação de escala automática foi disparada</span><span class="sxs-lookup"><span data-stu-id="11ff9-163">Time stamp when the autoscale action was triggered</span></span> |
| <span data-ttu-id="11ff9-164">ID</span><span class="sxs-lookup"><span data-stu-id="11ff9-164">id</span></span> |<span data-ttu-id="11ff9-165">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-165">Yes</span></span> |<span data-ttu-id="11ff9-166">ID do Gerenciador de Recursos da configuração de autoescala</span><span class="sxs-lookup"><span data-stu-id="11ff9-166">Resource Manager ID of the autoscale setting</span></span> |
| <span data-ttu-id="11ff9-167">name</span><span class="sxs-lookup"><span data-stu-id="11ff9-167">name</span></span> |<span data-ttu-id="11ff9-168">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-168">Yes</span></span> |<span data-ttu-id="11ff9-169">O nome da configuração de escala automática</span><span class="sxs-lookup"><span data-stu-id="11ff9-169">The name of the autoscale setting</span></span> |
| <span data-ttu-id="11ff9-170">detalhes</span><span class="sxs-lookup"><span data-stu-id="11ff9-170">details</span></span> |<span data-ttu-id="11ff9-171">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-171">Yes</span></span> |<span data-ttu-id="11ff9-172">Explicação da ação que o serviço de escala automática realizada a alteração na contagem da instância</span><span class="sxs-lookup"><span data-stu-id="11ff9-172">Explanation of the action that the autoscale service took and the change in the instance count</span></span> |
| <span data-ttu-id="11ff9-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="11ff9-173">subscriptionId</span></span> |<span data-ttu-id="11ff9-174">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-174">Yes</span></span> |<span data-ttu-id="11ff9-175">ID da assinatura do recurso de destino que está sendo escalado</span><span class="sxs-lookup"><span data-stu-id="11ff9-175">Subscription ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="11ff9-176">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="11ff9-176">resourceGroupName</span></span> |<span data-ttu-id="11ff9-177">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-177">Yes</span></span> |<span data-ttu-id="11ff9-178">Nome do Grupo de Recursos do recurso de destino que está sendo escalado</span><span class="sxs-lookup"><span data-stu-id="11ff9-178">Resource Group name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="11ff9-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="11ff9-179">resourceName</span></span> |<span data-ttu-id="11ff9-180">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-180">Yes</span></span> |<span data-ttu-id="11ff9-181">Nome do recurso de destino que está sendo escalado</span><span class="sxs-lookup"><span data-stu-id="11ff9-181">Name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="11ff9-182">resourceType</span><span class="sxs-lookup"><span data-stu-id="11ff9-182">resourceType</span></span> |<span data-ttu-id="11ff9-183">Sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-183">Yes</span></span> |<span data-ttu-id="11ff9-184">Os três valores com suporte: "microsoft.classiccompute/domainnames/slots/roles" - funções de Serviço de Nuvem, "microsoft.compute/virtualmachinescalesets" - Conjuntos de Escala de Máquina Virtual e "Microsoft.Web/serverfarms" - Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="11ff9-184">The three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="11ff9-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="11ff9-185">resourceId</span></span> |<span data-ttu-id="11ff9-186">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-186">Yes</span></span> |<span data-ttu-id="11ff9-187">ID do Gerenciador de Recursos do recurso de destino que está sendo dimensionado</span><span class="sxs-lookup"><span data-stu-id="11ff9-187">Resource Manager ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="11ff9-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="11ff9-188">portalLink</span></span> |<span data-ttu-id="11ff9-189">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-189">Yes</span></span> |<span data-ttu-id="11ff9-190">Link do portal do Azure para a página de resumo do recurso de destino</span><span class="sxs-lookup"><span data-stu-id="11ff9-190">Azure portal link to the summary page of the target resource</span></span> |
| <span data-ttu-id="11ff9-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="11ff9-191">oldCapacity</span></span> |<span data-ttu-id="11ff9-192">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-192">Yes</span></span> |<span data-ttu-id="11ff9-193">A atual (antiga) contagem de instância quando Escala Automática adotou uma ação de escala</span><span class="sxs-lookup"><span data-stu-id="11ff9-193">The current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="11ff9-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="11ff9-194">newCapacity</span></span> |<span data-ttu-id="11ff9-195">sim</span><span class="sxs-lookup"><span data-stu-id="11ff9-195">Yes</span></span> |<span data-ttu-id="11ff9-196">A nova contagem de instância para a qual a Escala Automática escalou o recurso</span><span class="sxs-lookup"><span data-stu-id="11ff9-196">The new instance count that Autoscale scaled the resource to</span></span> |
| <span data-ttu-id="11ff9-197">propriedades</span><span class="sxs-lookup"><span data-stu-id="11ff9-197">Properties</span></span> |<span data-ttu-id="11ff9-198">Não</span><span class="sxs-lookup"><span data-stu-id="11ff9-198">No</span></span> |<span data-ttu-id="11ff9-199">Opcional.</span><span class="sxs-lookup"><span data-stu-id="11ff9-199">Optional.</span></span> <span data-ttu-id="11ff9-200">Conjunto de pares de <Chave, Valor> (por exemplo, Dicionário <Cadeia de caracteres, Cadeia de caracteres>).</span><span class="sxs-lookup"><span data-stu-id="11ff9-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="11ff9-201">O campo de propriedades é opcional.</span><span class="sxs-lookup"><span data-stu-id="11ff9-201">The properties field is optional.</span></span> <span data-ttu-id="11ff9-202">Em uma interface do usuário personalizada ou fluxo de trabalho de aplicativo Lógico, você pode inserir as chaves e valores que podem ser passados usando a carga útil.</span><span class="sxs-lookup"><span data-stu-id="11ff9-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using the payload.</span></span> <span data-ttu-id="11ff9-203">Uma maneira alternativa de passar as propriedades personalizadas de volta para a chamada de saída do webhook é usar o URI do webhook em si (como parâmetros de consulta)</span><span class="sxs-lookup"><span data-stu-id="11ff9-203">An alternate way to pass custom properties back to the outgoing webhook call is to use the webhook URI itself (as query parameters)</span></span> |
