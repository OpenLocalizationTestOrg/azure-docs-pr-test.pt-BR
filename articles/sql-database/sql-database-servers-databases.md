---
title: aaaCreate & Gerenciar servidores do SQL Azure e bancos de dados | Microsoft Docs
description: "Saiba mais sobre conceitos de banco de dados e servidor de banco de dados SQL e sobre como criar e gerenciar servidores e bancos de dados usando Olá portal do Azure PowerShell, Olá CLI do Azure, Transact-SQL e Olá API REST."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 0f526e388a5a620349f5a14e8d57a8355ac451ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-sql-database-servers-and-databases"></a>Criar e gerenciar servidores e bancos de dados do Banco de Dados SQL

Um banco de dados SQL do Azure é um banco de dados gerenciado no Microsoft Azure criado em um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) com um conjunto definido de [recursos de computação e armazenamento para cargas de trabalho diferentes](sql-database-service-tiers.md). Um banco de dados SQL do Azure está associado a um servidor lógico de Banco de Dados SQL, que é criado dentro de uma região do Azure específica. 

## <a name="an-azure-sql-database-can-be-a-single-pooled-or-partitioned-database"></a>Um banco de dados SQL do Azure pode ser um banco de dados único, em pool ou particionado

Um banco de dados SQL do Azure pode ser:

