---
title: aaaConnect tooAzure SQL Data Warehouse - SSMS | Microsoft Docs
description: Use o SQL Server Management Studio (SSMS) tooconnect tooand consulta Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a>Conecte-se tooSQL Data Warehouse com o SQL Server Management Studio (SSMS)
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * 
            [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Use o SQL Server Management Studio (SSMS) tooconnect tooand consulta Azure SQL Data Warehouse. 

## <a name="prerequisites"></a>Pré-requisitos
toouse neste tutorial, você precisa:

* Um SQL Data Warehouse existente. toocreate um, consulte [criar um SQL Data Warehouse][Create a SQL Data Warehouse].
* SSMS (SQL Server Management Studio) instalado. [Instale o SSMS][Install SSMS] gratuitamente se você ainda não o tiver.
* Olá totalmente qualificado o nome do SQL server. toofind isso, consulte [conectar tooSQL Data Warehouse][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. Conecte-se tooyour SQL Data Warehouse
1. Abra o SSMS.
2. Abrir Pesquisador de Objetos. toodo, selecione **arquivo** > **conectar Pesquisador**.
   
    ![Pesquisador de Objetos do SQL Server][1]
3. Preencha os campos de saudação na janela de tooServer conectar hello.
   
    ![Conecte-se tooServer][2]
   
   * **Nome do servidor**. Digite hello **nome do servidor** identificado anteriormente.
   * **Autenticação**. Selecione **Autenticação do SQL Server** ou **Autenticação Integrada do Active Directory**.
   * **Nome de Usuário** e **Senha**. Insira o nome de usuário e senha se a Autenticação do SQL Server foi selecionada acima.
   * Clique em **Conectar**.
4. tooexplore, expanda seu servidor do SQL Azure. Você pode exibir bancos de dados de saudação associados ao servidor de saudação. Expanda as tabelas de saudação do AdventureWorksDW toosee em seu banco de dados de exemplo.
   
    ![Explorar o AdventureWorksWeb][3]

## <a name="2-run-a-sample-query"></a>2. Executar uma consulta de exemplo
Agora que uma conexão foi estabelecida tooyour banco de dados, vamos escrever uma consulta.

1. Clique com o botão direito do mouse em seu banco de dados no Gerenciador de Objetos do SQL Server.
2. Selecione **Nova Consulta**. Uma nova janela de consulta é aberta.
   
    ![Nova Consulta][4]
3. Copie esta consulta TSQL na janela de consulta hello:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Execute consulta hello. toodo, clique `Execute` ou use Olá atalho a seguir: `F5`.
   
    ![Executar consulta][5]
5. Examine os resultados da consulta hello. Neste exemplo, a tabela de FactInternetSales de saudação tem 60398 linhas.
   
    ![Resultados da consulta][6]

## <a name="next-steps"></a>Próximas etapas
Agora que você pode se conectar e consultar, tente [visualizando dados Olá com PowerBI][visualizing hello data with PowerBI].

tooconfigure seu ambiente para a autenticação do Active Directory do Azure, consulte [autenticar tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
