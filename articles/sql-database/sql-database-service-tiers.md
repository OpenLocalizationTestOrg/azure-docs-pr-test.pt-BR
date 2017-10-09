---
title: "Níveis de serviço e desempenho do Banco de Dados SQL do Azure | Microsoft Docs"
description: "Comparar os níveis de serviço e desempenho do Banco de Dados SQL para bancos de dados únicos e apresentar pools elásticos de SQL"
keywords: "opções de banco de dados, desempenho do banco de dados"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: f5c5c596-cd1e-451f-92a7-b70d4916e974
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: b27b78788614d32e6c0c4267fe0ce504ebd2f444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-performance-options-are-available-for-an-azure-sql-database"></a>Quais opções de desempenho estão disponíveis para um Banco de Dados SQL do Azure

O [Banco de Dados SQL do Azure](sql-database-technical-overview.md) oferece quatro níveis de serviço para bancos de dados individuais e [em pool](sql-database-elastic-pool.md). Esses níveis de serviço são: **Básica**, **Standard**, **Premium** e **Premium RS**. Dentro de cada camada de serviço estão vários níveis de desempenho ([DTUs](sql-database-what-is-a-dtu.md)) e as opções de armazenamento toohandle tamanhos diferentes de cargas de trabalho e dados. Altos níveis de desempenho fornecem computação adicional e recursos de armazenamento criado toodeliver progressivos de produtividade e de capacidade. Você pode alterar os níveis de serviço, os níveis de desempenho e o armazenamento sem tempo de inatividade. 
- Os níveis serviço **Básico**, **Standard** e **Premium** têm um SLA de tempo de atividade de 99,99%, opções de continuidade dos negócios flexíveis, recursos de segurança e cobrança por hora. 
- Olá **Premium RS** camada fornece Olá mesmos níveis de desempenho como hello camada Premium com um SLA reduzido porque ele é executado com um número menor de cópias redundantes que um banco de dados Olá outros níveis de serviço. Portanto, no caso de saudação de uma falha no serviço, talvez seja necessário toorecover seu banco de dados de um backup com backup tooa retardo de 5 minutos.

> [!IMPORTANT]
> Um banco de dados do SQL Azure é um conjunto garantido de recursos e Olá esperado características de desempenho de seu banco de dados não são afetadas por qualquer outro banco de dados no Azure. 

## <a name="choosing-a-service-tier"></a>Como escolher uma camada de serviço
Olá, tabela a seguir fornece exemplos das camadas de saudação melhor adequados para cargas de trabalho de aplicativo diferente.

| Camada de serviço | Cargas de trabalho de destino |
| :--- | --- |
| **Básico** | Mais adequada para um banco de dados pequeno, suporta normalmente uma única operação ativa em um determinado momento. Os exemplos incluem bancos de dados usados para desenvolvimento ou teste ou aplicativos de pequena escala usados com pouca frequência. |
| **Standard** |Olá go-toooption para aplicativos em nuvem com requisitos de desempenho de e/s toomedium baixa, permitindo várias consultas simultâneas. Os exemplos incluem aplicativos da web ou de grupo de trabalho. |
| **Premium** | Projetado para volume transacional alto com requisitos de desempenho de e/s altos, suportando muitos usuários simultâneos. Os exemplos são bancos de dados com suporte a aplicativos de missão críticos. |
| **Premium RS** | Projetado para cargas de trabalho com uso intensivo de e/s que não necessitam de garantias do hello mais altas disponibilidade. Exemplos de teste de cargas de trabalho de alto desempenho, ou uma carga de trabalho analítica onde o banco de dados de saudação não é sistema saudação do registro. |
|||

