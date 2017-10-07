---
title: aaaVisualize dados do SQL Data Warehouse com o Power BI Microsoft Azure
description: Visualizar os dados do SQL Data Warehouse com o Power BI
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a>Visualizar os dados com o Power BI
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * 
            [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Este tutorial mostra como toouse Power BI tooconnect tooSQL Data Warehouse e criar algumas visualizações básico.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
toostep este tutorial, você precisa:

* Um SQL Data Warehouse pré-carregados com o banco de dados do hello AdventureWorksDW. tooprovision isso, consulte [criar um SQL Data Warehouse] [ Create a SQL Data Warehouse] e escolha dados de exemplo hello tooload. Se você já tiver um data warehouse, mas não tiver dados de exemplo, poderá [carregar dados de exemplo manualmente][load sample data manually].

## <a name="1-connect-tooyour-database"></a>1. Conecte-se o banco de dados tooyour
tooopen Power BI e conecte-se o banco de dados do AdventureWorksDW tooyour:

1. O logon no hello [portal do Azure][Azure portal].
2. Clique em **bancos de dados SQL** e escolha o banco de dados AdventureWorks do SQL Data Warehouse.
   
    ![Localize o banco de dados][1]
3. Clique o botão 'Abrir no Power BI' hello.
   
    ![Botão Power BI][2]
4. Agora você deve ver a página de conexão do SQL Data Warehouse Olá exibindo o endereço da web de banco de dados. Clique em Avançar.
   
    ![Conexão do Power BI][3]
5. Digite seu nome de usuário do SQL Azure server e a senha e você será o banco de dados do SQL Data Warehouse tooyour totalmente conectada.
   
    ![Entrada do Power BI][4]
6. Depois de ter entrado no Power BI, clique em Olá AdventureWorksDW dataset na folha de saudação à esquerda. Isso abrirá o banco de dados de saudação.
   
    ![Abrir AdventureWorksDW no Power BI][5]

## <a name="2-create-a-report"></a>2. Criar um relatório
Você está agora pronto toouse Power BI tooanalyze seus dados de exemplo AdventureWorksDW. análise de saudação tooperform AdventureWorksDW tem uma exibição chamada AggregateSales. Essa exibição contém algumas das métricas-chave para a análise de vendas da empresa de saudação Olá Olá.

1. toocreate um mapa da quantidade de vendas de acordo com o código de toopostal, no painel de campos à direita do hello, clique em Olá AggregateSales exibição tooexpand-lo. Clique em tooselect de colunas PostalCode e SalesAmount Olá-los.
   
    ![Selecionar AggregateSales no Power BI][6]
   
    O Power BI reconhecerá isso automaticamente como dados geográficos e os colocará em um mapa para você.
   
    ![Mapa do Power BI][7]
2. Esta etapa cria um gráfico de barras que mostra o valor de vendas por receita de cliente. toocreate este toohello vá expandido AggregateSales exibição. Clique em campo SalesAmount de saudação. Arraste Olá renda campo toohello esquerda e soltá-lo em um eixo.
   
    ![Selecionar eixo no Power BI][8]
   
    Mudamos gráfico de barras Olá sobre Olá esquerda.
   
    ![Barra do Power BI][9]
3. Esta etapa cria um gráfico de linhas que mostra o valor de vendas por data do pedido. toocreate este toohello vá expandido AggregateSales exibição. Clique em SalesAmount e em OrderDate. Na coluna de visualizações de saudação Clique ícone de gráfico de linhas de saudação; Este é o primeiro ícone de saudação na segunda linha hello em visualizações.
   
    ![Selecionar gráfico de linhas no Power BI][10]
   
    Agora você tem um relatório que mostra três visualizações diferentes de dados de saudação.
   
    ![Linha do Power BI][11]

Você pode salvar seu andamento a qualquer momento clicando em **Arquivo** e selecionando **Salvar**.

## <a name="next-steps"></a>Próximas etapas
Agora que damos você toowarm algum tempo para cima com dados de exemplo hello, consulte como muito[desenvolver][develop], [carregar][load], ou [ migrar][migrate]. Ou dar uma olhada Olá [site do Power BI][Power BI website].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
