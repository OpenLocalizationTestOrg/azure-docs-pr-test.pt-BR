---
title: "Monitorar operações, eventos e contadores para o Balanceador de Carga | Microsoft Docs"
description: "Saiba como habilitar o registro em log de eventos de alerta e do status da integridade de investigação para o Balanceador de Carga do Azure"
services: load-balancer
documentationcenter: na
author: KumudD
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/25/2017
ms.author: kumud
ms.openlocfilehash: 36b9379f88ce024c1dcbf9977a873d95076d10df
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a>Análise de log para Balanceador de Carga do Azure

[!INCLUDE [load-balancer-basic-sku-include.md](../../includes/load-balancer-basic-sku-include.md)]

Você pode usar diferentes tipos de log no Azure para gerenciar e solucionar problemas de balanceadores de carga. Alguns desses logs podem ser acessados por meio do portal. Todos os logs podem ser extraídos de um armazenamento de blobs do Azure e exibidos em diferentes ferramentas, como o Excel e o PowerBI. Você pode saber mais sobre os diferentes tipos de logs na lista abaixo.

* **Logs de auditoria:** é possível usar os [Logs de Auditoria do Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anteriormente conhecidos como Logs Operacionais) para exibir todas as operações que estão sendo enviadas à(s) sua(s) assinatura(s) do Azure, bem como seu status. Os logs de auditoria são habilitados por padrão e podem ser exibidos no portal do Azure.
* **Logs de eventos de alerta:** Você pode usar esse log para ver quais alertas foram gerados para o balanceador de carga. O status do balanceador de carga é coletado a cada cinco minutos. Esse log será gravado somente se um evento de alerta do balanceador de carga for gerado.
* **Logs de investigação de integridade:** Você pode usar esse log para exibir os problemas detectados pelo seu teste de integridade, como o número de instâncias no pool de back-end que não estão recebendo solicitações do balanceador de carga devido a falhas de investigação de integridade. Esse log é gravado quando há uma alteração no status de investigação de integridade.

> [!IMPORTANT]
> Atualmente, a análise de log funciona somente para balanceadores de carga voltados para a Internet. Os logs estão disponíveis apenas para os recursos implantados no modelo de implantação do Gerenciador de Recursos. Você não pode usar logs para recursos do modelo de implantação clássico. Para saber mais sobre esses modelos de implantação, consulte [Understanding Resource Manager deployment and classic deployment (Noções básicas sobre a implantação do Resource Manager e a implantação clássica)](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="enable-logging"></a>Habilitar o registro em log

O log de auditoria é habilitado automaticamente para todos os recursos do Gerenciador de Recursos. Você precisa habilitar o registro em log da investigação de integridade e de eventos para começar a coletar os dados disponíveis por meio desses logs. Use as etapas a seguir para habilitar o registro em log.

Entre no [portal do Azure](http://portal.azure.com). Se você ainda não tiver um balanceador de carga, [crie um](load-balancer-get-started-internet-arm-ps.md) antes de continuar.

1. No portal, clique em **Procurar**.
2. Selecione **Balanceadores de carga**.

    ![portal - balanceador de carga](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. Selecione um balanceador de carga existente >> **Todas as Configurações**.
4. No lado direito da caixa de diálogo com o nome do balanceador de carga, role até **Monitoramento**, clique em **Diagnóstico**.

    ![portal - configurações do balanceador de carga](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. No painel **Diagnóstico**, em **Status**, selecione **Ativar**.
6. Clique em **Conta de Armazenamento**.
7. Em **LOGS**, selecione uma conta de armazenamento existente ou crie uma nova. Use o controle deslizante para determinar por quantos dias os dados do evento serão mantidos nos logs de eventos. 
8. Clique em **Salvar**.

    ![Portal – Logs de diagnóstico](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> Os logs de auditoria não exigem uma conta de armazenamento separada. O uso do armazenamento para registro em log de eventos e da investigação de integridade incorrerá em cobranças de serviço.

## <a name="audit-log"></a>Log de auditoria

O log de auditoria é gerado por padrão. Os logs são preservados por 90 dias no repositório de Logs de Eventos do Azure. Saiba mais sobre esses logs lendo o artigo [Exibir logs de eventos e de auditoria](../monitoring-and-diagnostics/insights-debugging-with-events.md) .

## <a name="alert-event-log"></a>Log de eventos de alerta

Esse log só será gerado se você o tiver habilitado para cada balanceador de carga. Os dados são registrados no formato JSON e armazenados na conta de armazenamento especificada quando você habilitou o registro em log. Segue um exemplo de um evento.

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

A saída JSON mostra a propriedade *eventname* , que descreverá o motivo para o balanceador de carga ter criado um alerta. Nesse caso, o alerta gerado foi devido à exaustão da porta TCP causada pelos limites de NAT do IP de origem (SNAT).

## <a name="health-probe-log"></a>Log de investigação de integridade

Esse log só será gerado se você o tiver habilitado para cada balanceador de carga, conforme detalhado acima. Os dados são armazenados na conta de armazenamento especificada quando você habilitou o registro em log. Um contêiner denominado 'insights-logs-loadbalancerprobehealthstatus' é criado e os seguintes dados são registrados:

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

A saída JSON mostra no campo de propriedades as informações básicas do status da integridade da investigação. A propriedade *dipDownCount* mostra o número total de instâncias no back-end que não estão recebendo tráfego de rede devido à falha nas respostas de investigação.

## <a name="view-and-analyze-the-audit-log"></a>Exibir e analisar o log de auditoria

Você pode exibir e analisar dados do log de auditoria usando qualquer um dos seguintes métodos:

* **Ferramentas do azure:** recupere informações dos logs de auditoria por meio do Azure PowerShell, a CLI (Interface de Linha de Comando) do Azure, a API REST do Azure ou o portal de visualização do Azure. Instruções passo a passo para cada método são detalhadas no artigo [Operações de auditoria com o Gerenciador de Recursos](../azure-resource-manager/resource-group-audit.md) .
* **Power BI:** se você ainda não tiver uma conta do [Power BI](https://powerbi.microsoft.com/pricing), será possível experimentar gratuitamente. Usando o [Pacote de conteúdo dos Logs de Auditoria do Azure para Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), é possível analisar seus dados com painéis pré-configurados que ou é possível personalizar as exibições para elas se adequarem aos seus requisitos.

## <a name="view-and-analyze-the-health-probe-and-event-log"></a>Exibir e analisar o log de eventos de investigação de integridade

Você precisa se conectar à sua conta de armazenamento e recuperar as entradas de log JSON para logs de eventos e investigação de integridade. Depois de baixar os arquivos JSON, você pode convertê-los em CSV e exibi-lo no Excel, no PowerBI ou em qualquer outra ferramenta de visualização de dados.

> [!TIP]
> Se estiver familiarizado com o Visual Studio e os conceitos básicos de alteração de valores de constantes e variáveis em C#, você poderá usar as [ferramentas de conversor de log](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponíveis no GitHub.

## <a name="additional-resources"></a>Recursos adicionais

* [Visualizar os logs de auditoria do Azure com o Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) .
* [Exibir e analisar logs de auditoria do Azure no Power BI e muito mais](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) .

## <a name="next-steps"></a>Próximas etapas

[Entender as investigações do balanceador de carga](load-balancer-custom-probe-overview.md)
