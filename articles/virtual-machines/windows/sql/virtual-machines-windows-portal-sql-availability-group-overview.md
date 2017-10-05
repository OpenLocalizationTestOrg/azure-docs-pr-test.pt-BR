---
title: "Grupos de Disponibilidade do SQL Server - máquinas virtuais do Azure - visão geral | Microsoft Docs"
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
ms.openlocfilehash: 2cbb9ff3b2d13996b1b8dc64aa833807c264c877
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="36bf1-103">Introdução aos grupos de disponibilidade do AlwaysOn do SQL Server em máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="36bf1-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="36bf1-104">Este artigo apresenta os grupos de disponibilidade do SQL Server em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="36bf1-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="36bf1-105">Os grupos de disponibilidade Always On em máquinas virtuais do Azure são semelhantes aos grupos de disponibilidade Always On locais.</span><span class="sxs-lookup"><span data-stu-id="36bf1-105">Always On availability groups on Azure Virtual Machines are similar to Always On availability groups on premises.</span></span> <span data-ttu-id="36bf1-106">Para obter mais informações, confira [Grupos de Disponibilidade AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="36bf1-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="36bf1-107">O diagrama ilustra as partes de um Grupo de Disponibilidade do SQL Server completo em Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="36bf1-107">The diagram illustrates the parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="36bf1-109">A principal diferença para um Grupo de Disponibilidade em máquinas virtuais do Azure é que as máquinas virtuais do Azure exigem um [balanceador de carga](../../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="36bf1-109">The key difference for an Availability Group in Azure Virtual Machines is that the Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="36bf1-110">O balanceador de carga contém o endereço IP do ouvinte do grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="36bf1-110">The load balancer holds the IP addresses for the availability group listener.</span></span> <span data-ttu-id="36bf1-111">Se você tiver mais de um grupo de disponibilidade cada grupo exige um ouvinte.</span><span class="sxs-lookup"><span data-stu-id="36bf1-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="36bf1-112">Um balanceador de carga pode dar suporte a vários ouvintes.</span><span class="sxs-lookup"><span data-stu-id="36bf1-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="36bf1-113">Quando estiver pronto para criar um grupo de disponibilidade do SQL Server em máquinas virtuais do Azure, consulte estes tutoriais.</span><span class="sxs-lookup"><span data-stu-id="36bf1-113">When you are ready to build a SQL Server availability aroup on Azure Virtual Machines, refer to these tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="36bf1-114">Criar automaticamente um grupo de disponibilidade de um modelo</span><span class="sxs-lookup"><span data-stu-id="36bf1-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="36bf1-115">Configurar automaticamente o grupo de disponibilidade Always On na VM do Azure - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="36bf1-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="36bf1-116">Criar manualmente um grupo de disponibilidade no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="36bf1-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="36bf1-117">Você também pode criar as máquinas virtuais sem o modelo.</span><span class="sxs-lookup"><span data-stu-id="36bf1-117">You can also create the virtual machines yourself without the template.</span></span> <span data-ttu-id="36bf1-118">Primeiro, complete os pré-requisitos e criar o grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="36bf1-118">First, complete the prerequisites, then create the availability group.</span></span> <span data-ttu-id="36bf1-119">Confira os seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="36bf1-119">See the following topics:</span></span> 

- [<span data-ttu-id="36bf1-120">Configurar os pré-requisitos para grupos de disponibilidade do SQL Server Always On nas máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="36bf1-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="36bf1-121">Criar Grupo de Disponibilidade Always On para melhorar a disponibilidade e a recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="36bf1-121">Create Always On Availability Group to improve availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="36bf1-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="36bf1-122">Next steps</span></span>

<span data-ttu-id="36bf1-123">[Configurar um SQL Server sempre no grupo de disponibilidade em máquinas virtuais do Azure em diferentes regiões](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="36bf1-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
