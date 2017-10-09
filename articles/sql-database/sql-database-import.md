---
title: um BACPAC de aaaImport arquivo toocreate um banco de dados SQL do Azure | Microsoft Docs
description: Crie um novo banco de dados SQL do Azure importando um arquivo BACPAC existente.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: cf9a9631-56aa-4985-a565-1cacc297871d
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/26/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 0d5fc93acf27b79502969fcd6199d11161915b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a><span data-ttu-id="c75a4-103">Importar um tooa de arquivo BACPAC novo banco de dados do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="c75a4-103">Import a BACPAC file tooa new Azure SQL Database</span></span>

<span data-ttu-id="c75a4-104">Quando você precisa tooimport um banco de dados de um arquivo ou ao migrar de outra plataforma, você pode importar o esquema de banco de dados de saudação e dados de um [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) arquivo.</span><span class="sxs-lookup"><span data-stu-id="c75a4-104">When you need tooimport a database from an archive or when migrating from another platform, you can import hello database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="c75a4-105">Um arquivo BACPAC é um arquivo ZIP com uma extensão de BACPAC que contém os metadados de saudação e dados de um banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c75a4-105">A BACPAC file is a ZIP file with an extension of BACPAC containing hello metadata and data from a SQL Server database.</span></span> <span data-ttu-id="c75a4-106">Um arquivo BACPAC pode ser importado do armazenamento de Blobs do Azure (apenas no armazenamento padrão) ou de uma determinada localização do armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="c75a4-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="c75a4-107">velocidade de importação de saudação toomaximize, recomendamos que você especifica um maior desempenho e da camada de nível de serviço, como um P6 e, em seguida, toodown conforme apropriado de escala após Olá importação for bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="c75a4-107">toomaximize hello import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale toodown as appropriate after hello import is successful.</span></span> <span data-ttu-id="c75a4-108">Olá Além disso, o nível de compatibilidade do banco de dados após a importação de saudação é baseada no nível de compatibilidade de saudação do banco de dados de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="c75a4-108">Also, hello database compatibility level after hello import is based on hello compatibility level of hello source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="c75a4-109">Depois de migrar seu banco de dados SQL do tooAzure de banco de dados, você pode escolher toooperate Olá banco de dados em seu nível de compatibilidade atual (nível 100 para o banco de dados do hello AdventureWorks2008R2) ou em um nível superior.</span><span class="sxs-lookup"><span data-stu-id="c75a4-109">After you migrate your database tooAzure SQL Database, you can choose toooperate hello database at its current compatibility level (level 100 for hello AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="c75a4-110">Para obter mais informações sobre implicações de saudação e opções para a operação de um banco de dados em um nível de compatibilidade específicos, consulte [nível de compatibilidade do banco de dados ALTER](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span><span class="sxs-lookup"><span data-stu-id="c75a4-110">For more information on hello implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="c75a4-111">Consulte também [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) para obter informações sobre configurações de nível de banco de dados adicionais relacionados toocompatibility níveis.</span><span class="sxs-lookup"><span data-stu-id="c75a4-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related toocompatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="c75a4-112">tooimport BACPAC tooa novo banco de dados, você deve primeiro criar um servidor lógico do banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="c75a4-112">tooimport a BACPAC tooa new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="c75a4-113">Para obter um tutorial mostrando como toomigrate um SQL Server do banco de dados tooAzure banco de dados SQL usando SQLPackage, consulte [migrar um banco de dados do SQL Server](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="c75a4-113">For a tutorial showing you how toomigrate a SQL Server database tooAzure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="c75a4-114">Exportar de um arquivo BACPAC usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c75a4-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="c75a4-115">Este artigo fornece instruções para criar um banco de dados do SQL Azure de um arquivo BACPAC armazenado no armazenamento de BLOBs do Azure usando Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c75a4-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c75a4-116">Importação usando Olá apenas o portal do Azure oferece suporte a importação de um arquivo BACPAC do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="c75a4-116">Import using hello Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="c75a4-117">Olá de tooimport um banco de dados usando o portal do Azure, a página aberta Olá para o banco de dados e clique em **importação** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="c75a4-117">tooimport a database using hello Azure portal, open hello page for your database and click **Import** on hello toolbar.</span></span> <span data-ttu-id="c75a4-118">Especifique o contêiner e a conta de armazenamento Olá e selecione arquivo BACPAC a saudação ser tooimport.</span><span class="sxs-lookup"><span data-stu-id="c75a4-118">Specify hello storage account and container, and select hello BACPAC file you want tooimport.</span></span> <span data-ttu-id="c75a4-119">Selecione o tamanho de saudação do novo banco de dados de saudação (geralmente Olá mesmo como origem) e forneça as credenciais do SQL Server de destino hello.</span><span class="sxs-lookup"><span data-stu-id="c75a4-119">Select hello size of hello new database (usually hello same as origin) and provide hello destination SQL Server credentials.</span></span>  

   ![Importação de banco de dados](./media/sql-database-import/import.png)

<span data-ttu-id="c75a4-121">progresso de saudação toomonitor de saudação operação de importação, abrir a página Olá Olá servidor lógico que contém Olá banco de dados que estão sendo importados.</span><span class="sxs-lookup"><span data-stu-id="c75a4-121">toomonitor hello progress of hello import operation, open hello page for hello logical server containing hello database being imported.</span></span> <span data-ttu-id="c75a4-122">Role para baixo demais**operações** e, em seguida, clique em **importação/exportação** histórico.</span><span class="sxs-lookup"><span data-stu-id="c75a4-122">Scroll down too**Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-hello-progress-of-an-import-operation"></a><span data-ttu-id="c75a4-123">Olá monitorar o andamento de uma operação de importação</span><span class="sxs-lookup"><span data-stu-id="c75a4-123">Monitor hello progress of an import operation</span></span>

<span data-ttu-id="c75a4-124">progresso de saudação toomonitor de saudação operação de importação, abrir página Olá Olá servidor lógico em qual Olá banco de dados está sendo importado importado.</span><span class="sxs-lookup"><span data-stu-id="c75a4-124">toomonitor hello progress of hello import operation, open hello page for hello logical server into which hello database is being imported imported.</span></span> <span data-ttu-id="c75a4-125">Role para baixo demais**operações** e, em seguida, clique em **importação/exportação** histórico.</span><span class="sxs-lookup"><span data-stu-id="c75a4-125">Scroll down too**Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="c75a4-126">![importar](./media/sql-database-import/import-history.png) ![importar status](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="c75a4-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="c75a4-127">o banco de dados do tooverify hello está ativo no servidor de saudação, clique em **bancos de dados SQL** e verifique se o novo banco de dados de saudação **Online**.</span><span class="sxs-lookup"><span data-stu-id="c75a4-127">tooverify hello database is live on hello server, click **SQL databases** and verify hello new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="c75a4-128">Importação de um arquivo BACPAC usando o SQLPackage</span><span class="sxs-lookup"><span data-stu-id="c75a4-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="c75a4-129">tooimport um SQL banco de dados usando Olá [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) utilitário de linha de comando, consulte [Importar parâmetros e propriedades](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="c75a4-129">tooimport a SQL database using hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="c75a4-130">Olá SQLPackage utilitário é fornecido com as versões mais recentes do hello [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e [SQL Server Data Tools para Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), ou você pode baixar a versão mais recente de saudação do [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) diretamente do hello Microsoft download center.</span><span class="sxs-lookup"><span data-stu-id="c75a4-130">hello SQLPackage utility ships with hello latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download hello latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from hello Microsoft download center.</span></span>

<span data-ttu-id="c75a4-131">Recomendamos o uso de saudação do hello SQLPackage utilitário para dimensionamento e desempenho na maioria dos ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="c75a4-131">We recommend hello use of hello SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="c75a4-132">Para um SQL Server Customer Advisory Team blog sobre como migrar usando arquivos BACPAC, consulte [Migrando do SQL Server tooAzure banco de dados SQL usando arquivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="c75a4-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="c75a4-133">Consulte Olá SQLPackage comando para obter um exemplo de script como a seguir Olá tooimport **AdventureWorks2008R2** banco de dados do armazenamento local tooan banco de dados do Azure SQL servidor lógico, chamado **mynewserver20170403** neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="c75a4-133">See hello following SQLPackage command for a script example for how tooimport hello **AdventureWorks2008R2** database from local storage tooan Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="c75a4-134">Esse script mostra a criação de um novo banco de dados chamado hello **myMigratedDatabase**, com uma camada de serviço do **Premium**e um objetivo de serviço de **P6**.</span><span class="sxs-lookup"><span data-stu-id="c75a4-134">This script shows hello creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="c75a4-135">Altere esses valores como ambiente tooyour apropriado.</span><span class="sxs-lookup"><span data-stu-id="c75a4-135">Change these values as appropriate tooyour environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![sqlpackage import](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="c75a4-137">Um servidor lógico do Banco de Dados SQL do Azure escuta na porta 1433.</span><span class="sxs-lookup"><span data-stu-id="c75a4-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="c75a4-138">Se você estiver tentando tooconnect tooan banco de dados do Azure SQL servidor lógico de dentro de um firewall corporativo, essa porta deve estar aberta no firewall corporativo Olá para toosuccessfully você se conectar.</span><span class="sxs-lookup"><span data-stu-id="c75a4-138">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

<span data-ttu-id="c75a4-139">Este exemplo mostra como tooimport um banco de dados usando o SqlPackage.exe com autenticação Universal do Active Directory:</span><span class="sxs-lookup"><span data-stu-id="c75a4-139">This example shows how tooimport a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="c75a4-140">Importação de um arquivo BACPAC usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c75a4-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="c75a4-141">Saudação de uso [AzureRmSqlDatabaseImport novo](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit um toohello de solicitação de banco de dados de importação serviço do Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c75a4-141">Use hello [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit an import database request toohello Azure SQL Database service.</span></span> <span data-ttu-id="c75a4-142">Dependendo do tamanho de saudação do banco de dados, a operação de importação de saudação pode levar toocomplete algum tempo.</span><span class="sxs-lookup"><span data-stu-id="c75a4-142">Depending on hello size of your database, hello import operation may take some time toocomplete.</span></span>

 ```powershell
 $importRequest = New-AzureRmSqlDatabaseImport -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "MyImportSample" `
    -DatabaseMaxSizeBytes "262144000" `
    -StorageKeyType "StorageAccessKey" `
    -StorageKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0] `
    -StorageUri "http://$storageaccountname.blob.core.windows.net/importsample/sample.bacpac" `
    -Edition "Standard" `
    -ServiceObjectiveName "P6" `
    -AdministratorLogin "ServerAdmin" `
    -AdministratorLoginPassword $(ConvertTo-SecureString -String "ASecureP@assw0rd" -AsPlainText -Force)

 ```

<span data-ttu-id="c75a4-143">status toocheck Olá Olá solicitação de importação, use Olá [AzureRmSqlDatabaseImportExportStatus Get](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c75a4-143">toocheck hello status of hello import request, use hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="c75a4-144">Executando isso imediatamente após Olá geralmente solicitação retorna **Status: em andamento**.</span><span class="sxs-lookup"><span data-stu-id="c75a4-144">Running this immediately after hello request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="c75a4-145">Quando você vir **Status: bem-sucedida** Olá importação for concluída.</span><span class="sxs-lookup"><span data-stu-id="c75a4-145">When you see **Status: Succeeded** hello import is complete.</span></span>

```powershell
$importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
[Console]::Write("Importing")
while ($importStatus.Status -eq "InProgress")
{
    $importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$importStatus
```

> [!TIP]
<span data-ttu-id="c75a4-146">Para outro exemplo de script, confira [Importar um banco de dados de um arquivo BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c75a4-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c75a4-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c75a4-147">Next steps</span></span>
* <span data-ttu-id="c75a4-148">toolearn como tooconnect tooand consultar um banco de dados importado do SQL, consulte [conectar tooSQL banco de dados com o SQL Server Management Studio e executar um exemplo de consulta T-SQL](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="c75a4-148">toolearn how tooconnect tooand query an imported SQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="c75a4-149">Para um SQL Server Customer Advisory Team blog sobre como migrar usando arquivos BACPAC, consulte [Migrando do SQL Server tooAzure banco de dados SQL usando arquivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="c75a4-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="c75a4-150">Para obter uma discussão Olá inteira do SQL Server banco de dados do processo de migração, incluindo recomendações de desempenho, consulte [migrar um banco de dados de SQL Server tooAzure banco de dados SQL](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="c75a4-150">For a discussion of hello entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database tooAzure SQL Database](sql-database-cloud-migrate.md).</span></span>