Você pode criar bancos de dados individuais com recursos dedicados dentro de um nível de serviço em um [nível de desempenho](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) específico ou você também pode criar bancos de dados dentro de um [pool elástico de SQL](sql-database-service-tiers.md#elastic-pool-service-tiers-and-performance-in-edtus). Em um pool Elástico do SQL, os recursos de computação e armazenamento Olá são compartilhados entre vários bancos de dados dentro de um único servidor lógico. 

Os recursos disponíveis para bancos de dados individuais são expressos em termos de DTUs (Unidades de Transmissão de Dados), e os recursos para pools elásticos de SQL são expressos em termos de eDTUs (Unidades de Transação de Banco de Dados Elástico). Para saber mais sobre DTUs e eDTUs, confira [O que são DTUs e eDTUs?](sql-database-what-is-a-dtu.md).

toodecide em uma camada de serviço, inicie determinando recursos de banco de dados mínimo Olá que você precisa:

| **Recursos de camada de serviço** | **Básico** | **Standard** | **Premium** | **Premium RS**|
| :-- | --: | --: | --: | --: |
| Tamanho máximo de banco de dados individual | 2 GB | 250 GB | 4 TB*  | 500 GB  |
| Tamanho máximo do pool elástico | 156 GB | 2.9 TB | 4 TB* | 750 GB |
| Tamanho máximo do banco de dados em um pool elástico | 2 GB | 250 GB | 500 GB | 500 GB |
| Número máximo de bancos de dados por pool | 500  | 500 | 100 | 100 |
| Máximo de DTUs de um banco de dados individual | 5 | 100 | 4000 | 1000 |
| Máximo de DTUs por banco de dados em um pool elástico | 5 | 3000 | 4000 | 1000 |
| Período de retenção do backup de banco de dados | 7 dias | 35 dias | 35 dias | 35 dias |
||||||

> [!IMPORTANT]
> Armazenamento de too4 TB está disponível em Olá seguintes regiões: US East2, oeste dos EUA, nos Gov Virgínia, Europa Ocidental, Alemanha Central, Sul Leste da Ásia, Leste do Japão, Leste da Austrália, Canadá Central e Leste do Canadá. Consulte [Limitações atuais 4 TB](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize)
>

Depois de ter determinado da camada de serviço apropriado hello, você está pronto toodetermine nível de desempenho de saudação (número de saudação de DTUs) e a quantidade de armazenamento Olá para o banco de dados de saudação. 

- Olá S2 e S3 níveis de desempenho em Olá **padrão** camada geralmente são um bom ponto de partida. 
- Para bancos de dados com altas exigências de CPU ou e/s, Olá níveis de desempenho em Olá **Premium** camada são o ponto de partida direita hello. 
- Olá **Premium** camada oferece mais CPU e inicia em 10 vezes mais e/s em comparação com toohello mais alto nível de desempenho em Olá **padrão** camada.
- Olá **PremiumRS** camada oferece desempenho de saudação do hello **Premium** camada a um custo menor, mas com um SLA reduzido.

> [!IMPORTANT]
> Saudação de revisão [pools Elásticos SQL](sql-database-elastic-pool.md) tópico para obter detalhes de saudação sobre agrupamento de bancos de dados em Elástico SQL pools de recursos de computação e armazenamento tooshare. Olá restante neste tópico se concentra em camadas de serviço e níveis de desempenho para bancos de dados único.
>

## <a name="single-database-service-tiers-and-performance-levels"></a>Camadas de serviço e níveis de desempenho de banco de dados individual
Para bancos de dados individuais, há vários níveis de desempenho e quantidades de armazenamento dentro de cada nível de serviço. 

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

## <a name="scaling-up-or-scaling-down-a-single-database"></a>Escalar verticalmente ou reduzir um banco de dados

Depois de escolher inicialmente um nível de desempenho e da camada de serviço, você pode dimensionar um banco de dados para cima ou para baixo dinamicamente com base na experiência real.  

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-dynamically-scale-up-or-scale-down/player]
>

Alterar o nível de camada e/ou o desempenho de serviço de saudação de um banco de dados cria uma réplica de banco de dados original Olá no novo nível de desempenho hello e alterna conexões toohello réplica. Nenhum dado seja perdido durante esse processo, mas durante a saudação breve momento em que podemos passar toohello réplica, toohello de conexões de banco de dados são desabilitadas, portanto algumas transações em trânsito podem ser revertidas. Olá período de tempo para alterar Olá varia, mas é geralmente em 4 segundos é menor que 30 segundos 99% de tempo de saudação. Se houver grandes números de transações em trânsito em conexões de momento Olá estão desabilitadas, hello período de tempo para alterar Olá pode ser maior.  

durante todo o processo de expansão Olá Olá depende tanto o tamanho da saudação e camada de serviço de saudação do banco de dados antes e depois alterar hello. Por exemplo, um banco de dados de 250 GB que está mudando para, de ou dentro de uma camada de serviço Standard deverá ser concluída dentro de 6 horas. Para um banco de dados de saudação mesmo tamanho alterando níveis de desempenho dentro da camada de serviço Premium Olá, ele deve ser concluída dentro de 3 horas.

