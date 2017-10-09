---
title: "aaaAzure Data Lake repositório MapReduce ajuste diretrizes de desempenho | Microsoft Docs"
description: Diretrizes de ajuste de desempenho para MapReduce do Azure Data Lake Store
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
ms.openlocfilehash: e21414a23530e65613c85156af0209c88ec54d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-mapreduce-on-hdinsight-and-azure-data-lake-store"></a>Diretrizes de ajuste do desempenho para o MapReduce no HDInsight e Azure Data Lake Store


## <a name="prerequisites"></a>Pré-requisitos

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Uma conta do repositório Azure Data Lake**. Para obter instruções sobre como um, ver toocreate [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)
* **Cluster de HDInsight do Azure** com acesso tooa conta do repositório Data Lake. Confira [Criar um cluster HDInsight com o Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Verifique se que você habilitar a área de trabalho remota para o cluster de saudação.
* **Usando o MapReduce no HDInsight**.  Para obter mais informações, consulte [Usar o MapReduce no Hadoop no HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)  
* **Diretrizes de ajuste de desempenho no ADLS**.  Para ver os conceitos gerais de desempenho, confira [Diretrizes de ajuste de desempenho do Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)  

## <a name="parameters"></a>parâmetros

Ao executar trabalhos de MapReduce, eis os Olá parâmetros mais importantes que você pode configurar o desempenho de tooincrease em ADLS:

* **MapReduce.map.Memory.MB** – quantidade de saudação do mapeador de tooeach de tooallocate de memória
* **MapReduce.job.Maps** – Olá número de tarefas de mapa por trabalho
* **MapReduce** – quantidade de saudação do Redutor de tooeach de tooallocate de memória
* **MapReduce.job.Reduces** – Olá número de tarefas de redução por trabalho

**MapReduce.map.Memory / Mapreduce.reduce.memory** esse número deve ser ajustada com base em como a quantidade de memória é necessária para o mapa de saudação e/ou reduzir a tarefa.  valores padrão de saudação do mapreduce.map.memory e mapreduce.reduce.memory podem ser exibidos no Ambari através da configuração do Yarn hello.  No Ambari, navegar tooYARN e exiba a guia de configurações de saudação.  Olá memória YARN será exibida.  

**MapReduce.job.Maps / Mapreduce.job.reduces** isso determinará o número máximo de saudação de mapeadores ou reducers toobe criado.  número de saudação de divisões determinará quantos mapeadores serão criados para o trabalho de MapReduce Olá.  Portanto, você pode receber menos mapeadores de solicitado se há menos divisões que número de saudação de mapeadores solicitado.       

## <a name="guidance"></a>Diretrizes

**Etapa 1: Determinar o número de trabalhos em execução** -por padrão, MapReduce usará o cluster inteiro Olá para seu trabalho.  Você pode usar menos cluster hello usando menos mapeadores de que os contêineres disponíveis.  Guia de saudação neste documento presume que seu aplicativo é o único aplicativo de saudação em execução no seu cluster.      

**Etapa 2: Configurar mapreduce.map.memory/mapreduce.reduce.memory** – Olá tamanho da memória de saudação de mapa e reduzir tarefas serão dependentes em seu trabalho específico.  Você pode reduzir o tamanho da memória Olá se você quiser tooincrease simultaneidade.  número de saudação de tarefas em execução simultaneamente depende número Olá de contêineres.  Ao diminuir a quantidade de saudação de memória por mapeador ou Redutor, mais contêineres podem ser criados, que permitem mais toorun mapeadores ou reducers simultaneamente.  Quantidade Olá decrescente de memória muito pode causar algumas toorun processos sem memória.  Se você receber um erro de heap ao executar seu trabalho, você deve aumentar memória Olá por mapeador ou Redutor.  Considere que adicionar mais contêineres adicionará sobrecarga extra para cada contêiner adicional, o que pode degradar o desempenho.  Outra alternativa é tooget mais memória usando um cluster que tem a maior quantidade de memória ou aumentar Olá número de nós no cluster.  Mais memória permitirá toobe contêineres mais usado, o que significa que mais de simultaneidade.  

**Etapa 3: Determinar a memória Total YARN** -tootune mapreduce.job.maps/mapreduce.job.reduces, você deve considerar a quantidade de saudação de memória total do YARN disponível para uso.  Essas informações estão disponíveis no Ambari.  Navegue tooYARN e exiba a guia de configurações de saudação.  Olá memória YARN é exibido nesta janela.  Você deve multiplicar Olá YARN de memória com número de saudação de nós no seu cluster tooget Olá total YARN de memória.

    Total YARN memory = nodes * YARN memory per node
Se você estiver usando um cluster vazio, memória poderá ser Olá total YARN de memória para o cluster.  Se outros aplicativos estão usando memória, em seguida, você pode escolher usar tooonly uma parte da memória do seu cluster, reduzindo o número de saudação de mapeadores reducers toohello número de contêineres, você deseja toouse.  

**Etapa 4: Calcular o número de contêineres YARN** – contêineres YARN ditam a quantidade de saudação de simultaneidade disponível para o trabalho de saudação.  Pegar a memória YARN total e divida-a por mapreduce.map.memory.  

    # of YARN containers = total YARN memory / mapreduce.map.memory

**Etapa 5: Definir mapreduce.job.maps/mapreduce.job.reduces** definir mapreduce.job.maps/mapreduce.job.reduces tooat menor número de saudação de recipientes disponíveis.  Você pode testar adicional, aumentando o número de saudação de toosee mapeadores e reducers se obter um melhor desempenho.  Tenha em mente que mais mapeadores terão uma sobrecarga adicional, então ter um número excessivo de mapeadores pode degradar o desempenho.  

Agendamento de CPU e o isolamento de CPU estão desativados por padrão para que o número de saudação de contêineres YARN é restrito por memória.

## <a name="example-calculation"></a>Exemplo de cálculo

Digamos que você possui um cluster composto de 8 nós D14 e você deseja toorun um trabalho de uso intensivo de e/s.  Aqui estão os cálculos de saudação, que você deve fazer:

**Etapa 1: Determinar o número de trabalhos em execução** -para nosso exemplo, vamos supor que nosso trabalho é Olá apenas uma execução.  

**Etapa 2: definir mapreduce.map.memory/mapreduce.reduce.memory** – em nosso exemplo, você está executando um trabalho com uso intensivo de E/S e decide que 3 GB de memória para tarefas de mapeamento serão suficientes.

    mapreduce.map.memory = 3GB
**Etapa 3: determinar o total de memória YARN**

    total memory from hello cluster is 8 nodes * 96GB of YARN memory for a D14 = 768GB
**Etapa 4: calcular o número de contêineres YARN**

    # of YARN containers = 768GB of available memory / 3 GB of memory =   256

**Etapa 5: definir mapreduce.job.maps/mapreduce.job.reduces**

    mapreduce.map.jobs = 256

## <a name="limitations"></a>Limitações

**Limitação do ADLS**

Como um serviço multilocatário, o ADLS define limites de largura de banda de nível de conta.  Se você receber esses limites, você começará toosee falhas de tarefas. Isso pode ser identificado observando os erros de limitação nos logs de tarefa.  Se precisar de mais largura de banda para seu trabalho, entre em contato conosco.   

toocheck se você estiver obtendo limitadas, você precisa tooenable Olá log de depuração no lado do cliente de saudação. Veja como fazer isso:

1. PUT hello seguinte propriedade nas propriedades log4j Olá Ambari > YARN > Configuração > Avançado yarn log4j: log4j.logger.com.microsoft.azure.datalake.store=DEBUG

2. Reinicie todos os nós/serviço Olá para efeito de tootake Olá config.

3. Se você estiver obtendo limitada, você verá o código de erro HTTP 429 Olá no arquivo de log YARN Olá. arquivo de log do Hello YARN está em /tmp/&lt;usuário&gt;/yarn.log

## <a name="examples-toorun"></a>Exemplos tooRun

toodemonstrate como MapReduce é executado no repositório Azure Data Lake, abaixo está um código de exemplo que foi executado em um cluster com hello configurações a seguir:

* 16 nós D14v2
* Cluster Hadoop executando HDI 3.6

Para um ponto de partida, aqui estão alguns comandos de exemplo toorun MapReduce Teragen, Terasort e Teravalidate.  Você pode ajustar esses comandos com base em seus recursos.

**Teragen**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 10000000000 adl://example/data/1TB-sort-input

**Terasort**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 -Dmapreduce.job.reduces=512 -Dmapreduce.reduce.memory.mb=3072 adl://example/data/1TB-sort-input adl://example/data/1TB-sort-output

**Teravalidate**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapreduce.job.maps=512 -Dmapreduce.map.memory.mb=3072 adl://example/data/1TB-sort-output adl://example/data/1TB-sort-validate
