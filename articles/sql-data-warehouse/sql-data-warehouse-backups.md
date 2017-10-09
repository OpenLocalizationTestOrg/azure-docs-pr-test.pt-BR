---
title: "backups do SQL Data Warehouse aaaAzure - instantâneos, com redundância geográfica | Microsoft Docs"
description: "Saiba mais sobre backups de banco de dados interno do SQL Data Warehouse que permitem que você toorestore um ponto de restauração do Azure SQL Data Warehouse tooa ou uma região geográfica diferente."
services: sql-data-warehouse
documentationcenter: 
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: b5aff094-05b2-4578-acf3-ec456656febd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 34659480485246f54a1490e185fc1b903fb2520d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-backups"></a>Backups do SQL Data Warehouse
O SQL Data Warehouse oferece backups locais e geográficos como parte de suas funcionalidades de backup do data warehouse. Essas funcionalidades incluem instantâneos de Blob de Armazenamento do Azure e armazenamento com redundância geográfica. Use o data warehouse backups toorestore sua restauração do data warehouse tooa ponto na região primária hello, ou restaurar tooa uma região geográfica diferente. Este artigo explica as especificações de saudação de backups no SQL Data Warehouse.

## <a name="what-is-a-data-warehouse-backup"></a>O que é um backup do data warehouse?
Um backup de dados do warehouse é que você pode usar toorestore uma hora específica do data warehouse tooa de dados de saudação.  Considerando que o SQL Data Warehouse é um sistema distribuído, um backup do data warehouse consiste em vários arquivos que são armazenados em blobs do Azure. 

Os backups de banco de dados são uma parte essencial de qualquer estratégia de recuperação de desastre e continuidade dos negócios, porque eles protegem seus dados contra exclusão ou corrupção acidentais. Para obter mais informações, veja [Visão geral sobre a continuidade dos negócios](../sql-database/sql-database-business-continuity.md).

## <a name="data-redundancy"></a>Redundância de dados
O SQL Data Warehouse também protege seus dados armazenando-os em Armazenamento Premium LRS (localmente redundante) do Azure. Esse recurso de armazenamento do Azure armazena várias cópias síncronas de dados saudação em Olá local tooguarantee transparente de dados proteção de dados se houver falhas localizadas. A redundância de dados faz com que os dados possam sobreviver a problemas de infraestrutura como falhas de disco. A redundância de dados garante a continuidade de negócios com uma infraestrutura altamente disponível e tolerante a falhas.

toolearn mais sobre:

* Armazenamento Premium do Azure, consulte [tooAzure Introdução armazenamento Premium](../storage/common/storage-premium-storage.md).
* Armazenamento com redundância local, veja [Replicação do Armazenamento do Azure](../storage/common/storage-redundancy.md#locally-redundant-storage).

## <a name="azure-storage-blob-snapshots"></a>Instantâneos do Azure Storage Blob
Como um benefício de usar o armazenamento Premium do Azure, SQL Data Warehouse usa data warehouse de Blob de armazenamento do Azure instantâneos toobackup Olá localmente. Você pode restaurar um ponto de restauração de instantâneo do data warehouse tooa. Instantâneos iniciam no mínimo a cada oito horas e permanecem disponíveis por sete dias.  

toolearn mais sobre:

* Instantâneos de blob do Azure, consulte [Criar um instantâneo de blob](../storage/blobs/storage-blob-snapshots.md).

## <a name="geo-redundant-backups"></a>Backups com redundância geográfica
A cada 24 horas, o SQL Data Warehouse armazena Olá total do data warehouse no armazenamento padrão. Olá data warehouse completo é criado toomatch Olá hora do último instantâneo de saudação. armazenamento padrão Olá pertence tooa conta de armazenamento com redundância geográfica com acesso de leitura (RA-GRS). recurso de armazenamento do Azure RA-GRS Olá replica Olá arquivos de backup tooa [Datacenter emparelhado](../best-practices-availability-paired-regions.md). Essa replicação geográfica garante que você possa restaurar do data warehouse, caso você não pode acessar os instantâneos de saudação em sua região primária. 

Esse recurso está ligado por padrão. Se não quiser que os backups com redundância geográfica toouse, você pode [recusar] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn). 

> [!NOTE]
> No armazenamento do Azure, o termo de saudação *replicação* refere-se a arquivos de toocopying de tooanother de um local. Do SQL *replicação de banco de dados* refere-se tookeeping toomultiple bancos de dados secundários sincronizados com o banco de dados primário. 
> 
> 

> [!NOTE]
> Não é possível recusar backups com redundância geográfica no DWU 9000 e DWU 18000. 
>
> 

toolearn mais sobre:

