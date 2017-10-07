---
title: "aaaMonitor banco de dados do Azure Cosmos solicitações e armazenamento | Microsoft Docs"
description: "Saiba como toomonitor seu banco de dados do Azure Cosmos a conta para métricas de desempenho, como erros de servidor e as solicitações e métricas de uso, como o consumo de armazenamento."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 4c6a2e6f-6e78-48e3-8dc6-f4498b235a9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: mimig
ms.openlocfilehash: aea029d10717236a573a080dab9d06d87f97f318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-cosmos-db-requests-usage-and-storage"></a>Monitorar solicitações, o uso e o armazenamento do Azure Cosmos DB
Você pode monitorar suas contas do banco de dados do Azure Cosmos no hello [portal do Azure](https://portal.azure.com/). Para cada conta do Azure Cosmos DB, tanto as métricas de desempenho, como solicitações e erros de servidor, quanto as métricas de uso, como consumo de armazenamento, estão disponíveis.

As métricas podem ser examinadas na folha de conta hello, nova folha de métricas hello, ou no Monitor do Azure.

## <a name="view-performance-metrics-on-hello-metrics-blade"></a>Métricas de desempenho do modo de exibição na folha de métricas de saudação
1. Em Olá [portal do Azure](https://portal.azure.com/), clique em **mais serviços**, role muito**bancos de dados**, clique em **o banco de dados do Azure Cosmos**e clique em nome de saudação do hello Conta de banco de dados do Cosmos do Azure para o qual você gostaria que tooview métricas de desempenho.
2. No menu de recurso hello, em **monitoramento**, clique em **métricas**.

folha de métricas de saudação abre e você pode selecionar Olá coleção tooreview. Você pode revisar as métricas de disponibilidade, solicitações, taxa de transferência e armazenamento e compará-los SLAs de banco de dados de Cosmos toohello do Azure.

## <a name="view-performance-metrics-by-using-azure-monitoring"></a>Exibir métricas de desempenho usando o Azure Monitor
1. Em Olá [portal do Azure](https://portal.azure.com/), clique em **Monitor** em Olá Jumpbar.
2. No menu de recursos de saudação, clique em **métricas**.
3. Em Olá **Monitor - métricas** janela no hello **esource grupo** menu suspenso, o grupo de recursos de saudação selecione associado à conta do banco de dados do Azure Cosmos Olá que deseja toomonitor. 
4. Em Olá **recurso** menu suspenso, selecione Olá toomonitor de conta de banco de dados.
5. Na lista de saudação do **métricas disponíveis**, selecione Olá toodisplay de métricas. Use Olá CTRL toomulti botão Selecionar. 

    Suas métricas são exibidas na Olá **plotar** janela. 

## <a name="view-performance-metrics-on-hello-account-blade"></a>Métricas de desempenho do modo de exibição na folha de conta Olá
1. Em Olá [portal do Azure](https://portal.azure.com/), clique em **mais serviços**, role muito**bancos de dados**, clique em **o banco de dados do Azure Cosmos**e clique em nome de saudação do hello Conta de banco de dados do Cosmos do Azure para o qual você gostaria que tooview métricas de desempenho.
2. Olá **monitoramento** Lente exibe Olá blocos a seguir por padrão:
   
   * Total de solicitações para Olá dia atual.
   * Armazenamento usado.
   
   Se sua tabela exibe **nenhum dado disponível** e você acredita que tem dados no banco de dados, consulte Olá [solução de problemas](#troubleshooting) seção.
   
   ![Captura de tela de Lente de monitoramento de saudação que mostra solicitações Olá Olá uso e armazenamento](./media/monitor-accounts/documentdb-total-requests-and-usage.png)
3. Clicando em Olá **solicitações** ou **cota de uso** bloco abre um detalhadas **métrica** folha.
4. Olá **métrica** folha mostra detalhes sobre as métricas de saudação que você selecionou.  Olá parte superior da folha de saudação está um gráfico de solicitações no gráfico a cada hora e abaixo que é a tabela que mostra os valores de agregação para solicitações limitadas e total.  Olá folha de métricas também mostra Olá lista de alertas que foram toohello definido, filtrada métricas que aparecem na folha de métricas atual hello (dessa forma, se você tiver um número de alertas, você só verá Olá aqueles relevantes apresentadas aqui).   
   
   ![Captura de tela da folha de métricas de saudação que inclui limitadas solicitações](./media/monitor-accounts/documentdb-metric-blade.png)

## <a name="customize-performance-metric-views-in-hello-portal"></a>Personalizar os modos de exibição de métrica de desempenho no portal de saudação
1. métricas de saudação toocustomize exibidos em um gráfico específico, clique em Olá gráfico tooopen no hello **métrica** folha e depois clique em **Editar gráfico**.  
   ![Captura de tela de controles de folha de métricas de hello, com editar gráfico realçado](./media/monitor-accounts/madocdb3.png)
2. Em Olá **Editar gráfico** folha, há métricas de saudação do toomodify opções exibem no gráfico de hello, bem como o intervalo de tempo.  
   ![Captura de tela da folha de editar gráfico Olá](./media/monitor-accounts/madocdb4.png)
3. métricas de saudação toochange exibidas na parte Olá, basta selecionar ou limpar métricas de desempenho disponíveis hello e, em seguida, clique em **Okey** na parte inferior da saudação da folha de saudação.  
4. Olá toochange intervalo de tempo, escolha um intervalo diferente (por exemplo, **personalizado**) e, em seguida, clique em **Okey** na parte inferior da saudação da folha de saudação.  
   
   ![Captura de tela da parte de intervalo de tempo de saudação do mostrando de folha de editar gráfico hello como tooenter um intervalo de tempo personalizado](./media/monitor-accounts/madocdb5.png)

## <a name="create-side-by-side-charts-in-hello-portal"></a>Criar gráficos lado a lado no portal de saudação
Olá Portal do Azure permite que você os gráficos métrica toocreate lado a lado.  

1. Primeiro, clique no gráfico de saudação você deseja toocopy e selecione **personalizar**.
   
   ![Captura de tela de gráfico do Total de solicitações de saudação com a opção de personalizar Olá realçada](./media/monitor-accounts/madocdb6.png)
2. Clique em **Clone** Olá parte do menu toocopy hello e, em seguida, clique em **feito personalizando**.
   
   ![Tela de captura do gráfico do Total de solicitações de saudação com hello Clone e feito Personalizando opções realçadas](./media/monitor-accounts/madocdb7.png)  

Agora você pode tratar essa parte como qualquer outra parte métrica, personalizando o intervalo de métricas e a hora de saudação exibido na parte de saudação.  Ao fazer isso, você pode ver dois diferentes métricas gráfico-lado a lado no hello simultaneamente.  
    ![Captura de tela de gráfico do Total de solicitações de saudação e Olá novas solicitações de Total após a hora de gráfico](./media/monitor-accounts/madocdb8.png)  

## <a name="set-up-alerts-in-hello-portal"></a>Configurar alertas no portal de saudação
1. Em Olá [portal do Azure](https://portal.azure.com/), clique em **mais serviços**, clique em **o banco de dados do Azure Cosmos**e então clique Olá nome da conta de banco de dados do Azure Cosmos Olá para o qual você gostaria que toosetup alertas de métrica de desempenho.
2. No menu de recursos de saudação, clique em **regras de alerta** tooopen folha de regras de alerta de saudação.  
   ![Captura de tela de saudação alerta regras parte selecionada](./media/monitor-accounts/madocdb10.5.png)
3. Em Olá **regras de alerta** folha, clique em **adicionar alerta**.  
   ![Captura de tela da folha de regras de alerta hello, com o botão Adicionar alerta Olá realçado](./media/monitor-accounts/madocdb11.png)
4. Em Olá **adicionar uma regra de alerta** folha, especifique:
   
   * nome de saudação da regra de alerta Olá que você está configurando.
   * Uma descrição da nova regra de alerta de saudação.
   * Olá métrica para a regra de alerta de saudação.
   * condição de Hello, limite e o período que determinam quando o alerta Olá ativa. Por exemplo, um erro de servidor contagem maior que 5 sobre Olá últimos 15 minutos.
   * Olá se o administrador de serviço e coadministrators são enviados por email quando Olá alerta será acionado.
   * Endereços de email adicionais para notificações de alerta.  
     ![Captura de tela de saudação Adicionar folha de uma regra de alerta](./media/monitor-accounts/madocdb12.png)

## <a name="monitor-azure-cosmos-db-programatically"></a>Monitorar o Azure Cosmos DB de forma programática
Olá métricas de nível de conta disponíveis no portal de hello, como o uso do armazenamento de conta e total de solicitações, não estão disponíveis por meio de saudação APIs do DocumentDB. No entanto, você pode recuperar dados de uso no nível de coleção hello usando Olá APIs do DocumentDB. dados de nível de coleção tooretrieve, Olá a seguir:

* Olá toouse API REST, [executar GET em coleção Olá](https://msdn.microsoft.com/library/mt489073.aspx). informações de cota e uso de saudação de coleção Olá são retornadas nos cabeçalhos de x-ms-resource-quota e x-ms-resource-usage Olá em resposta hello.
* Olá toouse SDK .NET, use Olá [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) método, que retorna um [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx) que contém um número de propriedades de uso como  **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage**e muito mais.

tooaccess de métricas adicionais, use Olá [SDK do Azure Monitor](https://www.nuget.org/packages/Microsoft.Azure.Insights). As definições de métricas disponíveis podem ser recuperadas chamando:

    https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metricDefinitions?api-version=2015-04-08

Consultas tooretrieve métricas individuais use Olá formato a seguir:

    https://management.azure.com/subscriptions/{SubecriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metrics?api-version=2015-04-08&$filter=%28name.value%20eq%20%27Total%20Requests%27%29%20and%20timeGrain%20eq%20duration%27PT5M%27%20and%20startTime%20eq%202016-06-03T03%3A26%3A00.0000000Z%20and%20endTime%20eq%202016-06-10T03%3A26%3A00.0000000Z

Para obter mais informações, consulte [recuperar métricas de recursos por meio de saudação API REST do Azure Monitor](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/). Observe que "Azure Inights" foi renomeado para "Azure Monitor".  Essa entrada de blog refere-se o nome anterior toohello.

## <a name="troubleshooting"></a>Solucionar problemas
Se o monitoramento blocos exibição Olá **nenhum dado disponível** mensagem e você recentemente feitas solicitações ou adicionado dados toohello banco de dados, você pode editar o uso do bloco tooreflect Olá recente hello.

### <a name="edit-a-tile-toorefresh-current-data"></a>Editar um toorefresh de bloco de dados atual
1. métricas de saudação toocustomize que exibem uma parte específica, clique em saudação do hello gráfico tooopen **métrica** folha e depois clique em **Editar gráfico**.  
   ![Captura de tela de controles de folha de métricas de hello, com editar gráfico realçado](./media/monitor-accounts/madocdb3.png)
2. Em Olá **Editar gráfico** folha em Olá **intervalo de tempo** seção, clique em **última hora**e, em seguida, clique em **Okey**.  
   ![Captura de tela da folha de editar gráfico Olá com a última hora selecionada](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)
3. Seu bloco agora deve ser atualizado para mostrar seus dados atuais e o uso.  
   ![Captura de tela de saudação atualizada Total de solicitações após o bloco de hora](./media/monitor-accounts/documentdb-no-available-data-fixed.png)

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre o planejamento de capacidade do banco de dados do Azure Cosmos, consulte Olá [Calculadora de Planejador de capacidade do banco de dados do Azure Cosmos](https://www.documentdb.com/capacityplanner).

