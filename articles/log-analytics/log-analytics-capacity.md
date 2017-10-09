---
title: "aaaCapacity e solução de desempenho na análise de Log do Azure | Microsoft Docs"
description: "Capacidade de saudação de uso e solução de desempenho na análise de Log toohelp entender Olá capacidade dos seus servidores Hyper-V."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 51617a6f-ffdd-4ed2-8b74-1257149ce3d4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: c47bb1e8bb9d4460b0241e89a616f3b356844b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-hyper-v-virtual-machine-capacity-with-hello-capacity-and-performance-solution-preview"></a>Planejar a capacidade de máquina virtual do Hyper-V com hello capacidade e solução de desempenho (visualização)

![Símbolo de capacidade e desempenho](./media/log-analytics-capacity/capacity-solution.png)

Você pode usar o hello capacidade e solução de desempenho na análise de Log toohelp entender Olá capacidade dos seus servidores Hyper-V. solução de saudação fornece ideias sobre seu ambiente do Hyper-V, mostrando Olá utilização geral (CPU, memória e disco) de hosts hello e Olá VMs em execução nesses hosts Hyper-V. Métricas serão coletadas para CPU, memória e discos em todos os hosts e VMs Olá executando neles.

solução de saudação:

-   Mostra os hosts com maior e menor utilização de CPU e memória
-   Mostra as VMs com maior e menor utilização de CPU e memória
-   Mostra as VMs com a maior e menor utilização da taxa de transferência e IOPS
-   Mostra quais VMs são executadas em quais hosts
-   Mostra Olá discos superiores com alta taxa de transferência, IOPS, e volumes compartilhados de latência em cluster
- Permite que você toocustomize e filtrar com base em grupos

> [!NOTE]
> versão anterior Olá Olá capacidade e solução de desempenho chamado gerenciamento de capacidade exigida do System Center Operations Manager e o System Center Virtual Machine Manager. A solução atualizada não tem essas dependências.


## <a name="connected-sources"></a>Fontes conectadas

Olá, a tabela a seguir descreve Olá conectado fontes que são suportadas por essa solução.

| Fonte Conectada | Suporte | Descrição |
|---|---|---|
| [Agentes do Windows](log-analytics-windows-agents.md) | Sim | solução de saudação coleta informações de dados de capacidade e desempenho de agentes do Windows. |
| [Agentes do Linux](log-analytics-linux-agents.md) | Não    | solução Olá não coletará informações de dados de capacidade e desempenho dos agentes do Linux diretos.|
| [Grupo de gerenciamento do SCOM](log-analytics-om-agents.md) | Sim |solução Olá coleta dados de desempenho e capacidade de agentes em um grupo de gerenciamento do SCOM conectado. Uma conexão direta de tooOMS de agente do SCOM Olá não é necessária. Dados são encaminhados do repositório de OMS toohello do grupo de gerenciamento de saudação.|
| [Conta de armazenamento do Azure](log-analytics-azure-storage.md) | Não | O armazenamento do Azure não inclui dados de desempenho, nem de capacidade.|

## <a name="prerequisites"></a>Pré-requisitos

- O Windows ou agentes do Operations Manager devem ser instalados no Windows Server 2012 ou nos hosts superiores do Hyper-V, e não nas máquinas virtuais.


## <a name="configuration"></a>Configuração

Execute Olá etapa tooadd Olá capacidade e desempenho solução tooyour espaço de trabalho a seguir.

- Adicionar Olá capacidade e desempenho solução tooyour OMS espaço de trabalho usando Olá processo descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).

## <a name="management-packs"></a>Pacotes de gerenciamento

Se seu grupo de gerenciamento do SCOM é conectado tooyour espaço de trabalho do OMS, em seguida, Olá pacotes de gerenciamento a seguir será instalado no SCOM quando você adicionar essa solução. Não é necessária nenhuma configuração nem a manutenção desses pacotes de gerenciamento.

- Microsoft.IntelligencePacks.CapacityPerformance

evento de 1201 Olá se parece com:


```
New Management Pack with id:"Microsoft.IntelligencePacks.CapacityPerformance", version:"1.10.3190.0" received.
```

Quando Olá solução capacidade e desempenho é atualizada, o número de versão Olá será alterado.

Para obter mais informações sobre como os pacotes de gerenciamento da solução são atualizados, consulte [tooLog conectar o Operations Manager análise](log-analytics-om-agents.md).

