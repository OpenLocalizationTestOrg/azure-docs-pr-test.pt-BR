---
title: "Restaurar uma única tabela do backup do Banco de Dados SQL do Azure | Microsoft Docs"
description: "Saiba como restaurar uma única tabela do backup do Banco de Dados SQL do Azure."
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
ms.openlocfilehash: 8c750c503d10ea63b9665958b96db2dfea3d9a3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-restore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="12eac-103">Como restaurar uma única tabela de um backup do Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="12eac-103">How to restore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="12eac-104">É possível se deparar com uma situação na qual você acidentalmente modificou alguns dados no banco de dados SQL e agora deseja recuperar a única tabela afetada.</span><span class="sxs-lookup"><span data-stu-id="12eac-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want to recover the single affected table.</span></span> <span data-ttu-id="12eac-105">Este artigo descreve como restaurar uma única tabela em um banco de dados de um dos [backups automáticos](sql-database-automated-backups.md)do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="12eac-105">This article describes how to restore a single table in a database from one of the SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-the-table-and-restore-a-copy-of-the-database"></a><span data-ttu-id="12eac-106">Etapas de preparação: renomear a tabela e restaurar uma cópia do banco de dados</span><span class="sxs-lookup"><span data-stu-id="12eac-106">Preparation steps: Rename the table and restore a copy of the database</span></span>
1. <span data-ttu-id="12eac-107">Identifique a tabela no banco de dados SQL do Azure que deseja substituir pela cópia restaurada.</span><span class="sxs-lookup"><span data-stu-id="12eac-107">Identify the table in your Azure SQL database that you want to replace with the restored copy.</span></span> <span data-ttu-id="12eac-108">Use o Microsoft SQL Management Studio para renomear a tabela.</span><span class="sxs-lookup"><span data-stu-id="12eac-108">Use Microsoft SQL Management Studio to rename the table.</span></span> <span data-ttu-id="12eac-109">Por exemplo, renomeie a tabela como &lt;nome da tabela&gt;_old.</span><span class="sxs-lookup"><span data-stu-id="12eac-109">For example, rename the table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="12eac-110">Para evitar o bloqueio, certifique-se de que não há nenhuma atividade em execução na tabela que está sendo renomeada.</span><span class="sxs-lookup"><span data-stu-id="12eac-110">To avoid being blocked, make sure that there's no activity running on the table that you are renaming.</span></span> <span data-ttu-id="12eac-111">Se tiver problemas, lembre-se de executar esse procedimento durante uma janela de manutenção.</span><span class="sxs-lookup"><span data-stu-id="12eac-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="12eac-112">Restaure um backup do banco de dados para um estado que deseja recuperar usando as etapas de [Restauração pontual](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="12eac-112">Restore a backup of your database to a point in time that you want to recover to using the [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="12eac-113">O nome do banco de dados restaurado estará no formato DBName+TimeStamp; por exemplo, **Adventureworks2012_2016-01-01T22-12Z**.</span><span class="sxs-lookup"><span data-stu-id="12eac-113">The name of the restored database will be in the DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="12eac-114">Essa etapa não substitui o nome do banco de dados existente no servidor.</span><span class="sxs-lookup"><span data-stu-id="12eac-114">This step doesn't overwrite the existing database name on the server.</span></span> <span data-ttu-id="12eac-115">Esta é uma medida de segurança, e destina-se a permitir que você verifique o banco de dados restaurado antes de remover seu banco de dados atual e renomear o banco de dados restaurado para uso em produção.</span><span class="sxs-lookup"><span data-stu-id="12eac-115">This is a safety measure, and it's intended to allow you to verify the restored database before they drop their current database and rename the restored database for production use.</span></span>
   
## <a name="copying-the-table-from-the-restored-database-by-using-the-sql-database-migration-tool"></a><span data-ttu-id="12eac-116">Copiando a tabela do banco de dados restaurado usando a Ferramenta de migração do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="12eac-116">Copying the table from the restored database by using the SQL Database Migration tool</span></span>

