---
title: "análise de aaaLog para CDN do Azure | Microsoft Docs"
description: "O cliente pode habilitar a análise de log para a CDN do Azure."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a>Logs de Diagnóstico para a CDN do Azure

Depois de habilitar CDN para o seu aplicativo, você provavelmente deseja uso da CDN toomonitor Olá, verificar a integridade de saudação de sua entrega e solucionar possíveis problemas. A CDN do Azure fornece esses recursos com a [Análise de Núcleo de CDN](cdn-analyze-usage-patterns.md) e os [Logs de Diagnóstico](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)

## <a name="cdn-core-analytics"></a>Análise de Núcleo de CDN
Como um usuário atual do Azure CDN Verizon padrão ou perfil de premium, você já está tooview capaz de análise de núcleo no portal suplementar da saudação acessível por meio da opção de "Gerenciar" hello da saudação portal do Azure. 

## <a name="azure-diagnostic-logs"></a>Logs de Diagnóstico do Azure

Azure Com esse novo recurso, você pode exibir a análise de núcleo e salvá-la em um ou mais destinos, incluindo:

 - Conta de Armazenamento do Azure
 - Hubs de eventos do Azure
 - [Repositório do OMS Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 Este recurso está disponível para todos os pontos de extremidade CDN pertencentes tooVerizon (Standard e Premium) e perfis de CDN do Akamai (padrão).

Logs de diagnóstico permitem tooexport métricas de uso básico de sua variedade de tooa de ponto de extremidade CDN de fontes para que você pode consumi-los de forma personalizada. Por exemplo, você pode fazer Olá seguintes tipos de exportação de dados:

- Exportar armazenamento tooblob de dados, exportar tooCSV e gerar gráficos no excel.
- Exportar hubs tooevent de dados e correlacionar com dados de outros serviços do azure.
- Exportar dados toolog análise e exibir os dados em seu próprio espaço de trabalho do OMS

Hello figura a seguir mostra uma exibição de análise de núcleo de CDN típica em dados.

![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/01_OMS-workspace.png)

*Figura 1 – exibição de Análise de Núcleo de CDN*

Olá seguindo as instruções passo a passo passa pelo esquema de saudação do dados de análise de núcleo hello, etapas envolvidas na habilitação do recurso hello e entregá-los toovarious destinos e consumo desses destinos.

## <a name="enable-logging-with-azure-portal"></a>Habilitar registro em log com o Portal do Azure

> [!NOTE]
> Olá logs de diagnóstico estão ativados **off** por padrão. 

Siga as próximas etapas, Olá tooenable registro em log com a análise de núcleo de CDN:

Entrar toohello [portal do Azure](http://portal.azure.com). Se você ainda não tiver a CDN habilitada para o fluxo de trabalho, [Habilite a CDN do Azure](cdn-create-new-endpoint.md) antes de continuar.

1. No portal de hello, navegue até muito**perfil CDN**.
2. Selecione um perfil CDN e selecione o ponto de extremidade CDN Olá que você deseja tooenable **Logs de diagnóstico**.

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. Vá muito**Logs de diagnóstico** folha sob **monitoramento** seção, em seguida, alterar o status de saudação muito**em**.

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a>Habilitar registro em log com o Armazenamento do Azure
    
logs de saudação toostore do armazenamento do Azure toouse, selecione **tooa conta de armazenamento de arquivos**, selecione os dias de retenção e clique em **CoreAnalytics** em **Log**.

![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

*Figura 2 – Registro em log com o Armazenamento do Azure*

### <a name="logging-with-oms-log-analytics"></a>Registro em log com o OMS Log Analytics

logs de saudação toostore de análise de logs do OMS toouse, siga estas etapas:

1. De saudação **Logs de diagnóstico** folha sob **monitoramento**, selecione **enviar tooLog análise** de 

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. Configure o log de análise de Log Olá clicando em configurar. Isso leva tooa caixa de diálogo onde você pode selecionar um espaço de trabalho anterior ou criar um novo.

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. Clique em **Criar Novo Espaço de Trabalho**.

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/07_Create-new.png)

4. Em seguida, você deve selecionar um novo nome de espaço de trabalho, uma assinatura existente, um grupo de recursos (novo ou existente), um local e um tipo de preço. Você tem a opção de saudação de Fixar este painel de tooyour de configuração. Clique em configuração de saudação toocomplete Okey.

    Em seguida, você verá seu espaço de trabalho com os nomes do grupo de recursos e do Espaço de Trabalho do OMS. Os nomes devem ser exclusivos e podem usar apenas letras, números e hifens. Espaços e sublinhados não são permitidos. 

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. Em seguida receber uma mensagem curta informando que seu espaço de trabalho foi criado e você retornará tooyour tela de configuração de log. Você pode confirmar o nome de saudação do seu espaço de trabalho de análise de Log.

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    Depois de ter definido a configuração de análise de Log hello, certifique-se de que conferir caixa CoreAnalytics Olá log CDN.

6. Se tudo estiver tooyour preferência, clique em Olá **salvar** botão na parte superior de saudação da caixa de diálogo de configuração de saudação.

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/10_Save-me.png)

    Olá **salvar** botão não está mais ativa e que Olá no/fora botão agora é ON, mas azul, em vez de roxo.

7. Se você quiser toosee seu novo espaço de trabalho do OMS, vá tooyour portal do Azure painel, clique em nome de saudação do seu espaço de trabalho de análise de Log. Em seguida, você verá seu espaço de trabalho (certifique-se de que o espaço de trabalho do OMS é realçado Olá esquerda). Clique em Olá Portal do OMS bloco toosee seu espaço de trabalho no repositório do OMS hello. 

    ![portal – Logs de diagnóstico](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    O repositório do OMS agora está pronto toolog dados. Em ordem tooconsume dados, você deve usar um [solução do OMS](#consuming-oms-log-analytics-data), coberto neste artigo.

Para obter mais informações sobre os atrasos em dados de log, consulte [aqui](#log-data-delays).

## <a name="enable-logging-with-powershell"></a>Habilitar o registro em log com o PowerShell

Abaixo está um exemplo de como tooenable e obter Logs de diagnóstico por meio de Olá Cmdlets do PowerShell do Azure.

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a>Habilitando os Logs de Diagnóstico em uma conta de armazenamento

Primeiro, faça logon e selecione uma assinatura:

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


tooEnable Logs de diagnóstico em uma conta de armazenamento, use este comando:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
tooEnable Logs de diagnóstico em um espaço de trabalho do OMS, use este comando:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a>Consumir logs de diagnóstico do Armazenamento do Azure
Esta seção descreve o esquema de saudação da análise de núcleo CDN hello, como eles são organizados dentro de uma conta de armazenamento do Azure e fornece Olá de toodownload do código de exemplo registra no arquivo CSV de tooa.

### <a name="using-microsoft-azure-storage-explorer"></a>Usando o Gerenciador de Armazenamento do Microsoft Azure
Antes de poder acessar dados de análise de núcleo de saudação do hello conta de armazenamento do Azure, primeiro é necessário um conteúdo de saudação tooaccess ferramenta em uma conta de armazenamento. Embora várias ferramentas estão disponíveis no mercado Olá, Olá que recomendamos é Olá Microsoft Azure Storage Explorer. Você pode baixar a ferramenta de saudação do [aqui](http://storageexplorer.com/). Depois de baixar e instalar software hello, configure-toouse Olá a mesma conta de armazenamento do Azure que foi configurado como um destino toohello CDN Logs de diagnóstico.

1.  Abra o **Gerenciador de Armazenamento do Microsoft Azure**
2.  Localize a conta de armazenamento Olá
3.  Vá toohello **"Contêineres de Blob"** nó sob esse armazenamento de conta e expanda o nó Olá
4.  Contêiner Olá selecione denominado **"insights-logs-coreanalytics"** e clique duas vezes
5.  Mostrar os resultados de backup em Olá painel direito começando com hello primeiro nível, que se parece com **"resourceId ="**. Continue clicando em todo o caminho de saudação até que você veja o arquivo hello **PT1H.json**. Consulte Olá Observação para obter explicação do caminho Olá seguinte.
6.  Cada blob **PT1H.json** representa hello logs de análise para uma hora para um ponto de extremidade CDN específico ou seu domínio personalizado.
7.  esquema de saudação do conteúdo Olá deste arquivo JSON é descrita na seção de saudação esquema de saudação Logs de análise de núcleo


> [!NOTE]
> **Formato de caminho de blob**
> 
> Os logs de análise principal são gerados a cada hora. Todos os dados de uma hora são coletados e armazenados em um único Blob do Azure como um conteúdo JSON. Olá caminho toothis BLOBs do Azure aparece como se houver uma estrutura hierárquica. Isso é porque a ferramenta de Gerenciador de armazenamento Olá interpreta '/' como um separador de diretório e mostra a hierarquia de saudação para sua conveniência. Na verdade, o caminho inteiro Olá apenas representa o nome de blob de saudação. Esse nome de blob Olá segue Olá seguindo a convenção de nomenclatura 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

**Descrição dos campos:**

|value|Descrição|
|-------|---------|
|ID da assinatura    |ID da saudação assinatura do Azure. Isso está no formato de Guid de saudação.|
|Recurso |Nome do grupo de recursos CDN Olá recurso grupo toowhich Olá pertence.|
|Nome do Perfil |Nome da saudação perfil CDN|
|Nome do Ponto de Extremidade |Nome do ponto de extremidade CDN da saudação|
|Ano|  representação de 4 dígitos do ano hello, por exemplo, de 2017|
|Mês| representação de 2 dígitos do número do mês hello. 01 = janeiro... 12 = dezembro|
|Dia|   representação de 2 dígitos de dia de saudação do mês de saudação|
|PT1H.json| Armazenamento de dados de análise de saudação real do arquivo JSON|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a>Exportando Olá dados de análise de núcleo tooa arquivo CSV

toomake it tooaccess fácil Olá Core análise, podemos fornecer um código de exemplo para uma ferramenta que permite fazer o download de arquivos JSON de saudação em um formato de arquivo simples separados por vírgulas, que pode ser usado tooeasily criar gráficos ou outras agregações.

Aqui está como você pode usar a ferramenta de saudação:

1.  Visite o link do github Olá: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )
2.  Baixar o código de saudação
3.  Siga as instruções toocompile e configurar
4.  Execute a ferramenta de saudação
5.  Arquivo CSV resultante mostra dados de análise de saudação em uma hierarquia simples simple.

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a>Consumir logs de diagnóstico de um repositório do OMS Log Analytics
Análise de log é um serviço no OMS Operations Management Suite () que monitora o toomaintain de ambientes de nuvem e local sua disponibilidade e desempenho. Ele coleta dados gerados pelos recursos em seus ambientes de nuvem e locais e de outras análises de tooprovide ferramentas monitoramento em várias origens. 

toouse análise de Log, você deve [habilitar registro em log](#enable-logging-with-azure-storage) repositório de análise de Log de OMS do Azure toohello, que é discutido neste artigo.

### <a name="using-hello-oms-repository"></a>Usando Olá repositório do OMS

 Olá diagrama a seguir mostra a arquitetura de saudação de entradas de saudação e saídas do repositório de saudação:

![Repositório do OMS Log Analytics](./media/cdn-diagnostics-log/12_Repo-overview.png)

*Figura 3 – Repositório do Log Analytics*

Você pode exibir dados de saudação em uma variedade de maneiras usando soluções de gerenciamento. Você pode obter as soluções de gerenciamento de saudação [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

Você pode instalar as soluções de gerenciamento do Azure marketplace clicando Olá **obtê-lo agora** link na parte inferior da saudação de cada solução.

### <a name="adding-an-oms-cdn-management-solution"></a>Adicionar uma solução de gerenciamento de CDN do OMS

Siga essas etapas tooadd uma solução de gerenciamento:

1.   Se você ainda não fez isso, entre em toohello portal do Azure usando sua assinatura do Azure e vá tooyour painel.
    ![Painel do Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)

2. Em Olá **novo** folha sob **Marketplace**, selecione **monitoramento + gerenciamento**.

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. Em Olá **monitoramento + gerenciamento** folha, clique em **ver todos os**.

    ![Ver tudo](./media/cdn-diagnostics-log/15_See-all.png)

4.  Pesquisar CDN na caixa de pesquisa de saudação.

    ![Ver tudo](./media/cdn-diagnostics-log/16_Search-for.png)

5.  Selecione **Análise de Núcleo de CDN do Azure**. 

    ![Ver tudo](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  Depois de clicar em **criar**, você será perguntado toocreate um novo espaço de trabalho do OMS ou use uma existente. 

    ![Ver tudo](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  Selecione o espaço de trabalho de saudação criado antes. Em seguida, você precisa tooadd uma conta de automação.

    ![Ver tudo](./media/cdn-diagnostics-log/19_Add-automation.png)

8. Olá tela a seguir mostra Olá formulário de conta de automação que deve preencher. 

    ![Ver tudo](./media/cdn-diagnostics-log/20_Automation.png)

9. Depois que você criou a conta de automação hello, você está pronto tooadd sua solução. Clique em Olá **criar** botão.

    ![Ver tudo](./media/cdn-diagnostics-log/21_Ready.png)

10. Espaço de trabalho tooyour agora foi adicionada ao sua solução. Volte tooyour painel do portal do Azure.

    ![Ver tudo](./media/cdn-diagnostics-log/22_Dashboard.png)

    Clique em espaço de trabalho de análise de Log Olá você criou o espaço de trabalho do toogo tooyour. 

11. Clique em Olá **Portal do OMS** bloco toosee sua nova solução no portal do OMS hello.

    ![Ver tudo](./media/cdn-diagnostics-log/23_workspace.png)

12. O portal do OMS deve agora ser semelhante Olá tela a seguir:

    ![Ver tudo](./media/cdn-diagnostics-log/24_OMS-solution.png)

    Clique em uma saudação blocos toosee vários modos de exibição em seus dados.

    ![Ver tudo](./media/cdn-diagnostics-log/25_Interior-view.png)

    Você pode rolar para a esquerda ou direita toosee mais blocos que representam a exibições individuais em dados saudação. 

    Clicar em um dos blocos de saudação fornece mais detalhes sobre seus dados.

     ![Ver tudo](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a>Ofertas e tipos de preços

Você pode ver ofertas e camadas de preços para soluções de gerenciamento do OMS e ofertas [aqui](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).

### <a name="customizing-views"></a>Personalizando exibições

Você pode personalizar o modo de exibição de Olá em seus dados usando Olá **Designer de exibição**. Vá tooyour espaço de trabalho do OMS e inicia a criação clicando Olá **View Designer** lado a lado.

![Criador de Modos de Exibição](./media/cdn-diagnostics-log/27_Designer.png)

Você pode arrastar e remova os tipos de gráficos da esquerda hello e preencha Olá detalhes de dados que você deseja tooanalyze em saudação à esquerda.

![Criador de Modos de Exibição](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a>Atrasos em dados de log

Atrasos em dados de log da Verizon | Atrasos em dados de log da Akamai
--- | ---
Dados de log Verizon é 1 hora atrasados e ocupam too2 toostart de horas que aparece após a conclusão da propagação de ponto de extremidade. | Dados de log do Akamai é 24 horas atrasadas e ocupam too2 toostart de horas que aparece se ele foi criado mais de 24 horas atrás. Se tiver sido criado recentemente, pode demorar até too25 horas para Olá logs toostart que aparecem.

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a>Tipos de log de diagnóstico para análise de núcleo de CDN

Atualmente, nós oferecemos somente logs de análise de núcleo, que contêm as métricas mostrando estatísticas de resposta HTTP e estatísticas de saída como visto no hello POPs CDN/bordas.

### <a name="core-analytics-metrics-details"></a>Detalhes das métricas da análise principal
Olá, a tabela a seguir mostra uma lista de métricas disponíveis no hello que logs de análise de núcleo. Nem todas as métricas estão disponíveis de todos os provedores, embora essas diferenças sejam mínimas. Olá, a tabela a seguir também mostra se uma determinada métrica está disponível de um provedor. Observe que as métricas de Olá estão disponíveis para apenas esses pontos de extremidade CDN com tráfego neles.


|Métrica                     | Descrição   | Verizon  | Akamai 
|---------------------------|---------------|---|---|
| RequestCountTotal         |Número total de ocorrências de solicitação durante esse período| Sim  |Sim   |
| RequestCountHttpStatus2xx |Contagem de todas as solicitações que resultaram em um código HTTP 2xx (por exemplo, 200, 202)              | Sim  |Sim   |
| RequestCountHttpStatus3xx | Contagem de todas as solicitações que resultaram em um código HTTP 3xx (por exemplo, 300, 302)              | Sim  |Sim   |
| RequestCountHttpStatus4xx |Contagem de todas as solicitações que resultaram em um código HTTP 4xx (por exemplo, 400, 404)               | Sim   |Sim   |
| RequestCountHttpStatus5xx | Contagem de todas as solicitações que resultaram em um código HTTP 5xx (por exemplo, 500, 504)              | Sim  |Sim   |
| RequestCountHttpStatusOthers |  Contagem de todos os outros códigos HTTP (fora de 2xx a 5xx) | Sim  |Sim   |
| RequestCountHttpStatus200 | Contagem de todas as solicitações que resultaram em um código de resposta HTTP 200              |Não   |Sim   |
| RequestCountHttpStatus206 | Contagem de todas as solicitações que resultaram em um código de resposta HTTP 206              |Não   |Sim   |
| RequestCountHttpStatus302 | Contagem de todas as solicitações que resultaram em um código de resposta HTTP 302              |Não   |Sim   |
| RequestCountHttpStatus304 |  Contagem de todas as solicitações que resultaram em um código de resposta HTTP 304             |Não   |Sim   |
| RequestCountHttpStatus404 | Contagem de todas as solicitações que resultaram em um código de resposta HTTP 404              |Não   |Sim   |
| RequestCountCacheHit |Contagem de todas as solicitações que resultaram em uma Ocorrência no Cache. Isso significa que o ativo de saudação foi servido diretamente Olá POP toohello cliente.               | Sim  |Não   |
| RequestCountCacheMiss | Contagem de todas as solicitações que resultaram em uma Perda do Cache. Isso significa Olá ativo não foi encontrado no cliente de toohello Olá POP mais próximo e, portanto, foi recuperado do hello origem.              |Sim   | Não  |
| RequestCountCacheNoCache | Contagem de todas as solicitações tooan ativo que impediu que está sendo armazenado em cache devido a configuração do usuário tooa na borda de saudação.              |Sim   | Não  |
| RequestCountCacheUncacheable | Contagem de todas as solicitações tooassets impediu que está sendo armazenado em cache pelo controle de Cache do ativo Olá e expira cabeçalhos, que indicam que ele deve não ser armazenado em cache pelo cliente Olá HTTP ou um POP                |Sim   |Não   |
| RequestCountCacheOthers | Contagem de todas as solicitações com o status de cache não cobertas pelos itens acima.              |Sim   | Não  |
| EgressTotal | Transferência de dados de saída em GB              |Sim   |Sim   |
| EgressHttpStatus2xx | Transferência de dados de saída* para respostas com códigos de status HTTP 2xx em GB            |Sim   |Não   |
| EgressHttpStatus3xx | Transferência de dados de saída para respostas com códigos de status HTTP 3xx em GB              |Sim   |Não   |
| EgressHttpStatus4xx | Transferência de dados de saída para respostas com códigos de status HTTP 4xx em GB               |Sim   | Não  |
| EgressHttpStatus5xx | Transferência de dados de saída para respostas com códigos de status HTTP 5xx em GB               |Sim   |  Não |
| EgressHttpStatusOthers | Transferência de dados de saída para respostas com outros códigos de status HTTP em GB                |Sim   |Não   |
| EgressCacheHit |  Saída de transferência de dados para respostas que foram entregues diretamente do cache CDN Olá em Olá POPs de CDN/bordas  |Sim   |  Não |
| EgressCacheMiss | Transferência de dados de saída para respostas que não foram encontradas no hello mais próximo servidor POP e recuperadas do servidor de origem Olá              |Sim   |  Não |
| EgressCacheNoCache | Transferência de dados de saída para ativos que são impedidos de serem armazenados em cache devido a configuração do usuário tooa na borda da saudação.                |Sim   |Não   |
| EgressCacheUncacheable | Transferência de dados de saída de ativos que são impedidos de serem armazenados em cache por Cache-Control do ativo hello e/ou expira, que indicam que ele deve não ser armazenado em cache em um POP ou pelo cliente Olá HTTP                    |Sim   | Não  |
| EgressCacheOthers |  Transferências de dados de saída para outros cenários de cache.             |Sim   | Não  |

* Transferência de dados saída refere-se tootraffic entregue do cliente de toohello servidores POPS de CDN.


### <a name="schema-of-hello-core-analytics-logs"></a>Esquema de saudação Logs de análise de núcleo 

Todos os logs são armazenados no formato JSON e cada entrada tem campos de cadeia de caracteres hello abaixo de esquema a seguir:

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

Onde 'tempo' de saudação representa a hora de início de saudação do limite de hora Olá para o qual as estatísticas de saudação é relatada. Quando uma métrica não tem suporte por um provedor de CDN, em vez de um valor double ou integer, haverá um valor null. Esse valor nulo indica ausência de saudação de uma métrica, e isso é diferente de um valor de 0. Observe também que haja um conjunto de métricas por domínio configurado no ponto de extremidade de saudação.

Propriedades de exemplo abaixo:

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a>Recursos adicionais

* [Logs de Diagnóstico do Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [Análise principal por meio do portal suplementar da CDN do Azure](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [Log Analytics do OMS do Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [API REST do Log Analytics do Azure](https://docs.microsoft.com/en-us/rest/api/loganalytics)