## <a name="using-hello-solution"></a>Usando a solução de saudação

Quando você adiciona Olá capacidade e desempenho solução tooyour espaço de trabalho, hello capacidade e desempenho é adicionado toohello painel de visão geral. Este bloco exibe uma contagem do número de saudação de hosts do Hyper-V ativos no momento e número de saudação de máquinas virtuais ativas que foram monitorados para Olá período de tempo selecionado.

![Bloco de capacidade e desempenho](./media/log-analytics-capacity/capacity-tile.png)


### <a name="review-utilization"></a>Como revisar a utilização

Clique em Olá capacidade e desempenho bloco tooopen Olá capacidade e desempenho do painel. Painel de saudação inclui colunas de saudação de Olá a tabela a seguir. Cada coluna lista os itens tooten correspondência critérios da coluna para Olá especificado escopo e tempo de intervalo. Você pode executar uma pesquisa de log que retorna todos os registros clicando **ver todos os** na parte inferior da coluna de saudação ou clicando o cabeçalho de coluna de saudação do hello.

- **Hosts**
    - **Utilização da CPU de host** mostra uma tendência de gráfica de utilização de CPU de saudação de computadores host e uma lista de hosts, com base em Olá período de tempo selecionado. Passe o mouse sobre detalhes de tooview de gráfico de linha de saudação para um ponto específico no tempo. Clique em Olá gráfico tooview mais detalhes na pesquisa de log. Clique em qualquer pesquisa de log de tooopen de nome de host e exiba detalhes do contador de CPU para VMs hospedadas.
    - **Utilização de memória de host** mostra uma tendência de gráfica de utilização de memória de saudação de computadores host e uma lista de hosts, com base em Olá período de tempo selecionado. Passe o mouse sobre detalhes de tooview de gráfico de linha de saudação para um ponto específico no tempo. Clique em Olá gráfico tooview mais detalhes na pesquisa de log. Clique em qualquer host nome tooopen log pesquisa e exibir memória contador detalhes para VMs hospedadas.
- **Máquinas virtuais**
    - **Utilização de CPU da VM** mostra uma tendência de gráfica de utilização de CPU de saudação de máquinas virtuais e uma lista de máquinas virtuais, com base em Olá período de tempo selecionado. Passe o mouse sobre detalhes de tooview de gráfico de linha de saudação para um ponto específico no tempo de saudação principais 3 máquinas virtuais. Clique em Olá gráfico tooview mais detalhes na pesquisa de log. Clique em qualquer pesquisa de log de tooopen de nome VM e exibir detalhes do contador de CPU agregados para Olá VM.
    - **Utilização de memória da VM** mostra uma tendência de gráfica de utilização de memória de saudação de máquinas virtuais e uma lista de máquinas virtuais, com base em Olá período de tempo selecionado. Passe o mouse sobre detalhes de tooview de gráfico de linha de saudação para um ponto específico no tempo de saudação principais 3 máquinas virtuais. Clique em Olá gráfico tooview mais detalhes na pesquisa de log. Clique em qualquer pesquisa de log de tooopen de nome VM e exibir detalhes do contador memória agregados para Olá VM.
    - **IOPS de disco Total da VM** mostra uma tendência de gráfica de saudação total em disco IOPS para máquinas virtuais e uma lista de máquinas virtuais com hello IOPS para cada um, com base em Olá período de tempo selecionado. Passe o mouse sobre detalhes de tooview de gráfico de linha de saudação para um ponto específico no tempo de saudação principais 3 máquinas virtuais. Clique em Olá gráfico tooview mais detalhes na pesquisa de log. Clique em qualquer pesquisa de log de tooopen de nome VM e a exibição de detalhes de saudação VM do contador de IOPS de disco agregados.
    - **Taxa de transferência de disco Total VM** mostra selecionados de uma tendência de gráfica de taxa de transferência do hello total em disco para máquinas virtuais e uma lista de máquinas virtuais com taxa de transferência do hello total em disco para cada, Olá com base no período de tempo. Passe o mouse sobre detalhes de tooview de gráfico de linha de saudação para um ponto específico no tempo de saudação principais 3 máquinas virtuais. Clique em Olá gráfico tooview mais detalhes na pesquisa de log. Clique em qualquer pesquisa de log de tooopen de nome VM e exibir detalhes do contador de taxa de transferência agregada total em disco para Olá VM.
