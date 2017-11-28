---
title: Importar um arquivo BACPAC para criar um Banco de Dados SQL do Azure | Microsoft Docs
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
ms.openlocfilehash: 285e17ed6d0ce700cb518864df7a3b5f5e55bee5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="import-a-bacpac-file-to-a-new-azure-sql-database"></a><span data-ttu-id="9c7c3-103">Importar um arquivo BACPAC para um novo Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="9c7c3-103">Import a BACPAC file to a new Azure SQL Database</span></span>

<span data-ttu-id="9c7c3-104">Quando você precisa importar um banco de dados de um arquivo ou ao migrar de outra plataforma, você pode importar o esquema de banco de dados e os dados de um arquivo [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4).</span><span class="sxs-lookup"><span data-stu-id="9c7c3-104">When you need to import a database from an archive or when migrating from another platform, you can import the database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="9c7c3-105">Um arquivo BACPAC é um arquivo ZIP com uma extensão BACPAC que contém os metadados e dados de um banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-105">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span></span> <span data-ttu-id="9c7c3-106">Um arquivo BACPAC pode ser importado do armazenamento de Blobs do Azure (apenas no armazenamento padrão) ou de uma determinada localização do armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="9c7c3-107">Para aumentar a velocidade de importação, recomendamos que você especifique um serviço desempenho e da camada de nível superior tal como um P6 e, em seguida, reduza verticalmente conforme apropriado após a importação ser bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-107">To maximize the import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale to down as appropriate after the import is successful.</span></span> <span data-ttu-id="9c7c3-108">Além disso, o nível de compatibilidade do banco de dados após a importação baseia-se no nível de compatibilidade do banco de dados de origem.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-108">Also, the database compatibility level after the import is based on the compatibility level of the source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="9c7c3-109">Depois de migrar seu banco de dados para o Banco de Dados SQL do Azure, é possível operar o banco de dados em seu nível de compatibilidade atual (nível 100 para o banco de dados AdventureWorks2008R2) ou em um nível superior.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-109">After you migrate your database to Azure SQL Database, you can choose to operate the database at its current compatibility level (level 100 for the AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="9c7c3-110">Para obter mais informações sobre as implicações e as opções para a operação de um banco de dados em um nível de compatibilidade específico, consulte [nível de compatibilidade de ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span><span class="sxs-lookup"><span data-stu-id="9c7c3-110">For more information on the implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="9c7c3-111">Consulte também [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) para obter informações sobre configurações de nível de banco de dados adicionais relacionadas aos níveis de compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related to compatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="9c7c3-112">Para importar um BACPAC para um novo banco de dados, você deve primeiro criar um servidor lógico do Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-112">To import a BACPAC to a new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="9c7c3-113">Para um tutorial que mostra como migrar um banco de dados do SQL Server para o Banco de Dados SQL do Azure usando o SQLPackage, consulte [Migrar um banco de dados do SQL Server](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="9c7c3-113">For a tutorial showing you how to migrate a SQL Server database to Azure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="9c7c3-114">Exportar de um arquivo BACPAC usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9c7c3-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="9c7c3-115">Este artigo fornece instruções para criar um Banco de Dados SQL Azure de um arquivo BACPAC armazenado no Armazenamento de Blobs do Azure usando o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9c7c3-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9c7c3-116">Importar usando o Portal do Azure dá suporte somente à importação de um arquivo BACPAC do Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-116">Import using the Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="9c7c3-117">Para importar um banco de dados usando o Portal do Azure, abra a página do banco de dados e clique em **Importar** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-117">To import a database using the Azure portal, open the page for your database and click **Import** on the toolbar.</span></span> <span data-ttu-id="9c7c3-118">Especifique a conta de armazenamento e o contêiner e selecione o arquivo BACPAC que você deseja importar.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-118">Specify the storage account and container, and select the BACPAC file you want to import.</span></span> <span data-ttu-id="9c7c3-119">Selecione o tamanho do novo banco de dados (normalmente, o mesmo que o de origem) e forneça credenciais do SQL Server de destino.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-119">Select the size of the new database (usually the same as origin) and provide the destination SQL Server credentials.</span></span>  

   ![Importação de banco de dados](./media/sql-database-import/import.png)

<span data-ttu-id="9c7c3-121">Para monitorar o progresso da operação de importação, abra a página para o servidor lógico que contém o banco de dados que está sendo importado.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-121">To monitor the progress of the import operation, open the page for the logical server containing the database being imported.</span></span> <span data-ttu-id="9c7c3-122">Role para baixo até **Operações** e, em seguida, clique em **Importar/Exportar histórico**.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-122">Scroll down to **Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-the-progress-of-an-import-operation"></a><span data-ttu-id="9c7c3-123">Monitorar o progresso de uma operação de importação</span><span class="sxs-lookup"><span data-stu-id="9c7c3-123">Monitor the progress of an import operation</span></span>

<span data-ttu-id="9c7c3-124">Para monitorar o progresso da operação de importação, abra a página para o servidor lógico que contém o banco de dados que está sendo importado.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-124">To monitor the progress of the import operation, open the page for the logical server into which the database is being imported imported.</span></span> <span data-ttu-id="9c7c3-125">Role para baixo até **Operações** e, em seguida, clique em **Importar/Exportar histórico**.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-125">Scroll down to **Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="9c7c3-126">![importar](./media/sql-database-import/import-history.png) ![importar status](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="9c7c3-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="9c7c3-127">Para verificar se o banco de dados está ativo no servidor, clique em **Bancos de Dados SQL** e verifique se o novo banco de dados está **Online**.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-127">To verify the database is live on the server, click **SQL databases** and verify the new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="9c7c3-128">Importação de um arquivo BACPAC usando o SQLPackage</span><span class="sxs-lookup"><span data-stu-id="9c7c3-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="9c7c3-129">Para importar um Banco de Dados SQL usando o utilitário de linha de comando [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx), consulte [Importar parâmetros e propriedades](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="9c7c3-129">To import a SQL database using the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="9c7c3-130">O utilitário SQLPackage acompanha as últimas versões do [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx) ou você pode baixar a última versão do [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) diretamente no Centro de Download da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-130">The SQLPackage utility ships with the latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download the latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from the Microsoft download center.</span></span>

<span data-ttu-id="9c7c3-131">Recomendamos o uso do utilitário SQLPackage para escala e desempenho na maioria dos ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-131">We recommend the use of the SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="9c7c3-132">Para ler uma postagem de blog da Equipe de Consultoria ao Cliente do SQL Server sobre a migração usando arquivos BACPAC, confira [Migrando do SQL Server para o Banco de Dados SQL do Azure usando arquivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="9c7c3-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="9c7c3-133">Confira o comando SQLPackage a seguir para um script de exemplo sobre como importar o banco de dados **AdventureWorks2008R2** do armazenamento local para um servidor lógico do Banco de Dados SQL do Azure, chamado **mynewserver20170403** neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-133">See the following SQLPackage command for a script example for how to import the **AdventureWorks2008R2** database from local storage to an Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="9c7c3-134">Esse script mostra a criação de um novo banco de dados chamado **myMigratedDatabase** com uma camada de serviço **Premium** e um Objetivo de Serviço **P6**.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-134">This script shows the creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="9c7c3-135">Altere esses valores conforme apropriado para o ambiente.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-135">Change these values as appropriate to your environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![sqlpackage import](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="9c7c3-137">Um servidor lógico do Banco de Dados SQL do Azure escuta na porta 1433.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="9c7c3-138">Se você estiver tentando conectar um servidor lógico do Banco de Dados SQL do Azure de dentro de um firewall corporativo, essa porta deverá estar aberta no firewall corporativo para que você possa conectar-se com êxito.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-138">If you are attempting to connect to an Azure SQL Database logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span></span>
>

<span data-ttu-id="9c7c3-139">Este exemplo mostra como importar um banco de dados usando SqlPackage.exe com Autenticação Universal do Active Directory:</span><span class="sxs-lookup"><span data-stu-id="9c7c3-139">This example shows how to import a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="9c7c3-140">Importação de um arquivo BACPAC usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c7c3-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="9c7c3-141">Use o cmdlet [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) para enviar uma solicitação de importação de banco de dados para o serviço de Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-141">Use the [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet to submit an import database request to the Azure SQL Database service.</span></span> <span data-ttu-id="9c7c3-142">Dependendo do tamanho do banco de dados, a operação de importação pode demorar para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-142">Depending on the size of your database, the import operation may take some time to complete.</span></span>

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

<span data-ttu-id="9c7c3-143">Para verificar o status da solicitação de importação, use o cmdlet [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus).</span><span class="sxs-lookup"><span data-stu-id="9c7c3-143">To check the status of the import request, use the [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="9c7c3-144">Executar isso imediatamente após a solicitação geralmente retorna **Status: InProgress**.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-144">Running this immediately after the request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="9c7c3-145">Quando você vir **Status: Êxito**, a importação estará concluída.</span><span class="sxs-lookup"><span data-stu-id="9c7c3-145">When you see **Status: Succeeded** the import is complete.</span></span>

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
<span data-ttu-id="9c7c3-146">Para outro exemplo de script, confira [Importar um banco de dados de um arquivo BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9c7c3-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c7c3-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9c7c3-147">Next steps</span></span>
* <span data-ttu-id="9c7c3-148">Para saber mais sobre como conectar e consultar um Banco de Dados SQL importado, confira [Conectar-se ao Banco de Dados SQL com o SQL Server Management Studio e executar um exemplo de consulta T-SQL](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="9c7c3-148">To learn how to connect to and query an imported SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="9c7c3-149">Para ler uma postagem de blog da Equipe de Consultoria ao Cliente do SQL Server sobre a migração usando arquivos BACPAC, confira [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/) (Migrando do SQL Server para o Banco de Dados SQL do Azure usando arquivos BACPAC).</span><span class="sxs-lookup"><span data-stu-id="9c7c3-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="9c7c3-150">Para ver uma discussão de todo o processo de migração do banco de dados do SQL Server, incluindo as recomendações de desempenho, confira [Migrar um banco de dados do SQL Server para o Banco de Dados SQL do Azure](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="9c7c3-150">For a discussion of the entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database to Azure SQL Database](sql-database-cloud-migrate.md).</span></span>



