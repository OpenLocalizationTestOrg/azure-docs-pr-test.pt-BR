---
title: Transparent Data Encryption no SQL Data Warehouse (T-SQL) | Microsoft Docs
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
ms.openlocfilehash: 74c9032aababdce91ed617cd7a4c628915b42504
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="e1cda-103">Introdução ao Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="e1cda-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e1cda-104">Visão Geral da Segurança</span><span class="sxs-lookup"><span data-stu-id="e1cda-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="e1cda-105">Autenticação</span><span class="sxs-lookup"><span data-stu-id="e1cda-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="e1cda-106">Criptografia (Portal)</span><span class="sxs-lookup"><span data-stu-id="e1cda-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="e1cda-107">Criptografia (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="e1cda-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="e1cda-108">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="e1cda-108">Required Permssions</span></span>
<span data-ttu-id="e1cda-109">Para habilitar a TDE (Transparent Data Encryption), você deve ser um administrador ou um membro da função dbmanager.</span><span class="sxs-lookup"><span data-stu-id="e1cda-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="e1cda-110">Habilitando a criptografia</span><span class="sxs-lookup"><span data-stu-id="e1cda-110">Enabling Encryption</span></span>
<span data-ttu-id="e1cda-111">Siga estas etapas para habilitar a TDE para um SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="e1cda-111">Follow these steps to enable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="e1cda-112">Conecte ao banco de dados *mestre* no servidor que está hospedando o banco de dados que usa um logon de administrador ou de um membro da função **dbmanager** no banco de dados mestre</span><span class="sxs-lookup"><span data-stu-id="e1cda-112">Connect to the *master* database on the server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="e1cda-113">Execute a instrução a seguir para criptografar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e1cda-113">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="e1cda-114">Desabilitando a criptografia</span><span class="sxs-lookup"><span data-stu-id="e1cda-114">Disabling Encryption</span></span>
<span data-ttu-id="e1cda-115">Siga estas etapas para desabilitar a TDE para um SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="e1cda-115">Follow these steps to disable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="e1cda-116">Conecte-se ao banco de dados *mestre* que usa um logon de administrador ou de um membro da função **dbmanager** no banco de dados mestre</span><span class="sxs-lookup"><span data-stu-id="e1cda-116">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="e1cda-117">Execute a instrução a seguir para criptografar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e1cda-117">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="e1cda-118">Um SQL Data Warehouse em pausa deve ser retomado antes das mudanças nas configurações da TDE.</span><span class="sxs-lookup"><span data-stu-id="e1cda-118">A paused SQL Data Warehouse must be resumed before making changes to the TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="e1cda-119">Verificando a criptografia</span><span class="sxs-lookup"><span data-stu-id="e1cda-119">Verifying Encryption</span></span>
<span data-ttu-id="e1cda-120">Para verificar o status de criptografia para um SQL Data Warehouse, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="e1cda-120">To verify encryption status for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="e1cda-121">Conecte-se ao banco de dados *mestre* ou de instância que usa um logon de administrador ou de um membro da função **dbmanager** no banco de dados mestre</span><span class="sxs-lookup"><span data-stu-id="e1cda-121">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="e1cda-122">Execute a instrução a seguir para criptografar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e1cda-122">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="e1cda-123">Um resultado de ```1``` indica um banco de dados criptografado, ```0``` indica um banco de dados não criptografado.</span><span class="sxs-lookup"><span data-stu-id="e1cda-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="e1cda-124">DMVs de criptografia</span><span class="sxs-lookup"><span data-stu-id="e1cda-124">Encryption DMVs</span></span>
* <span data-ttu-id="e1cda-125">[sys.databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="e1cda-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="e1cda-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="e1cda-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
