---
title: "aaaHadoop componentes e versões - HDInsight do Azure | Microsoft Docs"
description: "Saiba mais componentes do Hadoop hello e as versões em HDInsight e hello níveis de serviço disponíveis nesta distribuição de nuvem de Hortonworks Data Platform."
keywords: "versões do Hadoop, componentes de ecossistema do hadoop, componentes do hadoop, como versão do hadoop toocheck"
services: hdinsight
editor: cgronlun
manager: asadk
author: bprakash
tags: azure-portal
documentationcenter: 
ms.assetid: 367b3f4a-f7d3-4e59-abd0-5dc59576f1ff
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: bprakash
ms.openlocfilehash: b661d901b0113458c3501ec06454fc8841189672
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-hadoop-components-and-versions-available-with-hdinsight"></a>Quais são os componentes do Hadoop hello e versões disponíveis com o HDInsight?

Saiba mais sobre os componentes de ecossistema do Apache Hadoop hello e versões no Microsoft Azure HDInsight, bem como Olá níveis de serviço Standard e Premium. Além disso, saiba como versões de componente toocheck Hadoop no HDInsight. 

Cada versão do HDInsight é uma distribuição de nuvem de uma versão do HDP (Hortonworks Data Platform).

## <a name="hadoop-components-available-with-different-hdinsight-versions"></a>Componentes do Hadoop disponíveis com diferentes versões do HDInsight
O HDInsight do Azure dá suporte a várias versões do cluster Hadoop que podem ser implantadas a qualquer momento. Cada opção de versão cria uma versão específica de distribuição de HDP hello e um conjunto de componentes que estão contidos a essa distribuição. A partir de 17 de fevereiro de 2017, versão do cluster saudação padrão usado pelo Azure HDInsight é 3.5 e é baseada em HDP 2.5.

versões de componente Olá associadas a versões de cluster do HDInsight estão listadas na Olá a tabela a seguir. 

> [!NOTE]
> versão do padrão de saudação para Olá serviço HDInsight pode ser alterado sem aviso prévio. Se você tiver uma dependência de versão, especifique a versão do HDInsight Olá quando você cria os clusters com hello .NET SDK com o PowerShell do Azure e a CLI do Azure.

| Componente | HDInsight 3.6 (padrão) | HDInsight 3.5 | HDInsight 3.4 | HDInsight 3.3 | HDInsight 3.2 | HDInsight 3.1 | HDInsight 3.0 |
| --- | --- | --- | --- | --- | --- | --- |--- |
| Hortonworks Data Platform |2.6 |2.5 |2.4 |2.3 |2.2 |2.1.7 |2,0 |
| Apache Hadoop e YARN |2.7.3 |2.7.3 |2.7.1 |2.7.1 |2.6.0 |2.4.0 |2.2.0 |
| Apache Tez |0.7.0 |0.7.0 |0.7.0 |0.7.0 |0.5.2 |0.4.0 |-|
| Apache Pig |0.16.0 |0.16.0 |0.15.0 |0.15.0 |0.14.0 |0.12.1 |0.12.0 |
| Apache Hive e HCatalog |1.2.1 |1.2.1 |1.2.1 |1.2.1 |0.14.0 |0.13.1 |0.12.0 |
| Apache Hive2 | 2.1.0 |-|-|-|-|-|-|
| Apache Tez Hive2 | 0.8.4 |-|-|-|-|-|-|
| Apache Ranger | 0.7.0 |0.6.0 |-|-|-|-|-|
| HBase no Apache |1.1.2 |1.1.2 |1.1.2 |1.1.1 |0.98.4 |0.98.0 |-|
| Apache Sqoop |1.4.6 |1.4.6 |1.4.6 |1.4.6 |1.4.5 |1.4.4 |1.4.4 |
| Apache Oozie |4.2.0 |4.2.0 |4.2.0 |4.2.0 |4.1.0 |4.0.0 |4.0.0 |
| O Apache Zookeeper |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.5 |3.4.5 |
| Apache Storm |1.1.0 |1.0.1 |0.10.0 |0.10.0 |0.9.3 |0.9.1 |-|
| O Apache Mahout |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0 |0.9.0 |-|
| Apache Phoenix |4.7.0 |4.7.0 |4.4.0 |4.4.0 |4.2.0 |4.0.0.2.1.7.0-2162 |-|
| Apache Spark |2.1.0 (somente Linux) |1.6.2 + 2.0 (somente Linux) |1.6.0 (somente Linux) |1.5.2 (somente build experimental do Linux) |1.3.1 (somente Windows) |-|-|
| Apache Kafka | 0.10.0 | 0.10.0 | 0.9.0 |-|-|-|-|
| Apache Ambari | 2.5.0 | 2.4.0 | 2.2.1 | 2.1.0 |-|-|-|
| Apache Zeppelin | 0.7.0 |-|-|-|-|-|-|
| Mono |4.2.1 |4.2.1 |3.2.8 |-|-|-|

