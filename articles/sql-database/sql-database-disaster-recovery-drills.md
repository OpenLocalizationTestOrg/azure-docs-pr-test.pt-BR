---
title: "banco de dados de recuperação de desastre do aaaSQL | Microsoft Docs"
description: "Saiba mais diretrizes e práticas recomendadas para usar manter toohelp detalhada de recuperação do banco de dados do Azure SQL tooperform desastres sua missão essenciais aos negócios aplicativos resilientes toofailures e interrupções."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="7b153-103">Executar análise de recuperação de desastres</span><span class="sxs-lookup"><span data-stu-id="7b153-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="7b153-104">Recomenda-se a validação periódica da preparação do aplicativo para o fluxo de trabalho de recuperação.</span><span class="sxs-lookup"><span data-stu-id="7b153-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="7b153-105">Verificando o comportamento do aplicativo hello e implicações de interrupção de perda de e/ou saudação de dados que o failover envolve é uma boa prática de engenharia.</span><span class="sxs-lookup"><span data-stu-id="7b153-105">Verifying hello application behavior and implications of data loss and/or hello disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="7b153-106">Isso também é uma exigência da maioria dos padrões do setor, como parte da certificação de continuidade dos negócios.</span><span class="sxs-lookup"><span data-stu-id="7b153-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="7b153-107">A execução de uma análise de recuperação de desastres é composta por:</span><span class="sxs-lookup"><span data-stu-id="7b153-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="7b153-108">Simulação da interrupção da camada de dados</span><span class="sxs-lookup"><span data-stu-id="7b153-108">Simulating data tier outage</span></span>
* <span data-ttu-id="7b153-109">Recuperando</span><span class="sxs-lookup"><span data-stu-id="7b153-109">Recovering</span></span>
* <span data-ttu-id="7b153-110">Validação da integridade do aplicativo após a recuperação</span><span class="sxs-lookup"><span data-stu-id="7b153-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="7b153-111">Dependendo de como você [seu aplicativo para continuidade de negócios](sql-database-business-continuity.md), análise de Olá Olá fluxo de trabalho tooexecute pode variar.</span><span class="sxs-lookup"><span data-stu-id="7b153-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), hello workflow tooexecute hello drill can vary.</span></span> <span data-ttu-id="7b153-112">Abaixo descrevemos práticas recomendadas de saudação realizando uma simulação de recuperação de desastres no contexto de saudação do banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7b153-112">Below we describe hello best practices conducting a disaster recovery drill in hello context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="7b153-113">Restauração geográfica</span><span class="sxs-lookup"><span data-stu-id="7b153-113">Geo-restore</span></span>
<span data-ttu-id="7b153-114">tooprevent Olá potencial perda de dados ao realizar uma simulação de recuperação de desastres, é recomendável executar análise hello usando um ambiente de teste ao criar uma cópia do ambiente de produção de hello e usá-lo fluxo de trabalho de failover do aplicativo do tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="7b153-114">tooprevent hello potential data loss when conducting a disaster recovery drill, we recommend performing hello drill using a test environment by creating a copy of hello production environment and using it tooverify hello application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="7b153-115">Simulação de interrupção</span><span class="sxs-lookup"><span data-stu-id="7b153-115">Outage simulation</span></span>
<span data-ttu-id="7b153-116">toosimulate Olá interrupção, você pode excluir ou renomear o banco de dados de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b153-116">toosimulate hello outage, you can delete or rename hello source database.</span></span> <span data-ttu-id="7b153-117">Isso causará falha de conectividade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7b153-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="7b153-118">Recuperação</span><span class="sxs-lookup"><span data-stu-id="7b153-118">Recovery</span></span>
* <span data-ttu-id="7b153-119">Executar restauração geográfica de saudação do banco de dados de saudação em um servidor diferente, conforme descrito [aqui](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="7b153-119">Perform hello geo-restore of hello database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="7b153-120">Alteração Olá aplicativo configuração tooconnect toohello recuperado banco de dados e siga Olá [configurar um banco de dados após a recuperação](sql-database-disaster-recovery.md) guia de recuperação de saudação toocomplete.</span><span class="sxs-lookup"><span data-stu-id="7b153-120">Change hello application configuration tooconnect toohello recovered database and follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="7b153-121">Validação</span><span class="sxs-lookup"><span data-stu-id="7b153-121">Validation</span></span>
* <span data-ttu-id="7b153-122">Olá completa drill verificando recuperação Olá aplicativos integridade post (incluindo cadeias de caracteres de conexão, logons, teste de funcionalidade básica ou outra parte de validações de procedimentos de aprovações de aplicativo padrão).</span><span class="sxs-lookup"><span data-stu-id="7b153-122">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="7b153-123">Replicação geográfica</span><span class="sxs-lookup"><span data-stu-id="7b153-123">Geo-replication</span></span>
<span data-ttu-id="7b153-124">Para um banco de dados que é protegido usando a análise de saudação de replicação geográfica exercício envolve toohello failover planejado banco de dados secundário.</span><span class="sxs-lookup"><span data-stu-id="7b153-124">For a database that is protected using geo-replication hello drill exercise involves planned failover toohello secondary database.</span></span> <span data-ttu-id="7b153-125">Olá failover planejado garante que hello primário e bancos de dados secundários Olá sincronizados quando a troca de funções hello.</span><span class="sxs-lookup"><span data-stu-id="7b153-125">hello planned failover ensures that hello primary and hello secondary databases remain in sync when hello roles are switched.</span></span> <span data-ttu-id="7b153-126">Ao contrário de Olá failover não planejado, esta operação não resulta na perda de dados, assim drill Olá pode ser executada no ambiente de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="7b153-126">Unlike hello unplanned failover, this operation does not result in data loss, so hello drill can be performed in hello production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="7b153-127">Simulação de interrupção</span><span class="sxs-lookup"><span data-stu-id="7b153-127">Outage simulation</span></span>
<span data-ttu-id="7b153-128">interrupção de saudação toosimulate, você pode desabilitar o aplicativo hello ou banco de dados de toohello de máquina virtual conectada.</span><span class="sxs-lookup"><span data-stu-id="7b153-128">toosimulate hello outage, you can disable hello web application or virtual machine connected toohello database.</span></span> <span data-ttu-id="7b153-129">Isso resulta em falhas de conectividade Olá para clientes do hello da web.</span><span class="sxs-lookup"><span data-stu-id="7b153-129">This results in hello connectivity failures for hello web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="7b153-130">Recuperação</span><span class="sxs-lookup"><span data-stu-id="7b153-130">Recovery</span></span>
* <span data-ttu-id="7b153-131">Fazer se a configuração aplicativo hello em Olá DR região pontos toohello antiga secundária que se torna Olá totalmente acessível novo primário.</span><span class="sxs-lookup"><span data-stu-id="7b153-131">Make sure hello application configuration in hello DR region points toohello former secondary which becomes hello fully accessible new primary.</span></span>
* <span data-ttu-id="7b153-132">Executar [failover planejado](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake Olá secundário um novo primário do banco de dados</span><span class="sxs-lookup"><span data-stu-id="7b153-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake hello secondary database a new primary</span></span>
* <span data-ttu-id="7b153-133">Siga Olá [configurar um banco de dados após a recuperação](sql-database-disaster-recovery.md) guia de recuperação de saudação toocomplete.</span><span class="sxs-lookup"><span data-stu-id="7b153-133">Follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="7b153-134">Validação</span><span class="sxs-lookup"><span data-stu-id="7b153-134">Validation</span></span>
* <span data-ttu-id="7b153-135">Olá completa drill verificando recuperação Olá aplicativos integridade post (incluindo cadeias de caracteres de conexão, logons, teste de funcionalidade básica ou outra parte de validações de procedimentos de aprovações de aplicativo padrão).</span><span class="sxs-lookup"><span data-stu-id="7b153-135">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b153-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7b153-136">Next steps</span></span>
* <span data-ttu-id="7b153-137">toolearn sobre cenários de continuidade de negócios, consulte [cenários de continuidade](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="7b153-137">toolearn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="7b153-138">toolearn sobre backups de banco de dados do SQL Azure automatizadas, consulte [backups automatizados de banco de dados SQL](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="7b153-138">toolearn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="7b153-139">toolearn sobre como usar backups automatizados para recuperação, consulte [restaurar um banco de dados de backups de iniciadas pelo serviço de saudação](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="7b153-139">toolearn about using automated backups for recovery, see [restore a database from hello service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="7b153-140">toolearn sobre as opções de recuperação mais rápidas, consulte [replicação geográfica ativa](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7b153-140">toolearn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
