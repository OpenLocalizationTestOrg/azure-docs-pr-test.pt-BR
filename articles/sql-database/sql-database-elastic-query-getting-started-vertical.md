---
title: aaaGet iniciado com consultas de bancos de dados (particionamento vertical) | Microsoft Docs
description: "como a consulta de banco de dados Elástico toouse com particionado verticalmente bancos de dados"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: e5b44b10-c432-4f96-b20e-08615ff4d5dd
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: torsteng
ms.openlocfilehash: 9e6183268e8bf87e3ac28f502711fcc05a7a3f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a>Introdução às consultas entre bancos de dados (particionamento vertical) (preview)
Consulta de banco de dados Elástico (visualização) para o banco de dados SQL permite consultas do T-SQL toorun que abrangem vários bancos de dados usando um ponto de conexão única. Este tópico aplica-se muito[particionado verticalmente bancos de dados](sql-database-elastic-query-vertical-partitioning.md).  

Quando concluído, você verá: Saiba como tooconfigure e usar um banco de dados do Azure SQL tooperform as consultas que abrangem vários bancos de dados relacionados. 

Para obter mais informações sobre o recurso de consulta de banco de dados Elástico hello, consulte [visão geral de consulta de banco de dados Elástico de banco de dados do Azure SQL](sql-database-elastic-query-overview.md). 

## <a name="prerequisites"></a>Pré-requisitos

Você deve ter a permissão para ALTERAR QUALQUER FONTE DE DADOS EXTERNA. Essa permissão é incluída com a permissão ALTER DATABASE hello. Permissões ALTER ANY EXTERNAL DATA SOURCE são necessários toorefer toohello subjacente da fonte de dados.

## <a name="create-hello-sample-databases"></a>Criar hello bancos de dados de exemplo
toostart com, precisamos de dois bancos de dados de toocreate, **clientes** e **pedidos**, em Olá mesmos ou em diferentes servidores lógicos.   

Executar Olá consultas a seguir no hello **pedidos** saudação do banco de dados toocreate **OrderInformation** tabela e a entrada de dados de exemplo hello. 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

Agora, execute seguinte consulta no hello **clientes** saudação do banco de dados toocreate **CustomerInformation** tabela e a entrada de dados de exemplo hello. 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a>Criar objetos de banco de dados
### <a name="database-scoped-master-key-and-credentials"></a>Chave mestra e credenciais do escopo do banco de dados
1. Abra o SQL Server Management Studio ou o SQL Server Data Tools no Visual Studio.
2. Conecte-se o banco de dados de pedidos de toohello e execute Olá comandos T-SQL a seguir:
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    Olá "username" e "password" devem ser Olá nome de usuário e senha usada toologin no banco de dados de clientes hello.
    Atualmente não há suporte para a autenticação usando o Azure Active Directory com consultas elásticas.

### <a name="external-data-sources"></a>Fontes de dados externas
toocreate uma fonte de dados externa, execute Olá comando a seguir no banco de dados de pedidos de saudação: 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a>Tabelas externas
Crie uma tabela externa Olá pedidos banco de dados que corresponde a definição de saudação da tabela de CustomerInformation hello:

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Executar uma consulta T-SQL no banco de dados elástico de exemplo
Depois de definir a fonte de dados externa e suas tabelas externas, agora você pode usar tooquery T-SQL as tabelas externas. Execute esta consulta no banco de dados de pedidos de saudação: 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a>Custo
No momento, o recurso de consulta de banco de dados Elástico Olá está incluído nos custo de saudação do banco de dados SQL do Azure.  

Para saber mais sobre preços, consulte [Preços do Banco de Dados SQL](https://azure.microsoft.com/pricing/details/sql-database). 

## <a name="next-steps"></a>Próximas etapas

* Para obter uma visão geral de consulta elástica, consulte [Visão geral de consulta elástica](sql-database-elastic-query-overview.md).
* Para sintaxe e amostras de consultas para dados particionados verticalmente, consulte [Consultando dados particionados verticalmente)](sql-database-elastic-query-vertical-partitioning.md)
* Para um tutorial sobre particionamento horizontal (fragmentação), consulte [Introdução à consulta elástica para particionamento horizontal (fragmentação)](sql-database-elastic-query-getting-started.md).
* Para sintaxe e amostras de consultas para dados particionados horizontalmente, consulte [Consultando dados particionados horizontalmente)](sql-database-elastic-query-horizontal-partitioning.md)
* Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução Transact-SQL em um único Banco de Dados SQL do Azure remoto ou um conjunto de bancos de dados que serve como fragmentos em um esquema de particionamento horizontal.