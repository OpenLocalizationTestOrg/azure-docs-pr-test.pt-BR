---
title: "Portal do Azure: criar e gerenciar um pool elástico do Banco de Dados SQL | Microsoft Docs"
description: "Saiba como toouse Olá portal do Azure e toomanage de inteligência interna do banco de dados SQL, o monitor e um pool Elástico escalonável toooptimize banco de dados de desempenho de tamanho de direito e gerenciar os custos."
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a><span data-ttu-id="5c165-103">Criar e gerenciar um pool Elástico com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5c165-103">Create and manage an elastic pool with hello Azure portal</span></span>
<span data-ttu-id="5c165-104">Este tópico mostra como toocreate e gerenciar escalonável [pools Elásticos](sql-database-elastic-pool.md) com hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c165-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with hello Azure portal.</span></span> <span data-ttu-id="5c165-105">Você também pode criar e gerenciar um pool Elástico do Azure com [PowerShell](sql-database-elastic-pool-manage-powershell.md), Olá API REST, ou [c#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="5c165-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="5c165-106">Você também pode criar e mover bancos de dados de e para os pools elásticos usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="5c165-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="5c165-107">Criar um pool elástico</span><span class="sxs-lookup"><span data-stu-id="5c165-107">Create an elastic pool</span></span> 

<span data-ttu-id="5c165-108">Há duas maneiras de criar um pool elástico.</span><span class="sxs-lookup"><span data-stu-id="5c165-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="5c165-109">Você pode fazer isso do zero, se você souber que a instalação Olá pool desejado ou começar com uma recomendação do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-109">You can do it from scratch if you know hello pool setup you want, or start with a recommendation from hello service.</span></span> <span data-ttu-id="5c165-110">Banco de dados SQL tem inteligência interna que recomenda uma configuração de pool Elástico se mais eficiente com base no hello após telemetria de uso de seus bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="5c165-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on hello past usage telemetry for your databases.</span></span>

<span data-ttu-id="5c165-111">Você pode criar vários pools em um servidor, mas você não pode adicionar bancos de dados de diferentes servidores em Olá mesmo pool.</span><span class="sxs-lookup"><span data-stu-id="5c165-111">You can create multiple pools on a server, but you can't add databases from different servers into hello same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="5c165-112">Os pools elásticos têm uma disponibilidade geral (DG) em todas as regiões do Azure, exceto na Índia Ocidental, onde atualmente estão no modo de visualização.</span><span class="sxs-lookup"><span data-stu-id="5c165-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="5c165-113">A GA dos pools elásticos nessa região ocorrerá assim que possível.</span><span class="sxs-lookup"><span data-stu-id="5c165-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="5c165-114">Etapa 1: criar um pool elástico</span><span class="sxs-lookup"><span data-stu-id="5c165-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="5c165-115">Criando um pool Elástico de uma já existente **server** folha no portal de saudação é hello mais fácil maneira toomove bancos de dados existentes em um pool Elástico.</span><span class="sxs-lookup"><span data-stu-id="5c165-115">Creating an elastic pool from an existing **server** blade in hello portal is hello easiest way toomove existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="5c165-116">Você também pode criar um pool Elástico pesquisando **pool Elástico do SQL** em Olá **Marketplace** ou clicando em **+ adicionar** em Olá **pools Elásticos de SQL**procurar folha.</span><span class="sxs-lookup"><span data-stu-id="5c165-116">You can also create an elastic pool by searching **SQL elastic pool** in hello **Marketplace** or clicking **+Add** in hello **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="5c165-117">Você é capaz de toospecify um servidor novo ou existente por este fluxo de trabalho de provisionamento do pool.</span><span class="sxs-lookup"><span data-stu-id="5c165-117">You are able toospecify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="5c165-118">Em Olá [portal do Azure](http://portal.azure.com/), clique em **mais serviços**  **>**  **servidores SQL**e clique em servidor de saudação que contém a saudação bancos de dados você deseja que o pool Elástico do tooadd tooan.</span><span class="sxs-lookup"><span data-stu-id="5c165-118">In hello [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click hello server that contains hello databases you want tooadd tooan elastic pool.</span></span>
2. <span data-ttu-id="5c165-119">Clique em **Novo pool**.</span><span class="sxs-lookup"><span data-stu-id="5c165-119">Click **New pool**.</span></span>

    ![Adicionar pool de servidores tooa](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="5c165-121">**-OU-**</span><span class="sxs-lookup"><span data-stu-id="5c165-121">**-OR-**</span></span>

    <span data-ttu-id="5c165-122">Você verá uma mensagem informando que há são recomendadas pools Elásticos para o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-122">You may see a message saying there are recommended elastic pools for hello server.</span></span> <span data-ttu-id="5c165-123">Clique em Olá de toosee mensagem de saudação recomendado pools com base na telemetria de uso do banco de dados históricos, Olá camada toosee mais detalhes e clique personalizar pool hello.</span><span class="sxs-lookup"><span data-stu-id="5c165-123">Click hello message toosee hello recommended pools based on historical database usage telemetry, and then click hello tier toosee more details and customize hello pool.</span></span> <span data-ttu-id="5c165-124">Consulte [entender as recomendações de pool](#understand-elastic-pool-recommendations) mais adiante neste tópico para como recomendação de saudação é feita.</span><span class="sxs-lookup"><span data-stu-id="5c165-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how hello recommendation is made.</span></span>

    ![pool recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="5c165-126">Olá **pool Elástico** folha é exibida, que é onde você especificar configurações de saudação para o pool.</span><span class="sxs-lookup"><span data-stu-id="5c165-126">hello **elastic pool** blade appears, which is where you specify hello settings for your pool.</span></span> <span data-ttu-id="5c165-127">Se você clicou **novo pool** na etapa anterior de saudação, Olá preço é **padrão** por padrão e não há bancos de dados é selecionada.</span><span class="sxs-lookup"><span data-stu-id="5c165-127">If you clicked **New pool** in hello previous step, hello pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="5c165-128">Você pode criar um conjunto vazio, ou especificar um conjunto de bancos de dados existentes de toomove desse servidor no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-128">You can create an empty pool, or specify a set of existing databases from that server toomove into hello pool.</span></span> <span data-ttu-id="5c165-129">Se você estiver criando um pool recomendado, Olá recomendado preço, as configurações de desempenho e a lista de bancos de dados são preenchidos de antemão, mas você ainda pode alterá-los.</span><span class="sxs-lookup"><span data-stu-id="5c165-129">If you are creating a recommended pool, hello recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![Configurar pool elástico](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="5c165-131">Especifique um nome para o pool Elástico hello, ou deixá-lo como padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-131">Specify a name for hello elastic pool, or leave it as hello default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="5c165-132">Etapa 2: escolher um tipo de preço</span><span class="sxs-lookup"><span data-stu-id="5c165-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="5c165-133">Olá de preço do pool determina Olá recursos elastics toohello disponível no pool de saudação e Olá o número máximo de eDTUs (eDTU máximo) e o banco de dados do armazenamento (GBs) tooeach disponíveis.</span><span class="sxs-lookup"><span data-stu-id="5c165-133">hello pool's pricing tier determines hello features available toohello elastics in hello pool, and hello maximum number of eDTUs (eDTU MAX), and storage (GBs) available tooeach database.</span></span> <span data-ttu-id="5c165-134">Para obter detalhes, consulte Camadas de serviço.</span><span class="sxs-lookup"><span data-stu-id="5c165-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="5c165-135">toochange Olá preço para o pool de saudação, clique em **preço**, clique em Olá preço você deseja e, em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="5c165-135">toochange hello pricing tier for hello pool, click **Pricing tier**, click hello pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c165-136">Depois que você escolha Olá preço e confirmar suas alterações, clicando em **Okey** na última etapa de hello, não será Olá toochange capaz de preço do pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-136">After you choose hello pricing tier and commit your changes by clicking **OK** in hello last step, you won't be able toochange hello pricing tier of hello pool.</span></span> <span data-ttu-id="5c165-137">toochange Olá camada de preços para um pool Elástico existente, criar um pool Elástico em Olá desejado de preço e migre Olá bancos de dados toothis novo pool.</span><span class="sxs-lookup"><span data-stu-id="5c165-137">toochange hello pricing tier for an existing elastic pool, create an elastic pool in hello desired pricing tier and migrate hello databases toothis new pool.</span></span>
>

![Selecione uma faixa de preço.](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a><span data-ttu-id="5c165-139">Etapa 3: Configurar o pool de saudação</span><span class="sxs-lookup"><span data-stu-id="5c165-139">Step 3: Configure hello pool</span></span>

<span data-ttu-id="5c165-140">Depois de definir Olá preço, clique em Configurar pool onde adicionar bancos de dados, eDTUs de pool do conjunto e armazenamento (GBs de pool), e defina Olá eDTUs de min e max para elastics Olá no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-140">After setting hello pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set hello min and max eDTUs for hello elastics in hello pool.</span></span>

1. <span data-ttu-id="5c165-141">Clique em **Configurar pool**</span><span class="sxs-lookup"><span data-stu-id="5c165-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="5c165-142">Selecione bancos de dados de saudação que você deseja tooadd toohello pool.</span><span class="sxs-lookup"><span data-stu-id="5c165-142">Select hello databases you want tooadd toohello pool.</span></span> <span data-ttu-id="5c165-143">Esta etapa é opcional durante a criação de pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-143">This step is optional while creating hello pool.</span></span> <span data-ttu-id="5c165-144">Bancos de dados podem ser adicionados depois Olá pool foi criado.</span><span class="sxs-lookup"><span data-stu-id="5c165-144">Databases can be added after hello pool has been created.</span></span>
    <span data-ttu-id="5c165-145">bancos de dados tooadd, clique em **Adicionar banco de dados**, clique em bancos de dados de saudação que você deseja tooadd e, em seguida, clique em Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="5c165-145">tooadd databases, click **Add database**, click hello databases that you want tooadd, and then click hello **Select** button.</span></span>

    ![Adicionar bancos de dados](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="5c165-147">Se os bancos de dados Olá estiver trabalhando com tem telemetria suficiente histórico de uso, Olá **estimado de eDTU e GB uso** gráfico e hello **real eDTU uso** toohelp de atualização de gráfico de barras que facilitam a configuração decisões.</span><span class="sxs-lookup"><span data-stu-id="5c165-147">If hello databases you're working with have enough historical usage telemetry, hello **Estimated eDTU and GB usage** graph and hello **Actual eDTU usage** bar chart update toohelp you make configuration decisions.</span></span> <span data-ttu-id="5c165-148">Além disso, o serviço de saudação pode oferecer um toohelp de mensagem de recomendação você direita tamanho Olá pool.</span><span class="sxs-lookup"><span data-stu-id="5c165-148">Also, hello service may give you a recommendation message toohelp you right-size hello pool.</span></span> <span data-ttu-id="5c165-149">Veja [Recomendações dinâmicas](#understand-elastic-pool-recommendations).</span><span class="sxs-lookup"><span data-stu-id="5c165-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="5c165-150">Usar controles Olá Olá **configurar pool** tooexplore configurações de página e configurar o pool.</span><span class="sxs-lookup"><span data-stu-id="5c165-150">Use hello controls on hello **Configure pool** page tooexplore settings and configure your pool.</span></span> <span data-ttu-id="5c165-151">Confira [Limites dos pools elásticos](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) para saber mais sobre os limites de cada camada de serviço, e confira as [Considerações de preço e desempenho dos pools elásticos](sql-database-elastic-pool.md) para obter uma orientação detalhada sobre o tamanho correto de um pool elástico.</span><span class="sxs-lookup"><span data-stu-id="5c165-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="5c165-152">Para ler mais informações sobre as configurações do pool, confira as [Propriedades do pool elástico](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span><span class="sxs-lookup"><span data-stu-id="5c165-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![Configurar pool elástico](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="5c165-154">Clique em **selecione** em Olá **configurar Pool** folha depois de alterar as configurações.</span><span class="sxs-lookup"><span data-stu-id="5c165-154">Click **Select** in hello **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="5c165-155">Clique em **Okey** toocreate pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-155">Click **OK** toocreate hello pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="5c165-156">Compreensão das recomendações de pool elástico</span><span class="sxs-lookup"><span data-stu-id="5c165-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="5c165-157">Olá serviço de banco de dados SQL avalia o histórico de uso e recomenda um ou mais pools quando ele é mais econômico que bancos de dados único.</span><span class="sxs-lookup"><span data-stu-id="5c165-157">hello SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="5c165-158">Cada recomendação é configurada com um subconjunto de bancos de dados do servidor de saudação que melhor se adaptar pool Olá exclusivo.</span><span class="sxs-lookup"><span data-stu-id="5c165-158">Each recommendation is configured with a unique subset of hello server's databases that best fit hello pool.</span></span>

![pool recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="5c165-160">recomendação de pool de saudação inclui:</span><span class="sxs-lookup"><span data-stu-id="5c165-160">hello pool recommendation comprises:</span></span>

- <span data-ttu-id="5c165-161">A camada de preços para o pool de saudação (Basic, Standard, Premium ou Premium RS)</span><span class="sxs-lookup"><span data-stu-id="5c165-161">A pricing tier for hello pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="5c165-162">Os **eDTUs do POOL** apropriados (também chamados de Máx. de eDTUs por pool)</span><span class="sxs-lookup"><span data-stu-id="5c165-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="5c165-163">Olá **eDTU máximo** e **Mín** por banco de dados</span><span class="sxs-lookup"><span data-stu-id="5c165-163">hello **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="5c165-164">lista de saudação de bancos de dados recomendados para o pool de saudação</span><span class="sxs-lookup"><span data-stu-id="5c165-164">hello list of recommended databases for hello pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c165-165">serviço de saudação considera Olá últimos 30 dias de telemetria ao recomendar pools.</span><span class="sxs-lookup"><span data-stu-id="5c165-165">hello service takes hello last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="5c165-166">Para ver um banco de dados do toobe considerado como candidata para um pool Elástico, ele deve existir pelo menos 7 dias.</span><span class="sxs-lookup"><span data-stu-id="5c165-166">For a database toobe considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="5c165-167">Os bancos de dados que já estão em um pool elástico não são considerados candidatos para as recomendações de pool elástico.</span><span class="sxs-lookup"><span data-stu-id="5c165-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="5c165-168">serviço de saudação avalia as necessidades de recursos e eficácia dos custos de movimentação Olá único bancos de dados em cada camada de serviço em pools de saudação mesmo nível.</span><span class="sxs-lookup"><span data-stu-id="5c165-168">hello service evaluates resource needs and cost effectiveness of moving hello single databases in each service tier into pools of hello same tier.</span></span> <span data-ttu-id="5c165-169">Por exemplo, todos os bancos de dados padrão em um servidor são avaliados para sua adaptação em um pool elástico Standard.</span><span class="sxs-lookup"><span data-stu-id="5c165-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="5c165-170">Isso significa que o serviço Olá não faz recomendações entre camadas como mover um banco de dados padrão em um pool de Premium.</span><span class="sxs-lookup"><span data-stu-id="5c165-170">This means hello service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="5c165-171">Depois de adicionar o pool de toohello de bancos de dados, as recomendações são geradas dinamicamente com base no histórico de uso de bancos de dados de saudação que você selecionou hello.</span><span class="sxs-lookup"><span data-stu-id="5c165-171">After adding databases toohello pool, recommendations are dynamically generated based on hello historical usage of hello databases you have selected.</span></span> <span data-ttu-id="5c165-172">Essas recomendações são mostradas em Olá eDTU e GB gráfico de uso em uma faixa de recomendação na parte superior de saudação do hello **configurar pool** folha.</span><span class="sxs-lookup"><span data-stu-id="5c165-172">These recommendations are shown in hello eDTU and GB usage chart and in a recommendation banner at hello top of hello **Configure pool** blade.</span></span> <span data-ttu-id="5c165-173">Essas recomendações são pretendido tooassist você na criação de um pool Elástico otimizado para seus bancos de dados específicos.</span><span class="sxs-lookup"><span data-stu-id="5c165-173">These recommendations are intended tooassist you in creating an elastic pool optimized for your specific databases.</span></span>

![Recomendações dinâmicas](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="5c165-175">Gerenciamento e monitoração um pool elástico</span><span class="sxs-lookup"><span data-stu-id="5c165-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="5c165-176">Você pode usar o hello toomonitor portal do Azure e gerenciar um pool Elástico e bancos de dados de saudação no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-176">You can use hello Azure portal toomonitor and manage an elastic pool and hello databases in hello pool.</span></span> <span data-ttu-id="5c165-177">No portal de hello, você pode monitorar a utilização de saudação de um pool Elástico e bancos de dados hello dentro desse pool.</span><span class="sxs-lookup"><span data-stu-id="5c165-177">From hello portal, you can monitor hello utilization of an elastic pool and hello databases within that pool.</span></span> <span data-ttu-id="5c165-178">Você também pode fazer um conjunto de alterações de pool Elástico tooyour e enviar todas as alterações no hello mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="5c165-178">You can also make a set of changes tooyour elastic pool and submit all changes at hello same time.</span></span> <span data-ttu-id="5c165-179">Essas alterações incluem adicionar ou remover bancos de dados, alterar as configurações de pool elástico ou alterar suas configurações de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5c165-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="5c165-180">Olá gráfico a seguir mostra um pool Elástico de exemplo.</span><span class="sxs-lookup"><span data-stu-id="5c165-180">hello following graphic shows an example elastic pool.</span></span> <span data-ttu-id="5c165-181">exibição de saudação inclui:</span><span class="sxs-lookup"><span data-stu-id="5c165-181">hello view includes:</span></span>

*  <span data-ttu-id="5c165-182">Gráficos de monitoramento de uso do recurso de pool Elástico hello e bancos de dados de saudação contidos no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-182">Charts for monitoring resource usage of both hello elastic pool and hello databases contained in hello pool.</span></span>
*  <span data-ttu-id="5c165-183">Olá **configurar** pool botão toomake pool Elástico toohello é alterado.</span><span class="sxs-lookup"><span data-stu-id="5c165-183">hello **Configure** pool button toomake changes toohello elastic pool.</span></span>
*  <span data-ttu-id="5c165-184">Olá **criar banco de dados** botão que cria um banco de dados e adiciona-o pool Elástico atual de toohello.</span><span class="sxs-lookup"><span data-stu-id="5c165-184">hello **Create database** button that creates a database and adds it toohello current elastic pool.</span></span>
*  <span data-ttu-id="5c165-185">Trabalhos elásticos que ajudam a gerenciar muitos bancos de dados executando scripts Transact SQL em todos os bancos de dados em uma lista.</span><span class="sxs-lookup"><span data-stu-id="5c165-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![Exibição de pool][2]

<span data-ttu-id="5c165-187">Você pode ir tooa determinado pool toosee sua utilização de recursos.</span><span class="sxs-lookup"><span data-stu-id="5c165-187">You can go tooa particular pool toosee its resource utilization.</span></span> <span data-ttu-id="5c165-188">Por padrão, o pool de saudação é configurado tooshow armazenamento e eDTU o uso de saudação última hora.</span><span class="sxs-lookup"><span data-stu-id="5c165-188">By default, hello pool is configured tooshow storage and eDTU usage for hello last hour.</span></span> <span data-ttu-id="5c165-189">gráfico de saudação pode ser configurado tooshow diferentes métricas em várias janelas de tempo.</span><span class="sxs-lookup"><span data-stu-id="5c165-189">hello chart can be configured tooshow different metrics over various time windows.</span></span>

1. <span data-ttu-id="5c165-190">Selecione um toowork de pool Elástico com.</span><span class="sxs-lookup"><span data-stu-id="5c165-190">Select an elastic pool toowork with.</span></span>
2. <span data-ttu-id="5c165-191">Em **Monitoramento de Pool Elástico** há um gráfico rotulado **Utilização de recursos**.</span><span class="sxs-lookup"><span data-stu-id="5c165-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="5c165-192">Clique em gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-192">Click hello chart.</span></span>

    ![Monitoramento de pool elástico][3]

    <span data-ttu-id="5c165-194">Olá **métrica** folha abre, mostrar uma exibição detalhada de saudação especificados métricas em janela de tempo especificada de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-194">hello **Metric** blade opens, showing a detailed view of hello specified metrics over hello specified time window.</span></span>   

    ![Lâmina Métrica][9]

### <a name="toocustomize-hello-chart-display"></a><span data-ttu-id="5c165-196">exibição de gráfico de saudação toocustomize</span><span class="sxs-lookup"><span data-stu-id="5c165-196">toocustomize hello chart display</span></span>

<span data-ttu-id="5c165-197">Você pode editar gráfico hello e Olá folha de métricas toodisplay outras métricas como porcentagem da CPU, porcentagem de e/s de dados e porcentagem de e/s de log usado.</span><span class="sxs-lookup"><span data-stu-id="5c165-197">You can edit hello chart and hello metric blade toodisplay other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="5c165-198">Na folha de métricas de saudação, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="5c165-198">On hello metric blade, click **Edit**.</span></span>

    ![Clique em editar][6]

2. <span data-ttu-id="5c165-200">Em Olá **Editar gráfico** folha, selecione um intervalo de tempo (última hora, atualmente, ou última semana), ou clique em **personalizado** tooselect qualquer data vão Olá duas últimas semanas.</span><span class="sxs-lookup"><span data-stu-id="5c165-200">In hello **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** tooselect any date range in hello last two weeks.</span></span> <span data-ttu-id="5c165-201">Selecione o tipo de gráfico hello (barra ou linha) e selecione Olá toomonitor de recursos.</span><span class="sxs-lookup"><span data-stu-id="5c165-201">Select hello chart type (bar or line), then select hello resources toomonitor.</span></span>

   > [!Note]
   > <span data-ttu-id="5c165-202">Somente o gráfico de métricas com hello mesma unidade de medida pode ser exibida em hello em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="5c165-202">Only metrics with hello same unit of measure can be displayed in hello chart at hello same time.</span></span> <span data-ttu-id="5c165-203">Por exemplo, se você selecionar "percentual de eDTU", em seguida, você pode apenas selecionar outras métricas com porcentagem como a unidade de medida de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as hello unit of measure.</span></span>
   >

    ![Clique em editar](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="5c165-205">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c165-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="5c165-206">Gerenciamento e monitoração de bancos de dados um pool elástico</span><span class="sxs-lookup"><span data-stu-id="5c165-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="5c165-207">Bancos de dados individuais também podem ser monitorados para identificar potenciais problemas.</span><span class="sxs-lookup"><span data-stu-id="5c165-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="5c165-208">Em **Monitoramento de Banco de Dados Elástico**, há um gráfico que exibe as métricas para cinco bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="5c165-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="5c165-209">Por padrão, Olá gráfico exibe Olá top 5 bancos de dados no pool de saudação pelo uso de eDTU médio em Olá última hora.</span><span class="sxs-lookup"><span data-stu-id="5c165-209">By default, hello chart displays hello top 5 databases in hello pool by average eDTU usage in hello past hour.</span></span> <span data-ttu-id="5c165-210">Clique em gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-210">Click hello chart.</span></span>

    ![Monitoramento de pool elástico][4]

2. <span data-ttu-id="5c165-212">Olá **utilização de recursos de banco de dados** folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="5c165-212">hello **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="5c165-213">Isso fornece uma exibição detalhada de uso do banco de dados de saudação no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-213">This provides a detailed view of hello database usage in hello pool.</span></span> <span data-ttu-id="5c165-214">Usando a grade de saudação na parte inferior de saudação da folha Olá, você pode selecionar qualquer banco de dados em Olá pool toodisplay seu uso no gráfico de saudação (backup de bancos de dados too5).</span><span class="sxs-lookup"><span data-stu-id="5c165-214">Using hello grid in hello lower part of hello blade, you can select any databases in hello pool toodisplay its usage in hello chart (up too5 databases).</span></span> <span data-ttu-id="5c165-215">Você também pode personalizar a janela de métricas e a hora de saudação exibida no gráfico de saudação clicando **Editar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="5c165-215">You can also customize hello metrics and time window displayed in hello chart by clicking **Edit chart**.</span></span>

    ![Folha Utilização de Recursos do Banco de Dados][8]

### <a name="toocustomize-hello-view"></a><span data-ttu-id="5c165-217">exibição de saudação toocustomize</span><span class="sxs-lookup"><span data-stu-id="5c165-217">toocustomize hello view</span></span>

1. <span data-ttu-id="5c165-218">Em Olá **utilização de recursos de banco de dados** folha, clique em **Editar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="5c165-218">In hello **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![Clique em Editar gráfico](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="5c165-220">Em Olá **editar** folha de gráfico, selecione um intervalo de tempo (última hora ou nas últimas 24 horas) ou clique em **personalizado** tooselect dia diferente no hello após toodisplay de 2 semanas.</span><span class="sxs-lookup"><span data-stu-id="5c165-220">In hello **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** tooselect a different day in hello past 2 weeks toodisplay.</span></span>

    ![Clique em Personalizar](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="5c165-222">Clique em Olá **comparar bancos de dados por** suspensa tooselect um toouse de métrica diferente ao comparar os bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="5c165-222">Click hello **Compare databases by** dropdown tooselect a different metric toouse when comparing databases.</span></span>

    ![Editar gráfico Olá](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a><span data-ttu-id="5c165-224">tooselect toomonitor de bancos de dados</span><span class="sxs-lookup"><span data-stu-id="5c165-224">tooselect databases toomonitor</span></span>

<span data-ttu-id="5c165-225">Na lista de banco de dados de saudação do hello **utilização de recursos de banco de dados** folha, você pode encontrar bancos de dados procurando por meio de páginas de saudação na lista de saudação ou digitando o nome de saudação do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5c165-225">In hello database list in hello **Database Resource Utilization** blade, you can find particular databases by looking through hello pages in hello list or by typing in hello name of a database.</span></span> <span data-ttu-id="5c165-226">Use banco de dados da saudação tooselect Olá caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="5c165-226">Use hello checkbox tooselect hello database.</span></span>

![Pesquise toomonitor de bancos de dados][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="5c165-228">Adicionar um recurso de pool Elástico tooan alerta</span><span class="sxs-lookup"><span data-stu-id="5c165-228">Add an alert tooan elastic pool resource</span></span>

<span data-ttu-id="5c165-229">Você pode adicionar regras tooan pool Elástico que enviar email de alerta ou toopeople pontos de extremidade de tooURL de cadeias de caracteres quando o pool Elástico Olá atinge um limite de utilização que você configurou.</span><span class="sxs-lookup"><span data-stu-id="5c165-229">You can add rules tooan elastic pool that send email toopeople or alert strings tooURL endpoints when hello elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="5c165-230">**tooadd um recurso de alerta tooany:**</span><span class="sxs-lookup"><span data-stu-id="5c165-230">**tooadd an alert tooany resource:**</span></span>

1. <span data-ttu-id="5c165-231">Clique em Olá **utilização de recursos** saudação do gráfico tooopen **métrica** folha, clique em **adicionar alerta**e, em seguida, preencha as informações Olá Olá **adicionar um alerta regra** folha (**recurso** configurar automaticamente ao pool de saudação toobe você está trabalhando com).</span><span class="sxs-lookup"><span data-stu-id="5c165-231">Click hello **Resource utilization** chart tooopen hello **Metric** blade, click **Add alert**, and then fill out hello information in hello **Add an alert rule** blade (**Resource** is automatically set up toobe hello pool you're working with).</span></span>
2. <span data-ttu-id="5c165-232">Digite um **nome** e **descrição** que identifica Olá tooyou de alerta e destinatários de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-232">Type a **Name** and **Description** that identifies hello alert tooyou and hello recipients.</span></span>
3. <span data-ttu-id="5c165-233">Escolha um **métrica** que você deseja tooalert da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-233">Choose a **Metric** that you want tooalert from hello list.</span></span>

    <span data-ttu-id="5c165-234">gráfico de Olá dinamicamente mostra a utilização de recursos para essa métrica toohelp que você escolher um limite.</span><span class="sxs-lookup"><span data-stu-id="5c165-234">hello chart dynamically shows resource utilization for that metric toohelp you choose a threshold.</span></span>

4. <span data-ttu-id="5c165-235">Escolha uma **Condição** (maior que, menor que, etc.) e um **Limite**.</span><span class="sxs-lookup"><span data-stu-id="5c165-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="5c165-236">Escolha um **período** de tempo que Olá métrica regra deve ser atendida antes de gatilhos de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-236">Choose a **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span>
6. <span data-ttu-id="5c165-237">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c165-237">Click **OK**.</span></span>

<span data-ttu-id="5c165-238">Para obter mais informações, consulte [Criar alertas do Banco de Dados SQL no portal do Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5c165-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="5c165-239">Mover um banco de dados para um pool elástico</span><span class="sxs-lookup"><span data-stu-id="5c165-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="5c165-240">Você pode adicionar ou remover bancos de dados de um pool existente.</span><span class="sxs-lookup"><span data-stu-id="5c165-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="5c165-241">bancos de dados Olá podem estar em outros pools.</span><span class="sxs-lookup"><span data-stu-id="5c165-241">hello databases can be in other pools.</span></span> <span data-ttu-id="5c165-242">No entanto, você só pode adicionar bancos de dados que estão em Olá mesmo servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="5c165-242">However, you can only add databases that are on hello same logical server.</span></span>

1. <span data-ttu-id="5c165-243">Na folha Olá para o pool de saudação em **bancos de dados Elásticos** clique **configurar pool**.</span><span class="sxs-lookup"><span data-stu-id="5c165-243">In hello blade for hello pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![Clique em Configurar pool][1]

2. <span data-ttu-id="5c165-245">Em Olá **configurar pool** folha, clique em **adicionar toopool**.</span><span class="sxs-lookup"><span data-stu-id="5c165-245">In hello **Configure pool** blade, click **Add toopool**.</span></span>

    ![Clique em Adicionar toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="5c165-247">Em Olá **adicionar bancos de dados** folha, banco de dados selecione hello ou pool de toohello tooadd bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="5c165-247">In hello **Add databases** blade, select hello database or databases tooadd toohello pool.</span></span> <span data-ttu-id="5c165-248">Em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="5c165-248">Then click **Select**.</span></span>

    ![Selecione tooadd de bancos de dados](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="5c165-250">Olá **configurar pool** folha agora listas Olá banco de dados selecionado toobe adicionado, e seu status definido muito**pendente**.</span><span class="sxs-lookup"><span data-stu-id="5c165-250">hello **Configure pool** blade now lists hello database you selected toobe added, with its status set too**Pending**.</span></span>

    ![Adições de pool pendentes](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="5c165-252">Em Olá **folha de pool configurar**, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="5c165-252">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Clique em Salvar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="5c165-254">Remover um banco de dados de um pool elástico</span><span class="sxs-lookup"><span data-stu-id="5c165-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="5c165-255">Em Olá **configurar pool** folha, banco de dados selecione hello ou tooremove de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="5c165-255">In hello **Configure pool** blade, select hello database or databases tooremove.</span></span>

    ![lista de bancos de dados](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="5c165-257">Clique em **Remover do pool**.</span><span class="sxs-lookup"><span data-stu-id="5c165-257">Click **Remove from pool**.</span></span>

    ![lista de bancos de dados](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="5c165-259">Olá **configurar pool** folha agora listas Olá banco de dados selecionado toobe removida com seu status definido muito**pendente**.</span><span class="sxs-lookup"><span data-stu-id="5c165-259">hello **Configure pool** blade now lists hello database you selected toobe removed with its status set too**Pending**.</span></span>

    ![visualização de adição ou remoção de banco de dados](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="5c165-261">Em Olá **folha de pool configurar**, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="5c165-261">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Clique em Salvar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="5c165-263">Alterar as configurações de desempenho de um pool elástico</span><span class="sxs-lookup"><span data-stu-id="5c165-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="5c165-264">Como monitorar a utilização de recursos de saudação de um pool Elástico, você pode descobrir que alguns ajustes são necessários.</span><span class="sxs-lookup"><span data-stu-id="5c165-264">As you monitor hello resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="5c165-265">Talvez pool Olá precisa de uma alteração nos limites de armazenamento ou desempenho hello.</span><span class="sxs-lookup"><span data-stu-id="5c165-265">Maybe hello pool needs a change in hello performance or storage limits.</span></span> <span data-ttu-id="5c165-266">Possivelmente, você deseja toochange configurações de banco de dados de saudação no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-266">Possibly you want toochange hello database settings in hello pool.</span></span> <span data-ttu-id="5c165-267">Você pode alterar a instalação de saudação do pool de saudação em qualquer tempo tooget Olá melhor equilíbrio entre desempenho e custo.</span><span class="sxs-lookup"><span data-stu-id="5c165-267">You can change hello setup of hello pool at any time tooget hello best balance of performance and cost.</span></span> <span data-ttu-id="5c165-268">Veja [Quando um pool elástico deve ser usado?](sql-database-elastic-pool.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="5c165-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="5c165-269">toochange Olá eDTUs armazenamento limites ou por pool e eDTUs por banco de dados:</span><span class="sxs-lookup"><span data-stu-id="5c165-269">toochange hello eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="5c165-270">Olá abrir **configurar pool** folha.</span><span class="sxs-lookup"><span data-stu-id="5c165-270">Open hello **Configure pool** blade.</span></span>

    <span data-ttu-id="5c165-271">Em **as configurações do pool Elástico**, usar ou configurações de pool do controle deslizante toochange hello.</span><span class="sxs-lookup"><span data-stu-id="5c165-271">Under **elastic pool settings**, use either slider toochange hello pool settings.</span></span>

    ![Utilização de recursos de pool elástico](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="5c165-273">Quando altera a configuração de saudação, exibição Olá mostra Olá mensal custo estimado de alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-273">When hello setting changes, hello display shows hello estimated monthly cost of hello change.</span></span>

    ![Atualização de um pool elástico e o novo custo mensal](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="5c165-275">Latência de operações do pool elástico</span><span class="sxs-lookup"><span data-stu-id="5c165-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="5c165-276">Alterar Olá min eDTUs por banco de dados ou o máximo de eDTUs por banco de dados normalmente é concluído em 5 minutos ou menos.</span><span class="sxs-lookup"><span data-stu-id="5c165-276">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="5c165-277">Alterar eDTUs Olá por pool de depende da quantidade total de saudação do espaço usado por todos os bancos de dados no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c165-277">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="5c165-278">As alterações levam, em média, 90 minutos ou menos a cada 100 GB.</span><span class="sxs-lookup"><span data-stu-id="5c165-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="5c165-279">Por exemplo, se o espaço total Olá usado por todos os bancos de dados no pool de saudação é de 200 GB, Olá esperada de latência para mudar o eDTU do pool de saudação por pool é de 3 horas ou menos.</span><span class="sxs-lookup"><span data-stu-id="5c165-279">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c165-280">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5c165-280">Next steps</span></span>

- <span data-ttu-id="5c165-281">toounderstand que um pool Elástico, consulte [pool Elástico de banco de dados SQL](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="5c165-281">toounderstand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="5c165-282">Para ler mais diretrizes sobre o uso dos pools elásticos, confira [Considerações de preço e desempenho para pools elásticos](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="5c165-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="5c165-283">toouse trabalhos Elástico toorun Transact-SQL scripts em relação a qualquer número de bancos de dados no pool de hello, consulte [visão geral de trabalhos Elástico](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c165-283">toouse elastic jobs toorun Transact-SQL scripts against any number of databases in hello pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="5c165-284">tooquery em qualquer número de bancos de dados no pool de hello, consulte [visão geral de consulta Elástico](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c165-284">tooquery across any number of databases in hello pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="5c165-285">Para transações de qualquer número de bancos de dados no pool de hello, consulte [transações Elásticos](sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c165-285">For transactions any number of databases in hello pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
