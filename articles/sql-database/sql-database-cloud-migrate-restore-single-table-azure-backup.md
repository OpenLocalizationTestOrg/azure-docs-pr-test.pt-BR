---
title: "uma única tabela de backup de banco de dados SQL do aaaRestore | Microsoft Docs"
description: "Saiba como toorestore uma única tabela de backup de banco de dados SQL."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="92c78-103">Como toorestore uma única tabela de um backup de banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="92c78-103">How toorestore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="92c78-104">Você pode encontrar uma situação na qual você modificados acidentalmente alguns dados em um banco de dados SQL e agora quer toorecover Olá única afetados tabela.</span><span class="sxs-lookup"><span data-stu-id="92c78-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want toorecover hello single affected table.</span></span> <span data-ttu-id="92c78-105">Este artigo descreve como toorestore uma única tabela em um banco de dados de uma saudação banco de dados SQL [backups automáticos](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="92c78-105">This article describes how toorestore a single table in a database from one of hello SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a><span data-ttu-id="92c78-106">Etapas de preparação: renomear a tabela hello e restaure uma cópia do banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="92c78-106">Preparation steps: Rename hello table and restore a copy of hello database</span></span>
1. <span data-ttu-id="92c78-107">Identifique Olá tabela no banco de dados SQL do Azure que você deseja tooreplace com cópia Olá restaurado.</span><span class="sxs-lookup"><span data-stu-id="92c78-107">Identify hello table in your Azure SQL database that you want tooreplace with hello restored copy.</span></span> <span data-ttu-id="92c78-108">Use a tabela do Microsoft SQL Management Studio toorename hello.</span><span class="sxs-lookup"><span data-stu-id="92c78-108">Use Microsoft SQL Management Studio toorename hello table.</span></span> <span data-ttu-id="92c78-109">Por exemplo, renomeie a tabela hello como &lt;nome de tabela&gt;old.</span><span class="sxs-lookup"><span data-stu-id="92c78-109">For example, rename hello table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="92c78-110">tooavoid sendo bloqueado, certifique-se de que não há nenhuma atividade em execução em tabela Olá que você está renomeando.</span><span class="sxs-lookup"><span data-stu-id="92c78-110">tooavoid being blocked, make sure that there's no activity running on hello table that you are renaming.</span></span> <span data-ttu-id="92c78-111">Se tiver problemas, lembre-se de executar esse procedimento durante uma janela de manutenção.</span><span class="sxs-lookup"><span data-stu-id="92c78-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="92c78-112">Restaurar um backup de seu banco de dados tooa pontual que você deseja toorecover toousing Olá [restauraçãoPoint-In_Time](sql-database-recovery-using-backups.md#point-in-time-restore) etapas.</span><span class="sxs-lookup"><span data-stu-id="92c78-112">Restore a backup of your database tooa point in time that you want toorecover toousing hello [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="92c78-113">nome de saudação do banco de dados restaurado de saudação será no formato de carimbo de hora + DBName Olá; Por exemplo, **Adventureworks2012_2016-01-01T22-12Z**.</span><span class="sxs-lookup"><span data-stu-id="92c78-113">hello name of hello restored database will be in hello DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="92c78-114">Essa etapa não substitui o nome de banco de dados existente Olá no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="92c78-114">This step doesn't overwrite hello existing database name on hello server.</span></span> <span data-ttu-id="92c78-115">Esta é uma medida de segurança, e destina-se tooallow Olá de tooverify você restaurou o banco de dados antes de descartar o banco de dados atual e renomear Olá restaurado de banco de dados para uso em produção.</span><span class="sxs-lookup"><span data-stu-id="92c78-115">This is a safety measure, and it's intended tooallow you tooverify hello restored database before they drop their current database and rename hello restored database for production use.</span></span>
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a><span data-ttu-id="92c78-116">Copiando a tabela Olá da saudação restaurou o banco de dados usando a ferramenta de migração do banco de dados SQL Olá</span><span class="sxs-lookup"><span data-stu-id="92c78-116">Copying hello table from hello restored database by using hello SQL Database Migration tool</span></span>

