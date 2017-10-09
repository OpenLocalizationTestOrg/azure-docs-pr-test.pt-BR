---
title: aaaEnable criptografia transparente de dados para Stretch Database TSQL - Azure | Microsoft Docs
description: Habilitar TDE (Transparent Data Encryption) para SQL Server Stretch Database no Azure TSQL
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: jhubbard
editor: 
ms.assetid: 27753d91-9ca2-4d47-b34d-b5e2c2f029bb
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: anvang
ms.openlocfilehash: a9ba23649656fb344480d79438a1115f0eb353bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a>Habilitar TDE (Transparent Data Encryption) para Stretch Database no Azure (Transact-SQL)
> [!div class="op_single_selector"]
> * [Portal do Azure](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Criptografia de dados transparente (TDE) ajuda a proteger contra a ameaça de saudação de atividades mal-intencionadas executando criptografia em tempo real e a descriptografia de banco de dados hello, backups associados e arquivos de log de transações em repouso sem exigir alterações toohello aplicativo.

Ela criptografa o armazenamento de saudação de um banco de dados inteiro usando uma chave de criptografia de banco de dados de saudação de chamada de chave simétrica. chave de criptografia de banco de dados de saudação é protegida por um certificado de servidor interno. certificado de saudação do servidor interno é exclusivo para cada servidor do Azure. A Microsoft alterna automaticamente esses certificados pelo menos a cada 90 dias. Para obter uma descrição geral da TDE, consulte [Transparent Data Encryption (TDE)].

## <a name="enabling-encryption"></a>Habilitando a criptografia
tooenable TDE para um banco de dados do Azure que está armazenando Olá migrar dados de um banco de dados do SQL Server habilitado para Stretch, Olá coisas a seguir:

1. Conecte-se toohello *mestre* banco de dados em hello Azure server hospedagem Olá banco de dados usando um logon que seja um administrador ou um membro da saudação **dbmanager** função no banco de dados mestre Olá
2. Execute Olá banco de dados de saudação de tooencrypt instrução a seguir.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Desabilitando a criptografia
toodisable TDE para um banco de dados do Azure que está armazenando Olá migrar dados de um banco de dados do SQL Server habilitado para Stretch, Olá coisas a seguir:

1. Conecte-se toohello *mestre* banco de dados usando um logon que seja um administrador ou um membro da saudação **dbmanager** função no banco de dados mestre Olá
2. Execute Olá banco de dados de saudação de tooencrypt instrução a seguir.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a>Verificando a criptografia
status da criptografia tooverify para um banco de dados do Azure que está armazenando Olá migrar dados de um banco de dados do SQL Server habilitado para Stretch, Olá coisas a seguir:

1. Conecte-se toohello *mestre* ou instância de banco de dados usando um logon que seja um administrador ou um membro da saudação **dbmanager** função no banco de dados mestre Olá
2. Execute Olá banco de dados de saudação de tooencrypt instrução a seguir.

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

Um resultado de ```1``` indica um banco de dados criptografado, ```0``` indica um banco de dados não criptografado.

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
