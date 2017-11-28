---
title: "Autoescala avançada usando máquinas virtuais do Azure | Microsoft Docs"
description: "Usa o Resource Manager e Conjuntos de Dimensionamento de VMs com várias regras e perfis que enviam email e chamam URLs de webhook com ações de escala."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: 80955535c8d863cd3d8d1b77e2ab8bc016b6d9f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="70bd3-103">Configuração avançada de autoescala usando modelos do Resource Manager para Conjuntos de Dimensionamento de VMs</span><span class="sxs-lookup"><span data-stu-id="70bd3-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="70bd3-104">Você pode escalar e reduzir horizontalmente Conjuntos de Dimensionamento de Máquina Virtual com base nos limites de métrica de desempenho, em uma agenda recorrente ou em determinada data.</span><span class="sxs-lookup"><span data-stu-id="70bd3-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="70bd3-105">Você também pode configurar notificações por email e webhook para ações de escala.</span><span class="sxs-lookup"><span data-stu-id="70bd3-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="70bd3-106">Este passo a passo mostra um exemplo de configuração de todos esses objetos usando um modelo do Resource Manager em um Conjunto de Dimensionamento de VMs.</span><span class="sxs-lookup"><span data-stu-id="70bd3-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="70bd3-107">Este passo a passo explica as etapas para Conjuntos de Dimensionamento de VMs, as mesmas informações se aplicam ao dimensionamento automático de [Serviços de Nuvem](https://azure.microsoft.com/services/cloud-services/) e [Serviço de Aplicativo - Aplicativos Web](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="70bd3-107">While this walkthrough explains the steps for VM Scale Sets, the same information applies to autoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="70bd3-108">Para uma configuração simples de redução/escala horizontal em um Conjunto de Dimensionamento de VM com base em um métrica de desempenho simples, como CPU, consulte os documentos [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) e [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md)</span><span class="sxs-lookup"><span data-stu-id="70bd3-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer to the [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="70bd3-109">Passo a passo</span><span class="sxs-lookup"><span data-stu-id="70bd3-109">Walkthrough</span></span>
<span data-ttu-id="70bd3-110">Neste passo a passo, usamos [Azure Resource Manager](https://resources.azure.com/) para configurar e atualizar a configuração de dimensionamento automático para um conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="70bd3-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) to configure and update the autoscale setting for a scale set.</span></span> <span data-ttu-id="70bd3-111">O Gerenciador de Recursos do Azure é uma maneira fácil de gerenciar recursos do Azure por meio de modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="70bd3-111">Azure Resource Explorer is an easy way to manage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="70bd3-112">Se você não conhece bem a ferramenta do Azure Resource Manager, leia [esta introdução](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span><span class="sxs-lookup"><span data-stu-id="70bd3-112">If you are new to Azure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="70bd3-113">Implante um novo conjunto de dimensionamento com configuração básica de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="70bd3-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="70bd3-114">Este artigo usa um da Galeria de Início Rápido do Azure que tem um conjunto de dimensionamento do Windows com o modelo básico de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="70bd3-114">This article uses the one from the Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="70bd3-115">Os conjuntos de dimensionamento do Linux funcionam da mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="70bd3-115">Linux scale sets work the same way.</span></span>
2. <span data-ttu-id="70bd3-116">Depois que o conjunto de dimensionamento é criado, navegue até o recurso do conjunto de dimensionamento do Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="70bd3-116">After the scale set is created, navigate to the scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="70bd3-117">Você verá o item a seguir no nó do Microsoft.Insights.</span><span class="sxs-lookup"><span data-stu-id="70bd3-117">You see the following under Microsoft.Insights node.</span></span>

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="70bd3-119">A execução do modelo criou uma configuração padrão de dimensionamento automático com o nome **'autoscalewad'**.</span><span class="sxs-lookup"><span data-stu-id="70bd3-119">The template execution has created a default autoscale setting with the name **'autoscalewad'**.</span></span> <span data-ttu-id="70bd3-120">No lado direito, você pode exibir a definição completa dessa configuração de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="70bd3-120">On the right-hand side, you can view the full definition of this autoscale setting.</span></span> <span data-ttu-id="70bd3-121">Nesse caso, a configuração de dimensionamento automático padrão vem com uma regra de escala e redução baseada em % CPU.</span><span class="sxs-lookup"><span data-stu-id="70bd3-121">In this case, the default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="70bd3-122">Agora você pode adicionar mais perfis e regras com base no agendamento ou em requisitos específicos.</span><span class="sxs-lookup"><span data-stu-id="70bd3-122">You can now add more profiles and rules based on the schedule or specific requirements.</span></span> <span data-ttu-id="70bd3-123">Podemos criar uma configuração de dimensionamento automático com três perfis.</span><span class="sxs-lookup"><span data-stu-id="70bd3-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="70bd3-124">Para entender as regras de dimensionamento automático e perfis, confira [Práticas recomendadas de dimensionamento automático](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="70bd3-124">To understand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="70bd3-125">Perfis e regras</span><span class="sxs-lookup"><span data-stu-id="70bd3-125">Profiles & Rules</span></span> | <span data-ttu-id="70bd3-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="70bd3-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="70bd3-127">**Perfil**</span><span class="sxs-lookup"><span data-stu-id="70bd3-127">**Profile**</span></span> |<span data-ttu-id="70bd3-128">**Baseado em desempenho/métrica**</span><span class="sxs-lookup"><span data-stu-id="70bd3-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="70bd3-129">Regra</span><span class="sxs-lookup"><span data-stu-id="70bd3-129">Rule</span></span> |<span data-ttu-id="70bd3-130">Contagem de mensagens de fila de Barramento de Serviço > x</span><span class="sxs-lookup"><span data-stu-id="70bd3-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="70bd3-131">Regra</span><span class="sxs-lookup"><span data-stu-id="70bd3-131">Rule</span></span> |<span data-ttu-id="70bd3-132">Contagem de mensagens de fila de Barramento de Serviço < y</span><span class="sxs-lookup"><span data-stu-id="70bd3-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="70bd3-133">Regra</span><span class="sxs-lookup"><span data-stu-id="70bd3-133">Rule</span></span> |<span data-ttu-id="70bd3-134">CPU% > n</span><span class="sxs-lookup"><span data-stu-id="70bd3-134">CPU% > n</span></span> |
    | <span data-ttu-id="70bd3-135">Regra</span><span class="sxs-lookup"><span data-stu-id="70bd3-135">Rule</span></span> |<span data-ttu-id="70bd3-136">% CPU < p</span><span class="sxs-lookup"><span data-stu-id="70bd3-136">CPU% < p</span></span> |
    | <span data-ttu-id="70bd3-137">**Perfil**</span><span class="sxs-lookup"><span data-stu-id="70bd3-137">**Profile**</span></span> |<span data-ttu-id="70bd3-138">**Horas da manhã de dia de semana, (sem regras)**</span><span class="sxs-lookup"><span data-stu-id="70bd3-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="70bd3-139">**Perfil**</span><span class="sxs-lookup"><span data-stu-id="70bd3-139">**Profile**</span></span> |<span data-ttu-id="70bd3-140">**Dia de lançamento do produto (sem regras)**</span><span class="sxs-lookup"><span data-stu-id="70bd3-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="70bd3-141">Eis um cenário hipotético de dimensionamento que usaremos para este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="70bd3-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="70bd3-142">**Baseado em carga** ‑ Desejo escalar ou reduzir horizontalmente com base na carga do aplicativo hospedado no conjunto de dimensionamento.*</span><span class="sxs-lookup"><span data-stu-id="70bd3-142">**Load based** - I'd like to scale out or in based on the load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="70bd3-143">**Tamanho da Fila de Mensagens** ‑ Uso uma Fila do Barramento de Serviço para as mensagens recebidas pelo meu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70bd3-143">**Message Queue size** - I use a Service Bus Queue for the incoming messages to my application.</span></span> <span data-ttu-id="70bd3-144">Uso contagem de mensagens da fila e o percentual de CPU e configuro um perfil padrão para disparar uma ação de escala se a contagem de mensagens ou CPU atingir o limite.*</span><span class="sxs-lookup"><span data-stu-id="70bd3-144">I use the queue's message count and CPU% and configure a default profile to trigger a scale action if either of message count or CPU hits the threshold.*</span></span>
    * <span data-ttu-id="70bd3-145">**Dia e hora da semana** ‑ Desejo ter um perfil baseado na “hora do dia” recorrente semanal chamado “Horas da manhã de dias da semana”.</span><span class="sxs-lookup"><span data-stu-id="70bd3-145">**Time of week and day** - I want a weekly recurring 'time of the day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="70bd3-146">Com base nos dados históricos, sei que é melhor ter determinado número de instâncias de VM para lidar com a carga do meu aplicativo durante esse período.*</span><span class="sxs-lookup"><span data-stu-id="70bd3-146">Based on historical data, I know it is better to have certain number of VM instances to handle my application's load during this time.*</span></span>
    * <span data-ttu-id="70bd3-147">**Datas especiais** ‑ Adicionei um perfil de “Dia de lançamento de produto”.</span><span class="sxs-lookup"><span data-stu-id="70bd3-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="70bd3-148">Planejo com antecedência em relação a datas específicas para que meu aplicativo esteja pronto para lidar com a carga devido a anúncios de marketing e quando colocamos um novo produto no aplicativo.*</span><span class="sxs-lookup"><span data-stu-id="70bd3-148">I plan ahead for specific dates so my application is ready to handle the load due marketing announcements and when we put a new product in the application.*</span></span>
    * <span data-ttu-id="70bd3-149">*Os últimos dois perfis também podem ter outras regras com base em métrica de desempenho dentro deles. Nesse caso, decidi por não ter um e, em vez disso, contar com as regras com base em métricas de desempenho padrão. As regras são opcionais para perfis baseados em recorrência e data.*</span><span class="sxs-lookup"><span data-stu-id="70bd3-149">*The last two profiles can also have other performance metric based rules within them. In this case, I decided not to have one and instead to rely on the default performance metric based rules. Rules are optional for the recurring and date-based profiles.*</span></span>

    <span data-ttu-id="70bd3-150">A priorização de perfis e regras do mecanismo de dimensionamento automático também é vista no artigo [Práticas recomendadas de dimensionamento automático](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="70bd3-150">Autoscale engine's prioritization of the profiles and rules is also captured in the [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="70bd3-151">Para obter uma lista de métricas comuns para dimensionamento automático, confira [Métricas comuns para o dimensionamento automático](insights-autoscale-common-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="70bd3-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="70bd3-152">Verifique se você está usando o modo de **leitura/gravação** no Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="70bd3-152">Make sure you are on the **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, configuração de dimensionamento automático padrão](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="70bd3-154">Clique em Editar.</span><span class="sxs-lookup"><span data-stu-id="70bd3-154">Click Edit.</span></span> <span data-ttu-id="70bd3-155">**Substitua** o elemento “perfis” na configuração de dimensionamento automático pela seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="70bd3-155">**Replace** the 'profiles' element in autoscale setting with the following configuration:</span></span>

    ![perfis](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    <span data-ttu-id="70bd3-157">Para campos com suporte e seus valores, confira [Documentação da API REST de Dimensionamento Automático](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="70bd3-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="70bd3-158">Agora, sua configuração de dimensionamento automático contém os três perfis explicados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="70bd3-158">Now your autoscale setting contains the three profiles explained previously.</span></span>

7. <span data-ttu-id="70bd3-159">Finalmente, veja a seção **Notificação** de Dimensionamento Automático.</span><span class="sxs-lookup"><span data-stu-id="70bd3-159">Finally, look at the Autoscale **notification** section.</span></span> <span data-ttu-id="70bd3-160">As notificações de dimensionamento automático permitem fazer três coisas quando uma ação de escala ou redução horizontal é disparada com êxito.</span><span class="sxs-lookup"><span data-stu-id="70bd3-160">Autoscale notifications allow you to do three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="70bd3-161">Notificar o administrador e coadministradores de sua assinatura</span><span class="sxs-lookup"><span data-stu-id="70bd3-161">Notify the admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="70bd3-162">Enviar email a um conjunto de usuários</span><span class="sxs-lookup"><span data-stu-id="70bd3-162">Email a set of users</span></span>
   - <span data-ttu-id="70bd3-163">Disparar uma chamada webhook.</span><span class="sxs-lookup"><span data-stu-id="70bd3-163">Trigger a webhook call.</span></span> <span data-ttu-id="70bd3-164">Quando disparado, esse webhook enviará metadados sobre a condição de dimensionamento automático e do recurso de conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="70bd3-164">When fired, this webhook sends metadata about the autoscaling condition and the scale set resource.</span></span> <span data-ttu-id="70bd3-165">Para saber mais sobre a carga de webhook de dimensionamento automático, confira [Configurar webhook e notificações por email para dimensionamento automático](insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="70bd3-165">To learn more about the payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="70bd3-166">Adicionar o seguinte à configuração de dimensionamento automático substituindo o elemento **notificação** cujo valor é nulo</span><span class="sxs-lookup"><span data-stu-id="70bd3-166">Add the following to the Autoscale setting replacing your **notification** element whose value is null</span></span>

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
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

   <span data-ttu-id="70bd3-167">Pressione o botão **Colocar** no Gerenciador de Recursos para atualizar a configuração de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="70bd3-167">Hit **Put** button in Resource Explorer to update the autoscale setting.</span></span>

<span data-ttu-id="70bd3-168">Você atualizou uma configuração de dimensionamento automático em um conjunto de escala de VM definido para incluir vários perfis e notificações de escala.</span><span class="sxs-lookup"><span data-stu-id="70bd3-168">You have updated an autoscale setting on a VM Scale set to include multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70bd3-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70bd3-169">Next Steps</span></span>
<span data-ttu-id="70bd3-170">Use estes links para saber mais sobre o dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="70bd3-170">Use these links to learn more about autoscaling.</span></span>

[<span data-ttu-id="70bd3-171">Solucionar problemas de autoescala com conjuntos de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="70bd3-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="70bd3-172">Métricas comuns para o dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="70bd3-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="70bd3-173">Práticas Recomendadas para o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="70bd3-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="70bd3-174">Gerenciar o dimensionamento automático usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="70bd3-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="70bd3-175">Gerenciar o dimensionamento automático usando a CLI</span><span class="sxs-lookup"><span data-stu-id="70bd3-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="70bd3-176">Configurar webhooks e notificações por email para dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="70bd3-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
