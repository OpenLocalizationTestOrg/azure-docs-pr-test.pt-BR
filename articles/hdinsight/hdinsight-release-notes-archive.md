---
title: "Notas de versão de aaaArchived - componentes do Hadoop no HDInsight do Azure | Microsoft Docs"
description: "Notas de versão arquivadas para versões mais antigas de componentes do Hadoop para Azure HDInsight."
services: hdinsight
documentationcenter: 
editor: cgronlun
manager: jhubbard
author: nitinme
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 7a99c77f4557ca8c1dabe924cc67b2e0a134f8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-archive-for-hadoop-components-on-azure-hdinsight"></a>Notas de versão (arquivadas) dos componentes do Hadoop no Azure HDInsight

Este artigo fornece informações sobre Olá **antigos** atualizações de versão do HDInsight do Azure. Para obter informações sobre versões mais recentes, consulte as [Notas de versão do HDInsight](hdinsight-release-notes.md).

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para saber mais, confira o [artigo sobre controle de versão do HDInsight](hdinsight-component-versioning.md).



## <a name="notes-for-08302016-release-of-hdinsight"></a>Notas da versão de 30/08/2016 do HDInsight
números de versão completa Olá para clusters HDInsight baseados em Linux é implantado com esta versão:

| HDI | Versão de cluster do HDI | HDP | Compilação HDP | Build do Ambari |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8268980 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8268980 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8269383 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

números de versão completa Olá para clusters HDInsight baseados em Windows implantado com esta versão:

| HDI | Versão de cluster do HDI | HDP | Compilação HDP |
| --- | --- | --- | --- |
| 2,1 |2.1.10.1033.2559206 |1,3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1033.2559206 |2,0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1033.2559206 |2,1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1033.2559206 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1033.2559206 |2.3 |2.3.3.1-25 |


## <a name="08172016---release-of-r-server-on-hdinsight"></a>17/08/2016 – Versão do R Server no HDInsight
* R Server 8.0.5 – Uma versão basicamente de correção de bug. Consulte Olá [notas de versão do servidor de R](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes) para obter mais informações.
* Pacote do AzureML no nó de borda Olá - [esse pacote de R](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) habilita R toobe de modelos publicados e consumidos como um serviço da web do Azure ML.  Consulte Olá ["Operacionalizar um modelo"](hdinsight-hadoop-r-server-overview.md#operationalize-a-model) seção do nosso ["Visão geral de R Server no HDInsight"](hdinsight-hadoop-r-server-overview.md) artigo para obter mais informações.
* Dependências do Linux de saudação [top 100 pacotes R mais populares](https://github.com/metacran/cranlogs) -essas dependências do pacote de Linux agora são pré-instaladas.
* Os pacotes do repositório opção toouse Olá CRAN ao adicionar R toohello nós de dados. Para obter mais informações, confira ["Introdução ao uso do R Server no HDInsight"](hdinsight-hadoop-r-server-get-started.md).
* Confiabilidade Olá aprimorada de provisionamento do servidor do R quando os clusters são criados.

## <a name="notes-for-08012016-release-of-hdinsight"></a>Notas da versão de 01/08/2016 do HDInsight
números de versão completa Olá para clusters HDInsight baseados em Linux é implantado com esta versão:

| HDI | Versão de cluster do HDI | HDP | Compilação HDP | Build do Ambari |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8028416 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8028416 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8053402 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

números de versão completa Olá para clusters HDInsight baseados em Windows implantado com esta versão:

| HDI | Versão de cluster do HDI | HDP | Compilação HDP |
| --- | --- | --- | --- |
| 2,1 |2.1.10.1005.2488842 |1,3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1005.2488842 |2,0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1005.2488842 |2,1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1005.2488842 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1005.2488842 |2.3 |2.3.3.1-25 |

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Spark, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| Alterações tooHDInsight 3.4 clusters |valores padrão de saudação para seguintes configurações de hive são alterados para melhorar o desempenho <ul><li>`hive.vectorized.execution.reduce.enabled=true`</li><li>`hive.tez.min.partition.factor=1f`</li><li>`hive.tez.max.partition.factor=3f`</li><li>`tez.shuffle-vertex-manager.min-src-fraction=0.9`</li><li>`tez.shuffle-vertex-manager.max-src-fraction=0.95`</li><li>`tez.runtime.shuffle.connect.timeout= 30000`</li></ul> |O Barramento de |Todos |N/D |
| As correções a seguir estão incluídas nesta versão |HIVE-13632, HIVE-12897,HIVE-12907,HIVE-12908,HIVE-12988,HIVE-13510,HIVE-13572,HIVE-13716,HIVE-13726,HIVE-12505,HIVE-13632,HIVE-13661,HIVE-13705,HIVE-13743,HIVE-13810,HIVE-13857,HIVE-13902,HIVE-13911,HIVE-13933 |O Barramento de |Todos |N/D |

## <a name="notes-for-07142016-release-of-hdinsight"></a>Notas da versão de 14/07/2016 do HDInsight
números de versão completa Olá para clusters HDInsight baseados em Linux é implantado com esta versão:

| HDI | Versão de cluster do HDI | HDP | Compilação HDP | Build do Ambari |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7932505 |2.2 |2.2.9.1-11 |2.2.1.12-2 |
| 3.3 |3.3.1000.0.7932505 |2.3 |2.3.3.1-18 |2.2.1.12-2 |
| 3.4 |3.4.1000.0.7933003 |2.4 |2.4.2.0 |2.2.1.12-2 |

números de versão completa Olá para clusters HDInsight baseados em Windows implantado com esta versão:

| HDI | Versão de cluster do HDI | HDP | Compilação HDP |
| --- | --- | --- | --- |
| 2,1 |2.1.10.989.2441725 |1,3 |1.3.12.0-01795 |
| 3.0 |3.0.6.989.2441725 |2,0 |2.0.13.0-2117 |
| 3.1 |3.1.4.989.2441725 |2,1 |2.1.16.0-2374 |
| 3.2 |3.2.7.989.2441725 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.989.2441725 |2.3 |2.3.3.1-21 |

## <a name="notes-for-07072016-release-of-hdinsight"></a>Notas da versão de 07/07/2016 do HDInsight
números de versão completa Olá para clusters HDInsight baseados em Linux é implantado com esta versão:

| HDI | Versão de cluster do HDI | HDP | Compilação HDP |
| --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7864996 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.1000.0.7864996 |2.3 |2.3.3.1-18 |
| 3.4 |3.4.1000.0.7861906 |2.4 |2.4.2.0 |

números de versão completa Olá para clusters HDInsight baseados em Windows implantado com esta versão:

| HDI | Versão de cluster do HDI | HDP | Compilação HDP |
| --- | --- | --- | --- |
| 2,1 |2.1.10.977.2413853 |1,3 |1.3.12.0-01795 |
| 3.0 |3.0.6.977.2413853 |2,0 |2.0.13.0-2117 |
| 3.1 |3.1.4.977.2413853 |2,1 |2.1.16.0-2374 |
| 3.2 |3.2.7.977.2413853 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.977.2413853 |2.3 |2.3.3.1-21 |

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Spark, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| [Ferramentas do HDInsight para IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md) |O plug-in IntelliJ IDEA para clusters HDInsight Spark agora está integrado ao Kit de ferramentas do Azure para IntelliJ. Ele dá suporte a v2.9.1 do SDK do Azure, SDKs de Java mais recente e inclui todos os recursos de saudação do hello autônomo HDInsight Plugin para IntelliJ. |Ferramentas |Spark |N/D |
| [Ferramentas do HDInsight para Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md) |O Kit de ferramentas do Azure para Eclipse agora dá suporte a clusters HDInsight Spark. Ele permite Olá recursos a seguir: <ul><li>Crie e escreva um aplicativo Spark facilmente em Scala e Java com suporte à criação de primeira classe para IntelliSense, autoformatação, verificação de erro etc.</li><li>Teste o aplicativo do Spark hello localmente.</li><li>Cluster do Spark tooHDInsight trabalhos de enviar e recuperar resultados de saudação.</li><li>Faça logon no tooAzure e acessar todos os clusters do Spark Olá associados às suas assinaturas do Azure.</li><li>Navegue todos os recursos de armazenamento Olá associado do cluster HDInsight Spark.</li></ul> |Ferramentas |Spark |N/D |

A partir desta versão, alteramos política aplicação de patch de sistema operacional do convidado de saudação para clusters HDInsight baseados em Linux. meta de saudação da nova política de saudação é toosignificantly reduzir o número de saudação de reinicializações toopatching vencimento. Olá nova política patches máquinas virtuais (VMs) no Linux clusters toda segunda-feira ou quinta-feira, começando em 12: 00 UTC em uma sobreposição entre nós em qualquer cluster específico. No entanto, qualquer determinada VM reinicia apenas no máximo uma vez a cada 30 dias, devido a aplicação de patch tooguest sistema operacional. Além disso, a primeira reinicialização Olá para um cluster recém-criado não acontece mais 30 dias a partir da data de criação de cluster hello.

> [!NOTE]
> Essas alterações só se aplicam a toonewly criada clusters igual ou maior que esta versão.
>
>

## <a name="notes-for-06062016-release-of-hdinsight"></a>Notas da versão de 06/06/2016 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

| HDP | Versão do HDI | Versão do Spark | Número de build do Ambari | Número de build do HDP |
| --- | --- | --- | --- | --- |
| 2.3 |3.3.1000.0.7702215 |1.5.2 |2.2.1.8-2 |2.3.3.1-18 |
| 2.4 |3.4.1000.0.7702224 |1.6.1 |2.2.1.8-2 |2.4.2.0 |

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Spark, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| Spark no HDInsight está disponível de forma geral |Essa versão traz aprimoramentos na disponibilidade, escalabilidade e fonte de tooopen produtividade Apache Spark no HDInsight. <ul><li>SLA líder do setor com 99,9% de disponibilidade, o que o torna adequado para cargas de trabalho corporativas exigentes.</li><li>Camada de armazenamento escalonável usando o Azure Data Lake Store.</li><li>Ferramentas de produtividade para todas as fases de desenvolvimento e a exploração de dados. Os notebooks Jupyter com kernel Spark personalizado permitem a exploração de dados interativa, a integração a painéis de BI como Power BI, Tableau e Qlik é boa para o compartilhamento de dados rápido e relatórios contínuos, o plug-in IntelliJ é uma opção confiável para o desenvolvimento e depuração de artefato de código de longo prazo.</li></ul> |O Barramento de |Spark |N/D |
| Ferramentas do HDInsight para IntelliJ |Este é um plug-in IntelliJ IDEA para clusters HDInsight Spark. Ele permite Olá recursos a seguir:<ul><li>Crie e escreva um aplicativo Spark facilmente em Scala e Java com suporte à criação de primeira classe para IntelliSense, autoformatação, verificação de erro etc.</li><li>Teste o aplicativo do Spark hello localmente.</li><li>Cluster do Spark tooHDInsight trabalhos de enviar e recuperar resultados de saudação.</li><li>Faça logon no tooAzure e acessar todos os clusters do Spark Olá associados às suas assinaturas do Azure.</li><li>Navegue todos os recursos de armazenamento Olá associado do cluster HDInsight Spark.</li><li>Navegue todas Olá trabalhos trabalho e o histórico informações para seu cluster HDInsight Spark.</li><li>Depure os trabalhos Spark remotamente pelo computador desktop.</li></ul> |Ferramentas |Spark |N/D |

## <a name="notes-for-05132016-release-of-hdinsight"></a>Notas da versão de 13/05/2016 do HDInsight 3.1
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - inalterado)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - inalterado)
* HDInsight    (Windows)         3.1.4.922.2266903  (HDP 2.1.15.0-2374 - inalterado)
* HDInsight    (Windows)        3.2.7.922.2266903  (HDP 2.2.9.1-11)
* HDInsight (Windows)        3.3.0.922.2266903  (HDP 2.3.3.1-18)
* HDInsight    (Linux)            3.2.1000.0.7565644   (HDP    2.2.9.1-11)
* HDInsight (Linux)            3.3.1000.0.7565644   (HDP 2.3.3.1-18)
* HDInsight (Linux)            3.4.1000.0.7548380   (HDP 2.4.2.0)

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Spark, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| Atualização de versão do Spark e outras correções de bug |Esta versão atualiza a versão do hello Spark no HDInsight cluster too1.6.1 e correções de bugs de outros |O Barramento de |Spark |N/D |

