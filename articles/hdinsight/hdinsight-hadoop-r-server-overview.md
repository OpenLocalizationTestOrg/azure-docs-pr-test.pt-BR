---
title: aaaIntroduction tooR Server no Azure HDInsight | Microsoft Docs
description: "Saiba como toouse R Server em aplicativos de toocreate de HDInsight para análise de dados grande."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6dc21bf5-4429-435f-a0fb-eea856e0ea96
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: daf7b70a15748d66510a04da370f39c5f26eb4ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#<a name="introduction-toor-server-and-open-source-r-capabilities-on-hdinsight"></a>Introdução tooR servidor e recursos de R de código-fonte aberto no HDInsight

O Microsoft R Server está disponível como uma opção de implantação quando você cria clusters HDInsight no Azure. Esse novo recurso fornece os cientistas de dados estatísticos e programadores de R com tooscalable acesso sob demanda, distribuídos métodos de análise no HDInsight.

Clusters podem ser dimensionados adequadamente toohello projetos e tarefas em questão e, em seguida, subdividido quando eles não são mais necessários. Desde que eles fazem parte do Azure HDInsight, esses clusters vêm com suporte 24/7 de nível empresarial, um SLA de 99,9% de disponibilidade e Olá capacidade toointegrate com outros componentes de saudação ecossistema do Azure.

R Server no HDInsight fornece recursos mais recentes de saudação para análise de R em conjuntos de dados de praticamente qualquer tamanho, carregado tooeither armazenamento de BLOBs do Azure ou Data Lake. Desde o R Server se baseia no R de software livre, Olá R aplicativos que você criar podem aproveitar Olá 8000 + pacotes de R de software livre. rotinas de saudação em ScaleR, pacote de análise de dados grande da Microsoft incluído no R Server, também estão disponíveis.

nó de borda de saudação de um cluster fornece um local conveniente tooconnect toohello cluster e toorun seus scripts de R. Com um nó de borda, você deve ter funções de opção de execução hello paralelizado distribuída Olá de ScaleR entre núcleos de saudação do servidor de nó de borda hello. Você também pode executá-los em nós de saudação do cluster Olá por meio do ScaleR Hadoop mapear redução ou Spark contextos de computação.

