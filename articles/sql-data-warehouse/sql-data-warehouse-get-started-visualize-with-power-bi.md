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
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="5d5cc-103">Visualizar os dados com o Power BI</span><span class="sxs-lookup"><span data-stu-id="5d5cc-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5d5cc-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="5d5cc-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * <span data-ttu-id="5d5cc-105">
            [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="5d5cc-105">[Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span></span>
> * [<span data-ttu-id="5d5cc-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5d5cc-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="5d5cc-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="5d5cc-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="5d5cc-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="5d5cc-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="5d5cc-109">Este tutorial mostra como toouse Power BI tooconnect tooSQL Data Warehouse e criar algumas visualizações básico.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-109">This tutorial shows you how toouse Power BI tooconnect tooSQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="5d5cc-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5d5cc-110">Prerequisites</span></span>
<span data-ttu-id="5d5cc-111">toostep este tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="5d5cc-111">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="5d5cc-112">Um SQL Data Warehouse pré-carregados com o banco de dados do hello AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-112">A SQL Data Warehouse pre-loaded with hello AdventureWorksDW database.</span></span> <span data-ttu-id="5d5cc-113">tooprovision isso, consulte [criar um SQL Data Warehouse] [ Create a SQL Data Warehouse] e escolha dados de exemplo hello tooload.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-113">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="5d5cc-114">Se você já tiver um data warehouse, mas não tiver dados de exemplo, poderá [carregar dados de exemplo manualmente][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="5d5cc-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-tooyour-database"></a><span data-ttu-id="5d5cc-115">1. Conecte-se o banco de dados tooyour</span><span class="sxs-lookup"><span data-stu-id="5d5cc-115">1. Connect tooyour database</span></span>
<span data-ttu-id="5d5cc-116">tooopen Power BI e conecte-se o banco de dados do AdventureWorksDW tooyour:</span><span class="sxs-lookup"><span data-stu-id="5d5cc-116">tooopen Power BI and connect tooyour AdventureWorksDW database:</span></span>

1. <span data-ttu-id="5d5cc-117">O logon no hello [portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="5d5cc-117">Sign into hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="5d5cc-118">Clique em **bancos de dados SQL** e escolha o banco de dados AdventureWorks do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![Localize o banco de dados][1]
3. <span data-ttu-id="5d5cc-120">Clique o botão 'Abrir no Power BI' hello.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-120">Click hello 'Open in Power BI' button.</span></span>
   
    ![Botão Power BI][2]
4. <span data-ttu-id="5d5cc-122">Agora você deve ver a página de conexão do SQL Data Warehouse Olá exibindo o endereço da web de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-122">You should now see hello SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="5d5cc-123">Clique em Avançar.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-123">Click next.</span></span>
   
    ![Conexão do Power BI][3]
5. <span data-ttu-id="5d5cc-125">Digite seu nome de usuário do SQL Azure server e a senha e você será o banco de dados do SQL Data Warehouse tooyour totalmente conectada.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-125">Enter your Azure SQL server username and password and you will be fully connected tooyour SQL Data Warehouse database.</span></span>
   
    ![Entrada do Power BI][4]
6. <span data-ttu-id="5d5cc-127">Depois de ter entrado no Power BI, clique em Olá AdventureWorksDW dataset na folha de saudação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-127">Once you have signed into Power BI, click hello AdventureWorksDW dataset on hello left blade.</span></span> <span data-ttu-id="5d5cc-128">Isso abrirá o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-128">This will open hello database.</span></span>
   
    ![Abrir AdventureWorksDW no Power BI][5]

## <a name="2-create-a-report"></a><span data-ttu-id="5d5cc-130">2. Criar um relatório</span><span class="sxs-lookup"><span data-stu-id="5d5cc-130">2. Create a report</span></span>
<span data-ttu-id="5d5cc-131">Você está agora pronto toouse Power BI tooanalyze seus dados de exemplo AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-131">You are now ready toouse Power BI tooanalyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="5d5cc-132">análise de saudação tooperform AdventureWorksDW tem uma exibição chamada AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-132">tooperform hello analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="5d5cc-133">Essa exibição contém algumas das métricas-chave para a análise de vendas da empresa de saudação Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-133">This view contains a few of hello key metrics for analyzing hello sales of hello company.</span></span>

1. <span data-ttu-id="5d5cc-134">toocreate um mapa da quantidade de vendas de acordo com o código de toopostal, no painel de campos à direita do hello, clique em Olá AggregateSales exibição tooexpand-lo.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-134">toocreate a map of sales amount according toopostal code, in hello right-hand fields pane, click hello AggregateSales view tooexpand it.</span></span> <span data-ttu-id="5d5cc-135">Clique em tooselect de colunas PostalCode e SalesAmount Olá-los.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-135">Click hello PostalCode and SalesAmount columns tooselect them.</span></span>
   
    ![Selecionar AggregateSales no Power BI][6]
   
    <span data-ttu-id="5d5cc-137">O Power BI reconhecerá isso automaticamente como dados geográficos e os colocará em um mapa para você.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Mapa do Power BI][7]
2. <span data-ttu-id="5d5cc-139">Esta etapa cria um gráfico de barras que mostra o valor de vendas por receita de cliente.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="5d5cc-140">toocreate este toohello vá expandido AggregateSales exibição.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-140">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="5d5cc-141">Clique em campo SalesAmount de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-141">Click hello SalesAmount field.</span></span> <span data-ttu-id="5d5cc-142">Arraste Olá renda campo toohello esquerda e soltá-lo em um eixo.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-142">Drag hello Customer Income field toohello left and drop it into Axis.</span></span>
   
    ![Selecionar eixo no Power BI][8]
   
    <span data-ttu-id="5d5cc-144">Mudamos gráfico de barras Olá sobre Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-144">We moved hello bar chart over hello left.</span></span>
   
    ![Barra do Power BI][9]
3. <span data-ttu-id="5d5cc-146">Esta etapa cria um gráfico de linhas que mostra o valor de vendas por data do pedido.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="5d5cc-147">toocreate este toohello vá expandido AggregateSales exibição.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-147">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="5d5cc-148">Clique em SalesAmount e em OrderDate.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="5d5cc-149">Na coluna de visualizações de saudação Clique ícone de gráfico de linhas de saudação; Este é o primeiro ícone de saudação na segunda linha hello em visualizações.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-149">In hello Visualizations column click hello Line Chart icon; this is hello first icon in hello second line under visualizations.</span></span>
   
    ![Selecionar gráfico de linhas no Power BI][10]
   
    <span data-ttu-id="5d5cc-151">Agora você tem um relatório que mostra três visualizações diferentes de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-151">You now have a report that shows three different visualizations of hello data.</span></span>
   
    ![Linha do Power BI][11]

<span data-ttu-id="5d5cc-153">Você pode salvar seu andamento a qualquer momento clicando em **Arquivo** e selecionando **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5d5cc-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d5cc-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5d5cc-154">Next steps</span></span>
<span data-ttu-id="5d5cc-155">Agora que damos você toowarm algum tempo para cima com dados de exemplo hello, consulte como muito[desenvolver][develop], [carregar][load], ou [ migrar][migrate].</span><span class="sxs-lookup"><span data-stu-id="5d5cc-155">Now that we've given you some time toowarm up with hello sample data, see how too[develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="5d5cc-156">Ou dar uma olhada Olá [site do Power BI][Power BI website].</span><span class="sxs-lookup"><span data-stu-id="5d5cc-156">Or take a look at hello [Power BI website][Power BI website].</span></span>

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
