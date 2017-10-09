---
title: aaaExport um arquivo BACPAC de tooa de banco de dados SQL do Azure | Microsoft Docs
description: "Exportar um arquivo BACPAC do SQL Azure banco de dados tooa usando Olá Portal do Azure"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 41d63a97-37db-4e40-b652-77c2fd1c09b7
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: cb3b4227318e0fd2114529c86c9792615fe7fd1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-sql-database-tooa-bacpac-file"></a>Exportar um arquivo de BACPAC de tooa de banco de dados SQL do Azure

Quando você precisar tooexport um banco de dados para arquivamento ou para a plataforma de tooanother móvel, você pode exportar Olá tooa de esquema e os dados do banco de dados [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) arquivo. Um arquivo BACPAC é um arquivo ZIP com uma extensão de BACPAC que contém os metadados de saudação e dados de um banco de dados do SQL Server. Um arquivo BACPAC pode ser colocado no Armazenamento de Blobs do Azure ou em uma determinada localização no armazenamento local e depois importado novamente para o Banco de Dados SQL do Azure ou uma instalação local do SQL Server. 

> [!IMPORTANT] 
> A exportação automatizada do Banco de Dados SQL do Azure foi desativada em 1° de março de 2017. Você pode usar [retenção de backup de longo prazo](sql-database-long-term-retention.md
) ou [automação do Azure](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) tooperiodically arquivamento bancos de dados SQL usando o PowerShell, de acordo com o agendamento de tooa de sua escolha. Para obter um exemplo, baixe Olá [exemplo de script PowerShell](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) do Github.
>

## <a name="considerations-when-exporting-an-azure-sql-database"></a>Considerações ao exportar um banco de dados SQL do Azure