## <a name="notes-for-04112016-release-of-hdinsight"></a>Notas da versão de 11/04/2016 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight    (Windows)         2.1.10.889.2191206 (HDP 1.3.12.0-01795 - inalterado)
* HDInsight    (Windows)         3.0.6.889.2191206 (HDP 2.0.13.0-2117 - inalterado)
* HDInsight    (Windows)         3.1.4.889.2191206  (HDP 2.1.15.0-2374 - inalterado)
* HDInsight    (Windows)        3.2.7.889.2191206  (HDP 2.2.9.1-10)
* HDInsight (Windows)        3.3.0.889.2191206  (HDP 2.3.3.1-16 -inalterado)
* HDInsight    (Linux)            3.2.1000.0.7339916   (HDP 2.2.9.1-10)
* HDInsight (Linux)            3.3.1000.0.7339916   (HDP 2.3.3.1-16)
* HDInsight (Linux)            3.4.1000.0.7338911   (HDP 2.4.1.1-3)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| Problemas de atualização de metastore personalizado do HDI 3.4 |A criação de cluster falhará se você tiver usado um metastore personalizado, que foi usado anteriormente em uma versão inferior de outro cluster HDInsight. Isso foi devido a erro script de atualização tooan que agora foram corrigido |Criação do cluster |Todos |N/D |
| Recuperação de pane do Livy |Fornece resiliência de status do trabalho para qualquer trabalho enviado por meio do Livy |Confiabilidade |Spark no Linux |N/D |
| HA de conteúdo do Jupyter |Fornece Olá capacidade toosave e carga Jupyter notebook conteúdo tooand da conta de armazenamento Olá associada Olá cluster. Para saber mais, confira [Kernels disponíveis para notebooks Jupyter](hdinsight-apache-spark-jupyter-notebook-kernels.md). |Blocos de anotações |Spark no Linux |N/D  |
| Remoção de hiveContext de Jupyter Notebooks |Use a mágica `%%sql` no lugar da mágica `%%hive`. SqlContext é toohiveContext equivalente. Para saber mais, confira [Kernels disponíveis para notebooks Jupyter](hdinsight-apache-spark-jupyter-notebook-kernels.md) |Blocos de anotações |Clusters do Spark no Linux |N/D |
| Substituição de versões mais antigas do Spark |A versão mais antiga Spark 1.3.1 foi removido do serviço de saudação em 5/31 |O Barramento de |Clusters do Spark no Windows |N/D |

## <a name="notes-for-03292016-release-of-hdinsight"></a>Notas da versão de 29/03/2016 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - inalterado)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - inalterado)
* HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - unchanged)
* HDInsight (Windows)       3.2.7.875.2159884  (HDP 2.2.9.1-7 – inalterado)
* HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)
* HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - inalterado)
* HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - inalterado)
* HDInsight (Linux)            3.4.1000.0.7195842   (HDP 2.4.1.0-327)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| Versão do HDInsight 3.4 adicionada e versões atualizadas do HDP para todos os clusters do HDInsight |Com esta versão, adicionamos o HDInsight v3.4 (baseado no HDP 2.4) e também atualizamos outras versões do HDP. As notas de versão do HDP 2.4 estão disponíveis [aqui](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html) e mais informações sobre versões do HDInsight podem ser encontradas [aqui](hdinsight-component-versioning.md). |O Barramento de |Todos os clusters do Linux |N/D |
| HDInsight Premium |O HDInsight agora está disponível em duas categorias - Standard e Premium. O HDInsight Premium está atualmente em Preview e disponível apenas para os clusters Hadoop e Spark no Linux. Para saber mais, clique [aqui](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium). |O Barramento de |Hadoop e Spark no Linux |N/D |
| Servidor R da Microsoft |O HDInsight Premium fornece o Servidor R da Microsoft, que pode ser incluído nos clusters Hadoop e Spark no Linux. Para obter mais informações, consulte [Visão geral do R Server no HDInsight](hdinsight-hadoop-r-server-overview.md). |O Barramento de |Hadoop e Spark no Linux |N/D |
| Spark 1.6.0 |Os clusters do HDInsight 3.4 agora incluem o Spark 1.6.0 |O Barramento de |Clusters do Spark no Linux |N/D |
| Aprimoramentos do Bloco de notas Jupyter |Os blocos de notas Jupyter disponíveis com os clusters do Spark agora fornecem kernels adicionais do Spark. Eles também incluem aprimoramentos, como o uso de %%magic, a visualização automática e a integração com bibliotecas de visualização do Python (como matplotlib). Para saber mais, confira [Kernels disponíveis para notebooks Jupyter](hdinsight-apache-spark-jupyter-notebook-kernels.md). |O Barramento de |Clusters do Spark no Linux |N/D |

## <a name="notes-for-03222016-release-of-hdinsight"></a>Notas da versão de 22/03/2016 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight    (Windows)         2.1.10.875.2159884 (HDP 1.3.12.0-01795 - inalterado)
* HDInsight    (Windows)         3.0.6.875.2159884 (HDP 2.0.13.0-2117 - inalterado)
* HDInsight    (Windows)         3.1.4.875.2159884  (HDP 2.1.15.0-2374 - unchanged)
* HDInsight (Windows)       3.2.7.875.2159884  (HDP 2.2.9.1-7 – inalterado)
* HDInsight (Windows)        3.3.0.875.2159884  (HDP 2.3.3.1-16)
* HDInsight    (Linux)            3.2.1000.0.7193255   (HDP    2.2.9.1-8 - inalterado)
* HDInsight (Linux)            3.3.1000.0.7193255   (HDP 2.3.3.1-7 - inalterado)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| Versões atualizadas do HDInsight para todos os clusters de HDInsight |Com essa versão, atualizamos as versões do HDInsight para todos os clusters HDInsight |O Barramento de |Todos |N/D |

## <a name="notes-for-03102016-release-of-hdinsight"></a>Notas da versão de 10/03/2016 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight    (Windows)         2.1.10.859.2123216 (HDP 1.3.12.0-01795 - inalterado)
* HDInsight    (Windows)         3.0.6.859.2123216 (HDP 2.0.13.0-2117 - inalterado)
* HDInsight    (Windows)         3.1.4.859.2123216  (HDP 2.1.15.0-2374 - inalterado)
* HDInsight    (Windows)        3.2.7.859.2123216  (HDP 2.2.9.1-7)
* HDInsight (Windows)        3.3.0.859.2123216  (HDP 2.3.3.1-5 - inalterado)
* HDInsight    (Linux)            3.2.1000.7076817   (HDP    2.2.9.1-8)
* HDInsight (Linux)            3.3.1000.7076817   (HDP 2.3.3.1-7)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| Versões atualizadas do HDInsight para todos os clusters de HDInsight |Com essa versão, atualizamos as versões do HDInsight para todos os clusters HDInsight |O Barramento de |Todos |N/D |

## <a name="notes-for-01272016-release-of-hdinsight"></a>Notas da versão de 27/01/2016 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight    (Windows)         2.1.10.817.2028315 (HDP 1.3.12.0-01795 - inalterado)
* HDInsight    (Windows)         3.0.6.817.2028315 (HDP 2.0.13.0-2117 - inalterado)
* HDInsight    (Windows)         3.1.4.817.2028315  (HDP 2.1.15.0-2374 - inalterado)
* HDInsight    (Windows)        3.2.7.817.2028315  (HDP 2.2.9.1-1)
* HDInsight (Windows)        3.3.0.817.2028315  (HDP 2.3.3.1-5 - inalterado)
* HDInsight    (Linux)            3.2.1000.4072335   (HDP    2.2.9.1-1)
* HDInsight (Linux)            3.3.1000.4072335   (HDP 2.3.3.1-1)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| Versões atualizadas do HDInsight para todos os clusters de HDInsight |Com essa versão, atualizamos as versões do HDInsight para todos os clusters HDInsight |O Barramento de |Todos |N/D |

## <a name="notes-for-12022015-release-of-hdinsight"></a>Notas da versão de 02/12/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight    (Windows)         2.1.10.763.1931434 (HDP 1.3.12.0-01795 - inalterado)
* HDInsight    (Windows)         3.0.6.763.1931434 (HDP 2.0.13.0-2117 - inalterado)
* HDInsight    (Windows)         3.1.4.763.1931434  (HDP 2.1.15.0-2374 - inalterado)
* HDInsight    (Windows)        3.2.7.763.1931434  (HDP 2.2.7.1-34 - inalterado)
* HDInsight (Windows)        3.3.1000.0           (HDP 2.3.3.1-5)
* HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34 - inalterado)
* HDInsight (Linux)            3.3.1000.0           (HDP 2.3.3.0-3039)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| Versão do HDInsight 3.3 adicionada e versões atualizadas do HDP para todos os clusters do HDInsight |Com esta versão, adicionamos o HDInsight v3.3 (baseado no HDP 2.3) e também atualizamos outras versões do HDP. As notas de versão do HDP 2.3 estão disponíveis [aqui](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html) e mais informações sobre versões do HDInsight podem ser encontradas [aqui](hdinsight-component-versioning.md). |O Barramento de |Todos |N/D |

## <a name="notes-for-11302015-release-of-hdinsight"></a>Notas da versão de 30/11/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight    (Windows)         2.1.10.757.1923908 (HDP 1.3.12.0-01795 - inalterado)
* HDInsight    (Windows)         3.0.6.757.1923908  (HDP 2.0.13.0-2117 - inalterado)
* HDInsight    (Windows)         3.1.4.757.1923908  (HDP 2.1.15.0-2374 - inalterado)
* HDInsight    (Windows)        3.2.7.757.1923908  (HDP 2.2.7.1-34)
* HDInsight    (Linux)            3.2.1000.0.6392801 (HDP    2.2.7.1-34)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| Versões atualizadas do HDInsight para todos os clusters HDInsight e versões do HDP para clusters HDInsight 3.2 (Windows e Linux) |Com esta versão, as versões do HDInsight e do HDP foram atualizadas |O Barramento de |Todos |N/D |

## <a name="notes-for-10272015-release-of-hdinsight"></a>Notas da versão de 27/10/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight    (Windows)         2.1.10.726.1866228 (HDP 1.3.12.0-01795 - inalterado)
* HDInsight    (Windows)         3.0.6.726.1866228  (HDP 2.0.13.0-2117 - inalterado)
* HDInsight    (Windows)         3.1.4.726.1866228  (HDP 2.1.15.0-2374 - inalterado)
* HDInsight    (Windows)        3.2.7.726.1866228  (HDP 2.2.7.1-33)
* HDInsight    (Linux)            3.2.1000.0.6035701 (HDP    2.2.7.1-33)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| Versões atualizadas do HDInsight para todos os clusters HDInsight (Windows e Linux) |Com esta versão, as versões do HDInsight e do HDP foram atualizadas |O Barramento de |Todos |N/D |
| Jupyter corrigido para clusters Spark do Windows com clusters de letras maiúsculas |Clusters que tiveram os nomes DNS especificados em letras maiusculas tem problemas com blocos de anotações do Jupyter devido tooan seleção de solicitação de origem. correção de saudação foi toochange Olá nome DNS caso de toolower de configuração do Jupyter. |O Barramento de |HDInsight Spark (Windows) |N/D |

