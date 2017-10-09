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
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a>Importar um tooa de arquivo BACPAC novo banco de dados do SQL do Azure

Quando você precisa tooimport um banco de dados de um arquivo ou ao migrar de outra plataforma, você pode importar o esquema de banco de dados de saudação e dados de um [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) arquivo. Um arquivo BACPAC é um arquivo ZIP com uma extensão de BACPAC que contém os metadados de saudação e dados de um banco de dados do SQL Server. Um arquivo BACPAC pode ser importado do armazenamento de Blobs do Azure (apenas no armazenamento padrão) ou de uma determinada localização do armazenamento local. velocidade de importação de saudação toomaximize, recomendamos que você especifica um maior desempenho e da camada de nível de serviço, como um P6 e, em seguida, toodown conforme apropriado de escala após Olá importação for bem-sucedida. Olá Além disso, o nível de compatibilidade do banco de dados após a importação de saudação é baseada no nível de compatibilidade de saudação do banco de dados de origem de saudação. 

> [!IMPORTANT] 
> Depois de migrar seu banco de dados SQL do tooAzure de banco de dados, você pode escolher toooperate Olá banco de dados em seu nível de compatibilidade atual (nível 100 para o banco de dados do hello AdventureWorks2008R2) ou em um nível superior. Para obter mais informações sobre implicações de saudação e opções para a operação de um banco de dados em um nível de compatibilidade específicos, consulte [nível de compatibilidade do banco de dados ALTER](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Consulte também [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) para obter informações sobre configurações de nível de banco de dados adicionais relacionados toocompatibility níveis.   >

> [!NOTE]
> tooimport BACPAC tooa novo banco de dados, você deve primeiro criar um servidor lógico do banco de dados SQL. Para obter um tutorial mostrando como toomigrate um SQL Server do banco de dados tooAzure banco de dados SQL usando SQLPackage, consulte [migrar um banco de dados do SQL Server](sql-database-migrate-your-sql-server-database.md)
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a>Exportar de um arquivo BACPAC usando o portal do Azure

Este artigo fornece instruções para criar um banco de dados do SQL Azure de um arquivo BACPAC armazenado no armazenamento de BLOBs do Azure usando Olá [portal do Azure](https://portal.azure.com). Importação usando Olá apenas o portal do Azure oferece suporte a importação de um arquivo BACPAC do armazenamento de BLOBs do Azure.

Olá de tooimport um banco de dados usando o portal do Azure, a página aberta Olá para o banco de dados e clique em **importação** na barra de ferramentas de saudação. Especifique o contêiner e a conta de armazenamento Olá e selecione arquivo BACPAC a saudação ser tooimport. Selecione o tamanho de saudação do novo banco de dados de saudação (geralmente Olá mesmo como origem) e forneça as credenciais do SQL Server de destino hello.  

   ![Importação de banco de dados](./media/sql-database-import/import.png)

progresso de saudação toomonitor de saudação operação de importação, abrir a página Olá Olá servidor lógico que contém Olá banco de dados que estão sendo importados. Role para baixo demais**operações** e, em seguida, clique em **importação/exportação** histórico.

### <a name="monitor-hello-progress-of-an-import-operation"></a>Olá monitorar o andamento de uma operação de importação

progresso de saudação toomonitor de saudação operação de importação, abrir página Olá Olá servidor lógico em qual Olá banco de dados está sendo importado importado. Role para baixo demais**operações** e, em seguida, clique em **importação/exportação** histórico.
   
   ![importar](./media/sql-database-import/import-history.png) ![importar status](./media/sql-database-import/import-status.png)

o banco de dados do tooverify hello está ativo no servidor de saudação, clique em **bancos de dados SQL** e verifique se o novo banco de dados de saudação **Online**.

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a>Importação de um arquivo BACPAC usando o SQLPackage

tooimport um SQL banco de dados usando Olá [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) utilitário de linha de comando, consulte [Importar parâmetros e propriedades](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties). Olá SQLPackage utilitário é fornecido com as versões mais recentes do hello [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e [SQL Server Data Tools para Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), ou você pode baixar a versão mais recente de saudação do [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) diretamente do hello Microsoft download center.

Recomendamos o uso de saudação do hello SQLPackage utilitário para dimensionamento e desempenho na maioria dos ambientes de produção. Para um SQL Server Customer Advisory Team blog sobre como migrar usando arquivos BACPAC, consulte [Migrando do SQL Server tooAzure banco de dados SQL usando arquivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

Consulte Olá SQLPackage comando para obter um exemplo de script como a seguir Olá tooimport **AdventureWorks2008R2** banco de dados do armazenamento local tooan banco de dados do Azure SQL servidor lógico, chamado **mynewserver20170403** neste exemplo. Esse script mostra a criação de um novo banco de dados chamado hello **myMigratedDatabase**, com uma camada de serviço do **Premium**e um objetivo de serviço de **P6**. Altere esses valores como ambiente tooyour apropriado.

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![sqlpackage import](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Um servidor lógico do Banco de Dados SQL do Azure escuta na porta 1433. Se você estiver tentando tooconnect tooan banco de dados do Azure SQL servidor lógico de dentro de um firewall corporativo, essa porta deve estar aberta no firewall corporativo Olá para toosuccessfully você se conectar.
>

Este exemplo mostra como tooimport um banco de dados usando o SqlPackage.exe com autenticação Universal do Active Directory:

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a>Importação de um arquivo BACPAC usando o PowerShell

Saudação de uso [AzureRmSqlDatabaseImport novo](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit um toohello de solicitação de banco de dados de importação serviço do Azure SQL Database. Dependendo do tamanho de saudação do banco de dados, a operação de importação de saudação pode levar toocomplete algum tempo.

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

status toocheck Olá Olá solicitação de importação, use Olá [AzureRmSqlDatabaseImportExportStatus Get](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet. Executando isso imediatamente após Olá geralmente solicitação retorna **Status: em andamento**. Quando você vir **Status: bem-sucedida** Olá importação for concluída.

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
Para outro exemplo de script, confira [Importar um banco de dados de um arquivo BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).

## <a name="next-steps"></a>Próximas etapas
* toolearn como tooconnect tooand consultar um banco de dados importado do SQL, consulte [conectar tooSQL banco de dados com o SQL Server Management Studio e executar um exemplo de consulta T-SQL](sql-database-connect-query-ssms.md).
* Para um SQL Server Customer Advisory Team blog sobre como migrar usando arquivos BACPAC, consulte [Migrando do SQL Server tooAzure banco de dados SQL usando arquivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Para obter uma discussão Olá inteira do SQL Server banco de dados do processo de migração, incluindo recomendações de desempenho, consulte [migrar um banco de dados de SQL Server tooAzure banco de dados SQL](sql-database-cloud-migrate.md).



