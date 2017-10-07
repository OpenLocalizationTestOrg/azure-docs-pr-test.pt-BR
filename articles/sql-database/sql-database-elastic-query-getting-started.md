---
title: aaaReport em bancos de dados de nuvem expandido (particionamento horizontal) | Microsoft Docs
description: como toouse cruzada consultas de banco de dados do banco de dados
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a>Relatórios entre bancos de dados expandidos na nuvem (preview)
Você pode criar relatórios de vários bancos de dados do SQL Azure de um ponto de conexão única usando uma [consulta elástica](sql-database-elastic-query-overview.md). bancos de dados Olá devem ser particionados horizontalmente (também conhecido como "fragmentados").

Se você tiver um banco de dados existente, consulte [existente migrando bancos de dados de bancos de dados de saída tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).

objetos do SQL Olá toounderstand necessário tooquery, consulte [consultas em bancos de dados particionados horizontalmente](sql-database-elastic-query-horizontal-partitioning.md).

## <a name="prerequisites"></a>Pré-requisitos
Baixe e execute Olá [guia de Introdução com amostra das ferramentas de banco de dados Elástico](sql-database-elastic-scale-get-started.md).

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>Criar um mapa do fragmento manager usando o aplicativo de exemplo hello
Aqui você criará um mapa do fragmento manager juntamente com vários fragmentos, seguido de inserção de dados em fragmentos hello. Se você se deparar tooalready possuem instalação fragmentos com dados fragmentados, você pode ignorar Olá etapas a seguir e mover toohello próxima seção.

1. Compilar e executar Olá **Introdução às ferramentas de banco de dados Elástico** aplicativo de exemplo. Execute as etapas de saudação até a etapa 7 na seção Olá [Baixe e execute o aplicativo de exemplo hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app). No final da saudação da etapa 7, você verá saudação de prompt de comando a seguir:

    ![prompt de comando][1]