> [!TIP]
> toocheck status de saudação de um banco de dados SQL em andamento a operação de dimensionamento, você pode usar o hello consulta a seguir: ```select * from sys.dm_operation_status```.
>

* Se você estiver atualizando tooa nível mais alto de camadas ou de desempenho do serviço, tamanho máximo Olá não aumenta, a menos que você especificar explicitamente um tamanho máximo maior.
* toodowngrade um banco de dados, banco de dados de saudação deve ser menor que o tamanho máximo permitido de saudação da camada de serviço de destino hello. 
* Ao atualizar um banco de dados com [georeplicação](sql-database-geo-replication-portal.md) habilitado, atualize seu nível de desempenho desejado toohello bancos de dados secundários antes de atualizar o banco de dados primário do hello (guia Geral). Ao atualizar tooa diferente edição ugrading Olá banco de dados secundário primeiro é necessário. 
* Ao fazer o downgrade de um banco de dados com [georeplicação](sql-database-geo-replication-portal.md) habilitado, fazer o downgrade de sua camada de desempenho desejado toohello bancos de dados primário antes de rebaixar o banco de dados secundário do hello (guia Geral). Ao fazer o downgrade tooa diferente edição downgrade Olá banco de dados primário primeiro é necessário. 

* Olá ofertas de serviço de restauração são diferentes para Olá várias camadas de serviço. Se você estiver fazendo downgrade toohello **básica** camada, você terá um período de retenção de backup inferior - consulte [Backups de banco de dados do SQL Azure](sql-database-automated-backups.md).
* novas propriedades de saudação do banco de dados de saudação não são aplicadas até Olá alterações forem concluídas.


## <a name="current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize"></a>Limitações atuais de bancos de dados P11 e P15 com tamanho máximo de 4 TB

Há suporte para um tamanho máximo de 4 TB para banco de dados P11 e P15 em algumas regiões (conforme discutido anteriormente). Olá considerações e limitações a seguir se aplicam tooP11 e bancos de dados P15 com maxsize de 4 TB:

- Se você escolher a opção de maxsize de 4 TB Olá durante a criação de um banco de dados (usando um valor de 4 TB ou 4096 GB), Olá criar comando falhará com um erro se o banco de dados de saudação é provisionado em uma região sem suporte.
- P11 e P15 bancos de dados existentes localizados em uma das regiões Olá com suporte, você pode aumentar Olá maxsize armazenamento too4 TB. Isso pode ser verificado usando Olá [DATABASEPROPERTYEX selecione](https://msdn.microsoft.com/library/ms186823.aspx) ou inspecionando o tamanho do banco de dados de saudação em Olá portal do Azure. Atualizando um P11 existente ou P15 banco de dados pode somente ser executado por um logon principal no nível de servidor ou por membros da função de banco de dados dbmanager hello. 
- Se uma operação de atualização é executada em uma configuração de saudação de região com suporte é atualizada imediatamente. Olá permanecerá online durante o processo de atualização de saudação. No entanto, você não pode utilizar Olá completo 4 TB de armazenamento até que os arquivos de banco de dados real Olá foram atualizados toohello maxsize de novo. comprimento de saudação do tempo necessário depende no tamanho de saudação do banco de dados hello está sendo atualizado.  
- Ao criar ou atualizar um banco de dados P11 ou P15, você só pode escolher entre 1 TB e 4 TB de tamanho máximo. Atualmente, não há suporte para tamanhos de armazenamento intermediários. Ao criar um P11/P15, opção de armazenamento saudação padrão de 1 TB é pré-selecionada. Para bancos de dados localizados em uma das regiões Olá com suporte, você pode aumentar Olá too4TB máximo do armazenamento de banco de dados único novo ou existente. Para todas as outras regiões, o tamanho máximo não pode ultrapassar 1 TB. preço de saudação não altera quando você seleciona 4 TB de armazenamento incluído.
- Olá maxsize do banco de dados de 4 TB não pode ser alterado too1 TB mesmo se o armazenamento real do hello usado está abaixo de 1 TB. Portanto, você não pode fazer downgrade de um tooa P11 - 4 TB/P15 - 4 TB P11 - 1 TB/P15 - 1 TB ou uma camada de desempenho inferior, por exemplo, tooP1-P6) até que estamos fornecendo opções adicionais de armazenamento para o restante de saudação do hello níveis de desempenho. Essa restrição também se aplica a restauração de toohello e cenários de cópia, incluindo o point-in-time, a restauração geográfica, longo-prazo-backup-retenção e cópia de banco de dados. Quando um banco de dados está configurado com a opção de 4 TB hello, todas as operações de restauração desse banco de dados devem ser executadas em um P11/P15 com maxsize de 4 TB.
- Quando criar ou atualizar um banco de dados em uma região sem suporte, P11/P15 hello cria ou operação de atualização falha com a seguinte mensagem de erro de saudação: **P11 e P15 banco de dados com backup too4TB de armazenamento estão disponíveis nos East2, oeste dos EUA, nós Gov Virgínia, Europa Ocidental, Alemanha Central, Sudeste da Ásia, Leste do Japão, Leste da Austrália, Central do Canadá e Leste do Canadá.**
- Para cenários com replicação geográfica ativa:
   - Configurar uma relação de replicação geográfica: se o banco de dados primário Olá é P11 ou P15, Olá secondary(ies) também deve ser P11 ou P15; níveis de desempenho inferiores são rejeitadas como secundários, desde que eles não são capazes de dar suporte a 4 TB.
   - Atualizando Olá banco de dados primário em uma relação de replicação geográfica: alterar Olá maxsize too4 TB em um banco de dados principal dispara Olá mesmo alterar no banco de dados secundário hello. As duas atualizações devem ser bem-sucedidas para alteração de saudação em efeito do hello tootake primário. Região para a opção de 4TB Olá limitações (veja acima). Se for Olá secundário em uma região que não oferece suporte a 4 TB, Olá primário não está atualizado.
