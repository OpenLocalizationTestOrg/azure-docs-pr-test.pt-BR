---
title: aaaManage Azure discos com hello CLI do Azure | Microsoft Docs
description: Tutorial - gerenciar discos do Azure com hello CLI do Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a><span data-ttu-id="b2154-103">Gerenciar discos do Azure com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b2154-103">Manage Azure disks with hello Azure CLI</span></span>

<span data-ttu-id="b2154-104">Máquinas virtuais do Azure usam o sistema operacional do discos toostore Olá VMs, aplicativos e dados.</span><span class="sxs-lookup"><span data-stu-id="b2154-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="b2154-105">Ao criar uma VM é importante toochoose um tamanho de disco e carga de trabalho de configuração apropriado toohello esperado.</span><span class="sxs-lookup"><span data-stu-id="b2154-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="b2154-106">Este tutorial aborda a implantação e gerenciamento de discos de VM.</span><span class="sxs-lookup"><span data-stu-id="b2154-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="b2154-107">Você saberá mais sobre:</span><span class="sxs-lookup"><span data-stu-id="b2154-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b2154-108">Discos de sistema operacional e discos temporários</span><span class="sxs-lookup"><span data-stu-id="b2154-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="b2154-109">Discos de dados</span><span class="sxs-lookup"><span data-stu-id="b2154-109">Data disks</span></span>
> * <span data-ttu-id="b2154-110">Discos Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="b2154-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="b2154-111">Desempenho do disco</span><span class="sxs-lookup"><span data-stu-id="b2154-111">Disk performance</span></span>
> * <span data-ttu-id="b2154-112">Anexar e preparar os discos de dados</span><span class="sxs-lookup"><span data-stu-id="b2154-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="b2154-113">Redimensionamento de discos</span><span class="sxs-lookup"><span data-stu-id="b2154-113">Resizing disks</span></span>
> * <span data-ttu-id="b2154-114">Instantâneos de disco</span><span class="sxs-lookup"><span data-stu-id="b2154-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b2154-115">Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b2154-115">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="b2154-116">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2154-116">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b2154-117">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b2154-117">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="b2154-118">Discos padrão do Azure</span><span class="sxs-lookup"><span data-stu-id="b2154-118">Default Azure disks</span></span>

<span data-ttu-id="b2154-119">Quando uma máquina virtual do Azure é criada, dois discos são automaticamente anexados toohello máquina de virtual.</span><span class="sxs-lookup"><span data-stu-id="b2154-119">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="b2154-120">**Disco do sistema operacional** - discos do sistema operacional podem ser dimensionados para cima too1 terabyte e hosts Olá sistema operacional de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="b2154-120">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span> <span data-ttu-id="b2154-121">Olá OS disco é chamado */desenvolvimento/sda* por padrão.</span><span class="sxs-lookup"><span data-stu-id="b2154-121">hello OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="b2154-122">configuração de disco do sistema operacional de saudação de cache de disco de saudação é otimizado para desempenho do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="b2154-122">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="b2154-123">Devido a essa configuração, Olá disco do sistema operacional **não devem** hospedar aplicativos ou dados.</span><span class="sxs-lookup"><span data-stu-id="b2154-123">Because of this configuration, hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="b2154-124">Para aplicativos e dados, utilize um disco de dados, que é detalhado posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="b2154-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="b2154-125">**Disco temporário** -discos temporários usam uma unidade de estado sólido está localizada em Olá mesmo host do Azure como Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b2154-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="b2154-126">Os discos temporários são altamente eficazes e podem ser usados para operações como o processamento de dados temporário.</span><span class="sxs-lookup"><span data-stu-id="b2154-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="b2154-127">No entanto, se Olá VM for movida tooa novo host, todos os dados armazenados em um disco temporário são removidos.</span><span class="sxs-lookup"><span data-stu-id="b2154-127">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="b2154-128">tamanho de saudação do disco temporário Olá é determinado pelo Olá tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="b2154-128">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="b2154-129">Os discos temporários são rotulados */dev/sdb* e têm um ponto de montagem de */mnt*.</span><span class="sxs-lookup"><span data-stu-id="b2154-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="b2154-130">Tamanhos do disco temporário</span><span class="sxs-lookup"><span data-stu-id="b2154-130">Temporary disk sizes</span></span>