1. <span data-ttu-id="92c78-117">Baixe e instale Olá [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="92c78-117">Download and install hello [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="92c78-118">Abra Olá SQL Database Migration Wizard no hello **Selecionar processo** , selecione **banco de dados em analisar/migrar**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="92c78-118">Open hello SQL Database Migration Wizard, on hello **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![SQL Database Migration Wizard – Selecionar processo](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="92c78-120">Em Olá **conectar tooServer** caixa de diálogo caixa, aplicar Olá configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="92c78-120">In hello **Connect tooServer** dialog box, apply hello following settings:</span></span>

   * <span data-ttu-id="92c78-121">Nome do servidor: **seu SQL Server**</span><span class="sxs-lookup"><span data-stu-id="92c78-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="92c78-122">Autenticação: **autenticação do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="92c78-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="92c78-123">Logon: **seu logon**</span><span class="sxs-lookup"><span data-stu-id="92c78-123">Login: **Your login**</span></span>
   * <span data-ttu-id="92c78-124">Senha: **sua senha**</span><span class="sxs-lookup"><span data-stu-id="92c78-124">Password: **Your password**</span></span>
   * <span data-ttu-id="92c78-125">Banco de dados: **banco de dados mestre (listar todos os bancos de dados)**</span><span class="sxs-lookup"><span data-stu-id="92c78-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="92c78-126">Por padrão o assistente Olá salva suas informações de logon.</span><span class="sxs-lookup"><span data-stu-id="92c78-126">By default hello wizard saves your login information.</span></span> <span data-ttu-id="92c78-127">Se não desejar que essas informações sejam salvas, selecione **Esquecer Informações de Logon**.</span><span class="sxs-lookup"><span data-stu-id="92c78-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![SQL Database Migration Wizard – Selecionar origem – etapa 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="92c78-129">Em Olá **Selecionar origem** caixa de diálogo, o nome do banco de dados selecione Olá restaurado da saudação **etapas de preparação** seção como sua fonte e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="92c78-129">In hello **Select Source** dialog box, select hello restored database name from hello **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![SQL Database Migration Wizard – Selecionar origem – etapa 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="92c78-131">Em Olá **escolher objetos** caixa de diálogo, selecione Olá **selecionar objetos de banco de dados específico** opção e selecione Olá table(or tables) que você deseja que o servidor de destino do toomigrate toohello.</span><span class="sxs-lookup"><span data-stu-id="92c78-131">In hello **Choose Objects** dialog box, select hello **Select specific database objects** option, and then select hello table(or tables) that you want toomigrate toohello target server.</span></span>
   <span data-ttu-id="92c78-132">![SQL Database Migration Wizard – Escolher objetos](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="92c78-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="92c78-133">Em Olá **resumo do Assistente de Script** , clique em **Sim** quando você for avisado sobre esteja pronto toogenerate um script SQL.</span><span class="sxs-lookup"><span data-stu-id="92c78-133">On hello **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready toogenerate a SQL script.</span></span> <span data-ttu-id="92c78-134">Você também tem Olá opção toosave Olá Script TSQL para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="92c78-134">You also have hello option toosave hello TSQL Script for later use.</span></span>
   <span data-ttu-id="92c78-135">![SQL Database Migration Wizard – Resumo do Assistente para criação de script](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="92c78-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="92c78-136">Em Olá **resumo de resultados** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="92c78-136">On hello **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="92c78-137">![SQL Database Migration Wizard – Resumo dos resultados](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="92c78-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="92c78-138">Em Olá **Conexão de servidor de destino de instalação** , clique em **conectar tooServer**e, em seguida, insira os detalhes de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="92c78-138">On hello **Setup Target Server Connection** page, click **Connect tooServer**, and then enter hello details as follows:</span></span>
   
   * <span data-ttu-id="92c78-139">**Nome do Servidor**: instância do servidor de destino</span><span class="sxs-lookup"><span data-stu-id="92c78-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="92c78-140">**Autenticação**: **autenticação do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="92c78-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="92c78-141">Insira suas credenciais de logon.</span><span class="sxs-lookup"><span data-stu-id="92c78-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="92c78-142">**Banco de dados**: **banco de dados mestre (listar todos os bancos de dados)**.</span><span class="sxs-lookup"><span data-stu-id="92c78-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="92c78-143">Essa opção lista todos os bancos de dados de saudação no servidor de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="92c78-143">This option lists all hello databases on hello target server.</span></span>
     
     ![SQL Database Migration Wizard – Configurar conexão do servidor de destino](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="92c78-145">Clique em **conectar**, selecione banco de dados de destino de saudação que você deseja toomove Olá tabela e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="92c78-145">Click **Connect**, select hello target database that you want toomove hello table to, and then click **Next**.</span></span> <span data-ttu-id="92c78-146">Isso deve terminar de executar o script hello gerado anteriormente, e você deverá ver Olá recentemente movido banco de dados de destino do tabela toohello copiado.</span><span class="sxs-lookup"><span data-stu-id="92c78-146">This should finish running hello previously generated script, and you should see hello newly moved table copied toohello target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="92c78-147">Etapa de verificação</span><span class="sxs-lookup"><span data-stu-id="92c78-147">Verification step</span></span>

- <span data-ttu-id="92c78-148">Saudação de consulta e teste copiado recentemente tabela toomake-se de que dados saudação estão intactos.</span><span class="sxs-lookup"><span data-stu-id="92c78-148">Query and test hello newly copied table toomake sure that hello data is intact.</span></span> <span data-ttu-id="92c78-149">Após confirmação, você pode remover o formato de tabela Olá renomeado **etapas de preparação** seção.</span><span class="sxs-lookup"><span data-stu-id="92c78-149">Upon confirmation, you can drop hello renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="92c78-150">(por exemplo, &lt;nome da tabela&gt;_old).</span><span class="sxs-lookup"><span data-stu-id="92c78-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="92c78-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="92c78-151">Next steps</span></span>
[<span data-ttu-id="92c78-152">Backups automáticos do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="92c78-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

