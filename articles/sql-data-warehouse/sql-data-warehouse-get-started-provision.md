---
title: "aaaCreate um SQL Data Warehouse em Olá portal do Azure | Microsoft Docs"
description: "Saiba como toocreate um Azure SQL Data Warehouse em Olá portal do Azure"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: f5be6e3f2936e3af9d099854a468f8ce66fd8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="dc1c1-103">Criar um Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="dc1c1-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dc1c1-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dc1c1-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="dc1c1-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="dc1c1-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="dc1c1-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc1c1-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="dc1c1-107">Este tutorial usa Olá toocreate portal do Azure SQL Data Warehouse que contém um banco de dados de exemplo AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-107">This tutorial uses hello Azure portal toocreate a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc1c1-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dc1c1-108">Prerequisites</span></span>
<span data-ttu-id="dc1c1-109">tooget iniciado, você precisa:</span><span class="sxs-lookup"><span data-stu-id="dc1c1-109">tooget started, you need:</span></span>

* <span data-ttu-id="dc1c1-110">**Conta do Azure**: visite [avaliação gratuita do Azure] [ Azure Free Trial] ou [créditos do Azure MSDN] [ MSDN Azure Credits] toocreate uma conta.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="dc1c1-111">**Servidor do SQL Azure**: consulte [criar um banco de dados do SQL Azure com hello portal do Azure] [ Create an Azure SQL database in hello Azure portal] para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-111">**Azure SQL server**:  See [Create an Azure SQL database with hello Azure portal][Create an Azure SQL database in hello Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="dc1c1-112">A criação de um SQL Data Warehouse pode resultar em um novo serviço faturável.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="dc1c1-113">Confira [Preços do SQL Data Warehouse][SQL Data Warehouse pricing] para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="dc1c1-114">Criar um SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="dc1c1-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="dc1c1-115">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc1c1-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dc1c1-116">Clique em **+ Novo** > **Bancos de dados** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![Criar](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="dc1c1-118">Em Olá **SQL Data Warehouse** folha, preencha as informações de saudação necessárias, em seguida, pressione toocreate 'Criar'.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-118">In hello **SQL Data Warehouse** blade, fill in hello information needed, then press 'Create' toocreate.</span></span>

    ![Criar banco de dados](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="dc1c1-120">**Servidor**: recomendamos que você selecione seu servidor primeiro.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="dc1c1-121">**Nome do banco de dados**: nome de Olá Olá usado tooreference SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-121">**Database name**: hello name that is used tooreference hello SQL Data Warehouse.</span></span>  <span data-ttu-id="dc1c1-122">Ele deve ser exclusivo toohello server.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-122">It must be unique toohello server.</span></span>
   * <span data-ttu-id="dc1c1-123">**Desempenho**: é recomendável começar com 400 [DWUs][DWU].</span><span class="sxs-lookup"><span data-stu-id="dc1c1-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="dc1c1-124">Você pode mover Olá toohello de controle deslizante à esquerda ou direita tooadjust desempenho de saudação do seu data warehouse ou escala para cima ou para baixo após a criação.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-124">You can move hello slider toohello left or right tooadjust hello performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="dc1c1-125">toolearn mais sobre DWUs, consulte nossa documentação sobre [dimensionamento](sql-data-warehouse-manage-compute-overview.md) ou nosso [página de preços][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="dc1c1-125">toolearn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="dc1c1-126">**Assinatura**: selecione Olá [assinatura] que fará a cobrança para este depósito de dados do SQL.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-126">**Subscription**: Select hello [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="dc1c1-127">**Grupo de recursos**: [grupos de recursos] [ Resource group] são contêineres projetados toohelp você gerenciar uma coleção de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-127">**Resource group**: [Resource groups][Resource group] are containers designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="dc1c1-128">Saiba mais sobre [grupos de recursos](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dc1c1-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="dc1c1-129">**Selecionar origem**: clique em **Selecionar origem** > **Exemplo**.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="dc1c1-130">Azure preenche automaticamente Olá **exemplo Select** opção com AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-130">Azure automatically populates hello **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dc1c1-131">agrupamento de padrão de saudação para um SQL Data Warehouse é SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-131">hello default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="dc1c1-132">Se for necessário um agrupamento diferente, [T-SQL] [ T-SQL] pode ser usado toocreate banco de dados de saudação com um agrupamento diferente.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-132">If a different collation is needed, [T-SQL][T-SQL] can be used toocreate hello database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="dc1c1-133">Clique em **criar** toocreate seu SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-133">Click **Create** toocreate your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="dc1c1-134">Aguarde alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-134">Wait for a few minutes.</span></span> <span data-ttu-id="dc1c1-135">Quando o data warehouse estiver pronto, você deve ser retornado toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc1c1-135">When your data warehouse is ready, you should be returned toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="dc1c1-136">Você pode localizar seu SQL Data Warehouse no seu painel, listado em bancos de dados SQL, ou em recurso Olá grupo que você usou toocreate-lo.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in hello resource group that you used toocreate it.</span></span>

    ![exibição de portal](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="dc1c1-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dc1c1-138">Next steps</span></span>
<span data-ttu-id="dc1c1-139">Agora que você criou um SQL Data Warehouse, você está pronto muito[conectar](sql-data-warehouse-connect-overview.md) e começar a consultar.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-139">Now that you have created a SQL Data Warehouse, you are ready too[Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="dc1c1-140">dados de tooload no SQL Data Warehouse, consulte Olá [visão geral de carregamento](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="dc1c1-140">tooload data into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="dc1c1-141">Se você estiver tentando toomigrate um tooSQL de banco de dados do Data Warehouse existente, consulte Olá [visão geral da migração](sql-data-warehouse-overview-migrate.md) ou use [utilitário de migração](sql-data-warehouse-migrate-migration-utility.md).</span><span class="sxs-lookup"><span data-stu-id="dc1c1-141">If you are trying toomigrate an existing database tooSQL Data Warehouse, see hello [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="dc1c1-142">As regras de firewall também podem ser configuradas usando o Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="dc1c1-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="dc1c1-143">Para saber mais, confira [sp_set_firewall_rule][sp_set_firewall_rule] e [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span><span class="sxs-lookup"><span data-stu-id="dc1c1-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="dc1c1-144">Também é toolook uma grande ideia no hello [práticas recomendadas][Best practices].</span><span class="sxs-lookup"><span data-stu-id="dc1c1-144">It's also a great idea toolook at hello [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in hello Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[assinatura]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
