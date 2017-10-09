---
title: "aaaData cenários que envolvem o repositório Data Lake | Microsoft Docs"
description: "Entender Olá cenários diferentes e ferramentas usando os dados que podem incluídos, processada, baixadas e visualizadas em um repositório Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 37409a71-a563-4bb7-bc46-2cbd426a2ece
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: caaa3979b8a2532089778c3e3db3c711714d3c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-data-lake-store-for-big-data-requirements"></a>Como usar o Repositório Data Lake do Azure para exigências de big data
Há quatro estágios principais no processamento de big data:

* Ingestão de grandes quantidades de dados em um repositório de dados, em tempo real ou em lotes
* Processamento de dados Olá
* Baixando dados saudação
* Visualizando dados saudação

Neste artigo, vamos examinar esses estágios com respeito tooAzure repositório Data Lake toounderstand Olá opções e ferramentas disponível toomeet suas necessidades de dados grandes.

## <a name="ingest-data-into-data-lake-store"></a>Ingerir dados no Repositório Data Lake
Esta seção destaca Olá diferentes fontes de dados e hello maneiras diferentes, na qual esses dados podem ser incluídos em uma conta do repositório Data Lake.

![Ingerir dados no Data Lake Store](./media/data-lake-store-data-scenarios/ingest-data.png "Ingerir dados no Data Lake Store")

### <a name="ad-hoc-data"></a>Dados ad hoc
Representam conjuntos de dados menores que são usados para criar protótipos de um aplicativo de big data. Há diferentes maneiras de ingestão de dados ad hoc dependendo da fonte de saudação de dados de saudação.

| Fonte de dados | Ingeri-la usando |
| --- | --- |
| Computador local |<ul> <li>[Portal do Azure](/data-lake-store-get-started-portal.md)</li> <li>[PowerShell do Azure](data-lake-store-get-started-powershell.md)</li> <li>[CLI 2.0 de plataforma cruzada do Azure](data-lake-store-get-started-cli-2.0.md)</li> <li>[Usando as ferramentas do Data Lake para o Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md) </li></ul> |
| Blob de Armazenamento do Azure |<ul> <li>[Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)</li> <li>[ferramenta AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[DistCp em execução no cluster HDInsight](data-lake-store-copy-data-wasb-distcp.md)</li> </ul> |

### <a name="streamed-data"></a>Dados transmitidos
Representam os dados que podem ser gerados por várias fontes, como aplicativos, dispositivos, sensores, etc. Esses dados podem ser ingeridos em um Repositório Data Lake por uma variedade de ferramentas. Essas ferramentas geralmente serão capturar e processar dados de saudação em uma base por evento em tempo real e depois escrever eventos Olá em lotes em repositório Data Lake para que possa ser processadas mais.

Veja as ferramentas que você pode usar:

* [O Azure Stream Analytics](../stream-analytics/stream-analytics-data-lake-output.md) -eventos incluídos em Hubs de eventos podem ser gravados tooAzure Data Lake usando uma saída do repositório Azure Data Lake.
* [Profusão de HDInsight do Azure](../hdinsight/hdinsight-storm-write-data-lake-store.md) -você pode gravar dados diretamente tooData Lake repositório do hello cluster Storm.
* [EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md) – você pode receber eventos de Hubs de eventos e, em seguida, grave-o repositório de Lake tooData usando Olá [Data Lake repositório .NET SDK](data-lake-store-get-started-net-sdk.md).

### <a name="relational-data"></a>Dados relacionais
Você também pode originar dados nos bancos de dados relacionais. Durante um período, os bancos de dados relacionais coletam grandes volumes de dados que podem fornecer informações importantes se processados por meio de um pipeline de big data. Você pode usar o hello toomove ferramentas a seguir esses dados no repositório Data Lake.

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)

### <a name="web-server-log-data-upload-using-custom-applications"></a>Dados de log do servidor Web (carregar usando aplicativos personalizados)
Esse tipo de conjunto de dados é abordado especificamente porque a análise de dados de log do servidor da web é um caso de uso comuns para aplicativos de dados grande e exige grandes volumes de toobe de arquivos de log carregados repositório toohello Data Lake. Você pode usar qualquer um dos Olá toowrite ferramentas a seguir tooupload seus próprios scripts ou aplicativos tais dados.