## <a name="notes-for-10202015-release-of-hdinsight"></a>Notas da versão de 20/10/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.716.1846990 (Windows)    (HDP 1.3.12.0-01795 – inalterado)
* HDInsight     3.0.6.716.1846990 (Windows)      (HDP 2.0.13.0-2117 - inalterado)
* HDInsight     3.1.4.716.1846990 (Windows)      (HDP 2.1.16.0-2374)
* HDInsight        3.2.7.716.1846990 (Windows)      (HDP 2.2.7.1-0004)
* HDInsight        3.2.1000.0.5930166 (Linux)        (HDP 2.2.7.1-0004)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| TooHDP de versão alterado do padrão HDP 2.2 |versão do padrão de saudação para clusters de HDInsight Windows é alterado tooHDP 2.2. O HDInsight versão 3.2 (HDP 2.2) está disponível desde fevereiro de 2015. Essa alteração só inverte a versão de cluster padrão hello, quando uma seleção explícita não é feita durante o provisionamento de cluster hello usando Olá portal do Azure, cmdlets do PowerShell ou Olá SDK. |O Barramento de |Todos |N/D |
| Alterações no formato de nome de VM para a implantação de vários HDInsight em clusters Linux em uma única rede virtual |O suporte para a implantação de vários clusters HDInsight Linux em uma única rede virtual está sendo adicionado nesta versão. Como parte da atualização, o formato de saudação de nomes de máquina virtual no cluster Olá foi alterado do nó principal\*, workernode\* e zookeepernode\* toohn\*, baixo\*e zk\* respectivamente. Não é uma prática recomendada de tootake uma dependência direta no formato de saudação de nomes de máquina virtual, pois esse é o assunto toochange. Use "hostname -f" no computador local hello ou uma lista de saudação toodetermine Ambari APIs de hosts e mapeamento de saudação do toohosts de componentes. Você pode encontrar mais informações em [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md) e [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md). |O Barramento de |Clusters HDInsight no Linux |N/D |
| Alterações de configuração |Para clusters de HDInsight 3.1, Olá configurações a seguir agora está habilitado: <ul><li>tez.yarn.ats.enabled e yarn.log.server.url. Isso permite hello Application Server da linha do tempo e toobe Olá Log servidor capaz de tooserve out logs.</li></ul>Para clusters de HDInsight 3.2, Olá configurações a seguir foram modificada: <ul><li>foi definido MapReduce.fileoutputcommitter.Algorithm.Version too2. Isso permite o uso de versão V2 Olá Olá FileOutputCommitter.</li></ul> |O Barramento de |Todos |N/D |

## <a name="notes-for-09092015-release-of-hdinsight"></a>Notas da versão de 09/09/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.675.1768697 (HDP 1.3.12.0-01795 – inalterado)
* HDInsight     3.0.6.675.1768697  (HDP 2.0.13.0-2117 – inalterado)
* HDInsight     3.1.4.675.1768697  (HDP 2.1.15.0-2334 – inalterado)
* HDInsight        3.2.6.675.1768697  (HDP 2.2.6.1-0012 - inalterado)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| Versões atualizadas do HDInsight para todos os clusters de HDInsight |Com esta versão, as versões do HDInsight foram atualizadas |O Barramento de |Todos |N/D |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Notas da versão de 31/07/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight 2.1.10.640.1695824 (HDP 1.3.12.0-01795 – inalterado)
* HDInsight     3.0.6.640.1695824  (HDP 2.0.13.0-2117 – inalterado)
* HDInsight     3.1.4.640.1695824  (HDP 2.1.15.0-2334 – inalterado)
* HDInsight        3.2.6.640.1695824  (HDP 2.2.6.1-0012 - inalterado)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| Corrigir fluxo de trabalho de recriação de imagens de nó de cluster do Spark |Correção de bug que estava causando Spark toonot recuperação após a recriação de imagem de nós de cluster |O Barramento de |Spark |N/D |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Notas da versão de 31/07/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.635.1684502 (HDP 1.3.12.0-01795 – inalterado)
* HDInsight     3.0.6.635.1684502  (HDP 2.0.13.0-2117 – inalterado)
* HDInsight     3.1.4.635.1684502  (HDP 2.1.15.0-2334 – inalterado)
* HDInsight        3.2.6.635.1684502  (HDP 2.2.6.1-0012 - inalterado)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| Versões atualizadas do HDInsight para todos os clusters de HDInsight |Com esta versão, as versões do HDInsight foram atualizadas |O Barramento de |Todos |N/D |

## <a name="notes-for-07072015-release-of-hdinsight"></a>Notas da versão de 07/07/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.610.1630216    (HDP 1.3.12.0-01795 - inalterado)
* HDInsight     3.0.6.610.1630216    (HDP 2.0.13.0-2117 - inalterado)
* HDInsight     3.1.4.610.1630216    (HDP 2.1.15.0-2334 - inalterado)
* HDInsight        3.2.4.610.1630216    (HDP 2.2.6.1-0012)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

| Title | Descrição | Área afetada (por exemplo, serviço, componente ou SDK) | Tipo de cluster (por exemplo, Hadoop, HBase ou Storm) | JIRA (se aplicável) |
| --- | --- | --- | --- | --- |
| Atualizadas versões do HDP para clusters do HDInsight 3.2 |Com esta versão, o HDInsight 3.2 implanta o HDP 2.2.6.1-0012 |O Barramento de |Todos |N/D |

## <a name="notes-for-06262015-release-of-hdinsight"></a>Notas da versão de 26/06/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.601.1610731    (HDP 1.3.12.0-01795 - inalterado)
* HDInsight     3.0.6.601.1610731    (HDP 2.0.13.0-2117 - inalterado)
* HDInsight     3.1.4.601.1610731    (HDP 2.1.15.0-2334 - inalterado)
* HDInsight        3.2.4.601.1610731    (HDP 2.2.6.1-0011)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Área afetada (por exemplo, serviço, componente ou SDK)</p></th>
<th>Tipo de cluster (por exemplo, Hadoop, HBase ou Storm)</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>Atualizadas versões do HDP para clusters do HDInsight 3.2</td>
<td>Com esta versão, o HDInsight 3.2 implanta o HDP 2.2.6.1</td>
<td>O Barramento de</td>
<td>Todos</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-06182015-release-of-hdinsight"></a>Notas da versão de 18/6/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.596.1601657    (HDP 1.3.12.0-01795 - inalterado)
* HDInsight     3.0.6.596.1601657    (HDP 2.0.13.0-2117 - inalterado)
* HDInsight     3.1.4.596.1601657    (HDP 2.1.15.0-2334)
* HDInsight        3.2.4.596.1601657    (HDP 2.2.6.1-0002)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Área afetada (por exemplo, serviço, componente ou SDK)</p></th>
<th>Tipo de cluster (por exemplo, Hadoop, HBase ou Storm)</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>Portas HTTPS adicionais abertas</td>
<td>serviço de nuvem Olá agora abre too8005 8001 de 5 portas no cluster Olá ex.: em https://<clustername>.azurehdinsight.net:8001/. Solicitações toothese URLs são autenticados usando Olá mesmo mecanismo de senha de autenticação básica como a porta 443. Essas portas associar toohello a mesma porta em um nó principal ativa do hello. Ações de script podem ser usado toomake cliente serviços escutar nessas portas no cluster de saudação de toooutside de nó principal e rota de saudação.</td>
<td>Serviço de Nuvem</td>
<td>Todos</td>
<td>N/D</td>
</tr>
<tr>
<td>Problema intermitente de ordem aleatória do MapReduce para HDInsight 3.2</td>
<td>Correção de uma condição de corrida intermitente rara na ordem aleatória do MapReduce em clusters grandes, resultando em ocasionais falhas de tarefas. Confira <a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a> para obter mais informações.</td>
<td>Núcleo do Hadoop</td>
<td>Todos</td>
<td><a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE-6361</a></td>
</tr>
<tr>
<td>Mover tooLatest Java do Azure SDK 2.2 3.2 do HDInsight</td>
<td>Movido toolatest versão Olá SDK do Azure para Java usada pelo driver WASB hello. Olá, SDK mais recente tem algumas correções e notas de versão Olá Olá mesmo estão disponível em https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt.</td>
<td>Núcleo do Hadoop</td>
<td>Todos</td>
<td><a href="https://issues.apache.org/jira/browse/HADOOP-11959" target="_blank">HADOOP-11959</a></td>
</tr>
<tr>
<td>Mover tooHDP 2.1.15 para clusters de HDInsight 3.1</td>
<td>Hortonworks notas de versão para versão Olá estão disponíveis <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.15-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.15.html" target="_blank">aqui</a>.</td>
<td>HDP</td>
<td>Todos</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-06042015-release-of-hdinsight"></a>Notas da versão de 04/06/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.583.1575584    (HDP 1.3.12.0-01795 - inalterado)
* HDInsight     3.0.6.583.1575584    (HDP 2.0.13.0-2117 - inalterado)
* HDInsight     3.1.3.583.1575584    (HDP 2.1.12.1-0003 - inalterado)
* HDInsight        3.2.4.583.1575584    (HDP 2.2.6.1-1)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Área afetada (por exemplo, serviço, componente ou SDK)</p></th>
<th>Tipo de cluster (por exemplo, Hadoop, HBase ou Storm)</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>Correção para o erro 502 de gateway incorreto para clusters Storm</td>
<td>Esta versão corrige um bug que afetam a API de envio de trabalho Olá que causou Olá site toobe para baixo após uma reinicialização.</td>
<td>O Barramento de</td>
<td>Storm</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-06012015-release-of-hdinsight"></a>Notas da versão de 01/06/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.577.1563827    (HDP 1.3.12.0-01795 - inalterado)
* HDInsight     3.0.6.577.1563827    (HDP 2.0.13.0-2117 - inalterado)
* HDInsight     3.1.3.577.1563827    (HDP 2.1.12.1-0003 - inalterado))
* HDInsight        3.2.4.577.1563827    (HDP 2.2.6.0-2800 - inalterado)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Área afetada (por exemplo, serviço, componente ou SDK)</p></th>
<th>Tipo de cluster (por exemplo, Hadoop, HBase ou Storm)</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>Correções de vários bugs</td>
<td>Esta versão corrige bugs relacionadas toocluster provisionamento.</td>
<td>O Barramento de</td>
<td>Todos os tipos de cluster</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-05272015-release-of-hdinsight"></a>Notas da versão de 27/05/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight        3.2.4.570.1554102    (HDP 2.2.6.0-2800)
* Outras versões do cluster e o SDK não são implantados como parte desta versão.

