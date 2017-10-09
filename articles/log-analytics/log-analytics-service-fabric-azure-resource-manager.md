---
title: "aplicativos de serviço de malha com o uso de análise de Log de aaaAssess Olá portal do Azure | Microsoft Docs"
description: "Você pode usar a solução de malha do serviço de saudação na análise de Log com o risco de saudação do hello tooassess portal do Azure e a integridade de seus aplicativos do Service Fabric, microsserviços, nós e os clusters."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a>Avaliar microsserviços com hello portal do Azure e os aplicativos do Service Fabric

> [!div class="op_single_selector"]
> * [Gerenciador de Recursos](log-analytics-service-fabric-azure-resource-manager.md)
> * [PowerShell](log-analytics-service-fabric.md)
>
>

![Símbolo do Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

Este artigo descreve como toouse Olá solução Service Fabric na análise de Log toohelp identificar e solucionar problemas em seu cluster do Service Fabric.

Olá solução Service Fabric usa dados de diagnóstico do Azure de suas VMs de malha do serviço, coletando dados de tabelas do Azure WAD. O Log Analytics, em seguida, lê eventos da estrutura do Service Fabric, incluindo **Eventos de Serviço Confiável**, **Eventos de Ator**, **Eventos Operacionais** e **Eventos de ETW Personalizados**. Com o painel de solução hello, são problemas importantes tooview capaz e eventos relevantes em seu ambiente do Service Fabric.

tooget iniciado com a solução hello, você precisa tooconnect seu espaço de trabalho de análise de Log do Service Fabric cluster tooa. Aqui estão os três tooconsider de cenários:

1. Se você não tiver implantado o cluster do Service Fabric, use as etapas de saudação em ***implantar um espaço de trabalho de análise de Log do Cluster do Service Fabric conectado tooa*** toodeploy um novo cluster e configurou tooreport tooLog análise.
2. Se você precisar toocollect contadores de desempenho de seu hosts toouse outras soluções do OMS, como segurança no seu Cluster de malha do serviço, siga as etapas de saudação em ***implantar um espaço de trabalho de análise de Log do Cluster do Service Fabric conectado tooa com extensão de VM instalado.***
3. Se você já implantou o cluster do Service Fabric e deseja tooconnect-tooLog Analytics, siga etapas Olá ***adicionando um tooLog de conta de armazenamento existente análise.***

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a>Implante um espaço de trabalho de análise de Log do Cluster do Service Fabric conectado tooa.
Este modelo Olá a seguir:

1. Implanta um espaço de trabalho de análise de logs do Azure Service Fabric cluster já conectado tooa. Você tem um novo espaço de trabalho Olá opção toocreate durante a implantação de modelo hello, ou nome de entrada hello de um espaço de trabalho de análise de Log já existente.
2. Adiciona o espaço de trabalho do hello armazenamento de diagnóstico conta toohello análise de Log.
3. Permite que a solução de malha do serviço de saudação em seu espaço de trabalho de análise de Log.

[![Implantar tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)

Depois de selecionar Olá acima do botão implantar, Olá abre portal do Azure com parâmetros para você tooedit. Ser toocreate-se de que um novo grupo de recursos, se você inserir um novo nome de espaço de trabalho de análise de Log:

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

Aceite os termos legais hello e clique em **criar** toostart implantação de saudação. Concluída a implantação Olá, você deve ver o novo espaço de trabalho de saudação e o cluster criado e Olá WADServiceFabric * eventos, WADWindowsEventLogs e WADETWEvent tabelas adicionadas:

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a>Implante um espaço de trabalho de análise de Log do Cluster do Service Fabric conectado tooa com extensão de VM instalado.

Este modelo Olá a seguir:

1. Implanta um espaço de trabalho de análise de logs do Azure Service Fabric cluster já conectado tooa. Você pode criar um novo espaço de trabalho ou usar um existente.
2. Adiciona o espaço de trabalho do hello armazenamento de diagnóstico contas toohello análise de Log.
3. Permite que a solução de malha do serviço de Olá no espaço de trabalho de análise de Log de saudação.
4. Instala a extensão do agente MMA Olá em cada escala de máquina virtual definida no cluster do Service Fabric. Com o agente MMA Olá instalado, você está tooview capaz de métricas de desempenho sobre os nós.

[![Implantar tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)

Olá as mesmas etapas acima, os parâmetros de entrada hello necessários a seguir e disparar uma implantação. Novamente, você verá novo espaço de trabalho de saudação, cluster e tabelas do WAD todos criadas:

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a>Exibindo dados de desempenho

tooview dados de desempenho de seus nós:


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- Inicie o espaço de trabalho de análise de Log de saudação de Olá portal do Azure.
  ![Service Fabric](./media/log-analytics-service-fabric/6.png)
- Vá tooSettings no painel esquerdo do hello e selecionar dados >> contadores de desempenho do Windows >> "hello adicionar selecionado contadores de desempenho": ![Service Fabric](./media/log-analytics-service-fabric/7.png)
- Na pesquisa de Log, use Olá toodelve de consultas a seguir para as principais métricas sobre seus nós:

    a. Comparar Olá utilização média da CPU em todos os seus nós toosee uma hora última Olá os nós que estão com problemas e no intervalo de tempo que um nó tinha um pico:

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    b. Exibir gráficos de linhas semelhantes para a memória disponível em cada nó com esta consulta:

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    tooview uma lista de todos os nós, mostrando o valor médio exato de saudação MBytes disponíveis para cada nó, use esta consulta:

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    c. No caso de Olá que você deseja toodrill para baixo em um nó específico examinando a média de hora em hora Olá, mínima, máximo e 75 percentual da CPU, você está toodo capaz de isso, usar essa consulta (substitua o campo de computador):

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

Para obter mais informações sobre as métricas de desempenho na análise de Log em Olá [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).


## <a name="adding-an-existing-storage-account-toolog-analytics"></a>Adicionando um tooLog de conta de armazenamento existente análise

Este modelo simplesmente adiciona seu armazenamento contas tooa novo ou existente a análise de Log espaço de trabalho existente.

[![Implantar tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)

> [!NOTE]
> Selecionar um grupo de recursos, se você estiver trabalhando com um espaço de trabalho de análise de Log já existente, selecione "Usar existente" e pesquisa Olá para grupo de recursos que contém o espaço de trabalho de análise de Log de saudação. Caso contrário, crie um novo.
> ![Service Fabric](./media/log-analytics-service-fabric/8.png)
>
>

Depois que este modelo foi implantado, você será capaz de toosee Olá armazenamento conta conectada tooyour análise de Log espaço de trabalho. Neste exemplo, adicionei um mais armazenamento conta toohello Exchange espaço de trabalho que criei acima.
![Service Fabric](./media/log-analytics-service-fabric/9.png)

## <a name="view-service-fabric-events"></a>Exibir eventos do Service Fabric

Depois de implantações de saudação são concluídas e Olá solução de malha do serviço foi habilitado no seu espaço de trabalho, selecionar Olá **Service Fabric** bloco no painel de controle do hello análise de Log toolaunch portal Olá Service Fabric. Painel de saudação inclui colunas de saudação de Olá a tabela a seguir. Cada coluna lista top 10 eventos Olá correspondendo contagem critérios da coluna para Olá especificado intervalo de tempo. Você pode executar uma pesquisa de log que fornece a lista inteira de saudação clicando **ver todos os** na parte inferior direita do hello de cada coluna, ou clicando o cabeçalho da coluna hello.

| **Evento do Service Fabric** | **description** |
| --- | --- |
| Problemas importantes |Uma exibição de problemas como RunAsyncFailures RunAsynCancellations e nós com falha. |
| Eventos operacionais |Eventos operacionais importantes, como atualização de aplicativos e implantações. |
| Eventos de serviço confiável |Eventos importantes de serviços confiáveis como Runasyncinvocations. |
| Eventos de ator |Eventos de ator importantes gerados pelos seus microsserviços, como exceções lançadas por um método de ator, ativações e desativações de ator e assim por diante. |
| Eventos de aplicativo |Todos os eventos de ETW personalizados gerados por seus aplicativos. |

![Painel do Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Painel do Service Fabric](./media/log-analytics-service-fabric/sf4.png)

Olá tabela a seguir mostra os métodos de coleta de dados e outros detalhes sobre como os dados são coletados para a malha do serviço.

| plataforma | Agente direto | Agente do Operations Manager | Armazenamento do Azure | Operations Manager necessário? | Dados de agente do Operations Manager enviados por meio do grupo de gerenciamento | frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |  |  | &#8226; |  |  |10 minutos |

> [!NOTE]
> Você pode alterar o escopo de saudação desses eventos no hello solução Service Fabric clicando **dados com base nos últimos 7 dias** na parte superior de saudação do painel de saudação. Você também pode mostrar gerados no hello últimos sete dias, um dia ou seis horas. Ou, você pode selecionar **personalizado** toospecify um intervalo de datas personalizado.
>
>

## <a name="next-steps"></a>Próximas etapas

* Use [pesquisas de Log na análise de Log](log-analytics-log-searches.md) tooview obter dados de evento do Service Fabric.
