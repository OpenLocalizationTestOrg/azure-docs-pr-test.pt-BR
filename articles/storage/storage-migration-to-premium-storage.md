---
title: Migrando VMs para o Armazenamento Premium do Azure | Microsoft Docs
description: "Migre VMs existentes para o Armazenamento Premium do Azure. O Armazenamento Premium dá suporte ao disco de alto desempenho e baixa latência para cargas de trabalho que usam muita E/S em execução em máquinas virtuais do Azure."
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: 645b37fff2dd6a12114719bac66a937cf8e8ffaa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="migrating-to-azure-premium-storage-unmanaged-disks"></a><span data-ttu-id="a94cf-104">Migrando para o Armazenamento Premium do Azure (Discos não gerenciados)</span><span class="sxs-lookup"><span data-stu-id="a94cf-104">Migrating to Azure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="a94cf-105">Este artigo explica como migrar uma VM que usa discos Standard não gerenciados para uma VM que usa discos Premium não gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a94cf-105">This article discusses how to migrate a VM that uses unmanaged standard disks to a VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="a94cf-106">É recomendável usar o Azure Managed Disks para novas VMs e converter os discos não gerenciados anteriores em disco gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a94cf-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks to managed disks.</span></span> <span data-ttu-id="a94cf-107">O Managed Disks tratam das contas de armazenamento subjacentes para você.</span><span class="sxs-lookup"><span data-stu-id="a94cf-107">Managed Disks handle the underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="a94cf-108">Para saber mais, confira [Managed Disks Overview](storage-managed-disks-overview.md) (Visão geral do Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="a94cf-108">For more information, please see our [Managed Disks Overview](storage-managed-disks-overview.md).</span></span>
>

<span data-ttu-id="a94cf-109">O Armazenamento Premium do Azure dá suporte de disco de alto desempenho e baixa latência para máquinas virtuais executando cargas de trabalho intensivas para entradas e saídas.</span><span class="sxs-lookup"><span data-stu-id="a94cf-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="a94cf-110">Você pode tirar proveito da velocidade e desempenho desses discos migrando os discos de VM do aplicativo para o Armazenamento do Azure Premium.</span><span class="sxs-lookup"><span data-stu-id="a94cf-110">You can take advantage of the speed and performance of these disks by migrating your application's VM disks to Azure Premium Storage.</span></span>

<span data-ttu-id="a94cf-111">O objetivo deste guia é ajudar novos usuários do Armazenamento Premium do Azure a se preparar melhor para fazer uma transição sem problemas de seu sistema atual para o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="a94cf-111">The purpose of this guide is to help new users of Azure Premium Storage better prepare to make a smooth transition from their current system to Premium Storage.</span></span> <span data-ttu-id="a94cf-112">O guia aborda três principais componentes nesse processo:</span><span class="sxs-lookup"><span data-stu-id="a94cf-112">The guide addresses three of the key components in this process:</span></span>

