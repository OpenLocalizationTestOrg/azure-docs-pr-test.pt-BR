---
title: aaaConnect Excel tooSQL banco de dados | Microsoft Docs
description: "Saiba como o Microsoft Excel de tooconnect tooAzure SQL banco de dados na nuvem hello. Importar dados para o Excel para exploração de dados e geração de relatórios."
services: sql-database
keywords: conectar excel toosql, importar dados tooexcel
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
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a><span data-ttu-id="4135a-105">Conecte-se o banco de dados do Excel tooan SQL Azure e criar um relatório</span><span class="sxs-lookup"><span data-stu-id="4135a-105">Connect Excel tooan Azure SQL database and create a report</span></span>

<span data-ttu-id="4135a-106">Conecte-se o banco de dados do Excel tooa SQL na nuvem hello e importar dados e criar tabelas e gráficos com base nos valores no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="4135a-106">Connect Excel tooa SQL database in hello cloud and import data and create tables and charts based on values in hello database.</span></span> <span data-ttu-id="4135a-107">Neste tutorial, que você irá configurar a conexão de saudação entre o Excel e uma tabela de banco de dados, salvar arquivo hello que armazena informações de conexão de dados e Olá para Excel e, em seguida, criar um gráfico dinâmico de saudação valores do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4135a-107">In this tutorial you will set up hello connection between Excel and a database table, save hello file that stores data and hello connection information for Excel, and then create a pivot chart from hello database values.</span></span>

