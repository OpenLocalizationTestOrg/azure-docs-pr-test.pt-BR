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
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="a1b27-103">Introdução ao Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="a1b27-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a1b27-104">Visão Geral da Segurança</span><span class="sxs-lookup"><span data-stu-id="a1b27-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="a1b27-105">Autenticação</span><span class="sxs-lookup"><span data-stu-id="a1b27-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="a1b27-106">Criptografia (Portal)</span><span class="sxs-lookup"><span data-stu-id="a1b27-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="a1b27-107">Criptografia (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="a1b27-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="a1b27-108">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="a1b27-108">Required Permssions</span></span>
<span data-ttu-id="a1b27-109">tooenable criptografia de dados transparente (TDE), você deve ser um administrador ou um membro da função dbmanager de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1b27-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="a1b27-110">Habilitando a criptografia</span><span class="sxs-lookup"><span data-stu-id="a1b27-110">Enabling Encryption</span></span>
<span data-ttu-id="a1b27-111">Siga essas etapas tooenable TDE para um SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="a1b27-111">Follow these steps tooenable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="a1b27-112">Conecte-se toohello *mestre* banco de dados no servidor de saudação hospeda Olá banco de dados usando um logon que seja um administrador ou um membro da saudação **dbmanager** função no banco de dados mestre Olá</span><span class="sxs-lookup"><span data-stu-id="a1b27-112">Connect toohello *master* database on hello server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="a1b27-113">Execute Olá banco de dados de saudação de tooencrypt instrução a seguir.</span><span class="sxs-lookup"><span data-stu-id="a1b27-113">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="a1b27-114">Desabilitando a criptografia</span><span class="sxs-lookup"><span data-stu-id="a1b27-114">Disabling Encryption</span></span>
<span data-ttu-id="a1b27-115">Siga essas etapas toodisable TDE para um SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="a1b27-115">Follow these steps toodisable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="a1b27-116">Conecte-se toohello *mestre* banco de dados usando um logon que seja um administrador ou um membro da saudação **dbmanager** função no banco de dados mestre Olá</span><span class="sxs-lookup"><span data-stu-id="a1b27-116">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="a1b27-117">Execute Olá banco de dados de saudação de tooencrypt instrução a seguir.</span><span class="sxs-lookup"><span data-stu-id="a1b27-117">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="a1b27-118">Um SQL Data Warehouse em pausa deve ser reiniciado antes de fazer alterações em configurações de TDE toohello.</span><span class="sxs-lookup"><span data-stu-id="a1b27-118">A paused SQL Data Warehouse must be resumed before making changes toohello TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="a1b27-119">Verificando a criptografia</span><span class="sxs-lookup"><span data-stu-id="a1b27-119">Verifying Encryption</span></span>
<span data-ttu-id="a1b27-120">status da criptografia tooverify para um SQL Data Warehouse, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="a1b27-120">tooverify encryption status for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="a1b27-121">Conecte-se toohello *mestre* ou instância de banco de dados usando um logon que seja um administrador ou um membro da saudação **dbmanager** função no banco de dados mestre Olá</span><span class="sxs-lookup"><span data-stu-id="a1b27-121">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="a1b27-122">Execute Olá banco de dados de saudação de tooencrypt instrução a seguir.</span><span class="sxs-lookup"><span data-stu-id="a1b27-122">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="a1b27-123">Um resultado de ```1``` indica um banco de dados criptografado, ```0``` indica um banco de dados não criptografado.</span><span class="sxs-lookup"><span data-stu-id="a1b27-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="a1b27-124">DMVs de criptografia</span><span class="sxs-lookup"><span data-stu-id="a1b27-124">Encryption DMVs</span></span>
* <span data-ttu-id="a1b27-125">[sys.databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="a1b27-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="a1b27-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="a1b27-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