* Para uma exportação toobe transacionalmente consistente, você deve garantir que nenhuma atividade de gravação estiver ocorrendo durante a exportação de hello, ou que você está exportando um [cópia transacionalmente consistente](sql-database-copy.md) do banco de dados SQL do Azure.
* Se você estiver exportando tooblob armazenamento, o tamanho máximo de saudação de um arquivo BACPAC é 200 GB. tooarchive um arquivo BACPAC maior, exportar toolocal armazenamento.
* Não há suporte para a exportação de um armazenamento premium do BACPAC arquivo tooAzure usando Olá métodos discutidos neste artigo.
* Se a operação de exportação de saudação do banco de dados do SQL Azure exceder 20 horas, ele pode ser cancelado. tooincrease o desempenho durante a exportação, você pode:
  * Aumentar temporariamente seu nível de serviço.
  * Deixará todas de leitura e gravação de atividade durante a exportação de saudação.
  * Use um [índice clusterizado](https://msdn.microsoft.com/library/ms190457.aspx) com valores não nulos em todas as tabelas grandes. Sem índices clusterizados, a exportação poderá falhar se demorar mais de 6 a 12 horas. Isso ocorre porque o serviço de exportação de saudação precisa toocomplete uma verificação tootry tooexport toda tabela. Toodetermine uma boa maneira se as tabelas são otimizadas para exportação é toorun **DBCC SHOW_STATISTICS** e certifique-se de que Olá *RANGE_HI_KEY* não é nulo e seu valor tem boa distribuição. Para obter detalhes, consulte [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).

> [!NOTE]
> BACPACs não são toobe pretendido usado para operações de backup e restauração. O Banco de Dados SQL do Azure cria automaticamente backups de todos os bancos de dados de usuário. Para obter detalhes, confira [Visão geral da continuidade dos negócios](sql-database-business-continuity.md) e [Backups do Banco de Dados SQL](sql-database-automated-backups.md).  
> 

## <a name="export-tooa-bacpac-file-using-hello-azure-portal"></a>Exportar arquivo do BACPAC tooa usando Olá portal do Azure

Olá tooexport um banco de dados usando [portal do Azure](https://portal.azure.com), abra a página de saudação do banco de dados e clique em **exportar** na barra de ferramentas de saudação. Especifique o nome do arquivo BACPAC de saudação, fornecer Olá conta de armazenamento do Azure e o contêiner para exportação de saudação e fornecer Olá credenciais tooconnect toohello fonte banco de dados.  

![Exportação de banco de dados](./media/sql-database-export/database-export.png)

toomonitor progresso de saudação do hello operação de exportação, abra a página Olá Olá servidor lógico que contém Olá banco de dados que está sendo exportado. Role para baixo demais**operações** e, em seguida, clique em **importação/exportação** histórico.

![exportar histórico](./media/sql-database-export/export-history.png)
![exportar status de histórico](./media/sql-database-export/export-history2.png)

## <a name="export-tooa-bacpac-file-using-hello-sqlpackage-utility"></a>Exportar arquivo do BACPAC tooa usando o utilitário de SQLPackage Olá

tooexport um SQL banco de dados usando Olá [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) utilitário de linha de comando, consulte [Exportar parâmetros e propriedades](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties). Olá SQLPackage utilitário é fornecido com as versões mais recentes do hello [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e [SQL Server Data Tools para Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), ou você pode baixar a versão mais recente de saudação do [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) diretamente do hello Microsoft download center.

Recomendamos o uso de saudação do hello SQLPackage utilitário para dimensionamento e desempenho na maioria dos ambientes de produção. Para um SQL Server Customer Advisory Team blog sobre como migrar usando arquivos BACPAC, consulte [Migrando do SQL Server tooAzure banco de dados SQL usando arquivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

Este exemplo mostra como tooexport um banco de dados usando o SqlPackage.exe com autenticação Universal do Active Directory:

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=apptestserver.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="export-tooa-bacpac-file-using-sql-server-management-studio-ssms"></a>Exportar arquivo BACPAC tooa usando o SQL Server Management Studio (SSMS)

versões mais recentes de saudação do SQL Server Management Studio também fornecem um assistente tooexport um arquivo do banco de dados do Azure SQL tooa BACPAC. Consulte Olá [exportar um aplicativo da camada de dados](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).

## <a name="export-tooa-bacpac-file-using-powershell"></a>Exportar arquivo do BACPAC tooa usando o PowerShell

Saudação de uso [AzureRmSqlDatabaseExport novo](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) cmdlet toosubmit um toohello de solicitação de banco de dados de exportação serviço do Azure SQL Database. Dependendo do tamanho de saudação do banco de dados, a operação de exportação Olá pode levar algum tempo toocomplete.

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

status toocheck Olá Olá solicitação de exportação, use Olá [AzureRmSqlDatabaseImportExportStatus Get](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet. Executando isso imediatamente após Olá geralmente solicitação retorna **Status: em andamento**. Quando você vir **Status: bem-sucedida** Olá exportação for concluída.

```powershell
$exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
[Console]::Write("Exporting")
while ($exportStatus.Status -eq "InProgress")
{
    $exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$exportStatus
```

## <a name="next-steps"></a>Próximas etapas

* toolearn sobre retenção de backup de longo prazo de um backup de banco de dados SQL do Azure como uma alternativa tooexported um banco de dados para fins de arquivamento, consulte [retenção de backup de longo prazo](sql-database-long-term-retention.md).
- Para um SQL Server Customer Advisory Team blog sobre como migrar usando arquivos BACPAC, consulte [Migrando do SQL Server tooAzure banco de dados SQL usando arquivos BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* toolearn sobre como importar um banco de dados do SQL Server tooa BACPAC, consulte [importar um banco de dados do SQL Server de tooa BACPCAC](https://msdn.microsoft.com/library/hh710052.aspx).
* toolearn sobre como exportar um BACPAC de um banco de dados do SQL Server, consulte [exportar um aplicativo da camada de dados](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) e [migrar seu banco de dados primeiro](sql-database-migrate-your-sql-server-database.md).
* Se você estiver exportando do SQL Server como um tooAzure de toomigration prelude banco de dados SQL, consulte [migrar um banco de dados de SQL Server tooAzure banco de dados SQL](sql-database-cloud-migrate.md).
