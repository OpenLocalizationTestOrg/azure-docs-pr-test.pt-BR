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
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="a6cec-103">Habilitar TDE (Transparent Data Encryption) para Stretch Database no Azure (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="a6cec-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a6cec-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a6cec-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="a6cec-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="a6cec-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="a6cec-106">Criptografia de dados transparente (TDE) ajuda a proteger contra a ameaça de saudação de atividades mal-intencionadas executando criptografia em tempo real e a descriptografia de banco de dados hello, backups associados e arquivos de log de transações em repouso sem exigir alterações toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a6cec-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="a6cec-107">Ela criptografa o armazenamento de saudação de um banco de dados inteiro usando uma chave de criptografia de banco de dados de saudação de chamada de chave simétrica.</span><span class="sxs-lookup"><span data-stu-id="a6cec-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="a6cec-108">chave de criptografia de banco de dados de saudação é protegida por um certificado de servidor interno.</span><span class="sxs-lookup"><span data-stu-id="a6cec-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="a6cec-109">certificado de saudação do servidor interno é exclusivo para cada servidor do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6cec-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="a6cec-110">A Microsoft alterna automaticamente esses certificados pelo menos a cada 90 dias.</span><span class="sxs-lookup"><span data-stu-id="a6cec-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="a6cec-111">Para obter uma descrição geral da TDE, consulte [Transparent Data Encryption (TDE)].</span><span class="sxs-lookup"><span data-stu-id="a6cec-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="a6cec-112">Habilitando a criptografia</span><span class="sxs-lookup"><span data-stu-id="a6cec-112">Enabling Encryption</span></span>
<span data-ttu-id="a6cec-113">tooenable TDE para um banco de dados do Azure que está armazenando Olá migrar dados de um banco de dados do SQL Server habilitado para Stretch, Olá coisas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6cec-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="a6cec-114">Conecte-se toohello *mestre* banco de dados em hello Azure server hospedagem Olá banco de dados usando um logon que seja um administrador ou um membro da saudação **dbmanager** função no banco de dados mestre Olá</span><span class="sxs-lookup"><span data-stu-id="a6cec-114">Connect toohello *master* database on hello Azure server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="a6cec-115">Execute Olá banco de dados de saudação de tooencrypt instrução a seguir.</span><span class="sxs-lookup"><span data-stu-id="a6cec-115">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="a6cec-116">Desabilitando a criptografia</span><span class="sxs-lookup"><span data-stu-id="a6cec-116">Disabling Encryption</span></span>
<span data-ttu-id="a6cec-117">toodisable TDE para um banco de dados do Azure que está armazenando Olá migrar dados de um banco de dados do SQL Server habilitado para Stretch, Olá coisas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6cec-117">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="a6cec-118">Conecte-se toohello *mestre* banco de dados usando um logon que seja um administrador ou um membro da saudação **dbmanager** função no banco de dados mestre Olá</span><span class="sxs-lookup"><span data-stu-id="a6cec-118">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="a6cec-119">Execute Olá banco de dados de saudação de tooencrypt instrução a seguir.</span><span class="sxs-lookup"><span data-stu-id="a6cec-119">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="a6cec-120">Verificando a criptografia</span><span class="sxs-lookup"><span data-stu-id="a6cec-120">Verifying Encryption</span></span>
<span data-ttu-id="a6cec-121">status da criptografia tooverify para um banco de dados do Azure que está armazenando Olá migrar dados de um banco de dados do SQL Server habilitado para Stretch, Olá coisas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6cec-121">tooverify encryption status for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="a6cec-122">Conecte-se toohello *mestre* ou instância de banco de dados usando um logon que seja um administrador ou um membro da saudação **dbmanager** função no banco de dados mestre Olá</span><span class="sxs-lookup"><span data-stu-id="a6cec-122">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="a6cec-123">Execute Olá banco de dados de saudação de tooencrypt instrução a seguir.</span><span class="sxs-lookup"><span data-stu-id="a6cec-123">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="a6cec-124">Um resultado de ```1``` indica um banco de dados criptografado, ```0``` indica um banco de dados não criptografado.</span><span class="sxs-lookup"><span data-stu-id="a6cec-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
