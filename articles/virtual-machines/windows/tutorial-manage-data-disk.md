---
title: aaaManage Azure discos com hello Azure PowerShell | Microsoft Docs
description: Tutorial - gerenciar discos do Azure com hello Azure PowerShell
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
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="8a888-103">Gerenciar discos do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a888-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="8a888-104">Máquinas virtuais do Azure usam o sistema operacional do discos toostore Olá VMs, aplicativos e dados.</span><span class="sxs-lookup"><span data-stu-id="8a888-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="8a888-105">Ao criar uma VM é importante toochoose um tamanho de disco e carga de trabalho de configuração apropriado toohello esperado.</span><span class="sxs-lookup"><span data-stu-id="8a888-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="8a888-106">Este tutorial aborda a implantação e gerenciamento de discos de VM.</span><span class="sxs-lookup"><span data-stu-id="8a888-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="8a888-107">Você saberá mais sobre:</span><span class="sxs-lookup"><span data-stu-id="8a888-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a888-108">Discos de sistema operacional e discos temporários</span><span class="sxs-lookup"><span data-stu-id="8a888-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="8a888-109">Discos de dados</span><span class="sxs-lookup"><span data-stu-id="8a888-109">Data disks</span></span>
> * <span data-ttu-id="8a888-110">Discos Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="8a888-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="8a888-111">Desempenho do disco</span><span class="sxs-lookup"><span data-stu-id="8a888-111">Disk performance</span></span>
> * <span data-ttu-id="8a888-112">Anexar e preparar os discos de dados</span><span class="sxs-lookup"><span data-stu-id="8a888-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="8a888-113">Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo.</span><span class="sxs-lookup"><span data-stu-id="8a888-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="8a888-114">Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="8a888-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="8a888-115">Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="8a888-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="8a888-116">Discos padrão do Azure</span><span class="sxs-lookup"><span data-stu-id="8a888-116">Default Azure disks</span></span>

<span data-ttu-id="8a888-117">Quando uma máquina virtual do Azure é criada, dois discos são automaticamente anexados toohello máquina de virtual.</span><span class="sxs-lookup"><span data-stu-id="8a888-117">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="8a888-118">**Disco do sistema operacional** - discos do sistema operacional podem ser dimensionados para cima too1 terabyte e hosts Olá sistema operacional de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8a888-118">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span>  <span data-ttu-id="8a888-119">disco Olá SO é atribuído uma letra de unidade de *c:* por padrão.</span><span class="sxs-lookup"><span data-stu-id="8a888-119">hello OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="8a888-120">configuração de disco do sistema operacional de saudação de cache de disco de saudação é otimizado para desempenho do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="8a888-120">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="8a888-121">disco Olá SO **não devem** hospedar aplicativos ou dados.</span><span class="sxs-lookup"><span data-stu-id="8a888-121">hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="8a888-122">Para aplicativos e dados, use um disco de dados, que é detalhado posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="8a888-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="8a888-123">**Disco temporário** -discos temporários usam uma unidade de estado sólido está localizada em Olá mesmo host do Azure como Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8a888-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="8a888-124">Os discos temporários são altamente eficazes e podem ser usados para operações como o processamento de dados temporário.</span><span class="sxs-lookup"><span data-stu-id="8a888-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="8a888-125">No entanto, se Olá VM for movida tooa novo host, todos os dados armazenados em um disco temporário são removidos.</span><span class="sxs-lookup"><span data-stu-id="8a888-125">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="8a888-126">tamanho de saudação do disco temporário Olá é determinado pelo Olá tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="8a888-126">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="8a888-127">Os discos temporários são atribuídos à letra de unidade *d:* por padrão.</span><span class="sxs-lookup"><span data-stu-id="8a888-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="8a888-128">Tamanhos do disco temporário</span><span class="sxs-lookup"><span data-stu-id="8a888-128">Temporary disk sizes</span></span>