Esta versão contém Olá atualizações a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Área afetada (por exemplo, serviço, componente ou SDK)</p></th>
<th>Tipo de cluster (por exemplo, Hadoop, HBase ou Storm)</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>Atualização do HDP 2.2</td>
<td>Esta versão do HDInsight 3.2 contém HDP 2.2.6 e traz tooHDInsight de várias correções de bugs importantes. Olá completo notas de versão estão disponíveis em <a href="http://dev.hortonworks.com.s3.amazonaws.com/HDPDocuments/HDP2/HDP-2.2.6/HDP_RelNotes_v226/index.html">HDP 2.2.6 notas de versão</a>.</td>
<td>HDP</td>
<td>Todos os tipos de cluster</td>
<td>N/D</td>
</tr>
<tr>
<td>Alterar tooDefault Yarn configuração de memória de contêiner</td>
<td>Nesta atualização, o saudação padrão memória disponível tooYARN contêineres (yarn.nodemanager.resource.memory mb e yarn.scheduler.maximum de alocação de mb), iniciado pelo Gerenciador de nó, é too5632MB maior. Anteriormente foi reduzido too4608MB, mas com base nas várias execuções de trabalho, o novo valor de saudação deve oferecer melhor desempenho e confiabilidade toomost trabalhos, portanto, é melhor padrão. Como de costume, se você tiver dependência crítica nesta configuração de memória, configurá-lo explicitamente ao criar o cluster de saudação.</td>
<td>HDP</td>
<td>Todos os tipos de cluster</td>
<td>N/D</td>
</tr>
<tr>
<td>Paridade de configuração padrão para clusters HBase e Storm</td>
<td>Essa atualização restaura Hbase e Storm clusters toouse Olá os mesmos valores das configurações YARN clusters Hadoop. Isso é feito para fins de paridade entre todos os tipos de cluster.</td>
<td>HDP</td>
<td>HBase, Storm</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-05202015-release-of-hdinsight"></a>Notas da versão de 20/05/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.564.1542093    (HDP 1.3.12.0-01795 - inalterado)
* HDInsight     3.0.6.564.1542093    (HDP 2.0.13.0-2117 - inalterado)
* HDInsight     3.1.3.564.1542093    (HDP 2.1.12.1-0003)
* HDInsight        3.2.4.564.1542093    (HDP 2.2.4.6-2)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Área afetada (por exemplo, serviço, componente ou SDK)</p></th>
<th>Tipo de cluster (por exemplo, Hadoop, HBase ou Storm)</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>Suporte a EventHub do SCP.NET</td>
<td>pacotes de cluster Olá atualizado para HDInsight Storm trazem novos tooSCP.NET de recursos. Agora você tem acesso toonew APIs no construtor de topologia que tornam mais fácil toouse EventHubSpout ou Spouts de Java. Você deve atualizar seu toowork SDK de cliente SCP.NET com novos clusters como contratos Olá foram atualizados. Para obter detalhes sobre Olá novas APIs, uso e notas de versão (incluindo correções de bugs) consulte toohello arquivo Leiame incluído no hello pacote NuGet SCP.NET.</td>
<td>Ferramentas do VS</td>
<td>Clusters do Storm HDInsight 3.2</td>
<td>N/D</td>
</tr>
<tr>
<td>Atualização de driver JDBC</td>
<td>Versão atualizada Olá toohello de driver do SQL Server com suporte no sqljdbc_4.1.5605.100.</td>
<td>Metastore</td>
<td>Todos</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-04272015-release-of-hdinsight"></a>Notas da versão de 27/04/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.537.1486660    (HDP 1.3.12.0-01795 - inalterado)
* HDInsight     3.0.6.537.1486660    (HDP 2.0.13.0-2117 - inalterado)
* HDInsight     3.1.3.537.1486660    (HDP 2.1.12.0-2329 - inalterado)
* HDInsight        3.2.3.537.1486660    (HDP 2.2.2.2-4)
* SDK            1.5.8

Esta versão contém Olá atualizações a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Área afetada (por exemplo, serviço, componente ou SDK)</p></th>
<th>Tipo de cluster (por exemplo, Hadoop, HBase ou Storm)</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>Corrigir a dependência de DLL</td>
<td>Remove a dependência de HDInsight na estrutura de teste de unidade.</td>
<td>.</td>
<td>O Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Correção de bug para condição de corrida</td>
<td>Um cluster de criar a solicitação agora esperas em PUT solicitação toobe aceito antes de sondar o status de saudação</td>
<td>.</td>
<td>O Hadoop</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-04142015-release-of-hdinsight"></a>Notas da versão de 14/04/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - inalterado)
* HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - inalterado)
* HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - inalterado)
* HDInsight        3.2.3.525.1459730    (HDP 2.2.2.2-2)
* SDK            1.5.6

Esta versão contém Olá atualizações a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Área afetada (por exemplo, serviço, componente ou SDK)</p></th>
<th>Tipo de cluster (por exemplo, Hadoop, HBase ou Storm)</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>Correções de bug Tez</td>
<td>Correções para Apache TEZ 2214 e TEZ 1923 estão incluídas nesta versão do HDI 3.2. Isso é necessário para determinadas consultas de Hive no Tez que exigem tooshuffle uma quantidade significativa de dados.
</td>
<td>HDP</td>
<td>O Hadoop</td>
<td><a href="https://issues.apache.org/jira/browse/TEZ-2214">TEZ 2214</a></br><a href="https://issues.apache.org/jira/browse/TEZ-1923">TEZ 1923</a></td>
</tr>
</table>

## <a name="notes-for-04062015-release-of-hdinsight"></a>Notas da versão de 06/04/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.521.1453250    (HDP 1.3.12.0-01795 - inalterado)
* HDInsight     3.0.6.521.1453250    (HDP 2.0.13.0-2117 - inalterado)
* HDInsight     3.1.3.521.1453250    (HDP 2.1.12.0-2329 - inalterado)
* HDInsight        3.2.3.521.1453250    (HDP 2.2.2.2-1)
* SDK            1.5.6

Esta versão contém Olá atualizações a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Área afetada (por exemplo, serviço, componente ou SDK)</p></th>
<th>Tipo de cluster (por exemplo, Hadoop, HBase ou Storm)</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>SDK 1.5.6 do .NET do HDInsight</td>
<td>Atualizações tooremove algumas classes internas para HDInsight no Linux.</td>
<td>.</td>
<td>O Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Biblioteca de Avro 1.5.6</td>
<td>Adição de <b>KnownTypeAttribute</b> para o método <b>GetAllKnownTypes</b>. Corrigida NullReferenceException quando um tipo é null para o método GetAllKnownTypes.</td>
<td>.</td>
<td>O Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Correções de bug</td>
<td>Serviço de toohello várias correções de bugs</td>
<td>O Barramento de</td>
<td>Todos</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-04012015-release-of-hdinsight"></a>Notas da versão de 01/04/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.513.1431705    (HDP 1.3.12.0-01795)
* HDInsight     3.0.6.513.1431705    (HDP 2.0.13.0-2117)
* HDInsight     3.1.3.513.1431705    (HDP 2.1.12.0-2329)
* HDInsight        3.2.3.513.1431705    (HDP 2.2.2.1-2600)
* SDK            1.5.5

Esta versão contém Olá atualizações a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Área afetada (por exemplo, serviço, componente ou SDK)</p></th>
<th>Tipo de cluster (por exemplo, Hadoop, HBase ou Storm)</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>Capacidade tooenable/desabilitar credenciais remotas de área de trabalho em clusters do Windows por meio do SDK do .NET</td>
<td>Suporte programático para habilitar ou desabilitar as credenciais RDP em clusters do Windows.</td>
<td>.</td>
<td>Todos</td>
<td>N/D</td>
</tr>
<tr>
<td>Capacidade tooenable credenciais remotas de área de trabalho em clusters, enquanto eles estão sendo provisionados.</td>
<td>Suporte para habilitar credenciais da área de trabalho remota, como cluster hello está sendo criado. Isso remove o processo de duas etapas Olá para o primeiro cluster Olá provisionamento e, em seguida, habilitar a área de trabalho remota.</td>
<td>.</td>
<td>Todos</td>
<td>N/D</td>
</tr>
<tr>
<td>Too2.7.8 Python atualizado</td>
<td>Correções de Python atualizado em Clusters de HDInsight tooPython 2.7.8, que contém algum de segurança importante para as versões 2.1, 3.0, 3.1 e 3.2 do HDInsight</td>
<td>O Barramento de</td>
<td>Todos</td>
<td>N/D</td>
</tr>
<tr>
<td>Alteração de configuração do YARN</td>
<td>Alterado YARN aplicativos concluída yarn.resourcemanager.max de configuração em too1000 para todos os tipos de cluster para as versões 3.1 e 3.2 do HDInsight. Esse valor controla somente a lista de saudação de aplicativos concluídos em Olá YARN da interface do usuário. tooget informações sobre os aplicativos que foram enviadas toohello anterior lista mostrada na saudação da interface do usuário, você pode ir diretamente toohello histórico de servidor de aplicativos.</td>
<td>YARN</td>
<td>Todos</td>
<td>N/D</td>
</tr>
<tr>
<td>Redimensionamento de nós em um cluster HBase</td>
<td>Clusters HBase permitem redimensionamento de nós (aumento e redução) para as versões 3.1 e 3.2 do HDInsight</td>
<td>O Barramento de</td>
<td>hbase</td>
<td>N/D</td>
</tr>
<tr>
<td>Atualização do JDBC</td>
<td>Driver SQL JDBC é sqljdbc_4.0.2206.100 tooversion atualizado para a versão 3.2 do HDInsight. Essa versão contém aprimoramentos de segurança importantes.</td>
<td>HDP</td>
<td>Todos</td>
<td>N/D</td>
</tr>
<tr>
<td>Atualização da configuração da JVM</td>
<td>Atualizado JVM configuração networkaddress.cache.ttl too300 segundos do valor de padrão de saudação de -1 para as versões 3.1 e 3.2 do HDInsight. Esse valor de configuração controla Olá política para pesquisas de nome bem-sucedida saudação do serviço de nomes de cache. Esse procedimento corrige um bug toogrowing e redução de clusters HBase relacionados.</td>
<td>O Barramento de</td>
<td>hbase</td>
<td>N/D</td>
</tr>
<tr>
<td>Atualizar tooAzure Storage SDK para Java 2.0</td>
<td>Versão 3.2 do HDInsight é toouse atualizado hello mais recente da saudação SDK de armazenamento do Azure para Java. Contém várias correções de bugs importantes sobre a versão de hello 0.6.0 atual.</td>
<td>HDP</td>
<td>Todos</td>
<td>N/D</td>
</tr>
<tr>
<td>Código-fonte WASB tooApache atualizado</td>
<td>Versão 3.2 agora usa Olá código mais recente para o driver de sistema de arquivos WASB de saudação do Apache Hadoop de HDInsight. Com essa alteração, o driver WASB Olá agora é empacotado como um jar separado. Isso é apenas uma alteração de empacotamento e não contém qualquer toobehavior alterações do driver WASB hello. nome de saudação do arquivo JAR é hadoop-azure-2.6.0.jar.</td>
<td>HDP</td>
<td>Todos</td>
<td>N/D</td>
</tr>
<tr>
<td>Atualizações de nome de arquivo JAR no HDInsight 3.2</td>
<td>Esta versão de atualização tooHDInsight 3.2 contém várias correções de bugs e alguns jars internos fornecidos como parte do HDP foram atualizados. Esses pacotes HDP JAR arquivosestiverem toohello interno e não para uso direto por aplicativos cliente. Aplicativos devem empacotar sua própria versão do hello JARs para que uma atualização toohello JARs HDP interno não interrompem os aplicativos cliente.</td>
<td>HDP</td>
<td>Todos</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-03032015-release-of-hdinsight"></a>Notas da versão de 03/03/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.488.1375841    (HDP 1.3.9.0-01351 - inalterado)
* HDInsight     3.0.6.488.1375841    (HDP 2.0.9.0-2097 -  inalterado)
* HDInsight     3.1.3.488.1375841    (HDP 2.1.10.0-2290 - inalterado)
* HDInsight        3.2.3.488.1375841    (HDP-2.2.10.0-2340 - inalterado)
* SDK            1.5.0                (inalterado)