- Um banco de dados individual com seu [próprio conjunto de recursos](sql-database-what-is-a-dtu.md#what-are-database-transaction-units-dtus) (DTUs)
- Parte de um [pool elástico SQL](sql-database-elastic-pool.md) que [compartilha um conjunto de recursos](sql-database-what-is-a-dtu.md#what-are-elastic-database-transaction-units-edtus) (eDTUs)
- Parte de um [conjunto expandido de bancos de dados fragmentados](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling), que pode ser individual ou bancos de dados em pool
- Parte de um conjunto de bancos de dados que participa de um [padrão de design de SaaS multilocatário](sql-database-design-patterns-multi-tenancy-saas-applications.md), e cujos bancos de dados podem ser individuais ou bancos de dados em pool (ou ambos) 

> [!TIP]
> Para ver os nomes do banco de dados válidos, consulte [Identificadores do Banco de Dados](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers). 
>
 
- agrupamento de banco de dados padrão de saudação usado pelo banco de dados SQL do Microsoft Azure é **SQL_LATIN1_GENERAL_CP1_CI_AS**, onde **LATIN1_GENERAL** for inglês (Estados Unidos), **CP1** é a página de código 1252, **CI** diferencia maiusculas de minúsculas, e **AS** diferenciam acentos. Para obter mais informações sobre como tooset Olá agrupamento, consulte [COLLATE (Transact-SQL)](https://msdn.microsoft.com/library/ms184391.aspx).
- O Banco de Dados SQL do Microsoft Azure dá suporte ao cliente com protocolo TDS versão 7.3 ou posterior.
- São permitidas apenas conexões TCP/IP.

## <a name="what-is-an-azure-sql-logical-server"></a>O que é um servidor lógico do SQL Azure?

Um servidor lógico atua como um ponto administrativo central para vários bancos de dados, incluindo [pools elásticos SQL](sql-database-elastic-pool.md) [logons](sql-database-manage-logins.md), [regras de firewall](sql-database-firewall-configure.md), [regras de auditoria](sql-database-auditing.md), [políticas de detecção de ameaças](sql-database-threat-detection.md) e [grupos de failover](sql-database-geo-replication-overview.md). Um servidor lógico pode estar em uma região diferente da de seu grupo de recursos. servidor lógico Olá deve existir antes de criar o banco de dados do SQL Azure hello. Todos os bancos de dados em um servidor são criados dentro de saudação mesmo região como servidor lógico hello. 


> [!IMPORTANT]
> No banco de dados SQL, um servidor é um constructo lógico é diferente de uma instância do SQL Server que talvez você esteja familiarizado com em Olá, mundo local. Especificamente, Olá serviço de banco de dados SQL não faz nenhuma garantia sobre o local dos bancos de dados de saudação relação servidores lógicos tootheir e não expõe nenhum acesso de nível de instância ou recursos.
> 

Quando você cria um servidor lógico, você fornecer um servidor de conta de logon e senha que tenha direitos administrativos toohello banco de dados mestre no servidor e todos os bancos de dados criados no servidor. Essa conta inicial é uma conta de logon do SQL. O Banco de Dados SQL do Azure dá suporte à autenticação do SQL e à autenticação do Azure Active Directory. Para obter informações sobre logons e autenticação, confira [Gerenciando bancos de dados e logons no Banco de Dados SQL do Azure](sql-database-manage-logins.md). A Autenticação do Windows não é suportada. 

> [!TIP]
> Para ver os nomes de servidor e de grupo de recursos válidos, consulte [Regras e restrições de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).
>

Um servidor lógico do Banco de Dados do Azure:

- É criado dentro de uma assinatura do Azure, mas podem ser movidos com sua assinatura de recursos independentes de tooanother
- É o recurso pai de saudação para bancos de dados, pools Elásticos e data warehouses
- Fornece um namespace para bancos de dados, pools elásticos e data warehouses
- É um contêiner lógico com semântica de tempo de vida forte - delete Exclui um servidor e ele Olá bancos de dados independentes, pools Elásticos e data warehouses
- Participa [controle de acesso do Azure baseado em função (RBAC)](/active-directory/role-based-access-control-what-is) -bancos de dados, pools Elásticos e os data warehouses dentro de um servidor herdam direitos de acesso do servidor de saudação
- É um elemento de ordem superior da identidade de saudação de bancos de dados, pools Elásticos e data warehouses para recursos do Azure fins de gerenciamento (consulte Olá URL esquema de bancos de dados e grupos)
- Coloca recursos em uma região
- Fornece um ponto de extremidade de conexão para acesso ao banco de dados (<serverName>.database.windows.net)
- Fornece acesso toometadata em relação aos recursos contidos por meio de DMVs por conexão tooa banco de dados mestre 
- Fornece o escopo de saudação para políticas de gerenciamento que se aplicam a bancos de dados tooits - logons, firewall, auditoria, detecção de ameaças etc. 
- É restrito por uma cota de assinatura do pai hello (seis servidores por assinatura por padrão, - [consulte assinatura limita aqui](../azure-subscription-service-limits.md))
- Fornece o escopo de saudação de cota de banco de dados e cota de DTU para recursos de Olá nele (como 45.000 DTU)
- É o escopo de controle de versão Olá para recursos habilitados em recursos independentes 
- Os logons de entidade de segurança no nível do servidor podem gerenciar todos os bancos de dados em um servidor
- Pode conter logons toothose semelhante em instâncias do SQL Server em suas instalações que recebem acesso tooone ou mais bancos de dados no servidor de saudação e podem ser limitado concedidos direitos administrativos. Para obter mais informações, consulte [Logons](sql-database-manage-logins.md).

## <a name="azure-sql-databases-protected-by-sql-database-firewall"></a>Bancos de dados SQL do Azure protegidos pelo firewall do Banco de Dados SQL

toohelp proteger seus dados, um [firewall do banco de dados SQL](sql-database-firewall-configure.md) impede que todos os servidores de banco de dados do access tooyour ou qualquer um de seus bancos de dados de fora de seu servidor de toohello de conexão diretamente por meio de sua conexão de assinatura do Azure. conectividade do tooenable adicionais, você deve [criar uma ou mais regras de firewall](sql-database-firewall-configure.md#creating-and-managing-firewall-rules). Para criar e gerenciar pools elásticos de SQL, consulte [Pools elásticos](sql-database-elastic-pool.md).

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-portal"></a>Gerenciar servidores, bancos de dados e firewall usando o portal do Azure de saudação do SQL Azure

Você pode criar o grupo de recursos de saudação do Azure SQL do banco de dados antecipadamente ou ao criar o próprio servidor de saudação. Há vários métodos para obter o novo formulário do servidor de SQL tooa, criando um novo servidor SQL ou como parte da criação de um novo banco de dados. 

### <a name="create-a-blank-sql-server-logical-server"></a>Criar um SQL server (servidor lógico) em branco

Olá toocreate um servidor (sem um banco de dados) de banco de dados SQL usando [portal do Azure](https://portal.azure.com), navegar tooa em branco SQL server (servidor lógico) formulário. Olá seguinte captura de tela mostra um método para abrir um formulário toocreate um servidor SQL lógico em branco. 

   ![criar formulário de servidor lógico concluído](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

Se você receber o formulário toothis usando outro método, Olá informações formulário Olá são idênticas.

### <a name="create-a-blank-or-sample-sql-database"></a>Criar um banco de dados SQL em branco ou de exemplo

Olá toocreate um banco de dados SQL do Azure usando [portal do Azure](https://portal.azure.com), navegar tooa formulário de banco de dados SQL em branco e forneça Olá solicitou informações. Você pode criar grupo de recursos hello Azure SQL do banco de dados e o servidor lógico antecipadamente ou durante a criação de saudação próprio banco de dados. Você pode criar um banco de dados em branco ou um banco de dados de exemplo com base no Adventure Works LT. 

  ![criar database-1](./media/sql-database-get-started-portal/create-database-1.png)

> [IMPORTANTE] Para obter informações sobre como selecionar Olá preços para seu banco de dados, consulte [camadas de serviço](sql-database-service-tiers.md).
>

### <a name="manage-an-existing-sql-server"></a>Gerenciar um SQL Server existente

toomanage um servidor existente, navegue toohello servidor usando um número de métodos - tais como página de banco de dados SQL específica, hello **servidores SQL** página ou hello **todos os recursos** página. Olá seguinte captura de tela mostra como toobegin definindo um firewall de nível de servidor da saudação **visão geral** página para um servidor. 

   ![visão geral do servidor lógico](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

toomanage banco de dados existente, navegue toohello **bancos de dados SQL** página e clique em banco de dados de saudação desejar toomanage. Olá seguinte captura de tela mostra como toobegin definindo um firewall de nível de servidor para um banco de dados da saudação **visão geral** página para um banco de dados. 

   ![regra de firewall do servidor](./media/sql-database-get-started-portal/server-firewall-rule.png) 

> [!IMPORTANT]
> Propriedades de desempenho de tooconfigure para um banco de dados, consulte [camadas de serviço](sql-database-service-tiers.md).
>

> [!TIP]
> Para obter um tutorial de início rápido do portal do Azure, consulte [criar um banco de dados do SQL Azure no portal do Azure de saudação](sql-database-get-started-portal.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-powershell"></a>Gerenciar servidores, bancos de dados e firewalls do SQL Azure usando o PowerShell do Azure

toocreate e gerenciar o servidor SQL do Azure, bancos de dados e firewalls com o Azure PowerShell, use Olá cmdlets do PowerShell a seguir. Se você precisa tooinstall ou atualize o PowerShell, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps). Para criar e gerenciar pools elásticos de SQL, consulte [Pools elásticos](sql-database-elastic-pool.md).

| Cmdlet | Descrição |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Cria um banco de dados |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Obtém um ou mais bancos de dados|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Define propriedades para um banco de dados ou move um banco de dados existente para um pool, elástico|
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|Remove um banco de dados|
|[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)|Cria um grupos de recursos]
|[New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver)|Cria um servidor|
|[Get-AzureRmSqlServer](/powershell/module/azurerm.sql/get-azurermsqlserver)|Retorna informações sobre servidores|
|[Set-AzureRmSqlServer](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/set-azurermsqlserver)|Modifica as propriedades de um servidor|
|[Remove-AzureRmSqlServer](/powershell/module/azurerm.sql/remove-azurermsqlserver)|Remove um servidor|
|[New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule)|Cria uma regra de firewall no nível de servidor |
|[Get-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/get-azurermsqlserverfirewallrule)|Obtém as regras de firewall para um servidor|
|[Set-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/set-azurermsqlserverfirewallrule)|Modifica uma regra de firewall em um servidor|
|[Remove-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/remove-azurermsqlserverfirewallrule)|Exclui uma regra de firewall de um servidor.|

> [!TIP]
> Para obter um tutorial de início rápido do PowerShell, confira [Criar um único banco de dados SQL do Azure usando o PowerShell](sql-database-get-started-portal.md). Para scripts de exemplo do PowerShell, consulte [toocreate de usar o PowerShell um único SQL Azure de banco de dados e configurar uma regra de firewall](scripts/sql-database-create-and-configure-database-powershell.md) e [monitorar e escala de um único SQL de banco de dados usando o PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-cli"></a>Gerenciar servidores, bancos de dados e firewalls usando Olá CLI do Azure SQL Azure

toocreate e gerenciar o Azure SQL server, bancos de dados e firewalls com hello [CLI do Azure](/cli/azure/overview), use os seguintes Olá [banco de dados do SQL Azure CLI](/cli/azure/sql/db) comandos. Saudação de uso [nuvem Shell](/azure/cloud-shell/overview) toorun Olá CLI em seu navegador, ou [instalar](/cli/azure/install-azure-cli) -la no Windows, Linux ou macOS. Para criar e gerenciar pools elásticos de SQL, consulte [Pools elásticos](sql-database-elastic-pool.md).

| Cmdlet | Descrição |
| --- | --- |
|[az sql db create](/cli/azure/sql/db#create) |Cria um banco de dados|
|[az sql db list](/cli/azure/sql/db#list)|Lista todos os bancos de dados e data warehouses em um servidor, ou todos os bancos de dados em um pool elástico|
|[az sql db list-editions](/cli/azure/sql/db#list-editions)|Lista os objetivos de serviço disponíveis e os limites de armazenamento|
|[az sql db list-usages](/cli/azure/sql/db#list-usages)|Retorna os usos do banco de dados|
|[az sql db show](/cli/azure/sql/db#show)|Obtém um banco de dados ou data warehouse|
|[az sql db update](/cli/azure/sql/db#update)|Atualiza um banco de dados|
|[az sql db delete](/cli/azure/sql/db#delete)|Remove um banco de dados|
|[az group create](/cli/azure/group#create)|Cria um grupos de recursos|
|[az sql server create](/cli/azure/sql/server#create)|Cria um servidor|
|[az sql server list](/cli/azure/sql/server#list)|Lista servidores|
|[az sql server list-usages](/cli/azure/sql/server#list-usages)|Retorna os usos do servidor|
|[az sql server show](/cli/azure/sql/server#show)|Obtém um servidor|
|[az sql server update](/cli/azure/sql/server#update)|Atualiza um servidor|
|[az sql server delete](/cli/azure/sql/server#delete)|Exclui um servidor|
|[az sql server firewall-rule create](/cli/azure/sql/server/firewall-rule#create)|Cria uma regra de firewall de servidor|
|[az sql server firewall-rule list](/cli/azure/sql/server/firewall-rule#list)|Lista as regras de firewall de saudação em um servidor|
|[az sql server firewall-rule show](/cli/azure/sql/server/firewall-rule#show)|Mostra detalhes de saudação de uma regra de firewall|
|[az sql server firewall-rule update](/cli/azure/sql/server/firewall-rule#update)|Atualiza uma regra de firewall|
|[az sql server firewall-rule delete](/cli/azure/sql/server/firewall-rule#delete)|Exclui uma regra de firewall|

> [!TIP]
> Para um tutorial de início rápido da CLI do Azure, consulte [criar um único banco de dados SQL do Azure usando Olá CLI do Azure](sql-database-get-started-cli.md). Para scripts de exemplo da CLI do Azure, consulte [toocreate CLI Use um único SQL Azure de banco de dados e configurar uma regra de firewall](scripts/sql-database-create-and-configure-database-cli.md) e [toomonitor CLI Use e escala de um único banco de dados do SQL](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-transact-sql"></a>Gerenciar servidores, bancos de dados e firewalls do SQL Azure usando o Transact-SQL

toocreate e gerenciar o servidor SQL do Azure, bancos de dados e firewalls com Transact-SQL, use Olá comandos T-SQL a seguir. Você pode executar esses comandos usando Olá portal do Azure, [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [código do Visual Studio](https://code.visualstudio.com/docs), ou qualquer outro programa que pode conectar-se o servidor de banco de dados do Azure SQL tooan e passar o Transact-SQL comandos. Para gerenciar pools elásticos SQL, consulte [Pools elásticos](sql-database-elastic-pool.md).

> [!IMPORTANT]
> Não é possível criar ou excluir um servidor usando o Transact-SQL.
>

| Command | Descrição |
| --- | --- |
|[CREATE DATABASE (Banco de Dados SQL do Azure)](/sql/t-sql/statements/create-database-azure-sql-database)|Cria um novo banco de dados. Você deve ser conectado toohello banco de dados mestre toocreate um novo banco de dados.|
| [ALTER DATABASE (Banco de Dados SQL do Azure)](/sql/t-sql/statements/alter-database-azure-sql-database) |Modifica um Banco de Dados SQL do Azure. |
|[ALTER DATABASE (SQL Data Warehouse do Microsoft Azure)](/sql/t-sql/statements/alter-database-azure-sql-data-warehouse)|Modifica um SQL Data Warehouse do Azure.|
|[DROP DATABASE (Transact-SQL)](/sql/t-sql/statements/drop-database-transact-sql)|Exclui um banco de dados.|
|[sys.database_service_objectives (Banco de Dados SQL do Azure)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Retorna Olá edition (camada de serviço), o objetivo de serviço (preço) e o nome do pool Elástico, se houver, para um banco de dados do SQL Azure ou um Azure SQL Data Warehouse. Se conectado no banco de dados mestre em um servidor de banco de dados do Azure SQL toohello, retorna informações sobre todos os bancos de dados. Para o Azure SQL Data Warehouse, você deve ser conectado toohello banco de dados mestre.|
|[sys.dm_db_resource_stats (Banco de Dados SQL do Azure)](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database)| Retorna o consumo de CPU, E/S e memória para um banco de dados do Banco de Dados SQL do Azure. Existe uma linha para cada 15 segundos, mesmo se não houver nenhuma atividade no banco de dados de saudação.|
|[sys.resource_stats (Banco de Dados SQL do Azure)](/sql/relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database)|Retorna o uso de CPU e dados de armazenamento para um Banco de Dados SQL do Azure. dados de saudação são coletados e agregados em intervalos de cinco minutos.|
|[sys.database_connection_stats (Banco de Dados SQL do Azure)](/sql/relational-databases/system-catalog-views/sys-database-connection-stats-azure-sql-database)|Contém estatísticas para eventos de conectividade de banco de dados do Banco de Dados SQL, fornecendo uma visão geral da conexão de banco de dados e das falhas. |
|[sys.event_log (Banco de Dados SQL do Azure)](/sql/relational-databases/system-catalog-views/sys-event-log-azure-sql-database)|Retorna as conexões de banco de dados do Banco de Dados SQL do Azure com êxito, as falhas de conexão e os deadlocks. Você pode usar este tootrack informações ou solucionar problemas de sua atividade de banco de dados com o banco de dados SQL.|
|[sp_set_firewall_rule (Banco de Dados SQL do Azure)](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)|Cria ou atualiza as configurações de firewall de nível de servidor de saudação para o servidor de banco de dados SQL. Esse procedimento armazenado só está disponível no logon do banco de dados mestre toohello nível de servidor principal hello. Uma regra de firewall de nível de servidor só pode ser criada usando Transact-SQL após a primeira regra de firewall de nível de servidor Olá foi criada por um usuário com permissões no nível do Azure|
|[sys.firewall_rules (Banco de Dados SQL do Azure)](/sql/relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database)|Retorna informações sobre configurações de firewall de nível de servidor de saudação associadas ao seu banco de dados de SQL do Microsoft Azure.|
|[sp_delete_firewall_rule (Banco de Dados SQL do Azure)](/sql/relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database)|Remove as configurações de firewall no nível do servidor do servidor do Banco de Dados SQL. Esse procedimento armazenado só está disponível no logon do banco de dados mestre toohello nível de servidor principal hello.|
|[sp_set_database_firewall_rule (Banco de Dados SQL do Azure)](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)|Cria ou atualiza regras de firewall no nível de banco de dados de saudação para seu banco de dados do SQL Azure ou o SQL Data Warehouse. Regras de firewall do banco de dados podem ser configuradas para o banco de dados mestre hello e para bancos de dados de usuário no banco de dados SQL. As regras de firewall do banco de dados são úteis quando você usa usuários de banco de dados independentes. |
|[sys.database_firewall_rules (Banco de Dados SQL do Azure)](/sql/relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database)|Retorna informações sobre configurações de firewall de nível de banco de dados de saudação associadas ao seu banco de dados de SQL do Microsoft Azure. |
|[sp_delete_database_firewall_rule (Banco de Dados SQL do Azure)](/sql/relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database)|Remove a configuração de firewall no nível do banco de dados para o Banco de Dados SQL do Azure ou o SQL Data Warehouse. |


> [!TIP]
> Tutorial de início rápido usando o SQL Server Management Studio no Microsoft Windows, consulte [banco de dados do SQL Azure: Use SQL Server Management Studio tooconnect e consultar dados](sql-database-connect-query-ssms.md). Para obter um tutorial de início rápido usando o código do Visual Studio em Olá macOS, Linux ou Windows, consulte [banco de dados SQL: o código do Visual Studio para usar tooconnect e consultar dados](sql-database-connect-query-vscode.md).

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-rest-api"></a>Gerenciar servidores, bancos de dados e firewalls usando a API REST de saudação do SQL Azure

toocreate e gerenciar o servidor SQL do Azure, bancos de dados e firewalls usando Olá API REST, consulte [API de REST de banco de dados SQL do Azure](/rest/api/sql/).

## <a name="next-steps"></a>Próximas etapas

- toolearn sobre o pool de bancos de dados usando pools Elásticos do SQL, consulte [pools Elásticos](sql-database-elastic-pool.md).
- Para obter informações sobre Olá serviço de banco de dados SQL, consulte [o que é o banco de dados SQL?](sql-database-technical-overview.md).
- toolearn sobre como migrar uma tooAzure de banco de dados do SQL Server, consulte [migrar o banco de dados SQL do tooAzure](sql-database-cloud-migrate.md).
- Para obter informações sobre os recursos com suporte, consulte [Recursos](sql-database-features.md).