* [CLI 2.0 de plataforma cruzada do Azure](data-lake-store-get-started-cli-2.0.md)
* [PowerShell do Azure](data-lake-store-get-started-powershell.md)
* [SDK .NET do Repositório Azure Data Lake](data-lake-store-get-started-net-sdk.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)

Para carregar os dados de log do servidor web e também para carregar outros tipos de dados (por exemplo, dados opiniões social), é uma boa abordagem toowrite seus próprios scripts personalizados/aplicativos porque oferece Olá flexibilidade tooinclude seus dados carregando o componente como parte de seu aplicativo grande de dados maior. Em alguns casos esse código pode assumir a forma de saudação de um script ou o utilitário de linha de comando simples. Em outros casos, o código de saudação pode ser usado toointegrate grande processamento de dados em um aplicativo de negócios ou uma solução.

### <a name="data-associated-with-azure-hdinsight-clusters"></a>Dados associados aos clusters Azure HDInsight
A maioria dos tipos de cluster HDInsight (Hadoop, HBase, Storm) é compatível com o Repositório Data Lake como um repositório de armazenamento de dados. Os clusters HDInsight acessam dados dos WASB (Blobs de Armazenamento do Azure). Para obter melhor desempenho, você pode copiar dados de Olá de WASB em uma conta do repositório Data Lake associada Olá cluster. Você pode usar o hello seguintes ferramentas toocopy Olá dados.

* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)
* [Serviço AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
* [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)

### <a name="data-stored-in-on-premises-or-iaas-hadoop-clusters"></a>Dados armazenados localmente ou em clusters Hadoop da IaaS
É possível armazenar grandes quantidades de dados em clusters de Hadoop existentes, localmente em computadores que usam o HDFS. clusters de Hadoop Olá podem estar em uma implantação no local ou podem estar em um cluster de IaaS no Azure. Pode haver requisitos toocopy tal tooAzure dados repositório Data Lake uma abordagem única ou de forma recorrente. Há várias opções que você pode usar tooachieve isso. Abaixo está uma lista de alternativas e Olá associados vantagens e desvantagens.

| Abordagem | Detalhes | Vantagens | Considerações |
| --- | --- | --- | --- |
| Usar dados de toocopy da fábrica de dados do Azure (AAD) diretamente do Hadoop clusters tooAzure repositório Data Lake |[O ADF oferece suporte ao HDFS como uma fonte de dados](../data-factory/data-factory-hdfs-connector.md) |O ADF fornece suporte nativo para HDFS e gerenciamento e monitoramento de primeira classe completo |Requer toobe Data Management Gateway implantado no local ou em cluster de IaaS Olá |
| Exporte os dados do Hadoop como arquivos. Em seguida, copie Olá arquivos tooAzure repositório Data Lake usando o mecanismo apropriado. |Você pode copiar arquivos tooAzure repositório Data Lake usando: <ul><li>[Azure PowerShell para o sistema operacional Windows](data-lake-store-get-started-powershell.md)</li><li>[CLI 2.0 de plataforma cruzada do Azure para sistema operacional não Windows](data-lake-store-get-started-cli-2.0.md)</li><li>Aplicativo personalizado usando qualquer SDK do Data Lake Store</li></ul> |Tooget rápida é iniciado. Pode realizar carregamentos personalizados |Processo de várias etapas que envolve várias tecnologias. Gerenciamento e monitoramento crescerá toobe um desafio pela natureza de Olá personalizado de tempo dado das ferramentas de saudação |
| Use dados de toocopy Distcp de Hadoop tooAzure armazenamento. Copie dados do repositório do Azure Storage tooData Lake usando o mecanismo apropriado. |Você pode copiar dados de repositório do Azure Storage tooData Lake usando: <ul><li>[Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)</li><li>[ferramenta AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[Apache DistCp em execução em clusters do HDInsight](data-lake-store-copy-data-wasb-distcp.md)</li></ul> |Você pode usar ferramentas de software livre. |Processo de várias etapas que envolve várias tecnologias |

### <a name="really-large-datasets"></a>Conjuntos de dados realmente grandes
Para carregar conjuntos de dados que variam em vários terabytes, usando métodos Olá descritos acima, às vezes, é possível lenta e dispendiosa. Nesses casos, você pode usar opções de saudação abaixo.

* **Usando o ExpressRoute do Azure**. O Azure ExpressRoute permite criar conexões privadas entre os datacenters do Azure e a infraestrutura presente em seu local. Isso proporciona uma opção confiável para transferir grandes quantidades de dados. Para obter mais informações, confira a [documentação do ExpressRoute do Azure](../expressroute/expressroute-introduction.md).
* **Carregamento de dados "offline"**. Se a rota expressa do Azure não for possível usar por algum motivo, você pode usar [serviço de importação/exportação do Azure](../storage/common/storage-import-export-service.md) tooship unidades de disco rígido com seu dados tooan data center do Azure. Seus dados estão Blobs de armazenamento tooAzure carregado primeiro. Você pode usar [do Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) ou [AdlCopy ferramenta](data-lake-store-copy-data-azure-storage-blob.md) toocopy dados do repositório Azure armazenamento de Blobs tooData Lake.

  > [!NOTE]
  > Ao usar hello serviço de importação/exportação, tamanhos de arquivo hello em Olá discos que você enviar dados de tooAzure center não devem ser maiores que 195 GB.
  >
  >

## <a name="process-data-stored-in-data-lake-store"></a>Processar dados armazenados no Repositório Data Lake
Depois que os dados de saudação estão disponíveis no repositório Data Lake você pode executar análise em dados usando Olá suporte aplicativos de dados grande. No momento, você pode usar os trabalhos de análise de dados toorun HDInsight do Azure e análise do Azure Data Lake nos dados de saudação armazenados no repositório Data Lake.

![Analisar os dados no Data Lake Store](./media/data-lake-store-data-scenarios/analyze-data.png "Analisar os dados no Data Lake Store")

Você pode examinar Olá exemplos a seguir.

* [Criar um cluster HDInsight com o Repositório Data Lake como armazenamento](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Usar a Análise Data Lake do Azure com o Repositório Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

## <a name="download-data-from-data-lake-store"></a>Baixar dados do Repositório Data Lake
Você também pode ser toodownload ou mover dados de repositório Azure Data Lake para cenários como:

* Mova dados tooother repositórios toointerface com seus pipelines de processamento de dados existente. Por exemplo, você poderá toomove dados do repositório Data Lake tooAzure banco de dados SQL ou SQL Server local.
* Baixe o computador local do tooyour de dados para processamento em ambientes de IDE durante a criação de protótipos de aplicativo.

![Gerar dados no Data Lake Store](./media/data-lake-store-data-scenarios/egress-data.png "Gerar dados no Data Lake Store")

Nesses casos, você pode usar qualquer Olá as opções a seguir:

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)
* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)

Você também pode usar Olá toowrite métodos a seguir seus próprios dados do aplicativo de script/toodownload do repositório Data Lake.

* [CLI 2.0 de plataforma cruzada do Azure](data-lake-store-get-started-cli-2.0.md)
* [PowerShell do Azure](data-lake-store-get-started-powershell.md)
* [SDK .NET do Repositório Azure Data Lake](data-lake-store-get-started-net-sdk.md)

## <a name="visualize-data-in-data-lake-store"></a>Visualizar dados no Repositório Data Lake
Você pode usar uma combinação de serviços toocreate representações dos dados armazenados no repositório Data Lake.

![Visualizar dados no Data Lake Store](./media/data-lake-store-data-scenarios/visualize-data.png "Visualizar dados no Data Lake Store")

* Você pode iniciar usando [dados do Azure Data Factory toomove do repositório Data Lake tooAzure SQL Data Warehouse](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)
* Depois disso, você pode [integrar o Power BI com o Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-integrate-power-bi.md) toocreate a representação visual dos dados de saudação.