Esta versão contém Olá atualização a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Área afetada (por exemplo, serviço, componente ou SDK)</p></th>
<th>Tipo de cluster (por exemplo, Hadoop, HBase ou Storm)</th>
<th>JIRA</th>
</tr>
<tr>
<td>Aprimoramentos de confiabilidade</td>
<td>Fizemos correções que permitem a melhor com o aumento de carga com respeito toocluster criação Olá Olá serviço tooscale.</td>
<td>O Barramento de</td>
<td>Todos</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-02182015-release-of-hdinsight"></a>Notas da versão de 18/02/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.471.1342507    (HDP 1.3.9.0-01351 - inalterado)
* HDInsight     3.0.6.471.1342507    (HDP 2.0.9.0-2097 -  inalterado)
* HDInsight     3.1.3.471.1342507    (HDP 2.1.10.0-2290 - inalterado)
* HDInsight        3.2.3.471.1342507    (HDP-2.2.10.0-2340)
* SDK            1.5.0

Esta versão contém Olá atualizações a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Área afetada (por exemplo, serviço, componente ou SDK)</p></th>
<th>Tipo de cluster (por exemplo, Hadoop, HBase ou Storm)</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>Clusters do HDInsight 3.2</td>
<td>O Hadoop 2.6/HDP2.2 está disponível com clusters do HDInsight 3.2. Ele contém tooall grandes atualizações de componentes de código-fonte aberto hello. Para obter mais informações, veja Novidades no HDInsight e as <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html" target="_blank">Notas de versão do HDP 2.2.0.0</a>.</td>
<td>Software livre</td>
<td>Todos</td>
<td>N/D </td>
</tr>
<tr>
<td>HDInsight no Linux (Visualização)</td>
<td>Clusters podem ser implantados em execução no Ubuntu Linux. Para saber mais, confira Introdução ao HDInsight no Linux.</td>
<td>O Barramento de</td>
<td>O Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Disponibilidade geral do Storm</td>
<td>Clusters do Apache tempestade estão geralmente disponíveis. Para saber mais, veja Introdução ao uso do Storm no HDInsight.</td>
<td>O Barramento de</td>
<td>Storm</td>
<td>N/D</td>
</tr>
<tr>
<td>Tamanhos de máquina virtual</td>
<td>HDInsight do Azure está disponível em mais tipos e tamanhos de máquina virtual. HDInsight pode utilizar A2 tooA7 tamanhos criados para fins gerais; Nós D-Series que apresentam unidades de estado sólido (SSDs) e processadores mais rápidos de 60 por cento; e suportam a tamanhos A8 e A9 com InfiniBand de rede rápida.</td>
<td>O Barramento de</td>
<td>Todos</td>
<td>N/D</td>
</tr>
<tr>
<td>Dimensionamento de cluster</td>
<td>Você pode alterar o número de saudação de nós de dados para um cluster HDInsight em execução sem ter que toodelete ou recriá-la. Atualmente, apenas tipos de cluster Hadoop consulta e Apache Storm tenham essa capacidade, mas há suporte para o tipo de cluster HBase Apache em breve toofollow. Para saber mais, veja Gerenciar clusters HDInsight.</td>
<td>O Barramento de</td>
<td>Hadoop, Storm</td>
<td>N/D</td>
</tr>
<tr>
<td>Ferramentas do Visual Studio</td>
<td>Além disso toocomplete ferramentas para Apache Storm, Olá ferramentas para Apache Hive no Visual Studio foi atualizada tooinclude conclusão de instrução, validação e suporte aprimorado de depuração. Para saber mais, veja Introdução às ferramentas do Hadoop HDInsight para o Visual Studio.</td>
<td>Ferramentas</td>
<td>O Hadoop</td>
<td>N/D </td>
</tr>
<td>Conector de Hadoop para BD Cosmos do Azure</td>
<td>Com o conector de Hadoop para BD Cosmos do Azure, você pode executar agregações complexas, análise e manipulações de seus documentos JSON sem esquema armazenados nas coleções de BD Cosmos do Azure ou entre contas de banco de dados. Para saber mais e obter um tutorial, veja Executar trabalhos do Hadoop usando o BD Cosmos do Azure e o HDInsight.</td>
<td>O Barramento de</td>
<td>O Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Correções de bug</td>
<td>Fizemos várias correções de bug secundárias para serviços HDInsight. Não se espera nenhuma alteração no comportamento voltado ao cliente.</td>
<td>O Barramento de</td>
<td>Todos</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-02062015-release-of-hdinsight"></a>Notas da versão de 06/02/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.463.1325367    (HDP 1.3.9.0-01351 - inalterado)
* HDInsight     3.0.6.463.1325367    (HDP 2.0.9.0-2097 -  inalterado)
* HDInsight     3.1.2.463.1325367    (HDP 2.1.10.0-2290)
* SDK            N/D

Esta versão contém Olá atualizações a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Área afetada (por exemplo, serviço, componente ou SDK)</p></th>
<th>Tipo de cluster (por exemplo, Hadoop, HBase ou Storm)</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>Correções de bug</td>
<td>Fizemos várias correções de bug secundárias para serviços HDInsight. Não se espera nenhuma alteração no comportamento voltado ao cliente.</td>
<td>O Barramento de</td>
<td>Todos</td>
<td>N/D</td>
</tr>
<tr>
<td>Atualização de manutenção HDP 2.1</td>
<td>HDInsight 3.1 é atualizada toodeploy HDP 2.1.10.0. Para obter mais informações, confira <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.10/bk_releasenotes_hdp_2.1/content/ch_relnotes-HDP-2.1.10.html" target="_blank">Notas de versão do HDP-2.1.10</a>. </td>
<td>Software livre</td>
<td>Todos</td>
<td>N/D</td>
</tr>
<tr>
<td>Atualizações binárias HDP</td>
<td>Existem alguns arquivos JAR no HBase para os quais os nomes de arquivo foram atualizados. Esses arquivos JAR são usados internamente pelo HBase, portanto não é esperado que os clientes têm uma dependência em nomes de saudação desses arquivos JAR. Estão incluídos:
<ul>
<li>./lib/jetty-6.1.26.hwx.jar</li>
<li>./lib/jetty-sslengine-6.1.26.hwx.jar</li>
<li>./lib/jetty-util-6.1.26.hwx.jar</li>
</ul>
</td>
<td>Software livre</td>
<td>HBase</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-1292015-release-of-hdinsight"></a>Notas da versão de 29/01/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.455.1309616    (HDP 1.3.9.0-01351 - inalterado)
* HDInsight     3.0.6.455.1309616    (HDP 2.0.9.0-2097 -  inalterado)
* HDInsight     3.1.2.455.1309616    (HDP 2.1.9.0-2196 -  inalterado)
* SDK            N/D

Esta versão contém Olá atualização a seguir:

<table border="1">

<tr>
<th>Title</th>
<th>Descrição</th>
<th>Área afetada (por exemplo, serviço, componente ou SDK)</p></th>
<th>Tipo de cluster (por exemplo, Hadoop, HBase ou Storm)</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>Correções de bug</td>
<td>Fizemos algumas correções de bugs importantes que melhoram a confiabilidade de saudação do hello Clusters HDInsight durante as atualizações do Azure.</td>
<td>O Barramento de</td>
<td>Todos</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-152015-release-of-hdinsight"></a>Notas da versão de 05/01/2015 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão:

* HDInsight     2.1.10.420.1246118    (HDP 1.3.9.0-01351 - inalterado)
* HDInsight     3.0.6.420.1246118    (HDP 2.0.9.0-2097 - inalterado)
* HDInsight     3.1.2.420.1246118    (HDP 2.1.9.0-2196 - inalterado)

Esta versão contém Olá atualizações a seguir:

<table border="1">

<tr>
<th>Title</th>
<th>Descrição</th>
<th>Componente</th>
<th>Tipo de cluster</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>Exemplos para análise de tendência do Twitter e recomendações de vídeos baseadas no Mahout</td>
<td><p>Nesta versão, a saudação console de consulta de HDInsight tem dois exemplos adicionais:</p>

<p><b>Análise de Tendências do Twitter</b><br>
APIs públicas fornecidas por sites, como o Twitter, são uma fonte útil de dados para analisar e compreender as tendências populares. Neste tutorial, saiba como toouse Hive tooget uma lista de usuários do Twitter que enviou Olá tweets mais que contém uma palavra específica. </p>

<p><b>Recomendação de filme do Mahout</b><br>
O Apache Mahout é uma biblioteca de machine learning de Apache Hadoop. O Mahout contém algoritmos para processamento de dados (como filtragem, classificação e clustering). Neste tutorial, use uma recomendação mecanismo toogenerate filme as recomendações com base em filmes que viu seus amigos.</p></td>
<td>Console de consulta</td>
<td>O Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Alterar valor toodefault para a configuração do Hive: hive.auto.convert.join.noconditionaltask.size</td>
<td><p>Essa configuração de tamanho se aplica a junções de mapa tooautomatically convertido. valor de saudação representa a soma de saudação de tamanhos de saudação de tabelas que podem ser convertidos toohash mapas que cabem na memória. Em uma versão anterior, esse valor é aumentado de valor padrão de saudação de 10 MB too128 MB. No entanto, novo valor Olá de 128 MB estava causando trabalhos toofail toolack vencimento de memória. Esta versão reverte o valor padrão de saudação fazer too10 MB. Os clientes ainda podem escolher toooverride esse valor durante a criação do cluster, considerando suas consultas e tamanhos de tabela. Para obter mais informações sobre essa configuração e como toooverride, consulte <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.0.2/ds_Hive/optimize-joins.html#JoinOptimization-OptimizeAutoJoinConversion" target="_blank">otimizar a conversão de junção automática</a> na documentação de Hortonworks. </p></td>
<td>Hive</td>
<td>Hadoop, HBase</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-12232014-release-of-hdinsight"></a>Notas da versão de 23/12/2014 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão são:

* HDInsight     2.1.10.420.1246783    (HDP version inalterado)
* HDInsight     3.0.6.420.1246783    (HDP version inalterado)
* HDInsight     3.1.1.420.1246783    (HDP version inalterado)

Esta versão contém Olá atualização a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Componente</th>
<th>Tipo de cluster</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>Falhas na criação do cluster intermitentes devido a carga de tooexcessive</td>
<td><p>Algoritmo aprimorado para baixar os pacotes HDP durante a criação de cluster permite que mais robusto tratamento de falhas devido a carga de tooexcessive.</p></td>
<td>O Barramento de</td>
<td>Hadoop, Hbase, Storm</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-12182014-release-of-hdinsight"></a>Notas da versão de 18/12/2014 do HDInsight
Esta versão contém Olá atualização de componente a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Componente</th>
<th>Tipo de cluster</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td><a href = "hdinsight-hadoop-customize-cluster.md" target="_blank">Disponibilidade geral de personalização de cluster</a></td>
<td><p>Personalização permite Olá para você toocustomize o Azure HDInsight clusters com projetos que estão disponíveis no ecossistema do hello Apache Hadoop. Com esse novo recurso, você pode testar e implantar projetos de Hadoop tooAzure HDInsight. Isso é habilitado por meio de saudação **ação de Script** recurso, que pode modificar os clusters de Hadoop formas arbitrárias usando scripts personalizados. Esse recurso de personalização está disponível em todos os tipos de clusters do HDInsight, incluindo Hadoop, HBase e Storm. alimentação de saudação toodemonstrate dessa funcionalidade, documentamos Olá tooinstall de processo de saudação popular <a href = "hdinsight-hadoop-spark-install.md" target="_blank">Spark</a>, <a href = "hdinsight-hadoop-r-scripts.md" target="_blank">R</a>, <a href = "hdinsight-hadoop-solr-install.md" target="_blank">Solr</a>, e <a href = "hdinsight-hadoop-giraph-install.md" target="_blank">Giraph</a> módulos. Esta versão também adiciona o recurso de saudação para clientes toospecify sua ação de script personalizado por meio do portal do Azure de saudação, fornece diretrizes e práticas recomendadas sobre como personalizar toobuild scripts ações usando métodos auxiliares e fornece diretrizes sobre como tootest ação de script Hello. </p></td>
<td>Disponibilidade geral dos recursos</td>
<td>Todos</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-12052014-release-of-hdinsight"></a>Notas da versão de 21/11/2014 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão são:

* HDInsight     2.1.9.406.1221105    (HDP 1.3.9.0-01351)
* HDInsight     3.0.5.406.1221105    (HDP 2.0.9.0-2097)
* HDInsight     3.1.1.406.1221105    (HDP 2.1.9.0-2196)
* SDK do HDInsight N/D

Esta versão contém Olá atualizações de componentes a seguir:

<table border="1">
<tr>
<th>Title</th>
<th>Descrição</th>
<th>Componente</th>
<th>Tipo de cluster</th>
<th>JIRA (se aplicável)</th>
</tr>
<tr>
<td>Correção de bug: erro intermitente durante a adição de grandes números de tabela de tooa de partições em um Hive DDL </td>
<td><p>Se houver um erro de conexão intermitente com o banco de dados do hello Hive metastore quando a adição de uma série de tabela de Hive tooa partições, Olá Hive DDL pode falhar. Olá instrução isseen no log de erros de Hive Olá a seguir se essa falha ocorrer: </p><p>"ERROR [main]: ql.Driver (SessionState.java:printError(547)) - FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask. MetaException(message:java.lang.RuntimeException: commitTransaction was called but openTransactionCalls = 0. Isso provavelmente indica que há chamadas desbalanceada tooopenTransaction/commitTransaction)"</p></td>
<td>Hive</td>
<td>Hadoop, HBase</td>
<td>HIVE-482 (Este é um JIRA interno de modo que não é possível fazer um orçamento externamente. Mencionado aqui para referência.)</td>
</tr>
<tr>
<td>Correção de bug: suspensão ocasional em Olá Console de consulta do HDInsight</td>
<td>Quando isso acontece, hello instrução a seguir pode ser vista no log de WebHCat Olá para o trabalho de iniciador WebHCat hello: <p>"org.apache.hive.hcatalog.templeton.CatchallExceptionMapper | org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.yarn.exceptions.YarnRuntimeException): não foi possível carregar o arquivo de histórico {arquivo de histórico wasb url toohello} "</p></td>
<td>WebHCat</td>
<td>O Hadoop</td>
<td>HIVE-482 (Este é um JIRA interno de modo que não é possível fazer um orçamento externamente. Mencionado aqui para referência.)</td>
</tr>
<tr>
<td>Correção de bug: pico ocasional na latência das consultas do HBase</td>
<td>Se isso acontecer, os usuários irá notar um pico ocasional de 3 segundos na latência de saudação do Hbase consultas. </td>
<td>Gateway do cluster HDInsight</td>
<td>HBase</td>
<td>N/D</td>
</tr>
<tr>
<td>Mudanças de nomes dos arquivos JAR HDP</td>
<td>Para HDI cluster versão 3.0, há algumas alterações toohello interno JAR arquivos instalados pelo HDP. jetty-6.1.26.jar foi substituído por jetty-6.1.26.hwx.jar. jetty-util-6.1.26.jar foi substituído pelo jetty-util-6.1.26.hwx.jar. Essas alterações se aplicam a projetos de tooHadoop, Mahout, WebHCat e Oozie.</td>
<td>Hadoop, Mahout, WebHCat, Oozie</td>
<td>Hadoop, HBase</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-11212014-release-of-hdinsight"></a>Notas da versão de 21/11/2014 do HDInsight
números de versão completa Olá para clusters de HDInsight implantados com esta versão são:

* HDInsight 2.1.9.382.1169709 (sem alteração desde 14/11/2014)
* HDInsight 3.0.5.382.1169709 (sem alteração desde 14/11/2014)
* HDInsight 3.1.1.382.1169709 (sem alteração desde 14/11/2014)
* SDK do HDInsight 1.4.0

Esta versão contém Olá atualizações de componentes a seguir:

<table border="1">
<tr><th>Title</th><th>Descrição</th><th>Componente</th><th>Tipo de cluster</th><th>JIRA (se aplicável)</th></tr>
<tr>
<td>Acesso a logs de aplicativos</td>
<td>Capacidade tooprogrammatically enumerar aplicativos que foram executados nos seus clusters e toodownload relevantes logs específicos do aplicativo ou específicos de contêineres toohelp depuração problemático.</td>
<td>.</td>
<td>O Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Nome da região toospecify capacidade em IHdInsightClient.DeleteCluster </td>
<td>Hello Azure HDInsight SDK fornece Olá capacidade toospecify um nome de região ao usar **DeleteCluster**. Isso ajuda os clientes que tinham dois recursos com o mesmo nome em diferentes regiões e tiveram sido toodelete não é possível desbloquear o qualquer um deles.</td>
<td>.</td>
<td>Todos</td>
<td>N/D</td>
</tr>
<tr>
<td>ClusterDetails.DeploymentId</td>
<td>Olá **ClusterDetails** objeto retorna um **DeploymentID** campo que representa um identificador exclusivo para o cluster de saudação. É garantido que ele toobe em criação de cluster de tentativas com hello mesmo nomes.</td>
<td>.</td>
<td>Todos</td>
<td>N/D</td>
</tr>
</table>

## <a name="notes-for-11142014-release-of-hdinsight"></a>Notas da versão de 14/11/2014 do HDInsight

números de versão completa Olá para clusters de HDInsight implantados com esta versão são:

* HDInsight 2.1.9.382.1169709
* HDInsight 3.0.5.382.1169709
* HDInsight 3.1.1.382.1169709

Esta versão contém Olá novos recursos, atualizações de componentes e correções de bug a seguir.

<table border="1">
<tr><th>Title</th><th>Descrição</th><th>Componente</th><th>Tipo de cluster</th><th>JIRA (se aplicável)</th></tr>
<tr>
<td>Ação de script (visualização)</td>
<td>Visualização do recurso de personalização de cluster Olá que permite a modificação de Hadoop clusters maneiras arbitrário usando scripts personalizados. Com esse recurso, os usuários podem experimentar e implantar projetos que estão disponíveis no hello Apache Hadoop ecossistema tooAzure que clusters HDInsight. O recurso de personalização está disponível em todos os tipos de clusters do HDInsight, incluindo Hadoop, HBase e Storm.</td>
<td>New recurso</td>
<td>Todos</td>
<td>N/D</td>
</tr>
<tr>
<td>Trabalhos pré-compilados para sites do Azure e análise de logs de armazenamento</td>
<td>Olá HDInsight Console de consulta tem uma galeria de Introdução que dá suporte a soluções que funcionam em seus dados ou em dados de exemplo.
<p>**Soluções que funcionam com seus dados**:<br>
Criamos trabalhos para algumas das hello mais comuns dados análise cenários tooprovide um ponto de partida para criar suas próprias soluções. Você pode usar seus dados com hello trabalho toosee como ele funciona. Quando você estiver pronto, use o que você aprendeu toocreate uma solução que é modelada trabalho pré-compilada hello.</p>
<p>**Soluções que funcionam com dados de exemplo**:<br>
Saiba como toowork com HDInsight examinando alguns cenários básicos (como analisar dados de sensor e os logs da web). Você aprenderá como HDInsight toouse tooanalyze esses dados e como você pode se conectar a outros dados toothis aplicativos e serviços. Visualização de dados conectando tooMicrosoft Excel fornece um exemplo de energia Olá dessa abordagem.</p></td>
<td>Console de consulta</td>
<td>O Hadoop</td>
<td>N/D</td>
</tr>
<tr>
<td>Correção de perda de memória no Templeton</td>
<td>Foi tratada a perda de memória no Templeton que afetava os clientes que tinham um cluster em execução há tempos ou que estavam enviando 100s de solicitações de trabalhos por segundo. Olá problema manifestado como Templeton 5xx erros e solução de saudação toorestart Olá serviço was. solução alternativa de saudação não for mais necessário.</td>
<td>Templeton</td>
<td>Todos</td>
<td>https://issues.apache.org/jira/browse/HADOOP-11248</td>
</tr>
</table>

> [!NOTE]
> toodemonstrate Olá novos recursos disponibilizados pela personalização de cluster, usando a ação de Script tooinstall Spark e módulos de R em um cluster de procedimentos de saudação foram documentados. Para obter mais informações, consulte:

* [Instalar e usar o Spark 1.0 em clusters HDInsight](hdinsight-hadoop-spark-install.md)
* [Instalar e usar R em clusters Hadoop do HDInsight](hdinsight-hadoop-r-scripts.md)

## <a name="notes-for-11072014-release-of-hdinsight"></a>Notas da versão de 07/11/2014 do HDInsight

números de versão completa Olá para clusters de HDInsight implantado com esta versão são:

* HDInsight 2.1    2.1.9.374.1153876
* HDInsight 3.0    3.0.5.374.1153876
* HDInsight 3.1    3.1.1.374.1153876

Esta versão contém Olá atualizações de componentes a seguir:

<table border="1">
<tr><th>Title</th><th>Descrição</th><th>Componente</th><th>Tipo de cluster</th><th>JIRA (se aplicável)</th></tr>
<tr>
<td>HDP 2.1.7</td>
<td>Esta versão é baseada no Hortonworks Data Platform (HDP) 2.1.7. Para obter mais informações, confira <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html" target="_blank">Notas de versão do HDP 2.1.7</a>.</td>
<td>HDP</td>
<td>Todos</td>
<td>N/D</td>
</tr>
<tr>
<td>Servidor de linha do tempo do YARN</td>
<td>Olá YARN cronograma Server (também conhecido como Olá servidor genérico de histórico de aplicativo) foi habilitado por padrão. Saudação da linha do tempo de servidor fornece informações genéricas sobre aplicativos concluídos (como ID do aplicativo, nome do aplicativo, o status de aplicativo, hora de envio do aplicativo e tempo de conclusão de aplicativo).

Essas informações de aplicativo podem ser recuperadas do nó principal Olá acessando Olá URI http://headnodehost:8188 ou executando o comando YARN Olá: yarn aplicativo - lista - appStates todos.

Essas informações também podem ser recuperadas remotamente por uma API REST em https://{ClusterDnsName}. azurehdinsight.net/ws/v1/applicationhistory/.

Para obter mais informações, confira <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN Timeline Server</a> (Servidor de linha do tempo do YARN).</td>
<td>Serviço, YARN</td>
<td>Hadoop, HBase</td>
<td>N/D</td>
</tr>
<tr>
<td>ID de Implantação de Cluster</td>
<td>Iniciando pela versão 1.3.3.1.5426.29232 do SDK, os usuários podem acessar uma ID exclusiva para cada cluster, emitida pelo HDInsight. Este toofigure de clientes permite que as instâncias exclusivas de clusters quando um nome DNS está sendo reutilizado em criar ou descartar cenários.</td>
<td>.</td>
<td>Todos</td>
<td>N/D</td>
</tr>
</table>

> [!NOTE]
> bug Olá que impediu o número de versão completo Olá aparecendo no portal de saudação ou sendo retornada por Olá SDK ou o Windows PowerShell foi corrigido nesta versão.

## <a name="notes-for-10152014-release"></a>Notas para a versão de 15/10/2014