## <a name="check-for-current-hadoop-component-version-information"></a>Verificar informações atuais de versão do componente do Hadoop

as versões de componente ecossistema Hadoop Olá associadas a versões de cluster do HDInsight podem alterar com tooHDInsight de atualizações. componentes de Hadoop Olá toocheck e tooverify quais versões estão sendo usadas para um cluster, use Olá API REST do Ambari. Olá **GetComponentInformation** comando recupera informações sobre componentes de serviço. Para obter detalhes, consulte Olá [Ambari documentação][ambari-docs].

Para clusters do Windows, outra maneira toocheck Olá a versão do componente é toolog tooa cluster usando a área de trabalho remota e examinar o conteúdo de saudação do diretório de C:\apps\dist\ hello.

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [Baixa do Windows no HDInsight](#hdinsight-windows-retirement).

### <a name="release-notes"></a>Notas de versão

Consulte [notas de versão do HDInsight](hdinsight-release-notes.md) para notas de versão adicionais em versões mais recentes de saudação do HDInsight.

## <a name="supported-hdinsight-versions"></a>Versões do HDInsight com suporte
Olá tabela a seguir lista versões de saudação do HDInsight estão disponíveis atualmente no hello portal do Azure. versões HDP Olá que correspondem a versão do HDInsight tooeach são listadas juntamente com as datas de lançamento de produto hello. as datas de validade e desativação de suporte Olá também são fornecidas, quando eles são conhecidos.

> [!NOTE]
> Depois que o suporte para uma versão tiver expirado, ele pode não estar disponível por meio do portal clássico do Microsoft Azure hello. No entanto, as versões de cluster continuam toobe disponível usando Olá `Version` parâmetro hello do Windows PowerShell [AzureRmHDInsightCluster novo](https://msdn.microsoft.com/library/mt619331.aspx) de comando e Olá SDK .NET até a data de desativação de versão de saudação.
> 
> Clusters altamente disponíveis com dois headnodes são implantados por padrão para clusters HDInsight versão 2.1 e posterior. Eles não estão disponíveis para clusters HDInsight versão 1.6.

| Versão do HDInsight | Versão do HDP | SO da VM | Alta disponibilidade | Data do lançamento | Disponibilidade no hello portal do Azure | Data de expiração do suporte | Data de baixa |
| --- | --- | --- | --- | --- | --- | --- | --- |
| HDInsight 3.6 |HDP 2.6 |Ubuntu 16 |Sim |4 de abril de 2017 |Sim | | |
| HDInsight 3.5 |HDP 2.5 |Ubuntu 16 |Sim |30 de setembro de 2016 |Sim |5 de setembro de 2017 |31 de maio de 2018 |
| HDInsight 3.4 |HDP 2.4 |Ubuntu 14.0.4 LTS |Sim |29 de março de 2016 |Sim |29 de dezembro de 2016 |9 de janeiro de 2018 |
| HDInsight 3.3 |HDP 2.3 |Windows Server 2012 R2 |Sim |2 de dezembro de 2015 |Sim |27 de junho de 2016 |31 de julho de 2018 |
| HDInsight 3.3 |HDP 2.3 |Ubuntu 14.0.4 LTS |Sim |2 de dezembro de 2015 |Sim |27 de junho de 2016 |31 de julho de 2017 |
| HDInsight 3.2 |HDP 2.2 |Ubuntu 12.04 LTS ou Windows Server 2012 R2 |Sim |18 de fevereiro de 2015 |Não |1º de março de 2016 |1º de abril de 2017 |
| HDInsight 3.1 |HDP 2,1 |Windows Server 2012 R2 |Sim |24 de junho de 2014 |Não |18 de maio de 2015 |30 de junho de 2016 |
| HDInsight 3.0 |HDP 2,0 |Windows Server 2012 R2 |Sim |11 de fevereiro de 2014 |Não |17 de setembro de 2014 |30 de junho de 2015 |
| HDInsight 2.1 |HDP 1,3 |Windows Server 2012 R2 |Sim |28 de outubro de 2013 |Não |12 de maio de 2014 |31 de maio de 2015 |
| HDInsight 1.6 |HDP 1.1 | |Não |28 de outubro de 2013 |Não |26 de abril de 2014 |31 de maio de 2015 |

## <a name="hdinsight-windows-retirement"></a>Baixa do Windows do HDInsight
Microsoft Azure HDInsight versão 3.3 foi Olá última versão do HDInsight no Windows. Olá data de desativação para HDInsight no Windows é 31 de julho de 2018. Se você tiver qualquer clusters HDInsight no Windows 3.3 ou anterior, você deve migrar tooHDInsight no Linux (HDInsight versão 3.5 ou posterior) antes de 31 de julho de 2018. Migrando toohello o sistema operacional Linux permite tooretain Olá capacidade toocreate ou redimensionar seus clusters HDInsight. O suporte ao HDInsight versão 3.3 no Windows expirou em 27 de junho de 2016.

A partir do HDInsight versão 3.4, a Microsoft lançou HDInsight apenas em Olá sistema operacional Linux. Como resultado, alguns dos componentes de saudação no HDInsight estão disponíveis para Linux somente. Isso inclui Apache Ranger, Kafka, Hive interativo, Spark, aplicativos de HDInsight e o repositório Azure Data Lake como sistema de arquivos principal hello. Versões futuras do HDInsight estão disponíveis apenas em Olá sistema operacional Linux. Não haverá nenhuma versão futura do HDInsight no Windows. 

## <a name="faqs"></a>Perguntas frequentes

### <a name="what-is-hello-timeline-for-retiring-hdinsight-on-windows"></a>O que é o cronograma de saudação para desativar o HDInsight no Windows?
31 de julho de 2018 é hello data de desativação para HDInsight no Windows. Se Olá planejada data de desativação é diferente para a sua região, você será notificado separadamente. 

### <a name="what-is-hello-impact-of-retiring-hdinsight-on-windows-for-existing-customers"></a>Qual é o impacto de saudação de desativar o HDInsight no Windows para clientes existentes?
Após a baixa do HDInsight no Windows, não é possível criar um novo cluster HDInsight do Windows nem redimensionar um cluster HDInsight do Windows existente. O suporte ao HDInsight versão 3.3 expirou em 27 de junho de 2016. Portanto, não há nenhum suporte ou correções de bug para HDInsight 3.3 ou versões anteriores. Versões futuras do HDInsight estão disponíveis apenas em Olá sistema operacional Linux. Não haverá nenhuma versão futura do HDInsight no Windows.
 
### <a name="which-versions-of-hdinsight-on-windows-are-affected"></a>Quais versões do HDInsight no Windows são afetadas?
HDInsight do Azure versão 3.3 é Olá última versão do HDInsight para Windows. Antes de HDInsight no Windows é desativado, todas as janelas de HDInsight clusters versão 3.3 ou anterior deve ser migrado tooHDInsight no Linux versão 3.5 ou posterior. Migrando o tooHDInsight de clusters no Linux permite tooretain Olá capacidade toocreate novos clusters ou redimensionar clusters existentes. 

### <a name="what-do-i-need-toodo"></a>O que eu preciso toodo?
Migre um cluster HDInsight Windows clusters tooa suporte para Linux HDInsight antes de 31 de julho de 2018. Saiba mais em Olá [documento de migração de HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). Para obter detalhes sobre as versões de HDInsight do Azure, consulte a lista de saudação do [versões com suporte](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-component-versioning#supported-hdinsight-versions). 

### <a name="where-do-i-find-hello-cluster-os-type"></a>Onde encontrar o tipo de sistema operacional do cluster Olá?
No hello portal do Azure, vá toohello página de visão geral do HDInsight Cluster e localize **tipo de Cluster** em **Essentials**. tipos de sistema operacional do cluster de saudação são listados na página. 

### <a name="i-cant-migrate-tooan-hdinsight-linux-cluster-by-july-31-2018-what-is-hello-impact-toomy-hdinsight-windows-cluster"></a>Não é possível migrar tooan cluster HDInsight Linux por 31 de julho de 2018. O que é Olá impacto toomy cluster HDInsight Windows?
Olá cluster HDInsight Windows é executado como-é, mas você não pode criar um novo cluster HDInsight Windows ou redimensionar um cluster HDInsight Windows existente. 

### <a name="my-cluster-has-a-net-dependency-how-do-i-resolve-this-dependency-on-linux"></a>O cluster tem uma dependência do .NET. Como fazer para resolver essa dependência no Linux?
Você pode resolver a dependência do cluster Linux usando Olá [projeto Mono](http://www.mono-project.com/). Essa implementação de software livre do .NET está disponível para clusters HDInsight do Linux. Saiba mais em Olá [documento de migração de HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). 

### <a name="im-a-new-customer-for-hdinsight-on-windows-how-can-i-create-an-hdinsight-windows-cluster"></a>Sou um novo cliente para HDInsight no Windows. Como criar um cluster HDInsight do Windows?
A partir de 3 de julho de 2017, apenas clientes existentes do HDInsight do Windows podem criar novos clusters HDInsight do Windows. Novos clientes não é possível criar um cluster do Windows do HDInsight em Olá portal do Azure usando o PowerShell ou hello SDK. É recomendável que novos clientes criem um cluster HDInsight do Linux. Os clientes existentes podem criar novas janelas do HDInsight clusters até Olá HDInsight no Windows data de desativação. 

### <a name="is-there-a-pricing-impact-associated-with-moving-from-hdinsight-on-windows-toohdinsight-on-linux"></a>Há um impacto no preço associado à movimentação de HDInsight em Windows tooHDInsight no Linux?
Não, Olá preços é hello mesmo para HDInsight em qualquer sistema operacional. 

### <a name="what-are-hello-customer-advantages-associated-with-hello-move-tooonly-using-hdinsight-on-linux"></a>Quais são as vantagens de cliente Olá associadas Olá move tooonly usando HDInsight no Linux?
* Tempo de entrega mais rápido para tecnologias de dados grandes do código-fonte aberto por meio de Olá serviço HDInsight
* Uma grande comunidade e ecossistema de suporte
* Desenvolvimento de ativo tooexercise capacidade por Olá abrir comunidade de código para Hadoop e outras tecnologias de dados grandes

### <a name="does-hdinsight-on-linux-provide-additional-functionality-beyond-what-is-available-in-hdinsight-on-windows"></a>HDInsight no Linux oferece funcionalidade adicional além do que está disponível no HDInsight no Windows?
A partir do HDInsight versão 3.4, a Microsoft lançou HDInsight apenas em Olá sistema operacional Linux. Como resultado, alguns dos componentes de saudação no HDInsight estão disponíveis para Linux somente. Isso inclui Apache Ranger, Kafka, Hive interativo, Spark, aplicativos de HDInsight e o repositório Azure Data Lake como sistema de arquivos principal hello. 

## <a name="service-level-agreement-for-hdinsight-cluster-versions"></a>Contrato de nível de serviço para versões do cluster HDInsight
contrato de nível de serviço (SLA) do Hello é definido em termos de um _janela suporte_. janela de suporte de saudação é Olá período de tempo que uma versão de cluster HDInsight é suportada pelo suporte e atendimento ao cliente Microsoft. Se a versão de saudação tem um _suporte a data de validade_ que passou, cluster de HDInsight hello está fora da janela de suporte de saudação. Para obter mais informações sobre versões com suporte, consulte a lista de saudação do [suporte para versões de cluster do HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). Data de validade Olá suporte para uma versão X (depois que houver uma versão mais recente do X + 1) de HDInsight especificado é calculada como Olá posterior:  

* Fórmula 1: Adicione data de toohello de 180 dias, quando a versão do cluster HDInsight Olá X foi liberado.
* Fórmula 2: Adicione data toohello de 90 dias quando versão do cluster HDInsight Olá X + 1 é disponibilizado no portal do Azure.

Olá _data de desativação_ Olá data após o qual versão do cluster Olá não pode ser criado no HDInsight. Desde 31 de julho de 2017, você não pode redimensionar um cluster HDInsight após sua data de baixa. 

> [!NOTE]
> Clusters de HDInsight Windows (incluindo versões 2.1, 3.0, 3.1, 3.2 e 3.3) é executado na família do sistema operacional convidado do Azure versão 4, que usa a versão de 64 bits de saudação do Windows Server 2012 R2. Família do sistema operacional convidado do Azure versão 4 oferece suporte a versões do hello do .NET Framework 4.0, 4.5, 4.5.1 e 4.5.2.

## <a name="hortonworks-release-notes-associated-with-hdinsight-versions"></a>Notas de versão do Hortonworks associadas a versões do HDInsight

seção Olá fornece links toorelease anotações para distribuições de Hortonworks Data Platform hello e componentes do Apache que são usados com o HDInsight.
* O cluster do HDInsight versão 3.6 usa uma distribuição do Hadoop baseada no [Hortonworks Data Platform 2.6](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.0/bk_release-notes/content/ch_relnotes.html).
* O cluster do HDInsight versão 3.5 usa uma distribuição do Hadoop baseada no [Hortonworks Data Platform 2.5](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.5.0/bk_release-notes/content/ch_relnotes_v250.html). Versão 3.5 do cluster HDInsight é hello _padrão_ cluster Hadoop que é criado no hello portal do Azure.
* O cluster HDInsight versão 3.4 usa uma distribuição do Hadoop baseada em [Hortonworks Data Platform 2.4](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html).
* O cluster HDInsight versão 3.3 usa uma distribuição do Hadoop baseada em [Hortonworks Data Platform 2.3](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html).

  * [Notas de versão do Apache Storm](https://storm.apache.org/2015/11/05/storm0100-released.html) estão disponíveis no site do Apache hello.
  * [Notas de versão do Apache Hive](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12332384&styleName=Text&projectId=12310843) estão disponíveis no site do Apache hello.
* O cluster do HDInsight versão 3.2 usa uma distribuição do Hadoop baseada no [Hortonworks Data Platform 2.2][hdp-2-2].

  * Notas de versão para componentes específicos do Apache estão disponíveis conforme a seguir: [Hive 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310843&version=12326450), [Pig 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310730&version=12326954), [HBase 0.98.4](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310753&version=12326810), [Phoenix 4.2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12315120&version=12327581), [M/R 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310941&version=12327180), [HDFS 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310942&version=12327181), [YARN 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12313722&version=12327197), [Common](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310240&version=12327179), [Tez 0.5.2](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314426&version=12328742), [Ambari 2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12312020&version=12327486), [Storm 0.9.3](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314820&version=12327112) e [Oozie 4.1.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12324960&projectId=12311620).
* O cluster HDInsight versão 3.1 usa uma distribuição do Hadoop baseada no [Hortonworks Data Platform 2.1.7][hdp-2-1-7]. Os clusters do HDInsight 3.1 criados antes de 7 de novembro de 2014 são baseados no [Hortonworks Data Platform 2.1.1][hdp-2-1-1].
* O cluster do HDInsight versão 3.0 usa uma distribuição do Hadoop baseada no [Hortonworks Data Platform 2.0][hdp-2-0-8].
* O cluster do HDInsight versão 2.1 usa uma distribuição do Hadoop baseada no [Hortonworks Data Platform 1.3][hdp-1-3-0].
* O cluster do HDInsight versão 1.6 usa uma distribuição do Hadoop baseada no [Hortonworks Data Platform 1.1][hdp-1-1-0].

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard e HDInsight Premium

HDInsight do Azure fornece ofertas de nuvem Olá grandes dados em duas categorias: _padrão_ e _Premium_. Olá, tabela a seguir lista recursos que estão disponíveis _somente_ do HDInsight Premium. Recursos que não são descritos na tabela Olá explicitamente estão disponíveis em HDInsight Standard e Premium.

> [!NOTE]
> Olá oferta do HDInsight Premium está atualmente na visualização e está disponível somente para clusters do Linux.

| Recurso do HDInsight Premium | Descrição |
| --- | --- |
| Clusters HDInsight ingressados no domínio |Ingresse em domínios do HDInsight clusters tooAzure do Active Directory (AD do Azure) para segurança de nível empresarial. No HDInsight Premium, você pode configurar uma lista de funcionários de sua empresa que pode autenticar por meio do AD do Azure toolog no cluster do HDInsight tooan. Olá administrador de empresa pode configurar o controle de acesso baseado em função de segurança do Hive usando [Apache Ranger](http://hortonworks.com/apache/ranger/) e restringir toouse de acesso de dados conforme necessário. Finalmente, Olá administrador pode fazer auditoria de dados acessados pelos funcionários e as políticas, assim, atingir um alto grau de controle de seus recursos corporativos de controle de alterações tooaccess. Para obter mais informações, consulte [Configurar clusters HDInsight ingressados em domínio](hdinsight-domain-joined-configure.md). |

### <a name="cluster-types-supported-in-hdinsight-premium"></a>Tipos de cluster com suporte no HDInsight Premium
Olá, tabela a seguir lista os tipos de cluster Olá têm suporte no HDInsight Premium.

| Tipo de cluster | Standard | Premium (Visualização) |
| --- | --- | --- |
| O Hadoop |Sim |Sim (somente HDInsight 3.6) |
| Spark |Sim |Não |
| HBase |Sim |Não |
| Storm |Sim |Não |
| Servidor R |Sim |Não |
| Hive Interativo (versão prévia) |Sim |Não |
| Kafka (Versão prévia) |Sim |Não | 

### <a name="support-for-azure-data-lake-store-in-hdinsight-premium"></a>Suporte para Azure Data Lake Store no HDInsight Premium

Clusters HDInsight Premium não dão suporte ao uso do Azure Data Lake Store como armazenamento primário. No entanto, você pode usar o Azure Data Lake Store como armazenamento de complemento com clusters HDInsight Premium.

### <a name="pricing-and-sla"></a>Preço e SLA
Para obter informações sobre preços e SLA para o HDInsight Premium, consulte [preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="default-node-configuration-and-virtual-machine-sizes-for-clusters"></a>Tamanhos de máquina virtual e configuração de nó de padrão para clusters
Olá tamanhos de máquina virtual (VM) tabelas lista saudação padrão para clusters de HDInsight a seguir.

> [!IMPORTANT]
> Se você precisa de mais de 32 nós de trabalho em um cluster, você precisa selecionar um tamanho de nó de cabeçalho com pelo menos 8 núcleos e 14 GB de RAM.
> 
> 

* Todas as regiões com suporte, exceto Sul do Brasil e Oeste do Japão:

  | Tipo de cluster | O Hadoop | HBase | Storm | Spark | Servidor R |
  | --- | --- | --- | --- | --- | --- |
  | Cabeçalho: tamanho padrão da VM |D3 v2 |D3 v2 |A3 |D12 v2 |D12 v2 |
  | Cabeçalho: tamanhos de VM recomendados |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |A3, A4, A5 |D12 v2, D13 v2, D14 v2 |D12 v2, D13 v2, D14 v2 |
  | Trabalho: tamanho de VM padrão |D3 v2 |D3 v2 |D3 v2 |Windows: D12 v2; Linux: D4 v2 |Windows: D12 v2; Linux: D4 v2 |
  | Trabalho: tamanhos de VM recomendados |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |
  | Zookeeper: tamanho de VM padrão | |A3 |A2 | | |
  | Zookeeper: tamanhos de VM recomendados | |A3, A4, A5 |A2, A3, A4 | | |
  | Borda: tamanho padrão da VM | | | | |Windows: D12 v2; Linux: D4 v2 |
  | Borda: tamanho de VM recomendado | | | | |Windows: D12 v2, D13 v2, D14 v2; Linux: D4 v2, D12 v2, D13 v2, D14 v2 |
* Apenas Sul do Brasil e Oeste do Japão (sem tamanhos v2):

  | Tipo de cluster | O Hadoop | HBase | Storm | Spark | Servidor R |
  | --- | --- | --- | --- | --- | --- |
  | Cabeçalho: tamanho padrão da VM |D3 |D3 |A3 |D12 |D12 |
  | Cabeçalho: tamanhos de VM recomendados |D3, D4, D12 |D3, D4, D12 |A3, A4, A5 |D12, D13, D14 |D12, D13, D14 |
  | Trabalho: tamanho de VM padrão |D3 |D3 |D3 |Windows: D12; Linux: D4 |Windows: D12; Linux: D4 |
  | Trabalho: tamanhos de VM recomendados |D3, D4, D12 |D3, D4, D12 |D3, D4, D12 |Windows: D12, D13, D14; Linux: D4, D12, D13, D14 |Windows: D12, D13, D14; Linux: D4, D12, D13, D14 |
  | Zookeeper: tamanho de VM padrão | |A2 |A2 | | |
  | Zookeeper: tamanhos de VM recomendados | |A2, A3, A4 |A2, A3, A4 | | |
  | Borda: tamanhos padrão da VM | | | | |Windows: D12; Linux: D4 |
  | Borda: tamanhos de VM recomendados | | | | |Windows: D12, D13, D14; Linux: D4, D12, D13, D14 |

> [!NOTE]
> - Head é conhecido como *Nimbus* para Olá profusão de tipo de cluster.
> - Trabalho é conhecido como *Supervisor* para Olá profusão de tipo de cluster.
> - Trabalho é conhecido como *região* para Olá HBase tipo de cluster.

## <a name="next-steps"></a>Próximas etapas
- [Configuração de cluster para Hadoop, Spark e muito mais no HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
- [Trabalhar em Hadoop no HDInsight em um computador com Windows](hdinsight-hadoop-windows-tools.md)

[Supported HDInsight versions]:(#supported-hdinsight-versions)

[image-hdi-versioning-versionscreen]: ./media/hdinsight-component-versioning/hdi-versioning-version-screen.png

[wa-forums]: http://azure.microsoft.com/support/forums/

[connect-excel-with-hive-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md

[hdp-2-2]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[ambari-docs]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[zookeeper]: http://zookeeper.apache.org/
