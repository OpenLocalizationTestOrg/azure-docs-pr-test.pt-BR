---
title: Conectar o Excel ao banco de dados SQL | Microsoft Docs
description: "Saiba como conectar o Microsoft Excel ao banco de dados SQL do Azure na nuvem. Importar dados para o Excel para exploração de dados e geração de relatórios."
services: sql-database
keywords: conectar o excel ao sql, importar dados para o excel
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 97344d7c0be38b3092a3224074d486b5bb984176
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-excel-to-an-azure-sql-database-and-create-a-report"></a><span data-ttu-id="69839-105">Conectar o Excel a um Banco de Dados SQL do Azure e criar um relatório</span><span class="sxs-lookup"><span data-stu-id="69839-105">Connect Excel to an Azure SQL database and create a report</span></span>

<span data-ttu-id="69839-106">Conectar o Excel a um banco de dados SQL na nuvem e importar dados e criar tabelas e gráficos com base nos valores no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="69839-106">Connect Excel to a SQL database in the cloud and import data and create tables and charts based on values in the database.</span></span> <span data-ttu-id="69839-107">Neste tutorial, você irá configurar a conexão entre o Excel e uma tabela do banco de dados, salvar o arquivo que armazena os dados e as informações de conexão para o Excel, em seguida, criar um gráfico dinâmico a partir dos valores do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="69839-107">In this tutorial you will set up the connection between Excel and a database table, save the file that stores data and the connection information for Excel, and then create a pivot chart from the database values.</span></span>