- Não há suporte para o usando o serviço de importação/exportação Olá para carregar bancos de dados P11 - 4TB/P15 - 4TB. Use SqlPackage.exe muito[importar](sql-database-import.md) e [exportar](sql-database-export.md) dados.

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-portal"></a>Gerenciar as camadas de serviço único banco de dados e níveis de desempenho usando Olá portal do Azure

Olá de tooset ou alteração da camada de serviço, o nível de desempenho ou a quantidade de armazenamento para um novo ou existente do Azure SQL banco de dados usando Olá portal do Azure, abra Olá **Configure desempenho** janela para o banco de dados clicando em  **Tipo de preço (escala DTUs)** - conforme Olá captura de tela a seguir. 

- Definir ou alterar a camada de serviço Olá selecionando a camada de serviço Olá para sua carga de trabalho. 
- Definir ou alterar o nível de desempenho da saudação (**DTUs**) dentro de uma camada de serviço usando Olá **DTU** controle deslizante.
- Definir ou alterar a quantidade de armazenamento Olá para nível de desempenho hello usando Olá **armazenamento** controle deslizante. 

  ![Definir o nível de serviço e o nível de desempenho](./media/sql-database-service-tiers/service-tier-performance-level.png)

> [!IMPORTANT]
> Revise [Limitações atuais de bancos de dados P11 e P15 com tamanho máximo de 4 TB](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize) ao selecionar um nível de serviço P11 ou P15.
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-powershell"></a>Gerenciar níveis de serviço e níveis de desempenho de banco de dados individual usando o PowerShell

camadas de serviço de bancos de dados SQL do Azure tooset ou alteração, níveis de desempenho e a quantidade de armazenamento usando o PowerShell, usam Olá cmdlets do PowerShell a seguir. Se você precisa tooinstall ou atualize o PowerShell, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps). 

| Cmdlet | Descrição |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Cria um banco de dados |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Obtém um ou mais bancos de dados|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Define propriedades para um banco de dados ou move um banco de dados existente para um pool, elástico|


> [!TIP]
> Para um script de exemplo do PowerShell que monitora as métricas de desempenho de saudação de um banco de dados, redimensiona tooa mais alto nível de desempenho e cria uma regra de alerta em uma saudação métricas de desempenho, consulte [monitorar e escala de um único SQL de banco de dados usando PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md).

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-cli"></a>Gerenciar as camadas de serviço único banco de dados e níveis de desempenho usando Olá CLI do Azure

