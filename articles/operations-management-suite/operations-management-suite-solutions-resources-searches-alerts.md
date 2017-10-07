---
title: "aaaSaved pesquisas e alertas em soluções do OMS | Microsoft Docs"
description: "Soluções do OMS normalmente incluirá as pesquisas salvas em dados de tooanalyze de análise de Log coletados pela solução de saudação.  Eles podem também definir usuário de saudação toonotify alertas ou entram em ação automaticamente em um problema crítico de tooa de resposta.  Este artigo descreve como toodefine análise de Log salvos pesquisas e alertas em um modelo do ARM para que possam ser incluídos em soluções de gerenciamento."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a>Adição de análise de Log salvo tooOMS pesquisas e alertas de solução de gerenciamento (visualização)

> [!NOTE]
> Esta é uma documentação preliminar para criar soluções de gerenciamento no OMS, que estão atualmente em visualização. Qualquer esquema descrita abaixo é toochange de assunto.   


[Soluções de gerenciamento do OMS](operations-management-suite-solutions.md) geralmente inclui [pesquisas salvas](../log-analytics/log-analytics-log-searches.md) nos dados de tooanalyze de análise de Log coletados pela solução de saudação.  Eles também podem definir [alertas](../log-analytics/log-analytics-alerts.md) toonotify Olá usuário ou entram em ação automaticamente em um problema crítico de tooa de resposta.  Este artigo descreve como toodefine análise de Log salvos pesquisas e alertas em um [modelo de gerenciamento de recursos](../resource-manager-template-walkthrough.md) para que eles podem ser incluídos em [soluções de gerenciamento de](operations-management-suite-solutions-creating.md).

> [!NOTE]
> Olá exemplos neste artigo usam parâmetros e variáveis que são ambos soluções toomanagement necessárias ou comuns e descritos na [criando soluções de gerenciamento no OMS Operations Management Suite ()](operations-management-suite-solutions-creating.md)  

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você já está familiarizado com como muito[criar uma solução de gerenciamento](operations-management-suite-solutions-creating.md) e a estrutura de saudação de um [modelo do ARM](../resource-group-authoring-templates.md) e o arquivo de solução.


