---
title: "aaaMigrate toopremium armazenamento de depósito de dados existentes do Azure | Microsoft Docs"
description: "Instruções para migrar um armazenamento toopremium existente do data warehouse"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a>Migrar o armazenamento do data warehouse toopremium
Recentemente, o Azure SQL Data Warehouse apresentou o [Armazenamento premium para maior previsibilidade de desempenho][premium storage for greater performance predictability]. Os dados existentes warehouses atualmente no armazenamento padrão podem ser migrados toopremium armazenamento. Você pode tirar proveito da migração automática, ou se você preferir toocontrol quando toomigrate (que envolvem algum tempo de inatividade), você pode fazer Olá a migração.

Se você tiver mais de um data warehouse, use Olá [agenda a migração automática] [ automatic migration schedule] toodetermine quando ele também será migrado.

## <a name="determine-storage-type"></a>Determinar o tipo de armazenamento
Se você tiver criado um data warehouse antes de saudação datas a seguir, você está usando atualmente o armazenamento padrão.

| **Região** | **Data warehouse criado antes desta data** |
|:--- |:--- |
| Leste da Austrália |Armazenamento premium ainda não disponível |
| Leste da China |1º de novembro de 2016 |
| Norte da China |1º de novembro de 2016 |
| Alemanha Central |1º de novembro de 2016 |
| Nordeste da Alemanha |1º de novembro de 2016 |
| Oeste da Índia |Armazenamento premium ainda não disponível |
| Oeste do Japão |Armazenamento premium ainda não disponível |
| Centro-Norte dos EUA |10 de novembro de 2016 |

## <a name="automatic-migration-details"></a>Detalhes da migração automática
Por padrão, irá migrar seu banco de dados para que você entre 6:00 e às 6:00 AM na hora local, da região durante a saudação [agenda a migração automática][automatic migration schedule]. O data warehouse existente será inutilizável durante a migração de saudação. migração de saudação levará aproximadamente uma hora por terabyte de armazenamento por depósito de dados. Você não será cobrado durante qualquer parte da migração automática de saudação.

> [!NOTE]
> Quando a saudação migração for concluída, o data warehouse será novamente online e utilizável.
>
>

Microsoft está demorando Olá após a migração de saudação toocomplete etapas (eles não exigem qualquer envolvimento de sua parte). Neste exemplo, imagine que o data warehouse existente no armazenamento standard é chamado atualmente de "MyDW".

1. Microsoft renomeia "MyDW" muito "MyDW_DO_NOT_USE_ [Timestamp]".
2. A Microsoft pausa o “MyDW_DO_NOT_USE_[carimbo de data/hora]”. Durante esse tempo, um backup é feito. Você poderá ver várias pausas e retomadas se encontrarmos problemas durante o processo.
3. Microsoft cria um novo data warehouse denominado "MyDW" no armazenamento premium do backup Olá feito na etapa 2. "MyDW" não será exibido até após a conclusão da restauração de saudação.
4. Após a conclusão da restauração hello, "MyDW" retorna toohello mesmo data warehouse unidades e estado (em pausa ou ativa) que estava antes da migração de saudação.
5. Após a conclusão da migração hello, a Microsoft exclui "MyDW_DO_NOT_USE_ [Timestamp]".

> [!NOTE]
> Olá configurações a seguir não serão transferidos como parte da migração de saudação:
>
> * Auditoria no nível de banco de dados de saudação precisa toobe habilitada novamente.
> * Regras de firewall no nível de banco de dados de saudação necessário toobe adicionado novamente. Regras de firewall no nível do servidor de saudação não são afetadas.
>
>

### <a name="automatic-migration-schedule"></a>cronograma de migração automática
As migrações automáticas ocorrerem entre 6:00 e às 6:00 AM (hora local por região) durante a saudação agenda de interrupção a seguir.