| <span data-ttu-id="8a888-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="8a888-129">Type</span></span> | <span data-ttu-id="8a888-130">Tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="8a888-130">VM Size</span></span> | <span data-ttu-id="8a888-131">Tamanho máximo do disco temporário (GB)</span><span class="sxs-lookup"><span data-stu-id="8a888-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="8a888-132">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="8a888-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="8a888-133">Série A e D</span><span class="sxs-lookup"><span data-stu-id="8a888-133">A and D series</span></span> | <span data-ttu-id="8a888-134">800</span><span class="sxs-lookup"><span data-stu-id="8a888-134">800</span></span> |
| [<span data-ttu-id="8a888-135">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="8a888-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="8a888-136">Série F</span><span class="sxs-lookup"><span data-stu-id="8a888-136">F series</span></span> | <span data-ttu-id="8a888-137">800</span><span class="sxs-lookup"><span data-stu-id="8a888-137">800</span></span> |
| [<span data-ttu-id="8a888-138">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="8a888-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="8a888-139">Série D e G</span><span class="sxs-lookup"><span data-stu-id="8a888-139">D and G series</span></span> | <span data-ttu-id="8a888-140">6144</span><span class="sxs-lookup"><span data-stu-id="8a888-140">6144</span></span> |
| [<span data-ttu-id="8a888-141">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="8a888-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="8a888-142">Série L</span><span class="sxs-lookup"><span data-stu-id="8a888-142">L series</span></span> | <span data-ttu-id="8a888-143">5630</span><span class="sxs-lookup"><span data-stu-id="8a888-143">5630</span></span> |
| [<span data-ttu-id="8a888-144">GPU</span><span class="sxs-lookup"><span data-stu-id="8a888-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="8a888-145">Série N</span><span class="sxs-lookup"><span data-stu-id="8a888-145">N series</span></span> | <span data-ttu-id="8a888-146">1440</span><span class="sxs-lookup"><span data-stu-id="8a888-146">1440</span></span> |
| [<span data-ttu-id="8a888-147">Alto desempenho</span><span class="sxs-lookup"><span data-stu-id="8a888-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="8a888-148">Séries A e H</span><span class="sxs-lookup"><span data-stu-id="8a888-148">A and H series</span></span> | <span data-ttu-id="8a888-149">2000</span><span class="sxs-lookup"><span data-stu-id="8a888-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="8a888-150">Discos de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="8a888-150">Azure data disks</span></span>

<span data-ttu-id="8a888-151">Os discos de dados extras podem ser adicionados para instalação de aplicativos e armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="8a888-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="8a888-152">Os discos de dados devem ser usados em qualquer situação onde o armazenamento de dados durável e responsivo é desejado.</span><span class="sxs-lookup"><span data-stu-id="8a888-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="8a888-153">Cada disco de dados tem uma capacidade máxima de 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="8a888-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="8a888-154">Olá tamanho da saudação máquina virtual determina quantos discos de dados podem ser anexado tooa VM.</span><span class="sxs-lookup"><span data-stu-id="8a888-154">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="8a888-155">Para cada núcleo da VM, podem ser anexados dois discos de dados.</span><span class="sxs-lookup"><span data-stu-id="8a888-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="8a888-156">Máximo de discos de dados por VM</span><span class="sxs-lookup"><span data-stu-id="8a888-156">Max data disks per VM</span></span>

| <span data-ttu-id="8a888-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="8a888-157">Type</span></span> | <span data-ttu-id="8a888-158">Tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="8a888-158">VM Size</span></span> | <span data-ttu-id="8a888-159">Máximo de discos de dados por VM</span><span class="sxs-lookup"><span data-stu-id="8a888-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="8a888-160">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="8a888-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="8a888-161">Série A e D</span><span class="sxs-lookup"><span data-stu-id="8a888-161">A and D series</span></span> | <span data-ttu-id="8a888-162">32</span><span class="sxs-lookup"><span data-stu-id="8a888-162">32</span></span> |
| [<span data-ttu-id="8a888-163">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="8a888-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="8a888-164">Série F</span><span class="sxs-lookup"><span data-stu-id="8a888-164">F series</span></span> | <span data-ttu-id="8a888-165">32</span><span class="sxs-lookup"><span data-stu-id="8a888-165">32</span></span> |
| [<span data-ttu-id="8a888-166">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="8a888-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="8a888-167">Série D e G</span><span class="sxs-lookup"><span data-stu-id="8a888-167">D and G series</span></span> | <span data-ttu-id="8a888-168">64</span><span class="sxs-lookup"><span data-stu-id="8a888-168">64</span></span> |
| [<span data-ttu-id="8a888-169">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="8a888-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="8a888-170">Série L</span><span class="sxs-lookup"><span data-stu-id="8a888-170">L series</span></span> | <span data-ttu-id="8a888-171">64</span><span class="sxs-lookup"><span data-stu-id="8a888-171">64</span></span> |
| [<span data-ttu-id="8a888-172">GPU</span><span class="sxs-lookup"><span data-stu-id="8a888-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="8a888-173">Série N</span><span class="sxs-lookup"><span data-stu-id="8a888-173">N series</span></span> | <span data-ttu-id="8a888-174">48</span><span class="sxs-lookup"><span data-stu-id="8a888-174">48</span></span> |
| [<span data-ttu-id="8a888-175">Alto desempenho</span><span class="sxs-lookup"><span data-stu-id="8a888-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="8a888-176">Série A e H</span><span class="sxs-lookup"><span data-stu-id="8a888-176">A and H series</span></span> | <span data-ttu-id="8a888-177">32</span><span class="sxs-lookup"><span data-stu-id="8a888-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="8a888-178">Tipos de disco da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8a888-178">VM disk types</span></span>

<span data-ttu-id="8a888-179">O Azure fornece dois tipos de disco.</span><span class="sxs-lookup"><span data-stu-id="8a888-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="8a888-180">Disco Standard</span><span class="sxs-lookup"><span data-stu-id="8a888-180">Standard disk</span></span>

<span data-ttu-id="8a888-181">Armazenamento padrão é apoiado por HDDs e oferece armazenamento econômico e eficaz.</span><span class="sxs-lookup"><span data-stu-id="8a888-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="8a888-182">Os discos Standard são ideais para uma carga de trabalho econômica de desenvolvimento e teste.</span><span class="sxs-lookup"><span data-stu-id="8a888-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="8a888-183">Disco Premium</span><span class="sxs-lookup"><span data-stu-id="8a888-183">Premium disk</span></span>

<span data-ttu-id="8a888-184">Os discos Premium são apoiados por disco de baixa latência e alto desempenho baseado em SSD.</span><span class="sxs-lookup"><span data-stu-id="8a888-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="8a888-185">Perfeitos para VMs que executam carga de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="8a888-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="8a888-186">O Armazenamento Premium dá suporte às VMs das séries DS, DSv2, GS e FS.</span><span class="sxs-lookup"><span data-stu-id="8a888-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="8a888-187">Discos Premium vêm em três tipos (P10, P20, P30), o tamanho de saudação do disco de saudação determina o tipo de disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="8a888-187">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="8a888-188">Selecionar um valor de saudação do tamanho de disco é arredondado até o próximo tipo de toohello.</span><span class="sxs-lookup"><span data-stu-id="8a888-188">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="8a888-189">Por exemplo, se for tamanho Olá abaixo de tipo de disco de saudação de 128 GB será P10, entre 129 e 512 P20 e mais de 512 P30.</span><span class="sxs-lookup"><span data-stu-id="8a888-189">For example, if hello size is below 128 GB hello disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="8a888-190">Desempenho do disco Premium</span><span class="sxs-lookup"><span data-stu-id="8a888-190">Premium disk performance</span></span>

|<span data-ttu-id="8a888-191">Tipo de disco de armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="8a888-191">Premium storage disk type</span></span> | <span data-ttu-id="8a888-192">P10</span><span class="sxs-lookup"><span data-stu-id="8a888-192">P10</span></span> | <span data-ttu-id="8a888-193">P20</span><span class="sxs-lookup"><span data-stu-id="8a888-193">P20</span></span> | <span data-ttu-id="8a888-194">P30</span><span class="sxs-lookup"><span data-stu-id="8a888-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8a888-195">Tamanho do disco (arredondado)</span><span class="sxs-lookup"><span data-stu-id="8a888-195">Disk size (round up)</span></span> | <span data-ttu-id="8a888-196">128 GB</span><span class="sxs-lookup"><span data-stu-id="8a888-196">128 GB</span></span> | <span data-ttu-id="8a888-197">512 GB</span><span class="sxs-lookup"><span data-stu-id="8a888-197">512 GB</span></span> | <span data-ttu-id="8a888-198">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="8a888-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="8a888-199">IOPS por disco</span><span class="sxs-lookup"><span data-stu-id="8a888-199">IOPS per disk</span></span> | <span data-ttu-id="8a888-200">500</span><span class="sxs-lookup"><span data-stu-id="8a888-200">500</span></span> | <span data-ttu-id="8a888-201">2.300</span><span class="sxs-lookup"><span data-stu-id="8a888-201">2,300</span></span> | <span data-ttu-id="8a888-202">5.000</span><span class="sxs-lookup"><span data-stu-id="8a888-202">5,000</span></span> |
<span data-ttu-id="8a888-203">Taxa de transferência por disco</span><span class="sxs-lookup"><span data-stu-id="8a888-203">Throughput per disk</span></span> | <span data-ttu-id="8a888-204">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="8a888-204">100 MB/s</span></span> | <span data-ttu-id="8a888-205">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="8a888-205">150 MB/s</span></span> | <span data-ttu-id="8a888-206">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="8a888-206">200 MB/s</span></span> |

<span data-ttu-id="8a888-207">Enquanto Olá acima tabela identifica o IOPS máximo por disco, um nível mais alto de desempenho pode ser obtido com a distribuição de vários discos de dados.</span><span class="sxs-lookup"><span data-stu-id="8a888-207">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="8a888-208">Por exemplo, dados de 64 discos podem ser anexados tooStandard_GS5 VM.</span><span class="sxs-lookup"><span data-stu-id="8a888-208">For instance, 64 data disks can be attached tooStandard_GS5 VM.</span></span> <span data-ttu-id="8a888-209">Se cada um desses discos for dimensionado como um P30, será possível chegar a um máximo de 80.000 IOPS.</span><span class="sxs-lookup"><span data-stu-id="8a888-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="8a888-210">Para obter informações detalhadas sobre o máximo de IOPS por VM, confira [Tamanhos da VM Linux](./sizes.md).</span><span class="sxs-lookup"><span data-stu-id="8a888-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="8a888-211">Criar e anexar discos</span><span class="sxs-lookup"><span data-stu-id="8a888-211">Create and attach disks</span></span>

<span data-ttu-id="8a888-212">exemplo de hello toocomplete neste tutorial, você deve ter uma máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="8a888-212">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="8a888-213">Se necessário, este [exemplo de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) pode criar uma para você.</span><span class="sxs-lookup"><span data-stu-id="8a888-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="8a888-214">Trabalho tutorial hello, substitua VM e o grupo de recursos de saudação nomes onde for necessário.</span><span class="sxs-lookup"><span data-stu-id="8a888-214">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

<span data-ttu-id="8a888-215">Criar a configuração inicial com hello [AzureRmDiskConfig novo](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="8a888-215">Create hello initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="8a888-216">saudação de exemplo a seguir configura um disco que é 128 gigabytes de tamanho.</span><span class="sxs-lookup"><span data-stu-id="8a888-216">hello following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="8a888-217">Criar disco de dados de saudação com hello [AzureRmDisk novo](/powershell/module/azurerm.compute/new-azurermdisk) comando.</span><span class="sxs-lookup"><span data-stu-id="8a888-217">Create hello data disk with hello [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="8a888-218">Get hello VM que você deseja tooadd Olá Olá de toowith de disco de dados [AzureRmVM Get](/powershell/module/azurerm.compute/get-azurermvm) comando.</span><span class="sxs-lookup"><span data-stu-id="8a888-218">Get hello virtual machine that you want tooadd hello data disk toowith hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="8a888-219">Adicionar Olá dados disco toohello configuração de máquina virtual com hello [AzureRmVMDataDisk adicionar](/powershell/module/azurerm.compute/add-azurermvmdatadisk) comando.</span><span class="sxs-lookup"><span data-stu-id="8a888-219">Add hello data disk toohello virtual machine configuration with hello [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="8a888-220">Atualizar a máquina virtual de saudação com hello [AzureRmVM atualização](/powershell/module/azurerm.compute/add-azurermvmdatadisk) comando.</span><span class="sxs-lookup"><span data-stu-id="8a888-220">Update hello virtual machine with hello [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="8a888-221">Preparar discos de dados</span><span class="sxs-lookup"><span data-stu-id="8a888-221">Prepare data disks</span></span>

<span data-ttu-id="8a888-222">Depois que um disco tenha sido anexado toohello máquina de virtual, o sistema de operacional de saudação precisa toobe configurado toouse Olá disco.</span><span class="sxs-lookup"><span data-stu-id="8a888-222">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="8a888-223">Olá exemplo a seguir mostra como configurar o primeiro disco de saudação adicionado toomanually toohello VM.</span><span class="sxs-lookup"><span data-stu-id="8a888-223">hello following example shows how toomanually configure hello first disk added toohello VM.</span></span> <span data-ttu-id="8a888-224">Esse processo também pode ser automatizado usando Olá [extensão do script personalizado](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="8a888-224">This process can also be automated using hello [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="8a888-225">Configuração manual</span><span class="sxs-lookup"><span data-stu-id="8a888-225">Manual configuration</span></span>

<span data-ttu-id="8a888-226">Crie uma conexão de RDP com a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="8a888-226">Create an RDP connection with hello virtual machine.</span></span> <span data-ttu-id="8a888-227">Abra o PowerShell e execute este script.</span><span class="sxs-lookup"><span data-stu-id="8a888-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="8a888-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8a888-228">Next steps</span></span>

<span data-ttu-id="8a888-229">Neste tutorial, você aprendeu sobre tópicos de discos da VM como:</span><span class="sxs-lookup"><span data-stu-id="8a888-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a888-230">Discos de sistema operacional e discos temporários</span><span class="sxs-lookup"><span data-stu-id="8a888-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="8a888-231">Discos de dados</span><span class="sxs-lookup"><span data-stu-id="8a888-231">Data disks</span></span>
> * <span data-ttu-id="8a888-232">Discos Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="8a888-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="8a888-233">Desempenho do disco</span><span class="sxs-lookup"><span data-stu-id="8a888-233">Disk performance</span></span>
> * <span data-ttu-id="8a888-234">Anexar e preparar os discos de dados</span><span class="sxs-lookup"><span data-stu-id="8a888-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="8a888-235">Avançar toohello toolearn próximo de tutorial sobre como automatizar a configuração da VM.</span><span class="sxs-lookup"><span data-stu-id="8a888-235">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8a888-236">Automatizar a configuração da VM</span><span class="sxs-lookup"><span data-stu-id="8a888-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
