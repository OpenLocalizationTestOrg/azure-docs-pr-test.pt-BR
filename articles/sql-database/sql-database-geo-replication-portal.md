---
title: "Portal do Azure: replicação geográfica do Banco de Dados SQL | Microsoft Docs"
description: "Configurar a replicação geográfica para o banco de dados do SQL Azure hello portal do Azure e iniciar failover"
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
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a><span data-ttu-id="d4cfa-103">Configurar a replicação geográfica ativa para o banco de dados do SQL Azure hello portal do Azure e iniciar failover</span><span class="sxs-lookup"><span data-stu-id="d4cfa-103">Configure active geo-replication for Azure SQL Database in hello Azure portal and initiate failover</span></span>

<span data-ttu-id="d4cfa-104">Este artigo mostra como tooconfigure replicação geográfica ativa para banco de dados SQL em Olá [portal do Azure](http://portal.azure.com) e tooinitiate failover.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-104">This article shows you how tooconfigure active geo-replication for SQL Database in hello [Azure portal](http://portal.azure.com) and tooinitiate failover.</span></span>

<span data-ttu-id="d4cfa-105">failover de tooinitiate com hello portal do Azure, consulte [iniciar um failover planejado ou não planejado para o banco de dados do SQL Azure com hello portal do Azure](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d4cfa-105">tooinitiate failover with hello Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with hello Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="d4cfa-106">tooconfigure replicação geográfica usando Olá portal do Azure, você precisará Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4cfa-106">tooconfigure active geo-replication by using hello Azure portal, you need hello following resource:</span></span>

* <span data-ttu-id="d4cfa-107">Um banco de dados do SQL Azure: banco de dados primário Olá que você deseja tooreplicate tooa região geográfica diferente.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-107">An Azure SQL database: hello primary database that you want tooreplicate tooa different geographical region.</span></span>

> [!Note]
<span data-ttu-id="d4cfa-108">Replicação geográfica deve estar entre bancos de dados em Olá mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-108">Active geo-replication must be between databases in hello same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="d4cfa-109">Adicionar um banco de dados secundário</span><span class="sxs-lookup"><span data-stu-id="d4cfa-109">Add a secondary database</span></span>
<span data-ttu-id="d4cfa-110">Olá etapas a seguir criam um novo banco de dados secundário em uma parceria de replicação geográfica.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-110">hello following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="d4cfa-111">tooadd um banco de dados secundário, você deve ser o proprietário da assinatura hello ou coproprietário.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-111">tooadd a secondary database, you must be hello subscription owner or co-owner.</span></span>

<span data-ttu-id="d4cfa-112">banco de dados secundário Olá Olá mesmo nome como o banco de dados primário hello e tem, por padrão, Olá mesmo nível de serviço.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-112">hello secondary database has hello same name as hello primary database and has, by default, hello same service level.</span></span> <span data-ttu-id="d4cfa-113">banco de dados secundário Olá pode ser um único banco de dados ou um banco de dados em um pool Elástico.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-113">hello secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="d4cfa-114">Para obter mais informações, consulte [Camadas de serviço](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="d4cfa-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="d4cfa-115">Após Olá secundário é criado e propagado, dados começam a replicar de saudação banco de dados primário toohello novo banco de dados secundário.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-115">After hello secondary is created and seeded, data begins replicating from hello primary database toohello new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="d4cfa-116">Se o banco de dados de parceiro Olá já existe (por exemplo, em decorrência de encerrar um relacionamento de replicação geográfica anterior) Olá falhará.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-116">If hello partner database already exists (for example, as a result of terminating a previous geo-replication relationship) hello command fails.</span></span>
> 

1. <span data-ttu-id="d4cfa-117">Em Olá [portal do Azure](http://portal.azure.com), procurar toohello banco de dados que você deseja tooset para replicação geográfica.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-117">In hello [Azure portal](http://portal.azure.com), browse toohello database that you want tooset up for geo-replication.</span></span>
2. <span data-ttu-id="d4cfa-118">Na página de banco de dados do SQL hello, selecione **georeplicação**e, em seguida, selecione Olá região toocreate Olá banco de dados secundário.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-118">On hello SQL database page, select **geo-replication**, and then select hello region toocreate hello secondary database.</span></span> <span data-ttu-id="d4cfa-119">Você pode selecionar qualquer região diferente de região Olá hospeda o banco de dados primário hello, mas é recomendável Olá [região emparelhada](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="d4cfa-119">You can select any region other than hello region hosting hello primary database, but we recommend hello [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Configurar a replicação geográfica](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="d4cfa-121">Selecione ou configurar o servidor de saudação e preços do banco de dados secundário hello.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-121">Select or configure hello server and pricing tier for hello secondary database.</span></span>
   
    ![Configurar secundário](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="d4cfa-123">Opcionalmente, você pode adicionar um pool Elástico do banco de dados secundário tooan.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-123">Optionally, you can add a secondary database tooan elastic pool.</span></span> <span data-ttu-id="d4cfa-124">toocreate Olá banco de dados secundário em um pool, clique em **pool Elástico** e selecione um pool no servidor de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-124">toocreate hello secondary database in a pool, click **elastic pool** and select a pool on hello target server.</span></span> <span data-ttu-id="d4cfa-125">Um pool já deve existir no servidor de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-125">A pool must already exist on hello target server.</span></span> <span data-ttu-id="d4cfa-126">Esse fluxo de trabalho não cria um pool.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="d4cfa-127">Clique em **criar** tooadd Olá secundário.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-127">Click **Create** tooadd hello secondary.</span></span>
6. <span data-ttu-id="d4cfa-128">banco de dados secundário Olá é criado e começa a saudação processo de preparação.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-128">hello secondary database is created and hello seeding process begins.</span></span>
   
    ![Configurar secundário](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="d4cfa-130">Quando Olá propagação processo for concluído, o banco de dados secundário Olá exibe seu status.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-130">When hello seeding process is complete, hello secondary database displays its status.</span></span>
   
    ![Propagação concluída](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="d4cfa-132">Iniciar um failover</span><span class="sxs-lookup"><span data-stu-id="d4cfa-132">Initiate a failover</span></span>

<span data-ttu-id="d4cfa-133">banco de dados secundário Olá pode ser desligados toobecome Olá primário.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-133">hello secondary database can be switched toobecome hello primary.</span></span>  

1. <span data-ttu-id="d4cfa-134">Em Olá [portal do Azure](http://portal.azure.com), procurar banco de dados primário na parceria de replicação geográfica Olá toohello.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-134">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="d4cfa-135">Na folha de banco de dados SQL hello, selecione **todas as configurações** > **georeplicação**.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-135">On hello SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="d4cfa-136">Em Olá **SECUNDÁRIOS** lista, selecione Olá banco de dados toobecome Olá novo primário e clique em **Failover**.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-136">In hello **SECONDARIES** list, select hello database you want toobecome hello new primary and click **Failover**.</span></span>
   
    ![Failover](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="d4cfa-138">Clique em **Sim** toobegin Olá failover.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-138">Click **Yes** toobegin hello failover.</span></span>

<span data-ttu-id="d4cfa-139">comando Olá imediatamente alterna o banco de dados secundário Olá na função primária hello.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-139">hello command immediately switches hello secondary database into hello primary role.</span></span> 

<span data-ttu-id="d4cfa-140">Há um curto período durante o qual ambos os bancos de dados não estão disponíveis (em ordem de saudação de 0 segundos too25) enquanto a troca de funções hello.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-140">There is a short period during which both databases are unavailable (on hello order of 0 too25 seconds) while hello roles are switched.</span></span> <span data-ttu-id="d4cfa-141">Se o banco de dados primário Olá tem vários bancos de dados secundários, o comando Olá automaticamente configura Olá novo primário outros secundários tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-141">If hello primary database has multiple secondary databases, hello command automatically reconfigures hello other secondaries tooconnect toohello new primary.</span></span> <span data-ttu-id="d4cfa-142">saudação de toda a operação deve levar menos de um minuto toocomplete em circunstâncias normais.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-142">hello entire operation should take less than a minute toocomplete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="d4cfa-143">Esse comando é projetado para rápida recuperação de banco de dados de saudação em caso de uma interrupção.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-143">This command is designed for quick recovery of hello database in case of an outage.</span></span> <span data-ttu-id="d4cfa-144">Ele dispara o failover sem sincronização de dados (failover forçado).</span><span class="sxs-lookup"><span data-stu-id="d4cfa-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="d4cfa-145">Se Olá primário está online e confirmar transações quando o comando Olá é emitido alguma perda de dados pode ocorrer.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-145">If hello primary is online and committing transactions when hello command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="d4cfa-146">Remover banco de dados secundário</span><span class="sxs-lookup"><span data-stu-id="d4cfa-146">Remove secondary database</span></span>
<span data-ttu-id="d4cfa-147">Esta operação permanentemente encerra Olá replicação toohello banco de dados secundário e alterações Olá função do banco de dados de leitura-gravação regular Olá tooa secundário.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-147">This operation permanently terminates hello replication toohello secondary database, and changes hello role of hello secondary tooa regular read-write database.</span></span> <span data-ttu-id="d4cfa-148">Se Olá conectividade toohello banco de dados secundário for interrompido, o comando Olá terá êxito, mas Olá secundário faz não tornam-se leitura / gravação até depois que a conectividade é restaurada.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-148">If hello connectivity toohello secondary database is broken, hello command succeeds but hello secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="d4cfa-149">Em Olá [portal do Azure](http://portal.azure.com), procurar banco de dados primário na parceria de replicação geográfica Olá toohello.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-149">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="d4cfa-150">Na página de banco de dados do SQL hello, selecione **georeplicação**.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-150">On hello SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="d4cfa-151">Em Olá **SECUNDÁRIOS** lista, Olá selecione banco de dados tooremove da parceria de replicação geográfica hello.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-151">In hello **SECONDARIES** list, select hello database you want tooremove from hello geo-replication partnership.</span></span>
4. <span data-ttu-id="d4cfa-152">Clique em **Parar Replicação**.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-152">Click **Stop Replication**.</span></span>
   
    ![Remover secundário](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="d4cfa-154">Uma janela de confirmação é aberta.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-154">A confirmation window opens.</span></span> <span data-ttu-id="d4cfa-155">Clique em **Sim** tooremove o banco de dados de saudação da parceria de replicação geográfica hello.</span><span class="sxs-lookup"><span data-stu-id="d4cfa-155">Click **Yes** tooremove hello database from hello geo-replication partnership.</span></span> <span data-ttu-id="d4cfa-156">(Defini-lo tooa o banco de dados de leitura / gravação não faz parte de qualquer replicação.)</span><span class="sxs-lookup"><span data-stu-id="d4cfa-156">(Set it tooa read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4cfa-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4cfa-157">Next steps</span></span>
* <span data-ttu-id="d4cfa-158">toolearn mais sobre a replicação geográfica, consulte [replicação geográfica ativa](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d4cfa-158">toolearn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="d4cfa-159">Para obter uma visão geral e os cenários de continuidade dos negócios, consulte [Visão geral da continuidade dos negócios](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="d4cfa-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

