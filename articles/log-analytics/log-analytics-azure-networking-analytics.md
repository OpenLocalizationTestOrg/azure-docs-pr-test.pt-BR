---
title: "aaaAzure solução de análise de rede na análise de Log | Microsoft Docs"
description: "Você pode usar o hello solução de análise de rede do Azure nos logs de Gateway de aplicativo do Azure e logs de grupo de segurança de rede do Azure de tooreview análise de Log."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a>Soluções de monitoramento de rede do Azure no Log Analytics

Análise de log oferece Olá soluções para monitorar suas redes a seguir:
* Monitor de Desempenho de Rede (NPM) para
 * Olá monitorar a integridade da rede
* Tooreview de análise de Gateway do aplicativo do Azure
 * Logs do Gateway de Aplicativo do Azure
 * Métricas do Gateway de Aplicativo do Azure
* Tooreview de análise do grupo de segurança de rede do Azure
 * Logs do Grupo de Segurança de Rede do Azure

## <a name="network-performance-monitor-npm"></a>Monitor de Desempenho de Rede (NPM)

Olá [Monitor de desempenho de rede](log-analytics-network-performance-monitor.md) solução de gerenciamento é uma solução, que monitora a integridade de saudação, a disponibilidade e a acessibilidade de redes de monitoramento de rede.  É usado toomonitor conectividade entre:

* Nuvem pública e local
* Data centers e locais de usuário (filiais)
* Sub-redes hospedando várias camadas de um aplicativo de várias camadas.

Para obter mais informações, confira [Monitor de Desempenho de Rede](log-analytics-network-performance-monitor.md).

## <a name="azure-application-gateway-and-network-security-group-analytics"></a>Análise do Gateway de Aplicativo e do Grupo de Segurança de Rede do Azure
soluções de saudação toouse:
1. Adicionar tooLog de solução de gerenciamento Olá Analytics, e
2. Habilite o diagnóstico toodirect Olá diagnóstico tooa análise de Log espaço de trabalho. Não é necessário toowrite Olá logs tooAzure o armazenamento de Blob.

Você pode habilitar o diagnóstico e solução de saudação correspondente para um ou ambos os grupos de segurança de rede e Gateway de aplicativo.

Se você não habilitar o log de diagnóstico para um tipo de recurso específico, mas instala solução hello, folhas de painel Olá para esse recurso estão em branco e exibem uma mensagem de erro.

