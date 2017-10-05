---
title: Visualizar os dados do SQL Data Warehouse com o Power BI | Microsoft Azure
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
ms.openlocfilehash: a41393730143b14e91318a61858d989fff3786c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="51fbf-103">Visualizar os dados com o Power BI</span><span class="sxs-lookup"><span data-stu-id="51fbf-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="51fbf-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="51fbf-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * <span data-ttu-id="51fbf-105">
            [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="51fbf-105">[Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span></span>
> * [<span data-ttu-id="51fbf-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="51fbf-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="51fbf-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="51fbf-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="51fbf-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="51fbf-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="51fbf-109">Este tutorial mostra como usar o Power BI para se conectar ao SQL Data Warehouse e criar algumas visualizações básicas.</span><span class="sxs-lookup"><span data-stu-id="51fbf-109">This tutorial shows you how to use Power BI to connect to SQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="51fbf-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="51fbf-110">Prerequisites</span></span>
<span data-ttu-id="51fbf-111">Para acompanhar este tutorial, você precisará:</span><span class="sxs-lookup"><span data-stu-id="51fbf-111">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="51fbf-112">Um SQL Data Warehouse pré-carregado com o banco de dados AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="51fbf-112">A SQL Data Warehouse pre-loaded with the AdventureWorksDW database.</span></span> <span data-ttu-id="51fbf-113">Para provisionar isso, consulte [Criar um SQL Data Warehouse][Create a SQL Data Warehouse] e opte por carregar os dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="51fbf-113">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span></span> <span data-ttu-id="51fbf-114">Se você já tiver um data warehouse, mas não tiver dados de exemplo, poderá [carregar dados de exemplo manualmente][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="51fbf-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-to-your-database"></a><span data-ttu-id="51fbf-115">1. Conectar-se ao seu banco de dados</span><span class="sxs-lookup"><span data-stu-id="51fbf-115">1. Connect to your database</span></span>
<span data-ttu-id="51fbf-116">Para abrir o Power BI e conectar-se ao banco de dados AdventureWorksDW:</span><span class="sxs-lookup"><span data-stu-id="51fbf-116">To open Power BI and connect to your AdventureWorksDW database:</span></span>

1. <span data-ttu-id="51fbf-117">Faça logon no [Portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="51fbf-117">Sign into the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="51fbf-118">Clique em **bancos de dados SQL** e escolha o banco de dados AdventureWorks do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="51fbf-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![Localize o banco de dados][1]
3. <span data-ttu-id="51fbf-120">Clique no botão “Abrir no Power BI”.</span><span class="sxs-lookup"><span data-stu-id="51fbf-120">Click the 'Open in Power BI' button.</span></span>
   
    ![Botão Power BI][2]
4. <span data-ttu-id="51fbf-122">Agora você deve ver a página de conexão do SQL Data Warehouse exibindo o endereço Web do seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="51fbf-122">You should now see the SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="51fbf-123">Clique em Avançar.</span><span class="sxs-lookup"><span data-stu-id="51fbf-123">Click next.</span></span>
   
    ![Conexão do Power BI][3]
5. <span data-ttu-id="51fbf-125">Insira seu nome de usuário e senha do servidor do Azure SQL e você será totalmente conectado ao banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="51fbf-125">Enter your Azure SQL server username and password and you will be fully connected to your SQL Data Warehouse database.</span></span>
   
    ![Entrada do Power BI][4]
6. <span data-ttu-id="51fbf-127">Depois de entrar no Power BI, clique no conjunto de dados do AdventureWorksDW na folha esquerda.</span><span class="sxs-lookup"><span data-stu-id="51fbf-127">Once you have signed into Power BI, click the AdventureWorksDW dataset on the left blade.</span></span> <span data-ttu-id="51fbf-128">Isso abrirá o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="51fbf-128">This will open the database.</span></span>
   
    ![Abrir AdventureWorksDW no Power BI][5]

## <a name="2-create-a-report"></a><span data-ttu-id="51fbf-130">2. Criar um relatório</span><span class="sxs-lookup"><span data-stu-id="51fbf-130">2. Create a report</span></span>
<span data-ttu-id="51fbf-131">Agora você está pronto para usar o Power BI para analisar os dados de exemplo do AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="51fbf-131">You are now ready to use Power BI to analyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="51fbf-132">Para executar a análise, o AdventureWorksDW possui uma exibição chamada AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="51fbf-132">To perform the analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="51fbf-133">Essa exibição contém algumas das principais métricas para analisar as vendas da empresa.</span><span class="sxs-lookup"><span data-stu-id="51fbf-133">This view contains a few of the key metrics for analyzing the sales of the company.</span></span>

1. <span data-ttu-id="51fbf-134">Para criar um mapa do valor de vendas de acordo com o CEP, clique no painel de campos à direita, clique na exibição AggregateSales para expandi-la.</span><span class="sxs-lookup"><span data-stu-id="51fbf-134">To create a map of sales amount according to postal code, in the right-hand fields pane, click the AggregateSales view to expand it.</span></span> <span data-ttu-id="51fbf-135">Clique nas colunas PostalCode e SalesAmount para selecioná-las.</span><span class="sxs-lookup"><span data-stu-id="51fbf-135">Click the PostalCode and SalesAmount columns to select them.</span></span>
   
    ![Selecionar AggregateSales no Power BI][6]
   
    <span data-ttu-id="51fbf-137">O Power BI reconhecerá isso automaticamente como dados geográficos e os colocará em um mapa para você.</span><span class="sxs-lookup"><span data-stu-id="51fbf-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Mapa do Power BI][7]
2. <span data-ttu-id="51fbf-139">Esta etapa cria um gráfico de barras que mostra o valor de vendas por receita de cliente.</span><span class="sxs-lookup"><span data-stu-id="51fbf-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="51fbf-140">Para criar isso, vá para a exibição expandida AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="51fbf-140">To create this go to the expanded AggregateSales view.</span></span> <span data-ttu-id="51fbf-141">Clique no campo SalesAmount.</span><span class="sxs-lookup"><span data-stu-id="51fbf-141">Click the SalesAmount field.</span></span> <span data-ttu-id="51fbf-142">Arraste o campo Receita de Cliente para a esquerda e solte-o no Eixo.</span><span class="sxs-lookup"><span data-stu-id="51fbf-142">Drag the Customer Income field to the left and drop it into Axis.</span></span>
   
    ![Selecionar eixo no Power BI][8]
   
    <span data-ttu-id="51fbf-144">Mudamos o gráfico de barras para o lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="51fbf-144">We moved the bar chart over the left.</span></span>
   
    ![Barra do Power BI][9]
3. <span data-ttu-id="51fbf-146">Esta etapa cria um gráfico de linhas que mostra o valor de vendas por data do pedido.</span><span class="sxs-lookup"><span data-stu-id="51fbf-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="51fbf-147">Para criar isso, vá para a exibição expandida AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="51fbf-147">To create this go to the expanded AggregateSales view.</span></span> <span data-ttu-id="51fbf-148">Clique em SalesAmount e em OrderDate.</span><span class="sxs-lookup"><span data-stu-id="51fbf-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="51fbf-149">Na coluna Visualizações, clique no ícone Gráfico de Linhas; é o primeiro ícone na segunda linha sob visualizações.</span><span class="sxs-lookup"><span data-stu-id="51fbf-149">In the Visualizations column click the Line Chart icon; this is the first icon in the second line under visualizations.</span></span>
   
    ![Selecionar gráfico de linhas no Power BI][10]
   
    <span data-ttu-id="51fbf-151">Agora você tem um relatório que mostra três visualizações diferentes dos dados.</span><span class="sxs-lookup"><span data-stu-id="51fbf-151">You now have a report that shows three different visualizations of the data.</span></span>
   
    ![Linha do Power BI][11]

<span data-ttu-id="51fbf-153">Você pode salvar seu andamento a qualquer momento clicando em **Arquivo** e selecionando **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="51fbf-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51fbf-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="51fbf-154">Next steps</span></span>
<span data-ttu-id="51fbf-155">Agora que proporcionamos a você uma introdução à verificação de dados de exemplo, confira como [desenvolver][develop], [carregar][load] ou [migrar][migrate].</span><span class="sxs-lookup"><span data-stu-id="51fbf-155">Now that we've given you some time to warm up with the sample data, see how to [develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="51fbf-156">Ou confira o [Site do Power BI][Power BI website].</span><span class="sxs-lookup"><span data-stu-id="51fbf-156">Or take a look at the [Power BI website][Power BI website].</span></span>

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
[connecting to SQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