| <span data-ttu-id="b2154-131">Tipo</span><span class="sxs-lookup"><span data-stu-id="b2154-131">Type</span></span> | <span data-ttu-id="b2154-132">Tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="b2154-132">VM Size</span></span> | <span data-ttu-id="b2154-133">Tamanho máximo do disco temporário (GB)</span><span class="sxs-lookup"><span data-stu-id="b2154-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="b2154-134">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="b2154-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="b2154-135">Série A e D</span><span class="sxs-lookup"><span data-stu-id="b2154-135">A and D series</span></span> | <span data-ttu-id="b2154-136">800</span><span class="sxs-lookup"><span data-stu-id="b2154-136">800</span></span> |
| [<span data-ttu-id="b2154-137">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="b2154-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="b2154-138">Série F</span><span class="sxs-lookup"><span data-stu-id="b2154-138">F series</span></span> | <span data-ttu-id="b2154-139">800</span><span class="sxs-lookup"><span data-stu-id="b2154-139">800</span></span> |
| [<span data-ttu-id="b2154-140">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="b2154-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="b2154-141">Série D e G</span><span class="sxs-lookup"><span data-stu-id="b2154-141">D and G series</span></span> | <span data-ttu-id="b2154-142">6144</span><span class="sxs-lookup"><span data-stu-id="b2154-142">6144</span></span> |
| [<span data-ttu-id="b2154-143">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="b2154-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="b2154-144">Série L</span><span class="sxs-lookup"><span data-stu-id="b2154-144">L series</span></span> | <span data-ttu-id="b2154-145">5630</span><span class="sxs-lookup"><span data-stu-id="b2154-145">5630</span></span> |
| [<span data-ttu-id="b2154-146">GPU</span><span class="sxs-lookup"><span data-stu-id="b2154-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="b2154-147">Série N</span><span class="sxs-lookup"><span data-stu-id="b2154-147">N series</span></span> | <span data-ttu-id="b2154-148">1440</span><span class="sxs-lookup"><span data-stu-id="b2154-148">1440</span></span> |
| [<span data-ttu-id="b2154-149">Alto desempenho</span><span class="sxs-lookup"><span data-stu-id="b2154-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="b2154-150">Séries A e H</span><span class="sxs-lookup"><span data-stu-id="b2154-150">A and H series</span></span> | <span data-ttu-id="b2154-151">2000</span><span class="sxs-lookup"><span data-stu-id="b2154-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="b2154-152">Discos de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="b2154-152">Azure data disks</span></span>

<span data-ttu-id="b2154-153">Os discos de dados extras podem ser adicionados para instalação de aplicativos e armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="b2154-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="b2154-154">Os discos de dados devem ser usados em qualquer situação onde o armazenamento de dados durável e responsivo é desejado.</span><span class="sxs-lookup"><span data-stu-id="b2154-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="b2154-155">Cada disco de dados tem uma capacidade máxima de 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="b2154-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="b2154-156">Olá tamanho da saudação máquina virtual determina quantos discos de dados podem ser anexado tooa VM.</span><span class="sxs-lookup"><span data-stu-id="b2154-156">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="b2154-157">Para cada núcleo da VM, podem ser anexados dois discos de dados.</span><span class="sxs-lookup"><span data-stu-id="b2154-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="b2154-158">Máximo de discos de dados por VM</span><span class="sxs-lookup"><span data-stu-id="b2154-158">Max data disks per VM</span></span>

| <span data-ttu-id="b2154-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="b2154-159">Type</span></span> | <span data-ttu-id="b2154-160">Tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="b2154-160">VM Size</span></span> | <span data-ttu-id="b2154-161">Máximo de discos de dados por VM</span><span class="sxs-lookup"><span data-stu-id="b2154-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="b2154-162">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="b2154-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="b2154-163">Série A e D</span><span class="sxs-lookup"><span data-stu-id="b2154-163">A and D series</span></span> | <span data-ttu-id="b2154-164">32</span><span class="sxs-lookup"><span data-stu-id="b2154-164">32</span></span> |
| [<span data-ttu-id="b2154-165">Computação otimizada</span><span class="sxs-lookup"><span data-stu-id="b2154-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="b2154-166">Série F</span><span class="sxs-lookup"><span data-stu-id="b2154-166">F series</span></span> | <span data-ttu-id="b2154-167">32</span><span class="sxs-lookup"><span data-stu-id="b2154-167">32</span></span> |
| [<span data-ttu-id="b2154-168">Memória otimizada</span><span class="sxs-lookup"><span data-stu-id="b2154-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="b2154-169">Série D e G</span><span class="sxs-lookup"><span data-stu-id="b2154-169">D and G series</span></span> | <span data-ttu-id="b2154-170">64</span><span class="sxs-lookup"><span data-stu-id="b2154-170">64</span></span> |
| [<span data-ttu-id="b2154-171">Armazenamento otimizado</span><span class="sxs-lookup"><span data-stu-id="b2154-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="b2154-172">Série L</span><span class="sxs-lookup"><span data-stu-id="b2154-172">L series</span></span> | <span data-ttu-id="b2154-173">64</span><span class="sxs-lookup"><span data-stu-id="b2154-173">64</span></span> |
| [<span data-ttu-id="b2154-174">GPU</span><span class="sxs-lookup"><span data-stu-id="b2154-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="b2154-175">Série N</span><span class="sxs-lookup"><span data-stu-id="b2154-175">N series</span></span> | <span data-ttu-id="b2154-176">48</span><span class="sxs-lookup"><span data-stu-id="b2154-176">48</span></span> |
| [<span data-ttu-id="b2154-177">Alto desempenho</span><span class="sxs-lookup"><span data-stu-id="b2154-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="b2154-178">Série A e H</span><span class="sxs-lookup"><span data-stu-id="b2154-178">A and H series</span></span> | <span data-ttu-id="b2154-179">32</span><span class="sxs-lookup"><span data-stu-id="b2154-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="b2154-180">Tipos de disco da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b2154-180">VM disk types</span></span>

<span data-ttu-id="b2154-181">O Azure fornece dois tipos de disco.</span><span class="sxs-lookup"><span data-stu-id="b2154-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="b2154-182">Disco Standard</span><span class="sxs-lookup"><span data-stu-id="b2154-182">Standard disk</span></span>

<span data-ttu-id="b2154-183">Armazenamento padrão é apoiado por HDDs e oferece armazenamento econômico e eficaz.</span><span class="sxs-lookup"><span data-stu-id="b2154-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="b2154-184">Os discos Standard são ideais para uma carga de trabalho econômica de desenvolvimento e teste.</span><span class="sxs-lookup"><span data-stu-id="b2154-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="b2154-185">Disco Premium</span><span class="sxs-lookup"><span data-stu-id="b2154-185">Premium disk</span></span>

<span data-ttu-id="b2154-186">Os discos Premium são apoiados por disco de baixa latência e alto desempenho baseado em SSD.</span><span class="sxs-lookup"><span data-stu-id="b2154-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="b2154-187">Perfeitos para VMs que executam carga de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="b2154-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="b2154-188">O Armazenamento Premium dá suporte às VMs das séries DS, DSv2, GS e FS.</span><span class="sxs-lookup"><span data-stu-id="b2154-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="b2154-189">Discos Premium vêm em três tipos (P10, P20, P30), o tamanho de saudação do disco de saudação determina o tipo de disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2154-189">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="b2154-190">Selecionar um valor de saudação do tamanho de disco é arredondado até o próximo tipo de toohello.</span><span class="sxs-lookup"><span data-stu-id="b2154-190">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="b2154-191">Por exemplo, se o tamanho do disco Olá é menos de 128 GB, o tipo de disco Olá é P10.</span><span class="sxs-lookup"><span data-stu-id="b2154-191">For example, if hello disk size is less than 128 GB, hello disk type is P10.</span></span> <span data-ttu-id="b2154-192">Se o tamanho do disco Olá estiver entre 129 e 512 GB, o tamanho de saudação é um P20.</span><span class="sxs-lookup"><span data-stu-id="b2154-192">If hello disk size is between 129 GB and 512 GB, hello size is a P20.</span></span> <span data-ttu-id="b2154-193">Nada mais de 512 GB, o tamanho de saudação é um P30.</span><span class="sxs-lookup"><span data-stu-id="b2154-193">Anything over 512 GB, hello size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="b2154-194">Desempenho do disco Premium</span><span class="sxs-lookup"><span data-stu-id="b2154-194">Premium disk performance</span></span>

|<span data-ttu-id="b2154-195">Tipo de disco de armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="b2154-195">Premium storage disk type</span></span> | <span data-ttu-id="b2154-196">P10</span><span class="sxs-lookup"><span data-stu-id="b2154-196">P10</span></span> | <span data-ttu-id="b2154-197">P20</span><span class="sxs-lookup"><span data-stu-id="b2154-197">P20</span></span> | <span data-ttu-id="b2154-198">P30</span><span class="sxs-lookup"><span data-stu-id="b2154-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2154-199">Tamanho do disco (arredondado)</span><span class="sxs-lookup"><span data-stu-id="b2154-199">Disk size (round up)</span></span> | <span data-ttu-id="b2154-200">128 GB</span><span class="sxs-lookup"><span data-stu-id="b2154-200">128 GB</span></span> | <span data-ttu-id="b2154-201">512 GB</span><span class="sxs-lookup"><span data-stu-id="b2154-201">512 GB</span></span> | <span data-ttu-id="b2154-202">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="b2154-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="b2154-203">IOPS máxima por disco</span><span class="sxs-lookup"><span data-stu-id="b2154-203">Max IOPS per disk</span></span> | <span data-ttu-id="b2154-204">500</span><span class="sxs-lookup"><span data-stu-id="b2154-204">500</span></span> | <span data-ttu-id="b2154-205">2.300</span><span class="sxs-lookup"><span data-stu-id="b2154-205">2,300</span></span> | <span data-ttu-id="b2154-206">5.000</span><span class="sxs-lookup"><span data-stu-id="b2154-206">5,000</span></span> |
<span data-ttu-id="b2154-207">Taxa de transferência por disco</span><span class="sxs-lookup"><span data-stu-id="b2154-207">Throughput per disk</span></span> | <span data-ttu-id="b2154-208">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="b2154-208">100 MB/s</span></span> | <span data-ttu-id="b2154-209">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="b2154-209">150 MB/s</span></span> | <span data-ttu-id="b2154-210">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="b2154-210">200 MB/s</span></span> |

<span data-ttu-id="b2154-211">Enquanto Olá acima tabela identifica o IOPS máximo por disco, um nível mais alto de desempenho pode ser obtido com a distribuição de vários discos de dados.</span><span class="sxs-lookup"><span data-stu-id="b2154-211">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="b2154-212">Por exemplo, uma VM Standard_GS5 pode atingir o máximo de 80.000 IOPS.</span><span class="sxs-lookup"><span data-stu-id="b2154-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="b2154-213">Para obter informações detalhadas sobre o máximo de IOPS por VM, veja [Tamanhos da VM Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="b2154-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="b2154-214">Criar e anexar discos</span><span class="sxs-lookup"><span data-stu-id="b2154-214">Create and attach disks</span></span>

<span data-ttu-id="b2154-215">Discos de dados podem ser criados e anexados no momento da criação da VM ou tooan existente de VM.</span><span class="sxs-lookup"><span data-stu-id="b2154-215">Data disks can be created and attached at VM creation time or tooan existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="b2154-216">Anexar disco na criação da VM</span><span class="sxs-lookup"><span data-stu-id="b2154-216">Attach disk at VM creation</span></span>

<span data-ttu-id="b2154-217">Criar um grupo de recursos com hello [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="b2154-217">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="b2154-218">Criar uma VM usando Olá [criar vm az]( /cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="b2154-218">Create a VM using hello [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="b2154-219">Olá `--datadisk-sizes-gb` argumento é usado toospecify que um disco adicional deve ser criado e anexado a máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="b2154-219">hello `--datadisk-sizes-gb` argument is used toospecify that an additional disk should be created and attached toohello virtual machine.</span></span> <span data-ttu-id="b2154-220">toocreate e anexar mais de um disco, use uma lista delimitada por espaço dos valores de tamanho de disco.</span><span class="sxs-lookup"><span data-stu-id="b2154-220">toocreate and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="b2154-221">Saudação de exemplo a seguir, uma máquina virtual é criada com discos de dados de dois, ambos os 128 GB.</span><span class="sxs-lookup"><span data-stu-id="b2154-221">In hello following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="b2154-222">Como os tamanhos de disco Olá 128 GB, ambos esses discos são configurados como P10s, que fornecem o IOPS máximo de 500 por disco.</span><span class="sxs-lookup"><span data-stu-id="b2154-222">Because hello disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a><span data-ttu-id="b2154-223">Anexar disco tooexisting VM</span><span class="sxs-lookup"><span data-stu-id="b2154-223">Attach disk tooexisting VM</span></span>

<span data-ttu-id="b2154-224">toocreate e anexar uma novo disco tooan máquina virtual existente, use Olá [anexar disco de vm az](/cli/azure/vm/disk#attach) comando.</span><span class="sxs-lookup"><span data-stu-id="b2154-224">toocreate and attach a new disk tooan existing virtual machine, use hello [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="b2154-225">Olá exemplo a seguir cria um disco premium, 128 gigabytes de tamanho e anexa toohello que VM criada na última etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="b2154-225">hello following example creates a premium disk, 128 gigabytes in size, and attaches it toohello VM created in hello last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="b2154-226">Preparar discos de dados</span><span class="sxs-lookup"><span data-stu-id="b2154-226">Prepare data disks</span></span>

<span data-ttu-id="b2154-227">Depois que um disco tenha sido anexado toohello máquina de virtual, o sistema de operacional de saudação precisa toobe configurado toouse Olá disco.</span><span class="sxs-lookup"><span data-stu-id="b2154-227">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="b2154-228">saudação de exemplo a seguir mostra como toomanually configurar um disco.</span><span class="sxs-lookup"><span data-stu-id="b2154-228">hello following example shows how toomanually configure a disk.</span></span> <span data-ttu-id="b2154-229">Esse processo também pode ser automatizado utilizando a inicialização por nuvem, que é abordada em um [tutorial posterior](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="b2154-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="b2154-230">Configuração manual</span><span class="sxs-lookup"><span data-stu-id="b2154-230">Manual configuration</span></span>

<span data-ttu-id="b2154-231">Crie uma conexão SSH com a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2154-231">Create an SSH connection with hello virtual machine.</span></span> <span data-ttu-id="b2154-232">Substitua o endereço IP de exemplo hello com IP público de saudação da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2154-232">Replace hello example IP address with hello public IP of hello virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="b2154-233">Partição de disco Olá com `fdisk`.</span><span class="sxs-lookup"><span data-stu-id="b2154-233">Partition hello disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="b2154-234">Gravar um sistema de arquivos toohello partição usando Olá `mkfs` comando.</span><span class="sxs-lookup"><span data-stu-id="b2154-234">Write a file system toohello partition by using hello `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="b2154-235">Monte o novo disco de saudação para que seja acessível no sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2154-235">Mount hello new disk so that it is accessible in hello operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="b2154-236">disco Olá agora pode ser acessado por meio de saudação *datadrive* ponto de montagem, o que pode ser verificado executando Olá `df -h` comando.</span><span class="sxs-lookup"><span data-stu-id="b2154-236">hello disk can now be accessed through hello *datadrive* mountpoint, which can be verified by running hello `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="b2154-237">saída de Hello mostra a nova unidade de saudação montada em */datadrive*.</span><span class="sxs-lookup"><span data-stu-id="b2154-237">hello output shows hello new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="b2154-238">tooensure que Olá unidade é remontado após uma reinicialização, ela deve ser adicionada toohello */etc/fstab* arquivo.</span><span class="sxs-lookup"><span data-stu-id="b2154-238">tooensure that hello drive is remounted after a reboot, it must be added toohello */etc/fstab* file.</span></span> <span data-ttu-id="b2154-239">toodo fique saudação UUID de disco Olá Olá `blkid` utilitário.</span><span class="sxs-lookup"><span data-stu-id="b2154-239">toodo so, get hello UUID of hello disk with hello `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="b2154-240">saída de Hello exibe Olá UUID da unidade hello, `/dev/sdc1` nesse caso.</span><span class="sxs-lookup"><span data-stu-id="b2154-240">hello output displays hello UUID of hello drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="b2154-241">Adicionar um toohello semelhante de linha a seguir toohello */etc/fstab* arquivo.</span><span class="sxs-lookup"><span data-stu-id="b2154-241">Add a line similar toohello following toohello */etc/fstab* file.</span></span> <span data-ttu-id="b2154-242">Observe também que as barreiras de gravação podem ser desabilitadas utilizando *barrier=0*, essa configuração pode melhorar o desempenho do disco.</span><span class="sxs-lookup"><span data-stu-id="b2154-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="b2154-243">Agora que hello disco tiver sido configurado, feche a sessão SSH de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2154-243">Now that hello disk has been configured, close hello SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="b2154-244">Redimensionar o disco da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b2154-244">Resize VM disk</span></span>

<span data-ttu-id="b2154-245">Quando uma máquina virtual tiver sido implantada, disco de saudação do sistema operacional ou discos de dados anexados podem ser aumentados em tamanho.</span><span class="sxs-lookup"><span data-stu-id="b2154-245">Once a VM has been deployed, hello operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="b2154-246">Aumentando o tamanho de saudação de um disco é benéfico quando precisar de mais espaço de armazenamento ou um nível mais alto de desempenho (P10, P20, P30).</span><span class="sxs-lookup"><span data-stu-id="b2154-246">Increasing hello size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="b2154-247">Observe que discos não podem ser reduzidos.</span><span class="sxs-lookup"><span data-stu-id="b2154-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="b2154-248">Antes de aumentar o tamanho do disco, Olá Id ou nome do disco Olá é necessária.</span><span class="sxs-lookup"><span data-stu-id="b2154-248">Before increasing disk size, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="b2154-249">Saudação de uso [lista de discos az](/cli/azure/vm/disk#list) comando tooreturn todos os discos em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b2154-249">Use hello [az disk list](/cli/azure/vm/disk#list) command tooreturn all disks in a resource group.</span></span> <span data-ttu-id="b2154-250">Anote o nome do disco Olá que deseja tooresize.</span><span class="sxs-lookup"><span data-stu-id="b2154-250">Take note of hello disk name that you would like tooresize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="b2154-251">Olá VM também deve ser desalocada.</span><span class="sxs-lookup"><span data-stu-id="b2154-251">hello VM must also be deallocated.</span></span> <span data-ttu-id="b2154-252">Saudação de uso [az vm desalocar]( /cli/azure/vm#deallocate) toostop de comando e desalocar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b2154-252">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="b2154-253">Saudação de uso [atualização de disco az](/cli/azure/vm/disk#update) disco de saudação do comando tooresize.</span><span class="sxs-lookup"><span data-stu-id="b2154-253">Use hello [az disk update](/cli/azure/vm/disk#update) command tooresize hello disk.</span></span> <span data-ttu-id="b2154-254">Este exemplo redimensiona um disco chamado *myDataDisk* too1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="b2154-254">This example resizes a disk named *myDataDisk* too1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="b2154-255">Após a conclusão da operação de redimensionamento hello, inicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b2154-255">Once hello resize operation has completed, start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="b2154-256">Se você tiver redimensionado Olá operacional do disco do sistema, partição Olá automaticamente é expandido.</span><span class="sxs-lookup"><span data-stu-id="b2154-256">If you’ve resized hello operating system disk, hello partition is automatically be expanded.</span></span> <span data-ttu-id="b2154-257">Se você tiver redimensionado um disco de dados, todas as partições atuais necessário toobe expandido no sistema de operacional Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="b2154-257">If you have resized a data disk, any current partitions need toobe expanded in hello VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="b2154-258">Discos padrão do Azure</span><span class="sxs-lookup"><span data-stu-id="b2154-258">Snapshot Azure disks</span></span>

<span data-ttu-id="b2154-259">Tirar um instantâneo do disco cria uma cópia apenas, point-in-time leitura de disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2154-259">Taking a disk snapshot creates a read only, point-in-time copy of hello disk.</span></span> <span data-ttu-id="b2154-260">Instantâneos VM do Azure são úteis para salvar rapidamente o estado de saudação de uma VM antes de fazer alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="b2154-260">Azure VM snapshots are useful for quickly saving hello state of a VM before making configuration changes.</span></span> <span data-ttu-id="b2154-261">No evento Olá Olá, alterações de configuração provam toobe maneira indesejada, estado da VM pode ser restaurado usando Olá instantâneo.</span><span class="sxs-lookup"><span data-stu-id="b2154-261">In hello event hello configuration changes prove toobe undesired, VM state can be restored using hello snapshot.</span></span> <span data-ttu-id="b2154-262">Quando uma VM tem mais de um disco, um instantâneo é tirado de cada disco independentemente Olá outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="b2154-262">When a VM has more than one disk, a snapshot is taken of each disk independently of hello others.</span></span> <span data-ttu-id="b2154-263">Para fazer backups consistentes com aplicativos, considere a possibilidade de interrupção Olá VM antes de tirar instantâneos de disco.</span><span class="sxs-lookup"><span data-stu-id="b2154-263">For taking application consistent backups, consider stopping hello VM before taking disk snapshots.</span></span> <span data-ttu-id="b2154-264">Como alternativa, use Olá [serviço de Backup do Azure](/azure/backup/), que permite que você tooperform automatizada backups durante a saudação VM está em execução.</span><span class="sxs-lookup"><span data-stu-id="b2154-264">Alternatively, use hello [Azure Backup service](/azure/backup/), which enables you tooperform automated backups while hello VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="b2154-265">Como criar um instantâneo</span><span class="sxs-lookup"><span data-stu-id="b2154-265">Create snapshot</span></span>

<span data-ttu-id="b2154-266">Antes de criar um instantâneo do disco de máquina virtual, hello Id ou nome do disco Olá é necessário.</span><span class="sxs-lookup"><span data-stu-id="b2154-266">Before creating a virtual machine disk snapshot, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="b2154-267">Saudação de uso [Mostrar de vm az](https://docs.microsoft.com/en-us/cli/azure/vm#show) id do disco de saudação do comando tooreturn. Neste exemplo, a id do disco Olá é armazenado em uma variável para que ele pode ser usado em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="b2154-267">Use hello [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command tooreturn hello disk id. In this example, hello disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="b2154-268">Agora que você tem a id de saudação do disco da máquina virtual hello, hello comando a seguir cria um instantâneo do disco hello.</span><span class="sxs-lookup"><span data-stu-id="b2154-268">Now that you have hello id of hello virtual machine disk, hello following command creates a snapshot of hello disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="b2154-269">Como criar o disco a partir de um instantâneo</span><span class="sxs-lookup"><span data-stu-id="b2154-269">Create disk from snapshot</span></span>

<span data-ttu-id="b2154-270">Esse instantâneo, em seguida, pode ser convertido em um disco, o que pode ser usado toorecreate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b2154-270">This snapshot can then be converted into a disk, which can be used toorecreate hello virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="b2154-271">Como restaurar a máquina virtual a partir de um instantâneo</span><span class="sxs-lookup"><span data-stu-id="b2154-271">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="b2154-272">recuperação de máquina virtual toodemonstrate, máquina virtual existente de saudação delete.</span><span class="sxs-lookup"><span data-stu-id="b2154-272">toodemonstrate virtual machine recovery, delete hello existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="b2154-273">Crie uma nova máquina virtual do disco de instantâneo hello.</span><span class="sxs-lookup"><span data-stu-id="b2154-273">Create a new virtual machine from hello snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="b2154-274">Reanexar um disco de dados</span><span class="sxs-lookup"><span data-stu-id="b2154-274">Reattach data disk</span></span>

<span data-ttu-id="b2154-275">Todos os discos de dados necessário toobe reanexado toohello VM.</span><span class="sxs-lookup"><span data-stu-id="b2154-275">All data disks need toobe reattached toohello virtual machine.</span></span>

<span data-ttu-id="b2154-276">Localizar primeiro nome do disco de dados hello usando Olá [lista de discos az](https://docs.microsoft.com/cli/azure/disk#list) comando.</span><span class="sxs-lookup"><span data-stu-id="b2154-276">First find hello data disk name using hello [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="b2154-277">Este exemplo coloca Olá nome do disco de saudação em uma variável chamada *datadisk*, que é usada na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="b2154-277">This example places hello name of hello disk in a variable named *datadisk*, which is used in hello next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="b2154-278">Saudação de uso [anexar disco de vm az](https://docs.microsoft.com/cli/azure/vm/disk#attach) disco de saudação do comando tooattach.</span><span class="sxs-lookup"><span data-stu-id="b2154-278">Use hello [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command tooattach hello disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="b2154-279">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b2154-279">Next steps</span></span>

<span data-ttu-id="b2154-280">Neste tutorial, você aprendeu sobre tópicos de discos da VM como:</span><span class="sxs-lookup"><span data-stu-id="b2154-280">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b2154-281">Discos de sistema operacional e discos temporários</span><span class="sxs-lookup"><span data-stu-id="b2154-281">OS disks and temporary disks</span></span>
> * <span data-ttu-id="b2154-282">Discos de dados</span><span class="sxs-lookup"><span data-stu-id="b2154-282">Data disks</span></span>
> * <span data-ttu-id="b2154-283">Discos Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="b2154-283">Standard and Premium disks</span></span>
> * <span data-ttu-id="b2154-284">Desempenho do disco</span><span class="sxs-lookup"><span data-stu-id="b2154-284">Disk performance</span></span>
> * <span data-ttu-id="b2154-285">Anexar e preparar os discos de dados</span><span class="sxs-lookup"><span data-stu-id="b2154-285">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="b2154-286">Redimensionamento de discos</span><span class="sxs-lookup"><span data-stu-id="b2154-286">Resizing disks</span></span>
> * <span data-ttu-id="b2154-287">Instantâneos de disco</span><span class="sxs-lookup"><span data-stu-id="b2154-287">Disk snapshots</span></span>

<span data-ttu-id="b2154-288">Avançar toohello toolearn próximo de tutorial sobre como automatizar a configuração da VM.</span><span class="sxs-lookup"><span data-stu-id="b2154-288">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b2154-289">Automatizar a configuração da VM</span><span class="sxs-lookup"><span data-stu-id="b2154-289">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