<span data-ttu-id="69839-108">Você precisará de um banco de dados SQL no Azure antes de começar.</span><span class="sxs-lookup"><span data-stu-id="69839-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="69839-109">Se você não tiver um, consulte [Criar seu primeiro banco de dados SQL](sql-database-get-started-portal.md) para obter um banco de dados com dados de exemplo em funcionamento em alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="69839-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) to get a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="69839-110">Neste artigo, você importará dados de exemplo do artigo para o Excel, mas poderá seguir etapas semelhantes em seus próprios dados.</span><span class="sxs-lookup"><span data-stu-id="69839-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="69839-111">Você também precisará de uma cópia do Excel.</span><span class="sxs-lookup"><span data-stu-id="69839-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="69839-112">Este artigo usa o [Microsoft Excel 2016](https://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="69839-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-to-a-sql-database-and-create-an-odc-file"></a><span data-ttu-id="69839-113">Conectar o Excel a um banco de dados SQL e criar um arquivo odc</span><span class="sxs-lookup"><span data-stu-id="69839-113">Connect Excel to a SQL database and create an odc file</span></span>
1. <span data-ttu-id="69839-114">Para conectar o Excel ao banco de dados SQL, abra o Excel e crie uma nova pasta de trabalho ou abra uma pasta do Excel existente.</span><span class="sxs-lookup"><span data-stu-id="69839-114">To connect Excel to SQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="69839-115">Na barra de menus na parte superior da página, clique em **Dados**, clique em **De Outras Fontes** e, em seguida, clique em **Do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="69839-115">In the menu bar at the top of the page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![Selecione a fonte de dados: Conectar o Excel ao banco de dados SQL.](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="69839-117">O Assistente de conexão de dados é aberto.</span><span class="sxs-lookup"><span data-stu-id="69839-117">The Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="69839-118">Na caixa de diálogo **Conectar ao servidor do banco de dados**, digite o **Nome do servidor** do Banco de Dados SQL que você deseja conectar no formato <*nomeservidor*>**.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="69839-118">In the **Connect to Database Server** dialog box, type the SQL Database **Server name** you want to connect to in the form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="69839-119">Por exemplo, **adworkserver.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="69839-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="69839-120">Em **Credenciais de logon**, clique em **Usar o seguinte Nome de Usuário e Senha**, digite o **Nome de Usuário** e a **Senha** que você configurou para o servidor do Banco de Dados SQL ao criá-lo, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="69839-120">Under **Log on credentials**, click **Use the following User Name and Password**, type the **User Name** and **Password** you set up for the SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![Digite as credenciais de logon e nome do servidor](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="69839-122">Dependendo do seu ambiente de rede, você não poderá conectar ou poderá perder a conexão se o servidor do Banco de Dados SQL não permitir o tráfego a partir de seu endereço IP do cliente.</span><span class="sxs-lookup"><span data-stu-id="69839-122">Depending on your network environment, you may not be able to connect or you may lose the connection if the SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="69839-123">Vá para o [portal do Azure](https://portal.azure.com/), clique em servidores SQL, clique no servidor, no firewall em configurações e adicione o endereço IP do cliente.</span><span class="sxs-lookup"><span data-stu-id="69839-123">Go to the [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="69839-124">Consulte [Como definir as configurações de firewall](sql-database-configure-firewall-settings.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="69839-124">See [How to configure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="69839-125">Na caixa de diálogo **Selecionar Banco de Dados e Tabela**, selecione o banco de dados com o qual você deseja trabalhar na lista, em seguida, clique nas tabelas ou exibições com as quais deseja trabalhar (escolhemos **vGetAllCategories**), em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="69839-125">In the **Select Database and Table** dialog, select the database you want to work with from the list, and then click the tables or views you want to work with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![Selecione um banco de dados e a tabela.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="69839-127">A caixa de diálogo **Salvar Arquivo de Conexão de Dados e Concluir** é aberta, em que você fornece informações sobre o arquivo de conexão de banco de dados do Office (*.odc) que o Excel usa.</span><span class="sxs-lookup"><span data-stu-id="69839-127">The **Save Data Connection File and Finish** dialog box opens, where you provide information about the Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="69839-128">Você pode deixar os padrões ou personalizar suas seleções.</span><span class="sxs-lookup"><span data-stu-id="69839-128">You can leave the defaults or customize your selections.</span></span>
6. <span data-ttu-id="69839-129">Você pode deixar os padrões, mas observe o **Nome de Arquivo** em particular.</span><span class="sxs-lookup"><span data-stu-id="69839-129">You can leave the defaults, but note the **File Name** in particular.</span></span> <span data-ttu-id="69839-130">Uma **Descrição**, **Nome Amigável** e **Palavras-Chave de Pesquisa** ajudam você e outros usuários a lembrarem o que está sendo conectado e a encontrarem a conexão.</span><span class="sxs-lookup"><span data-stu-id="69839-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting to and find the connection.</span></span> <span data-ttu-id="69839-131">Clique em **Sempre tentar usar este arquivo para atualizar os dados** se você quiser as informações de conexão armazenadas no arquivo odc para que ele possa ser atualizado quando você se conectar e, em seguida, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="69839-131">Click **Always attempt to use this file to refresh data** if you want connection information stored in the odc file so it can update when you connect to it, and then click **Finish**.</span></span>
   
    ![Salvando um arquivo odc](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="69839-133">A caixa de diálogo **Importar dados** é exibida.</span><span class="sxs-lookup"><span data-stu-id="69839-133">The **Import data** dialog box appears.</span></span>

## <a name="import-the-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="69839-134">Importar os dados para o Excel e criar um gráfico dinâmico</span><span class="sxs-lookup"><span data-stu-id="69839-134">Import the data into Excel and create a pivot chart</span></span>
<span data-ttu-id="69839-135">Agora que você estabeleceu a conexão e criou o arquivo com dados e informações de conexão, está pronto para importar os dados.</span><span class="sxs-lookup"><span data-stu-id="69839-135">Now that you've established the connection and created the file with data and connection information, you're reading to import the data.</span></span>

1. <span data-ttu-id="69839-136">Na caixa de diálogo **Importar Dados**, clique na opção desejada para apresentar os dados na planilha, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="69839-136">In the **Import Data** dialog, click the option you want for presenting your data in the worksheet and then click **OK**.</span></span> <span data-ttu-id="69839-137">Escolhemos **Gráfico Dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="69839-137">We chose **PivotChart**.</span></span> <span data-ttu-id="69839-138">Você também pode optar por criar uma **Nova planilha** ou **Adicionar dados a um Modelo de Dados**.</span><span class="sxs-lookup"><span data-stu-id="69839-138">You can also choose to create a **New worksheet** or to **Add this data to a Data Model**.</span></span> <span data-ttu-id="69839-139">Para obter mais informações sobre os Modelos de Dados, consulte [Criar um modelo de dados no Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span><span class="sxs-lookup"><span data-stu-id="69839-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="69839-140">Clique em **Propriedades** para explorar as informações sobre o arquivo odc que você criou na etapa anterior e escolha as opções para atualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="69839-140">Click **Properties** to explore information about the odc file you created in the previous step and to choose options for refreshing the data.</span></span>
   
    ![Escolhendo o formato dos dados no Excel](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="69839-142">Agora, a planilha tem uma tabela dinâmica vazia e um gráfico.</span><span class="sxs-lookup"><span data-stu-id="69839-142">The worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="69839-143">Em **Campos da Tabela Dinâmica**, selecione todas as caixas de seleção para os campos que você deseja exibir.</span><span class="sxs-lookup"><span data-stu-id="69839-143">Under **PivotTable Fields**, select all the check-boxes for the fields you want to view.</span></span>
   
    ![Configure o relatório do banco de dados.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="69839-145">Se você quiser conectar outras pastas de trabalho do Excel e planilhas ao banco de dados, clique em **Dados**, **Conexões**, **Adicionar**, escolha a conexão que você criou na lista, em seguida, clique em **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="69839-145">If you want to connect other Excel workbooks and worksheets to the database, click **Data**, click **Connections**, click **Add**, choose the connection you created from the list, and then click **Open**.</span></span>
> <span data-ttu-id="69839-146">![Abrir uma conexão a partir de outra pasta de trabalho](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="69839-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="69839-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="69839-147">Next steps</span></span>
* <span data-ttu-id="69839-148">Saiba como [Conectar o Banco de Dados SQL com o SQL Server Management Studio](sql-database-connect-query-ssms.md) para ter uma consulta e análise avançadas.</span><span class="sxs-lookup"><span data-stu-id="69839-148">Learn how to [Connect to SQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="69839-149">Saiba mais sobre os benefícios dos [pools elásticos](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="69839-149">Learn about the benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="69839-150">Saiba como [criar um aplicativo Web que se conecta ao Banco de Dados SQL em back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="69839-150">Learn how to [create a web application that connects to SQL Database on the back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>

