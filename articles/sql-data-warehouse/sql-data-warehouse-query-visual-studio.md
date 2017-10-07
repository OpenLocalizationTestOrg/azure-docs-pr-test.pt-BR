---
title: aaaConnect tooAzure SQL Data Warehouse - VSTS | Microsoft Docs
description: Consultar o SQL Data Warehouse com o Visual Studio.
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a>Conecte-se tooSQL Data Warehouse com o Visual Studio e SSDT
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * 
            [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Use o Visual Studio tooquery Azure SQL Data Warehouse em apenas alguns minutos. Esse método usa a extensão do SQL Server Data Tools (SSDT) Olá no Visual Studio. 

## <a name="prerequisites"></a>Pré-requisitos
toouse neste tutorial, você precisa:

* Um SQL Data Warehouse existente. toocreate um, consulte [criar um SQL Data Warehouse][Create a SQL Data Warehouse].
* SSDT para Visual Studio. Se você tiver o Visual Studio, provavelmente já terá isso. Para obter instruções e opções de instalação, confira [Instalar o Visual Studio e o SSDT][Installing Visual Studio and SSDT].
* Olá totalmente qualificado o nome do SQL server. toofind isso, consulte [conectar tooSQL Data Warehouse][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. Conecte-se tooyour SQL Data Warehouse
1. Abra o Visual Studio 2013 ou 2015.
2. Abra o Pesquisador de Objetos do SQL Server. toodo, selecione **exibição** > **Pesquisador de objetos do SQL Server**.
   
    ![Pesquisador de Objetos do SQL Server][1]
3. Clique em Olá **adicionar SQL Server** ícone.
   
    ![Adicionar SQL Server][2]
4. Preencha os campos de saudação na janela de tooServer conectar hello.
   
    ![Conecte-se tooServer][3]
   
   * **Nome do servidor**. Digite hello **nome do servidor** identificado anteriormente.
   * **Autenticação**. Selecione **Autenticação do SQL Server** ou **Autenticação Integrada do Active Directory**.
   * **Nome de Usuário** e **Senha**. Insira o nome de usuário e senha se a Autenticação do SQL Server foi selecionada acima.
   * Clique em **Conectar**.
5. tooexplore, expanda seu servidor do SQL Azure. Você pode exibir bancos de dados de saudação associados ao servidor de saudação. Expanda as tabelas de saudação do AdventureWorksDW toosee em seu banco de dados de exemplo.
   
    ![Explorar o AdventureWorksWeb][4]

## <a name="2-run-a-sample-query"></a>2. Executar uma consulta de exemplo
Agora que uma conexão foi estabelecida tooyour banco de dados, vamos escrever uma consulta.

1. Clique com o botão direito do mouse em seu banco de dados no Gerenciador de Objetos do SQL Server.
2. Selecione **Nova Consulta**. Uma nova janela de consulta é aberta.
   
    ![Nova Consulta][5]
3. Copie esta consulta TSQL na janela de consulta hello:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Execute consulta hello. toodo isso, clique em seta Olá verde ou use Olá atalho a seguir: `CTRL` + `SHIFT` + `E`.
   
    ![Executar consulta][6]
5. Examine os resultados da consulta hello. Neste exemplo, a tabela de FactInternetSales de saudação tem 60398 linhas.
   
    ![Resultados da consulta][7]

## <a name="next-steps"></a>Próximas etapas
Agora que você pode se conectar e consultar, tente [visualizando dados Olá com PowerBI][visualizing hello data with PowerBI].

tooconfigure seu ambiente para a autenticação do Active Directory do Azure, consulte [autenticar tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
