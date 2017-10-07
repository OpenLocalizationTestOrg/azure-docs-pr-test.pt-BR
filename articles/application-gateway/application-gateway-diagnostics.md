---
title: "aaaMonitor acessar logs, logs de desempenho, integridade de back-end e métricas para o Application Gateway | Microsoft Docs"
description: Saiba como tooenable e gerenciar os logs de acesso e logs de desempenho para o Application Gateway
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a>Integridade do back-end, logs de diagnóstico e métricas do Gateway de Aplicativo

Usando o Gateway de aplicativo do Azure, você pode monitorar os recursos em Olá maneiras a seguir:

* [Integridade de back-end](#back-end-health): Application Gateway fornece integridade de saudação de toomonitor Olá recurso de servidores Olá Olá pools de back-end por meio de saudação portal do Azure e do PowerShell. Você também pode encontrar integridade Olá dos pools de back-end Olá por meio de logs de diagnóstico de desempenho de saudação.

* [Logs](#diagnostic-logs): permitem Logs de desempenho, acesso, e outros dados toobe salvo ou consumidos a partir de um recurso para fins de monitoramento.

* [Métricas](#metrics): atualmente, o Gateway de Aplicativo tem uma métrica. Essa métrica mede a taxa de transferência de saudação do gateway de aplicativo hello em bytes por segundo.

## <a name="back-end-health"></a>Integridade do back-end

Application Gateway fornece integridade de saudação do hello recurso toomonitor de membros individuais de pools de back-end Olá através do portal hello, PowerShell e Olá interface de linha de comando (CLI). Você também pode encontrar uma integridade agregada resumo dos pools de back-end por meio de logs de diagnóstico de desempenho de saudação. 

relatório de integridade de back-end de saudação reflete a saída de hello de instâncias de saudação toohello de investigação de integridade back-end Application Gateway. Quando probing for bem-sucedida e Olá volta final pode receber tráfego, ele será considerado íntegro. Caso contrário, ele é considerado não íntegro.

> [!IMPORTANT]
> Se houver um grupo de segurança de rede (NSG) em uma sub-rede de Gateway do aplicativo, abra a intervalos de porta 65503 65534 na sub-rede de Gateway do aplicativo hello para tráfego de entrada. Essas portas são necessárias para Olá toowork de API de integridade de back-end.


### <a name="view-back-end-health-through-hello-portal"></a>Exibir a integridade de back-end por meio do portal Olá

No portal de hello, integridade de back-end é fornecida automaticamente. Em um gateway de aplicativo existente, selecione **Monitoramento** > **Integridade do back-end**. 

Cada membro no pool de back-end hello está listado nesta página (se ele é uma NIC, IP ou FQDN). São mostrados o nome do pool de back-end, a porta, as configurações de HTTP do back-end e o status de integridade. Os valores válidos para o status de integridade são **Íntegro**, **Não íntegro** e **Desconhecido**.

> [!NOTE]
> Se você ver um status de integridade de back-end do **desconhecido**, certifique-se de que esse acesso toohello back-end não está bloqueado por uma regra NSG, uma rota definida pelo usuário (UDR) ou um personalizadas de DNS na rede virtual hello.

![Integridade do back-end][10]

### <a name="view-back-end-health-through-powershell"></a>Exibir a integridade do back-end por meio do PowerShell

Olá, código do PowerShell a seguir mostra como a integridade de back-end tooview usando Olá `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a>Exibir a integridade do back-end por meio da CLI 2.0 do Azure

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a>Resultados

saudação de trecho de código a seguir mostra um exemplo de resposta de saudação:

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <a name="diagnostic-logging"></a>Logs de diagnóstico

Você pode usar diferentes tipos de logs no Azure toomanage e solucionar problemas com gateways de aplicativo. Você pode acessar alguns desses logs por meio do portal hello. Todos os logs podem ser extraídos de um Armazenamento de blobs do Azure e exibidos em diferentes ferramentas, como [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel e Power BI. Você pode aprender mais sobre Olá diferentes tipos de logs de saudação lista a seguir:

* **Log de atividades**: você pode usar [logs de atividades do Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anteriormente conhecida como logs de auditoria e logs operacionais) tooview todas as operações que são enviadas tooyour assinatura do Azure e seu status. As entradas de log de atividades são coletadas por padrão, e você pode exibi-los no portal do Azure de saudação.
* **Log de acesso**: você pode usar padrões de acesso a este log tooview Application Gateway e analisar informações importantes, incluindo chamador Olá IP, URL solicitada, latência de resposta, o código de retorno e bytes de entrada e saída. Um log de acesso é coletado a cada 300 segundos. Esse log contém um registro por instância do Gateway de Aplicativo. instância do Application Gateway Olá pode ser identificada pela propriedade de instanceId hello.
* **Log de desempenho**: você pode usar este tooview de log como instâncias de Gateway de aplicativos são executados. Esse log captura informações de desempenho de cada instância, incluindo o total de solicitações atendidas, a vazão de dados em bytes, o total de solicitações atendidas, a contagem de solicitações com falha e a contagem de instâncias de back-end íntegras ou não íntegras. Um log de desempenho é coletado a cada 60 segundos.
* **Log de firewall**: você pode usar este solicitações Olá tooview de log que são registrados por meio do modo de detecção ou prevenção de um gateway de aplicativo que é configurado com o firewall do aplicativo web hello.

> [!NOTE]
> Logs estão disponíveis apenas para os recursos implantados no modelo de implantação do Azure Resource Manager hello. Você não pode usar os logs para recursos no modelo de implantação clássico hello. Para melhor compreensão de modelos de saudação dois, consulte Olá [Noções básicas sobre o Gerenciador de recursos de implantação e implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md) artigo.

Você tem três opções para armazenar os logs:

* **Conta de armazenamento**: as contas de armazenamento são mais adequadas para os logs quando eles são armazenados por mais tempo e examinados quando necessário.
* **Hubs de eventos**: hubs de eventos são uma ótima opção para a integração com outras informações de segurança e tooget alertas sobre os recursos das ferramentas de gerenciamento de eventos (SEIM).
* **Log Analytics**: o Log Analytics é mais adequado para o monitoramento geral em tempo real do aplicativo ou para a observação de tendências.

### <a name="enable-logging-through-powershell"></a>Habilitar o log por meio do PowerShell

O log de atividade é habilitado automaticamente para todos os recursos do Resource Manager. Você deve habilitar o acesso e toostart de log de desempenho coleta dados de saudação disponíveis por meio desses logs. tooenable log Olá use as etapas a seguir:

1. Observe a ID do recurso da sua conta de armazenamento, onde são armazenados dados de log hello. Esse valor é de formulário Olá: /subscriptions/\<subscriptionId\>/resourceGroups/\<nome do grupo de recursos\>/providers/Microsoft.Storage/storageAccounts/\<denomedecontadearmazenamento\>. Use qualquer conta de armazenamento em sua assinatura. Você pode usar essas informações para Olá toofind portal do Azure.

    ![Portal: ID do recurso da conta de armazenamento](./media/application-gateway-diagnostics/diagnostics1.png)

2. Anote a ID do Recurso do gateway de aplicativo para o qual o log está habilitado. Esse valor é de formulário Olá: /subscriptions/\<subscriptionId\>/resourceGroups/\<nome do grupo de recursos\>/providers/Microsoft.Network/applicationGateways/\<gateway de aplicativo nome\>. Você pode usar essas informações para toofind portal hello.

    ![Portal: ID do recurso do gateway de aplicativo](./media/application-gateway-diagnostics/diagnostics2.png)

3. Habilite o log de diagnóstico usando Olá cmdlet do PowerShell a seguir:

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
>Os logs de atividades não exigem uma conta de armazenamento separada. uso de saudação do armazenamento para o log de desempenho e acesso incorre em encargos de serviço.

### <a name="enable-logging-through-hello-azure-portal"></a>Habilitar registro em log por meio de saudação portal do Azure

1. Olá portal do Azure, encontrar seu recurso e clique em **logs de diagnóstico**.

   Para o Gateway de Aplicativo, três logs estão disponíveis:

   * Log de acesso
   * Log de desempenho
   * Log de firewall

2. toostart a coleta de dados, clique em **Ativar diagnóstico**.

   ![Ativando o diagnóstico][1]

3. Olá **as configurações de diagnóstico** folha fornece configurações Olá Olá logs de diagnóstico. Neste exemplo, a análise de Log armazena Olá logs. Clique em **configurar** em **análise de Log** tooconfigure seu espaço de trabalho. Você também pode usar hubs de eventos e um armazenamento conta toosave Olá logs de diagnóstico.

   ![Iniciar o processo de configuração Olá][2]

4. Escolha um espaço de trabalho do OMS (Operations Management Suite) existente ou crie um novo. Este exemplo usa um existente.

   ![Opções de espaços de trabalho do OMS][3]

5. Confirme as configurações de saudação e clique em **salvar**.

   ![Folha Configurações de diagnóstico com seleções][4]

### <a name="activity-log"></a>Log de atividades

Por padrão, o Azure gera o log de atividades hello. Olá logs são preservados por 90 dias no armazenamento de logs de eventos do Azure hello. Saiba mais sobre esses logs lendo Olá [exibir eventos e log de atividades](../monitoring-and-diagnostics/insights-debugging-with-events.md) artigo.

### <a name="access-log"></a>Log de acesso

log de acesso de saudação é gerado apenas se você tiver habilitado em cada instância de Gateway do aplicativo, conforme detalhado nas etapas anteriores de saudação. Olá dados são armazenados na conta de armazenamento Olá especificado quando você habilitou o log de saudação. Cada acesso do Application Gateway é registrado no formato JSON, conforme mostrado no exemplo a seguir de saudação:


|Valor  |Descrição  |
|---------|---------|
|instanceId     | Application Gateway instância solicitação Olá atendidas.        |
|clientIP     | IP de origem para a solicitação de saudação.        |
|clientPort     | Porta de origem para solicitação de saudação.       |
|httpMethod     | Método HTTP usado por solicitação hello.       |
|requestUri     | URI da solicitação recebida hello.        |
|RequestQuery     | **Roteada por servidor**: instância de pool de Back-end que recebeu a solicitação de saudação. </br> **X-AzureApplicationGateway-LOG-ID**: ID de correlação usado para solicitação de saudação. Ele pode ser usado tootroubleshoot tráfego problemas em servidores de back-end de saudação. </br>**STATUS do servidor**: código de resposta HTTP recebido do Application Gateway de back-end hello.       |
|UserAgent     | Agente do usuário do cabeçalho de solicitação HTTP de saudação.        |
|httpStatus     | Código de status HTTP retornado toohello cliente do Application Gateway.       |
|httpVersion     | Versão HTTP da solicitação de saudação.        |
|receivedBytes     | Tamanho do pacote recebido, em bytes.        |
|sentBytes| Tamanho do pacote enviado, em bytes.|
|timeTaken| Período de tempo (em milissegundos) necessário para que um toobe de solicitação processadas e seu toobe resposta enviada. Isso é calculado como o intervalo de saudação do tempo de saudação quando o Application Gateway recebe o primeiro byte de um tempo de toohello de solicitação HTTP quando resposta Olá envia a conclusão da operação Olá. É importante toonote que Olá campo Time-Taken geralmente inclui o tempo de saudação que viajam pela rede Olá pacotes de solicitação e resposta de saudação. |
|sslEnabled| Se os pools de back-end de toohello de comunicação usado SSL. Os valores válidos são ativado e desativado.|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a>Log de desempenho

log de desempenho de saudação é gerado apenas se você habilitou em cada instância de Gateway do aplicativo, conforme detalhado nas etapas anteriores de saudação. Olá dados são armazenados na conta de armazenamento Olá especificado quando você habilitou o log de saudação. dados de log de desempenho de saudação são gerados em intervalos de 1 minuto. Olá seguintes dados é registrado:


|Valor  |Descrição  |
|---------|---------|
|instanceId     |  Instância do Gateway de Aplicativo para a qual os dados de desempenho estão sendo gerados. Para um gateway de aplicativo de várias instâncias, há uma linha por instância.        |
|healthyHostCount     | Número de hosts íntegros no pool de back-end de saudação.        |
|unHealthyHostCount     | Número de hosts não íntegro no pool de back-end de saudação.        |
|requestCount     | Número de solicitações atendidas.        |
|latency | Latência (em milissegundos) de solicitações de saudação instância toohello back-end que atende a solicitações de saudação. |
|failedRequestCount| Número de solicitações com falha.|
|throughput| Taxa de transferência média desde o último log hello, medido em bytes por segundo.|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> Latência é calculada de tempo de saudação quando o primeiro byte de solicitação HTTP de Olá Olá é recebida toohello tempo quando o último byte de resposta HTTP de Olá Olá é enviado. Sua saudação soma de Olá Application Gateway tempo de processamento mais hello toohello de custo de rede volta terminar, mais tempo Olá Olá back-end leva tooprocess Olá solicitação.

### <a name="firewall-log"></a>Log de firewall

log de firewall de saudação é gerado apenas se você habilitou para cada gateway do aplicativo, conforme detalhado nas etapas anteriores de saudação. Esse log também requer que firewall saudação do aplicativo web está configurado em um gateway de aplicativo. Olá dados são armazenados na conta de armazenamento Olá especificado quando você habilitou o log de saudação. Olá seguintes dados é registrado:


|Valor  |Descrição  |
|---------|---------|
|instanceId     | Instância do Gateway de Aplicativo para a qual os dados de firewall estão sendo gerados. Para um gateway de aplicativo de várias instâncias, há uma linha por instância.         |
|clientIp     |   IP de origem para a solicitação de saudação.      |
|clientPort     |  Porta de origem para solicitação de saudação.       |
|requestUri     | URL de solicitação recebida hello.       |
|ruleSetType     | Tipo de conjunto de regras. valor disponível da saudação é OWASP.        |
|ruleSetVersion     | Versão utilizada do conjunto de regras. Os valores disponíveis são 2.2.9 e 3.0.     |
|ruleId     | ID da regra de saudação acionar o evento.        |
|Message     | Mensagem amigável para Olá acionar o evento. Mais detalhes são fornecidos na seção de detalhes de saudação.        |
|ação     |  Ação executada na solicitação de saudação. Os valores disponíveis são Bloqueada e Permitida.      |
|site     | Site para o qual Olá log foi gerado. No momento, somente Global é listado porque as regras são globais.|
|detalhes     | Detalhes da saudação acionar o evento.        |
|details.message     | Descrição da regra de saudação.        |
|details.data     | Dados específicos encontrados na solicitação regra Olá correspondentes.         |
|details.file     | Arquivo de configuração que continha a regra de saudação.        |
|details.line     | Número de linha no arquivo de configuração de saudação que disparou o evento de saudação.       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a>Exibir e analisar o log de atividades de saudação

Você pode exibir e analisar dados de log de atividade usando qualquer um dos métodos a seguir de saudação:

* **Ferramentas do Azure**: recuperar informações do log de atividades de saudação por meio do PowerShell do Azure, Olá CLI do Azure, Olá API REST do Azure, ou Olá portal do Azure. Instruções passo a passo para cada método são detalhadas no hello [operações de atividade com o Gerenciador de recursos](../azure-resource-manager/resource-group-audit.md) artigo.
* **Power BI**: se ainda não tiver uma conta do [Power BI](https://powerbi.microsoft.com/pricing), experimente uma gratuitamente. Usando Olá [conteúdo de Logs de atividades do Azure pack para o Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), você pode analisar seus dados com painéis pré-configurados que você pode usar como está ou personalizar.

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a>Exibir e analisar Olá acesso, desempenho e logs de firewall

Azure [análise de Log](../log-analytics/log-analytics-azure-networking-analytics.md) pode coletar arquivos de log de eventos e contadores Olá de sua conta de armazenamento de Blob. Ele inclui visualizações e tooanalyze de recursos avançados de pesquisa seus logs.

Também pode conectar-se a conta de armazenamento tooyour e recuperar entradas de log Olá JSON para logs de acesso e o desempenho. Depois de baixar os arquivos JSON hello, você pode convertê-los tooCSV e exibi-los no Excel, Power BI ou qualquer outra ferramenta de visualização de dados.

> [!TIP]
> Se você estiver familiarizado com os conceitos básicos de alterar valores de constantes e variáveis em c# e o Visual Studio, você pode usar o hello [ferramentas de conversor de log](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponíveis no GitHub.
> 
> 

## <a name="metrics"></a>Métricas

Métricas são um recurso para certos recursos do Azure, onde você pode exibir os contadores de desempenho no portal de saudação. Para o Gateway de Aplicativo, uma única métrica está disponível no momento. Essa métrica é a taxa de transferência, e você pode vê-lo no portal de saudação. Procurar tooan gateway de aplicativo e clique em **métricas**. valores de saudação tooview, selecione taxa de transferência em Olá **métricas disponíveis** seção. Olá a imagem a seguir, você verá um exemplo com filtros de saudação que você pode usar dados de saudação toodisplay em intervalos de tempo diferentes.

![Exibição da métrica com filtros][5]

toosee uma lista atual de métricas, consulte [suporte para métricas com o Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

### <a name="alert-rules"></a>Regras de alerta

Você pode iniciar as regras de alerta com base nas métricas de um recurso. Por exemplo, um alerta pode chamar um webhook ou um administrador de email se for de taxa de transferência de saudação do gateway de aplicativo hello acima, abaixo ou em um limite por um período especificado.

saudação de exemplo a seguir orienta você na criação de uma regra de alerta que envia um administrador de tooan email depois de violações de taxa de transferência um limite:

1. Clique em **adicionar alerta métrica** tooopen Olá **Adicionar regra** folha. Você também pode acessar esta folha da folha de métricas de saudação.

   ![Botão “Adicionar alerta de métrica”][6]

2. Em Olá **Adicionar regra** folha, preencha o nome hello, condição e notificar seções e clique em **Okey**.

   * Em Olá **condição** seletor, selecione um dos valores de saudação quatro: **maior**, **maior que ou igual**, **menor**, ou  **Menor ou igual a**.

   * Em Olá **período** seletor, selecione um período de 5 minutos too6 horas.

   * Se você selecionar **proprietários, Contribuidores e leitores de Email**, email Olá pode ser dinâmica com base em usuários de saudação que têm acesso toothat recursos. Caso contrário, você pode fornecer uma lista separada por vírgulas de usuários em Olá **email(s) administrador adicional** caixa.

   ![Folha Adicionar regra][7]

Se Olá limite for ultrapassado, chega um email que é semelhante toohello um no Olá a imagem a seguir:

![Email para o limite violado][8]

Uma lista de alertas é exibida após a criação de um alerta de métrica. Ele fornece uma visão geral de todas as regras de alerta de saudação.

![Lista de alertas e regras][9]

toolearn mais informações sobre notificações de alerta, consulte [receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

toounderstand mais sobre webhooks e como usá-los com alertas, visite [configurar um webhook em um alerta de métrica do Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="next-steps"></a>Próximas etapas

* Visualize o contador e os logs de eventos com o [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).
* Postagem no blog [Visualize your Azure Activity Log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) (Visualizar o log de atividades do Azure com o Power BI).
* Postagem no blog [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Exibir e analisar os Logs de Atividades do Azure no Power BI e muito mais).

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
