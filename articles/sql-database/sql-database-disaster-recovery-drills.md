---
title: "Análises de recuperação de desastre do Banco de Dados SQL | Microsoft Docs"
description: "Obtenha orientação e as práticas recomendadas para usar o Banco de dados SQL do Azure para executar as análises de recuperação de desastres para ajudar a manter seus aplicativos comerciais importantes resilientes a falhas e interrupções."
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
ms.openlocfilehash: 1b1d65a41a794a566287dcffe3581ac58e2a965f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="802c6-103">Executar análise de recuperação de desastres</span><span class="sxs-lookup"><span data-stu-id="802c6-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="802c6-104">Recomenda-se a validação periódica da preparação do aplicativo para o fluxo de trabalho de recuperação.</span><span class="sxs-lookup"><span data-stu-id="802c6-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="802c6-105">Consideramos uma boa prática de engenharia a verificação do comportamento do aplicativo e as implicações de perda de dados e/ou interrupção que envolvem o failover.</span><span class="sxs-lookup"><span data-stu-id="802c6-105">Verifying the application behavior and implications of data loss and/or the disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="802c6-106">Isso também é uma exigência da maioria dos padrões do setor, como parte da certificação de continuidade dos negócios.</span><span class="sxs-lookup"><span data-stu-id="802c6-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="802c6-107">A execução de uma análise de recuperação de desastres é composta por:</span><span class="sxs-lookup"><span data-stu-id="802c6-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="802c6-108">Simulação da interrupção da camada de dados</span><span class="sxs-lookup"><span data-stu-id="802c6-108">Simulating data tier outage</span></span>
* <span data-ttu-id="802c6-109">Recuperando</span><span class="sxs-lookup"><span data-stu-id="802c6-109">Recovering</span></span>
* <span data-ttu-id="802c6-110">Validação da integridade do aplicativo após a recuperação</span><span class="sxs-lookup"><span data-stu-id="802c6-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="802c6-111">Dependendo de como você [criou seu aplicativo para continuidade de negócios](sql-database-business-continuity.md), o fluxo de trabalho para executar a análise pode variar.</span><span class="sxs-lookup"><span data-stu-id="802c6-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), the workflow to execute the drill can vary.</span></span> <span data-ttu-id="802c6-112">A seguir, descrevemos as práticas recomendadas para condução de uma análise de recuperação de desastres no contexto do Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="802c6-112">Below we describe the best practices conducting a disaster recovery drill in the context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="802c6-113">Restauração geográfica</span><span class="sxs-lookup"><span data-stu-id="802c6-113">Geo-restore</span></span>
<span data-ttu-id="802c6-114">Para evitar a possível perda de dados durante a realização de uma análise de recuperação de desastres, recomendamos a execução da análise usando um ambiente de teste criando uma cópia do ambiente de produção e usando-a para verificar o fluxo de trabalho de failover do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="802c6-114">To prevent the potential data loss when conducting a disaster recovery drill, we recommend performing the drill using a test environment by creating a copy of the production environment and using it to verify the application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="802c6-115">Simulação de interrupção</span><span class="sxs-lookup"><span data-stu-id="802c6-115">Outage simulation</span></span>
<span data-ttu-id="802c6-116">Para simular a interrupção, você pode excluir ou renomear o banco de dados de origem.</span><span class="sxs-lookup"><span data-stu-id="802c6-116">To simulate the outage, you can delete or rename the source database.</span></span> <span data-ttu-id="802c6-117">Isso causará falha de conectividade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="802c6-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="802c6-118">Recuperação</span><span class="sxs-lookup"><span data-stu-id="802c6-118">Recovery</span></span>
* <span data-ttu-id="802c6-119">Execute a restauração geográfica do banco de dados em um servidor diferente, como descrito [aqui](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="802c6-119">Perform the geo-restore of the database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="802c6-120">Altere a configuração de aplicativo para se conectar aos bancos de dados recuperados e siga o guia [Configurar um banco de dados após a recuperação](sql-database-disaster-recovery.md) para concluir a recuperação.</span><span class="sxs-lookup"><span data-stu-id="802c6-120">Change the application configuration to connect to the recovered database and follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="802c6-121">Validação</span><span class="sxs-lookup"><span data-stu-id="802c6-121">Validation</span></span>
* <span data-ttu-id="802c6-122">Conclua a análise verificando a integridade do aplicativo após a recuperação (incluindo cadeias de conexão, logons, teste de funcionalidade básica ou outras validações que fazem parte dos procedimentos de aprovações padrão do aplicativo).</span><span class="sxs-lookup"><span data-stu-id="802c6-122">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="802c6-123">Replicação geográfica</span><span class="sxs-lookup"><span data-stu-id="802c6-123">Geo-replication</span></span>
<span data-ttu-id="802c6-124">Para um banco de dados protegido usando a replicação geográfica, o exercício de análise envolverá failover planejado para o banco de dados secundário.</span><span class="sxs-lookup"><span data-stu-id="802c6-124">For a database that is protected using geo-replication the drill exercise involves planned failover to the secondary database.</span></span> <span data-ttu-id="802c6-125">O failover planejado garante que os bancos de dados primário e secundário permaneçam em sincronia quando as funções são alternadas.</span><span class="sxs-lookup"><span data-stu-id="802c6-125">The planned failover ensures that the primary and the secondary databases remain in sync when the roles are switched.</span></span> <span data-ttu-id="802c6-126">Ao contrário de failover não planejado, essa operação não resultará na perda de dados, assim, a análise pode ser executada no ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="802c6-126">Unlike the unplanned failover, this operation does not result in data loss, so the drill can be performed in the production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="802c6-127">Simulação de interrupção</span><span class="sxs-lookup"><span data-stu-id="802c6-127">Outage simulation</span></span>
<span data-ttu-id="802c6-128">Para simular a interrupção, você pode desabilitar o aplicativo Web ou a máquina virtual conectada ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="802c6-128">To simulate the outage, you can disable the web application or virtual machine connected to the database.</span></span> <span data-ttu-id="802c6-129">Isso resulta em falhas de conectividade para os clientes da web.</span><span class="sxs-lookup"><span data-stu-id="802c6-129">This results in the connectivity failures for the web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="802c6-130">Recuperação</span><span class="sxs-lookup"><span data-stu-id="802c6-130">Recovery</span></span>
* <span data-ttu-id="802c6-131">Certifique-se de que a configuração do aplicativo na região de DR aponta para o secundário anterior que se torna o novo primário totalmente acessível.</span><span class="sxs-lookup"><span data-stu-id="802c6-131">Make sure the application configuration in the DR region points to the former secondary which becomes the fully accessible new primary.</span></span>
* <span data-ttu-id="802c6-132">Execute [failover planejado](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) para tornar o banco de dados secundário um novo primário</span><span class="sxs-lookup"><span data-stu-id="802c6-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) to make the secondary database a new primary</span></span>
* <span data-ttu-id="802c6-133">Siga o guia [Configurar um banco de dados após a recuperação](sql-database-disaster-recovery.md) para concluir a recuperação.</span><span class="sxs-lookup"><span data-stu-id="802c6-133">Follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="802c6-134">Validação</span><span class="sxs-lookup"><span data-stu-id="802c6-134">Validation</span></span>
* <span data-ttu-id="802c6-135">Conclua a análise verificando a integridade do aplicativo após a recuperação (incluindo cadeias de conexão, logons, teste de funcionalidade básica ou outras validações que fazem parte dos procedimentos de aprovações padrão do aplicativo).</span><span class="sxs-lookup"><span data-stu-id="802c6-135">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="802c6-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="802c6-136">Next steps</span></span>
* <span data-ttu-id="802c6-137">Para saber mais sobre cenários de continuidade dos negócios, consulte [Cenários de continuidade](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="802c6-137">To learn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="802c6-138">Para saber mais sobre backups automatizados do Banco de Dados SQL do Azure, consulte [Backups automatizados do Banco de Dados SQL](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="802c6-138">To learn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="802c6-139">Para saber mais sobre como usar backups automatizados de recuperação, veja [Restaurar um banco de dados de backups iniciados pelo serviço](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="802c6-139">To learn about using automated backups for recovery, see [restore a database from the service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="802c6-140">Para saber mais sobre opções de recuperação mais rápidas, confira [replicação geográfica ativa](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="802c6-140">To learn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
