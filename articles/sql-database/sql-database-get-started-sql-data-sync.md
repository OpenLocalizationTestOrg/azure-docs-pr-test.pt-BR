---
title: "aaaGetting iniciado com a sincronização de dados SQL do Azure (visualização) | Microsoft Docs"
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
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="1f821-103">Introdução à Sincronização de Dados SQL do Azure (visualização)</span><span class="sxs-lookup"><span data-stu-id="1f821-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="1f821-104">Neste tutorial, você aprenderá como tooset a sincronização de dados do SQL Azure, criando um grupo de sincronização híbrido que contém instâncias de banco de dados do SQL Azure e SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1f821-104">In this tutorial, you learn how tooset up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="1f821-105">novo grupo de sincronização Hello está totalmente configurado e sincroniza no agendamento Olá definido.</span><span class="sxs-lookup"><span data-stu-id="1f821-105">hello new sync group is fully configured and synchronizes on hello schedule you set.</span></span>

<span data-ttu-id="1f821-106">Este tutorial presume que você tem pelo menos alguma experiência anterior com o Banco de Dados SQL e o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1f821-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="1f821-107">Para obter uma visão geral da Sincronização de Dados SQL, confira [Sincronizar dados](sql-database-sync-data.md).</span><span class="sxs-lookup"><span data-stu-id="1f821-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="1f821-108">Para obter exemplos completos do PowerShell que mostram como tooconfigure sincronização de dados SQL, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f821-108">For complete PowerShell examples that show how tooconfigure SQL Data Sync, see hello following articles:</span></span>
-   [<span data-ttu-id="1f821-109">Use o PowerShell toosync entre vários bancos de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1f821-109">Use PowerShell toosync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="1f821-110">Use o PowerShell toosync entre um banco de dados do SQL Azure e um banco de dados do SQL Server local</span><span class="sxs-lookup"><span data-stu-id="1f821-110">Use PowerShell toosync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="1f821-111">Olá completo conjunto de documentação técnica para sincronização de dados do SQL Azure, localizadas anteriormente no MSDN, está disponível como um. Documento PDF.</span><span class="sxs-lookup"><span data-stu-id="1f821-111">hello complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="1f821-112">Baixe [aqui](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span><span class="sxs-lookup"><span data-stu-id="1f821-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="1f821-113">Etapa 1: Criar grupo de sincronização</span><span class="sxs-lookup"><span data-stu-id="1f821-113">Step 1 - Create sync group</span></span>

### <a name="locate-hello-data-sync-settings"></a><span data-ttu-id="1f821-114">Localize as configurações de sincronização de dados Olá</span><span class="sxs-lookup"><span data-stu-id="1f821-114">Locate hello Data Sync settings</span></span>

1.  <span data-ttu-id="1f821-115">No seu navegador, navegue toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f821-115">In your browser, navigate toohello Azure portal.</span></span>

2.  <span data-ttu-id="1f821-116">No portal de hello, localize bancos de dados SQL do seu painel ou no ícone de bancos de dados SQL de saudação na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f821-116">In hello portal, locate your SQL databases from your Dashboard or from hello SQL Databases icon on hello toolbar.</span></span>

    ![Lista de bancos de dados SQL do Azure](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="1f821-118">Em Olá **bancos de dados SQL** folha, selecione Olá SQL banco de dados existente que você deseja toouse como Olá banco de dados de hub para sincronização de dados. folha de banco de dados SQL de saudação abre.</span><span class="sxs-lookup"><span data-stu-id="1f821-118">On hello **SQL databases** blade, select hello existing SQL database that you want toouse as hello hub database for Data Sync. hello SQL database blade opens.</span></span>

4.  <span data-ttu-id="1f821-119">Na folha de banco de dados SQL Olá para o banco de dados selecionado hello, selecione **sincronizar bancos de dados tooother**.</span><span class="sxs-lookup"><span data-stu-id="1f821-119">On hello SQL database blade for hello selected database, select **Sync tooother databases**.</span></span> <span data-ttu-id="1f821-120">Abre a folha de sincronização de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f821-120">hello Data Sync blade opens.</span></span>

    ![Opção de sincronização de bancos de dados tooother](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="1f821-122">Criar um novo grupo de sincronização</span><span class="sxs-lookup"><span data-stu-id="1f821-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="1f821-123">Na folha de sincronização de dados hello, selecione **novo grupo de sincronização**.</span><span class="sxs-lookup"><span data-stu-id="1f821-123">On hello Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="1f821-124">Olá **novo grupo de sincronização** folha é aberta com a etapa 1, **criar grupo de sincronização**, realçado.</span><span class="sxs-lookup"><span data-stu-id="1f821-124">hello **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="1f821-125">Olá **criar grupo de sincronização de dados** também abre uma folha.</span><span class="sxs-lookup"><span data-stu-id="1f821-125">hello **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="1f821-126">Em Olá **criar grupo de sincronização de dados** folha, Olá coisas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f821-126">On hello **Create Data Sync Group** blade, do hello following things:</span></span>

    1.  <span data-ttu-id="1f821-127">Em Olá **nome do grupo de sincronização** campo, digite um nome para o novo grupo de sincronização hello.</span><span class="sxs-lookup"><span data-stu-id="1f821-127">In hello **Sync Group Name** field, enter a name for hello new sync group.</span></span>

    2.  <span data-ttu-id="1f821-128">Em Olá **banco de dados de metadados de sincronização** , escolha se toocreate um novo banco de dados (recomendado) ou toouse um banco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="1f821-128">In hello **Sync Metadata Database** section, choose whether toocreate a new database (recommended) or toouse an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="1f821-129">A Microsoft recomenda que você crie um toouse de banco de dados novo e vazio como Olá banco de dados de metadados de sincronização.</span><span class="sxs-lookup"><span data-stu-id="1f821-129">Microsoft recommends that you create a new, empty database toouse as hello Sync Metadata Database.</span></span> <span data-ttu-id="1f821-130">A Sincronização de Dados cria tabelas nesse banco de dados e executa uma carga de trabalho frequente.</span><span class="sxs-lookup"><span data-stu-id="1f821-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="1f821-131">Este banco de dados é automaticamente compartilhado como Olá banco de dados de metadados de sincronização para todos os seus grupos de sincronização na região selecionada da saudação.</span><span class="sxs-lookup"><span data-stu-id="1f821-131">This database is automatically shared as hello Sync Metadata Database for all of your Sync groups in hello selected region.</span></span> <span data-ttu-id="1f821-132">Não é possível alterar o banco de dados de metadados de sincronização de saudação, seu nome ou seu nível de serviço sem removê-la.</span><span class="sxs-lookup"><span data-stu-id="1f821-132">You can't change hello Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="1f821-133">Se você escolheu **Novo banco de dados**, selecione **Criar novo banco de dados.**</span><span class="sxs-lookup"><span data-stu-id="1f821-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="1f821-134">Olá **banco de dados SQL** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="1f821-134">hello **SQL Database** blade opens.</span></span> <span data-ttu-id="1f821-135">Em Olá **banco de dados SQL** folha, nome e configurar o novo banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f821-135">On hello **SQL Database** blade, name and configure hello new database.</span></span> <span data-ttu-id="1f821-136">Depois, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f821-136">Then select **OK**.</span></span>

        <span data-ttu-id="1f821-137">Se você escolheu **banco de dados existente**, selecione banco de dados de saudação da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f821-137">If you chose **Use existing database**, select hello database from hello list.</span></span>

    3.  <span data-ttu-id="1f821-138">Em Olá **sincronização automática** seção, primeiro selecione **na** ou **Off**.</span><span class="sxs-lookup"><span data-stu-id="1f821-138">In hello **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="1f821-139">Se você escolheu **na**, em Olá **frequência de sincronização** seção, insira um número e selecione segundos, minutos, horas ou dias.</span><span class="sxs-lookup"><span data-stu-id="1f821-139">If you chose **On**, in hello **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![Especificar frequência de sincronização](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="1f821-141">Em Olá **resolução de conflitos** seção, selecione "Hub ganha" ou "Wins de membro".</span><span class="sxs-lookup"><span data-stu-id="1f821-141">In hello **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![Especificar como os conflitos são resolvidos](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="1f821-143">Selecione **Okey** e aguarde Olá nova sincronização grupo toobe criados e implantados.</span><span class="sxs-lookup"><span data-stu-id="1f821-143">Select **OK** and wait for hello new sync group toobe created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="1f821-144">Etapa 2: Adicionar membros de sincronização</span><span class="sxs-lookup"><span data-stu-id="1f821-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="1f821-145">Depois que o novo grupo de sincronização Olá é criado e implantado, a etapa 2, **adicionar membros de sincronização**, está realçado na Olá **novo grupo de sincronização** folha.</span><span class="sxs-lookup"><span data-stu-id="1f821-145">After hello new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in hello **New sync group** blade.</span></span>

<span data-ttu-id="1f821-146">Em Olá **banco de dados Hub** seção, insira as credenciais existentes de saudação para o servidor de banco de dados SQL Olá quais Olá banco de dados de hub está localizado.</span><span class="sxs-lookup"><span data-stu-id="1f821-146">In hello **Hub Database** section, enter hello existing credentials for hello SQL Database server on which hello hub database is located.</span></span> <span data-ttu-id="1f821-147">Não insira *novas* credenciais nesta seção.</span><span class="sxs-lookup"><span data-stu-id="1f821-147">Don't enter *new* credentials in this section.</span></span>

![Banco de dados hub foi adicionado toosync grupo](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="1f821-149">Adicionar um Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="1f821-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="1f821-150">Em Olá **banco de dados membro** seção, opcionalmente, adicione um grupo de sincronização do banco de dados do Azure SQL toohello selecionando **adicionar um banco de dados do Azure**.</span><span class="sxs-lookup"><span data-stu-id="1f821-150">In hello **Member Database** section, optionally add an Azure SQL Database toohello sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="1f821-151">Olá **configurar banco de dados do Azure** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="1f821-151">hello **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="1f821-152">Em Olá **configurar banco de dados do Azure** folha, Olá coisas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f821-152">On hello **Configure Azure Database** blade, do hello following things:</span></span>

1.  <span data-ttu-id="1f821-153">Em Olá **nome de membro de sincronização** campo, forneça um nome para o novo membro de sincronização hello.</span><span class="sxs-lookup"><span data-stu-id="1f821-153">In hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="1f821-154">Esse nome é diferente do nome de saudação do hello próprio banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1f821-154">This name is distinct from hello name of hello database itself.</span></span>

2.  <span data-ttu-id="1f821-155">Em Olá **assinatura** Olá de campo, selecione associados a assinatura do Azure para fins de cobrança.</span><span class="sxs-lookup"><span data-stu-id="1f821-155">In hello **Subscription** field, select hello associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="1f821-156">Em Olá **Azure SQL Server** servidor de banco de dados SQL existente Olá campo, selecione.</span><span class="sxs-lookup"><span data-stu-id="1f821-156">In hello **Azure SQL Server** field, select hello existing SQL database server.</span></span>

4.  <span data-ttu-id="1f821-157">Em Olá **banco de dados do SQL Azure** Olá campo, selecione SQL banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1f821-157">In hello **Azure SQL Database** field, select hello existing SQL database.</span></span>

5.  <span data-ttu-id="1f821-158">Em Olá **direções de sincronização** , selecione a sincronização bidirecional, toohello Hub, ou de saudação Hub.</span><span class="sxs-lookup"><span data-stu-id="1f821-158">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

    ![Adicionar um novo membro de sincronização do Banco de Dados SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="1f821-160">Em Olá **Username** e **senha** campos, insira as credenciais existentes de saudação para o servidor de banco de dados SQL Olá quais Olá membro banco de dados está localizado.</span><span class="sxs-lookup"><span data-stu-id="1f821-160">In hello **Username** and **Password** fields, enter hello existing credentials for hello SQL Database server on which hello member database is located.</span></span> <span data-ttu-id="1f821-161">Não insira *novas* credenciais nesta seção.</span><span class="sxs-lookup"><span data-stu-id="1f821-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="1f821-162">Selecione **Okey** e aguarde Olá nova sincronização membro toobe criados e implantados.</span><span class="sxs-lookup"><span data-stu-id="1f821-162">Select **OK** and wait for hello new sync member toobe created and deployed.</span></span>

    ![Novo membro de sincronização do banco de dados SQL foi adicionado](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="1f821-164">Adicionar um Banco de dados do SQL Server local</span><span class="sxs-lookup"><span data-stu-id="1f821-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="1f821-165">Em Olá **banco de dados membro** seção, opcionalmente, adicione um grupo de sincronização no local do SQL Server toohello selecionando **adicionar um banco de dados local**.</span><span class="sxs-lookup"><span data-stu-id="1f821-165">In hello **Member Database** section, optionally add an on-premises SQL Server toohello sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="1f821-166">Olá **configurar local** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="1f821-166">hello **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="1f821-167">Em Olá **configurar local** folha, Olá coisas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f821-167">On hello **Configure On-Premises** blade, do hello following things:</span></span>

1.  <span data-ttu-id="1f821-168">Selecione **Olá escolher Gateway de agente de sincronização**.</span><span class="sxs-lookup"><span data-stu-id="1f821-168">Select **Choose hello Sync Agent Gateway**.</span></span> <span data-ttu-id="1f821-169">Olá **selecione o agente de sincronização** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="1f821-169">hello **Select Sync Agent** blade opens.</span></span>

    ![Escolher gateway de agente de sincronização Olá](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="1f821-171">Em Olá **Olá escolher Gateway de agente de sincronização** folha, escolha se toouse um agente existente ou criar um novo agente.</span><span class="sxs-lookup"><span data-stu-id="1f821-171">On hello **Choose hello Sync Agent Gateway** blade, choose whether toouse an existing agent or create a new agent.</span></span>

    <span data-ttu-id="1f821-172">Se você escolheu **existente agentes**, selecione Olá agente existente na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f821-172">If you chose **Existing agents**, select hello existing agent from hello list.</span></span>

    <span data-ttu-id="1f821-173">Se você escolheu **criar um novo agente**, Olá coisas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f821-173">If you chose **Create a new agent**, do hello following things:</span></span>

    1.  <span data-ttu-id="1f821-174">Baixar o software de agente de sincronização de cliente Olá Olá link fornecido e instalá-lo no computador de saudação onde saudação do SQL Server está localizada.</span><span class="sxs-lookup"><span data-stu-id="1f821-174">Download hello client sync agent software from hello link provided and install it on hello computer where hello SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="1f821-175">Você tem tooopen saída a porta TCP 1433 no agente de cliente de saudação do hello firewall toolet se comunicar com o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f821-175">You have tooopen outbound TCP port 1433 in hello firewall toolet hello client agent communicate with hello server.</span></span>


    2.  <span data-ttu-id="1f821-176">Insira um nome para o agente de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f821-176">Enter a name for hello agent.</span></span>

    3.  <span data-ttu-id="1f821-177">Selecione **Criar e Gerar Chave**.</span><span class="sxs-lookup"><span data-stu-id="1f821-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="1f821-178">Copiar Olá agente chave toohello área de transferência.</span><span class="sxs-lookup"><span data-stu-id="1f821-178">Copy hello agent key toohello clipboard.</span></span>
        
        ![Criando um novo agente de sincronização](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="1f821-180">Selecione **Okey** tooclose Olá **selecione o agente de sincronização** folha.</span><span class="sxs-lookup"><span data-stu-id="1f821-180">Select **OK** tooclose hello **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="1f821-181">No computador do SQL Server hello, localize e execute o aplicativo do agente cliente de sincronização de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f821-181">On hello SQL Server computer, locate and run hello Client Sync Agent app.</span></span>

        ![aplicativo do agente cliente de sincronização de dados do Hello](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="1f821-183">No aplicativo de agente de sincronização hello, selecione **Enviar chave do agente**.</span><span class="sxs-lookup"><span data-stu-id="1f821-183">In hello sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="1f821-184">Olá **configuração de banco de dados de metadados de sincronização** caixa de diálogo é aberta.</span><span class="sxs-lookup"><span data-stu-id="1f821-184">hello **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="1f821-185">Em Olá **configuração de banco de dados de metadados de sincronização** caixa de diálogo Colar na chave de agente Olá copiado da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f821-185">In hello **Sync Metadata Database Configuration** dialog box, paste in hello agent key copied from hello Azure portal.</span></span> <span data-ttu-id="1f821-186">Também fornece credenciais de saudação existentes para o servidor de banco de dados do Azure SQL Olá quais Olá metadados de banco de dados está localizado.</span><span class="sxs-lookup"><span data-stu-id="1f821-186">Also provide hello existing credentials for hello Azure SQL Database server on which hello metadata database is located.</span></span> <span data-ttu-id="1f821-187">(Se você criou um novo banco de dados de metadados, esse banco de dados está em Olá mesmo servidor como banco de dados de hub hello.) Selecione **Okey** e aguarde Olá toofinish de configuração.</span><span class="sxs-lookup"><span data-stu-id="1f821-187">(If you created a new metadata database, this database is on hello same server as hello hub database.) Select **OK** and wait for hello configuration toofinish.</span></span>

        ![Insira as credenciais de chave e o servidor de agente Olá](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="1f821-189">Se você receber um erro de firewall neste ponto, você tem toocreate uma regra de firewall no tráfego de entrada do Azure tooallow do computador do SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="1f821-189">If you get a firewall error at this point, you have toocreate a firewall rule on Azure tooallow incoming traffic from hello SQL Server computer.</span></span> <span data-ttu-id="1f821-190">Você pode criar a regra de saudação manualmente no portal de hello, mas talvez você ache mais fácil toocreate-lo no SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="1f821-190">You can create hello rule manually in hello portal, but you may find it easier toocreate it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="1f821-191">No SSMS, tente o banco de dados de hub toohello de tooconnect no Azure.</span><span class="sxs-lookup"><span data-stu-id="1f821-191">In SSMS, try tooconnect toohello hub database on Azure.</span></span> <span data-ttu-id="1f821-192">Digite o nome como \<hub_database_name\>.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="1f821-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="1f821-193">Siga as etapas de saudação na regra de firewall no Azure Olá do tooconfigure de caixa de diálogo hello.</span><span class="sxs-lookup"><span data-stu-id="1f821-193">Follow hello steps in hello dialog box tooconfigure hello Azure firewall rule.</span></span> <span data-ttu-id="1f821-194">Em seguida, retorne toohello aplicativo de agente cliente de sincronização.</span><span class="sxs-lookup"><span data-stu-id="1f821-194">Then return toohello Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="1f821-195">No aplicativo do agente cliente de sincronização de saudação, clique em **registrar** tooregister um banco de dados do SQL Server com o agente de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f821-195">In hello Client Sync Agent app, click **Register** tooregister a SQL Server database with hello agent.</span></span> <span data-ttu-id="1f821-196">Olá **configuração do SQL Server** caixa de diálogo é aberta.</span><span class="sxs-lookup"><span data-stu-id="1f821-196">hello **SQL Server Configuration** dialog box opens.</span></span>

        ![Adicionar e configurar um banco de dados do SQL Server](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="1f821-198">Em Olá **configuração do SQL Server** caixa de diálogo caixa, escolha se tooconnect usando a autenticação do SQL Server ou autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="1f821-198">In hello **SQL Server Configuration** dialog box, choose whether tooconnect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="1f821-199">Se você escolher a autenticação do SQL Server, insira as credenciais existentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f821-199">If you chose SQL Server authentication, enter hello existing credentials.</span></span> <span data-ttu-id="1f821-200">Fornece saudação do SQL Server e nome de saudação do banco de dados de saudação que você deseja toosync.</span><span class="sxs-lookup"><span data-stu-id="1f821-200">Provide hello SQL Server name and hello name of hello database that you want toosync.</span></span> <span data-ttu-id="1f821-201">Selecione **Testar conexão** tootest suas configurações.</span><span class="sxs-lookup"><span data-stu-id="1f821-201">Select **Test connection** tootest your settings.</span></span> <span data-ttu-id="1f821-202">Em seguida, selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1f821-202">Then select **Save**.</span></span> <span data-ttu-id="1f821-203">banco de dados registrado Olá aparece na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f821-203">hello registered database appears in hello list.</span></span>

        ![O banco de dados do SQL Server agora está registrado](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="1f821-205">Agora você pode fechar o aplicativo do agente cliente de sincronização de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f821-205">You can now close hello Client Sync Agent app.</span></span>

    12. <span data-ttu-id="1f821-206">No portal Olá Olá **configurar local** folha, selecione **selecione Olá banco de dados.**</span><span class="sxs-lookup"><span data-stu-id="1f821-206">In hello portal, on hello **Configure On-Premises** blade, select **Select hello Database.**</span></span> <span data-ttu-id="1f821-207">Olá **Selecionar banco de dados** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="1f821-207">hello **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="1f821-208">Em Olá **Selecionar banco de dados** folha em Olá **nome de membro de sincronização** campo, forneça um nome para o novo membro de sincronização hello.</span><span class="sxs-lookup"><span data-stu-id="1f821-208">On hello **Select Database** blade, in hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="1f821-209">Esse nome é diferente do nome de saudação do hello próprio banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1f821-209">This name is distinct from hello name of hello database itself.</span></span> <span data-ttu-id="1f821-210">Selecione o banco de dados de saudação da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f821-210">Select hello database from hello list.</span></span> <span data-ttu-id="1f821-211">Em Olá **direções de sincronização** , selecione a sincronização bidirecional, toohello Hub, ou de saudação Hub.</span><span class="sxs-lookup"><span data-stu-id="1f821-211">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

        ![Selecione Olá no banco de dados local](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="1f821-213">Selecione **Okey** tooclose Olá **Selecionar banco de dados** folha.</span><span class="sxs-lookup"><span data-stu-id="1f821-213">Select **OK** tooclose hello **Select Database** blade.</span></span> <span data-ttu-id="1f821-214">Em seguida, selecione **Okey** tooclose Olá **configurar local** folha e aguardar Olá sincronizar novo membro toobe criados e implantados.</span><span class="sxs-lookup"><span data-stu-id="1f821-214">Then select **OK** tooclose hello **Configure On-Premises** blade and wait for hello new sync member toobe created and deployed.</span></span> <span data-ttu-id="1f821-215">Por fim, clique em **Okey** tooclose Olá **selecionar membros de sincronização** folha.</span><span class="sxs-lookup"><span data-stu-id="1f821-215">Finally, click **OK** tooclose hello **Select sync members** blade.</span></span>

        ![No banco de dados local adicionado toosync grupo](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="1f821-217">tooconnect tooSQL a sincronização de dados e o agente local do hello, adicionar a função de toohello de nome de usuário `DataSync_Executor`.</span><span class="sxs-lookup"><span data-stu-id="1f821-217">tooconnect tooSQL Data Sync and hello local agent, add your user name toohello role `DataSync_Executor`.</span></span> <span data-ttu-id="1f821-218">Sincronização de dados cria essa função na instância do SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="1f821-218">Data Sync creates this role on hello SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="1f821-219">Etapa 3: Configurar grupo de sincronização</span><span class="sxs-lookup"><span data-stu-id="1f821-219">Step 3 - Configure sync group</span></span>

<span data-ttu-id="1f821-220">Depois que os novos membros do grupo de sincronização Olá são criados e implantados, etapa 3, **Configurar grupo de sincronização**, está realçado na Olá **novo grupo de sincronização** folha.</span><span class="sxs-lookup"><span data-stu-id="1f821-220">After hello new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in hello **New sync group** blade.</span></span>

1.  <span data-ttu-id="1f821-221">Em Olá **tabelas** folha, selecione um banco de dados de lista de saudação de sincronização de membros do grupo e, em seguida, selecione **atualizar esquema**.</span><span class="sxs-lookup"><span data-stu-id="1f821-221">On hello **Tables** blade, select a database from hello list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="1f821-222">Na lista de saudação de tabelas disponíveis, selecione tabelas Olá que você deseja toosync.</span><span class="sxs-lookup"><span data-stu-id="1f821-222">From hello list of available tables, select hello tables that you want toosync.</span></span>

    ![Selecione as tabelas toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="1f821-224">Por padrão, todas as colunas na tabela de saudação são selecionadas.</span><span class="sxs-lookup"><span data-stu-id="1f821-224">By default, all columns in hello table are selected.</span></span> <span data-ttu-id="1f821-225">Se você não quiser toosync todas as colunas de hello, desabilite Olá a caixa de seleção para as colunas de saudação que você não deseja toosync.</span><span class="sxs-lookup"><span data-stu-id="1f821-225">If you don't want toosync all hello columns, disable hello checkbox for hello columns that you don't want toosync.</span></span> <span data-ttu-id="1f821-226">Certifique-se de coluna de chave primária de saudação tooleave selecionada.</span><span class="sxs-lookup"><span data-stu-id="1f821-226">Be sure tooleave hello primary key column selected.</span></span>

    ![Selecionar campos toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="1f821-228">Por fim, selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1f821-228">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f821-229">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1f821-229">Next steps</span></span>
<span data-ttu-id="1f821-230">Parabéns.</span><span class="sxs-lookup"><span data-stu-id="1f821-230">Congratulations.</span></span> <span data-ttu-id="1f821-231">Você criou um grupo de sincronização que inclui uma instância do Banco de Dados SQL e um banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1f821-231">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="1f821-232">Para obter mais informações sobre o Banco de Dados SQL e a Sincronização de Dados SQL, consulte:</span><span class="sxs-lookup"><span data-stu-id="1f821-232">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="1f821-233">Baixar a documentação técnica do hello concluída a sincronização de dados SQL</span><span class="sxs-lookup"><span data-stu-id="1f821-233">Download hello complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="1f821-234">Baixar a documentação da API de REST de sincronização de dados de SQL Olá</span><span class="sxs-lookup"><span data-stu-id="1f821-234">Download hello SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="1f821-235">Visão geral do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="1f821-235">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="1f821-236">Gerenciamento de ciclo de vida do banco de dados</span><span class="sxs-lookup"><span data-stu-id="1f821-236">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
