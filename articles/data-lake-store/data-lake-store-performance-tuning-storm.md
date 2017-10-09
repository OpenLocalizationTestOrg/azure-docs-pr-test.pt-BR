---
title: "diretrizes de ajuste de desempenho de Data Lake repositório profusão de aaaAzure | Microsoft Docs"
description: Diretrizes de ajuste de desempenho para Storm do Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: 5412fd46cf2373f5877030913df4fe1fc6f5473a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-storm-on-hdinsight-and-azure-data-lake-store"></a>Diretrizes de ajuste do desempenho para Storm no HDInsight e Azure Data Lake Store

Entenda os fatores de saudação que devem ser considerados ao ajustar o desempenho de saudação de uma topologia de profusão do Azure. Por exemplo, é importante toounderstand características de saudação do trabalho Olá Olá spouts e parafusos hello (se o trabalho de saudação é intensivo de memória ou e/s). Este artigo abrange uma gama de diretrizes de ajuste de desempenho, incluindo a solução de problemas comuns.

## <a name="prerequisites"></a>Pré-requisitos

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Uma conta do repositório Azure Data Lake**. Para obter instruções sobre como um, ver toocreate [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md).
* **Um cluster Azure HDInsight** com acesso tooa conta do repositório Data Lake. Confira [Criar um cluster HDInsight com o Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Verifique se que você habilitar a área de trabalho remota para o cluster de saudação.
* **Executando um cluster Storm no Data Lake Store**. Para obter mais informações, consulte [Storm no HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-overview).
* **Diretrizes de ajuste de desempenho do Data Lake Store**.  Para ver conceitos gerais de desempenho, consulte [Diretrizes de ajuste de desempenho do Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance).  

## <a name="tune-hello-parallelism-of-hello-topology"></a>Ajustar o paralelismo de saudação da topologia de saudação

Você pode ser capaz de tooimprove desempenho por cada vez maior simultaneidade de saudação de tooand de e/s de saudação do repositório Data Lake. Uma topologia Storm tem um conjunto de configurações que determinam o paralelismo hello:
* Número de processos do operador (trabalhadores Olá são distribuídos uniformemente por Olá VMs).
* Número de instâncias de executor de spout.
* Número de instâncias de bolt executor.
* Número de tarefas de spout.
* Número de tarefas de bolt.

Por exemplo, em um cluster com 4 VMs e 4 processos de trabalho, 32 spout executores e 32 spout tarefas e 256 executores de raio e tarefas de raio 512, considere o seguinte de saudação:

Cada supervisor, que é um nó de trabalho, tem um único processo de trabalho de máquina virtual Java (JVM). Esse processo JVM gerencia 4 threads de spout e 64 threads de bolt. Em cada thread, as tarefas são executadas sequencialmente. Com hello anterior de configuração, cada thread spout tem 1 tarefa e cada thread de raio tem 2 tarefas.

No Storm, aqui está Olá vários componentes envolvidos e como eles afetam o nível de saudação de paralelismo, que você tem:
* nó principal da saudação (chamado Nimbus no Storm) é usado toosubmit e gerenciar trabalhos. Esses nós não têm impacto sobre o grau de paralelismo hello.
* nós de supervisor Hello. Em HDInsight, isso corresponde nó de trabalho tooa VM do Azure.
* tarefas do trabalhador Olá são processos de Storm Olá VMs que executam. Cada tarefa de trabalho corresponde a instância do tooa da JVM. Tempestade distribui o número de saudação de processos de trabalho você especificar nós de trabalho toohello maneira mais uniforme possível.
* Instâncias de executores de bolt e spout. Cada instância do executor corresponde tooa thread em execução dentro de trabalhadores hello (JVMs).
* Tarefas do Storm. Essas são tarefas lógicas que cada um desses threads executa. Isso não altera o nível de saudação de paralelismo, portanto você deve avaliar se precisar de várias tarefas por executor ou não.

### <a name="get-hello-best-performance-from-data-lake-store"></a>Obter um melhor desempenho de saudação do repositório Data Lake

Ao trabalhar com o repositório Data Lake, você obter Olá melhor desempenho se você Olá a seguir:
* Una seus pequenos acréscimos em tamanhos maiores (o ideal é 4 MB).
* Faça o máximo possível de solicitações simultâneas. Como cada thread de raio está fazendo o bloqueio de leituras, convém toohave em algum lugar no intervalo de saudação de 8 a 12 threads por núcleo. Isso mantém a CPU NIC e Olá Olá utilizada. Uma VM maior permite mais solicitações simultâneas.  

### <a name="example-topology"></a>Exemplo de topologia

Suponhamos que você tenha um cluster de 8 nós de trabalho com a VM D13v2 do Azure. Essa VM tenha 8 núcleos, portanto entre Olá 8 nós de trabalho, você tem 64 núcleos total.

Digamos que façamos oito threads de bolt por núcleo. Dados 64 núcleos, isso significa que desejamos um total de 512 instâncias de executor de bolt (ou seja, threads). Nesse caso, digamos que podemos começar com uma JVM por VM e use principalmente a simultaneidade de thread hello dentro de simultaneidade de tooachieve JVM hello. Isso significa que precisamos de oito tarefas de trabalho (uma por VM do Azure) e 512 executores de bolt. Dada essa configuração, tempestade tenta trabalhadores de saudação toodistribute uniformemente entre nós de trabalho (também conhecidos como nós de supervisor), dando a cada nó de trabalho 1 JVM. Agora dentro de supervisores hello, tempestade tenta toodistribute executores de saudação uniformemente entre os supervisores, dando a cada supervisor (ou seja, JVM) 8 threads de cada.

## <a name="tune-additional-parameters"></a>Ajuste de parâmetros adicionais
Depois de ter topologia básica hello, você pode considerar se deseja tootweak qualquer um dos parâmetros de saudação:
* **Número de JVMs por nó de trabalho.** Se você tiver uma grande estrutura de dados (por exemplo, uma tabela de pesquisa) hospedada na memória, cada JVM vai precisar de uma cópia separada. Como alternativa, você pode usar estrutura de dados de saudação entre vários threads se você tiver menos JVMs. Para e/s do raio hello, Olá número de JVMs não faz muito de uma diferença como número de saudação de threads adicionado entre esses JVMs. Para simplificar, é toohave uma boa ideia uma JVM por trabalho. Dependendo de qual aplicativo de processamento ou de que está fazendo o raio requer, no entanto, talvez seja necessário toochange esse número.
* **Número de executores de spout.** Como hello exemplo anterior usa parafusos para gravar o repositório de Lake tooData, número de saudação de spouts não é desempenho de raio toohello diretamente relevantes. No entanto, dependendo da quantidade de saudação de processamento ou e/s ocorrendo no spout Olá, é uma boa ideia Olá tootune spouts para melhor desempenho. Certifique-se de que você tem suficiente spouts toobe tookeep capaz de saudação parafusos ocupado. Olá taxas de saída de hello spouts devem corresponder a taxa de transferência de saudação do hello parafusos. configuração real Olá depende spout hello.
* **Número de tarefas.** Cada bolt é executado como um único thread. Tarefas adicionais por bolt não fornecem simultaneidade adicional. Olá único momento em que eles sejam do benefício é se o processo de confirmar Olá tupla terá uma grande proporção de seu tempo de execução de raio. É um toogroup boa ideia que muitos tuplas em um maior acrescentar antes de enviar uma confirmação de rolo hello. Portanto, na maioria dos casos, várias tarefas não oferecem qualquer benefício adicional.
* **Agrupamento local ou aleatório.** Quando essa configuração é habilitada, tuplas são enviadas toobolts dentro Olá mesmo processo de trabalho. Isso reduz as chamadas de rede e comunicação entre processos. Isso é recomendado para a maioria das topologias.

Esse cenário básico é um bom ponto de partida. Teste com seu próprios Olá de tootweak dados precede o desempenho ideal de tooachieve de parâmetros.

## <a name="tune-hello-spout"></a>Ajustar spout Olá

Você pode modificar Olá configurações tootune Olá spout a seguir.

- **Tempo limite de tupla: topology.message.timeout.secs**. Essa configuração determina a quantidade de saudação de tempo uma mensagem toocomplete e receber a confirmação, antes que ela seja considerada falha.

- **Memória máxima por processo de trabalho: worker.childopts**. Essa configuração permite que você especifique trabalhadores de Java toohello parâmetros de linha de comando adicionais. Olá usado mais comumente configuração aqui é XmX, que determina o heap da JVM do tooa Olá máximo da memória alocada.

- **Máx. de spouts pendentes: topology.max.spout.pending**. Essa configuração determina o número de saudação de tuplas no podem ser voo (ainda não confirmado em todos os nós na topologia Olá) por thread spout a qualquer momento.

 Toodo um cálculo BOM é o tamanho de saudação do tooestimate de cada um dos seus tuplas. Em seguida, calcule quanta memória um thread de spout tem. Olá memória total alocada tooa thread, dividido por esse valor, deverá lhe fornecer Olá limite superior spout máximo de saudação pendentes parâmetro.

## <a name="tune-hello-bolt"></a>Ajustar a isoladas Olá
Quando você está escrevendo o repositório de Lake tooData, definir uma política de sincronização de tamanho (buffer no lado do cliente Olá) too4 MB. Uma liberação ou hsync() é executada somente quando o tamanho do buffer de saudação é hello nesse valor. driver de repositório Data Lake Olá Worker Olá VM automaticamente faz esse buffer, a menos que você executa uma hsync() explicitamente.

parafuso de profusão de repositório do Data Lake saudação padrão tem um parâmetro de política do sincronização tamanho (fileBufferSize) pode ser usado tootune esse parâmetro.

Em topologias com alto e/S, é uma boa ideia toohave cada thread de raio gravar arquivo próprio tooits e tooset uma política de rotação de arquivo (fileRotationSize). Quando o arquivo hello atinge um determinado tamanho, fluxo Olá automaticamente é liberado e um novo arquivo é gravado. Olá tamanho de arquivo para rotação recomendado é de 1 GB.

### <a name="handle-tuple-data"></a>Manipulação de dados de tupla

No Storm, um spout mantém na tupla tooa até que ele seja confirmado explicitamente pelo raio hello. Se uma tupla foi lida pelo raio hello, mas ainda não foram confirmada, spout Olá pode não ter persistido no back-end do repositório Data Lake. Depois de uma tupla é confirmada, spout Olá pode ser garantida persistência pelo raio hello e pode excluir dados de origem de saudação de qualquer fonte que ela está lendo de.  

Para melhor desempenho em repositório Data Lake, ter raio de saudação de buffer de dados de tupla de 4 MB. Em seguida, escreva toohello repositório Data Lake volta terminar como uma gravação de 4 MB. Depois que dados saudação foi gravado com êxito toohello repositório (por chamada hflush()), raio Olá pode confirmar Olá dados toohello back spout. Este é o exemplo hello parafuso fornecido não aqui. Também é aceitável toohold um número maior de tuplas antes Olá hflush() chamada é feita e hello tuplas confirmadas. No entanto, isso aumenta o número de saudação de tuplas em trânsito que spout Olá precisa toohold e, portanto, aumenta Olá a quantidade de memória exigida por JVM.

> [!NOTE]
Aplicativos podem ter uma tuplas de tooacknowledge requisito com mais frequência (em tamanhos de dados menor que 4 MB) por outros motivos de desempenho não. No entanto, que pode afetar hello e/s taxa de transferência toohello armazenamento back-end. Avalie cuidadosamente essa compensação em relação ao desempenho de e/s do raio da saudação.

Se taxa de entrada hello de tuplas for não alta, para que o buffer de 4 MB de saudação leva um tempo longo toofill, considere reduzir isso por:
* Reduzindo o número de saudação de parafusos, portanto, há menos toofill de buffers.
* Ter uma política com base em contagem ou tempo, onde um hflush() é disparado cada x liberações ou cada milissegundos y e tuplas Olá acumuladas até o momento reconhecidas novamente.

Observe que a taxa de transferência Olá nesse caso é menor, mas com uma taxa baixa de eventos, taxa de transferência máxima não é objetivo maior Olá mesmo assim. Essas reduções ajudar a reduzir o tempo total de saudação que leva para um tooflow tupla toohello armazenam. Isso pode ser relevante se você quiser um pipeline em tempo real, mesmo com uma taxa baixa de evento. Observe também que se a taxa de entrada de tupla for baixa, você deve ajustar parâmetro topology.message.timeout_secs Olá para Olá tuplas não atingir o tempo limite enquanto eles estão obtendo em buffer ou processado.

## <a name="monitor-your-topology-in-storm"></a>Monitorar a topologia no Storm  
Durante a execução de sua topologia, você pode monitorá-lo na interface do usuário Storm hello. Aqui estão Olá parâmetros principais toolook em:

* **Latência total de execução do processo.** Este é o tempo médio de saudação uma tupla leva toobe emitidos pelo spout hello, processados pelo raio hello e confirmado.

* **Latência total de processo do bolt.** Este é o tempo médio de saudação gasto pela tupla Olá a isoladas Olá até receber uma confirmação.

* **Latência total de execute do bolt.** Isso é a média de saudação tempo gasto pelo raio Olá no hello executar o método.

* **Número de falhas.** Isso se refere a toohello número de tuplas que toobe totalmente processado antes que eles atingiu o tempo limite de falha.

* **Capacidade.** Medida da ocupação do sistema. Se esse número é 1, os bolts estão trabalhando tão rápido quanto possível. Se for menor que 1, aumente o paralelismo de saudação. Se for maior que 1, reduza o paralelismo de saudação.

## <a name="troubleshoot-common-problems"></a>Solução de problemas comuns
Eis alguns cenários comuns de solução de problemas.
* **Grande número de tuplas atingindo o tempo limite.** Pesquisar em cada nó na Olá topologia toodetermine onde é o afunilamento hello. Olá mais comuns motivo para isso é que Olá parafusos não tookeep capaz de backup com spouts hello. Isso leva tootuples sobrecarregando os buffers internos de saudação enquanto espera toobe processados. Considere aumentar o valor de tempo limite de saudação ou diminuindo spout máximo de saudação pendente.

* **Há uma latência alta de execução do processo total, mas uma latência baixa de processo do bolt.** Nesse caso, é possível que Olá tuplas não são sejam confirmadas rápido o suficiente. Verifique se há um número suficiente de confirmadores. Outra possibilidade é que estão aguardando na fila de saudação por muito tempo antes de saudação bolts início processá-las. Diminua spout máximo de saudação pendente.

* **Latência de execute do bolt elevada.** Isso significa que o método Execute () Olá a isoladas está demorando muito. Otimizar código hello, ou examinar os tamanhos de gravação e comportamento de liberação.

### <a name="data-lake-store-throttling"></a>Limitação do Data Lake Store
Se você atingir os limites de largura de banda fornecida pelo repositório Data Lake hello, você poderá ver falhas de tarefas. Verifique os logs de tarefa para erros de limitação. Você pode diminuir o paralelismo Olá aumentando o tamanho do contêiner.    

toocheck se você estiver obtendo limitada, habilitar Olá log de depuração no lado do cliente hello:

1. Em **Ambari** > **Storm** > **Config** > **avançado profusão de trabalhador de log4j**, alterar  **&lt;raiz nível = "info"&gt;**  muito**&lt;raiz nível = "depuração"&gt;**. Reinicie todos os nós/serviço Olá para efeito de tootake configuração hello.
2. Topologia de profusão de saudação do Monitor registra em nós de trabalho (em /var/log/storm/worker-artifacts /&lt;TopologyName&gt;/&lt;porta&gt;/worker.log) para o repositório Data Lake exceções de limitação.

## <a name="next-steps"></a>Próximas etapas
Ajuste de desempenho adicional para o Storm pode ser referenciado [neste blog](https://blogs.msdn.microsoft.com/shanyu/2015/05/14/performance-tuning-for-hdinsight-storm-and-microsoft-azure-eventhubs/).

Para um toorun exemplo adicionais, consulte [la no GitHub](https://github.com/hdinsight/storm-performance-automation).
