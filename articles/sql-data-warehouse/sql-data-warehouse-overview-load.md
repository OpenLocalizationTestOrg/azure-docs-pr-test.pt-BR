---
title: dados de aaaLoad no Azure SQL Data Warehouse | Microsoft Docs
description: "Saiba mais cenários comuns de saudação para carregamento no SQL Data Warehouse de dados. Essas opções incluem usar PolyBase, armazenamento de blobs do Azure, arquivos simples e envio de disco. Você também pode usar ferramentas de terceiros."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a>Carregar dados no SQL Data Warehouse do Azure
Um resumo das opções de cenário hello e recomendações para carregar dados no SQL Data Warehouse.

Olá mais difícil de carregamento de dados geralmente está preparando dados saudação para carga de saudação. Carregamento simplifica o Azure usando o armazenamento de BLOBs do Azure como um repositório de dados comum para muitos serviços Olá e usando o Azure Data Factory tooorchestrate a movimentação de dados e comunicação entre Olá serviços do Azure. Esses processos são integrados com a tecnologia PolyBase que usa processamento altamente paralelo dados de tooload (MPP) em paralelo do armazenamento de BLOBs do Azure no SQL Data Warehouse. 

Para ver os tutoriais que carregam bancos de dados de exemplo, consulte [Carregar bancos de dados de exemplo][Load sample databases].

## <a name="load-from-azure-blob-storage"></a>Carregar por meio do armazenamento de blobs do Azure
tooimport dados de maneira mais rápidos de saudação no SQL Data Warehouse são toouse dados tooload do armazenamento de BLOBs do Azure. PolyBase usa SQL Data Warehouse processamento altamente paralelo dados de tooload de design (MPP) em paralelo do armazenamento de BLOBs do Azure. toouse PolyBase, você pode usar os comandos T-SQL ou um pipeline da fábrica de dados do Azure.

### <a name="1-use-polybase-and-t-sql"></a>1. Usar PolyBase e T-SQL
Resumo do processo de carregamento:

1. Mover o armazenamento de blob de tooAzure de dados ou o repositório Azure Data Lake e armazená-lo em arquivos de texto.
2. Configurar objetos externos no local do SQL Data Warehouse toodefine hello e formato de dados de saudação
3. Execute um T-SQL comando tooload Olá de dados em paralelo em uma nova tabela de banco de dados.

<!-- 5. Schedule and run a loading job. --> 

Para obter um tutorial, consulte [carregar dados de armazenamento de BLOBs do Azure tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="2-use-azure-data-factory"></a>2. Usar o Azure Data Factory
Para um toouse de maneira mais simples do PolyBase, você pode criar um pipeline da fábrica de dados do Azure que usa dados tooload do armazenamento de BLOBs do Azure no SQL Data Warehouse. Isso é rápido tooconfigure como objetos de T-SQL Olá toodefine não é necessário. Se você precisar de dados externos de saudação tooquery sem importá-lo, use T-SQL. 

Resumo do processo de carregamento:

1. Mover o armazenamento de blob de tooAzure de dados e armazená-lo em arquivos de texto. O Azure Data Factory atualmente não dá suporte à conectividade ADLS com PolyBase).
2. Crie um pipeline do Azure Data Factory tooingest Olá dados. Use a opção de PolyBase de saudação.
4. Agendar e executar o pipeline de saudação.

Para obter um tutorial, consulte [carregar dados de armazenamento de BLOBs do Azure tooSQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].

## <a name="load-from-sql-server"></a>Carregar do SQL Server
dados de tooload de tooSQL do SQL Server Data Warehouse, você pode usar o Integration Services (SSIS), transferência de arquivos simples ou enviar tooMicrosoft de discos. Ler em toosee um resumo da saudação diferente carregar tootutorials processos e links.

tooplan uma migração de dados completo do SQL Server tooSQL Data Warehouse, consulte Olá [visão geral da migração][Migration overview]. 

### <a name="use-integration-services-ssis"></a>Usar o SSIS (Integration Services)
Se você já estiver usando tooload de pacotes do Integration Services (SSIS) no SQL Server, você pode atualizar seu toouse de pacotes do SQL Server como origem hello e SQL Data Warehouse como destino de saudação. Isso é rápido e fácil toodo, e é uma boa opção se estiver tentando toomigrate não o carregamento de dados toouse já na nuvem de saudação do processo. compensação de saudação é carga Olá será mais lenta do que o PolyBase porque esse SSIS não executa Olá carga em paralelo.