* Armazenamento com redundância geográfica, veja [Replicação do Armazenamento do Azure](../storage/common/storage-redundancy.md).
* Armazenamento RA-GRS, veja [Armazenamento com redundância geográfica com acesso de leitura](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage).

## <a name="data-warehouse-backup-schedule-and-retention-period"></a>Período de retenção e agendamento de backup de data warehouse
SQL Data Warehouse cria instantâneos no depósito de dados online a cada quatro horas tooeight e mantém cada instantâneo por sete dias. Você pode restaurar seu tooone de banco de dados online Olá de pontos de restauração em Olá últimos sete dias. 

toosee ao último instantâneo de saudação iniciado, execute esta consulta em seu SQL Data Warehouse on-line. 

```sql
select top 1 *
from sys.pdw_loader_backup_runs 
order by run_id desc;
```

Se você precisar de um instantâneo de tooretain por mais de sete dias, você pode restaurar um restauração ponto tooa novo data warehouse. Após a restauração hello, SQL Data Warehouse inicia a criação de instantâneos Olá novo do data warehouse. Se você não fizer alterações toohello novo data warehouse, instantâneos de saudação permanecem vazios e, portanto, o custo de instantâneo de Olá é mínimo. Você também pode pausar Olá tookeep de banco de dados SQL Data Warehouse de criação de instantâneos.

### <a name="what-happens-toomy-backup-retention-while-my-data-warehouse-is-paused"></a>O que acontece toomy retenção de backup enquanto o depósito de dados está em pausa?
O SQL Data Warehouse não cria nem expira instantâneos enquanto um data warehouse está em pausa. idade de instantâneo Olá não altera enquanto o data warehouse de saudação está em pausa. Retenção de instantâneo é baseada no número de saudação de dias Olá data warehouse é online, não dias do calendário.

Por exemplo, se um instantâneo começa em 1 de outubro às 16: 00 e data warehouse de saudação está pausado 3 de outubro às 16: 00, o instantâneo de saudação é dois dias. Sempre que o data warehouse de saudação volta a ficar online instantâneo Olá é dois dias. Se data warehouse de saudação online 5 de outubro às 16: 00, o instantâneo de saudação é dois dias e permanece por mais cinco dias.

Quando o data warehouse de saudação volta a ficar online, o SQL Data Warehouse retoma novos instantâneos e expira instantâneos quando eles têm mais de sete dias de dados.

### <a name="how-long-is-hello-retention-period-for-a-dropped-data-warehouse"></a>Quanto tempo é o período de retenção de saudação de um depósito de dados soltos?
Quando um data warehouse é descartado, Olá data warehouse e instantâneos de saudação são salvos por sete dias e, em seguida, removidos. Você pode restaurar tooany de depósito de dados Olá Olá salvada de pontos de restauração.

> [!IMPORTANT]
> Se você excluir uma instância lógica do SQL server, todos os bancos de dados que pertencem a instância de toohello também são excluídos e não podem ser recuperados. Você não pode restaurar um servidor excluído.
> 
> 

## <a name="data-warehouse-backup-costs"></a>Custos de backup do data warehouse
Olá total de custos para o depósito de dados primário e sete dias de instantâneos de Blob do Azure é arredondado toohello mais próximo TB. Por exemplo, se o data warehouse é 1,5 TB e instantâneos Olá usam 100 GB, você será cobrado de 2 TB de dados em taxas de armazenamento Premium do Azure. 

> [!NOTE]
> Cada instantâneo é inicialmente vazio e aumenta à medida que você fizer alterações toohello principal do data warehouse. Todos os instantâneos aumentam em tamanho, como alterações de depósito de dados hello. Portanto, os custos de armazenamento Olá para instantâneos crescem acordo taxa toohello de alteração.
> 
> 

Se você estiver usando armazenamento com redundância geográfica, você receberá uma cobrança de armazenamento separada. armazenamento com redundância geográfica Olá será cobrado na taxa padrão de acesso de leitura geograficamente redundantes (RA-GRS) hello.

Para obter mais informações sobre os preços do SQL Data Warehouse, consulte [Preços do SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="using-database-backups"></a>Usando backups de banco de dados
Olá principal uso para os backups do SQL data warehouse é tooone de depósito de dados toorestore Olá Olá de pontos de restauração dentro do período de retenção de saudação.  

* toorestore um SQL data warehouse, consulte [restaurar um SQL data warehouse](sql-data-warehouse-restore-database-overview.md).

## <a name="related-topics"></a>Tópicos relacionados
### <a name="scenarios"></a>Cenários
* Para obter uma visão geral sobre a continuidade de negócios, veja [Visão geral da continuidade de negócios](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

* toorestore um data warehouse, consulte [restaurar um SQL data warehouse](sql-data-warehouse-restore-database-overview.md)

<!-- ### Tutorials -->