<span data-ttu-id="4135a-108">Você precisará de um banco de dados SQL no Azure antes de começar.</span><span class="sxs-lookup"><span data-stu-id="4135a-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="4135a-109">Se você não tiver um, consulte [criar seu primeiro banco de dados do SQL](sql-database-get-started-portal.md) tooget um banco de dados com dados de exemplo em funcionamento em poucos minutos.</span><span class="sxs-lookup"><span data-stu-id="4135a-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) tooget a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="4135a-110">Neste artigo, você importará dados de exemplo do artigo para o Excel, mas poderá seguir etapas semelhantes em seus próprios dados.</span><span class="sxs-lookup"><span data-stu-id="4135a-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="4135a-111">Você também precisará de uma cópia do Excel.</span><span class="sxs-lookup"><span data-stu-id="4135a-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="4135a-112">Este artigo usa o [Microsoft Excel 2016](https://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="4135a-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a><span data-ttu-id="4135a-113">Conecte-se o banco de dados do Excel tooa SQL e criar um arquivo odc</span><span class="sxs-lookup"><span data-stu-id="4135a-113">Connect Excel tooa SQL database and create an odc file</span></span>
1. <span data-ttu-id="4135a-114">tooconnect Excel tooSQL banco de dados, abra o Excel e, em seguida, criar uma nova pasta de trabalho ou abrir uma pasta de trabalho do Excel existente.</span><span class="sxs-lookup"><span data-stu-id="4135a-114">tooconnect Excel tooSQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="4135a-115">Na barra de menus Olá na parte superior de saudação da página Olá clique **dados**, clique em **de outras fontes**e, em seguida, clique em **do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="4135a-115">In hello menu bar at hello top of hello page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![Selecionar fonte de dados: conectar-se o banco de dados do Excel tooSQL.](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="4135a-117">Olá Assistente de Conexão de dados é aberto.</span><span class="sxs-lookup"><span data-stu-id="4135a-117">hello Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="4135a-118">Em Olá **conectar tooDatabase servidor** caixa de diálogo, Olá do tipo banco de dados SQL **nome do servidor** deseja tooconnect tooin Olá formulário <*servername* > **. t**.</span><span class="sxs-lookup"><span data-stu-id="4135a-118">In hello **Connect tooDatabase Server** dialog box, type hello SQL Database **Server name** you want tooconnect tooin hello form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="4135a-119">Por exemplo, **adworkserver.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="4135a-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="4135a-120">Em **credenciais de logon**, clique em **Olá usar nome de usuário e senha a seguir**, Olá tipo **nome de usuário** e **senha** configuradas para Olá o servidor de banco de dados SQL quando você criou e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4135a-120">Under **Log on credentials**, click **Use hello following User Name and Password**, type hello **User Name** and **Password** you set up for hello SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![Digite as credenciais de nome e logon do servidor de saudação](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="4135a-122">Dependendo do seu ambiente de rede, você pode não ser capaz de tooconnect ou você pode perder a conexão de saudação se o servidor de banco de dados SQL Olá não permitir o tráfego do seu endereço IP do cliente.</span><span class="sxs-lookup"><span data-stu-id="4135a-122">Depending on your network environment, you may not be able tooconnect or you may lose hello connection if hello SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="4135a-123">Vá toohello [portal do Azure](https://portal.azure.com/), clique em servidores SQL, seu servidor, clique em firewall em configurações e adicionar o endereço IP do cliente.</span><span class="sxs-lookup"><span data-stu-id="4135a-123">Go toohello [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="4135a-124">Consulte [como configurações de firewall tooconfigure](sql-database-configure-firewall-settings.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="4135a-124">See [How tooconfigure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="4135a-125">Em Olá **Selecionar banco de dados e tabela** caixa de diálogo, o banco de dados selecione Olá deseja toowork com lista de saudação e, em seguida, clique em tabelas de saudação ou modos de exibição que você deseja toowork com (escolhemos **vGetAllCategories**) e, em seguida, Clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4135a-125">In hello **Select Database and Table** dialog, select hello database you want toowork with from hello list, and then click hello tables or views you want toowork with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![Selecione um banco de dados e a tabela.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="4135a-127">Olá **salvar arquivo de Conexão de dados e concluir** caixa de diálogo é aberta, onde você fornece informações sobre arquivo (*. odc) da conexão de banco de dados de Office de hello que usa o Excel.</span><span class="sxs-lookup"><span data-stu-id="4135a-127">hello **Save Data Connection File and Finish** dialog box opens, where you provide information about hello Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="4135a-128">Você pode deixar os padrões de saudação ou personalizar suas seleções.</span><span class="sxs-lookup"><span data-stu-id="4135a-128">You can leave hello defaults or customize your selections.</span></span>
6. <span data-ttu-id="4135a-129">Você pode deixar Olá padrões, mas Olá Observação **nome de arquivo** em particular.</span><span class="sxs-lookup"><span data-stu-id="4135a-129">You can leave hello defaults, but note hello **File Name** in particular.</span></span> <span data-ttu-id="4135a-130">Um **descrição**, um **nome amigável**, e **pesquisar palavras-chave** ajudam você e outros usuários Lembre-se de que você está se conectando tooand localizar conexão hello.</span><span class="sxs-lookup"><span data-stu-id="4135a-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting tooand find hello connection.</span></span> <span data-ttu-id="4135a-131">Clique em **sempre tentar toouse esse arquivo de dados de toorefresh** se você deseja informações de conexão armazenadas no arquivo odc de saudação para que ele possa atualizar quando você conectar tooit e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="4135a-131">Click **Always attempt toouse this file toorefresh data** if you want connection information stored in hello odc file so it can update when you connect tooit, and then click **Finish**.</span></span>
   
    ![Salvando um arquivo odc](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="4135a-133">Olá **importar dados** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="4135a-133">hello **Import data** dialog box appears.</span></span>

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="4135a-134">Importar dados de saudação no Excel e criar um gráfico dinâmico</span><span class="sxs-lookup"><span data-stu-id="4135a-134">Import hello data into Excel and create a pivot chart</span></span>
<span data-ttu-id="4135a-135">Agora que que você estabeleceu conexão hello e arquivo hello criado com informações de conexão e de dados, você está lendo dados de saudação tooimport.</span><span class="sxs-lookup"><span data-stu-id="4135a-135">Now that you've established hello connection and created hello file with data and connection information, you're reading tooimport hello data.</span></span>

1. <span data-ttu-id="4135a-136">Em Olá **importar dados** caixa de diálogo, clique em opção Olá desejada para apresentar os dados na planilha de saudação e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="4135a-136">In hello **Import Data** dialog, click hello option you want for presenting your data in hello worksheet and then click **OK**.</span></span> <span data-ttu-id="4135a-137">Escolhemos **Gráfico Dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="4135a-137">We chose **PivotChart**.</span></span> <span data-ttu-id="4135a-138">Você também pode escolher toocreate um **nova planilha** ou muito**adicionar este tooa de dados modelo de dados**.</span><span class="sxs-lookup"><span data-stu-id="4135a-138">You can also choose toocreate a **New worksheet** or too**Add this data tooa Data Model**.</span></span> <span data-ttu-id="4135a-139">Para obter mais informações sobre os Modelos de Dados, consulte [Criar um modelo de dados no Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span><span class="sxs-lookup"><span data-stu-id="4135a-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="4135a-140">Clique em **propriedades** tooexplore informações sobre o arquivo odc de saudação criado no hello etapa e toochoose opções anteriores para atualizar os dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="4135a-140">Click **Properties** tooexplore information about hello odc file you created in hello previous step and toochoose options for refreshing hello data.</span></span>
   
    ![Escolher o formato de saudação para os dados no Excel](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="4135a-142">planilha de saudação agora tem uma tabela dinâmica vazia e um gráfico.</span><span class="sxs-lookup"><span data-stu-id="4135a-142">hello worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="4135a-143">Em **PivotTable Fields**, selecione todos os Olá caixas de seleção para Olá campos que você deseja tooview.</span><span class="sxs-lookup"><span data-stu-id="4135a-143">Under **PivotTable Fields**, select all hello check-boxes for hello fields you want tooview.</span></span>
   
    ![Configure o relatório do banco de dados.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="4135a-145">Se quiser tooconnect outros Excel pastas de trabalho e planilhas toohello banco de dados, clique em **dados**, clique em **conexões**, clique em **adicionar**, escolher conexão Olá criado na lista de saudação e depois clique em **abrir**.</span><span class="sxs-lookup"><span data-stu-id="4135a-145">If you want tooconnect other Excel workbooks and worksheets toohello database, click **Data**, click **Connections**, click **Add**, choose hello connection you created from hello list, and then click **Open**.</span></span>
> <span data-ttu-id="4135a-146">![Abrir uma conexão a partir de outra pasta de trabalho](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="4135a-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4135a-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4135a-147">Next steps</span></span>
* <span data-ttu-id="4135a-148">Saiba como muito[conectar tooSQL banco de dados com o SQL Server Management Studio](sql-database-connect-query-ssms.md) avançadas de consulta e análise.</span><span class="sxs-lookup"><span data-stu-id="4135a-148">Learn how too[Connect tooSQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="4135a-149">Saiba mais sobre os benefícios de saudação do [pools Elásticos](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="4135a-149">Learn about hello benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="4135a-150">Saiba como muito[criar um aplicativo web que se conecta tooSQL banco de dados back-end Olá](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4135a-150">Learn how too[create a web application that connects tooSQL Database on hello back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>

