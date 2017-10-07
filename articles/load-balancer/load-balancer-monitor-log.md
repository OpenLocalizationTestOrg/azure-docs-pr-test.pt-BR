---
title: "aaaMonitor operações, eventos e contadores de Balanceador de carga | Microsoft Docs"
description: Saiba como tooenable eventos de alerta e teste o log de status de integridade para o balanceador de carga do Azure
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a>Análise de log para Balanceador de Carga do Azure

Você pode usar diferentes tipos de logs no Azure toomanage e solucionar problemas de balanceadores de carga. Alguns desses logs podem ser acessado por meio do portal hello. Todos os logs podem ser extraídos de um armazenamento de blobs do Azure e exibidos em diferentes ferramentas, como o Excel e o PowerBI. Você pode aprender mais sobre Olá diferentes tipos de logs de lista de saudação abaixo.

* **Logs de auditoria:** você pode usar [os Logs de auditoria do Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anteriormente conhecido como Logs operacionais) tooview todas as operações que estão sendo enviado tooyour assinaturas do Azure e seu status. Logs de auditoria são habilitados por padrão e podem ser exibidos no portal do Azure de saudação.
* **Logs de eventos de alerta:** você pode usar este rasied de alertas do log tooview pelo Balanceador de carga de saudação. status de Olá Olá balanceador de carga são coletados a cada cinco minutos. Esse log será gravado somente se um evento de alerta do balanceador de carga for gerado.
* **Logs de investigação de integridade:** você pode usar esse problemas de tooview log detectado pelo seu teste de integridade, como o número de saudação de instâncias de seu pool de back-end que não estejam recebendo solicitações do balanceador de carga Olá devido a falhas de investigação de integridade. Esse log é gravado toowhen há uma alteração no status de investigação de integridade de saudação.

> [!IMPORTANT]
> Atualmente, a análise de log funciona somente para balanceadores de carga voltados para a Internet. Logs só estão disponíveis para os recursos implantados no modelo de implantação do Gerenciador de recursos de saudação. Você não pode usar os logs para recursos no modelo de implantação clássico hello. Para obter mais informações sobre modelos de implantação hello, consulte [Noções básicas sobre o Gerenciador de recursos de implantação e implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="enable-logging"></a>Habilitar o registro em log

O log de auditoria é habilitado automaticamente para todos os recursos do Gerenciador de Recursos. Você precisará tooenable eventos e integridade investigação log toostart coletando dados de saudação disponíveis por meio desses logs. Use Olá log de tooenable as etapas a seguir.

Entrar toohello [portal do Azure](http://portal.azure.com). Se você ainda não tiver um balanceador de carga, [crie um](load-balancer-get-started-internet-arm-ps.md) antes de continuar.

1. No portal de saudação, clique em **procurar**.
2. Selecione **Balanceadores de carga**.

    ![portal - balanceador de carga](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. Selecione um balanceador de carga existente >> **Todas as Configurações**.
4. Olá direita da caixa de diálogo de saudação em nome de Olá Olá do balanceador de carga, role muito**monitoramento**, clique em **diagnóstico**.

    ![portal - configurações do balanceador de carga](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. Em Olá **diagnóstico** painel, em **Status**, selecione **em**.
6. Clique em **Conta de Armazenamento**.
7. Em **LOGS**, selecione uma conta de armazenamento existente ou crie uma nova. Use Olá controle deslizante toodetermine quantos dias a partir da data de evento será armazenada nos logs de eventos de saudação. 
8. Clique em **Salvar**.

    ![Portal – Logs de diagnóstico](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> Os logs de auditoria não exigem uma conta de armazenamento separada. Olá uso de armazenamento para integridade e eventos de log de teste incorrerão em encargos de serviço.

## <a name="audit-log"></a>Log de auditoria

log de auditoria de saudação é gerado por padrão. Olá logs são preservados por 90 dias no armazenamento de Logs de eventos do Azure. Saiba mais sobre esses logs lendo Olá [exibir eventos e logs de auditoria](../monitoring-and-diagnostics/insights-debugging-with-events.md) artigo.

## <a name="alert-event-log"></a>Log de eventos de alerta

Esse log só será gerado se você o tiver habilitado para cada balanceador de carga. eventos de saudação são registrados no formato JSON e armazenados na conta de armazenamento Olá especificado quando você habilitou o log de saudação. a seguir Olá é um exemplo de um evento.

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

Olá JSON de saída mostra Olá *eventname* propriedade que descreve a razão Olá Olá balanceador de carga criado um alerta. Nesse caso, o alerta Olá gerado venceu esgotamento de porta de tooTCP causado por origem que limita IP NAT (SNAT).

## <a name="health-probe-log"></a>Log de investigação de integridade

Esse log só será gerado se você o tiver habilitado para cada balanceador de carga, conforme detalhado acima. Olá dados são armazenados na conta de armazenamento Olá especificado quando você habilitou o log de saudação. Um contêiner denominado 'insights-logs-loadbalancerprobehealthstatus' é criado e Olá dados a seguir é registrada:

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

a saída JSON Olá mostra no hello propriedades campo Olá informações básicas sobre status de integridade de investigação de saudação. Olá *dipDownCount* propriedade mostra o número total de saudação de instâncias Olá back-end que não estejam recebendo o tráfego de rede devido a respostas de investigação de toofailed.

## <a name="view-and-analyze-hello-audit-log"></a>Exibir e analisar o log de auditoria de saudação

Você pode exibir e analisar dados de log de auditoria usando qualquer um dos métodos a seguir de saudação:

* **Ferramentas do Azure:** recuperar informações de logs de auditoria Olá por meio do PowerShell do Azure, hello Azure Interface de linha de comando (CLI), Olá API REST do Azure, ou Olá portal de visualização do Azure. Instruções passo a passo para cada método são detalhadas no hello [operações com o Gerenciador de recursos de auditoria](../azure-resource-manager/resource-group-audit.md) artigo.
* **Power BI:** se você ainda não tiver uma conta do [Power BI](https://powerbi.microsoft.com/pricing), será possível experimentar gratuitamente. Usando Olá [conteúdo de Logs de auditoria do Azure pack para o Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), você pode analisar seus dados com painéis pré-configurados, ou você pode personalizar exibições toosuit seus requisitos.

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a>Exibir e analisar a investigação de integridade hello e log de eventos

Você precisa de armazenamento de tooyour tooconnect de conta e recuperar entradas de log Olá JSON para logs de investigação de integridade e eventos. Depois de baixar os arquivos JSON hello, você pode convertê-los tooCSV e view no Excel, Power BI ou qualquer outra ferramenta de visualização de dados.

> [!TIP]
> Se você estiver familiarizado com os conceitos básicos de alterar valores de constantes e variáveis em c# e o Visual Studio, você pode usar o hello [ferramentas de conversor de log](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponíveis no GitHub.

## <a name="additional-resources"></a>Recursos adicionais

* [Visualizar os logs de auditoria do Azure com o Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) .
* [Exibir e analisar logs de auditoria do Azure no Power BI e muito mais](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) .

## <a name="next-steps"></a>Próximas etapas

[Entender as investigações do balanceador de carga](load-balancer-custom-probe-overview.md)
