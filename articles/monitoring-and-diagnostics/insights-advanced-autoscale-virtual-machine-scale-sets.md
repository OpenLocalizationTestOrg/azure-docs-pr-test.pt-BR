---
title: "aaaAdvanced AutoEscala usando máquinas virtuais do Azure | Microsoft Docs"
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
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="809ba-103">Configuração avançada de autoescala usando modelos do Resource Manager para Conjuntos de Dimensionamento de VMs</span><span class="sxs-lookup"><span data-stu-id="809ba-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="809ba-104">Você pode escalar e reduzir horizontalmente Conjuntos de Dimensionamento de Máquina Virtual com base nos limites de métrica de desempenho, em uma agenda recorrente ou em determinada data.</span><span class="sxs-lookup"><span data-stu-id="809ba-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="809ba-105">Você também pode configurar notificações por email e webhook para ações de escala.</span><span class="sxs-lookup"><span data-stu-id="809ba-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="809ba-106">Este passo a passo mostra um exemplo de configuração de todos esses objetos usando um modelo do Resource Manager em um Conjunto de Dimensionamento de VMs.</span><span class="sxs-lookup"><span data-stu-id="809ba-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="809ba-107">Embora este passo a passo explica as etapas de saudação para conjuntos de escala de VM, hello informações mesmo se aplica tooautoscaling [serviços de nuvem](https://azure.microsoft.com/services/cloud-services/), e [do serviço de aplicativo - aplicativos Web](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="809ba-107">While this walkthrough explains hello steps for VM Scale Sets, hello same information applies tooautoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="809ba-108">Uma escala simple de entrada/saída de configuração em um conjunto de escala de VM com base em uma métrica de desempenho simples, como CPU, consulte toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) e [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documentos</span><span class="sxs-lookup"><span data-stu-id="809ba-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="809ba-109">Passo a passo</span><span class="sxs-lookup"><span data-stu-id="809ba-109">Walkthrough</span></span>
<span data-ttu-id="809ba-110">Neste passo a passo, usamos [Gerenciador de recursos do Azure](https://resources.azure.com/) tooconfigure e atualização de configuração de dimensionamento automático de saudação para um conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="809ba-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) tooconfigure and update hello autoscale setting for a scale set.</span></span> <span data-ttu-id="809ba-111">Gerenciador de recursos do Azure é uma maneira fácil toomanage recursos do Azure por meio de modelos do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="809ba-111">Azure Resource Explorer is an easy way toomanage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="809ba-112">Se você estiver nova ferramenta de Gerenciador de recursos de tooAzure, leia [esta introdução](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span><span class="sxs-lookup"><span data-stu-id="809ba-112">If you are new tooAzure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="809ba-113">Implante um novo conjunto de dimensionamento com configuração básica de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="809ba-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="809ba-114">Este artigo usa Olá da saudação Galeria de início rápido do Azure, que tem uma janela de conjunto de escala com um modelo básico de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="809ba-114">This article uses hello one from hello Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="809ba-115">Escala de Linux define trabalho Olá mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="809ba-115">Linux scale sets work hello same way.</span></span>
2. <span data-ttu-id="809ba-116">Após a criação do conjunto de escala hello, navegue toohello escala conjunto de recursos do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="809ba-116">After hello scale set is created, navigate toohello scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="809ba-117">Você verá o seguinte Olá nó Insights.</span><span class="sxs-lookup"><span data-stu-id="809ba-117">You see hello following under Microsoft.Insights node.</span></span>

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="809ba-119">execução de modelo Olá criou uma configuração de dimensionamento automático padrão com o nome da saudação **'autoscalewad'**.</span><span class="sxs-lookup"><span data-stu-id="809ba-119">hello template execution has created a default autoscale setting with hello name **'autoscalewad'**.</span></span> <span data-ttu-id="809ba-120">No lado direito da saudação, você pode exibir a definição completa Olá dessa configuração de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="809ba-120">On hello right-hand side, you can view hello full definition of this autoscale setting.</span></span> <span data-ttu-id="809ba-121">Nesse caso, a configuração de AutoEscala saudação padrão vem com uma regra de CPU % com base em expansão e escala no.</span><span class="sxs-lookup"><span data-stu-id="809ba-121">In this case, hello default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="809ba-122">Agora você pode adicionar mais perfis e regras com base no agendamento de saudação ou requisitos específicos.</span><span class="sxs-lookup"><span data-stu-id="809ba-122">You can now add more profiles and rules based on hello schedule or specific requirements.</span></span> <span data-ttu-id="809ba-123">Podemos criar uma configuração de dimensionamento automático com três perfis.</span><span class="sxs-lookup"><span data-stu-id="809ba-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="809ba-124">perfis de toounderstand e regras de dimensionamento automático, examine [práticas recomendadas de dimensionamento automático](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="809ba-124">toounderstand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="809ba-125">Perfis e regras</span><span class="sxs-lookup"><span data-stu-id="809ba-125">Profiles & Rules</span></span> | <span data-ttu-id="809ba-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="809ba-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="809ba-127">**Perfil**</span><span class="sxs-lookup"><span data-stu-id="809ba-127">**Profile**</span></span> |<span data-ttu-id="809ba-128">**Baseado em desempenho/métrica**</span><span class="sxs-lookup"><span data-stu-id="809ba-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="809ba-129">Regra</span><span class="sxs-lookup"><span data-stu-id="809ba-129">Rule</span></span> |<span data-ttu-id="809ba-130">Contagem de mensagens de fila de Barramento de Serviço > x</span><span class="sxs-lookup"><span data-stu-id="809ba-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="809ba-131">Regra</span><span class="sxs-lookup"><span data-stu-id="809ba-131">Rule</span></span> |<span data-ttu-id="809ba-132">Contagem de mensagens de fila de Barramento de Serviço < y</span><span class="sxs-lookup"><span data-stu-id="809ba-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="809ba-133">Regra</span><span class="sxs-lookup"><span data-stu-id="809ba-133">Rule</span></span> |<span data-ttu-id="809ba-134">CPU% > n</span><span class="sxs-lookup"><span data-stu-id="809ba-134">CPU% > n</span></span> |
    | <span data-ttu-id="809ba-135">Regra</span><span class="sxs-lookup"><span data-stu-id="809ba-135">Rule</span></span> |<span data-ttu-id="809ba-136">% CPU < p</span><span class="sxs-lookup"><span data-stu-id="809ba-136">CPU% < p</span></span> |
    | <span data-ttu-id="809ba-137">**Perfil**</span><span class="sxs-lookup"><span data-stu-id="809ba-137">**Profile**</span></span> |<span data-ttu-id="809ba-138">**Horas da manhã de dia de semana, (sem regras)**</span><span class="sxs-lookup"><span data-stu-id="809ba-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="809ba-139">**Perfil**</span><span class="sxs-lookup"><span data-stu-id="809ba-139">**Profile**</span></span> |<span data-ttu-id="809ba-140">**Dia de lançamento do produto (sem regras)**</span><span class="sxs-lookup"><span data-stu-id="809ba-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="809ba-141">Eis um cenário hipotético de dimensionamento que usaremos para este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="809ba-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="809ba-142">**Carga com base em** -gostaria tooscale out ou com base na carga de saudação em meu aplicativo hospedado em meu set.* de escala</span><span class="sxs-lookup"><span data-stu-id="809ba-142">**Load based** - I'd like tooscale out or in based on hello load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="809ba-143">**Tamanho da fila de mensagens** -posso usar uma fila do barramento de serviço para o aplicativo de toomy de mensagens de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="809ba-143">**Message Queue size** - I use a Service Bus Queue for hello incoming messages toomy application.</span></span> <span data-ttu-id="809ba-144">Uso de contagem de mensagens da fila hello e % de CPU e configurar um perfil de padrão tootrigger uma ação de escala se a contagem de mensagens ou CPU acertos Olá threshold.*</span><span class="sxs-lookup"><span data-stu-id="809ba-144">I use hello queue's message count and CPU% and configure a default profile tootrigger a scale action if either of message count or CPU hits hello threshold.*</span></span>
    * <span data-ttu-id="809ba-145">**Hora do dia e semana** -desejo um perfil de 'tempo do dia de saudação' com base semanal recorrente chamado 'Horas da manhã dia da semana'.</span><span class="sxs-lookup"><span data-stu-id="809ba-145">**Time of week and day** - I want a weekly recurring 'time of hello day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="809ba-146">Com base em dados históricos, saber é melhor toohave determinado de VM instâncias toohandle de carga do meu aplicativo durante esse tempo. *</span><span class="sxs-lookup"><span data-stu-id="809ba-146">Based on historical data, I know it is better toohave certain number of VM instances toohandle my application's load during this time.*</span></span>
    * <span data-ttu-id="809ba-147">**Datas especiais** ‑ Adicionei um perfil de “Dia de lançamento de produto”.</span><span class="sxs-lookup"><span data-stu-id="809ba-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="809ba-148">Planeje com antecedência para datas específicas para que meu aplicativo está pronto toohandle Olá carga devido anúncios de marketing e quando, colocamos um novo produto no Application Olá</span><span class="sxs-lookup"><span data-stu-id="809ba-148">I plan ahead for specific dates so my application is ready toohandle hello load due marketing announcements and when we put a new product in hello application.*</span></span>
    * <span data-ttu-id="809ba-149">*últimos dois perfis de saudação também podem ter outras regras com base métrica de desempenho dentro deles. Nesse caso, decidi não toohave um e, em vez disso, toorely na métrica de desempenho do saudação padrão com base em regras. As regras são opcionais para perfis de saudação recorrente e baseado em data.*</span><span class="sxs-lookup"><span data-stu-id="809ba-149">*hello last two profiles can also have other performance metric based rules within them. In this case, I decided not toohave one and instead toorely on hello default performance metric based rules. Rules are optional for hello recurring and date-based profiles.*</span></span>

    <span data-ttu-id="809ba-150">Priorização de dimensionamento automático do mecanismo de regras e perfis de saudação também é capturada no hello [práticas recomendadas de dimensionamento automático](insights-autoscale-best-practices.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="809ba-150">Autoscale engine's prioritization of hello profiles and rules is also captured in hello [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="809ba-151">Para obter uma lista de métricas comuns para dimensionamento automático, confira [Métricas comuns para o dimensionamento automático](insights-autoscale-common-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="809ba-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="809ba-152">Verifique se você está no hello **leitura/gravação** modo no Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="809ba-152">Make sure you are on hello **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, configuração de dimensionamento automático padrão](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="809ba-154">Clique em Editar.</span><span class="sxs-lookup"><span data-stu-id="809ba-154">Click Edit.</span></span> <span data-ttu-id="809ba-155">**Substituir** elemento perfis' hello' na configuração de dimensionamento automático com hello a seguinte configuração:</span><span class="sxs-lookup"><span data-stu-id="809ba-155">**Replace** hello 'profiles' element in autoscale setting with hello following configuration:</span></span>

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
    <span data-ttu-id="809ba-157">Para campos com suporte e seus valores, confira [Documentação da API REST de Dimensionamento Automático](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="809ba-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="809ba-158">Agora sua configuração de dimensionamento automático contém três perfis de saudação explicados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="809ba-158">Now your autoscale setting contains hello three profiles explained previously.</span></span>

7. <span data-ttu-id="809ba-159">Finalmente, veja Olá AutoEscala **notificação** seção.</span><span class="sxs-lookup"><span data-stu-id="809ba-159">Finally, look at hello Autoscale **notification** section.</span></span> <span data-ttu-id="809ba-160">Notificações de dimensionamento automático permitem toodo três ações quando uma expansão ou na ação é disparado com êxito.</span><span class="sxs-lookup"><span data-stu-id="809ba-160">Autoscale notifications allow you toodo three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="809ba-161">Notificar Olá administrador e coadministradores da sua assinatura</span><span class="sxs-lookup"><span data-stu-id="809ba-161">Notify hello admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="809ba-162">Enviar email a um conjunto de usuários</span><span class="sxs-lookup"><span data-stu-id="809ba-162">Email a set of users</span></span>
   - <span data-ttu-id="809ba-163">Disparar uma chamada webhook.</span><span class="sxs-lookup"><span data-stu-id="809ba-163">Trigger a webhook call.</span></span> <span data-ttu-id="809ba-164">Quando disparado, esse webhook envia metadados sobre a condição de dimensionamento automático hello e recursos do conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="809ba-164">When fired, this webhook sends metadata about hello autoscaling condition and hello scale set resource.</span></span> <span data-ttu-id="809ba-165">toolearn mais informações sobre a carga de saudação do webhook de dimensionamento automático, consulte [Webhook configurar & notificações por Email para dimensionamento automático](insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="809ba-165">toolearn more about hello payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="809ba-166">Adicionar Olá após a substituição de configuração de AutoEscala toohello seu **notificação** elemento cujo valor é nulo</span><span class="sxs-lookup"><span data-stu-id="809ba-166">Add hello following toohello Autoscale setting replacing your **notification** element whose value is null</span></span>

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

   <span data-ttu-id="809ba-167">Acertos **colocar** botão na configuração de dimensionamento automático do Gerenciador de recursos tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="809ba-167">Hit **Put** button in Resource Explorer tooupdate hello autoscale setting.</span></span>

<span data-ttu-id="809ba-168">Você atualizou uma configuração em um tooinclude de conjunto de escalas de VM vários perfis de escala de AutoEscala e dimensionar as notificações.</span><span class="sxs-lookup"><span data-stu-id="809ba-168">You have updated an autoscale setting on a VM Scale set tooinclude multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="809ba-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="809ba-169">Next Steps</span></span>
<span data-ttu-id="809ba-170">Use esses toolearn links mais informações sobre o dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="809ba-170">Use these links toolearn more about autoscaling.</span></span>

[<span data-ttu-id="809ba-171">Solucionar problemas de autoescala com conjuntos de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="809ba-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="809ba-172">Métricas comuns para o dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="809ba-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="809ba-173">Práticas Recomendadas para o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="809ba-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="809ba-174">Gerenciar o dimensionamento automático usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="809ba-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="809ba-175">Gerenciar o dimensionamento automático usando a CLI</span><span class="sxs-lookup"><span data-stu-id="809ba-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="809ba-176">Configurar webhooks e notificações por email para dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="809ba-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
