---
title: "Introdução à Sincronização de Dados SQL do Azure (Visualização) | Microsoft Docs"
description: "Esse tutorial ajudará você a começar a Sincronização de Dados SQL do Azure (Versão prévia)."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 2d0f9d7f32ad79f49d58165d734b9df4af862835
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="57121-103">Introdução à Sincronização de Dados SQL do Azure (visualização)</span><span class="sxs-lookup"><span data-stu-id="57121-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="57121-104">Neste tutorial, você aprenderá a configurar a Sincronização de Dados SQL do Azure criando um grupo de sincronização híbrido que contém as instâncias de Banco de Dados SQL do Azure e do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="57121-104">In this tutorial, you learn how to set up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="57121-105">O novo grupo de sincronização ficará totalmente configurado e sincronizado no agendamento que você definir.</span><span class="sxs-lookup"><span data-stu-id="57121-105">The new sync group is fully configured and synchronizes on the schedule you set.</span></span>

<span data-ttu-id="57121-106">Este tutorial presume que você tem pelo menos alguma experiência anterior com o Banco de Dados SQL e o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="57121-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="57121-107">Para obter uma visão geral da Sincronização de Dados SQL, confira [Sincronizar dados](sql-database-sync-data.md).</span><span class="sxs-lookup"><span data-stu-id="57121-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="57121-108">Para obter exemplos completos do PowerShell que mostrem como configurar a Sincronização de Dados SQL, veja os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="57121-108">For complete PowerShell examples that show how to configure SQL Data Sync, see the following articles:</span></span>
-   [<span data-ttu-id="57121-109">Usar o PowerShell para sincronização entre vários banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="57121-109">Use PowerShell to sync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="57121-110">Usar o PowerShell para sincronizar entre um Banco de Dados SQL do Azure e um banco de dados local do SQL Server</span><span class="sxs-lookup"><span data-stu-id="57121-110">Use PowerShell to sync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="57121-111">A documentação técnica completa para Sincronização de Dados SQL do Azure, localizada anteriormente no MSDN, está disponível como documento .PDF.</span><span class="sxs-lookup"><span data-stu-id="57121-111">The complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="57121-112">Baixe [aqui](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span><span class="sxs-lookup"><span data-stu-id="57121-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="57121-113">Etapa 1: Criar grupo de sincronização</span><span class="sxs-lookup"><span data-stu-id="57121-113">Step 1 - Create sync group</span></span>

### <a name="locate-the-data-sync-settings"></a><span data-ttu-id="57121-114">Localizar as configurações de Sincronização de Dados</span><span class="sxs-lookup"><span data-stu-id="57121-114">Locate the Data Sync settings</span></span>

1.  <span data-ttu-id="57121-115">Em seu navegador, navegue até o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="57121-115">In your browser, navigate to the Azure portal.</span></span>

2.  <span data-ttu-id="57121-116">No portal, localize os bancos de dados SQL no seu Painel ou no ícone Bancos de Dados SQL na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="57121-116">In the portal, locate your SQL databases from your Dashboard or from the SQL Databases icon on the toolbar.</span></span>

    ![Lista de bancos de dados SQL do Azure](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="57121-118">Na folha **bancos de dados SQL**, selecione o banco de dados SQL existente que você deseja usar como banco de dados de hub para a Sincronização de Dados. A folha do banco de dados SQL é aberta.</span><span class="sxs-lookup"><span data-stu-id="57121-118">On the **SQL databases** blade, select the existing SQL database that you want to use as the hub database for Data Sync. The SQL database blade opens.</span></span>

4.  <span data-ttu-id="57121-119">Na folha do banco de dados SQL para o banco de dados selecionado, selecione **Sincronizar para outros bancos de dados**.</span><span class="sxs-lookup"><span data-stu-id="57121-119">On the SQL database blade for the selected database, select **Sync to other databases**.</span></span> <span data-ttu-id="57121-120">A folha Sincronização de Dados é aberta.</span><span class="sxs-lookup"><span data-stu-id="57121-120">The Data Sync blade opens.</span></span>

    ![Opção Sincronizar para outros bancos de dados](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="57121-122">Criar um novo grupo de sincronização</span><span class="sxs-lookup"><span data-stu-id="57121-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="57121-123">Na folha Sincronização de Dados, selecione **Novo Grupo de Sincronização**.</span><span class="sxs-lookup"><span data-stu-id="57121-123">On the Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="57121-124">A folha **Novo grupo de sincronização** é aberta com a Etapa 1, **Criar grupo de sincronização**, realçada.</span><span class="sxs-lookup"><span data-stu-id="57121-124">The **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="57121-125">A folha **Criar Grupo de Sincronização de Dados** também é aberta.</span><span class="sxs-lookup"><span data-stu-id="57121-125">The **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="57121-126">Na folha **Criar Grupo de Sincronização de Dados**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="57121-126">On the **Create Data Sync Group** blade, do the following things:</span></span>

    1.  <span data-ttu-id="57121-127">No campo **Nome do Grupo de Sincronização**, digite um nome para o novo grupo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="57121-127">In the **Sync Group Name** field, enter a name for the new sync group.</span></span>

    2.  <span data-ttu-id="57121-128">Na seção **Banco de Dados de Metadados de Sincronização**, escolha se deseja criar um novo banco de dados (recomendado) ou usar um banco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="57121-128">In the **Sync Metadata Database** section, choose whether to create a new database (recommended) or to use an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="57121-129">A Microsoft recomenda que você crie um novo banco de dados vazio para usar como o Banco de Dados de Metadados de Sincronização.</span><span class="sxs-lookup"><span data-stu-id="57121-129">Microsoft recommends that you create a new, empty database to use as the Sync Metadata Database.</span></span> <span data-ttu-id="57121-130">A Sincronização de Dados cria tabelas nesse banco de dados e executa uma carga de trabalho frequente.</span><span class="sxs-lookup"><span data-stu-id="57121-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="57121-131">Esse banco de dados é compartilhado automaticamente como o Banco de Dados de Metadados de Sincronização para todos os seus Grupos de sincronização na região selecionada.</span><span class="sxs-lookup"><span data-stu-id="57121-131">This database is automatically shared as the Sync Metadata Database for all of your Sync groups in the selected region.</span></span> <span data-ttu-id="57121-132">Você não pode alterar o Banco de Dados de Metadados de Sincronização, seu nome ou o nível de serviço sem removê-lo.</span><span class="sxs-lookup"><span data-stu-id="57121-132">You can't change the Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="57121-133">Se você escolheu **Novo banco de dados**, selecione **Criar novo banco de dados.**</span><span class="sxs-lookup"><span data-stu-id="57121-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="57121-134">A folha **Banco de Dados SQL** é aberta.</span><span class="sxs-lookup"><span data-stu-id="57121-134">The **SQL Database** blade opens.</span></span> <span data-ttu-id="57121-135">Na folha **Banco de Dados SQL**, nomeie e configure o novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="57121-135">On the **SQL Database** blade, name and configure the new database.</span></span> <span data-ttu-id="57121-136">Depois, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="57121-136">Then select **OK**.</span></span>

        <span data-ttu-id="57121-137">Se você escolheu **Usar banco de dados existente**, selecione o banco de dados na lista.</span><span class="sxs-lookup"><span data-stu-id="57121-137">If you chose **Use existing database**, select the database from the list.</span></span>

    3.  <span data-ttu-id="57121-138">Na seção **Sincronização Automática**, primeiro selecione **Ativa** ou **Inativa**.</span><span class="sxs-lookup"><span data-stu-id="57121-138">In the **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="57121-139">Se você escolheu **Ativa**, na seção **Frequência de Sincronização**, insira um número e selecione segundos, minutos, horas ou dias.</span><span class="sxs-lookup"><span data-stu-id="57121-139">If you chose **On**, in the **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![Especificar frequência de sincronização](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="57121-141">Na seção **Resolução de Conflitos**, selecione "Hub ganha" ou "Membro ganha".</span><span class="sxs-lookup"><span data-stu-id="57121-141">In the **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![Especificar como os conflitos são resolvidos](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="57121-143">Selecione **OK** e aguarde até que o novo grupo de sincronização seja criado e implantado.</span><span class="sxs-lookup"><span data-stu-id="57121-143">Select **OK** and wait for the new sync group to be created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="57121-144">Etapa 2: Adicionar membros de sincronização</span><span class="sxs-lookup"><span data-stu-id="57121-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="57121-145">Depois que o novo grupo de sincronização é criado e implantado, a Etapa 2, **Adicionar membros de sincronização**, fica realçada na folha **Novo grupo de sincronização**.</span><span class="sxs-lookup"><span data-stu-id="57121-145">After the new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in the **New sync group** blade.</span></span>

<span data-ttu-id="57121-146">Na seção **Banco de Dados Hub**, insira as credenciais existentes para o servidor de Banco de Dados SQL em que o banco de dados hub está localizado.</span><span class="sxs-lookup"><span data-stu-id="57121-146">In the **Hub Database** section, enter the existing credentials for the SQL Database server on which the hub database is located.</span></span> <span data-ttu-id="57121-147">Não insira *novas* credenciais nesta seção.</span><span class="sxs-lookup"><span data-stu-id="57121-147">Don't enter *new* credentials in this section.</span></span>

![O banco de dados hub foi adicionado ao grupo de sincronização](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="57121-149">Adicionar um Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="57121-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="57121-150">Na seção **Banco de Dados Membro**, opcionalmente, adicione um Banco de Dados SQL do Azure ao grupo de sincronização selecionando **Adicionar um Banco de Dados do Azure**.</span><span class="sxs-lookup"><span data-stu-id="57121-150">In the **Member Database** section, optionally add an Azure SQL Database to the sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="57121-151">A folha **Configurar Banco de Dados do Azure** é aberta.</span><span class="sxs-lookup"><span data-stu-id="57121-151">The **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="57121-152">Na folha **Configurar Banco de Dados do Azure**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="57121-152">On the **Configure Azure Database** blade, do the following things:</span></span>

1.  <span data-ttu-id="57121-153">No campo **Nome de Membro de Sincronização**, forneça um nome para o novo membro de sincronização.</span><span class="sxs-lookup"><span data-stu-id="57121-153">In the **Sync Member Name** field, provide a name for the new sync member.</span></span> <span data-ttu-id="57121-154">Esse nome é diferente do nome do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="57121-154">This name is distinct from the name of the database itself.</span></span>

2.  <span data-ttu-id="57121-155">No campo **Assinatura**, selecione a assinatura associada do Azure para fins de cobrança.</span><span class="sxs-lookup"><span data-stu-id="57121-155">In the **Subscription** field, select the associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="57121-156">No **Azure SQL Server**, selecione o servidor de banco de dados SQL existente.</span><span class="sxs-lookup"><span data-stu-id="57121-156">In the **Azure SQL Server** field, select the existing SQL database server.</span></span>

4.  <span data-ttu-id="57121-157">No **Banco de Dados SQL do Azure**, selecione o banco de dados SQL existente.</span><span class="sxs-lookup"><span data-stu-id="57121-157">In the **Azure SQL Database** field, select the existing SQL database.</span></span>

5.  <span data-ttu-id="57121-158">No campo **Direções de Sincronização**, selecione Sincronização Bidirecional, Para o Hub ou Do Hub.</span><span class="sxs-lookup"><span data-stu-id="57121-158">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span></span>

    ![Adicionar um novo membro de sincronização do Banco de Dados SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="57121-160">Nos campos **Nome de Usuário** e **Senha**, insira as credenciais existentes para o servidor de Banco de Dados SQL em que o banco de dados membro está localizado.</span><span class="sxs-lookup"><span data-stu-id="57121-160">In the **Username** and **Password** fields, enter the existing credentials for the SQL Database server on which the member database is located.</span></span> <span data-ttu-id="57121-161">Não insira *novas* credenciais nesta seção.</span><span class="sxs-lookup"><span data-stu-id="57121-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="57121-162">Selecione **OK** e aguarde até que o novo membro de sincronização seja criado e implantado.</span><span class="sxs-lookup"><span data-stu-id="57121-162">Select **OK** and wait for the new sync member to be created and deployed.</span></span>

    ![Novo membro de sincronização do banco de dados SQL foi adicionado](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="57121-164">Adicionar um Banco de dados do SQL Server local</span><span class="sxs-lookup"><span data-stu-id="57121-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="57121-165">Na seção **Banco de Dados Membro**, opcionalmente, adicione um SQL Server local ao grupo de sincronização selecionando **Adicionar um Banco de Dados Local**.</span><span class="sxs-lookup"><span data-stu-id="57121-165">In the **Member Database** section, optionally add an on-premises SQL Server to the sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="57121-166">A folha **Configurar Local** é aberta.</span><span class="sxs-lookup"><span data-stu-id="57121-166">The **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="57121-167">Na folha **Configurar Local**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="57121-167">On the **Configure On-Premises** blade, do the following things:</span></span>

1.  <span data-ttu-id="57121-168">Selecione **Escolher o Gateway de Agente de Sincronização**.</span><span class="sxs-lookup"><span data-stu-id="57121-168">Select **Choose the Sync Agent Gateway**.</span></span> <span data-ttu-id="57121-169">A folha **Selecionar Agente de Sincronização** é aberta.</span><span class="sxs-lookup"><span data-stu-id="57121-169">The **Select Sync Agent** blade opens.</span></span>

    ![Escolher o gateway de agente de sincronização](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="57121-171">Na folha **Escolher o Gateway de Agente de Sincronização**, escolha se deseja usar um agente existente ou criar um novo agente.</span><span class="sxs-lookup"><span data-stu-id="57121-171">On the **Choose the Sync Agent Gateway** blade, choose whether to use an existing agent or create a new agent.</span></span>

    <span data-ttu-id="57121-172">Se você escolheu **Agentes existentes**, selecione o agente existente na lista.</span><span class="sxs-lookup"><span data-stu-id="57121-172">If you chose **Existing agents**, select the existing agent from the list.</span></span>

    <span data-ttu-id="57121-173">Se você escolheu **Criar um novo agente**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="57121-173">If you chose **Create a new agent**, do the following things:</span></span>

    1.  <span data-ttu-id="57121-174">Baixe o software cliente do agente de sincronização no link fornecido e instale-o no computador em que o SQL Server está localizado.</span><span class="sxs-lookup"><span data-stu-id="57121-174">Download the client sync agent software from the link provided and install it on the computer where the SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="57121-175">Você precisa abrir a porta de saída TCP 1433 no firewall para permitir que o agente do cliente se comunique com o servidor.</span><span class="sxs-lookup"><span data-stu-id="57121-175">You have to open outbound TCP port 1433 in the firewall to let the client agent communicate with the server.</span></span>


    2.  <span data-ttu-id="57121-176">Insira um nome para o agente.</span><span class="sxs-lookup"><span data-stu-id="57121-176">Enter a name for the agent.</span></span>

    3.  <span data-ttu-id="57121-177">Selecione **Criar e Gerar Chave**.</span><span class="sxs-lookup"><span data-stu-id="57121-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="57121-178">Copie a chave do agente para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="57121-178">Copy the agent key to the clipboard.</span></span>
        
        ![Criando um novo agente de sincronização](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="57121-180">Selecione **OK** para fechar a folha **Selecionar o Agente de Sincronização**.</span><span class="sxs-lookup"><span data-stu-id="57121-180">Select **OK** to close the **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="57121-181">No computador do SQL Server, localize e execute o aplicativo Agente de Sincronização do Cliente.</span><span class="sxs-lookup"><span data-stu-id="57121-181">On the SQL Server computer, locate and run the Client Sync Agent app.</span></span>

        ![Os dados do aplicativo cliente do agente de sincronização de dados](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="57121-183">No aplicativo do agente de sincronização, selecione **Enviar Chave do Agente**.</span><span class="sxs-lookup"><span data-stu-id="57121-183">In the sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="57121-184">A caixa de diálogo **Configuração de Banco de Dados de Metadados de Sincronização** é aberta.</span><span class="sxs-lookup"><span data-stu-id="57121-184">The **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="57121-185">Na caixa de diálogo **Configuração de Banco de Dados de Metadados de sincronização**, cole a chave do agente copiada do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="57121-185">In the **Sync Metadata Database Configuration** dialog box, paste in the agent key copied from the Azure portal.</span></span> <span data-ttu-id="57121-186">Insira também as credenciais existentes para o servidor de Banco de Dados SQL do Azure em que o banco de dados de metadados está localizado.</span><span class="sxs-lookup"><span data-stu-id="57121-186">Also provide the existing credentials for the Azure SQL Database server on which the metadata database is located.</span></span> <span data-ttu-id="57121-187">(Se você criou um novo banco de dados de metadados, esse banco de dados está no mesmo servidor do banco de dados hub.) Selecione **OK** e aguarde até que a configuração seja concluída.</span><span class="sxs-lookup"><span data-stu-id="57121-187">(If you created a new metadata database, this database is on the same server as the hub database.) Select **OK** and wait for the configuration to finish.</span></span>

        ![Insira as credenciais de chave e servidor do agente](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="57121-189">Se você receber um erro de firewall nesta hora, precisará criar uma regra de firewall no Azure para permitir o tráfego de entrada do computador do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="57121-189">If you get a firewall error at this point, you have to create a firewall rule on Azure to allow incoming traffic from the SQL Server computer.</span></span> <span data-ttu-id="57121-190">Você pode criar a regra manualmente no portal, mas pode achar mais fácil criá-la no SSMS (SQL Server Management Studio).</span><span class="sxs-lookup"><span data-stu-id="57121-190">You can create the rule manually in the portal, but you may find it easier to create it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="57121-191">No SSMS, tente se conectar ao banco de dados hub no Azure.</span><span class="sxs-lookup"><span data-stu-id="57121-191">In SSMS, try to connect to the hub database on Azure.</span></span> <span data-ttu-id="57121-192">Digite o nome como \<hub_database_name\>.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="57121-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="57121-193">Siga as etapas na caixa de diálogo para configurar a regra de firewall do Azure.</span><span class="sxs-lookup"><span data-stu-id="57121-193">Follow the steps in the dialog box to configure the Azure firewall rule.</span></span> <span data-ttu-id="57121-194">Em seguida, retorne ao aplicativo Agente de Sincronização do Cliente.</span><span class="sxs-lookup"><span data-stu-id="57121-194">Then return to the Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="57121-195">No aplicativo Agente de Sincronização do Cliente, clique em **Registrar** para registrar um banco de dados do SQL Server no agente.</span><span class="sxs-lookup"><span data-stu-id="57121-195">In the Client Sync Agent app, click **Register** to register a SQL Server database with the agent.</span></span> <span data-ttu-id="57121-196">A caixa de diálogo **Configuração do SQL Server** é aberta.</span><span class="sxs-lookup"><span data-stu-id="57121-196">The **SQL Server Configuration** dialog box opens.</span></span>

        ![Adicionar e configurar um banco de dados do SQL Server](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="57121-198">Na caixa de diálogo **Configuração do SQL Server**, escolha se deseja se conectar usando a autenticação do SQL Server ou a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="57121-198">In the **SQL Server Configuration** dialog box, choose whether to connect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="57121-199">Se você escolher a autenticação do SQL Server, insira as credenciais existentes.</span><span class="sxs-lookup"><span data-stu-id="57121-199">If you chose SQL Server authentication, enter the existing credentials.</span></span> <span data-ttu-id="57121-200">Forneça o nome do SQL Server e o nome do banco de dados que você deseja sincronizar. Selecione **Testar conexão** para testar suas configurações.</span><span class="sxs-lookup"><span data-stu-id="57121-200">Provide the SQL Server name and the name of the database that you want to sync. Select **Test connection** to test your settings.</span></span> <span data-ttu-id="57121-201">Em seguida, selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="57121-201">Then select **Save**.</span></span> <span data-ttu-id="57121-202">O banco de dados registrado aparece na lista.</span><span class="sxs-lookup"><span data-stu-id="57121-202">The registered database appears in the list.</span></span>

        ![O banco de dados do SQL Server agora está registrado](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="57121-204">Agora você pode fechar o aplicativo Agente de Sincronização do Cliente.</span><span class="sxs-lookup"><span data-stu-id="57121-204">You can now close the Client Sync Agent app.</span></span>

    12. <span data-ttu-id="57121-205">No portal, na folha **Configurar Local**, selecione **Selecionar o Banco de Dados.**</span><span class="sxs-lookup"><span data-stu-id="57121-205">In the portal, on the **Configure On-Premises** blade, select **Select the Database.**</span></span> <span data-ttu-id="57121-206">A folha **Selecionar Banco de Dados** é aberta.</span><span class="sxs-lookup"><span data-stu-id="57121-206">The **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="57121-207">Na folha **Selecionar Banco de Dados**, no campo **Nome de Membro de Sincronização**, forneça um nome para o novo membro de sincronização.</span><span class="sxs-lookup"><span data-stu-id="57121-207">On the **Select Database** blade, in the **Sync Member Name** field, provide a name for the new sync member.</span></span> <span data-ttu-id="57121-208">Esse nome é diferente do nome do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="57121-208">This name is distinct from the name of the database itself.</span></span> <span data-ttu-id="57121-209">Selecione o banco de dados na lista.</span><span class="sxs-lookup"><span data-stu-id="57121-209">Select the database from the list.</span></span> <span data-ttu-id="57121-210">No campo **Direções de Sincronização**, selecione Sincronização Bidirecional, Para o Hub ou Do Hub.</span><span class="sxs-lookup"><span data-stu-id="57121-210">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span></span>

        ![Selecione o banco de dados local](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="57121-212">Selecione **OK** para fechar a folha **Selecionar o Banco de Dados**.</span><span class="sxs-lookup"><span data-stu-id="57121-212">Select **OK** to close the **Select Database** blade.</span></span> <span data-ttu-id="57121-213">Em seguida, selecione **OK** para fechar a folha **Configurar Local** e aguarde até o novo membro de sincronização ser criado e implantado.</span><span class="sxs-lookup"><span data-stu-id="57121-213">Then select **OK** to close the **Configure On-Premises** blade and wait for the new sync member to be created and deployed.</span></span> <span data-ttu-id="57121-214">Por fim, clique em **OK** para fechar a folha **Selecionar membros de sincronização**.</span><span class="sxs-lookup"><span data-stu-id="57121-214">Finally, click **OK** to close the **Select sync members** blade.</span></span>

        ![Banco de dados local adicionado ao grupo de sincronização](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="57121-216">Para conectar-se à Sincronização de Dados SQL e ao agente local, adicione seu nome de usuário à função `DataSync_Executor`.</span><span class="sxs-lookup"><span data-stu-id="57121-216">To connect to SQL Data Sync and the local agent, add your user name to the role `DataSync_Executor`.</span></span> <span data-ttu-id="57121-217">A Sincronização de Dados cria essa função na instância do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="57121-217">Data Sync creates this role on the SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="57121-218">Etapa 3: Configurar grupo de sincronização</span><span class="sxs-lookup"><span data-stu-id="57121-218">Step 3 - Configure sync group</span></span>

<span data-ttu-id="57121-219">Depois que os novos membros do grupo de sincronização são criados e implantados, a Etapa 3, **Configurar grupo de sincronização**, fica realçado na folha **Novo grupo de sincronização**.</span><span class="sxs-lookup"><span data-stu-id="57121-219">After the new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in the **New sync group** blade.</span></span>

1.  <span data-ttu-id="57121-220">Na folha **Tabelas**, selecione um banco de dados da lista de sincronização de membros do grupo e selecione **Atualizar esquema**.</span><span class="sxs-lookup"><span data-stu-id="57121-220">On the **Tables** blade, select a database from the list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="57121-221">Na lista de tabelas disponíveis, selecione as tabelas que você deseja sincronizar.</span><span class="sxs-lookup"><span data-stu-id="57121-221">From the list of available tables, select the tables that you want to sync.</span></span>

    ![Selecione as tabelas para sincronizar](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="57121-223">Por padrão, todas as colunas na tabela são selecionadas.</span><span class="sxs-lookup"><span data-stu-id="57121-223">By default, all columns in the table are selected.</span></span> <span data-ttu-id="57121-224">Se não quiser sincronizar todas as colunas, desmarque a caixa de seleção das colunas que você não deseja sincronizar. Deixe a coluna de chave primária selecionada.</span><span class="sxs-lookup"><span data-stu-id="57121-224">If you don't want to sync all the columns, disable the checkbox for the columns that you don't want to sync. Be sure to leave the primary key column selected.</span></span>

    ![Selecionar os campos para sincronizar](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="57121-226">Por fim, selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="57121-226">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57121-227">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="57121-227">Next steps</span></span>
<span data-ttu-id="57121-228">Parabéns.</span><span class="sxs-lookup"><span data-stu-id="57121-228">Congratulations.</span></span> <span data-ttu-id="57121-229">Você criou um grupo de sincronização que inclui uma instância do Banco de Dados SQL e um banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="57121-229">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="57121-230">Para obter mais informações sobre o Banco de Dados SQL e a Sincronização de Dados SQL, consulte:</span><span class="sxs-lookup"><span data-stu-id="57121-230">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="57121-231">Baixe a documentação técnica completa da Sincronização de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="57121-231">Download the complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="57121-232">Baixe a documentação da API REST de Sincronização de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="57121-232">Download the SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="57121-233">Visão geral do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="57121-233">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="57121-234">Gerenciamento de ciclo de vida do banco de dados</span><span class="sxs-lookup"><span data-stu-id="57121-234">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
