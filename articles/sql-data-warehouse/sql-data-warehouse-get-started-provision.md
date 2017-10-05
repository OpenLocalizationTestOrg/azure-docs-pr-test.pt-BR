---
title: Criar um SQL Data Warehouse no Portal do Azure | Microsoft Docs
description: Saiba como criar um Azure SQL Data Warehouse no Portal do Azure
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
ms.openlocfilehash: 24ed2d8bad3090e378acf2a42fb909dee0a8517b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="83098-103">Criar um Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="83098-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="83098-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="83098-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="83098-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="83098-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="83098-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="83098-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="83098-107">Este tutorial usa o Portal do Azure para criar um SQL Data Warehouse que contém um exemplo de banco de dados AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="83098-107">This tutorial uses the Azure portal to create a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83098-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="83098-108">Prerequisites</span></span>
<span data-ttu-id="83098-109">Para começar, você precisa do seguinte:</span><span class="sxs-lookup"><span data-stu-id="83098-109">To get started, you need:</span></span>

* <span data-ttu-id="83098-110">**Conta do Azure**: visite [Avaliação gratuita do Azure][Azure Free Trial] ou [Créditos do Azure no MSDN][MSDN Azure Credits] para criar uma conta.</span><span class="sxs-lookup"><span data-stu-id="83098-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="83098-111">**Servidor SQL do Azure**: veja [Criar um banco de dados SQL com o portal do Azure][Create an Azure SQL database in the Azure portal] para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="83098-111">**Azure SQL server**:  See [Create an Azure SQL database with the Azure portal][Create an Azure SQL database in the Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="83098-112">A criação de um SQL Data Warehouse pode resultar em um novo serviço faturável.</span><span class="sxs-lookup"><span data-stu-id="83098-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="83098-113">Confira [Preços do SQL Data Warehouse][SQL Data Warehouse pricing] para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="83098-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="83098-114">Criar um SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="83098-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="83098-115">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="83098-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="83098-116">Clique em **+ Novo** > **Bancos de dados** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="83098-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![Criação](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="83098-118">Na folha **SQL Data Warehouse** , preencha as informações necessárias e, em seguida, pressione ‘Criar’ para criar.</span><span class="sxs-lookup"><span data-stu-id="83098-118">In the **SQL Data Warehouse** blade, fill in the information needed, then press 'Create' to create.</span></span>

    ![Criar banco de dados](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="83098-120">**Servidor**: recomendamos que você selecione seu servidor primeiro.</span><span class="sxs-lookup"><span data-stu-id="83098-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="83098-121">**Nome do banco de dados**: o nome usado para referenciar o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="83098-121">**Database name**: The name that is used to reference the SQL Data Warehouse.</span></span>  <span data-ttu-id="83098-122">Esse nome tem que ser exclusivo do servidor.</span><span class="sxs-lookup"><span data-stu-id="83098-122">It must be unique to the server.</span></span>
   * <span data-ttu-id="83098-123">**Desempenho**: é recomendável começar com 400 [DWUs][DWU].</span><span class="sxs-lookup"><span data-stu-id="83098-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="83098-124">Você pode mover o controle deslizante para a esquerda ou direita para ajustar o desempenho de seu data warehouse, ou ampliar ou reduzir após a criação.</span><span class="sxs-lookup"><span data-stu-id="83098-124">You can move the slider to the left or right to adjust the performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="83098-125">Para saber mais sobre DWUs, veja nossa documentação sobre [dimensionamento](sql-data-warehouse-manage-compute-overview.md) ou nossa [página de preços][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="83098-125">To learn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="83098-126">**Assinatura**: selecione a [assinatura] na qual esse SQL Data Warehouse será cobrado.</span><span class="sxs-lookup"><span data-stu-id="83098-126">**Subscription**: Select the [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="83098-127">**Grupo de recursos**: os [grupos de recursos][Resource group] são contêineres projetados para ajudar você a gerenciar uma coleção de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="83098-127">**Resource group**: [Resource groups][Resource group] are containers designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="83098-128">Saiba mais sobre [grupos de recursos](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="83098-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="83098-129">**Selecionar origem**: clique em **Selecionar origem** > **Exemplo**.</span><span class="sxs-lookup"><span data-stu-id="83098-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="83098-130">O Azure preenche automaticamente a opção **Selecionar exemplo** com AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="83098-130">Azure automatically populates the **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="83098-131">O agrupamento padrão para um SQL Data Warehouse é SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="83098-131">The default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="83098-132">Se for necessário um agrupamento diferente, [T-SQL][T-SQL] poderá ser usado para criar o banco de dados com um agrupamento diferente.</span><span class="sxs-lookup"><span data-stu-id="83098-132">If a different collation is needed, [T-SQL][T-SQL] can be used to create the database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="83098-133">Clique em **Criar** para criar seu SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="83098-133">Click **Create** to create your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="83098-134">Aguarde alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="83098-134">Wait for a few minutes.</span></span> <span data-ttu-id="83098-135">Quando o data warehouse estiver pronto, retorne para o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="83098-135">When your data warehouse is ready, you should be returned to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="83098-136">Você pode encontrar o SQL Data Warehouse em seu painel, relacionado sob seus Bancos de Dados SQL ou no grupo de recursos que você usou para criá-lo.</span><span class="sxs-lookup"><span data-stu-id="83098-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in the resource group that you used to create it.</span></span>

    ![exibição de portal](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="83098-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="83098-138">Next steps</span></span>
<span data-ttu-id="83098-139">Agora que você criou um SQL Data Warehouse, está pronto para [Conectar](sql-data-warehouse-connect-overview.md) e começar a consultar.</span><span class="sxs-lookup"><span data-stu-id="83098-139">Now that you have created a SQL Data Warehouse, you are ready to [Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="83098-140">Para carregar dados no SQL Data Warehouse, veja a [visão geral de carregamento](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="83098-140">To load data into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="83098-141">Se você estiver tentando migrar um banco de dados existente para o SQL Data Warehouse, confira a [Visão geral de migração](sql-data-warehouse-overview-migrate.md) ou use o [Utilitário de migração](sql-data-warehouse-migrate-migration-utility.md).</span><span class="sxs-lookup"><span data-stu-id="83098-141">If you are trying to migrate an existing database to SQL Data Warehouse, see the [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="83098-142">As regras de firewall também podem ser configuradas usando o Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="83098-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="83098-143">Para saber mais, confira [sp_set_firewall_rule][sp_set_firewall_rule] e [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span><span class="sxs-lookup"><span data-stu-id="83098-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="83098-144">Também é uma ótima ideia dar uma olhada nas [práticas recomendadas][Best practices].</span><span class="sxs-lookup"><span data-stu-id="83098-144">It's also a great idea to look at the [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in the Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
<span data-ttu-id="83098-145">[assinatura]: ../azure-glossary-cloud-terminology.md#subscription</span><span class="sxs-lookup"><span data-stu-id="83098-145">[subscription]: ../azure-glossary-cloud-terminology.md#subscription</span></span>
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