modelos de saudação ou previsões que resultados de análise podem ser baixado para usam no local. Elas também podem ser operacionalizadas em qualquer lugar no Azure, como por meio de um [serviço Web](../machine-learning/machine-learning-publish-a-machine-learning-web-service.md) no [Azure Machine Learning Studio](http://studio.azureml.net).

## <a name="get-started-with-r-on-hdinsight"></a>Introdução ao R no HDInsight
tooinclude R Server em um cluster HDInsight, você deve selecionar Olá tipo de cluster de servidor de R ao criar um cluster HDInsight usando Olá portal do Azure. Olá tipo de cluster de servidor de R inclui R Server Olá nós de dados de cluster hello e em um nó de borda, que serve como uma zona de aterrissagem para análise baseada em servidor de R. Consulte [guia de Introdução ao servidor do R no HDInsight](hdinsight-hadoop-r-server-get-started.md) para obter uma explicação sobre como toocreate Olá cluster.

## <a name="learn-about-data-storage-options"></a>Saiba mais sobre as opções de armazenamento de dados
Armazenamento padrão para o sistema de arquivos HDFS Olá de clusters de HDInsight pode ser associado uma conta de armazenamento do Azure ou um repositório Azure Data Lake. Essa associação garante que os dados que são carregados toohello armazenamento de cluster durante a análise é feito persistente. Há várias ferramentas para lidar com hello dados transferência toohello opção de armazenamento que você selecionar, incluindo Olá recurso de carregamento baseado no portal de conta de armazenamento hello e hello [AzCopy](../storage/common/storage-use-azcopy.md) utilitário.

Você tem a opção de saudação de adicionar acesso tooadditional Blob e lake armazenamentos de dados durante o processo, independentemente da opção de armazenamento primário Olá em uso de provisionamento de cluster de saudação. Consulte [guia de Introdução ao servidor do R no HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-get-started) para obter informações sobre como adicionar contas de acesso de tooadditional. Consulte Olá suplementar [opções de armazenamento do Azure para R Server HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-storage) artigo toolearn mais sobre como usar várias contas de armazenamento.

Você também pode usar [arquivos do Azure](../storage/files/storage-how-to-use-files-linux.md) como uma opção de armazenamento para uso no nó de borda hello. Arquivos do Azure permite que você toomount um compartilhamento de arquivo que foi criado no armazenamento do Azure toohello sistema de arquivos do Linux. Para obter mais informações sobre essas opções de armazenamento de dados para R Server no cluster HDInsight, confira [Opções de Armazenamento do Azure para o R Server em clusters HDInsight](hdinsight-hadoop-r-server-storage.md).

## <a name="access-r-server-on-hello-cluster"></a>Acesso R Server no cluster Olá
Você pode conectar tooR Server no nó de borda hello usando um navegador, desde que você escolheu tooinclude RStudio servidor durante o processo de provisionamento de saudação. Se você não o instalou ao provisionar o cluster Olá, você pode adicioná-lo mais tarde. Para obter informações sobre como instalar o RStudio Server após a criação de um cluster, veja [Instalando o RStudio Server em clusters HDInsight](hdinsight-hadoop-r-server-install-r-studio.md). Você também pode conectar toohello R Server usando o console do SSH/PuTTY tooaccess Olá R. 

## <a name="develop-and-run-r-scripts"></a>Desenvolver e executar scripts R
scripts de saudação R, criar e executar podem usar qualquer um dos Olá 8000 + pacotes de software livre R em adição toohello paralelizado e distribuídas rotinas disponíveis na biblioteca de ScaleR hello. Em geral, um script que é executado com R Server no nó de borda Olá é executado em interpretador Olá R nesse nó. exceções de saudação são as etapas que precisam toocall uma função ScaleR com um contexto de computação é definido tooHadoop mapear redução (RxHadoopMR) ou Spark (RxSpark). Nesse caso, a função hello executa no modo distribuído entre os nós de dados (tarefas) do cluster Olá associados a dados Olá referenciados. Para obter mais informações sobre as opções de contexto de computação diferentes hello, consulte [computação opções de contexto para o servidor do R no HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).

## <a name="operationalize-a-model"></a>Operacionalizar um modelo
Quando a modelagem de dados for concluída, você pode colocar previsões de toomake Olá modelo para novos dados a partir do Azure e no local. Esse processo é conhecido como pontuação. A pontuação pode ser feita em HDInsight, no Azure Machine Learning ou local.

### <a name="score-in-hdinsight"></a>Pontuação no HDInsight
tooscore no HDInsight, escrever uma função de R que chama suas previsões de toomake de modelo para um novo arquivo de dados que você carregou tooyour conta de armazenamento. Salve previsões Olá back toohello conta de armazenamento. Você pode executar Olá rotina sob demanda no nó de borda de saudação do cluster ou por meio de um trabalho agendado.  

### <a name="score-in-azure-machine-learning-aml"></a>Pontuação no AML (Azure Machine Learning)
tooscore usando um serviço web AML, use Olá abre o pacote de R de aprendizado de máquina do Azure de origem, conhecido como [AzureML](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) toopublish seu modelo como um serviço web do Azure. Para sua conveniência, este pacote é instalado em um nó de borda de saudação. Em seguida, usar os recursos de Olá no aprendizado de máquina toocreate uma interface do usuário para o serviço web de saudação e, em seguida, chamar Olá web service, conforme necessário para pontuação.

Se você escolher essa opção, será necessário tooconvert quaisquer objetos de modelo de código-fonte aberto ScaleR modelo objetos tooequivalent para usam com o serviço web de saudação. Use as funções de coerção do ScaleR, tais como `as.randomForest()` para modelos baseados em combinação, para essa conversão.

### <a name="score-on-premises"></a>Pontuação local
tooscore local depois de criar seu modelo, você pode serializar um modelo de saudação em R, download, desserializá-lo e, em seguida, usá-lo para pontuar novos dados. Você pode classificar dados novo usando a abordagem de saudação descrita anteriormente na [pontuação no HDInsight](#scoring-in-hdinsight) ou usando [DeployR](https://deployr.revolutionanalytics.com/).

## <a name="maintain-hello-cluster"></a>Manter o cluster Olá
### <a name="install-and-maintain-r-packages"></a>Instalar e manter pacotes R
A maioria dos pacotes de saudação R que você usar é necessários no nó de borda Olá desde a maioria das etapas dos seus scripts de R lá executados. tooinstall pacotes R adicionais no nó de borda hello, você pode usar a saudação normal `install.packages()` método em R.

Se você apenas estiver usando rotinas de biblioteca de ScaleR Olá cluster Olá, você não é geralmente necessário tooinstall pacotes de R adicionais Olá nós de dados. No entanto, talvez seja necessário pacotes adicionais toosupport Olá uso **rxExec** ou **RxDataStep** execução Olá nós de dados.

Nesses casos, pacotes de saudação adicional podem ser instalados com uma ação de script depois de criar o cluster de saudação. Para saber mais, confira [Criando um cluster HDInsight com o R Server](hdinsight-hadoop-r-server-get-started.md).   

### <a name="change-hadoop-map-reduce-memory-settings"></a>Alterar as configurações de memória do Hadoop Map Reduce
Um cluster pode ser modificado toochange quantidade de saudação de memória disponível tooR servidor quando ele está em execução em um trabalho de redução de mapa. toomodify um cluster, use Olá Apache Ambari da interface do usuário que está disponível por meio de saudação folha portal do Azure para seu cluster. Para obter instruções sobre como tooaccess Olá Ambari UI para seu cluster, consulte [gerenciar clusters HDInsight usando Olá da interface do usuário do Ambari Web](hdinsight-hadoop-manage-ambari.md).

Também é possível toochange quantidade de saudação de memória disponível tooR servidor usando opções de Hadoop na chamada de saudação muito**RxHadoopMR** da seguinte maneira:

    hadoopSwitches = "-libjars /etc/hadoop/conf -Dmapred.job.map.memory.mb=6656"  

### <a name="scale-your-cluster"></a>Ajustar escala do cluster
Um cluster existente pode ser dimensionado para cima ou para baixo, por meio do portal hello. Dimensionando, você pode obter a capacidade adicional de saudação que talvez sejam necessários para tarefas de processamento maior ou reduza um cluster quando ele estiver ocioso. Para obter instruções sobre como tooscale um cluster, consulte [HDInsight gerenciar clusters](hdinsight-administer-use-portal-linux.md).

### <a name="maintain-hello-system"></a>Manter o sistema Olá
Outras atualizações e patches do sistema operacional tooapply manutenção é realizada em Olá subjacente VMs do Linux em um cluster HDInsight fora do horário comercial. Normalmente, manutenção é feita às 3:30:00 (com base na hora local Olá Olá VM) toda segunda-feira e quinta-feira. As atualizações são executadas de forma que eles não afetam mais de um trimestre de cluster Olá por vez.  

Como nós de cabeçalho Olá são redundante e nem todos os nós de dados são afetados, todos os trabalhos que estão em execução durante esse tempo podem reduzir a velocidade. Eles ainda devem executar toocompletion, no entanto. Todos os dados locais ou de software personalizados que você tem são preservados nesses eventos de manutenção, a menos que uma falha catastrófica ocorra e exija uma recriação do cluster.

## <a name="learn-about-ide-options-for-r-server-on-an-hdinsight-cluster"></a>Saiba mais sobre opções de IDE para o Servidor R em um cluster HDInsight
nó de borda do Hello Linux de um cluster HDInsight é saudação inicial de zona para a análise baseada em R. Versões recentes do HDInsight fornecem uma opção padrão para instalar a versão da comunidade Olá [RStudio Server](https://www.rstudio.com/products/rstudio-server/) no nó de borda hello como um IDE baseada em navegador. Uso do servidor de RStudio como um IDE para o desenvolvimento de saudação e execução de scripts de R podem ser consideravelmente mais produtivas do que usando apenas o console Olá R. Se você escolheu tooadd RStudio servidor quando criar hello cluster mas gostariam tooadd-lo mais tarde, em seguida, consulte [instalando o R Studio Server em clusters de HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-install-r-studio). +

Outra opção de IDE completa é tooinstall um IDE de área de trabalho e usá-lo em cluster de saudação tooaccess através do uso de um contexto de computação de redução de mapa ou Spark remoto. As opções incluem a Microsoft RTVS ([Ferramentas do R para Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx)), RStudio e o [StatET](http://www.walware.de/goto/statet) baseado em Eclipse da Walware.

Por fim, você pode acessar o console de R Server de saudação no nó de borda Olá digitando **R** no prompt de comando do Linux Olá depois de se conectar via SSH ou PuTY. Ao usar a interface do console hello, ele é conveniente toorun um editor de texto para o desenvolvimento de script R em outra janela e recorte e cole seções do seu script no console de saudação R conforme necessário.

## <a name="learn-about-pricing"></a>Saiba mais sobre preços
Hello taxas associadas um cluster de servidor de R de HDInsight estruturadas da mesma forma toohello taxas para clusters de HDInsight saudação padrão. Eles se baseiam no dimensionamento de saudação do hello subjacente VMs em nome hello, dados e nós de borda, com a adição de saudação de um upgrade de horas de núcleo. Para obter mais informações sobre preços do HDInsight e a disponibilidade de saudação de uma avaliação gratuita de 30 dias, consulte [preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="next-steps"></a>Próximas etapas
toolearn mais informações sobre como toouse R Server com HDInsight clusters, consulte Olá seguintes tópicos:

* [Introdução ao uso do Servidor R no HDInsight](hdinsight-hadoop-r-server-get-started.md)
* [Adicionar servidor RStudio tooHDInsight (se não é instalado durante a criação do cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opções de contexto de computação para o Servidor R no HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)
* [Opções de Armazenamento do Azure para o Servidor R no HDInsight](hdinsight-hadoop-r-server-storage.md)
