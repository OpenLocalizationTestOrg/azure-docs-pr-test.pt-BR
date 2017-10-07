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
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a>Usar o dimensionamento automático ações toosend email e webhook notificações de alerta no Monitor do Azure
Este artigo mostra como configurar gatilhos para que você possa chamar URLs da web específicas ou enviar emails com base em ações de escala automática no Azure.  

## <a name="webhooks"></a>Webhooks
Webhooks permitem que você tenha sistemas de tooother de notificações de alerta do Azure tooroute Olá para notificações de pós-processamento ou personalizados. Por exemplo, o roteamento tooservices alerta Olá que pode lidar com uma entrada da web solicitação toosend SMS, bugs de log, notificar uma equipe usando bate-papo ou serviços de mensagens, etc. Olá webhook URI deve ser um ponto de extremidade HTTP ou HTTPS válido.

## <a name="email"></a>Email
É possível enviar emails tooany endereço de email válido. Os administradores e coadministradores de assinatura de saudação onde regra hello está sendo executado também serão notificados.

## <a name="cloud-services-and-web-apps"></a>Serviços de nuvem e aplicativos Web
Você pode aceitar de saudação portal do Azure para serviços de nuvem e Farms de servidores (aplicativos da Web).

* Escolha Olá **o dimensionamento por** métrica.

![escalar por](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a>Conjuntos de escala de Máquina Virtual
Para ver as Máquinas Virtuais mais novas criadas com o Gerenciador de Recursos (conjuntos de escala da Máquina Virtual), você pode configurar isso usando a API REST, modelos do Gerenciador de Recursos, PowerShell e CLI. Uma interface de portal ainda não está disponível.
Ao usar o hello API REST ou o modelo do Gerenciador de recursos, inclua o elemento de notificações de saudação com hello as opções a seguir.

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
| Campo | Obrigatório? | Descrição |
| --- | --- | --- |
| operation |sim |o valor deve ser "Scale" |
| sendToSubscriptionAdministrator |sim |o valor deve ser "true" ou "false" |
| sendToSubscriptionCoAdministrators |sim |o valor deve ser "true" ou "false" |
| customEmails |sim |o valor pode ser null [] ou uma matriz da cadeia de caracteres de emails |
| Webhooks |sim |o valor pode ser um Uri válido ou nulo |
| serviceUri |sim |um Uri de https válido |
| propriedades |sim |o valor deve ser vazio {} ou pode conter pares de chave-valor |

## <a name="authentication-in-webhooks"></a>Autenticação em webhooks
Olá webhook pode autenticar usando autenticação baseada em token, onde salvar o webhook Olá URI com uma token de ID como um parâmetro de consulta. Por exemplo, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue

## <a name="autoscale-notification-webhook-payload-schema"></a>Escala automática do esquema de carga útil do webhook de notificação
Quando a notificação de dimensionamento automático Olá é gerada, hello metadados a seguir estão incluídos na carga de webhook hello:

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


| Campo | Obrigatório? | Descrição |
| --- | --- | --- |
| status |sim |status de saudação que indica que uma ação de dimensionamento automático foi gerada |
| operation |sim |Para um aumento de instâncias, será "Escalar Horizontalmente" e para uma diminuição de instâncias, será "Reduzir Horizontalmente" |
| context |sim |contexto de ação de dimensionamento automático Olá |
| timestamp |sim |Carimbo de hora quando a ação de dimensionamento automático Olá foi disparada |
| ID |Sim |ID do Gerenciador de recursos de configuração de dimensionamento automático Olá |
| name |Sim |nome de saudação da configuração de AutoEscala Olá |
| detalhes |Sim |Explicação da ação de saudação que levou o serviço de AutoEscala hello e Olá alterar na contagem de instâncias de saudação |
| subscriptionId |Sim |ID de assinatura do recurso de destino de hello está sendo dimensionado |
| resourceGroupName |Sim |Nome do grupo de recursos do recurso de destino de hello está sendo dimensionado |
| resourceName |Sim |Nome do recurso de destino de hello está sendo dimensionado |
| resourceType |Sim |Olá três valores com suporte: "microsoft.classiccompute/domainnames/slots/roles" - funções de serviço de nuvem, "microsoft.compute/virtualmachinescalesets" - conjuntos de escala de máquina Virtual e "Web/serverfarms" - aplicativo Web |
| resourceId |Sim |ID do Gerenciador de recursos do recurso de destino de saudação que está sendo dimensionado |
| portalLink |Sim |Página de resumo do link do portal do Azure toohello do recurso de destino Olá |
| oldCapacity |Sim |Olá atual (antigo) contagem de instâncias quando o dimensionamento automático levou a uma ação de escala |
| newCapacity |Sim |Contagem de instâncias novo Olá que AutoEscala dimensionado recurso Olá muito|
| Propriedades |Não |Opcional. Conjunto de pares de <Chave, Valor> (por exemplo, Dicionário <Cadeia de caracteres, Cadeia de caracteres>). Olá propriedades campo é opcional. Em uma interface de usuário personalizada ou fluxo de trabalho de aplicativo com base em lógica, você pode inserir chaves e valores que podem ser passados usando a carga de saudação. Um modo alternativo de propriedades personalizadas toopass fazer a chamada de webhook saída toohello é toouse Olá webhook URI em si (como parâmetros de consulta) |
