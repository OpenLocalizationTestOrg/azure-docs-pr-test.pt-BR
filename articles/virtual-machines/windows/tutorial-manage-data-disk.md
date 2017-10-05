---
title: Gerenciar discos do Azure com o Azure PowerShell | Microsoft Docs
description: "Tutorial – Gerenciar discos do Azure com o Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 6f1bc9361745adc211f22416a7ba8ac1b8dc614e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="2e7a8-103">Gerenciar discos do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e7a8-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="2e7a8-104">Máquinas virtuais do Azure usam discos para armazenar o sistema operacional de VMs, aplicativos e dados.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-104">Azure virtual machines use disks to store the VMs operating system, applications, and data.</span></span> <span data-ttu-id="2e7a8-105">Ao criar uma VM, é importante escolher um tamanho de disco e a configuração apropriada para a carga de trabalho esperada.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-105">When creating a VM it is important to choose a disk size and configuration appropriate to the expected workload.</span></span> <span data-ttu-id="2e7a8-106">Este tutorial aborda a implantação e gerenciamento de discos de VM.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="2e7a8-107">Você saberá mais sobre:</span><span class="sxs-lookup"><span data-stu-id="2e7a8-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2e7a8-108">Discos de sistema operacional e discos temporários</span><span class="sxs-lookup"><span data-stu-id="2e7a8-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="2e7a8-109">Discos de dados</span><span class="sxs-lookup"><span data-stu-id="2e7a8-109">Data disks</span></span>
> * <span data-ttu-id="2e7a8-110">Discos Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="2e7a8-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="2e7a8-111">Desempenho do disco</span><span class="sxs-lookup"><span data-stu-id="2e7a8-111">Disk performance</span></span>
> * <span data-ttu-id="2e7a8-112">Anexar e preparar os discos de dados</span><span class="sxs-lookup"><span data-stu-id="2e7a8-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="2e7a8-113">Este tutorial requer o módulo do Azure PowerShell, versão 3.6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="2e7a8-114">Execute ` Get-Module -ListAvailable AzureRM` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="2e7a8-115">Se você precisa atualizar, consulte [Instalar o módulo do Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="2e7a8-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="2e7a8-116">Discos padrão do Azure</span><span class="sxs-lookup"><span data-stu-id="2e7a8-116">Default Azure disks</span></span>

<span data-ttu-id="2e7a8-117">Quando uma máquina virtual do Azure é criada, dois discos são automaticamente anexados à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-117">When an Azure virtual machine is created, two disks are automatically attached to the virtual machine.</span></span> 

<span data-ttu-id="2e7a8-118">**Disco do sistema operacional**: os discos do sistema operacional podem ser dimensionados para até 1 terabyte e hospedar o sistema operacional das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-118">**Operating system disk** - Operating system disks can be sized up to 1 terabyte, and hosts the VMs operating system.</span></span>  <span data-ttu-id="2e7a8-119">O disco do SO é atribuído à letra de unidade *c:* por padrão.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-119">The OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="2e7a8-120">A configuração de cache do disco do SO é otimizada para desempenho do SO.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-120">The disk caching configuration of the OS disk is optimized for OS performance.</span></span> <span data-ttu-id="2e7a8-121">O disco do SO **não deve** hospedar aplicativos nem dados.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-121">The OS disk **should not** host applications or data.</span></span> <span data-ttu-id="2e7a8-122">Para aplicativos e dados, use um disco de dados, que é detalhado posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="2e7a8-123">**Disco temporário**: discos temporários usam uma unidade de estado sólido localizada no mesmo host do Azure que a VM.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on the same Azure host as the VM.</span></span> <span data-ttu-id="2e7a8-124">Os discos temporários são altamente eficazes e podem ser usados para operações como o processamento de dados temporário.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="2e7a8-125">No entanto, se a VM for movida para um novo host, todos os dados armazenados em um disco temporário serão removidos.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-125">However, if the VM is moved to a new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="2e7a8-126">O tamanho do disco temporário é determinado pelo tamanho da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-126">The size of the temporary disk is determined by the VM size.</span></span> <span data-ttu-id="2e7a8-127">Os discos temporários são atribuídos à letra de unidade *d:* por padrão.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="2e7a8-128">Tamanhos do disco temporário</span><span class="sxs-lookup"><span data-stu-id="2e7a8-128">Temporary disk sizes</span></span>