Esta versão do hotfix corrigido um vazamento de memória em Templeton que usuários pesada de saudação do Templeton afetados. Em alguns casos, os usuários que são desempenhadas Templeton muito veria erros manifestados como 500 códigos de erro, porque as solicitações de saudação não teria suficiente toorun de memória. solução de saudação para esse problema foi serviço do toorestart Olá Templeton. Esse problema foi corrigido.

## <a name="notes-for-1072014-release"></a>Notas para a versão de 07/10/2014

* Ao usar o Ambari ponto de extremidade, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", Olá *host_name* campo retorna Olá totalmente qualificado (FQDN) do nome de domínio do nó de saudação em vez de apenas o nome de host de saudação. Por exemplo, em vez de retornar "**headnode0**", você pode obter Olá FQDN"**headnode0. { ClusterDNS} .azurehdinsight .net**". Essa alteração foi necessária toofacilitate cenários onde vários tipos de cluster (por exemplo, HBase e Hadoop) podem ser implantados em uma rede virtual. Isso acontece, por exemplo, ao usar HBase como uma plataforma de back-end para o Hadoop.

* Fornecemos novas configurações de memória para a implantação padrão de saudação do cluster do HDInsight hello. Configurações de memória padrão anterior não adequadamente conta para orientação de saudação do número de saudação de núcleos de CPU que está sendo implantado. Essas novas configurações de memória devem fornecer melhores padrões, de acordo com as recomendações da Hortonworks. toochange isso, consulte a documentação de referência SDK toohello sobre como alterar a configuração de cluster. Olá novas configurações de memória que são usadas pelo cluster de HDInsight saudação padrão 4 CPU core (8 contêiner) são discriminadas em Olá a tabela a seguir. (Olá valores usados toothis anterior versão também são fornecidos entre parênteses.)

<table border="1">
<tr><th>Componente</th><th>Alocação de memória</th></tr>
<tr><td> yarn.scheduler.minimum-allocation</td><td>768 MB (anteriormente 512 MB)</td></tr>
<tr><td> yarn.scheduler.maximum-allocation</td><td>6144 MB (inalterado)</td></tr>
<tr><td>yarn.nodemanager.resource.memory</td><td>6144 MB (inalterado)</td></tr>
<tr><td>mapreduce.map.memory</td><td>768 MB (anteriormente 512 MB)</td></tr>
<tr><td>mapreduce.map.java.opts</td><td>opts=-Xmx512m (anteriormente -Xmx410m)</td></tr>
<tr><td>mapreduce.reduce.memory</td><td>1536 MB (anteriormente 1024 MB)</td></tr>
<tr><td>mapreduce.reduce.java.opts</td><td>opts=-Xmx1024m (anteriormente -Xmx819m)</td></tr>
<tr><td>yarn.app.mapreduce.am.resource</td><td>768 MB (anteriormente 1024 MB)</td></tr>
<tr><td>yarn.app.mapreduce.am.command</td><td>opts=-Xmx512m (anteriormente -Xmx819m)</td></tr>
<tr><td>mapreduce.task.io.sort</td><td>256 MB (anteriormente 200 MB)</td></tr>
<tr><td>tez.am.resource.memory</td><td>1536 MB (inalterado)</td></tr>
</table>

Para obter mais informações sobre definições de configuração de memória Olá usada pelo YARN e MapReduce em Olá Hortonworks Data Platform que é usado pelo HDInsight, consulte [determinar definições de configuração de memória HDP](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1-latest/bk_installing_manually_book/content/rpm-chap1-11.html). Hortonworks também forneceu uma ferramenta toocalculate configurações de memória adequada.

Sobre hello Azure PowerShell e Olá mensagem de erro do SDK do HDInsight: "*Cluster não está configurado para acesso de serviços HTTP*":