> [!NOTE]
> Em janeiro de 2017, Olá suporte para a forma de envio de logs do tooLog Application Gateways e os grupos de segurança de rede, que análise alterada. Se você vir Olá **análise de rede do Azure (preterido)** solução, consulte muito[migrando de solução de análise de rede antiga Olá](#migrating-from-the-old-networking-analytics-solution) para obter as etapas que você precisa toofollow.
>
>

## <a name="review-azure-networking-data-collection-details"></a>Examinar os detalhes da coleção de dados de rede do Azure
análise de Gateway de aplicativo do Azure Hello e soluções de gerenciamento de análise de grupo de segurança de rede Olá coletam logs de diagnóstico diretamente no Azure Application Gateways e os grupos de segurança de rede. Não é necessário toowrite Olá logs tooAzure armazenamento de Blob e nenhum agente é necessária para a coleta de dados.

Olá tabela a seguir mostra os métodos de coleta de dados e outros detalhes sobre como os dados são coletados para análise de Gateway de aplicativo do Azure e análises de grupo de segurança de rede de saudação.

| Plataforma | Agente direto | Agente do Systems Center Operations Manager | As tabelas | Operations Manager necessário? | Dados de agente do Operations Manager enviados por meio do grupo de gerenciamento | Frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- |
| As tabelas |  |  |&#8226; |  |  |quando conectado |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a>Solução de análise de Gateway de Aplicativo do Azure no Log Analytics

![Símbolo da Análise do Gateway de Aplicativo do Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

Olá logs a seguir têm suporte para Gateways de aplicativo:

* ApplicationGatewayAccessLog
* ApplicationGatewayPerformanceLog
* ApplicationGatewayFirewallLog

Olá métricas a seguir têm suporte para Gateways de aplicativo:

* Taxa de transferência de 5 minutos

### <a name="install-and-configure-hello-solution"></a>Instalar e configurar a solução de saudação
Use Olá tooinstall instruções a seguir e configure a solução de análise do hello Azure Application Gateway:

1. Habilitar a solução de análise de Gateway de aplicativo do Azure de saudação do [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) ou usando o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).
2. Habilite o log de diagnóstico para Olá [Application Gateways](../application-gateway/application-gateway-diagnostics.md) toomonitor desejado.

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a>Habilitar o diagnóstico de Gateway de aplicativo do Azure no portal de saudação

1. No portal do Azure de Olá, navegar toomonitor de recurso do Application Gateway toohello
2. Selecione *logs de diagnóstico* tooopen Olá página a seguir

   ![imagem do recurso do Gateway de Aplicativo do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. Clique em *Ativar diagnóstico* tooopen Olá página a seguir

   ![imagem do recurso do Gateway de Aplicativo do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. tooturn em diagnóstico, clique em *na* em *Status*
5. Clique em Olá caixa de seleção *enviar tooLog análise*
6. Selecione um espaço de trabalho existente do Log Analytics ou crie um espaço de trabalho
7. Clique em caixa de seleção de saudação em **Log** para cada Olá toocollect de tipos de log
8. Clique em *salvar* tooenable log de saudação do diagnóstico tooLog análise

#### <a name="enable-azure-network-diagnostics-using-powershell"></a>Habilitar o diagnóstico de rede do Azure usando PowerShell

saudação de script do PowerShell a seguir fornece um exemplo de como tooenable log de diagnóstico para os gateways de aplicativos.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a>Usar a análise do Gateway de Aplicativo do Azure
![imagem do bloco Análise do Gateway de Aplicativo do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

Depois de clicar em Olá **analytics do Azure Application Gateway** lado a lado em Olá visão geral, você pode exibir resumos dos seus logs e, em seguida, fazer uma busca de toodetails para Olá categorias a seguir:

* Logs de acesso do Gateway de Aplicativo
  * Erros de cliente e servidor nos logs de acesso do Gateway de Aplicativo
  * Solicitações por hora para cada Gateway de Aplicativo
  * Solicitações com falha por hora para cada Gateway de Aplicativo
  * Erros por agente do usuário para Gateways de Aplicativo
* Desempenho do Gateway de Aplicativo
  * Integridade do host para o Gateway de Aplicativo
  * Percentil 95 e máximo para solicitações com falha do Gateway de Aplicativo

![imagem do painel Análise do Gateway de Aplicativo do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![imagem do painel Análise do Gateway de Aplicativo do Azure](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

Em Olá **analytics do Azure Application Gateway** painel, examine as informações de resumo de saudação em uma das folhas de saudação e, em seguida, clique em uma tooview informações detalhadas sobre a página de pesquisa de log de saudação.

Em qualquer uma das páginas de pesquisa de log hello, você pode exibir os resultados por tempo, resultados detalhados e o histórico de pesquisa de log. Você também pode filtrar pelos resultados de saudação toonarrow facetas.


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a>Solução de análise de Grupo de Segurança de Rede do Azure no Log Analytics

![Símbolo da Análise do Grupo de Segurança de Rede do Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

Olá logs a seguir têm suporte para grupos de segurança de rede:

* NetworkSecurityGroupEvent
* NetworkSecurityGroupRuleCounter

### <a name="install-and-configure-hello-solution"></a>Instalar e configurar a solução de saudação
Use Olá tooinstall instruções a seguir e configurar a solução de análise de rede do Azure hello:

1. Habilitar a solução de análise de grupo de segurança de rede do Azure de saudação do [do Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) ou usando o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).
2. Habilite o log de diagnóstico para Olá [grupo de segurança de rede](../virtual-network/virtual-network-nsg-manage-log.md) recursos que você deseja toomonitor.

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a>Habilitar o diagnóstico de grupo de segurança de rede do Azure no portal de saudação

1. No portal do Azure de Olá, navegar toohello toomonitor de recurso de grupo de segurança de rede
2. Selecione *logs de diagnóstico* tooopen Olá página a seguir

   ![imagem do recurso de Grupo de Segurança de Rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. Clique em *Ativar diagnóstico* tooopen Olá página a seguir

   ![imagem do recurso de Grupo de Segurança de Rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. tooturn em diagnóstico, clique em *na* em *Status*
5. Clique em Olá caixa de seleção *enviar tooLog análise*
6. Selecione um espaço de trabalho existente do Log Analytics ou crie um espaço de trabalho
7. Clique em caixa de seleção de saudação em **Log** para cada Olá toocollect de tipos de log
8. Clique em *salvar* tooenable log de saudação do diagnóstico tooLog análise

### <a name="enable-azure-network-diagnostics-using-powershell"></a>Habilitar o diagnóstico de rede do Azure usando PowerShell

saudação de script do PowerShell a seguir fornece um exemplo de como tooenable log de diagnóstico para os grupos de segurança de rede
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a>Usar a análise de Grupo de Segurança de Rede do Azure
Depois de clicar em Olá **análise do grupo de segurança de rede do Azure** lado a lado em Olá visão geral, você pode exibir resumos dos seus logs e, em seguida, fazer uma busca de toodetails para Olá categorias a seguir:

* Fluxos bloqueados no grupo de segurança de rede
  * Regras do grupo de segurança de rede com fluxos bloqueados
  * Endereços MAC com fluxos bloqueados
* Fluxos permitidos no grupo de segurança de rede
  * Regras com fluxos permitidos do grupo de segurança de rede
  * Endereços MAC com fluxos permitidos

![imagem do painel Análise do Grupo de Segurança de Rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![imagem do painel Análise do Grupo de Segurança de Rede do Azure](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

Em Olá **análise do grupo de segurança de rede do Azure** painel, examine as informações de resumo de saudação em uma das folhas de saudação e, em seguida, clique em uma tooview informações detalhadas sobre a página de pesquisa de log de saudação.

Em qualquer uma das páginas de pesquisa de log hello, você pode exibir os resultados por tempo, resultados detalhados e o histórico de pesquisa de log. Você também pode filtrar pelos resultados de saudação toonarrow facetas.

## <a name="migrating-from-hello-old-networking-analytics-solution"></a>Migrando de solução de análise de rede antiga Olá
Em janeiro de 2017, Olá suporte para a forma de envio de logs do Azure Application Gateways e grupos de segurança de rede do Azure tooLog alterada de análise. Essas alterações fornecem Olá vantagens a seguir:
+ Os logs são gravados diretamente tooLog análise sem Olá necessário toouse uma conta de armazenamento
+ Menor latência de tempo de saudação quando os logs são gerados toothem disponíveis na análise de Log
+ Menos etapas de configuração
+ Um formato comum para todos os tipos de diagnóstico do Azure

Olá toouse atualizado soluções:

1. [Configurar o diagnóstico toobe enviado diretamente tooLog análise de Gateways de aplicativo do Azure](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [Configurar o diagnóstico toobe enviado diretamente tooLog análise de grupos de segurança de rede do Azure](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. Habilitar Olá *análises de Gateway do aplicativo do Azure* e hello *análise de grupo de segurança de rede do Azure* solução usando Olá processo descrito em [soluções adicionar análise de Log Olá Galeria de soluções](log-analytics-add-solutions.md)
3. Atualizar todos os painéis, as consultas salvas ou alertas toouse Olá novo tipo de dados
  + O tipo é tooAzureDiagnostics. Você pode usar os logs de sistema de rede do hello ResourceType toofilter tooAzure.

    | Em vez de: | Use: |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + Para qualquer campo que tenha um sufixo de \_s, \_d, ou \_g em nome do hello, alteração Olá primeiro caractere toolower caso
   + Para qualquer campo que tenha um sufixo de \_o nome, dados de saudação é dividido em campos individuais com base nos nomes de campo Olá aninhado.
4. Remover Olá *análise de rede do Azure (preterido)* solução.
  + Se você estiver usando o PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`

Os dados coletados antes de alterar Olá não estiver visível na nova solução de saudação. Você pode continuar tooquery para esse dados usando Olá tipo antigo e nomes de campo.

## <a name="troubleshooting"></a>Solucionar problemas
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Próximas etapas
* Use [pesquisas de Log na análise de Log](log-analytics-log-searches.md) tooview obter dados de diagnóstico do Azure.