| <span data-ttu-id="2e7a8-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="2e7a8-129">Type</span></span> | <span data-ttu-id="2e7a8-130">Tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="2e7a8-130">VM Size</span></span> | <span data-ttu-id="2e7a8-131">Tamanho máximo do disco temporário (GB)</span><span class="sxs-lookup"><span data-stu-id="2e7a8-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="2e7a8-132">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="2e7a8-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="2e7a8-133">Série A e D</span><span class="sxs-lookup"><span data-stu-id="2e7a8-133">A and D series</span></span> | <span data-ttu-id="2e7a8-134">800</span><span class="sxs-lookup"><span data-stu-id="2e7a8-134">800</span></span> |
| [<span data-ttu-id="2e7a8-135">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="2e7a8-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="2e7a8-136">Série F</span><span class="sxs-lookup"><span data-stu-id="2e7a8-136">F series</span></span> | <span data-ttu-id="2e7a8-137">800</span><span class="sxs-lookup"><span data-stu-id="2e7a8-137">800</span></span> |
| [<span data-ttu-id="2e7a8-138">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="2e7a8-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="2e7a8-139">Série D e G</span><span class="sxs-lookup"><span data-stu-id="2e7a8-139">D and G series</span></span> | <span data-ttu-id="2e7a8-140">6144</span><span class="sxs-lookup"><span data-stu-id="2e7a8-140">6144</span></span> |
| [<span data-ttu-id="2e7a8-141">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="2e7a8-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="2e7a8-142">Série L</span><span class="sxs-lookup"><span data-stu-id="2e7a8-142">L series</span></span> | <span data-ttu-id="2e7a8-143">5630</span><span class="sxs-lookup"><span data-stu-id="2e7a8-143">5630</span></span> |
| [<span data-ttu-id="2e7a8-144">GPU</span><span class="sxs-lookup"><span data-stu-id="2e7a8-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="2e7a8-145">Série N</span><span class="sxs-lookup"><span data-stu-id="2e7a8-145">N series</span></span> | <span data-ttu-id="2e7a8-146">1440</span><span class="sxs-lookup"><span data-stu-id="2e7a8-146">1440</span></span> |
| [<span data-ttu-id="2e7a8-147">Alto desempenho</span><span class="sxs-lookup"><span data-stu-id="2e7a8-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="2e7a8-148">Séries A e H</span><span class="sxs-lookup"><span data-stu-id="2e7a8-148">A and H series</span></span> | <span data-ttu-id="2e7a8-149">2000</span><span class="sxs-lookup"><span data-stu-id="2e7a8-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="2e7a8-150">Discos de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="2e7a8-150">Azure data disks</span></span>

<span data-ttu-id="2e7a8-151">Os discos de dados extras podem ser adicionados para instalação de aplicativos e armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="2e7a8-152">Os discos de dados devem ser usados em qualquer situação onde o armazenamento de dados durável e responsivo é desejado.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="2e7a8-153">Cada disco de dados tem uma capacidade máxima de 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="2e7a8-154">O tamanho da máquina virtual determina quantos discos de dados podem ser anexados a uma VM.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-154">The size of the virtual machine determines how many data disks can be attached to a VM.</span></span> <span data-ttu-id="2e7a8-155">Para cada núcleo da VM, podem ser anexados dois discos de dados.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="2e7a8-156">Máximo de discos de dados por VM</span><span class="sxs-lookup"><span data-stu-id="2e7a8-156">Max data disks per VM</span></span>

| <span data-ttu-id="2e7a8-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="2e7a8-157">Type</span></span> | <span data-ttu-id="2e7a8-158">Tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="2e7a8-158">VM Size</span></span> | <span data-ttu-id="2e7a8-159">Máximo de discos de dados por VM</span><span class="sxs-lookup"><span data-stu-id="2e7a8-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="2e7a8-160">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="2e7a8-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="2e7a8-161">Série A e D</span><span class="sxs-lookup"><span data-stu-id="2e7a8-161">A and D series</span></span> | <span data-ttu-id="2e7a8-162">32</span><span class="sxs-lookup"><span data-stu-id="2e7a8-162">32</span></span> |
| [<span data-ttu-id="2e7a8-163">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="2e7a8-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="2e7a8-164">Série F</span><span class="sxs-lookup"><span data-stu-id="2e7a8-164">F series</span></span> | <span data-ttu-id="2e7a8-165">32</span><span class="sxs-lookup"><span data-stu-id="2e7a8-165">32</span></span> |
| [<span data-ttu-id="2e7a8-166">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="2e7a8-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="2e7a8-167">Série D e G</span><span class="sxs-lookup"><span data-stu-id="2e7a8-167">D and G series</span></span> | <span data-ttu-id="2e7a8-168">64</span><span class="sxs-lookup"><span data-stu-id="2e7a8-168">64</span></span> |
| [<span data-ttu-id="2e7a8-169">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="2e7a8-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="2e7a8-170">Série L</span><span class="sxs-lookup"><span data-stu-id="2e7a8-170">L series</span></span> | <span data-ttu-id="2e7a8-171">64</span><span class="sxs-lookup"><span data-stu-id="2e7a8-171">64</span></span> |
| [<span data-ttu-id="2e7a8-172">GPU</span><span class="sxs-lookup"><span data-stu-id="2e7a8-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="2e7a8-173">Série N</span><span class="sxs-lookup"><span data-stu-id="2e7a8-173">N series</span></span> | <span data-ttu-id="2e7a8-174">48</span><span class="sxs-lookup"><span data-stu-id="2e7a8-174">48</span></span> |
| [<span data-ttu-id="2e7a8-175">Alto desempenho</span><span class="sxs-lookup"><span data-stu-id="2e7a8-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="2e7a8-176">Série A e H</span><span class="sxs-lookup"><span data-stu-id="2e7a8-176">A and H series</span></span> | <span data-ttu-id="2e7a8-177">32</span><span class="sxs-lookup"><span data-stu-id="2e7a8-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="2e7a8-178">Tipos de disco da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2e7a8-178">VM disk types</span></span>

<span data-ttu-id="2e7a8-179">O Azure fornece dois tipos de disco.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="2e7a8-180">Disco Standard</span><span class="sxs-lookup"><span data-stu-id="2e7a8-180">Standard disk</span></span>

<span data-ttu-id="2e7a8-181">Armazenamento padrão é apoiado por HDDs e oferece armazenamento econômico e eficaz.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="2e7a8-182">Os discos Standard são ideais para uma carga de trabalho econômica de desenvolvimento e teste.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="2e7a8-183">Disco Premium</span><span class="sxs-lookup"><span data-stu-id="2e7a8-183">Premium disk</span></span>

<span data-ttu-id="2e7a8-184">Os discos Premium são apoiados por disco de baixa latência e alto desempenho baseado em SSD.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="2e7a8-185">Perfeitos para VMs que executam carga de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="2e7a8-186">O Armazenamento Premium dá suporte às VMs das séries DS, DSv2, GS e FS.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="2e7a8-187">Os discos Premium são apresentados em três tipos (P10, P20 e P30), o tamanho do disco determina o tipo de disco.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-187">Premium disks come in three types (P10, P20, P30), the size of the disk determines the disk type.</span></span> <span data-ttu-id="2e7a8-188">Na seleção do tamanho de um disco, o valor é arredondado para o próximo tipo.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-188">When selecting, a disk size the value is rounded up to the next type.</span></span> <span data-ttu-id="2e7a8-189">Por exemplo, se o tamanho for inferior a 128 GB, o tipo de disco será P10, entre 129 e 512, será P20 e acima de 512, será P30.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-189">For example, if the size is below 128 GB the disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="2e7a8-190">Desempenho do disco Premium</span><span class="sxs-lookup"><span data-stu-id="2e7a8-190">Premium disk performance</span></span>

|<span data-ttu-id="2e7a8-191">Tipo de disco de armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="2e7a8-191">Premium storage disk type</span></span> | <span data-ttu-id="2e7a8-192">P10</span><span class="sxs-lookup"><span data-stu-id="2e7a8-192">P10</span></span> | <span data-ttu-id="2e7a8-193">P20</span><span class="sxs-lookup"><span data-stu-id="2e7a8-193">P20</span></span> | <span data-ttu-id="2e7a8-194">P30</span><span class="sxs-lookup"><span data-stu-id="2e7a8-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2e7a8-195">Tamanho do disco (arredondado)</span><span class="sxs-lookup"><span data-stu-id="2e7a8-195">Disk size (round up)</span></span> | <span data-ttu-id="2e7a8-196">128 GB</span><span class="sxs-lookup"><span data-stu-id="2e7a8-196">128 GB</span></span> | <span data-ttu-id="2e7a8-197">512 GB</span><span class="sxs-lookup"><span data-stu-id="2e7a8-197">512 GB</span></span> | <span data-ttu-id="2e7a8-198">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="2e7a8-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="2e7a8-199">IOPS por disco</span><span class="sxs-lookup"><span data-stu-id="2e7a8-199">IOPS per disk</span></span> | <span data-ttu-id="2e7a8-200">500</span><span class="sxs-lookup"><span data-stu-id="2e7a8-200">500</span></span> | <span data-ttu-id="2e7a8-201">2.300</span><span class="sxs-lookup"><span data-stu-id="2e7a8-201">2,300</span></span> | <span data-ttu-id="2e7a8-202">5.000</span><span class="sxs-lookup"><span data-stu-id="2e7a8-202">5,000</span></span> |
<span data-ttu-id="2e7a8-203">Taxa de transferência por disco</span><span class="sxs-lookup"><span data-stu-id="2e7a8-203">Throughput per disk</span></span> | <span data-ttu-id="2e7a8-204">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="2e7a8-204">100 MB/s</span></span> | <span data-ttu-id="2e7a8-205">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="2e7a8-205">150 MB/s</span></span> | <span data-ttu-id="2e7a8-206">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="2e7a8-206">200 MB/s</span></span> |

<span data-ttu-id="2e7a8-207">Embora a tabela acima identifique a IOPS máxima por disco, um nível mais alto de desempenho pode ser obtido com a distribuição de vários discos de dados.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-207">While the above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="2e7a8-208">Por exemplo, 64 discos de dados podem ser anexados à VM Standard_GS5.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-208">For instance, 64 data disks can be attached to Standard_GS5 VM.</span></span> <span data-ttu-id="2e7a8-209">Se cada um desses discos for dimensionado como um P30, será possível chegar a um máximo de 80.000 IOPS.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="2e7a8-210">Para obter informações detalhadas sobre o máximo de IOPS por VM, confira [Tamanhos da VM Linux](./sizes.md).</span><span class="sxs-lookup"><span data-stu-id="2e7a8-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="2e7a8-211">Criar e anexar discos</span><span class="sxs-lookup"><span data-stu-id="2e7a8-211">Create and attach disks</span></span>

<span data-ttu-id="2e7a8-212">Para concluir o exemplo neste tutorial, você deverá ter uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-212">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="2e7a8-213">Se necessário, este [exemplo de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) pode criar uma para você.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="2e7a8-214">Ao trabalhar com este tutorial, substitua o grupo de recursos e os nomes de VM onde for necessário.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-214">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

<span data-ttu-id="2e7a8-215">Crie a configuração inicial com [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="2e7a8-215">Create the initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="2e7a8-216">O exemplo a seguir configura um disco com tamanho de 128 gigabytes.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-216">The following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="2e7a8-217">Crie o disco de dados com o comando [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="2e7a8-217">Create the data disk with the [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="2e7a8-218">Obtenha a máquina virtual à qual deseja adicionar o disco de dados com o comando [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="2e7a8-218">Get the virtual machine that you want to add the data disk to with the [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="2e7a8-219">Adicione o disco de dados à configuração da máquina virtual com o comando [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="2e7a8-219">Add the data disk to the virtual machine configuration with the [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="2e7a8-220">Atualize a máquina virtual com o comando [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="2e7a8-220">Update the virtual machine with the [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="2e7a8-221">Preparar discos de dados</span><span class="sxs-lookup"><span data-stu-id="2e7a8-221">Prepare data disks</span></span>

<span data-ttu-id="2e7a8-222">Depois que um disco é anexado à máquina virtual, o sistema operacional precisa ser configurado para usar o disco.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-222">Once a disk has been attached to the virtual machine, the operating system needs to be configured to use the disk.</span></span> <span data-ttu-id="2e7a8-223">O exemplo a seguir mostra como configurar manualmente o primeiro disco adicionado à VM.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-223">The following example shows how to manually configure the first disk added to the VM.</span></span> <span data-ttu-id="2e7a8-224">Esse processo também pode ser automatizado usando a [extensão de script personalizado](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="2e7a8-224">This process can also be automated using the [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="2e7a8-225">Configuração manual</span><span class="sxs-lookup"><span data-stu-id="2e7a8-225">Manual configuration</span></span>

<span data-ttu-id="2e7a8-226">Crie uma conexão RDP com a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-226">Create an RDP connection with the virtual machine.</span></span> <span data-ttu-id="2e7a8-227">Abra o PowerShell e execute este script.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="2e7a8-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2e7a8-228">Next steps</span></span>

<span data-ttu-id="2e7a8-229">Neste tutorial, você aprendeu sobre tópicos de discos da VM como:</span><span class="sxs-lookup"><span data-stu-id="2e7a8-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2e7a8-230">Discos de sistema operacional e discos temporários</span><span class="sxs-lookup"><span data-stu-id="2e7a8-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="2e7a8-231">Discos de dados</span><span class="sxs-lookup"><span data-stu-id="2e7a8-231">Data disks</span></span>
> * <span data-ttu-id="2e7a8-232">Discos Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="2e7a8-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="2e7a8-233">Desempenho do disco</span><span class="sxs-lookup"><span data-stu-id="2e7a8-233">Disk performance</span></span>
> * <span data-ttu-id="2e7a8-234">Anexar e preparar os discos de dados</span><span class="sxs-lookup"><span data-stu-id="2e7a8-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="2e7a8-235">Vá para o próximo tutorial para saber como automatizar a configuração da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2e7a8-235">Advance to the next tutorial to learn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2e7a8-236">Automatizar a configuração da VM</span><span class="sxs-lookup"><span data-stu-id="2e7a8-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
