---
title: "Portal do Azure: replicação geográfica do Banco de Dados SQL | Microsoft Docs"
description: "Configurar a replicação geográfica para o Banco de Dados SQL do Azure usando o Portal do Azure e inicializar o failover"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: db90fad2fe397f0c8466db6bdc1bd8c8d1cf8f15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-the-azure-portal-and-initiate-failover"></a><span data-ttu-id="683a0-103">Configurar a replicação geográfica ativa para o Banco de Dados SQL do Azure usando o Portal do Azure e inicializar o failover</span><span class="sxs-lookup"><span data-stu-id="683a0-103">Configure active geo-replication for Azure SQL Database in the Azure portal and initiate failover</span></span>

<span data-ttu-id="683a0-104">Este artigo mostra como configurar a replicação geográfica ativa para o Banco de Dados SQL no [portal do Azure](http://portal.azure.com) e para inicializar o failover.</span><span class="sxs-lookup"><span data-stu-id="683a0-104">This article shows you how to configure active geo-replication for SQL Database in the [Azure portal](http://portal.azure.com) and to initiate failover.</span></span>

<span data-ttu-id="683a0-105">Para iniciar um failover com o portal do Azure, veja [Iniciar um failover planejado ou não planejado para o Banco de Dados SQL do Azure com o portal do Azure](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="683a0-105">To initiate failover with the Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with the Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="683a0-106">Para configurar a replicação geográfica ativa usando o Portal do Azure, você precisa do seguinte recurso:</span><span class="sxs-lookup"><span data-stu-id="683a0-106">To configure active geo-replication by using the Azure portal, you need the following resource:</span></span>

* <span data-ttu-id="683a0-107">Um Banco de Dados SQL do Azure: o banco de dados primário que você deseja replicar para uma região geográfica diferente.</span><span class="sxs-lookup"><span data-stu-id="683a0-107">An Azure SQL database: The primary database that you want to replicate to a different geographical region.</span></span>

> [!Note]
<span data-ttu-id="683a0-108">A replicação geográfica ativa deve estar entre bancos de dados da mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="683a0-108">Active geo-replication must be between databases in the same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="683a0-109">Adicionar um banco de dados secundário</span><span class="sxs-lookup"><span data-stu-id="683a0-109">Add a secondary database</span></span>
<span data-ttu-id="683a0-110">As etapas a seguir criam um novo banco de dados secundário em uma parceria de replicação geográfica.</span><span class="sxs-lookup"><span data-stu-id="683a0-110">The following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="683a0-111">Para adicionar um banco de dados secundário, você deve ser o proprietário ou coproprietário da assinatura.</span><span class="sxs-lookup"><span data-stu-id="683a0-111">To add a secondary database, you must be the subscription owner or co-owner.</span></span>

<span data-ttu-id="683a0-112">O banco de dados secundário tem o mesmo nome do banco de dados primário e, por padrão, tem o mesmo nível de serviço.</span><span class="sxs-lookup"><span data-stu-id="683a0-112">The secondary database has the same name as the primary database and has, by default, the same service level.</span></span> <span data-ttu-id="683a0-113">O banco de dados secundário pode ser um banco de dados individual ou um banco de dados em um pool elástico.</span><span class="sxs-lookup"><span data-stu-id="683a0-113">The secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="683a0-114">Para obter mais informações, consulte [Camadas de serviço](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="683a0-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="683a0-115">Depois que o banco de dados secundário for criado e propagado, os dados começarão a serem replicados desde o banco de dados primário até o novo banco de dados secundário.</span><span class="sxs-lookup"><span data-stu-id="683a0-115">After the secondary is created and seeded, data begins replicating from the primary database to the new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="683a0-116">O comando falhará se o banco de dados do parceiro já existir (por exemplo, como resultado do término de uma relação de replicação geográfica anterior).</span><span class="sxs-lookup"><span data-stu-id="683a0-116">If the partner database already exists (for example, as a result of terminating a previous geo-replication relationship) the command fails.</span></span>
> 

1. <span data-ttu-id="683a0-117">No [portal do Azure](http://portal.azure.com), navegue até o banco de dados que você deseja configurar para a replicação geográfica.</span><span class="sxs-lookup"><span data-stu-id="683a0-117">In the [Azure portal](http://portal.azure.com), browse to the database that you want to set up for geo-replication.</span></span>
2. <span data-ttu-id="683a0-118">Na página de banco de dados SQL, selecione **replicação geográfica** e, em seguida, selecione a região para criar o banco de dados secundário.</span><span class="sxs-lookup"><span data-stu-id="683a0-118">On the SQL database page, select **geo-replication**, and then select the region to create the secondary database.</span></span> <span data-ttu-id="683a0-119">É possível selecionar qualquer região além da região que hospeda o banco de dados primário, mas recomendamos a [região emparelhada](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="683a0-119">You can select any region other than the region hosting the primary database, but we recommend the [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Configurar a replicação geográfica](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="683a0-121">Selecione ou configure o servidor e o tipo de preço do banco de dados secundário.</span><span class="sxs-lookup"><span data-stu-id="683a0-121">Select or configure the server and pricing tier for the secondary database.</span></span>
   
    ![Configurar secundário](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="683a0-123">Opcionalmente, você pode adicionar um banco de dados secundário a um pool elástico.</span><span class="sxs-lookup"><span data-stu-id="683a0-123">Optionally, you can add a secondary database to an elastic pool.</span></span> <span data-ttu-id="683a0-124">Para criar o banco de dados secundário em um pool, clique em **pool elástico** e selecione um pool no servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="683a0-124">To create the secondary database in a pool, click **elastic pool** and select a pool on the target server.</span></span> <span data-ttu-id="683a0-125">Um pool já deve existir no servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="683a0-125">A pool must already exist on the target server.</span></span> <span data-ttu-id="683a0-126">Esse fluxo de trabalho não cria um pool.</span><span class="sxs-lookup"><span data-stu-id="683a0-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="683a0-127">Clique em **Criar** para adicionar o secundário.</span><span class="sxs-lookup"><span data-stu-id="683a0-127">Click **Create** to add the secondary.</span></span>
6. <span data-ttu-id="683a0-128">O banco de dados secundário é criado e começa o processo de propagação.</span><span class="sxs-lookup"><span data-stu-id="683a0-128">The secondary database is created and the seeding process begins.</span></span>
   
    ![Configurar secundário](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="683a0-130">Quando o processo de propagação for concluído, o banco de dados secundário exibirá seu status.</span><span class="sxs-lookup"><span data-stu-id="683a0-130">When the seeding process is complete, the secondary database displays its status.</span></span>
   
    ![Propagação concluída](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="683a0-132">Iniciar um failover</span><span class="sxs-lookup"><span data-stu-id="683a0-132">Initiate a failover</span></span>

<span data-ttu-id="683a0-133">O banco de dados secundário pode ser alternado para se tornar primário.</span><span class="sxs-lookup"><span data-stu-id="683a0-133">The secondary database can be switched to become the primary.</span></span>  

1. <span data-ttu-id="683a0-134">No [portal do Azure](http://portal.azure.com), navegue até o banco de dados primário na parceria de replicação geográfica.</span><span class="sxs-lookup"><span data-stu-id="683a0-134">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="683a0-135">Na folha Banco de dados SQL, selecione **Todas as configurações** > **replicação geográfica**.</span><span class="sxs-lookup"><span data-stu-id="683a0-135">On the SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="683a0-136">Na lista **SECUNDÁRIOS**, selecione o banco de dados que deverá se tornar o novo primário e clique em **Failover**.</span><span class="sxs-lookup"><span data-stu-id="683a0-136">In the **SECONDARIES** list, select the database you want to become the new primary and click **Failover**.</span></span>
   
    ![Failover](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="683a0-138">Clique em **Sim** para iniciar o failover.</span><span class="sxs-lookup"><span data-stu-id="683a0-138">Click **Yes** to begin the failover.</span></span>

<span data-ttu-id="683a0-139">O comando mudará imediatamente o banco de dados secundário para a função primária.</span><span class="sxs-lookup"><span data-stu-id="683a0-139">The command immediately switches the secondary database into the primary role.</span></span> 

<span data-ttu-id="683a0-140">Há um breve período durante o qual os bancos de dados não estão disponíveis (na ordem de 0 a 25 segundos) enquanto as funções são alternadas.</span><span class="sxs-lookup"><span data-stu-id="683a0-140">There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched.</span></span> <span data-ttu-id="683a0-141">Se o banco de dados primário tiver vários bancos de dados secundários, o comando reconfigurará automaticamente os outros secundários para se conectarem ao novo primário.</span><span class="sxs-lookup"><span data-stu-id="683a0-141">If the primary database has multiple secondary databases, the command automatically reconfigures the other secondaries to connect to the new primary.</span></span> <span data-ttu-id="683a0-142">A operação inteira deve levar menos de um minuto para ser concluída em circunstâncias normais.</span><span class="sxs-lookup"><span data-stu-id="683a0-142">The entire operation should take less than a minute to complete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="683a0-143">Este comando destina-se à recuperação rápida do banco de dados em caso de interrupção.</span><span class="sxs-lookup"><span data-stu-id="683a0-143">This command is designed for quick recovery of the database in case of an outage.</span></span> <span data-ttu-id="683a0-144">Ele dispara o failover sem sincronização de dados (failover forçado).</span><span class="sxs-lookup"><span data-stu-id="683a0-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="683a0-145">Se o primário estiver online e realizando transações quando o comando for emitido, alguma perda de dados poderá ocorrer.</span><span class="sxs-lookup"><span data-stu-id="683a0-145">If the primary is online and committing transactions when the command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="683a0-146">Remover banco de dados secundário</span><span class="sxs-lookup"><span data-stu-id="683a0-146">Remove secondary database</span></span>
<span data-ttu-id="683a0-147">Essa operação termina permanentemente a replicação para o banco de dados secundário e altera a função do secundário para um banco de dados de leitura/gravação normal.</span><span class="sxs-lookup"><span data-stu-id="683a0-147">This operation permanently terminates the replication to the secondary database, and changes the role of the secondary to a regular read-write database.</span></span> <span data-ttu-id="683a0-148">Se a conectividade com o banco de dados secundário for desfeita, o comando terá êxito, mas o secundário só se tornará de leitura/gravação quando a conectividade for restaurada.</span><span class="sxs-lookup"><span data-stu-id="683a0-148">If the connectivity to the secondary database is broken, the command succeeds but the secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="683a0-149">No [portal do Azure](http://portal.azure.com), navegue até o banco de dados primário na parceria de replicação geográfica.</span><span class="sxs-lookup"><span data-stu-id="683a0-149">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="683a0-150">Na página do Banco de dados SQL, selecione **Replicação geográfica**.</span><span class="sxs-lookup"><span data-stu-id="683a0-150">On the SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="683a0-151">Na lista **SECUNDÁRIOS**, selecione o banco de dados que você deseja remover da parceria de replicação geográfica.</span><span class="sxs-lookup"><span data-stu-id="683a0-151">In the **SECONDARIES** list, select the database you want to remove from the geo-replication partnership.</span></span>
4. <span data-ttu-id="683a0-152">Clique em **Parar Replicação**.</span><span class="sxs-lookup"><span data-stu-id="683a0-152">Click **Stop Replication**.</span></span>
   
    ![Remover secundário](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="683a0-154">Uma janela de confirmação é aberta.</span><span class="sxs-lookup"><span data-stu-id="683a0-154">A confirmation window opens.</span></span> <span data-ttu-id="683a0-155">Clique em **Sim** para remover o banco de dados da parceria de replicação geográfica.</span><span class="sxs-lookup"><span data-stu-id="683a0-155">Click **Yes** to remove the database from the geo-replication partnership.</span></span> <span data-ttu-id="683a0-156">(Defina-o como um banco de dados de leitura/gravação que não faz parte de nenhuma replicação.)</span><span class="sxs-lookup"><span data-stu-id="683a0-156">(Set it to a read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="683a0-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="683a0-157">Next steps</span></span>
* <span data-ttu-id="683a0-158">Para saber mais sobre a replicação geográfica ativa, confira [Replicação geográfica ativa](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="683a0-158">To learn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="683a0-159">Para obter uma visão geral e os cenários de continuidade dos negócios, consulte [Visão geral da continuidade dos negócios](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="683a0-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

