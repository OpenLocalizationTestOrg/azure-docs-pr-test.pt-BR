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
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a>Configuração avançada de autoescala usando modelos do Resource Manager para Conjuntos de Dimensionamento de VMs
Você pode escalar e reduzir horizontalmente Conjuntos de Dimensionamento de Máquina Virtual com base nos limites de métrica de desempenho, em uma agenda recorrente ou em determinada data. Você também pode configurar notificações por email e webhook para ações de escala. Este passo a passo mostra um exemplo de configuração de todos esses objetos usando um modelo do Resource Manager em um Conjunto de Dimensionamento de VMs.

> [!NOTE]
> Embora este passo a passo explica as etapas de saudação para conjuntos de escala de VM, hello informações mesmo se aplica tooautoscaling [serviços de nuvem](https://azure.microsoft.com/services/cloud-services/), e [do serviço de aplicativo - aplicativos Web](https://azure.microsoft.com/services/app-service/web/).
> Uma escala simple de entrada/saída de configuração em um conjunto de escala de VM com base em uma métrica de desempenho simples, como CPU, consulte toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) e [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documentos
>
>

## <a name="walkthrough"></a>Passo a passo
Neste passo a passo, usamos [Gerenciador de recursos do Azure](https://resources.azure.com/) tooconfigure e atualização de configuração de dimensionamento automático de saudação para um conjunto de escala. Gerenciador de recursos do Azure é uma maneira fácil toomanage recursos do Azure por meio de modelos do Gerenciador de recursos. Se você estiver nova ferramenta de Gerenciador de recursos de tooAzure, leia [esta introdução](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).

1. Implante um novo conjunto de dimensionamento com configuração básica de dimensionamento automático. Este artigo usa Olá da saudação Galeria de início rápido do Azure, que tem uma janela de conjunto de escala com um modelo básico de dimensionamento automático. Escala de Linux define trabalho Olá mesma maneira.
2. Após a criação do conjunto de escala hello, navegue toohello escala conjunto de recursos do Gerenciador de recursos do Azure. Você verá o seguinte Olá nó Insights.

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    execução de modelo Olá criou uma configuração de dimensionamento automático padrão com o nome da saudação **'autoscalewad'**. No lado direito da saudação, você pode exibir a definição completa Olá dessa configuração de dimensionamento automático. Nesse caso, a configuração de AutoEscala saudação padrão vem com uma regra de CPU % com base em expansão e escala no.  

3. Agora você pode adicionar mais perfis e regras com base no agendamento de saudação ou requisitos específicos. Podemos criar uma configuração de dimensionamento automático com três perfis. perfis de toounderstand e regras de dimensionamento automático, examine [práticas recomendadas de dimensionamento automático](insights-autoscale-best-practices.md).  

    | Perfis e regras | Descrição |
    |--- | --- |
    | **Perfil** |**Baseado em desempenho/métrica** |
    | Regra |Contagem de mensagens de fila de Barramento de Serviço > x |
    | Regra |Contagem de mensagens de fila de Barramento de Serviço < y |
    | Regra |CPU% > n |
    | Regra |% CPU < p |
    | **Perfil** |**Horas da manhã de dia de semana, (sem regras)** |
    | **Perfil** |**Dia de lançamento do produto (sem regras)** |

4. Eis um cenário hipotético de dimensionamento que usaremos para este passo a passo.

    * **Carga com base em** -gostaria tooscale out ou com base na carga de saudação em meu aplicativo hospedado em meu set.* de escala
    * **Tamanho da fila de mensagens** -posso usar uma fila do barramento de serviço para o aplicativo de toomy de mensagens de entrada hello. Uso de contagem de mensagens da fila hello e % de CPU e configurar um perfil de padrão tootrigger uma ação de escala se a contagem de mensagens ou CPU acertos Olá threshold.*
    * **Hora do dia e semana** -desejo um perfil de 'tempo do dia de saudação' com base semanal recorrente chamado 'Horas da manhã dia da semana'. Com base em dados históricos, saber é melhor toohave determinado de VM instâncias toohandle de carga do meu aplicativo durante esse tempo. *
    * **Datas especiais** ‑ Adicionei um perfil de “Dia de lançamento de produto”. Planeje com antecedência para datas específicas para que meu aplicativo está pronto toohandle Olá carga devido anúncios de marketing e quando, colocamos um novo produto no Application Olá
    * *últimos dois perfis de saudação também podem ter outras regras com base métrica de desempenho dentro deles. Nesse caso, decidi não toohave um e, em vez disso, toorely na métrica de desempenho do saudação padrão com base em regras. As regras são opcionais para perfis de saudação recorrente e baseado em data.*

    Priorização de dimensionamento automático do mecanismo de regras e perfis de saudação também é capturada no hello [práticas recomendadas de dimensionamento automático](insights-autoscale-best-practices.md) artigo.
    Para obter uma lista de métricas comuns para dimensionamento automático, confira [Métricas comuns para o dimensionamento automático](insights-autoscale-common-metrics.md)

5. Verifique se você está no hello **leitura/gravação** modo no Gerenciador de recursos

    ![Autoscalewad, configuração de dimensionamento automático padrão](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. Clique em Editar. **Substituir** elemento perfis' hello' na configuração de dimensionamento automático com hello a seguinte configuração:

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
    Para campos com suporte e seus valores, confira [Documentação da API REST de Dimensionamento Automático](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx). Agora sua configuração de dimensionamento automático contém três perfis de saudação explicados anteriormente.

7. Finalmente, veja Olá AutoEscala **notificação** seção. Notificações de dimensionamento automático permitem toodo três ações quando uma expansão ou na ação é disparado com êxito.
   - Notificar Olá administrador e coadministradores da sua assinatura
   - Enviar email a um conjunto de usuários
   - Disparar uma chamada webhook. Quando disparado, esse webhook envia metadados sobre a condição de dimensionamento automático hello e recursos do conjunto de escala de saudação. toolearn mais informações sobre a carga de saudação do webhook de dimensionamento automático, consulte [Webhook configurar & notificações por Email para dimensionamento automático](insights-autoscale-to-webhook-email.md).

   Adicionar Olá após a substituição de configuração de AutoEscala toohello seu **notificação** elemento cujo valor é nulo

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

   Acertos **colocar** botão na configuração de dimensionamento automático do Gerenciador de recursos tooupdate hello.

Você atualizou uma configuração em um tooinclude de conjunto de escalas de VM vários perfis de escala de AutoEscala e dimensionar as notificações.

## <a name="next-steps"></a>Próximas etapas
Use esses toolearn links mais informações sobre o dimensionamento automático.

[Solucionar problemas de autoescala com conjuntos de dimensionamento de máquinas virtuais](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[Métricas comuns para o dimensionamento automático](insights-autoscale-common-metrics.md)

[Práticas Recomendadas para o Serviço de Aplicativo do Azure](insights-autoscale-best-practices.md)

[Gerenciar o dimensionamento automático usando o PowerShell](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[Gerenciar o dimensionamento automático usando a CLI](insights-cli-samples.md#autoscale)

[Configurar webhooks e notificações por email para dimensionamento automático](insights-autoscale-to-webhook-email.md)