1. <span data-ttu-id="12eac-117">Baixe e instale o [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="12eac-117">Download and install the [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="12eac-118">Abra o SQL Database Migration Wizard e, na página **Selecionar Processo**, selecione **Banco de Dados em Analisar/Migrar** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="12eac-118">Open the SQL Database Migration Wizard, on the **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![SQL Database Migration Wizard – Selecionar processo](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="12eac-120">Na caixa de diálogo **Conectar ao Servidor** , aplique as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="12eac-120">In the **Connect to Server** dialog box, apply the following settings:</span></span>

   * <span data-ttu-id="12eac-121">Nome do servidor: **seu SQL Server**</span><span class="sxs-lookup"><span data-stu-id="12eac-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="12eac-122">Autenticação: **autenticação do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="12eac-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="12eac-123">Logon: **seu logon**</span><span class="sxs-lookup"><span data-stu-id="12eac-123">Login: **Your login**</span></span>
   * <span data-ttu-id="12eac-124">Senha: **sua senha**</span><span class="sxs-lookup"><span data-stu-id="12eac-124">Password: **Your password**</span></span>
   * <span data-ttu-id="12eac-125">Banco de dados: **banco de dados mestre (listar todos os bancos de dados)**</span><span class="sxs-lookup"><span data-stu-id="12eac-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="12eac-126">O assistente salva as informações de logon por padrão.</span><span class="sxs-lookup"><span data-stu-id="12eac-126">By default the wizard saves your login information.</span></span> <span data-ttu-id="12eac-127">Se não desejar que essas informações sejam salvas, selecione **Esquecer Informações de Logon**.</span><span class="sxs-lookup"><span data-stu-id="12eac-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![SQL Database Migration Wizard – Selecionar origem – etapa 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="12eac-129">Na caixa de diálogo **Selecionar Origem**, selecione o nome do banco de dados restaurado na seção **Etapas de preparação** como a origem e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="12eac-129">In the **Select Source** dialog box, select the restored database name from the **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![SQL Database Migration Wizard – Selecionar origem – etapa 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="12eac-131">Na caixa de diálogo **Escolher Objetos**, escolha a opção **Selecionar objetos de bancos de dados específicos** e a tabela (ou as tabelas) que você deseja migrar para o servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="12eac-131">In the **Choose Objects** dialog box, select the **Select specific database objects** option, and then select the table(or tables) that you want to migrate to the target server.</span></span>
   <span data-ttu-id="12eac-132">![SQL Database Migration Wizard – Escolher objetos](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="12eac-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="12eac-133">Na página **Resumo do Assistente para criação de script**, clique em **Sim** quando perguntado se você está pronto para gerar um script SQL.</span><span class="sxs-lookup"><span data-stu-id="12eac-133">On the **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready to generate a SQL script.</span></span> <span data-ttu-id="12eac-134">Você também tem a opção de salvar o Script TSQL para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="12eac-134">You also have the option to save the TSQL Script for later use.</span></span>
   <span data-ttu-id="12eac-135">![SQL Database Migration Wizard – Resumo do Assistente para criação de script](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="12eac-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="12eac-136">Na página **Resumo dos Resultados**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="12eac-136">On the **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="12eac-137">![SQL Database Migration Wizard – Resumo dos resultados](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="12eac-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="12eac-138">Na página **Configurar Conexão do Servidor de Destino**, clique em **Conectar ao Servidor** e insira os detalhes da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="12eac-138">On the **Setup Target Server Connection** page, click **Connect to Server**, and then enter the details as follows:</span></span>
   
   * <span data-ttu-id="12eac-139">**Nome do Servidor**: instância do servidor de destino</span><span class="sxs-lookup"><span data-stu-id="12eac-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="12eac-140">**Autenticação**: **autenticação do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="12eac-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="12eac-141">Insira suas credenciais de logon.</span><span class="sxs-lookup"><span data-stu-id="12eac-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="12eac-142">**Banco de dados**: **banco de dados mestre (listar todos os bancos de dados)**.</span><span class="sxs-lookup"><span data-stu-id="12eac-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="12eac-143">Esta opção lista todos os bancos de dados no servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="12eac-143">This option lists all the databases on the target server.</span></span>
     
     ![SQL Database Migration Wizard – Configurar conexão do servidor de destino](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="12eac-145">Clique em **Conectar**, selecione o banco de dados de destino para o qual deseja mover a tabela e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="12eac-145">Click **Connect**, select the target database that you want to move the table to, and then click **Next**.</span></span> <span data-ttu-id="12eac-146">Isso deverá terminar a execução do script gerado anteriormente e você deverá ver a tabela recém-movida copiada no banco de dados de destino.</span><span class="sxs-lookup"><span data-stu-id="12eac-146">This should finish running the previously generated script, and you should see the newly moved table copied to the target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="12eac-147">Etapa de verificação</span><span class="sxs-lookup"><span data-stu-id="12eac-147">Verification step</span></span>

- <span data-ttu-id="12eac-148">Consulte e teste a tabela recém-copiada para certificar-se de que os dados estão intactos.</span><span class="sxs-lookup"><span data-stu-id="12eac-148">Query and test the newly copied table to make sure that the data is intact.</span></span> <span data-ttu-id="12eac-149">Após a confirmação, é possível remover a tabela renomeada na seção **Etapas de preparação**.</span><span class="sxs-lookup"><span data-stu-id="12eac-149">Upon confirmation, you can drop the renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="12eac-150">(por exemplo, &lt;nome da tabela&gt;_old).</span><span class="sxs-lookup"><span data-stu-id="12eac-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="12eac-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="12eac-151">Next steps</span></span>
[<span data-ttu-id="12eac-152">Backups automáticos do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="12eac-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