- **Volumes compartilhados clusterizados**
    - **Total de taxa de transferência** mostra a soma de saudação de ambos leituras e gravações no volume compartilhado de cluster.
    - **Total de IOPS** mostra soma de saudação de operações de entrada/saída por segundo em volumes compartilhados do cluster.
    - **Latência total** mostra a latência total Olá em volumes compartilhados do cluster.
- **Densidade de host** lado a lado superior Olá mostra número total de saudação de solução de toohello disponível de hosts e máquinas virtuais. Clique em detalhes adicionais do hello lado a lado superior tooview na pesquisa de log. Também lista todos os hosts e número de saudação de máquinas virtuais que estão hospedados. Clique em um host toodrill nos resultados da VM Olá em uma pesquisa de log.


![folha de Hosts do painel](./media/log-analytics-capacity/dashboard-hosts.png)

![folha de máquinas virtuais do painel](./media/log-analytics-capacity/dashboard-vms.png)


### <a name="evaluate-performance"></a>Desempenho da avaliação

Ambientes de computação de produção diferem muito das tooanother de uma organização. Além disso, a capacidade e o desempenho para cargas de trabalho podem depender de como as suas VMs estão operando, e o que você considera normal. Procedimentos específicos toohelp medir o desempenho provavelmente não seria aplicada tooyour ambiente. Portanto, mais generalizada orientação prescritiva é melhor toohelp adequado. A Microsoft publica uma variedade de orientação prescritiva artigos toohelp medir o desempenho.

toosummarize, solução de saudação coleta dados de desempenho e capacidade de uma variedade de fontes, incluindo contadores de desempenho. Usar esses dados de desempenho e capacidade apresentadas em vários superfícies de solução hello e comparar toothose seus resultados no hello [medir o desempenho no Hyper-V](https://msdn.microsoft.com/library/cc768535.aspx) artigo. Embora o artigo de saudação foi publicado algum tempo atrás, diretrizes, considerações e métricas de saudação ainda são válidas. artigo Olá contém recursos úteis de tooother links.


## <a name="sample-log-searches"></a>Pesquisas de log de exemplo

Olá a tabela a seguir fornece as pesquisas de log de exemplo para dados de capacidade e desempenho coletados e calculado por esta solução.

| Consultar | Descrição |
|---|---|
| Todas as configurações de memória do host | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="Host Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Todas as configurações de memória da VM | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="VM Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Divisão dos IOPS de disco totais em todas as VMs | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Reads/s" OR CounterName="VHD Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Divisão da taxa de transferência de disco total em todas as VMs | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Read MB/s" OR CounterName="VHD Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Divisão de IOPS total em todos os CSVs | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Reads/s" OR CounterName="CSV Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Divisão da taxa de transferência total em todos os CSVs | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read MB/s" OR CounterName="CSV Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Divisão da latência total em todos os CSVs | <code> Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read Latency" OR CounterName="CSV Write Latency") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |

>[!NOTE]
> Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), e em seguida, Olá acima consultas alteraria toohello a seguir.

> | Consultar | Descrição |
|:--- |:--- |
| Todas as configurações de memória do host | Perf &#124; where ObjectName == "Capacity and Performance" and CounterName == "Host Assigned Memory MB" &#124; summarize MB = avg(CounterValue) by InstanceName |
| Todas as configurações de memória da VM | Perf &#124; where ObjectName == "Capacity and Performance" and CounterName == "VM Assigned Memory MB" &#124; summarize MB = avg(CounterValue) by InstanceName |
| Divisão dos IOPS de disco totais em todas as VMs | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "VHD Reads/s" or CounterName == "VHD Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Divisão da taxa de transferência de disco total em todas as VMs | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "VHD Read MB/s" or CounterName == "VHD Write MB/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Divisão de IOPS total em todos os CSVs | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Reads/s" or CounterName == "CSV Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Divisão da taxa de transferência total em todos os CSVs | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Reads/s" or CounterName == "CSV Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Divisão da latência total em todos os CSVs | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Read Latency" or CounterName == "CSV Write Latency") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |


## <a name="next-steps"></a>Próximas etapas
* Use [pesquisas de Log na análise de Log](log-analytics-log-searches.md) tooview obter dados de desempenho e capacidade.
