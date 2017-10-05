---
title: Transparent Data Encryption no SQL Data Warehouse (Portal) | Microsoft Docs
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
ms.openlocfilehash: b1db3bdfdfb54bda325c9b971cfcb4dd5efa333a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="3e6b9-103">Introdução aos dados TDE (Transparent Data Encryption) no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3e6b9-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e6b9-104">Visão Geral da Segurança</span><span class="sxs-lookup"><span data-stu-id="3e6b9-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="3e6b9-105">Autenticação</span><span class="sxs-lookup"><span data-stu-id="3e6b9-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="3e6b9-106">Criptografia (Portal)</span><span class="sxs-lookup"><span data-stu-id="3e6b9-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="3e6b9-107">Criptografia (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="3e6b9-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="3e6b9-108">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="3e6b9-108">Required Permssions</span></span>
<span data-ttu-id="3e6b9-109">Para habilitar a TDE (Transparent Data Encryption), você deve ser um administrador ou um membro da função dbmanager.</span><span class="sxs-lookup"><span data-stu-id="3e6b9-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="3e6b9-110">Habilitando a criptografia</span><span class="sxs-lookup"><span data-stu-id="3e6b9-110">Enabling Encryption</span></span>
<span data-ttu-id="3e6b9-111">Para habilitar a TDE para um SQL Data Warehouse, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="3e6b9-111">To enable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="3e6b9-112">Abra o banco de dados no [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="3e6b9-112">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="3e6b9-113">Na folha do banco de dados, clique no botão **Configurações**</span><span class="sxs-lookup"><span data-stu-id="3e6b9-113">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="3e6b9-114">Selecione a opção **Transparent Data Encryption**![][1]</span><span class="sxs-lookup"><span data-stu-id="3e6b9-114">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="3e6b9-115">Selecione a configuração **Ativado** ![][2]</span><span class="sxs-lookup"><span data-stu-id="3e6b9-115">Select the **On** setting ![][2]</span></span>
5. <span data-ttu-id="3e6b9-116">Selecione **Salvar**
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="3e6b9-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="3e6b9-117">Desabilitando a criptografia</span><span class="sxs-lookup"><span data-stu-id="3e6b9-117">Disabling Encryption</span></span>
<span data-ttu-id="3e6b9-118">Para desabilitar a TDE para um SQL Data Warehouse, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="3e6b9-118">To disable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="3e6b9-119">Abra o banco de dados no [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="3e6b9-119">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="3e6b9-120">Na folha do banco de dados, clique no botão **Configurações**</span><span class="sxs-lookup"><span data-stu-id="3e6b9-120">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="3e6b9-121">Selecione a opção **Transparent Data Encryption**![][1]</span><span class="sxs-lookup"><span data-stu-id="3e6b9-121">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="3e6b9-122">Selecione a configuração **Desativado** ![][4]</span><span class="sxs-lookup"><span data-stu-id="3e6b9-122">Select the **Off** setting ![][4]</span></span>
5. <span data-ttu-id="3e6b9-123">Selecione **Salvar**
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="3e6b9-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="3e6b9-124">DMVs de criptografia</span><span class="sxs-lookup"><span data-stu-id="3e6b9-124">Encryption DMVs</span></span>
<span data-ttu-id="3e6b9-125">A criptografia pode ser confirmada com as DMVs a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e6b9-125">Encryption can be confirmed with the following DMVs:</span></span>

* <span data-ttu-id="3e6b9-126">[sys.databases]</span><span class="sxs-lookup"><span data-stu-id="3e6b9-126">[sys.databases]</span></span>
* <span data-ttu-id="3e6b9-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="3e6b9-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
<span data-ttu-id="3e6b9-128">[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx</span><span class="sxs-lookup"><span data-stu-id="3e6b9-128">[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx</span></span>
<span data-ttu-id="3e6b9-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span><span class="sxs-lookup"><span data-stu-id="3e6b9-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
