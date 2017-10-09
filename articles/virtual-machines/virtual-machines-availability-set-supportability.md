---
title: aaaSupportability de Adicionar conjunto de disponibilidade existente tooan VMs do Azure | Microsoft Docs
description: "Suporte de adição de VMs do Azure tooan conjunto de disponibilidade existente."
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
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a><span data-ttu-id="bfbf6-103">Suporte de adição de VMs do Azure tooan conjunto de disponibilidade existente</span><span class="sxs-lookup"><span data-stu-id="bfbf6-103">Supportability of adding Azure VMs tooan existing availability set</span></span>

<span data-ttu-id="bfbf6-104">Ocasionalmente, você poderá encontrar limitações quando você adicionar novas máquinas virtuais (VMs) tooan conjunto de disponibilidade existente.</span><span class="sxs-lookup"><span data-stu-id="bfbf6-104">You may occasionally encounter limitations when you add new virtual machines (VMs) tooan existing availability set.</span></span> <span data-ttu-id="bfbf6-105">Olá que série VM, você pode combinar em Olá mesmo conjunto de disponibilidade de detalhes de gráfico a seguir.</span><span class="sxs-lookup"><span data-stu-id="bfbf6-105">hello following chart details which VM series you can mix in hello same availability set.</span></span>

<span data-ttu-id="bfbf6-106">Aqui está o hello suporte matriz toomix diferentes tipos de máquinas virtuais:</span><span class="sxs-lookup"><span data-stu-id="bfbf6-106">Here is hello supportability matrix toomix different types of VMs:</span></span>

<span data-ttu-id="bfbf6-107">Série e conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="bfbf6-107">Series & Availability Set</span></span>|<span data-ttu-id="bfbf6-108">Segunda VM</span><span class="sxs-lookup"><span data-stu-id="bfbf6-108">Second VM</span></span>|<span data-ttu-id="bfbf6-109">O </span><span class="sxs-lookup"><span data-stu-id="bfbf6-109">A</span></span>|<span data-ttu-id="bfbf6-110">Av2</span><span class="sxs-lookup"><span data-stu-id="bfbf6-110">Av2</span></span>|<span data-ttu-id="bfbf6-111">D</span><span class="sxs-lookup"><span data-stu-id="bfbf6-111">D</span></span>|<span data-ttu-id="bfbf6-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="bfbf6-112">Dv2</span></span>|<span data-ttu-id="bfbf6-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="bfbf6-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="bfbf6-114">Primeira VM</span><span class="sxs-lookup"><span data-stu-id="bfbf6-114">First VM</span></span>|||||||
|<span data-ttu-id="bfbf6-115">O </span><span class="sxs-lookup"><span data-stu-id="bfbf6-115">A</span></span>||<span data-ttu-id="bfbf6-116">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-116">OK</span></span>|<span data-ttu-id="bfbf6-117">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-117">OK</span></span>|<span data-ttu-id="bfbf6-118">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-118">OK</span></span>|<span data-ttu-id="bfbf6-119">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-119">OK</span></span>|<span data-ttu-id="bfbf6-120">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-120">OK</span></span>|
|<span data-ttu-id="bfbf6-121">Av2</span><span class="sxs-lookup"><span data-stu-id="bfbf6-121">Av2</span></span>||<span data-ttu-id="bfbf6-122">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-122">OK</span></span>|<span data-ttu-id="bfbf6-123">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-123">OK</span></span>|<span data-ttu-id="bfbf6-124">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-124">OK</span></span>|<span data-ttu-id="bfbf6-125">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-125">OK</span></span>|<span data-ttu-id="bfbf6-126">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-126">OK</span></span>|
|<span data-ttu-id="bfbf6-127">D</span><span class="sxs-lookup"><span data-stu-id="bfbf6-127">D</span></span>||<span data-ttu-id="bfbf6-128">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-128">OK</span></span>|<span data-ttu-id="bfbf6-129">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-129">OK</span></span>|<span data-ttu-id="bfbf6-130">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-130">OK</span></span>|<span data-ttu-id="bfbf6-131">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-131">OK</span></span>|<span data-ttu-id="bfbf6-132">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-132">OK</span></span>|
|<span data-ttu-id="bfbf6-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="bfbf6-133">Dv2</span></span>||<span data-ttu-id="bfbf6-134">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-134">OK</span></span>|<span data-ttu-id="bfbf6-135">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-135">OK</span></span>|<span data-ttu-id="bfbf6-136">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-136">OK</span></span>|<span data-ttu-id="bfbf6-137">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-137">OK</span></span>|<span data-ttu-id="bfbf6-138">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-138">OK</span></span>|
|<span data-ttu-id="bfbf6-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="bfbf6-139">Dv3</span></span>||<span data-ttu-id="bfbf6-140">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-140">OK</span></span>|<span data-ttu-id="bfbf6-141">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-141">OK</span></span>|<span data-ttu-id="bfbf6-142">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-142">OK</span></span>|<span data-ttu-id="bfbf6-143">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-143">OK</span></span>|<span data-ttu-id="bfbf6-144">OK</span><span class="sxs-lookup"><span data-stu-id="bfbf6-144">OK</span></span>|

<span data-ttu-id="bfbf6-145">Todas as outras séries não podem estar em Olá conjunto de disponibilidade mesmo porque eles exigem um hardware específico.</span><span class="sxs-lookup"><span data-stu-id="bfbf6-145">All other series could not be in hello same availability set because they require a specific hardware.</span></span>