## <a name="log-analytics-workspace"></a>Espaço de trabalho do Log Analytics
Todos os recursos de Log Analytics estão contidos em um [espaço](../log-analytics/log-analytics-manage-access.md).  Conforme descrito em [OMS espaço de trabalho e a conta de automação](operations-management-suite-solutions.md#oms-workspace-and-automation-account) espaço de trabalho de saudação não está incluído na solução de gerenciamento de hello, mas deve existir antes de saudação solução estiver instalada.  Se não estiver disponível, Olá solução instalação falhará.

nome de saudação do espaço de trabalho de saudação está em nome de saudação de cada recurso de análise de Log.  Isso é feito na solução de saudação com hello **espaço de trabalho** parâmetro como Olá seguinte exemplo de um recurso de savedsearch.

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a>Pesquisas salvas
Incluir [pesquisas salvas](../log-analytics/log-analytics-log-searches.md) em um solução tooallow usuários tooquery dados coletados pela sua solução.  Pesquisas salvas serão exibidas sob o **Favoritos** no portal do OMS hello e **pesquisas salvas** em Olá portal do Azure.  Uma pesquisa salva também é necessária para cada alerta.   

[Pesquisa de análise de log salva](../log-analytics/log-analytics-log-searches.md) recursos têm um tipo de `Microsoft.OperationalInsights/workspaces/savedSearches` e ter Olá estrutura a seguir.  Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello. 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



Cada uma das propriedades de saudação de pesquisas salvas são descritos na Olá a tabela a seguir. 

| Propriedade | Descrição |
|:--- |:--- |
| categoria | categoria de saudação de pesquisa salva hello.  Qualquer pesquisas salvas em Olá mesma solução geralmente compartilharão uma única categoria para que eles são agrupados juntos no console de saudação. |
| displayname | Nome toodisplay para Olá pesquisa salva no portal de saudação. |
| query | Toorun de consulta. |

> [!NOTE]
> Talvez seja necessário toouse caracteres de escape na consulta Olá se ele inclui os caracteres que podem ser interpretados como JSON.  Por exemplo, se a consulta foi **OperationName:"Microsoft.Compute/virtualMachines/write tipo: AzureActivity"**, ele deve ser gravado no arquivo de solução hello como **OperationName tipo: AzureActivity:\" Microsoft.Compute/virtualMachines/write\"**.

## <a name="alerts"></a>Alertas
[Alertas de Log Analytics](../log-analytics/log-analytics-alerts.md) são criados por regras de alerta que executar uma pesquisa salva em um intervalo regular.  Se os resultados de saudação de consulta Olá correspondam aos critérios especificados, será criado um registro de alerta e um ou mais ações são executadas.  

Regras de alerta em uma solução de gerenciamento são compostas de saudação três diferentes recursos a seguir.

- **Pesquisa salva.**  Define a pesquisa de log de saudação que será executada.  Várias regras de alerta podem compartilhar uma única pesquisa salva.
- **Agenda.**  Define a frequência hello pesquisa de log será executada.  Cada regra de alerta terá apenas um agendamento.
- **Ação de alerta.**  Cada regra de alerta terá um recurso de ação com um tipo de **alerta** que define os detalhes de saudação do alerta hello como critérios hello quando um registro de alerta será criado e Olá a severidade do alerta.  o recurso de ação Olá opcionalmente definirá uma resposta de email e o runbook.
- **Ação de Webhook (opcional).**  Se a regra de alerta Olá chamará um webhook, então requer um recurso de uma ação adicional com um tipo de **Webhook**.    

Salvar pesquisa recursos descritos acima.  Olá outros recursos são descritos abaixo.


### <a name="schedule-resource"></a>Recursos de agendamento

Uma pesquisa salva pode ter uma ou mais agendas com cada agenda que representa uma regra de alerta separada. Hello agendamento define quantas vezes hello pesquisa é executada e Olá intervalo de tempo pela qual Olá dados são recuperados.  Recursos de agendamento tem um tipo de `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` e ter Olá estrutura a seguir. Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello. 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



Propriedades de saudação para recursos de agendamento são descritas Olá a tabela a seguir.

| Nome do elemento | Obrigatório | Descrição |
|:--|:--|:--|
| Habilitado       | Sim | Especifica se o alerta de saudação é habilitado quando ele é criado. |
| intervalo      | Sim | Frequência hello consulta é executada em minutos. |
| queryTimeSpan | Sim | Período de tempo em minutos nos quais resultados tooevaluate. |

Olá agenda recurso depende de saudação pesquisa salva para que ele seja criado antes de agendamento de saudação.


### <a name="actions"></a>Ações
Há dois tipos de recurso de ação especificado pela Olá **tipo** propriedade.  Uma agenda requer um **alerta** ação que define os detalhes de saudação de regra de alerta hello e quais ações são executadas quando um alerta é criado.  Ele também pode incluir um **Webhook** ação se um webhook deve ser chamado de alerta de saudação.  

Recursos de ação com um tipo de `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.  

#### <a name="alert-actions"></a>Ações de alerta

Cada agenda terá um **alerta** ação.  Isso define os detalhes de saudação do alerta hello e, opcionalmente, as ações de notificação e correção.  Uma notificação envia um email tooone ou mais endereços.  Uma correção inicia um runbook na edição do Azure Automation tooattempt tooremediate Olá detectado.

Ações de alerta tem Olá estrutura a seguir.  Isso inclui variáveis e parâmetros comuns, para que você pode copiar e colar este trecho de código em seu arquivo de solução e altere os nomes de parâmetro hello. 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

Propriedades de saudação para recursos de ação de alerta são descritas Olá tabelas a seguir.

| Nome do elemento | Obrigatório | Descrição |
|:--|:--|:--|
| Tipo | Sim | Tipo de ação de saudação.  Isso será **alerta** para ações de alerta. |
| Nome | Sim | Nome de exibição de alerta de saudação.  Este é o nome de saudação que é exibido no console de saudação de regra de alerta de saudação. |
| Descrição | Não | Descrição opcional do alerta de saudação. |
| Severity | Sim | Severidade do alerta registro Olá Olá valores a seguir:<br><br> **Crítico**<br>**Aviso**<br>**Informativo** |


##### <a name="threshold"></a>Limite
Esta seção é necessária.  Ele define as propriedades de saudação para limite de alerta de saudação.

| Nome do elemento | Obrigatório | Descrição |
|:--|:--|:--|
| Operador | Sim | Operador de comparação de saudação do hello valores a seguir:<br><br>**gt = maior que<br>lt = menor que** |
| Valor | Sim | resultados de saudação do Hello valor toocompare. |


##### <a name="metricstrigger"></a>MetricsTrigger
Esta seção é opcional.  Inclua-o para um alerta de métrica de medição.

> [!NOTE]
> Alertas de métrica de medição estão atualmente em visualização pública. 

| Nome do elemento | Obrigatório | Descrição |
|:--|:--|:--|
| TriggerCondition | Sim | Especifica se o limite de saudação para o número total de violações ou falhas consecutivas da saudação valores a seguir:<br><br>**Total<br>consecutivas** |
| Operador | Sim | Operador de comparação de saudação do hello valores a seguir:<br><br>**gt = maior que<br>lt = menor que** |
| Valor | Sim | Número de saudação vezes Olá critérios deve ser atendido tootrigger alerta de saudação. |

##### <a name="throttling"></a>Limitação
Esta seção é opcional.  Inclua esta seção se deseja receber alertas toosuppress de saudação mesma regra por algum tempo depois que um alerta é criado.

| Nome do elemento | Obrigatório | Descrição |
|:--|:--|:--|
| DurationInMinutes | Sim, se a limitação elemento incluído | Número de alertas de toosuppress minutos depois que um de saudação mesma regra de alerta é criada. |

##### <a name="emailnotification"></a>EmailNotification
 Esta seção é opcional incluir se desejar Olá tooone de email de alerta toosend ou mais destinatários.

| Nome do elemento | Obrigatório | Descrição |
|:--|:--|:--|
| Destinatários | Sim | Lista delimitada por vírgulas de email endereços toosend notificação quando um alerta é criado, como no exemplo a seguir de saudação.<br><br>**[ "recipient1@contoso.com", "recipient2@contoso.com" ]** |
| Subject | Sim | Linha de assunto de mensagens de saudação. |
| Anexo | Não | Anexos não são atualmente suportados.  Se este elemento for incluído, ele deve ser **nenhum**. |


##### <a name="remediation"></a>Correção
Esta seção é opcional incluí-lo se você quiser toostart um runbook no alerta de toohello de resposta. |

| Nome do elemento | Obrigatório | Descrição |
|:--|:--|:--|
| RunbookName | Sim | Nome da saudação runbook toostart. |
| WebhookUri | Sim | URI do webhook Olá Olá runbook. |
| Expiry | Não | Data e hora em que Olá correção expira. |

#### <a name="webhook-actions"></a>Ações de Webhook

Ações de Webhook iniciar um processo chamar uma URL e, opcionalmente, fornecendo um toobe carga enviada. Eles são ações tooRemediation semelhantes, exceto que eles se destinam a webhooks que podem chamar outros processos além do runbooks de automação do Azure. Eles também fornecem a opção adicional de saudação do fornecimento de um processo remoto do toobe entregue toohello de carga.

Se o alerta chamará um webhook, será necessário um recurso de ação com um tipo de **Webhook** na adição toohello **alerta** recurso de ação.  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

Propriedades de saudação para recursos de ação de Webhook são descritas Olá tabelas a seguir.

| Nome do elemento | Obrigatório | Descrição |
|:--|:--|:--|
| type | Sim | Tipo de ação de saudação.  Isso será **Webhook** para ações de webhook. |
| name | Sim | Nome de exibição para a ação de saudação.  Isso não é exibido no console de saudação. |
| wehookUri | Sim | URI do webhook hello. |
| customPayload | Não | Carga personalizada toobe enviado toohello webhook. formato Olá dependerá de quais webhook hello está esperando. |




## <a name="sample"></a>Amostra

A seguir está um exemplo de uma solução que incluem que inclui Olá recursos a seguir:

- Pesquisa salva
- Agenda
- Ação de alerta
- Ações de webhook

Olá exemplo usa [parâmetros de solução padrão](operations-management-suite-solutions-solution-file.md#parameters) variáveis que normalmente seriam usados em uma solução como oposição toohardcoding valores nas definições de recursos de saudação.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for hello email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


Olá, arquivo de parâmetro a seguir fornece valores de exemplos para esta solução.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a>Próximas etapas
* [Adicionar modos de exibição](operations-management-suite-solutions-resources-views.md) tooyour solução de gerenciamento.
* [Adicionar runbooks de automação e outros recursos](operations-management-suite-solutions-resources-automation.md) tooyour solução de gerenciamento.

