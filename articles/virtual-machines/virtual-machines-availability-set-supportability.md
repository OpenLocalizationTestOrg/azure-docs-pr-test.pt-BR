---
title: "Capacidade de suporte de adição de VMs do Azure a um conjunto de disponibilidade existente | Microsoft Docs"
description: "Capacidade de suporte de adição de VMs do Azure a um conjunto de disponibilidade existente."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: 3ce9b8a79108cb9e57df14bcb3354cc637193233
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="supportability-of-adding-azure-vms-to-an-existing-availability-set"></a><span data-ttu-id="ccb5a-103">Capacidade de suporte de adição de VMs do Azure a um conjunto de disponibilidade existente</span><span class="sxs-lookup"><span data-stu-id="ccb5a-103">Supportability of adding Azure VMs to an existing availability set</span></span>

<span data-ttu-id="ccb5a-104">Ocasionalmente, você poderá encontrar limitações ao adicionar novas VMs (máquinas virtuais) a um conjunto de disponibilidade existente.</span><span class="sxs-lookup"><span data-stu-id="ccb5a-104">You may occasionally encounter limitations when you add new virtual machines (VMs) to an existing availability set.</span></span> <span data-ttu-id="ccb5a-105">O gráfico a seguir fornece detalhes sobre quais séries de VM podem ser combinadas no mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="ccb5a-105">The following chart details which VM series you can mix in the same availability set.</span></span>

<span data-ttu-id="ccb5a-106">Esta é a matriz de capacidade de suporte para combinação de diferentes tipos de VMs:</span><span class="sxs-lookup"><span data-stu-id="ccb5a-106">Here is the supportability matrix to mix different types of VMs:</span></span>

<span data-ttu-id="ccb5a-107">Série e conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="ccb5a-107">Series & Availability Set</span></span>|<span data-ttu-id="ccb5a-108">Segunda VM</span><span class="sxs-lookup"><span data-stu-id="ccb5a-108">Second VM</span></span>|<span data-ttu-id="ccb5a-109">O </span><span class="sxs-lookup"><span data-stu-id="ccb5a-109">A</span></span>|<span data-ttu-id="ccb5a-110">Av2</span><span class="sxs-lookup"><span data-stu-id="ccb5a-110">Av2</span></span>|<span data-ttu-id="ccb5a-111">D</span><span class="sxs-lookup"><span data-stu-id="ccb5a-111">D</span></span>|<span data-ttu-id="ccb5a-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="ccb5a-112">Dv2</span></span>|<span data-ttu-id="ccb5a-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="ccb5a-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="ccb5a-114">Primeira VM</span><span class="sxs-lookup"><span data-stu-id="ccb5a-114">First VM</span></span>|||||||
|<span data-ttu-id="ccb5a-115">O </span><span class="sxs-lookup"><span data-stu-id="ccb5a-115">A</span></span>||<span data-ttu-id="ccb5a-116">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-116">OK</span></span>|<span data-ttu-id="ccb5a-117">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-117">OK</span></span>|<span data-ttu-id="ccb5a-118">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-118">OK</span></span>|<span data-ttu-id="ccb5a-119">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-119">OK</span></span>|<span data-ttu-id="ccb5a-120">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-120">OK</span></span>|
|<span data-ttu-id="ccb5a-121">Av2</span><span class="sxs-lookup"><span data-stu-id="ccb5a-121">Av2</span></span>||<span data-ttu-id="ccb5a-122">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-122">OK</span></span>|<span data-ttu-id="ccb5a-123">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-123">OK</span></span>|<span data-ttu-id="ccb5a-124">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-124">OK</span></span>|<span data-ttu-id="ccb5a-125">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-125">OK</span></span>|<span data-ttu-id="ccb5a-126">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-126">OK</span></span>|
|<span data-ttu-id="ccb5a-127">D</span><span class="sxs-lookup"><span data-stu-id="ccb5a-127">D</span></span>||<span data-ttu-id="ccb5a-128">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-128">OK</span></span>|<span data-ttu-id="ccb5a-129">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-129">OK</span></span>|<span data-ttu-id="ccb5a-130">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-130">OK</span></span>|<span data-ttu-id="ccb5a-131">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-131">OK</span></span>|<span data-ttu-id="ccb5a-132">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-132">OK</span></span>|
|<span data-ttu-id="ccb5a-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="ccb5a-133">Dv2</span></span>||<span data-ttu-id="ccb5a-134">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-134">OK</span></span>|<span data-ttu-id="ccb5a-135">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-135">OK</span></span>|<span data-ttu-id="ccb5a-136">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-136">OK</span></span>|<span data-ttu-id="ccb5a-137">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-137">OK</span></span>|<span data-ttu-id="ccb5a-138">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-138">OK</span></span>|
|<span data-ttu-id="ccb5a-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="ccb5a-139">Dv3</span></span>||<span data-ttu-id="ccb5a-140">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-140">OK</span></span>|<span data-ttu-id="ccb5a-141">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-141">OK</span></span>|<span data-ttu-id="ccb5a-142">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-142">OK</span></span>|<span data-ttu-id="ccb5a-143">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-143">OK</span></span>|<span data-ttu-id="ccb5a-144">OK</span><span class="sxs-lookup"><span data-stu-id="ccb5a-144">OK</span></span>|

<span data-ttu-id="ccb5a-145">Todas as outras séries não podem estar no mesmo conjunto de disponibilidade porque exigem um hardware específico.</span><span class="sxs-lookup"><span data-stu-id="ccb5a-145">All other series could not be in the same availability set because they require a specific hardware.</span></span>