* [<span data-ttu-id="a94cf-113">Planejar a migração para o Armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="a94cf-113">Plan for the Migration to Premium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="a94cf-114">Preparar e copiar VHDs (discos rígidos virtuais) para o Armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="a94cf-114">Prepare and Copy Virtual Hard Disks (VHDs) to Premium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="a94cf-115">Criar uma Máquina Virtual do Azure usando o Armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="a94cf-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="a94cf-116">Você pode migrar VMs de outras plataformas para o Armazenamento do Azure Premium ou migrar VMs do Azure existentes do Armazenamento Standard para o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="a94cf-116">You can either migrate VMs from other platforms to Azure Premium Storage or migrate existing Azure VMs from Standard Storage to Premium Storage.</span></span> <span data-ttu-id="a94cf-117">Este guia aborda as etapas para os dois cenários.</span><span class="sxs-lookup"><span data-stu-id="a94cf-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="a94cf-118">Siga as etapas especificadas na seção relevante, dependendo do cenário.</span><span class="sxs-lookup"><span data-stu-id="a94cf-118">Follow the steps specified in the relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="a94cf-119">Você pode encontrar uma visão geral de recursos e os preços do Armazenamento Premium em [Armazenamento Premium: Armazenamento de Alto Desempenho para Cargas de Trabalho de Máquina Virtual do Azure](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="a94cf-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="a94cf-120">É recomendável migrar qualquer disco de máquina virtual que exija IOPS alta para o Armazenamento Premium do Azure para obter o melhor desempenho para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-120">We recommend migrating any virtual machine disk requiring high IOPS to Azure Premium Storage for the best performance for your application.</span></span> <span data-ttu-id="a94cf-121">Se o disco não requer IOPS alta, você pode limitar os custos mantendo-a no armazenamento padrão, que armazena dados de disco da máquina virtual em HDDs (unidades de disco rígido) em vez de SSDs.</span><span class="sxs-lookup"><span data-stu-id="a94cf-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="a94cf-122">A conclusão do processo de migração em sua totalidade pode exigir ações adicionais antes e depois das etapas fornecidas neste guia.</span><span class="sxs-lookup"><span data-stu-id="a94cf-122">Completing the migration process in its entirety may require additional actions both before and after the steps provided in this guide.</span></span> <span data-ttu-id="a94cf-123">Os exemplos incluem a configuração pontos de extremidade ou redes virtuais ou alterações de código no próprio aplicativo, o que pode exigir algum tempo de inatividade no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-123">Examples include configuring virtual networks or endpoints or making code changes within the application itself which may require some downtime in your application.</span></span> <span data-ttu-id="a94cf-124">Essas ações são exclusivas para cada aplicativo e devem ser concluídas junto com as etapas fornecidas neste guia para fazer a transição completa para o Armazenamento Premium da maneira mais simples possível.</span><span class="sxs-lookup"><span data-stu-id="a94cf-124">These actions are unique to each application, and you should complete them along with the steps provided in this guide to make the full transition to Premium Storage as seamless as possible.</span></span>

## <span data-ttu-id="a94cf-125"><a name="plan-the-migration-to-premium-storage"></a>Planejar a migração para o Armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="a94cf-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for the migration to Premium Storage</span></span>
<span data-ttu-id="a94cf-126">Esta seção garante que você se prepare para seguir as etapas de migração neste artigo e o ajuda a tomar a melhor decisão quanto a tipos de VM e disco.</span><span class="sxs-lookup"><span data-stu-id="a94cf-126">This section ensures that you are ready to follow the migration steps in this article, and helps you to make the best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a94cf-127">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a94cf-127">Prerequisites</span></span>
* <span data-ttu-id="a94cf-128">Você também precisará de uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a94cf-128">You will need an Azure subscription.</span></span> <span data-ttu-id="a94cf-129">Se você ainda não tiver uma, você poderá criar uma assinatura de [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/) de um mês ou visitar [Preços do Azure](https://azure.microsoft.com/pricing/) para obter mais opções.</span><span class="sxs-lookup"><span data-stu-id="a94cf-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="a94cf-130">Para executar os cmdlets PowerShell, você precisará do módulo Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a94cf-130">To execute PowerShell cmdlets, you will need the Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="a94cf-131">Consulte [Como instalar e configurar o PowerShell do Azure](/powershell/azure/overview) para obter o ponto e as instruções de instalação.</span><span class="sxs-lookup"><span data-stu-id="a94cf-131">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the install point and installation instructions.</span></span>
* <span data-ttu-id="a94cf-132">Quando planeja usar VMs do Azure em execução no Armazenamento Premium, você precisa usar VMs compatíveis com o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="a94cf-132">When you plan to use Azure VMs running on Premium Storage, you need to use the Premium Storage capable VMs.</span></span> <span data-ttu-id="a94cf-133">Você pode usar discos de Armazenamento Standard e Premium com VMs compatíveis com o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="a94cf-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="a94cf-134">Os discos de armazenamento Premium estarão disponíveis com mais tipos de VM no futuro.</span><span class="sxs-lookup"><span data-stu-id="a94cf-134">Premium storage disks will be available with more VM types in the future.</span></span> <span data-ttu-id="a94cf-135">Para obter informações sobre todos os tamanhos e tipos de discos de VM do Azure disponíveis, veja [Tamanhos para máquinas virtuais](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [Tamanhos para Serviços de Nuvem](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="a94cf-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="a94cf-136">Considerações</span><span class="sxs-lookup"><span data-stu-id="a94cf-136">Considerations</span></span>
<span data-ttu-id="a94cf-137">Uma VM do Azure oferece suporte à anexação de vários discos de Armazenamento Premium, para que seus aplicativos possam ter até 256 TB de armazenamento por VM.</span><span class="sxs-lookup"><span data-stu-id="a94cf-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up to 256 TB of storage per VM.</span></span> <span data-ttu-id="a94cf-138">Com o Armazenamento Premium, seus aplicativos podem atingir 80.000 IOPS (operações de entrada/saída por segundo) por VM e taxa de transferência de disco de 2.000 MB por segundo por VM com latências extremamente baixas para operações de leitura.</span><span class="sxs-lookup"><span data-stu-id="a94cf-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="a94cf-139">Você tem opções de várias VMs e Discos.</span><span class="sxs-lookup"><span data-stu-id="a94cf-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="a94cf-140">Esta seção se destina a ajudá-lo a encontrar uma opção mais adequada para sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a94cf-140">This section is to help you to find an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="a94cf-141">Tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="a94cf-141">VM sizes</span></span>
<span data-ttu-id="a94cf-142">As especificações de tamanho de VM do Azure são listadas em [Tamanhos para máquinas virtuais](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a94cf-142">The Azure VM size specifications are listed in [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="a94cf-143">Examine as características de desempenho das máquinas virtuais que funcionam com o Armazenamento Premium e escolha o tamanho de VM mais apropriado que melhor atende à sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a94cf-143">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="a94cf-144">Certifique-se de que há largura de banda suficiente disponível na sua VM para direcionar o tráfego de disco.</span><span class="sxs-lookup"><span data-stu-id="a94cf-144">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="a94cf-145">Tamanhos do disco</span><span class="sxs-lookup"><span data-stu-id="a94cf-145">Disk sizes</span></span>
<span data-ttu-id="a94cf-146">Há cinco tipos de discos que podem ser usados com a VM e cada um tem IOPs específicos e limites de taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="a94cf-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="a94cf-147">Leve em consideração esses limites ao escolher o tipo de disco para sua VM com base nas necessidades de seu aplicativo em termos de capacidade, desempenho, escalabilidade e cargas de pico.</span><span class="sxs-lookup"><span data-stu-id="a94cf-147">Take into consideration these limits when choosing the disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="a94cf-148">Tipo de discos premium</span><span class="sxs-lookup"><span data-stu-id="a94cf-148">Premium Disks Type</span></span>  | <span data-ttu-id="a94cf-149">P10</span><span class="sxs-lookup"><span data-stu-id="a94cf-149">P10</span></span>   | <span data-ttu-id="a94cf-150">P20</span><span class="sxs-lookup"><span data-stu-id="a94cf-150">P20</span></span>   | <span data-ttu-id="a94cf-151">P30</span><span class="sxs-lookup"><span data-stu-id="a94cf-151">P30</span></span>            | <span data-ttu-id="a94cf-152">P40</span><span class="sxs-lookup"><span data-stu-id="a94cf-152">P40</span></span>            | <span data-ttu-id="a94cf-153">P50</span><span class="sxs-lookup"><span data-stu-id="a94cf-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="a94cf-154">Tamanho do disco</span><span class="sxs-lookup"><span data-stu-id="a94cf-154">Disk size</span></span>           | <span data-ttu-id="a94cf-155">128 GB</span><span class="sxs-lookup"><span data-stu-id="a94cf-155">128 GB</span></span>| <span data-ttu-id="a94cf-156">512 GB</span><span class="sxs-lookup"><span data-stu-id="a94cf-156">512 GB</span></span>| <span data-ttu-id="a94cf-157">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="a94cf-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="a94cf-158">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="a94cf-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="a94cf-159">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="a94cf-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="a94cf-160">IOPS por disco</span><span class="sxs-lookup"><span data-stu-id="a94cf-160">IOPS per disk</span></span>       | <span data-ttu-id="a94cf-161">500</span><span class="sxs-lookup"><span data-stu-id="a94cf-161">500</span></span>   | <span data-ttu-id="a94cf-162">2.300</span><span class="sxs-lookup"><span data-stu-id="a94cf-162">2300</span></span>  | <span data-ttu-id="a94cf-163">5.000</span><span class="sxs-lookup"><span data-stu-id="a94cf-163">5000</span></span>           | <span data-ttu-id="a94cf-164">7500</span><span class="sxs-lookup"><span data-stu-id="a94cf-164">7500</span></span>           | <span data-ttu-id="a94cf-165">7500</span><span class="sxs-lookup"><span data-stu-id="a94cf-165">7500</span></span>           | 
| <span data-ttu-id="a94cf-166">Taxa de transferência por disco</span><span class="sxs-lookup"><span data-stu-id="a94cf-166">Throughput per disk</span></span> | <span data-ttu-id="a94cf-167">100 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="a94cf-167">100 MB per second</span></span> | <span data-ttu-id="a94cf-168">150 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="a94cf-168">150 MB per second</span></span> | <span data-ttu-id="a94cf-169">200 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="a94cf-169">200 MB per second</span></span> | <span data-ttu-id="a94cf-170">250 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="a94cf-170">250 MB per second</span></span> | <span data-ttu-id="a94cf-171">250 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="a94cf-171">250 MB per second</span></span> |

<span data-ttu-id="a94cf-172">Dependendo da carga de trabalho, determine se discos de dados adicionais são necessários para sua VM.</span><span class="sxs-lookup"><span data-stu-id="a94cf-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="a94cf-173">Você pode anexar diversos discos de dados persistentes à sua VM.</span><span class="sxs-lookup"><span data-stu-id="a94cf-173">You can attach several persistent data disks to your VM.</span></span> <span data-ttu-id="a94cf-174">Se necessário, pode distribuir entre os discos para aumentar a capacidade e o desempenho do volume.</span><span class="sxs-lookup"><span data-stu-id="a94cf-174">If needed, you can stripe across the disks to increase the capacity and performance of the volume.</span></span> <span data-ttu-id="a94cf-175">(Veja o que é a distribuição de disco [aqui](storage-premium-storage-performance.md#disk-striping).) Se você distribuir discos de dados do Armazenamento Premium usando [Espaços de Armazenamento][4], deverá configurá-lo com uma coluna para cada disco usado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="a94cf-176">Caso contrário, o desempenho geral do volume distribuído pode ser menor que o esperado devido a uma distribuição irregular de tráfego entre os discos.</span><span class="sxs-lookup"><span data-stu-id="a94cf-176">Otherwise, the overall performance of the striped volume may be lower than expected due to uneven distribution of traffic across the disks.</span></span> <span data-ttu-id="a94cf-177">Para as VMs do Linux, você pode usar o utilitário *mdadm* para obter o mesmo resultado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-177">For Linux VMs you can use the *mdadm* utility to achieve the same.</span></span> <span data-ttu-id="a94cf-178">Consulte o artigo [Configurar o Software RAID no Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="a94cf-178">See article [Configure Software RAID on Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="a94cf-179">Metas de escalabilidade da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a94cf-179">Storage account scalability targets</span></span>
<span data-ttu-id="a94cf-180">As contas de Armazenamento Premium têm as seguintes metas de escalabilidade, além das [Metas de Desempenho e Escalabilidade do Armazenamento do Azure](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="a94cf-180">Premium Storage accounts have the following scalability targets in addition to the [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="a94cf-181">Se as exigências de seu aplicativo exceder as metas de escalabilidade de uma única conta de armazenamento, crie seu aplicativo para usar múltiplas contas de armazenamento e particione seus dados nessas contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a94cf-181">If your application requirements exceed the scalability targets of a single storage account, build your application to use multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="a94cf-182">Capacidade total da conta</span><span class="sxs-lookup"><span data-stu-id="a94cf-182">Total Account Capacity</span></span> | <span data-ttu-id="a94cf-183">Largura de banda total para uma conta de armazenamento com redundância local</span><span class="sxs-lookup"><span data-stu-id="a94cf-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="a94cf-184">Capacidade de disco: 35 TB</span><span class="sxs-lookup"><span data-stu-id="a94cf-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="a94cf-185">Capacidade do instantâneo: 10 TB</span><span class="sxs-lookup"><span data-stu-id="a94cf-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="a94cf-186">Até 50 gigabits para Entrada + Saída</span><span class="sxs-lookup"><span data-stu-id="a94cf-186">Up to 50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="a94cf-187">Para obter mais informações sobre as especificações do Armazenamento Premium, verifique as [Metas de Escalabilidade e Desempenho ao usar o Armazenamento Premium](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="a94cf-187">For the more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="a94cf-188">Política de cache de disco</span><span class="sxs-lookup"><span data-stu-id="a94cf-188">Disk caching policy</span></span>
<span data-ttu-id="a94cf-189">Por padrão, a política de cache de disco é *Somente leitura* para todos os discos de dados Premium e *Leitura e gravação* para o disco de sistema operacional Premium anexado à VM.</span><span class="sxs-lookup"><span data-stu-id="a94cf-189">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="a94cf-190">Esta definição de configuração é recomendável para atingir o desempenho ideal de E/Ss dos seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a94cf-190">This configuration setting is recommended to achieve the optimal performance for your application's IOs.</span></span> <span data-ttu-id="a94cf-191">Para discos de dados de gravação intensa ou somente gravação (como arquivos de log do SQL Server), desabilite o cache de disco para que possa obter o melhor desempenho do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="a94cf-192">As configurações de cache existentes para os discos de dados podem ser atualizadas usando o [Portal do Azure](https://portal.azure.com) ou o parâmetro *-HostCaching* do cmdlet *Set-AzureDataDisk*.</span><span class="sxs-lookup"><span data-stu-id="a94cf-192">The cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or the *-HostCaching* parameter of the *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="a94cf-193">Local</span><span class="sxs-lookup"><span data-stu-id="a94cf-193">Location</span></span>
<span data-ttu-id="a94cf-194">Escolha um local onde o Armazenamento do Azure Premium está disponível.</span><span class="sxs-lookup"><span data-stu-id="a94cf-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="a94cf-195">Confira [Serviços do Azure por região](https://azure.microsoft.com/regions/#services) para obter informações atualizadas sobre as localizações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a94cf-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="a94cf-196">As máquinas virtuais na mesma região da conta de armazenamento que armazena os discos da VM fornecerão um desempenho muito melhor em relação a estarem em regiões separadas.</span><span class="sxs-lookup"><span data-stu-id="a94cf-196">VMs located in the same region as the Storage account that stores the disks for the VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="a94cf-197">Outras definições de configuração da VM do Azure</span><span class="sxs-lookup"><span data-stu-id="a94cf-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="a94cf-198">Ao criar uma VM do Azure, você será solicitado a definir certas configurações da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a94cf-198">When creating an Azure VM, you will be asked to configure certain VM settings.</span></span> <span data-ttu-id="a94cf-199">Lembre-se de que algumas configurações são fixas durante o tempo de vida da VM, enquanto você pode modificar ou adicionar outras posteriormente.</span><span class="sxs-lookup"><span data-stu-id="a94cf-199">Remember, few settings are fixed for the lifetime of the VM, while you can modify or add others later.</span></span> <span data-ttu-id="a94cf-200">Revise essas definições de configuração da máquina virtual do Azure e verifique se elas estão definidas corretamente para atender aos seus requisitos de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a94cf-200">Review these Azure VM configuration settings and make sure that these are configured appropriately to match your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="a94cf-201">Otimização</span><span class="sxs-lookup"><span data-stu-id="a94cf-201">Optimization</span></span>
<span data-ttu-id="a94cf-202">[Armazenamento Premium do Azure: design de alto desempenho](storage-premium-storage-performance.md) fornece diretrizes para criação de aplicativos de alto desempenho usando o Armazenamento Premium do Azure.</span><span class="sxs-lookup"><span data-stu-id="a94cf-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="a94cf-203">Você pode seguir as diretrizes combinadas a práticas recomendadas aplicáveis a tecnologias usadas por seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-203">You can follow the guidelines combined with performance best practices applicable to technologies used by your application.</span></span>

## <span data-ttu-id="a94cf-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Preparar e copiar VHDs (discos rígidos virtuais) para o Armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="a94cf-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) to Premium Storage</span></span>
<span data-ttu-id="a94cf-205">A seção a seguir fornece diretrizes para preparar VHDs de sua VM e copiar VHDs para o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a94cf-205">The following section provides guidelines for preparing VHDs from your VM and copying VHDs to Azure Storage.</span></span>

* [<span data-ttu-id="a94cf-206">Cenário 1: "estou migrando VMs do Azure existentes para o Armazenamento do Azure Premium".</span><span class="sxs-lookup"><span data-stu-id="a94cf-206">Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="a94cf-207">Cenário 2: "estou migrando VMs de outras plataformas para o Armazenamento Premium do Azure".</span><span class="sxs-lookup"><span data-stu-id="a94cf-207">Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="a94cf-208">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a94cf-208">Prerequisites</span></span>
<span data-ttu-id="a94cf-209">Para preparar os VHDs para a migração, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="a94cf-209">To prepare the VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="a94cf-210">Uma assinatura do Azure, uma conta de armazenamento e um contêiner na conta de armazenamento para o qual o VHD será copiado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-210">An Azure subscription, a storage account, and a container in that storage account to which you can copy your VHD.</span></span> <span data-ttu-id="a94cf-211">Observe que a conta de armazenamento de destino pode ser uma conta de Armazenamento Standard ou Premium, dependendo do requisito.</span><span class="sxs-lookup"><span data-stu-id="a94cf-211">Note that the destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="a94cf-212">Uma ferramenta para generalizar o VHD, caso você planeje criar várias instâncias da VM por meio dele.</span><span class="sxs-lookup"><span data-stu-id="a94cf-212">A tool to generalize the VHD if you plan to create multiple VM instances from it.</span></span> <span data-ttu-id="a94cf-213">Por exemplo, o sysprep para Windows ou o virt-sysprep para Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="a94cf-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="a94cf-214">Uma ferramenta para carregar o arquivo VHD para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a94cf-214">A tool to upload the VHD file to the Storage account.</span></span> <span data-ttu-id="a94cf-215">Consulte [Transferir dados com o Utilitário de Linha de Comando AzCopy](storage-use-azcopy.md) ou use um [Gerenciador de armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="a94cf-215">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="a94cf-216">Este guia descreve a cópia de seu VHD usando a ferramenta AzCopy.</span><span class="sxs-lookup"><span data-stu-id="a94cf-216">This guide describes copying your VHD using the AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="a94cf-217">Se você escolher a opção de cópia síncrona com o AzCopy, para obter o melhor desempenho, copie o VHD executando uma dessas ferramentas em uma VM do Azure que está na mesma região que a conta de armazenamento de destino.</span><span class="sxs-lookup"><span data-stu-id="a94cf-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in the same region as the destination storage account.</span></span> <span data-ttu-id="a94cf-218">Se você estiver copiando um VHD de uma VM do Azure em uma região diferente, o desempenho pode ser mais lento.</span><span class="sxs-lookup"><span data-stu-id="a94cf-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="a94cf-219">Para copiar uma grande quantidade de dados usando uma largura de banda limitada, considere o [uso do serviço de Importação/Exportação do Azure para transferir os dados para o Armazenamento de Blobs](storage-import-export-service.md); isso permite transferir os dados enviando as unidades de disco rígido para um datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="a94cf-219">For copying a large amount of data over limited bandwidth, consider [using the Azure Import/Export service to transfer data to Blob Storage](storage-import-export-service.md); this allows you to transfer your data by shipping hard disk drives to an Azure datacenter.</span></span> <span data-ttu-id="a94cf-220">Você pode usar o serviço de Importação/Exportação para copiar os dados para apenas uma conta de armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="a94cf-220">You can use the Azure Import/Export service to copy data to a standard storage account only.</span></span> <span data-ttu-id="a94cf-221">Quando os dados estiverem em sua conta de armazenamento padrão, você pode usar a [cópia da API do blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) ou o AzCopy para transferir os dados para sua conta de armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="a94cf-221">Once the data is in your standard storage account, you can use either the [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy to transfer the data to your premium storage account.</span></span>
>
> <span data-ttu-id="a94cf-222">Observe que o Microsoft Azure dá suporte apenas a arquivos VHD de tamanho fixo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="a94cf-223">Os arquivos VHDX ou VHDs dinâmicos não têm suporte.</span><span class="sxs-lookup"><span data-stu-id="a94cf-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="a94cf-224">Se você tiver um VHD dinâmico, poderá convertê-lo para ter um tamanho fixo usando o cmdlet [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a94cf-224">If you have a dynamic VHD, you can convert it to fixed size using the [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="a94cf-225"><a name="scenario1"></a>Cenário 1: "estou migrando VMs do Azure existentes para o Armazenamento Premium do Azure".</span><span class="sxs-lookup"><span data-stu-id="a94cf-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>
<span data-ttu-id="a94cf-226">Se você estiver migrando VMs existentes do Azure, interrompa a VM, prepare VHDs por tipo de VHD desejado e copie o VHD com o AzCopy ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a94cf-226">If you are migrating existing Azure VMs, stop the VM, prepare VHDs per the type of VHD you want, and then copy the VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="a94cf-227">A VM precisa estar completamente inoperante para migrar para um estado limpo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-227">The VM needs to be completely down to migrate a clean state.</span></span> <span data-ttu-id="a94cf-228">Haverá um tempo de inatividade até que a migração seja concluída.</span><span class="sxs-lookup"><span data-stu-id="a94cf-228">There will be a downtime until the migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="a94cf-229">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="a94cf-229">Step 1.</span></span> <span data-ttu-id="a94cf-230">Preparar VHDs para migração</span><span class="sxs-lookup"><span data-stu-id="a94cf-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="a94cf-231">Se você estiver migrando VMs do Azure existentes para o Armazenamento Premium, o VHD poderá ser:</span><span class="sxs-lookup"><span data-stu-id="a94cf-231">If you are migrating existing Azure VMs to Premium Storage, your VHD may be:</span></span>

* <span data-ttu-id="a94cf-232">Uma imagem de sistema operacional generalizado</span><span class="sxs-lookup"><span data-stu-id="a94cf-232">A generalized operating system image</span></span>
* <span data-ttu-id="a94cf-233">Um disco de sistema operacional exclusivo</span><span class="sxs-lookup"><span data-stu-id="a94cf-233">A unique operating system disk</span></span>
* <span data-ttu-id="a94cf-234">Um disco de dados</span><span class="sxs-lookup"><span data-stu-id="a94cf-234">A data disk</span></span>

<span data-ttu-id="a94cf-235">Abaixo, percorremos estes três cenários para preparar o VHD.</span><span class="sxs-lookup"><span data-stu-id="a94cf-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-to-create-multiple-vm-instances"></a><span data-ttu-id="a94cf-236">Use um VHD do Sistema Operacional Generalizado para criar várias instâncias de VM</span><span class="sxs-lookup"><span data-stu-id="a94cf-236">Use a generalized Operating System VHD to create multiple VM instances</span></span>
<span data-ttu-id="a94cf-237">Se você estiver carregando um VHD que será usado para criar várias instâncias de VM do Azure genéricas, você deverá primeiro generalizar o VHD usando um utilitário sysprep.</span><span class="sxs-lookup"><span data-stu-id="a94cf-237">If you are uploading a VHD that will be used to create multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="a94cf-238">Isso se aplica a um VHD local ou que está localizado na nuvem.</span><span class="sxs-lookup"><span data-stu-id="a94cf-238">This applies to a VHD that is on-premises or in the cloud.</span></span> <span data-ttu-id="a94cf-239">O Sysprep remove do VHD quaisquer informações específicas da máquina.</span><span class="sxs-lookup"><span data-stu-id="a94cf-239">Sysprep removes any machine-specific information from the VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a94cf-240">Tire um instantâneo ou realize backup de sua VM antes de generalizá-lo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="a94cf-241">Executar sysprep interromperá e desalocará a instância de VM.</span><span class="sxs-lookup"><span data-stu-id="a94cf-241">Running sysprep will stop and deallocate the VM instance.</span></span> <span data-ttu-id="a94cf-242">Siga as etapas abaixo para usar o sysprep em um VHD do sistema operacional Windows.</span><span class="sxs-lookup"><span data-stu-id="a94cf-242">Follow steps below to sysprep a Windows OS VHD.</span></span> <span data-ttu-id="a94cf-243">Observe que executar o comando Sysprep exigirá que você desligue a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a94cf-243">Note that running the Sysprep command will require you to shut down the virtual machine.</span></span> <span data-ttu-id="a94cf-244">Para saber mais sobre o Sysprep, consulte [Visão Geral do Sysprep](http://technet.microsoft.com/library/hh825209.aspx) ou [Referência Técnica do Sysprep](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="a94cf-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="a94cf-245">Abra uma janela de Prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="a94cf-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="a94cf-246">Digite o comando a seguir para abrir o Sysprep:</span><span class="sxs-lookup"><span data-stu-id="a94cf-246">Enter the following command to open Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="a94cf-247">Na Ferramenta de Preparação do Sistema, selecione Entrar no Sistema OOBE, marque a caixa de seleção Generalizar, selecione **Desligar** e, em seguida, clique em **OK** conforme mostrado na imagem abaixo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-247">In the System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select the Generalize check box, select **Shutdown**, and then click **OK**, as shown in the image below.</span></span> <span data-ttu-id="a94cf-248">Sysprep generalizará o sistema operacional e desligar o sistema.</span><span class="sxs-lookup"><span data-stu-id="a94cf-248">Sysprep will generalize the operating system and shut down the system.</span></span>

    ![][1]

<span data-ttu-id="a94cf-249">Para uma VM Ubuntu, use virt-sysprep para obter o mesmo resultado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-249">For an Ubuntu VM, use virt-sysprep to achieve the same.</span></span> <span data-ttu-id="a94cf-250">Consulte [virt sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="a94cf-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="a94cf-251">Consulte também um [software de Provisionamento do Servidor Linux](http://www.cyberciti.biz/tips/server-provisioning-software.html) de fonte aberta para ver outros sistemas operacionais Linux.</span><span class="sxs-lookup"><span data-stu-id="a94cf-251">See also some of the open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-to-create-a-single-vm-instance"></a><span data-ttu-id="a94cf-252">Use um VHD de Sistema Operacional Exclusivo para criar uma única instância de VM</span><span class="sxs-lookup"><span data-stu-id="a94cf-252">Use a unique Operating System VHD to create a single VM instance</span></span>
<span data-ttu-id="a94cf-253">Se você tiver um aplicativo em execução na máquina virtual que exige dados específicos da máquina, não generalize o VHD.</span><span class="sxs-lookup"><span data-stu-id="a94cf-253">If you have an application running on the VM which requires the machine specific data, do not generalize the VHD.</span></span> <span data-ttu-id="a94cf-254">Um VHD não generalizado pode ser usado para criar uma instância VM exclusiva do Azure.</span><span class="sxs-lookup"><span data-stu-id="a94cf-254">A non-generalized VHD can be used to create a unique Azure VM instance.</span></span> <span data-ttu-id="a94cf-255">Por exemplo, se você tiver um Controlador de Domínio em seu VHD, executar o sysprep irá torná-lo inútil como um Controlador de Domínio.</span><span class="sxs-lookup"><span data-stu-id="a94cf-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="a94cf-256">Examine os aplicativos em execução em sua VM e o impacto da execução do sysprep nelas antes de generalizar o VHD.</span><span class="sxs-lookup"><span data-stu-id="a94cf-256">Review the applications running on your VM and the impact of running sysprep on them before generalizing the VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="a94cf-257">Registrar o VHD do disco de dados</span><span class="sxs-lookup"><span data-stu-id="a94cf-257">Register data disk VHD</span></span>
<span data-ttu-id="a94cf-258">Se você tiver discos de dados no Azure a serem migrados, verifique se as VMs que usam esses discos de dados foram desligadas.</span><span class="sxs-lookup"><span data-stu-id="a94cf-258">If you have data disks in Azure to be migrated, you must make sure the VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="a94cf-259">Siga as etapas descritas abaixo para copiar o VHD para o Armazenamento Premium do Azure e registre-o como um disco de dados provisionado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-259">Follow the steps described below to copy VHD to Azure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="a94cf-260">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="a94cf-260">Step 2.</span></span> <span data-ttu-id="a94cf-261">Criar o destino para seu VHD</span><span class="sxs-lookup"><span data-stu-id="a94cf-261">Create the destination for your VHD</span></span>
<span data-ttu-id="a94cf-262">Crie uma conta de armazenamento para manter seus VHDs.</span><span class="sxs-lookup"><span data-stu-id="a94cf-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="a94cf-263">Considere os seguintes pontos ao planejar onde armazenar seus VHDs:</span><span class="sxs-lookup"><span data-stu-id="a94cf-263">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="a94cf-264">O destino da conta de armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="a94cf-264">The target Premium storage account.</span></span>
* <span data-ttu-id="a94cf-265">O local da conta de armazenamento deve ser igual às VMs do Azure compatíveis com o Armazenamento Premium que você criará no estágio final.</span><span class="sxs-lookup"><span data-stu-id="a94cf-265">The storage account location must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="a94cf-266">Você pode copiar para uma nova conta de armazenamento ou planejar usar a mesma conta de armazenamento com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="a94cf-266">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="a94cf-267">Copie e salve a chave da conta de armazenamento da conta de armazenamento de destino para a próxima fase.</span><span class="sxs-lookup"><span data-stu-id="a94cf-267">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="a94cf-268">Para discos de dados, você pode optar por manter alguns discos de dados em uma conta de armazenamento padrão (por exemplo, discos que têm um armazenamento melhor), mas é altamente recomendável mover todos os dados para a carga de trabalho de produção para usar o armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="a94cf-268">For data disks, you can choose to keep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <span data-ttu-id="a94cf-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="a94cf-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="a94cf-270">Copiar o VHD com o AzCopy ou o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a94cf-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="a94cf-271">Você precisará localizar o caminho do contêiner e o armazenamento de chaves de conta para processar qualquer uma dessas duas opções.</span><span class="sxs-lookup"><span data-stu-id="a94cf-271">You will need to find your container path and storage account key to process either of these two options.</span></span> <span data-ttu-id="a94cf-272">A chave de conta de armazenamento e o caminho do contêiner podem ser encontrados em **Portal do Azure** > **Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="a94cf-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="a94cf-273">A URL do contêiner será semelhante a "https://myaccount.blob.core.windows.net/mycontainer/".</span><span class="sxs-lookup"><span data-stu-id="a94cf-273">The container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="a94cf-274">Opção 1: copiar um VHD com o AzCopy (cópia assíncrona)</span><span class="sxs-lookup"><span data-stu-id="a94cf-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="a94cf-275">Usando o AzCopy, é possível carregar o VHD facilmente pela Internet.</span><span class="sxs-lookup"><span data-stu-id="a94cf-275">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="a94cf-276">Dependendo do tamanho dos VHDs, isso pode levar tempo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-276">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="a94cf-277">Lembre-se de verificar os limites de entrada/saída da conta de armazenamento ao usar essa opção.</span><span class="sxs-lookup"><span data-stu-id="a94cf-277">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="a94cf-278">Consulte [Metas de Desempenho e Escalabilidade do Armazenamento do Azure](storage-scalability-targets.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="a94cf-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="a94cf-279">Baixe e instale o AzCopy aqui: [Versão mais recente do AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="a94cf-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="a94cf-280">Abra o PowerShell do Azure e vá para a pasta onde o AzCopy está instalado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-280">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="a94cf-281">Use o comando a seguir para copiar o arquivo VHD de "Origem" para "Destino".</span><span class="sxs-lookup"><span data-stu-id="a94cf-281">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="a94cf-282">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="a94cf-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="a94cf-283">Aqui estão as descrições dos parâmetros usados no comando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="a94cf-283">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="a94cf-284">**/Source: *&lt;source&gt;:*** local da pasta ou URL do contêiner de armazenamento que contém o VHD.</span><span class="sxs-lookup"><span data-stu-id="a94cf-284">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="a94cf-285">**/SourceKey: *&lt;source-account-key&gt;:*** chave de conta de armazenamento de origem.</span><span class="sxs-lookup"><span data-stu-id="a94cf-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="a94cf-286">**/Dest: *&lt;destination&gt;:*** a URL do contêiner de armazenamento para a qual copiar o VHD.</span><span class="sxs-lookup"><span data-stu-id="a94cf-286">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="a94cf-287">**/DestKey: *&lt;dest-account-key&gt;:*** chave de conta de armazenamento de destino.</span><span class="sxs-lookup"><span data-stu-id="a94cf-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="a94cf-288">**/Pattern: *&lt;file-name&gt;:*** especifica o nome do arquivo do VHD a ser copiado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-288">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="a94cf-289">Para obter detalhes sobre como usar a ferramenta AzCopy, consulte [Transferir dados com o Utilitário de Linha de Comando AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="a94cf-289">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="a94cf-290">Opção 2: copiar um VHD com o PowerShell (cópia sincronizada)</span><span class="sxs-lookup"><span data-stu-id="a94cf-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="a94cf-291">Você também pode copiar o arquivo VHD usando o cmdlet do PowerShell Start-AzureStorageBlobCopy.</span><span class="sxs-lookup"><span data-stu-id="a94cf-291">You can also copy the VHD file using the PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="a94cf-292">Use o comando a seguir no Azure PowerShell para copiar o VHD.</span><span class="sxs-lookup"><span data-stu-id="a94cf-292">Use the following command on Azure PowerShell to copy VHD.</span></span> <span data-ttu-id="a94cf-293">Substitua os valores entre <> por valores correspondentes de sua conta de armazenamento de origem e de destino.</span><span class="sxs-lookup"><span data-stu-id="a94cf-293">Replace the values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="a94cf-294">Para usar esse comando, você deve ter um contêiner chamado vhds na conta de armazenamento de destino.</span><span class="sxs-lookup"><span data-stu-id="a94cf-294">To use this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="a94cf-295">Se o contêiner não existir, crie um antes de executar o comando.</span><span class="sxs-lookup"><span data-stu-id="a94cf-295">If the container doesn't exist, create one before running the command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="a94cf-296">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="a94cf-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="a94cf-297"><a name="scenario2"></a>Cenário 2: "estou migrando VMs de outras plataformas para o Armazenamento Premium do Azure".</span><span class="sxs-lookup"><span data-stu-id="a94cf-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>
<span data-ttu-id="a94cf-298">Se você estiver migrando o VHD do Armazenamento em Nuvem não do Azure, primeiro deverá exportar o VHD para um diretório local.</span><span class="sxs-lookup"><span data-stu-id="a94cf-298">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="a94cf-299">Tenha à mão o caminho de origem completo do diretório local em que o VHD é armazenado e use AzCopy para carregá-la no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a94cf-299">Have the complete source path of the local directory where VHD is stored handy, and then using AzCopy to upload it to Azure Storage.</span></span>

#### <a name="step-1-export-vhd-to-a-local-directory"></a><span data-ttu-id="a94cf-300">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="a94cf-300">Step 1.</span></span> <span data-ttu-id="a94cf-301">Exportar o VHD para um diretório local</span><span class="sxs-lookup"><span data-stu-id="a94cf-301">Export VHD to a local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="a94cf-302">Copiar um VHD do AWS</span><span class="sxs-lookup"><span data-stu-id="a94cf-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="a94cf-303">Se você estiver usando o AWS, exporte a instância do EC2 para um VHD em um depósito do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="a94cf-303">If you are using AWS, export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="a94cf-304">Execute as etapas descritas na documentação do Amazon para Exportar instâncias do Amazon EC2, a fim de instalar a ferramenta de interface de linha de comando (CLI) do Amazon EC2. Em seguida, execute o comando create-instance-export-task para exportar a instância do EC2 para um arquivo VHD.</span><span class="sxs-lookup"><span data-stu-id="a94cf-304">Follow the steps described in the Amazon documentation for Exporting Amazon EC2 Instances to install the Amazon EC2 command-line interface (CLI) tool and run the create-instance-export-task command to export the EC2 instance to a VHD file.</span></span> <span data-ttu-id="a94cf-305">Use **VHD** para a variável DISK&#95;IMAGE&#95;FORMAT ao executar o comando **create-instance-export-task**.</span><span class="sxs-lookup"><span data-stu-id="a94cf-305">Be sure to use **VHD** for the DISK&#95;IMAGE&#95;FORMAT variable when running the **create-instance-export-task** command.</span></span> <span data-ttu-id="a94cf-306">O arquivo VHD exportado é salvo no depósito do Amazon S3 designado durante esse processo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-306">The exported VHD file is saved in the Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="a94cf-307">Baixe o arquivo VHD do depósito S3.</span><span class="sxs-lookup"><span data-stu-id="a94cf-307">Download the VHD file from the S3 bucket.</span></span> <span data-ttu-id="a94cf-308">Selecione o arquivo VHD, em seguida **Ações** > **Baixar**.</span><span class="sxs-lookup"><span data-stu-id="a94cf-308">Select the VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="a94cf-309">Copiar um VHD de outra nuvem que não é do Azure</span><span class="sxs-lookup"><span data-stu-id="a94cf-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="a94cf-310">Se você estiver migrando o VHD do Armazenamento em Nuvem não do Azure, primeiro deverá exportar o VHD para um diretório local.</span><span class="sxs-lookup"><span data-stu-id="a94cf-310">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="a94cf-311">Copie o caminho de origem completo do diretório local onde o VHD está armazenado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-311">Copy the complete source path of the local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="a94cf-312">Copiar um VHD do local</span><span class="sxs-lookup"><span data-stu-id="a94cf-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="a94cf-313">Se você estiver migrando o VHD de um ambiente local, você precisará do caminho de origem completo em que o VHD está armazenado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-313">If you are migrating VHD from an on-premises environment, you will need the complete source path where VHD is stored.</span></span> <span data-ttu-id="a94cf-314">O caminho de origem pode ser um compartilhamento de arquivo ou local do servidor.</span><span class="sxs-lookup"><span data-stu-id="a94cf-314">The source path could be a server location or file share.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="a94cf-315">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="a94cf-315">Step 2.</span></span> <span data-ttu-id="a94cf-316">Criar o destino para seu VHD</span><span class="sxs-lookup"><span data-stu-id="a94cf-316">Create the destination for your VHD</span></span>
<span data-ttu-id="a94cf-317">Crie uma conta de armazenamento para manter seus VHDs.</span><span class="sxs-lookup"><span data-stu-id="a94cf-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="a94cf-318">Considere os seguintes pontos ao planejar onde armazenar seus VHDs:</span><span class="sxs-lookup"><span data-stu-id="a94cf-318">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="a94cf-319">A conta de armazenamento de destino pode ser o armazenamento standard ou premium, dependendo do requisito do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-319">The target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="a94cf-320">A região da conta de armazenamento deve ser igual as VMs do Azure compatíveis com o Armazenamento Premium que você criará no estágio final.</span><span class="sxs-lookup"><span data-stu-id="a94cf-320">The storage account region must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="a94cf-321">Você pode copiar para uma nova conta de armazenamento ou planejar usar a mesma conta de armazenamento com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="a94cf-321">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="a94cf-322">Copie e salve a chave da conta de armazenamento da conta de armazenamento de destino para a próxima fase.</span><span class="sxs-lookup"><span data-stu-id="a94cf-322">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="a94cf-323">É altamente recomendável mover todos os dados para a carga de trabalho de produção para usar o armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="a94cf-323">We strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <a name="step-3-upload-the-vhd-to-azure-storage"></a><span data-ttu-id="a94cf-324">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="a94cf-324">Step 3.</span></span> <span data-ttu-id="a94cf-325">Carregar o VHD no Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a94cf-325">Upload the VHD to Azure Storage</span></span>
<span data-ttu-id="a94cf-326">Agora que você tem o VHD no diretório local, pode usar o AzCopy ou o AzurePowerShell para carregar o arquivo .vhd no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a94cf-326">Now that you have your VHD in the local directory, you can use AzCopy or AzurePowerShell to upload the .vhd file to Azure Storage.</span></span> <span data-ttu-id="a94cf-327">Ambas as opções são fornecidas aqui:</span><span class="sxs-lookup"><span data-stu-id="a94cf-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-to-upload-the-vhd-file"></a><span data-ttu-id="a94cf-328">Opção 1: usar Add-AzureVhd do Azure PowerShell para carregar o arquivo .vhd</span><span class="sxs-lookup"><span data-stu-id="a94cf-328">Option 1: Using Azure PowerShell Add-AzureVhd to upload the .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="a94cf-329">Um exemplo <Uri> pode ser ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="a94cf-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="a94cf-330">Um exemplo <FileInfo> pode ser ***"C:\path\to\upload.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="a94cf-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-to-upload-the-vhd-file"></a><span data-ttu-id="a94cf-331">Opção 2: usar o AzCopy para carregar o arquivo .vhd</span><span class="sxs-lookup"><span data-stu-id="a94cf-331">Option 2: Using AzCopy to upload the .vhd file</span></span>
<span data-ttu-id="a94cf-332">Usando o AzCopy, é possível carregar o VHD facilmente pela Internet.</span><span class="sxs-lookup"><span data-stu-id="a94cf-332">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="a94cf-333">Dependendo do tamanho dos VHDs, isso pode levar tempo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-333">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="a94cf-334">Lembre-se de verificar os limites de entrada/saída da conta de armazenamento ao usar essa opção.</span><span class="sxs-lookup"><span data-stu-id="a94cf-334">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="a94cf-335">Consulte [Metas de Desempenho e Escalabilidade do Armazenamento do Azure](storage-scalability-targets.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="a94cf-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="a94cf-336">Baixe e instale o AzCopy aqui: [Versão mais recente do AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="a94cf-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="a94cf-337">Abra o PowerShell do Azure e vá para a pasta onde o AzCopy está instalado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-337">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="a94cf-338">Use o comando a seguir para copiar o arquivo VHD de "Origem" para "Destino".</span><span class="sxs-lookup"><span data-stu-id="a94cf-338">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="a94cf-339">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="a94cf-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="a94cf-340">Aqui estão as descrições dos parâmetros usados no comando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="a94cf-340">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="a94cf-341">**/Source: *&lt;source&gt;:*** local da pasta ou URL do contêiner de armazenamento que contém o VHD.</span><span class="sxs-lookup"><span data-stu-id="a94cf-341">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="a94cf-342">**/SourceKey: *&lt;source-account-key&gt;:*** chave de conta de armazenamento de origem.</span><span class="sxs-lookup"><span data-stu-id="a94cf-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="a94cf-343">**/Dest: *&lt;destination&gt;:*** a URL do contêiner de armazenamento para a qual copiar o VHD.</span><span class="sxs-lookup"><span data-stu-id="a94cf-343">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="a94cf-344">**/DestKey: *&lt;dest-account-key&gt;:*** chave de conta de armazenamento de destino.</span><span class="sxs-lookup"><span data-stu-id="a94cf-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="a94cf-345">**/BlobType: page:** Especifica que o destino é um blob de páginas.</span><span class="sxs-lookup"><span data-stu-id="a94cf-345">**/BlobType: page:** Specifies that the destination is a page blob.</span></span>
   * <span data-ttu-id="a94cf-346">**/Pattern: *&lt;file-name&gt;:*** especifica o nome do arquivo do VHD a ser copiado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-346">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="a94cf-347">Para obter detalhes sobre como usar a ferramenta AzCopy, consulte [Transferir dados com o Utilitário de Linha de Comando AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="a94cf-347">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="a94cf-348">Outras opções para carregar um VHD</span><span class="sxs-lookup"><span data-stu-id="a94cf-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="a94cf-349">Você também pode carregar um VHD para sua conta de armazenamento usando um dos seguintes meios:</span><span class="sxs-lookup"><span data-stu-id="a94cf-349">You can also upload a VHD to your storage account using one of the following means:</span></span>

* [<span data-ttu-id="a94cf-350">API do Blob da Cópia de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a94cf-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="a94cf-351">Carregamento de Blobs do Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a94cf-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="a94cf-352">Referência de API REST do Serviço de Importação/Exportação do Armazenamento</span><span class="sxs-lookup"><span data-stu-id="a94cf-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="a94cf-353">É recomendável usar o Serviço de Importação/Exportação se o tempo de carregamento estimado é de mais de sete dias.</span><span class="sxs-lookup"><span data-stu-id="a94cf-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="a94cf-354">Você pode usar [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) para estimar o tempo com base no tamanho dos dados e na unidade de transferência.</span><span class="sxs-lookup"><span data-stu-id="a94cf-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="a94cf-355">A Importação/Exportação pode ser usada para copiar para a conta de armazenamento standard.</span><span class="sxs-lookup"><span data-stu-id="a94cf-355">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="a94cf-356">Você precisará copiar do armazenamento standard para a conta de armazenamento premium usando uma ferramenta como o AzCopy.</span><span class="sxs-lookup"><span data-stu-id="a94cf-356">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="a94cf-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Criar máquinas virtuais do Azure usando o Armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="a94cf-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="a94cf-358">Depois de o VHD ser carregado ou copiado para a conta de armazenamento desejada, siga as instruções nesta seção para registrar o VHD como uma imagem do sistema operacional ou disco do sistema operacional de acordo com seu cenário, em seguida, crie uma instância de VM a partir dele.</span><span class="sxs-lookup"><span data-stu-id="a94cf-358">After the VHD is uploaded or copied to the desired storage account, follow the instructions in this section to register the VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="a94cf-359">O VHD do disco de dados pode ser anexado à VM assim que criado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-359">The data disk VHD can be attached to the VM once it is created.</span></span>
<span data-ttu-id="a94cf-360">Um exemplo de script de migração é fornecido no fim desta seção.</span><span class="sxs-lookup"><span data-stu-id="a94cf-360">A sample migration script is provided at the end of this section.</span></span> <span data-ttu-id="a94cf-361">Este script simples não corresponde a todos os cenários.</span><span class="sxs-lookup"><span data-stu-id="a94cf-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="a94cf-362">Talvez seja necessário atualizar o script para corresponder a seu cenário específico.</span><span class="sxs-lookup"><span data-stu-id="a94cf-362">You may need to update the script to match with your specific scenario.</span></span> <span data-ttu-id="a94cf-363">Para ver se esse script se aplica a seu cenário, confira abaixo [Um script de migração de exemplo](#a-sample-migration-script).</span><span class="sxs-lookup"><span data-stu-id="a94cf-363">To see if this script applies to your scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="a94cf-364">Lista de verificação</span><span class="sxs-lookup"><span data-stu-id="a94cf-364">Checklist</span></span>
1. <span data-ttu-id="a94cf-365">Aguarde até que a cópia de todos os discos de VHD seja concluída.</span><span class="sxs-lookup"><span data-stu-id="a94cf-365">Wait until all the VHD disks copying is complete.</span></span>
2. <span data-ttu-id="a94cf-366">Verifique se o Armazenamento Premium está disponível na região para a qual você está migrando.</span><span class="sxs-lookup"><span data-stu-id="a94cf-366">Make sure Premium Storage is available in the region you are migrating to.</span></span>
3. <span data-ttu-id="a94cf-367">Decida qual nova série de VM você usará.</span><span class="sxs-lookup"><span data-stu-id="a94cf-367">Decide the new VM series you will be using.</span></span> <span data-ttu-id="a94cf-368">Deve ser compatível com Armazenamento Premium, e o tamanho deve depender da disponibilidade na região e se basear em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="a94cf-368">It should be a Premium Storage capable, and the size should be depending on the availability in the region and based on your needs.</span></span>
4. <span data-ttu-id="a94cf-369">Decida o tamanho exato da VM que você usará.</span><span class="sxs-lookup"><span data-stu-id="a94cf-369">Decide the exact VM size you will use.</span></span> <span data-ttu-id="a94cf-370">O tamanho da VM precisa ser grande o suficiente para dar suporte ao número de discos de dados que você tem.</span><span class="sxs-lookup"><span data-stu-id="a94cf-370">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="a94cf-371">Por exemplo</span><span class="sxs-lookup"><span data-stu-id="a94cf-371">E.g.</span></span> <span data-ttu-id="a94cf-372">, se você tiver quatro discos de dados, a VM deverá ter dois ou mais núcleos.</span><span class="sxs-lookup"><span data-stu-id="a94cf-372">if you have 4 data disks, the VM must have 2 or more cores.</span></span> <span data-ttu-id="a94cf-373">Considere também as necessidades de capacidade de processamento, memória e largura de banda de rede.</span><span class="sxs-lookup"><span data-stu-id="a94cf-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="a94cf-374">Crie uma conta de Armazenamento Premium na região de destino.</span><span class="sxs-lookup"><span data-stu-id="a94cf-374">Create a Premium Storage account in the target region.</span></span> <span data-ttu-id="a94cf-375">Essa é a conta que você usará para a nova VM.</span><span class="sxs-lookup"><span data-stu-id="a94cf-375">This is the account you will use for the new VM.</span></span>
6. <span data-ttu-id="a94cf-376">Tenha os detalhes da VM atual à mão, incluindo a lista de discos e blobs VHD correspondentes.</span><span class="sxs-lookup"><span data-stu-id="a94cf-376">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="a94cf-377">Prepare seu aplicativo para o tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="a94cf-377">Prepare your application for downtime.</span></span> <span data-ttu-id="a94cf-378">Para fazer uma migração limpa, você precisa interromper todo o processamento no sistema atual.</span><span class="sxs-lookup"><span data-stu-id="a94cf-378">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="a94cf-379">Só então você pode colocá-lo em estado consistente, podendo então migrar para a nova plataforma.</span><span class="sxs-lookup"><span data-stu-id="a94cf-379">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="a94cf-380">A duração do tempo de inatividade dependerá da quantidade de dados nos discos para migração.</span><span class="sxs-lookup"><span data-stu-id="a94cf-380">Downtime duration will depend on the amount of data in the disks to migrate.</span></span>

> [!NOTE]
> <span data-ttu-id="a94cf-381">Se você estiver criando uma VM do Azure Resource Manager por meio de um Disco de VHD especializado, confira [este modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) para implantação da VM do Resource Manager usando o disco existente.</span><span class="sxs-lookup"><span data-stu-id="a94cf-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer to [this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="a94cf-382">Registrar seu VHD</span><span class="sxs-lookup"><span data-stu-id="a94cf-382">Register your VHD</span></span>
<span data-ttu-id="a94cf-383">Para criar uma máquina virtual no VHD do sistema operacional ou anexar um disco de dados a uma nova VM, primeiro você deve registrá-los.</span><span class="sxs-lookup"><span data-stu-id="a94cf-383">To create a VM from OS VHD or to attach a data disk to a new VM, you must first register them.</span></span> <span data-ttu-id="a94cf-384">Siga as etapas abaixo, dependendo do cenário do VHD.</span><span class="sxs-lookup"><span data-stu-id="a94cf-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="a94cf-385">VHD do Sistema Operacional Generalizado para criar várias instâncias de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="a94cf-385">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="a94cf-386">Depois do VHD de imagem do sistema operacional generalizado ser carregado para a conta de armazenamento, registre-o como uma **Imagem da VM do Azure** para que você possa criar uma ou mais instâncias de VM a partir dele.</span><span class="sxs-lookup"><span data-stu-id="a94cf-386">After generalized OS image VHD is uploaded to the storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="a94cf-387">Use os seguintes cmdlets do PowerShell para registrar seu VHD como uma imagem do sistema operacional da VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="a94cf-387">Use the following PowerShell cmdlets to register your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="a94cf-388">Forneça a URL completa do contêiner para onde o VHD foi copiado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-388">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="a94cf-389">Copie e salve o nome dessa nova Imagem da VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="a94cf-389">Copy and save the name of this new Azure VM Image.</span></span> <span data-ttu-id="a94cf-390">No exemplo acima, é *OSImageName*.</span><span class="sxs-lookup"><span data-stu-id="a94cf-390">In the example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="a94cf-391">VHD do sistema operacional exclusivo para criar uma instância de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="a94cf-391">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="a94cf-392">Depois do VHD exclusivo do sistema operacional ser carregado para a conta de armazenamento, registre-o como um **Disco do Sistema Operacional do Azure** para que você possa criar uma instância de VM a partir dele.</span><span class="sxs-lookup"><span data-stu-id="a94cf-392">After the unique OS VHD is uploaded to the storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="a94cf-393">Use estes cmdlets do PowerShell para registrar seu VHD como um Disco do sistema operacional do Azure.</span><span class="sxs-lookup"><span data-stu-id="a94cf-393">Use these PowerShell cmdlets to register your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="a94cf-394">Forneça a URL completa do contêiner para onde o VHD foi copiado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-394">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="a94cf-395">Copie e salve o nome desse novo Disco do sistema operacional do Azure.</span><span class="sxs-lookup"><span data-stu-id="a94cf-395">Copy and save the name of this new Azure OS Disk.</span></span> <span data-ttu-id="a94cf-396">No exemplo acima, é *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="a94cf-396">In the example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-to-be-attached-to-new-azure-vm-instances"></a><span data-ttu-id="a94cf-397">VHD do disco de dados a ser anexado à(s) instância(s) de VM(s) do Azure</span><span class="sxs-lookup"><span data-stu-id="a94cf-397">Data disk VHD to be attached to new Azure VM instance(s)</span></span>
<span data-ttu-id="a94cf-398">Depois do VHD do disco de dados ser carregado para a conta de armazenamento, registre-o como um Disco de Dados do Azure para que ele possa ser anexado à sua nova instância VM do Azure da série DS, DSv2 ou GS.</span><span class="sxs-lookup"><span data-stu-id="a94cf-398">After the data disk VHD is uploaded to storage account, register it as an Azure Data Disk so that it can be attached to your new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="a94cf-399">Use estes cmdlets do PowerShell para registrar seu VHD como um Disco de Dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="a94cf-399">Use these PowerShell cmdlets to register your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="a94cf-400">Forneça a URL completa do contêiner para onde o VHD foi copiado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-400">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="a94cf-401">Copie e salve o nome desse novo Disco de Dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="a94cf-401">Copy and save the name of this new Azure Data Disk.</span></span> <span data-ttu-id="a94cf-402">No exemplo acima, é *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="a94cf-402">In the example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="a94cf-403">Criar uma VM com capacidade de Armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="a94cf-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="a94cf-404">Assim que a imagem do sistema operacional ou o disco do sistema operacional for registrado, crie uma nova VM da série DS, DSv2 ou GS.</span><span class="sxs-lookup"><span data-stu-id="a94cf-404">Once the OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="a94cf-405">Você usará a imagem do sistema operacional ou o nome de disco do sistema operacional registrado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-405">You will be using the operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="a94cf-406">Selecione o tipo de VM na camada de Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="a94cf-406">Select the VM type from the Premium Storage tier.</span></span> <span data-ttu-id="a94cf-407">No exemplo abaixo, estamos usando o tamanho de VM *Standard_DS2*.</span><span class="sxs-lookup"><span data-stu-id="a94cf-407">In example below, we are using the *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="a94cf-408">Atualize o tamanho do disco para assegurar que ele corresponda à sua capacidade, requisitos de desempenho e aos tamanhos de disco do Azure disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a94cf-408">Update the disk size to make sure it matches your capacity and performance requirements and the available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="a94cf-409">Execute passo a passo os cmdlets do PowerShell abaixo para criar a nova VM.</span><span class="sxs-lookup"><span data-stu-id="a94cf-409">Follow the step by step PowerShell cmdlets below to create the new VM.</span></span> <span data-ttu-id="a94cf-410">Primeiro, defina os parâmetros comuns:</span><span class="sxs-lookup"><span data-stu-id="a94cf-410">First, set the common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="a94cf-411">Primeiro, crie um serviço de nuvem em que você hospedará suas novas VMs.</span><span class="sxs-lookup"><span data-stu-id="a94cf-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="a94cf-412">Em segundo lugar, dependendo do cenário, crie a instância VM do Azure por meio da imagem do sistema operacional ou do disco do sistema operacional registrado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-412">Next, depending on your scenario, create the Azure VM instance from either the OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="a94cf-413">VHD do Sistema Operacional Generalizado para criar várias instâncias de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="a94cf-413">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="a94cf-414">Crie uma ou mais instâncias de VM do Azure novas da Série DS usando a **Imagem do sistema operacional do Azure** registrada.</span><span class="sxs-lookup"><span data-stu-id="a94cf-414">Create the one or more new DS Series Azure VM instances using the **Azure OS Image** that you registered.</span></span> <span data-ttu-id="a94cf-415">Especifique o nome da Imagem do sistema operacional na configuração da máquina virtual ao criar uma nova máquina, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-415">Specify this OS Image name in the VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="a94cf-416">VHD do sistema operacional exclusivo para criar uma instância de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="a94cf-416">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="a94cf-417">Crie uma nova instância de VM do Azure da série DS usando o **Disco do sistema operacional do Azure** registrado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-417">Create a new DS series Azure VM instance using the **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="a94cf-418">Especifique o nome do Disco do sistema operacional na configuração da máquina virtual ao criar uma nova máquina, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-418">Specify this OS Disk name in the VM configuration when creating the new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="a94cf-419">Especifique outras informações da VM do Azure, como um serviço de nuvem, região, conta de armazenamento, conjunto de disponibilidade e política de cache.</span><span class="sxs-lookup"><span data-stu-id="a94cf-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="a94cf-420">Observe que a instância VM deve estar localizada junto com o sistema operacional ou discos de dados associados, portanto, o serviço de nuvem selecionado, a região e a conta de armazenamento devem estar no mesmo local dos VHDs subjacentes desses discos.</span><span class="sxs-lookup"><span data-stu-id="a94cf-420">Note that the VM instance must be co-located with associated operating system or data disks, so the selected cloud service, region and storage account must all be in the same location as the underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="a94cf-421">Anexar disco de dados</span><span class="sxs-lookup"><span data-stu-id="a94cf-421">Attach data disk</span></span>
<span data-ttu-id="a94cf-422">Por fim, se você registrou os VHDs de disco de dados, anexe-os à nova VM do Azure compatível com Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="a94cf-422">Lastly, if you have registered data disk VHDs, attach them to the new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="a94cf-423">Use o seguinte cmdlet do PowerShell para anexar um disco de dados à nova VM e especifique a política de cache.</span><span class="sxs-lookup"><span data-stu-id="a94cf-423">Use following PowerShell cmdlet to attach data disk to the new VM and specify the caching policy.</span></span> <span data-ttu-id="a94cf-424">No exemplo abaixo, a política de cache é definida como *Somente Leitura*.</span><span class="sxs-lookup"><span data-stu-id="a94cf-424">In example below the caching policy is set to *ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="a94cf-425">Pode haver etapas adicionais necessárias para dar suporte aos aplicativos que não são abrangidas por este guia.</span><span class="sxs-lookup"><span data-stu-id="a94cf-425">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="a94cf-426">Verificação e planejamento de backup</span><span class="sxs-lookup"><span data-stu-id="a94cf-426">Checking and plan backup</span></span>
<span data-ttu-id="a94cf-427">Depois que a nova VM estiver em funcionamento, acesse-a usando a mesma id de logon e senha usadas para a VM original e verifique se tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="a94cf-427">Once the new VM is up and running, access it using the same login id and password is as the original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="a94cf-428">Todas as configurações, incluindo volumes distribuídos, devem estar presentes na nova VM.</span><span class="sxs-lookup"><span data-stu-id="a94cf-428">All the settings, including the striped volumes, would be present in the new VM.</span></span>

<span data-ttu-id="a94cf-429">A última etapa consiste em planejar o backup e a agenda de manutenção para a nova VM com base nas necessidades do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-429">The last step is to plan backup and maintenance schedule for the new VM based on the application's needs.</span></span>

### <span data-ttu-id="a94cf-430"><a name="a-sample-migration-script"></a>Um script de migração de exemplo</span><span class="sxs-lookup"><span data-stu-id="a94cf-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="a94cf-431">Se você tiver várias VMs para migrar, a automação por meio de scripts do PowerShell será útil.</span><span class="sxs-lookup"><span data-stu-id="a94cf-431">If you have multiple VMs to migrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="a94cf-432">A seguir está um script de exemplo que automatiza a migração de uma VM.</span><span class="sxs-lookup"><span data-stu-id="a94cf-432">Following is a sample script that automates the migration of a VM.</span></span> <span data-ttu-id="a94cf-433">Observe que o script abaixo é apenas um exemplo, e algumas suposições são feitas sobre os discos de VM atuais.</span><span class="sxs-lookup"><span data-stu-id="a94cf-433">Note that below script is only an example, and there are few assumptions made about the current VM disks.</span></span> <span data-ttu-id="a94cf-434">Talvez seja necessário atualizar o script para corresponder a seu cenário específico.</span><span class="sxs-lookup"><span data-stu-id="a94cf-434">You may need to update the script to match with your specific scenario.</span></span>

<span data-ttu-id="a94cf-435">As suposições são:</span><span class="sxs-lookup"><span data-stu-id="a94cf-435">The assumptions are:</span></span>

* <span data-ttu-id="a94cf-436">Você está criando VMs clássicas do Azure.</span><span class="sxs-lookup"><span data-stu-id="a94cf-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="a94cf-437">Seus Discos de origem do Sistema Operacional e Discos de Dados de origem estão na mesma conta de armazenamento e no mesmo contêiner.</span><span class="sxs-lookup"><span data-stu-id="a94cf-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="a94cf-438">Se os Discos de SO e Discos de Dados não estiverem no mesmo lugar, você poderá usar o AzCopy ou o Azure PowerShell para copiar VHDs em contêineres e contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a94cf-438">If your OS Disks and Data Disks are not in the same place, you can use AzCopy or Azure PowerShell to copy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="a94cf-439">Confira a etapa anterior: [Copiar VHD com AzCopy ou PowerShell](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="a94cf-439">Refer to the previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="a94cf-440">Editar este script para atender a seu cenário é outra opção, mas recomendamos usar o AzCopy ou o PowerShell, pois é mais fácil e rápido.</span><span class="sxs-lookup"><span data-stu-id="a94cf-440">Editing this script to meet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="a94cf-441">O script de automação é fornecido abaixo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-441">The automation script is provided below.</span></span> <span data-ttu-id="a94cf-442">Substitua o texto por suas informações e atualize o script para corresponder a seu cenário específico.</span><span class="sxs-lookup"><span data-stu-id="a94cf-442">Replace text with your information and update the script to match with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="a94cf-443">Usar o script existente não preserva a configuração de rede da VM de origem.</span><span class="sxs-lookup"><span data-stu-id="a94cf-443">Using the existing script does not preserve the network configuration of your source VM.</span></span> <span data-ttu-id="a94cf-444">Você precisará reconfigurar as configurações de rede em suas VMs migradas.</span><span class="sxs-lookup"><span data-stu-id="a94cf-444">You will need to re-config the networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE to show how to migrate a VM from a standard storage account to a premium storage account. You can customize it according to your specific requirements.

    .Description
    The script will copy the vhds (page blobs) of the source VM to the new storage account.
    And then it will create a new VM from these copied vhds based on the inputs that you specified for the new VM.
    You can modify the script to satisfy your specific requirement, but please be aware of the items specified
    in the Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. THE ENTIRE RISK OF USE, INABILITY TO USE, OR
    RESULTS FROM THE USE OF THIS CODE REMAINS WITH THE USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    To find more information about how to set up Azure PowerShell, refer to the following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # the cloud service name of the VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # The VM name to copy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # The destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # The destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # the destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # the destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # the location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not to copy the os disk, the default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently to report the copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # the name suffix to add to new created disks to avoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import the Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check the Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer to this article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ to connect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if the VM is shut down
    #  Stopping the VM is a required step so that the file system is consistent when you do the copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - The source VM doesn't exist in the current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping the VM is a required step so that the file system is consistent when you do the copy operation. Azure does not support live migration at this time. If you'd like to create a VM from a generalized image, sys-prep the Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish to stop $SourceVMName now? Input 'N' if you want to shut down the VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until the VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName to shut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting the sourve vm to a configuration file, you can restore the original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration to $vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy the vhds of the source vm
    #  You can choose to copy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly to be $false. The default is to copy only data disk vhds
    #  and the new VM will boot from the original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering the data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in the destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need to copy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting the source VM so that dest VM can boot
        # from the same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose to copy data disks only. Moving VM requires removing the original VM (the disks and backing vhd files will NOT be deleted) so that the new VM can boot from the same vhd. This is an irreversible action. Do you wish to proceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing the original VM (the vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill the OS disk is released by source VM. This may take up to several minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy the os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update the media link to point to the target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy to complete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  the new VM can be created from the copied disks or the original os disk.
    #  You can ddd your own logic here to satisfy your specific requirements of the vm.
    #######################################################################

    # Create a VM from the existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached the copied data disks to the new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of the source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want to add more custimization to the new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="a94cf-445"><a name="optimization"></a>Otimização</span><span class="sxs-lookup"><span data-stu-id="a94cf-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="a94cf-446">A configuração atual da VM pode ser personalizada especificamente para funcionar bem com discos Padrão.</span><span class="sxs-lookup"><span data-stu-id="a94cf-446">Your current VM configuration may be customized specifically to work well with Standard disks.</span></span> <span data-ttu-id="a94cf-447">Por exemplo, para aumentar o desempenho usando vários discos em um volume distribuído.</span><span class="sxs-lookup"><span data-stu-id="a94cf-447">For instance, to increase the performance by using many disks in a striped volume.</span></span> <span data-ttu-id="a94cf-448">Por exemplo, em vez de usar quatro discos separadamente no Armazenamento Premium, você poderá otimizar o custo tendo um único disco.</span><span class="sxs-lookup"><span data-stu-id="a94cf-448">For example, instead of using 4 disks separately on Premium Storage, you may be able to optimize the cost by having a single disk.</span></span> <span data-ttu-id="a94cf-449">Otimizações como essa precisam ser tratadas caso a caso e exigem etapas personalizadas após a migração.</span><span class="sxs-lookup"><span data-stu-id="a94cf-449">Optimizations like this need to be handled on a case by case basis and require custom steps after the migration.</span></span> <span data-ttu-id="a94cf-450">Observe também que esse processo pode não funcionar bem para bancos de dados e aplicativos que dependem do layout de disco definido na configuração.</span><span class="sxs-lookup"><span data-stu-id="a94cf-450">Also, note that this process may not well work for databases and applications that depend on the disk layout defined in the setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="a94cf-451">Preparação</span><span class="sxs-lookup"><span data-stu-id="a94cf-451">Preparation</span></span>
1. <span data-ttu-id="a94cf-452">Conclua a Migração Simples, conforme descrito na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="a94cf-452">Complete the Simple Migration as described in the earlier section.</span></span> <span data-ttu-id="a94cf-453">Serão executadas otimizações na nova VM após a migração.</span><span class="sxs-lookup"><span data-stu-id="a94cf-453">Optimizations will be performed on the new VM after the migration.</span></span>
2. <span data-ttu-id="a94cf-454">Defina os novos tamanhos de disco necessários para a configuração otimizada.</span><span class="sxs-lookup"><span data-stu-id="a94cf-454">Define the new disk sizes needed for the optimized configuration.</span></span>
3. <span data-ttu-id="a94cf-455">Determine o mapeamento dos volumes/discos atuais para as especificações do novo disco.</span><span class="sxs-lookup"><span data-stu-id="a94cf-455">Determine mapping of the current disks/volumes to the new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="a94cf-456">Etapas de execução</span><span class="sxs-lookup"><span data-stu-id="a94cf-456">Execution steps</span></span>
1. <span data-ttu-id="a94cf-457">Crie os novos discos com os tamanhos corretos na VM de Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="a94cf-457">Create the new disks with the right sizes on the Premium Storage VM.</span></span>
2. <span data-ttu-id="a94cf-458">Faça logon na VM e copie os dados do volume atual para o novo disco que está mapeado para esse volume.</span><span class="sxs-lookup"><span data-stu-id="a94cf-458">Login to the VM and copy the data from the current volume to the new disk that maps to that volume.</span></span> <span data-ttu-id="a94cf-459">Faça isso para todos os volumes atuais que precisam ser mapeados para um novo disco.</span><span class="sxs-lookup"><span data-stu-id="a94cf-459">Do this for all the current volumes that need to map to a new disk.</span></span>
3. <span data-ttu-id="a94cf-460">Em seguida, altere as configurações de aplicativo para alternar para os novos discos e desanexe os volumes antigos.</span><span class="sxs-lookup"><span data-stu-id="a94cf-460">Next, change the application settings to switch to the new disks, and detach the old volumes.</span></span>

<span data-ttu-id="a94cf-461">Para ajustar o aplicativo para melhorar o desempenho de disco, confira [Otimizar o desempenho do aplicativo](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="a94cf-461">For tuning the application for better disk performance, please refer to [Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="a94cf-462">Migrações de aplicativos</span><span class="sxs-lookup"><span data-stu-id="a94cf-462">Application migrations</span></span>
<span data-ttu-id="a94cf-463">Bancos de dados e outros aplicativos complexos podem exigir etapas especiais, conforme definido pelo provedor do aplicativo para a migração.</span><span class="sxs-lookup"><span data-stu-id="a94cf-463">Databases and other complex applications may require special steps as defined by the application provider for the migration.</span></span> <span data-ttu-id="a94cf-464">Consulte a documentação do respectivo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a94cf-464">Please refer to respective application documentation.</span></span> <span data-ttu-id="a94cf-465">Por exemplo</span><span class="sxs-lookup"><span data-stu-id="a94cf-465">E.g.</span></span> <span data-ttu-id="a94cf-466">, normalmente, bancos de dados podem ser migrados por meio de backup e restauração.</span><span class="sxs-lookup"><span data-stu-id="a94cf-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a94cf-467">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a94cf-467">Next steps</span></span>
<span data-ttu-id="a94cf-468">Consulte as seguintes fontes para cenários específicos de migração de máquinas virtuais:</span><span class="sxs-lookup"><span data-stu-id="a94cf-468">See the following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="a94cf-469">Migrar Máquinas Virtuais do Azure entre as Contas de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="a94cf-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="a94cf-470">Crie e carregue um VHD do Windows Server no Azure.</span><span class="sxs-lookup"><span data-stu-id="a94cf-470">Create and upload a Windows Server VHD to Azure.</span></span>](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="a94cf-471">Criando e Carregando um Disco Rígido Virtual que Contém o Sistema Operacional Linux</span><span class="sxs-lookup"><span data-stu-id="a94cf-471">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="a94cf-472">Migrando Máquinas Virtuais do Amazon AWS para o Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a94cf-472">Migrating Virtual Machines from Amazon AWS to Microsoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="a94cf-473">Confira também as fontes a seguir para saber mais sobre o Armazenamento do Azure e as Máquinas Virtuais do Azure:</span><span class="sxs-lookup"><span data-stu-id="a94cf-473">Also, see the following resources to learn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="a94cf-474">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a94cf-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="a94cf-475">Máquinas Virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="a94cf-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="a94cf-476">Armazenamento Premium: Armazenamento de Alto Desempenho para as Cargas de Trabalho da Máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="a94cf-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