| **Região** | **Data de início estimada** | **Data de término estimada** |
|:--- |:--- |:--- |
| Leste da Austrália |Ainda não foi determinado |Ainda não foi determinado |
| Leste da China |9 de janeiro de 2017 |13 de janeiro de 2017 |
| Norte da China |9 de janeiro de 2017 |13 de janeiro de 2017 |
| Alemanha Central |9 de janeiro de 2017 |13 de janeiro de 2017 |
| Nordeste da Alemanha |9 de janeiro de 2017 |13 de janeiro de 2017 |
| Oeste da Índia |Ainda não foi determinado |Ainda não foi determinado |
| Oeste do Japão |Ainda não foi determinado |Ainda não foi determinado |
| Centro-Norte dos EUA |9 de janeiro de 2017 |13 de janeiro de 2017 |

## <a name="self-migration-toopremium-storage"></a>Armazenamento de toopremium migração Self
Se você quiser toocontrol quando o tempo de inatividade, você pode usar o hello seguindo as etapas toomigrate um data warehouse existente no armazenamento de toopremium de armazenamento padrão. Se você escolher essa opção, você deve concluir a migração de Self Olá antes de começa a migração automática de saudação nessa região. Isso garante que você evite qualquer risco de migração automática Olá, causando um conflito (consulte toohello [agenda a migração automática][automatic migration schedule]).

### <a name="self-migration-instructions"></a>Instruções de automigração
toomigrate seus dados do data warehouse por conta própria, usam Olá backup e restauração recursos. parte de restauração de saudação de migração de saudação é esperado tootake cerca de uma hora por terabyte de armazenamento por do data warehouse. Se você quiser Olá tookeep mesmo nome após a conclusão da migração, siga Olá [toorename etapas durante a migração][steps toorename during migration].

1. [Pause][Pause] seu data warehouse. Isso leva a um backup automático.
2. [Restaure][Restore] usando o instantâneo mais recente.
3. Exclua seu data warehouse existente do armazenamento standard. **Se você não toodo esta etapa, você será cobrado para ambos os data warehouses.**

> [!NOTE]
> Olá configurações a seguir não serão transferidos como parte da migração de saudação:
>
> * Auditoria no nível de banco de dados de saudação precisa toobe habilitada novamente.
> * Regras de firewall no nível de banco de dados de saudação necessário toobe adicionado novamente. Regras de firewall no nível do servidor de saudação não são afetadas.
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a>Renomear o data warehouse durante a migração (opcional)
Dois bancos de dados no mesmo servidor lógico não pode ter de saudação Olá o mesmo nome. SQL Data Warehouse agora dá suporte a capacidade de saudação toorename um data warehouse.

Neste exemplo, imagine que o data warehouse existente no armazenamento standard é chamado atualmente de "MyDW".

1. Renomear "MyDW" usando Olá após o comando ALTER DATABASE. (Neste exemplo, iremos renomeá-lo "MyDW_BeforeMigration.")  Esse comando interrompe todas as transações existentes e deve ser feito em Olá toosucceed de banco de dados mestre.
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. [Pause][Pause] "MyDW_BeforeMigration." Isso leva a um backup automático.
3. [Restaurar] [ Restore] do seu instantâneo mais recente, um novo banco de dados com o nome da saudação era toobe (por exemplo, "MyDW").
4. Exclua "MyDW_BeforeMigration". **Se você não toodo esta etapa, você será cobrado para ambos os data warehouses.**


## <a name="next-steps"></a>Próximas etapas
Olá alterar toopremium armazenamento, você também tem um número maior de arquivos do banco de dados blob na arquitetura subjacente de saudação do data warehouse. benefícios de desempenho de saudação toomaximize dessa alteração, reconstrua os índices columnstore clusterizados usando Olá script a seguir. script Hello funciona, forçando a alguns dos seus existente blobs de dados toohello adicionais. Se você não executar nenhuma ação, dados saudação naturalmente serão redistribuir ao longo do tempo conforme você carregar mais dados em tabelas.

**Pré-requisitos:**

- Olá depósito de dados deve ser executado com unidades de depósito de 1.000 dados ou mais recente (consulte [capacidade de computação de escala][scale compute power]).
- Olá usuário executando o script hello deve estar no hello [mediumrc função] [ mediumrc role] ou superior. tooadd uma função do usuário toothis, execute o seguinte hello:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

Se você encontrar algum problema com o data warehouse, [criar um tíquete de suporte] [ create a support ticket] e fazer referência a "toopremium de armazenamento de migração" como causa possível hello.

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