* Esse erro é um conhecido [problema de compatibilidade](https://social.msdn.microsoft.com/Forums/azure/a7de016d-8de1-4385-b89e-d2e7a1a9d927/hdinsight-powershellsdk-error-cluster-is-not-configured-for-http-services-access?forum=hdinsight) que podem ocorrer devido a diferença tooa em Olá de saudação HDInsight SDK ou versão do PowerShell do Azure e hello de cluster hello. Clusters criados a partir de 15/08 dão suporte à nova funcionalidade de provisionamento em Redes Virtuais. Mas esse recurso não é interpretado corretamente por versões mais antigas do hello HDInsight SDK ou o Azure PowerShell. resultado de saudação é uma falha em algumas operações de envio de trabalho. Se você usar os cmdlets do PowerShell do Azure ou APIs do SDK do HDInsight (**Use AzureRmHDInsightCluster** ou **AzureRmHDInsightHiveJob Invoke**) toosubmit trabalhos, essas operações podem falhar com a mensagem de erro hello " *Cluster <clustername> não está configurado para acesso de serviços HTTP*. " Ou (dependendo da operação de saudação), você pode obter outras mensagens de erro, como "*não é possível conectar toocluster*".
* Esses problemas de compatibilidade são resolvidos em versões mais recentes de saudação do hello HDInsight SDK e do PowerShell do Azure. É recomendável atualizar Olá HDInsight SDK tooversion 1.3.1.6 ou posterior e o Azure PowerShell ferramentas tooversion 0.8.8 ou posterior. Você pode obter acesso toohello SDK mais recente do HDInsight de [preciosidade](http://nuget.codeplex.com/wikipage?title=Getting%20Started) e Olá ferramentas do PowerShell do Azure em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

## <a name="notes-for-9122014-release-of-hdinsight-31"></a>Notas da versão de 12/09/2014 do HDInsight 3.1
* Esta versão é baseada na HDP (plataforma de dados Hortonworks) 2.1.5. Para obter uma lista de erros de saudação corrigidos nesta versão, consulte Olá [corrigido nessa versão](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.5/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.5-fixed.html) página no site de Hortonworks hello.
* Na pasta de bibliotecas de Pig hello, Olá "avro-mapred-1.7.4.jar" arquivo foi alterado muito "avro-mapred-1.7.4-hadoop2.jar." conteúdo deste arquivo Hello contém uma correção de bug secundária que é incondicional. É recomendável que os clientes não faça uma dependência direta do nome de saudação do hello JAR arquivo tooavoid quebras quando os arquivos são renomeados.

## <a name="notes-for-8212014-release"></a>Notas para a versão de 21/08/2014
* Estamos adicionando Olá seguinte WebHCat configuração (seção 7155), que define o limite de memória saudação padrão para um controlador de Templeton trabalho too1 GB. (o valor padrão anterior de saudação foi 512 MB.)

     templeton.mapper.memory.mb (=1024)

  * Essa alteração endereços Olá erro com determinadas consultas de Hive devido a limites de memória toolower a seguir: "Contêiner está sendo executado além dos limites de memória física."
  * toorevert toohello os padrões antigo, você pode definir essa too512 de valor de configuração por meio do PowerShell do Azure no momento da criação de cluster usando o comando a seguir de saudação:

      Add-AzureRmHDInsightConfigValues -Core @{"templeton.mapper.memory.mb"="512";}
* nome de host de saudação da função de zookeeper Olá foi alterada muito*zookeeper*. Isso afeta a resolução de nome em cluster hello, mas isso não afetará as APIs REST externas. Se você tiver componentes Olá que use *zookeepernode* nome de host, você precisa tooupdate-los toouse novo nome. novos nomes de três nós de zookeeper Olá Olá são:

  * zookeeper0
  * zookeeper1
  * zookeeper2
* A matriz de suporte de versão do HBase é atualizada. Somente a versão HDInsight 3.1 (HBase versão 0.98) tem suporte para cargas de trabalho de produção no HBase. A versão 3.0, que estava disponível para visualização, não terá suporte se você prosseguir.

## <a name="notes-about-clusters-created-prior-too8152014"></a>Observações sobre clusters criados anterior em 15/too8/2014
Uma mensagem de erro do Azure PowerShell ou o SDK do HDInsight "Cluster <clustername> não está configurado para acesso de serviços HTTP" (ou, dependendo da operação de hello, outro mensagens de erro, como: "Não é possível conectar toocluster") podem ser encontrados devido a diferenças de versão tooa entre o Azure PowerShell ou Olá HDInsight SDK e um cluster. Clusters criados a partir de 15/08 dão suporte à nova funcionalidade de provisionamento em Redes Virtuais. Esse recurso não é interpretado corretamente por versões mais antigas do hello Azure PowerShell ou hello HDInsight SDK, que resulta em falhas de operações de envio de trabalho. Se você usar APIs do SDK do HDInsight ou do Azure PowerShell cmdlets (por exemplo, Use AzureRmHDInsightCluster ou AzureRmHDInsightHiveJob Invoke) toosubmit trabalhos, essas operações podem falhar com uma das mensagens de erro Olá descritas.

Esses problemas de compatibilidade são resolvidos em versões mais recentes de saudação do hello HDInsight SDK e do PowerShell do Azure. É recomendável atualizar Olá HDInsight SDK tooversion 1.3.1.6 ou posterior e o Azure PowerShell ferramentas tooversion 0.8.8 ou posterior. Você pode obter acesso toohello SDK mais recente do HDInsight de [NuGet][nuget-link]. Você pode acessar as ferramentas do PowerShell do Azure hello usando [Microsoft Web Platform Installer][webpi-link].

## <a name="notes-for-7282014-release"></a>Notas para a versão de 28/07/2014
* **HDInsight disponível no novo regiões**: expandir regiões do HDInsight presença geográfica toothree. Os clientes que usam o HDInsight agora podem criar clusters nessas regiões:
  * Ásia Oriental
  * Centro-Norte dos EUA
  * Centro-Sul dos Estados Unidos
* HDInsight versão 1.6 (HDP 1.1 e Hadoop 1.0.3) e HDInsight versão 2.1 (HDP1.3 e Hadoop 1.2) estão sendo removidos da saudação portal do Azure. Você pode continuar a clusters de Hadoop toocreate para essas versões usando Olá cmdlet do PowerShell do Azure, [New-AzureRmHDInsightCluster](http://msdn.microsoft.com/library/dn593744.aspx) ou usando Olá [HDInsight SDK](http://msdn.microsoft.com/library/azure/dn469975.aspx). Para obter mais informações, consulte [Controle de versão do componente do HDInsight](hdinsight-component-versioning.md).
* Alterações ao Hortonworks Data Platform (HDP) nesta versão:

<table border="1">
<tr><th>HDP</th><th>Alterações</th></tr>
<tr><td>HDP 1.3 / HDI 2.1</td><td>Sem alterações</td></tr>
<tr><td>HDP 2.0 / HDI 3.0</td><td>Sem alterações</td></tr>
<tr><td>HDP 2,1 / HDI 3,1</td><td>zookeeper: ['3.4.5.2.1.3.0-1948'] -> ['3.4.5.2.1.3.2-0002']</td></tr>
</table>

## <a name="notes-for-6242014-release"></a>Notas para a versão de 24/06/2014
Esta versão contém serviço de HDInsight toohello aprimoramentos:

* **Disponibilidade HDP 2.1**: 3.1 HDInsight (que contém HDP 2.1) está disponível e é a versão do saudação padrão para novos clusters.
* **HBase – melhorias do portal do Azure**: estamos tornando os clusters HBase disponíveis na Visualização. Você pode criar clusters do HBase do portal de saudação com apenas alguns cliques.

Com HBase, você pode criar uma variedade de cargas de trabalho em tempo real no HDInsight, de sites interativos que trabalhar com grandes conjuntos de dados tooservices armazenar dados de telemetria e o sensor de milhões de pontos de extremidade. Olá próxima etapa seria tooanalyze dados Olá essas cargas de trabalho com trabalhos de Hadoop e isso é possível no HDInsight por meio do PowerShell do Azure e o painel do cluster Olá Hive.

### <a name="apache-mahout-preinstalled-on-hdinsight-31"></a>Apache Mahout pré-instalado no HDInsight 3.1
 [Mahout](http://hortonworks.com/hadoop/mahout/) é instalado em clusters de HDInsight 3.1 Hadoop, para que você pode executar trabalhos Mahout sem necessidade de saudação de configuração de cluster adicionais. Por exemplo, você pode remoto em um cluster Hadoop usando o protocolo de área de trabalho remota (RDP), e sem etapas adicionais, você pode executar Olá Olá mundo Mahout comando a seguir:

        mahout org.apache.mahout.classifier.df.tools.Describe -p /user/hdp/glass.data -f /user/hdp/glass.info -d I 9 N L

        mahout org.apache.mahout.classifier.df.BreimanExample -d /user/hdp/glass.data -ds /user/hdp/glass.info -i 10 -t 100

Para obter uma explicação mais completa desse procedimento, consulte documentação Olá Olá [Breiman exemplo](https://mahout.apache.org/users/classification/breiman-example.html) no site do Apache Mahout hello.

### <a name="hive-queries-can-use-tez-in-hdinsight-31"></a>Consultas de Hive podem usar o Tez no HDInsight 3.1
O Hive 0.13 está disponível no HDInsight 3.1 e é capaz de executar consultas usando Tez, que pode ser utilizado para melhorias de desempenho significativas.
O Tez não está habilitado por padrão para consultas de Hive. toouse-lo, você deve aceitar. Você pode habilitar Tez executando Olá trecho de código a seguir:

        set hive.execution.engine=tez;
        select sc_status, count(*), histogram_numeric(sc_bytes,5) from website_logs_orc_local group by sc_status;

A Hortonworks publicou uma demonstração detalhada das melhorias nas consultas do Hive com o Tez, conforme fornecido em medições de desempenho padrão. Para obter mais informações, consulte [Medindo o desempenho do Hive 13 Apache para Hadoop Enterprise](http://hortonworks.com/blog/benchmarking-apache-hive-13-enterprise-hadoop/).

Para saber mais, consulte o artigo [Hive no Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez).

### <a name="global-availability"></a>Disponibilidade global
Com o lançamento de saudação do HDInsight no Hadoop 2.2, Microsoft disponibilizou HDInsight em todas as principais regiões em que o Azure está disponível. Especificamente, oeste Olá data centers Europa e Ásia Sudeste tem foi colocados online. Isso permite que os clusters de toolocate de clientes em um datacenter que está fechado e potencialmente em uma zona semelhante de requisitos de conformidade.

### <a name="dos--donts-between-cluster-versions"></a>Prós e contras entre as versões de clusters
**Os metastores do Oozie usados com um cluster do HDInsight 3.1 não são compatíveis com as versões anteriores dos clusters do HDInsight 2.1 e não podem ser usados com elas**.

Um banco de dados do metastore do Oozie personalizado implantado com um cluster do HDInsight 3.1 não pode ser reutilizado com um cluster do HDInsight 2.1. Esse é o caso de Olá mesmo se originou Olá metastore com um cluster HDInsight 2.1. Não há suporte para esse cenário porque o esquema de metastore Olá é atualizada quando usado com um cluster HDInsight 3.1, portanto, não é mais compatível com metastore Olá exigido pelo clusters Olá HDInsight 2.1. Qualquer tentativa tooreuse um Oozie metastore que foi usado com um cluster HDInsight 3.1 inutilizar o cluster do HDInsight 2.1 hello.

**Os metastores do Oozie não podem ser compartilhados entre clusters diferentes.**

Oozie metastores são anexados toospecific clusters, e eles não podem ser compartilhados entre clusters.

### <a name="breaking-changes"></a>Alterações de última hora
**Sintaxe do prefixo**: somente hello "wasb: / /" sintaxe tem suporte em 3.0 clusters e 3.1 do HDInsight. Olá antigo "asv: / /" sintaxe tem suporte em 1.6 clusters e 2.1 do HDInsight, mas não há suporte no HDInsight 3.1 ou 3.0 clusters. Isso significa que todos os trabalhos enviados tooan HDInsight 3.1 ou 3.0 cluster que explicitamente usa hello "asv: / /" sintaxe falhará. Olá "wasb: / /" sintaxe deve ser usada em vez disso. Além disso, os trabalhos enviados tooany HDInsight 3.1 ou 3.0 clusters que são criados com um metastore existente que contém explícitas referencia tooresources usando hello "asv: / /" sintaxe falhará. Essas metastores necessário toobe recriado usando hello "wasb: / /" recursos de tooaddress de sintaxe.

**Portas**: Olá portas usadas pelo Olá serviço HDInsight alterados. números de porta de saudação que estavam sendo usados foram dentro do intervalo de portas efêmeras de saudação do sistema de operacional do Windows hello. As portas são alocadas automaticamente por meio de um intervalo efêmero, para comunicações baseadas em protocolo de Internet de curta duração. novo conjunto de saudação do permitidos números de porta de serviço de plataforma HDP (Hortonworks Data) estão fora este tooavoid intervalo encontrar conflitos que podem surgir com portas Olá usadas por serviços em execução no nó principal hello. os novos números de porta Olá não devem causar alterações de quebra. Olá números usados são da seguinte maneira:

 **HDInsight 1.6 (HDP 1.1)**

<table border="1">
<tr><th>Nome</th><th>Valor</th></tr>
<tr><td>dfs.http.address</td><td>namenodehost:30070</td></tr>
<tr><td>dfs.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>dfs.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>dfs.datanode.ipc.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>dfs.secondary.http.address</td><td>0.0.0.0:30090</td></tr>
<tr><td>mapred.job.tracker.http.address</td><td>jobtrackerhost:30030</td></tr>
<tr><td>mapred.task.tracker.http.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>mapreduce.history.server.http.address</td><td>0.0.0.0:31111</td></tr>
<tr><td>templeton.port</td><td>30111</td></tr>
</table>

 **HDInsight 3.1 e 3.0 (HDP 2.1 e 2.0)**

<table border="1">
<tr><th>Nome</th><th>Valor</th></tr>
<tr><td>dfs.namenode.http-address</td><td>namenodehost:30070</td></tr>
<tr><td>dfs.namenode.https-address</td><td>headnodehost:30470</td></tr>
<tr><td>dfs.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>dfs.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>dfs.datanode.ipc.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>dfs.namenode.secondary.http-address</td><td>0.0.0.0:30090</td></tr>
<tr><td>yarn.nodemanager.webapp.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>templeton.port</td><td>30111</td></tr>
</table>

### <a name="dependencies"></a>Dependências
Olá seguintes dependências foram adicionadas ao HDInsight 3. x (HDP2.x):

* guice-servlet
* optiq-core
* javax.inject
* activation
* jsr305
* geronimo-jaspic_1.0_spec
* jul-to-slf4j
* java-xmlbuilder
* ant
* commons-compiler
* jdo-api
* commons-math3
* paranamer
* jaxb-impl
* stringtemplate
* eigenbase-xom
* jersey-servlet
* commons-exec
* jaxb-api
* jetty-all-server
* janino
* xercesImpl
* optiq-avatica
* jta
* eigenbase-properties
* groovy-all
* hamcrest-core
* mail
* linq4j
* jpam
* jersey-client
* aopalliance
* geronimo-annotation_1.0_spec
* ant-launcher
* jersey-guice
* xml-apis
* stax-api
* asm-commons
* asm-tree
* wadl
* geronimo-jta_1.1_spec
* guice
* leveldbjni-all
* velocity
* jettison
* snappy-java
* jetty-all
* commons-dbcp

Olá seguintes dependências não existem mais no HDInsight 3. x (HDP2.x):

* jdeb
* kfs
* sqlline
* ivy
* aspectjrt
* json
* core
* jdo2-api
* avro-mapred
* datanucleus-enhancer
* jsp
* commons-logging-api
* commons-math
* JavaEWAH
* aspectjtools
* javolution
* hdfsproxy
* hbase
* snappy

### <a name="version-changes"></a>Mudanças de versão
Olá alterações de versão a seguir foram feita entre HDInsight 2. x (HDP1.x) e HDInsight 3. x (HDP2.x):

* metrics-core: ['2.1.2'] -> ['3.0.0']
* derbynet: ['10.4.2.0'] -> ['10.10.1.1']
* datanucleus: ['rdbms-3.0.8'] -> ['rdbms-3.2.9']
* jasper-compiler: ['5.5.12'] -> ['5.5.23']
* log4j: ['1.2.15', '1.2.16'] -> ['1.2.16', '1.2.17']
* derbyclient: ['10.4.2.0'] -> ['10.10.1.1']
* httpcore: ['4.2.4'] -> ['4.2.5']
* hsqldb: ['1.8.0.10'] -> ['2.0.0']
* jets3t: ['0.6.1'] -> ['0.9.0']
* protobuf-java: ['2.4.1'] -> ['2.5.0']
* derby: ['10.4.2.0'] -> ['10.10.1.1']
* jasper: ['runtime-5.5.12'] -> ['runtime-5.5.23']
* commons-daemon: ['1.0.1'] -> ['1.0.13']
* datanucleus-core: ['3.0.9'] -> ['3.2.10']
* datanucleus-api-jdo: ['3.0.7'] -> ['3.2.6']
* zookeeper: ['3.4.5.1.3.9.0-01320'] -> ['3.4.5.2.1.3.0-1948']
* bonecp: ['0.7.1.RELEASE'] -> ['
* 0.8.0.RELEASE']

### <a name="drivers"></a>Drivers
driver do Java Database Connectivity (JDBC) Olá para o SQL Server é usado internamente pelo HDInsight e não é usado para operações externas. Se você quiser tooconnect tooHDInsight usando conectividade aberta de banco de dados (ODBC), use Olá Hive do Microsoft ODBC driver. Para obter mais informações, consulte [tooHDInsight Excel conectar-se com hello Microsoft ODBC Driver Hive](hdinsight-connect-excel-hive-odbc-driver.md).

### <a name="bug-fixes"></a>Correções de bug
Com esta versão, podemos ter atualizado Olá versões de HDInsight com várias correções de bug a seguir:

* HDInsight 2,1 (HDP 1,3)
* HDInsight 3,0 (HDP 2,0)
* HDInsight 3.1 (HDP 2.1)

## <a name="hortonworks-release-notes"></a>Notas de versão Hortonworks
Notas de versão do hello plataformas de dados de Hortonworks (HDPs) que são usados pelo clusters de versão do HDInsight estão disponíveis em Olá locais a seguir:

* HDInsight versão 3.1 usa uma distribuição de Hadoop que se baseia a saudação [Hortonworks Data Platform 2.1.7][hdp-2-1-7]. Este é um cluster de Hadoop padrão Olá criado ao usar o hello portal do Azure após 7/11/2014. Clusters de HDInsight 3.1 criados antes de 7/11/2014 baseadas no hello [Hortonworks Data Platform 2.1.1][hdp-2-1-1]
* HDInsight versão 3.0 usa uma distribuição de Hadoop que se baseia a saudação [Hortonworks Data Platform 2.0][hdp-2-0-8].
* HDInsight versão 2.1 usa uma distribuição de Hadoop que se baseia a saudação [Hortonworks Data Platform 1.3][hdp-1-3-0].
* HDInsight versão 1.6 usa uma distribuição de Hadoop que se baseia a saudação [Hortonworks Data Platform 1.1][hdp-1-1-0].

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[nuget-link]: https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.HDInsight/

[webpi-link]: http://go.microsoft.com/?linkid=9811175&clcid=0x409

[hdinsight-install-spark]: ../hdinsight-hadoop-spark-install/
[hdinsight-r-scripts]: ../hdinsight-hadoop-r-scripts/