Resumo do processo de carregamento:

1. Revise sua instância de SQL Server Integration Services pacote toopoint toohello para fonte hello e Olá o banco de dados de SQL Data Warehouse para o destino de saudação.
2. Migre seu tooSQL de esquema do Data Warehouse, se ainda não estiver lá.
3. Mapeamento de saudação de alteração em seus pacotes use somente tipos de dados Olá que são suportados pelo SQL Data Warehouse.
4. Agendar e executar o pacote de saudação.

Para obter um tutorial, consulte [carregar dados do SQL Server tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].

### <a name="use-azcopy-recommended-for--10-tb-data"></a>Usar o AZCopy (recomendado para < 10 TB de dados)
Se o tamanho de dados é < 10 TB, você pode exportar dados de saudação do arquivos de tooflat do SQL Server, copie o armazenamento de blob Olá arquivos tooAzure e, em seguida, usar dados tooload Olá no SQL Data Warehouse

Resumo do processo de carregamento:

1. Use dados de tooexport de utilitário de linha de comando do hello bcp de arquivos de tooflat do SQL Server.
2. Use Olá AZCopy utilitário de linha de comando toocopy dados do armazenamento de blob de tooAzure de arquivos simples.
3. Use tooload PolyBase no SQL Data Warehouse.

Para obter um tutorial, consulte [carregar dados de armazenamento de BLOBs do Azure tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="use-bcp"></a>Usar o bcp
Se você tiver uma pequena quantidade de dados, você pode usar bcp tooload diretamente no Azure SQL Data Warehouse.

Resumo do processo de carregamento:

1. Use dados de tooexport de utilitário de linha de comando do hello bcp de arquivos de tooflat do SQL Server.
2. Usar bcp tooload dados de simples diretamente arquivos tooSQL Data Warehouse.

Para obter um tutorial, consulte [carregar dados do SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].

### <a name="use-importexport-recommended-for--10-tb-data"></a>Usar Importar/Exportar (recomendado para > 10 TB de dados)
Se o tamanho dos dados é > 10 TB e você desejar toomove-tooAzure, recomendamos que você use nosso serviço de envio de disco [importação/exportação][Import/Export]. 

Resumo do processo de carregamento

1. Use dados de tooexport de utilitário de linha de comando do hello bcp de arquivos do SQL Server tooflat em discos transferível.
2. Remeter saudação discos tooMicrosoft.
3. Microsoft carrega dados saudação em SQL Data Warehouse

## <a name="load-from-hdinsight"></a>Carregar do HDInsight
O SQL Data Warehouse dá suporte ao carregamento de dados do HDInsight via PolyBase. processo de saudação é Olá mesmo que o carregamento de dados de armazenamento de BLOBs do Azure - usando PolyBase tooconnect tooHDInsight tooload dados. 

### <a name="1-use-polybase-and-t-sql"></a>1. Usar PolyBase e T-SQL
Resumo do processo de carregamento:

1. Mover tooHDInsight seus dados e armazená-lo em arquivos de texto, formato ORC ou Parquet.
2. Configure objetos externos no local do SQL Data Warehouse toodefine hello e formato de dados de saudação.
3. Execute um T-SQL comando tooload Olá de dados em paralelo em uma nova tabela de banco de dados.

Para obter um tutorial, consulte [carregar dados de armazenamento de BLOBs do Azure tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

## <a name="recommendations"></a>Recomendações
Muitos de nossos parceiros têm soluções de carregamento. toofind mais informações, consulte uma lista de nosso [parceiros de soluções][solution partners]. 

Se seus dados é proveniente de uma fonte não relacionais e você desejar tooload no SQL Data Warehouse você precisará tootransform-lo em linhas e colunas antes de carregá-lo. dados transformado de saudação não precisam toobe armazenado em um banco de dados, ele pode ser armazenado em arquivos de texto.

Crie estatísticas sobre os dados recém-carregados. O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou atualização automática.  Em ordem tooget Olá melhor desempenho de suas consultas, é importante primeiro carregar toocreate estatísticas em todas as colunas de todas as tabelas após hello ou alterações substanciais ocorrerem nos dados de saudação.  Para obter detalhes, confira [Estatísticas][Statistics].

## <a name="next-steps"></a>Próximas etapas
Para obter mais dicas de desenvolvimento, consulte Olá [visão geral do desenvolvimento][development overview].

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
