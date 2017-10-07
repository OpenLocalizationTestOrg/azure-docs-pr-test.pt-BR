---
title: aaaTransparent a criptografia de dados no Data Warehouse do SQL (T-SQL) | Microsoft Docs
description: TDE (Transparent Data Encryption) no SQL Data Warehouse (T-SQL)
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: barbkess
editor: 
ms.assetid: 8ccefef3-1308-41ee-b336-5e491d1098ae
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 3894431c76f14b217f3a6b9a42dbf2f4d216bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a>Introdução ao Transparent Data Encryption (TDE)
> [!div class="op_single_selector"]
> * [Visão Geral da Segurança](sql-data-warehouse-overview-manage-security.md)
> * [Autenticação](sql-data-warehouse-authentication.md)
> * [Criptografia (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Criptografia (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>Permissões necessárias
tooenable criptografia de dados transparente (TDE), você deve ser um administrador ou um membro da função dbmanager de saudação.

## <a name="enabling-encryption"></a>Habilitando a criptografia
Siga essas etapas tooenable TDE para um SQL Data Warehouse:

1. Conecte-se toohello *mestre* banco de dados no servidor de saudação hospeda Olá banco de dados usando um logon que seja um administrador ou um membro da saudação **dbmanager** função no banco de dados mestre Olá
2. Execute Olá banco de dados de saudação de tooencrypt instrução a seguir.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Desabilitando a criptografia
Siga essas etapas toodisable TDE para um SQL Data Warehouse:

1. Conecte-se toohello *mestre* banco de dados usando um logon que seja um administrador ou um membro da saudação **dbmanager** função no banco de dados mestre Olá
2. Execute Olá banco de dados de saudação de tooencrypt instrução a seguir.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> Um SQL Data Warehouse em pausa deve ser reiniciado antes de fazer alterações em configurações de TDE toohello.
> 
> 

## <a name="verifying-encryption"></a>Verificando a criptografia
status da criptografia tooverify para um SQL Data Warehouse, siga as etapas de saudação abaixo:

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

## <a name="encryption-dmvs"></a>DMVs de criptografia
* [sys.databases][sys.databases] 
* [sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
