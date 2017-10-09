---
title: aaaTransparent a criptografia de dados no Data Warehouse do SQL (Portal) | Microsoft Docs
description: TDE (Transparent Data Encryption) no SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="02fc4-103">Introdução aos dados TDE (Transparent Data Encryption) no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="02fc4-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="02fc4-104">Visão Geral da Segurança</span><span class="sxs-lookup"><span data-stu-id="02fc4-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="02fc4-105">Autenticação</span><span class="sxs-lookup"><span data-stu-id="02fc4-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="02fc4-106">Criptografia (Portal)</span><span class="sxs-lookup"><span data-stu-id="02fc4-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="02fc4-107">Criptografia (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="02fc4-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="02fc4-108">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="02fc4-108">Required Permssions</span></span>
<span data-ttu-id="02fc4-109">tooenable criptografia de dados transparente (TDE), você deve ser um administrador ou um membro da função dbmanager de saudação.</span><span class="sxs-lookup"><span data-stu-id="02fc4-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="02fc4-110">Habilitando a criptografia</span><span class="sxs-lookup"><span data-stu-id="02fc4-110">Enabling Encryption</span></span>
<span data-ttu-id="02fc4-111">tooenable TDE para um SQL Data Warehouse, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="02fc4-111">tooenable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="02fc4-112">Banco de dados aberto Olá no hello [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="02fc4-112">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="02fc4-113">Na folha de banco de dados de saudação, clique em Olá **configurações** botão</span><span class="sxs-lookup"><span data-stu-id="02fc4-113">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="02fc4-114">Selecione Olá **criptografia transparente de dados** opção![][1]</span><span class="sxs-lookup"><span data-stu-id="02fc4-114">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="02fc4-115">Selecione Olá **em** configuração![][2]</span><span class="sxs-lookup"><span data-stu-id="02fc4-115">Select hello **On** setting ![][2]</span></span>
5. <span data-ttu-id="02fc4-116">Selecione **Salvar**
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="02fc4-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="02fc4-117">Desabilitando a criptografia</span><span class="sxs-lookup"><span data-stu-id="02fc4-117">Disabling Encryption</span></span>
<span data-ttu-id="02fc4-118">toodisable TDE para um SQL Data Warehouse, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="02fc4-118">toodisable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="02fc4-119">Banco de dados aberto Olá no hello [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="02fc4-119">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="02fc4-120">Na folha de banco de dados de saudação, clique em Olá **configurações** botão</span><span class="sxs-lookup"><span data-stu-id="02fc4-120">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="02fc4-121">Selecione Olá **criptografia transparente de dados** opção![][1]</span><span class="sxs-lookup"><span data-stu-id="02fc4-121">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="02fc4-122">Selecione Olá **Off** configuração![][4]</span><span class="sxs-lookup"><span data-stu-id="02fc4-122">Select hello **Off** setting ![][4]</span></span>
5. <span data-ttu-id="02fc4-123">Selecione **Salvar**
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="02fc4-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="02fc4-124">DMVs de criptografia</span><span class="sxs-lookup"><span data-stu-id="02fc4-124">Encryption DMVs</span></span>
<span data-ttu-id="02fc4-125">A criptografia pode ser confirmada com hello DMVs a seguir:</span><span class="sxs-lookup"><span data-stu-id="02fc4-125">Encryption can be confirmed with hello following DMVs:</span></span>

* <span data-ttu-id="02fc4-126">[sys.databases]</span><span class="sxs-lookup"><span data-stu-id="02fc4-126">[sys.databases]</span></span>
* <span data-ttu-id="02fc4-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="02fc4-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