camadas de serviço de bancos de dados SQL do Azure tooset ou alteração, níveis de desempenho e a quantidade de armazenamento usando Olá CLI do Azure, usam o seguinte de Olá [banco de dados do SQL Azure CLI](/cli/azure/sql/db) comandos. Saudação de uso [nuvem Shell](/azure/cloud-shell/overview) toorun Olá CLI em seu navegador, ou [instalar](/cli/azure/install-azure-cli) -la no Windows, Linux ou macOS. Para criar e gerenciar pools elásticos de SQL, consulte [Pools elásticos](sql-database-elastic-pool.md).

| Cmdlet | Descrição |
| --- | --- |
|[az sql db create](/cli/azure/sql/db#create) |Cria um banco de dados|
|[az sql db list](/cli/azure/sql/db#list)|Lista todos os bancos de dados e data warehouses em um servidor, ou todos os bancos de dados em um pool elástico|
|[az sql db list-editions](/cli/azure/sql/db#list-editions)|Lista os objetivos de serviço disponíveis e os limites de armazenamento|
|[az sql db list-usages](/cli/azure/sql/db#list-usages)|Retorna os usos do banco de dados|
|[az sql db show](/cli/azure/sql/db#show)|Obtém um banco de dados ou data warehouse|
|[az sql db update](/cli/azure/sql/db#update)|Atualiza um banco de dados|

> [!TIP]
> Para um script de exemplo da CLI do Azure que se expande um único nível de desempenho diferentes de tooa de banco de dados SQL do Azure depois de consultar informações sobre o tamanho do banco de dados de saudação hello, consulte [toomonitor CLI Use e escala de um único banco de dados do SQL](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-transact-sql"></a>Gerenciar níveis de serviço e níveis de desempenho de banco de dados individual usando Transact-SQL

camadas de serviço de bancos de dados SQL do Azure tooset ou alteração, níveis de desempenho e a quantidade de armazenamento com o Transact-SQL, usam Olá comandos T-SQL a seguir. Você pode executar esses comandos usando Olá portal do Azure, [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [código do Visual Studio](https://code.visualstudio.com/docs), ou qualquer outro programa que pode conectar-se o servidor de banco de dados do Azure SQL tooan e passar o Transact-SQL comandos. 

| Command | Descrição |
| --- | --- |
|[CREATE DATABASE (Banco de Dados SQL do Azure)](/sql/t-sql/statements/create-database-azure-sql-database)|Cria um novo banco de dados. Você deve ser conectado toohello banco de dados mestre toocreate um novo banco de dados.|
| [ALTER DATABASE (Banco de Dados SQL do Azure)](/sql/t-sql/statements/alter-database-azure-sql-database) |Modifica um Banco de Dados SQL do Azure. |
|[sys.database_service_objectives (Banco de Dados SQL do Azure)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Retorna Olá edition (camada de serviço), o objetivo de serviço (preço) e o nome do pool Elástico, se houver, para um banco de dados do SQL Azure ou um Azure SQL Data Warehouse. Se conectado no banco de dados mestre em um servidor de banco de dados do Azure SQL toohello, retorna informações sobre todos os bancos de dados. Para o Azure SQL Data Warehouse, você deve ser conectado toohello banco de dados mestre.|
|[sys.database_usage (Banco de Dados SQL do Azure)](/sql/relational-databases/system-catalog-views/sys-database-usage-azure-sql-database)|Lista o número hello, tipo e duração de bancos de dados em um servidor de banco de dados SQL.|

Olá, exemplo a seguir mostra Olá maxsize que está sendo alterada usando o comando ALTER DATABASE de saudação:

 ```sql
ALTER DATABASE <myDatabaseName> 
   MODIFY (MAXSIZE = 4096 GB);
```

## <a name="manage-single-databases-using-hello-rest-api"></a>Gerenciar bancos de dados único usando a API REST de saudação

camadas de serviço de bancos de dados SQL do Azure tooset ou alteração, níveis de desempenho e a quantidade de armazenamento usando Olá API REST, consulte [API de REST de banco de dados SQL do Azure](/rest/api/sql/).

## <a name="next-steps"></a>Próximas etapas

* Saiba mais sobre [DTUs](sql-database-what-is-a-dtu.md).
* toolearn sobre como monitorar o uso de DTU, consulte [monitoramento e ajuste de desempenho](sql-database-troubleshoot-performance.md).

