---
title: "aaaSQL visão geral dos grupos de disponibilidade de servidor - máquinas virtuais do Azure - | Microsoft Docs"
description: "Este artigo apresenta os Grupos de Disponibilidade do SQL Server em máquinas virtuais do Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="edb43-103">Introdução aos grupos de disponibilidade do AlwaysOn do SQL Server em máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="edb43-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="edb43-104">Este artigo apresenta os grupos de disponibilidade do SQL Server em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="edb43-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="edb43-105">Sempre em grupos de disponibilidade em máquinas virtuais do Azure são semelhantes tooAlways grupos de disponibilidade no local.</span><span class="sxs-lookup"><span data-stu-id="edb43-105">Always On availability groups on Azure Virtual Machines are similar tooAlways On availability groups on premises.</span></span> <span data-ttu-id="edb43-106">Para obter mais informações, confira [Grupos de disponibilidade Always On (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="edb43-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="edb43-107">diagrama de saudação ilustra as partes de saudação de um grupo de disponibilidade de servidor do SQL de conclusão em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="edb43-107">hello diagram illustrates hello parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="edb43-109">Olá diferença chave para um grupo de disponibilidade em máquinas virtuais do Azure é que Olá máquinas virtuais do Azure, exigem um [balanceador de carga](../../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="edb43-109">hello key difference for an Availability Group in Azure Virtual Machines is that hello Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="edb43-110">o balanceador de carga Olá contém endereços IP Olá para o ouvinte do grupo de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="edb43-110">hello load balancer holds hello IP addresses for hello availability group listener.</span></span> <span data-ttu-id="edb43-111">Se você tiver mais de um grupo de disponibilidade cada grupo exige um ouvinte.</span><span class="sxs-lookup"><span data-stu-id="edb43-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="edb43-112">Um balanceador de carga pode dar suporte a vários ouvintes.</span><span class="sxs-lookup"><span data-stu-id="edb43-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="edb43-113">Quando você estiver pronto toobuild um aroup de disponibilidade do SQL Server em máquinas virtuais do Azure, consulte os tutoriais de toothese.</span><span class="sxs-lookup"><span data-stu-id="edb43-113">When you are ready toobuild a SQL Server availability aroup on Azure Virtual Machines, refer toothese tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="edb43-114">Criar automaticamente um grupo de disponibilidade de um modelo</span><span class="sxs-lookup"><span data-stu-id="edb43-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="edb43-115">Configurar automaticamente o grupo de disponibilidade Always On na VM do Azure - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="edb43-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="edb43-116">Criar manualmente um grupo de disponibilidade no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="edb43-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="edb43-117">Você também pode criar máquinas virtuais de saudação sem modelo hello.</span><span class="sxs-lookup"><span data-stu-id="edb43-117">You can also create hello virtual machines yourself without hello template.</span></span> <span data-ttu-id="edb43-118">Primeiro, complete os pré-requisitos de saudação e criar grupo de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="edb43-118">First, complete hello prerequisites, then create hello availability group.</span></span> <span data-ttu-id="edb43-119">Consulte Olá seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="edb43-119">See hello following topics:</span></span> 

- [<span data-ttu-id="edb43-120">Configurar os pré-requisitos para grupos de disponibilidade do SQL Server Always On nas máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="edb43-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="edb43-121">Criar grupo de disponibilidade AlwaysOn tooimprove disponibilidade e recuperação de desastres</span><span class="sxs-lookup"><span data-stu-id="edb43-121">Create Always On Availability Group tooimprove availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="edb43-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="edb43-122">Next steps</span></span>

<span data-ttu-id="edb43-123">[Configurar um SQL Server sempre no grupo de disponibilidade em máquinas virtuais do Azure em diferentes regiões](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="edb43-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
