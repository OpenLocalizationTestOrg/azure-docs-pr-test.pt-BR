---
title: aaaCollect e analisar os contadores de desempenho no Azure Log Analytics | Microsoft Docs
description: "Contadores de desempenho são coletados pelo desempenho tooanalyze de análise de Log em agentes do Windows e Linux.  Este artigo descreve como tooconfigure coleta de desempenho e contadores de para agentes do Windows e Linux, detalhes do que eles são armazenados no repositório do OMS hello, como tooanalyze-los no portal do OMS hello."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 20e145e4-2ace-4cd9-b252-71fb4f94099e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte
ms.openlocfilehash: 30146fecf8db1d8851b89fdb970f757bbb24abf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-and-linux-performance-data-sources-in-log-analytics"></a>Fontes de dados de desempenho do Windows e Linux no Log Analytics
Contadores de desempenho do Windows e Linux fornecem informações sobre o desempenho de saudação de componentes de hardware, sistemas operacionais e aplicativos.  Análise de log pode coletar os contadores de desempenho em intervalos frequentes para análise de quase em tempo Real (NRT) em dados de desempenho de tooaggregating de adição para relatório e análise de prazo mais longo.

![Contadores de desempenho](media/log-analytics-data-sources-performance-counters/overview.png)

## <a name="configuring-performance-counters"></a>Configurando os contadores de desempenho
Configurar contadores de desempenho no portal do OMS de saudação do hello [menu dados nas configurações de análise de Log](log-analytics-data-sources.md#configuring-data-sources).

Quando você configurar o Windows pela primeira vez ou contadores de desempenho do Linux para um novo espaço de trabalho OMS, você terá Olá opção tooquickly criar vários contadores comuns.  Eles são listados com um tooeach próximo da caixa de seleção.  Certifique-se de que qualquer contador que você deseja tooinitially cria são verificadas e, em seguida, clique em **adicionar Olá selecionado contadores de desempenho**.

Para os contadores de desempenho do Windows, você pode escolher uma instância específica para cada contador de desempenho. Para contadores de desempenho do Linux, instância de saudação de cada contador que você escolher se aplicará a tooall contadores de filho do contador pai de saudação. Olá tabela a seguir mostra Olá instâncias comuns disponíveis tooboth contadores de desempenho do Linux e Windows.

| Nome da instância | Descrição |
| --- | --- |
| \_Total |Total de todas as instâncias de saudação |
| \* |Todas as instâncias |
| (/&#124;/var) |Corresponde às instâncias chamadas: / ou /var |

### <a name="windows-performance-counters"></a>Contadores de desempenho do Windows

![Configurar contadores de desempenho do Windows](media/log-analytics-data-sources-performance-counters/configure-windows.png)

Siga este procedimento tooadd um novo toocollect de contador de desempenho do Windows.

1. Nome do tipo saudação do contador de saudação na caixa de texto de saudação em formato de saudação *\counter objeto (instância)*.  Quando você começar a digitar, verá uma lista de correspondência dos contadores comuns.  Você pode selecionar um contador de saudação lista ou digite uma de sua preferência.  Você também pode retornar todas as instâncias de um determinado contador especificando *objeto\contador*.  

    Durante a coleta de contadores de desempenho do SQL Server de instâncias nomeadas, todos os nomeadas começam de contadores de instância com *MSSQL$* e seguido pelo nome da saudação da instância de saudação.  Por exemplo, Olá toocollect taxa de acertos do Cache de Log de contador para todos os bancos de dados do objeto de desempenho de banco de dados de saudação para SQL nomeada instância INST2, especificar `MSSQL$INST2:Databases(*)\Log Cache Hit Ratio`.

2. Clique em  **+**  ou pressione **Enter** lista de toohello tooadd Olá contadores.
3. Quando você adiciona um contador, ele usa o padrão de saudação de 10 segundos para seus **intervalo de amostragem**.  Se desejar que os requisitos de armazenamento tooreduce Olá Olá coletado de dados de desempenho, você pode alterar esse valor mais alto de tooa de backup too1800 segundos (30 minutos).
4. Quando você terminar de adicionar contadores, clique em Olá **salvar** botão na parte superior de saudação da configuração de Olá Olá tela toosave.

### <a name="linux-performance-counters"></a>Contadores de desempenho do Linux

![Configurar contadores de desempenho do Linux](media/log-analytics-data-sources-performance-counters/configure-linux.png)

Siga este procedimento tooadd um novo toocollect de contador de desempenho do Linux.

1. Por padrão, todas as alterações de configuração são enviadas automaticamente tooall agentes.  Para agentes do Linux, um arquivo de configuração é enviado toohello Fluentd de Coletores de dados.  Se você quiser toomodify esse arquivo manualmente em cada agente do Linux, em seguida, desmarque a caixa de saudação *aplicar abaixo máquinas de Linux toomy configuração* e siga as orientações de saudação abaixo.
2. Nome do tipo saudação do contador de saudação na caixa de texto de saudação em formato de saudação *\counter objeto (instância)*.  Quando você começar a digitar, verá uma lista de correspondência dos contadores comuns.  Você pode selecionar um contador de saudação lista ou digite uma de sua preferência.  
3. Clique em  **+**  ou pressione **Enter** lista de toohello de outros contadores do objeto de saudação do contador tooadd hello.
4. Todos os contadores de uso de um objeto Olá mesmo **intervalo de amostragem**.  padrão de saudação é de 10 segundos.  Você alterar esse valor mais alto de tooa de backup too1800 segundos (30 minutos) se desejar que os requisitos de armazenamento tooreduce Olá Olá coletado de dados de desempenho.
5. Quando você terminar de adicionar contadores, clique em Olá **salvar** botão na parte superior de saudação da configuração de Olá Olá tela toosave.

#### <a name="configure-linux-performance-counters-in-configuration-file"></a>Configurar contadores de desempenho do Linux no arquivo de configuração
Em vez de configurar contadores de desempenho do Linux usando o portal do OMS hello, você tem opção de saudação de edição de arquivos de configuração no agente do Linux hello.  Toocollect de métricas de desempenho são controlados pela configuração de saudação em **/etc/opt/microsoft/omsagent/\<id do espaço de trabalho\>/conf/omsagent.conf**.

Cada objeto ou categoria, de toocollect de métricas de desempenho deve ser definido no arquivo de configuração de saudação como um único `<source>` elemento. sintaxe de saudação segue o padrão de saudação abaixo.

    <source>
      type oms_omi  
      object_name "Processor"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>


Olá parâmetros nesse elemento são descritos Olá a tabela a seguir.

| parâmetros | Descrição |
|:--|:--|
| object\_name | Nome do objeto de coleção de saudação. |
| instance\_regex |  Um *expressão regular* definindo toocollect quais instâncias. Olá valor: `.*` especifica todas as instâncias. métricas de processador toocollect para apenas Olá \_instância Total, você poderia especificar `_Total`. as métricas do processo toocollect para hello apenas instâncias crond ou sshd, você pode especificar: ' (crond\|sshd)`. |
| counter\_name\_regex | Um *expressão regular* definindo toocollect quais contadores (para o objeto de saudação). Especifique de todos os contadores do objeto hello, toocollect: `.*`. toocollect trocas somente contadores de espaço para o objeto de memória hello, por exemplo, você pode especificar:`.+Swap.+` |
| intervalo | Frequência na qual Olá contadores do objeto são coletados. |


Hello seguinte tabela lista Olá objetos e contadores que você pode especificar no arquivo de configuração de saudação.  Há contadores adicionais disponíveis para certos aplicativos, conforme descrito em [Coletar contadores de desempenho para aplicativos Linux no Log Analytics](log-analytics-data-sources-linux-applications.md).

| Nome do Objeto | Nome do contador |
|:--|:--|
| Disco Lógico | % de Inodes livres |
| Disco Lógico | % de Espaço Livre |
| Disco Lógico | % de Inodes Usados |
| Disco Lógico | % de Espaço Usado |
| Disco Lógico | Bytes Lidos no Disco/s  |
| Disco Lógico | Leituras de Disco/s  |
| Disco Lógico | Transferências de Disco/s |
| Disco Lógico | Bytes Gravados no Disco/s |
| Disco Lógico | Gravações de Disco/s |
| Disco Lógico | Megabytes Livres |
| Disco Lógico | Bytes de Disco Lógico/s |
| Memória | % de Memória Disponível |
| Memória | % de Espaço de Permuta Disponível |
| Memória | % de Memória Usada |
| Memória | % de Espaço de Permuta Usado |
| Memória | MBytes de Memória Disponíveis |
| Memória | MBytes de Espaço de Permuta Disponíveis |
| Memória | Leituras de Página/s |
| Memória | Gravações de Página/s |
| Memória | Páginas/s |
| Memória | MBytes de Espaço de Permuta Usado |
| Memória | MBytes de Memória Usada |
| Rede | Total de Bytes Transmitidos |
| Rede | Total de Bytes Recebidos |
| Rede | Total de Bytes |
| Rede | Total de Pacotes Transmitidos |
| Rede | Total de Pacotes Recebidos |
| Rede | Total de Erros de Rx |
| Rede | Total de Erros de Tx |
| Rede | Total de Colisões |
| Disco Físico | Média de segundos/Leitura do Disco |
| Disco Físico | Média de segundos/Transferência do Disco |
| Disco Físico | Média de segundos/Gravação do Disco |
| Disco Físico | Bytes/s do Disco Físico |
| Processo | % de Tempo Privilegiado |
| Processo | % de Tempo do Usuário |
| Processo | KBytes de Memória Usada |
| Processo | Memória Virtual Compartilhada |
| Processador | % de Tempo de DPC |
| Processador | % de Tempo Ocioso |
| Processador | % de Tempo de Interrupção |
| Processador | % de Tempo de Espera de E/S |
| Processador | % de Tempo Adequado |
| Processador | % de Tempo Privilegiado |
| Processador | % Tempo do Processador |
| Processador | % de Tempo do Usuário |
| Sistema | Memória Física Livre |
| Sistema | Espaço Livre em Arquivos de Paginação |
| Sistema | Memória Virtual Livre |
| Sistema | Processos |
| Sistema | Tamanho Armazenado em Arquivos de Paginação |
| Sistema | Tempo de atividade |
| Sistema | Usuários |


A seguir está a configuração padrão de saudação para métricas de desempenho.

    <source>
      type oms_omi
      object_name "Physical Disk"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Logical Disk"
      instance_regex ".*
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Processor"
      instance_regex ".*
      counter_name_regex ".*"
      interval 30s
    </source>

    <source>
      type oms_omi
      object_name "Memory"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>

## <a name="data-collection"></a>Coleta de dados
O Log Analytics coleta todos os contadores de desempenho especificados no seu intervalo de amostragem especificado em todos os agentes que têm o contador instalado.  Olá dados não estão agregados e dados brutos hello estão disponíveis em todos os modos de exibição de pesquisa de log por duração Olá especificada por sua assinatura do OMS.

## <a name="performance-record-properties"></a>Propriedades do registro de desempenho
Registros de desempenho têm um tipo de **Perf** e têm propriedades de saudação em Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| Computador |Computador que Olá evento foi coletado do. |
| CounterName |Nome do contador de desempenho de saudação |
| CounterPath |Caminho completo do contador de saudação na forma de saudação \\ \\ \<computador >\\objeto (instância)\\contador. |
| CounterValue |Valor numérico do contador de saudação. |
| InstanceName |Nome da instância do evento hello.  Vazio se não houver nenhuma instância. |
| ObjectName |Nome do objeto de desempenho de saudação |
| SourceSystem |Tipo de dados de saudação do agente foi coletado do. <br><br>OpsManager - agente do Windows, conexão direta ou SCOM <br> Linux: todos os agentes do Linux  <br> AzureStorage: Diagnóstico do Azure |
| TimeGenerated |Data e hora data Olá foi feita a amostragem. |

## <a name="sizing-estimates"></a>Estimativas de dimensionamento
 Uma estimativa aproximada de coleção de um determinado contador em intervalos de 10 segundos é cerca de 1 MB por dia por instância.  Você pode estimar os requisitos de armazenamento de saudação de um contador específico com hello seguinte fórmula.

    1 MB x (number of counters) x (number of agents) x (number of instances)

## <a name="log-searches-with-performance-records"></a>Pesquisas de log com registros de desempenho
Olá, tabela a seguir fornece exemplos de diferentes de pesquisas de log que recuperam registros de desempenho.

| Consultar | Descrição |
|:--- |:--- |
| Type=Perf |Todos os dados de desempenho |
| Type=Perf Computer="MyComputer" |Todos os dados de desempenho de um computador específico |
| Type=Perf CounterName="Current Disk Queue Length" |Todos os dados de desempenho de um contador específico |
| Type=Perf (ObjectName=Processor) CounterName="% Processor Time" InstanceName=_Total &#124; measure Avg(Average) as AVGCPU by Computer |Utilização média da CPU em todos os computadores |
| Type=Perf (CounterName="% Processor Time") &#124; measure max(Max) by Computer |Utilização máxima da CPU em todos os computadores |
| Type=Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" &#124; measure Avg(Average) by InstanceName |Comprimento médio da fila de disco atual em todas as instâncias de saudação de um determinado computador |
| Type=Perf CounterName="DiskTransfers/sec" &#124; measure percentile95(Average) by Computer |95º percentil de transferências de disco/s em todos os computadores |
| Type=Perf CounterName="% Processor Time" InstanceName="_Total"  &#124; measure avg(CounterValue) by Computer Interval 1HOUR |Por hora média de utilização da CPU em todos os computadores |
| Type=Perf Computer="MyComputer" CounterName=%* InstanceName=_Total &#124; measure percentile70(CounterValue) by CounterName Interval 1HOUR |Percentil de 70 por hora de cada contador de porcentagem % para um computador específico |
| Type=Perf CounterName="% Processor Time" InstanceName="_Total"  (Computer="MyComputer") &#124; measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR |Por hora média, mínima, máximo e percentil de 75 da CPU para um computador específico |
| Type=Perf ObjectName="MSSQL$INST2:Databases" InstanceName=master | Todos os dados de desempenho do desempenho de banco de dados de saudação do objeto para o banco de dados mestre Olá da saudação nomeada da instância do SQL Server INST2.  

>[!NOTE]
> Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), e em seguida, Olá acima consultas alteraria toohello a seguir.

> | Consultar | Descrição |
|:--- |:--- |
| Perf |Todos os dados de desempenho |
| Perf &#124; where Computer == "MyComputer" |Todos os dados de desempenho de um computador específico |
| Perf &#124; where CounterName == "Current Disk Queue Length" |Todos os dados de desempenho de um contador específico |
| Perf &#124; where ObjectName == "Processor" and CounterName == "% Processor Time" and InstanceName == "_Total" &#124; summarize AVGCPU = avg(Average) by Computer |Utilização média da CPU em todos os computadores |
| Perf &#124; where CounterName == "% Processor Time" &#124; summarize AggregatedValue = max(Max) by Computer |Utilização máxima da CPU em todos os computadores |
| Perf &#124; where ObjectName == "LogicalDisk" and CounterName == "Current Disk Queue Length" and Computer == "MyComputerName" &#124; summarize AggregatedValue = avg(Average) by InstanceName |Comprimento médio da fila de disco atual em todas as instâncias de saudação de um determinado computador |
| Perf &#124; where CounterName == "DiskTransfers/sec" &#124; summarize AggregatedValue = percentile(Average, 95) by Computer |95º percentil de transferências de disco/s em todos os computadores |
| Perf &#124; where CounterName == "% Processor Time" and InstanceName == "_Total" &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), Computer |Por hora média de utilização da CPU em todos os computadores |
| Perf &#124; where Computer == "MyComputer" and CounterName startswith_cs "%" and InstanceName == "_Total" &#124; summarize AggregatedValue = percentile(CounterValue, 70) by bin(TimeGenerated, 1h), CounterName | Percentil de 70 por hora de cada contador de porcentagem % para um computador específico |
| Perf &#124; where CounterName == "% Processor Time" and InstanceName == "_Total" and Computer == "MyComputer" &#124; summarize ["min(CounterValue)"] = min(CounterValue), ["avg(CounterValue)"] = avg(CounterValue), ["percentile75(CounterValue)"] = percentile(CounterValue, 75), ["max(CounterValue)"] = max(CounterValue) by bin(TimeGenerated, 1h), Computer |Por hora média, mínima, máximo e percentil de 75 da CPU para um computador específico |
| Perf &#124; where ObjectName == "MSSQL$INST2:Databases" and InstanceName == "master" | Todos os dados de desempenho do desempenho de banco de dados de saudação do objeto para o banco de dados mestre Olá da saudação nomeada da instância do SQL Server INST2.  

## <a name="viewing-performance-data"></a>Exibindo dados de desempenho
Quando você executa uma pesquisa de log de dados de desempenho, Olá **lista** exibição é exibida por padrão.  tooview Olá dados em formato de gráfico, clique em **métricas**.  Para uma exibição gráfica detalhada, clique em Olá  **+**  próximo tooa contador.  

![Exibição de métricas recolhida](media/log-analytics-data-sources-performance-counters/metricscollapsed.png)

dados de desempenho de tooaggregate em uma pesquisa de log, consulte [agregação de métrica sob demanda e visualização do OMS](http://blogs.technet.microsoft.com/msoms/2016/02/26/on-demand-metric-aggregation-and-visualization-in-oms/).


## <a name="next-steps"></a>Próximas etapas
* [Colete contadores de desempenho de aplicativos Linux](log-analytics-data-sources-linux-applications.md), incluindo Apache HTTP Server e MySQL.
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) dados de saudação tooanalyze coletados de fontes de dados e soluções.  
* Exportar os dados coletados muito[Power BI](log-analytics-powerbi.md) para análise e visualizações adicionais.