2. Na janela de comando hello, digite "1" e pressione **Enter**. Isso cria o Gerenciador do mapa de fragmentos Olá e adiciona dois servidores toohello de fragmentos. Em seguida, digite "3" e pressione **Enter**; repetir a ação de saudação quatro vezes. Isso insere linhas de dados de exemplo no seus fragmentos.
3. Olá [portal do Azure](https://portal.azure.com) devem mostrar três novos bancos de dados em seu servidor:

   ![Confirmação do Visual Studio][2]

   Neste ponto, as consultas de bancos de dados têm suporte por meio de bibliotecas de cliente do banco de dados Elástico hello. Por exemplo, use a opção 4 na janela de comando hello. resultados de saudação de uma consulta de vários fragmento são sempre um **UNION ALL** dos resultados de saudação de todos os fragmentos.

   Na próxima seção, Olá, podemos criar um ponto de extremidade de banco de dados de exemplo que oferece suporte a consultas mais sofisticadas de dados de saudação em fragmentos.

## <a name="create-an-elastic-query-database"></a>Criar um banco de dados de consulta elástico
1. Olá abrir [portal do Azure](https://portal.azure.com) e faça logon.
2. Criar um novo banco de dados do SQL Azure no hello mesmo servidor como sua configuração de fragmento. Nome do banco de dados hello "ElasticDBQuery".

    ![Portal do Azure e camada de preços][3]

    > [!NOTE]
    > você pode usar um banco de dados existente. Se você pode fazer isso, ele não deve ser um dos fragmentos de saudação que deseja tooexecute suas consultas em. Este banco de dados será usado para criar objetos de metadados para uma consulta de banco de dados Elástico de saudação.
    >

## <a name="create-database-objects"></a>Criar objetos de banco de dados
### <a name="database-scoped-master-key-and-credentials"></a>Chave mestra do escopo do banco de dados e credenciais
Estes são Gerenciador do mapa do fragmento usado tooconnect toohello e fragmentos de saudação:

1. Abra o SQL Server Management Studio ou o SQL Server Data Tools no Visual Studio.
2. Conecte-se o banco de dados tooElasticDBQuery e execute Olá comandos T-SQL a seguir:

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    "username" e "password" deve ser Olá mesmo como informações de logon usadas na etapa 6 de [Baixe e execute o aplicativo de exemplo hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) na [Introdução às ferramentas de banco de dados Elástico](sql-database-elastic-scale-get-started.md).

### <a name="external-data-sources"></a>Fontes de dados externas
toocreate uma fonte de dados externa, execute Olá comando a seguir no banco de dados de ElasticDBQuery hello:

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 "CustomerIDShardMap" é o nome de saudação do mapa do fragmento hello, se você criou o mapa do fragmento hello e o mapa do fragmento manager usando o exemplo de ferramentas de banco de dados Elástico hello. No entanto, se você usou a configuração personalizada para este exemplo, ele deve ser nome do mapa de fragmentos Olá escolhido em seu aplicativo.

### <a name="external-tables"></a>Tabelas externas
Crie uma tabela externa que coincide com a tabela de clientes de saudação em fragmentos Olá executando o comando a seguir no banco de dados ElasticDBQuery de saudação:

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Executar uma consulta T-SQL no banco de dados elástico de exemplo
Depois que tiver definido sua fonte de dados e tabelas externas, agora você poderá usar o T-SQL completo nas tabelas externas.

Execute esta consulta no banco de dados de ElasticDBQuery hello:

    select count(CustomerId) from [dbo].[Customers]

Você notará que consultam Olá agrega os resultados de todos os fragmentos de saudação e fornece Olá saída a seguir:

![Detalhes de saída][4]

## <a name="import-elastic-database-query-results-tooexcel"></a>Importar tooExcel de resultados de consulta de banco de dados Elástico
 Você pode importar resultados de saudação de um consulta tooan do arquivo de Excel.

1. Inicie o Excel 2013.
2. Navegue toohello **dados** faixa de opções.
3. Clique em **De Outras Fontes** e em **Do SQL Server**.

   ![Importação de outras fontes para o Excel][5]
4. Em Olá **Assistente de Conexão de dados** digite credenciais de nome e logon do servidor de saudação. Em seguida, clique em **Próximo**.
5. Na caixa de diálogo Olá **banco de dados Olá Select que contém dados Olá deseja**, selecione Olá **ElasticDBQuery** banco de dados.
6. Selecione Olá **clientes** tabela na exibição de lista hello e clique em **próximo**. Em seguida, clique em **Concluir**.
7. Em Olá **importar dados** formulário, em **selecione como deseja tooview esses dados na pasta de trabalho**, selecione **tabela** e clique em **Okey**.

Todos os Olá linhas de **clientes** tabela, armazenada em fragmentos diferentes preencher a planilha do Excel hello.

Agora você pode usar funções avançadas de visualização de dados do Excel. Você pode usar a cadeia de caracteres de conexão de saudação com seu nome de servidor, nome do banco de dados e credenciais tooconnect seu dados e BI integração ferramentas toohello Elástico consultar banco de dados. Certifique-se de que o SQL Server tem suporte como uma fonte de dados para a ferramenta. Você pode consultar o banco de dados de consulta Elástico toohello e tabelas externas, assim como qualquer outro banco de dados do SQL Server e tabelas do SQL Server que você se conectaria toowith sua ferramenta.

### <a name="cost"></a>Custo
Não há nenhum custo adicional para usar o recurso de consulta de banco de dados Elástico Olá.

Para obter informações sobre os preços, consulte [Detalhes de preços do Banco de Dados SQL](https://azure.microsoft.com/pricing/details/sql-database/).

## <a name="next-steps"></a>Próximas etapas

* Para obter uma visão geral de consulta elástica, veja [Visão geral de consulta elástica](sql-database-elastic-query-overview.md).
* Para obter um tutorial sobre particionamento vertical, veja [Introdução à consulta entre bancos de dados (particionamento vertical)](sql-database-elastic-query-getting-started-vertical.md).
* Para sintaxe e exemplos de consultas para dados particionados verticalmente, veja [Consulta de dados particionados verticalmente](sql-database-elastic-query-vertical-partitioning.md)
* Para sintaxe e exemplos de consultas para dados particionados horizontalmente, veja [Consulta de dados particionados horizontalmente](sql-database-elastic-query-horizontal-partitioning.md)
* Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução Transact-SQL em um único Banco de Dados SQL do Azure remoto ou um conjunto de bancos de dados que serve como fragmentos em um esquema de particionamento horizontal.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
