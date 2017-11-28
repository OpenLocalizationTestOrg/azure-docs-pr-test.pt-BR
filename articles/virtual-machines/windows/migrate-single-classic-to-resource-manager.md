---
title: "Migrar uma VM clássica para uma VM de disco gerenciado do ARM | Microsoft Docs"
description: "Migre uma única VM do Azure do modelo de implantação clássico para Managed Disksno modelo de implantação do Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 82389834d85981c0ed71bdcc891fbfdbe1377654
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manually-migrate-a-classic-vm-to-a-new-arm-managed-disk-vm-from-the-vhd"></a><span data-ttu-id="4875d-103">Migrar manualmente uma VM clássica para uma nova VM de disco gerenciado do ARM no VHD</span><span class="sxs-lookup"><span data-stu-id="4875d-103">Manually migrate a Classic VM to a new ARM Managed Disk VM from the VHD</span></span> 


<span data-ttu-id="4875d-104">Esta seção ajuda você a migrar suas VMs do Azure existentes do modelo de implantação clássico para [Managed Disks](managed-disks-overview.md) no modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4875d-104">This section helps you to migrate your existing Azure VMs from the classic deployment model to [Managed Disks](managed-disks-overview.md) in the Resource Manager deployment model.</span></span>


## <a name="plan-for-the-migration-to-managed-disks"></a><span data-ttu-id="4875d-105">Como planejar a migração para os Managed Disks</span><span class="sxs-lookup"><span data-stu-id="4875d-105">Plan for the migration to Managed Disks</span></span>

<span data-ttu-id="4875d-106">Esta seção ajuda você a tomar a melhor decisão sobre a VM e os tipos de disco.</span><span class="sxs-lookup"><span data-stu-id="4875d-106">This section helps you to make the best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="4875d-107">Local padrão</span><span class="sxs-lookup"><span data-stu-id="4875d-107">Location</span></span>

<span data-ttu-id="4875d-108">Escolha um local onde os Azure Managed Disks estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4875d-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="4875d-109">Se você estiver migrando para Managed Disks Premium, verifique também se o armazenamento premium está disponível na região que você pretende migrar.</span><span class="sxs-lookup"><span data-stu-id="4875d-109">If you are migrating to Premium Managed Disks, also ensure that Premium storage is available in the region where you are planning to migrate to.</span></span> <span data-ttu-id="4875d-110">Confira [Serviços do Azure por região](https://azure.microsoft.com/regions/#services) para obter informações atualizadas sobre as localizações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4875d-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="4875d-111">Tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="4875d-111">VM sizes</span></span>

<span data-ttu-id="4875d-112">Se você estiver migrando para Managed Disks Premium, será necessário atualizar o tamanho da VM para um tamanho compatível com o armazenamento premium disponível na região onde a VM está localizada.</span><span class="sxs-lookup"><span data-stu-id="4875d-112">If you are migrating to Premium Managed Disks, you have to update the size of the VM to Premium Storage capable size available in the region where VM is located.</span></span> <span data-ttu-id="4875d-113">Examine os tamanhos de VM que são compatíveis com o armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="4875d-113">Review the VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="4875d-114">As especificações de tamanho de VM do Azure são listadas em [Tamanhos para máquinas virtuais](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="4875d-114">The Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="4875d-115">Examine as características de desempenho das máquinas virtuais que funcionam com o Armazenamento Premium e escolha o tamanho de VM mais apropriado que melhor atende à sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="4875d-115">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="4875d-116">Certifique-se de que há largura de banda suficiente disponível na sua VM para direcionar o tráfego de disco.</span><span class="sxs-lookup"><span data-stu-id="4875d-116">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="4875d-117">Tamanhos do disco</span><span class="sxs-lookup"><span data-stu-id="4875d-117">Disk sizes</span></span>

<span data-ttu-id="4875d-118">**Managed Disks Premium**</span><span class="sxs-lookup"><span data-stu-id="4875d-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="4875d-119">Há sete tipos de discos Gerenciados premium que podem ser usados com sua VM e cada um tem IOPs e limites de taxa de transferência específicos.</span><span class="sxs-lookup"><span data-stu-id="4875d-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="4875d-120">Leve em consideração esses limites ao escolher o tipo de disco premium para sua VM com base nas necessidades de seu aplicativo em termos de capacidade, desempenho, escalabilidade e cargas de pico.</span><span class="sxs-lookup"><span data-stu-id="4875d-120">Consider these limits when choosing the Premium disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="4875d-121">Tipo de discos premium</span><span class="sxs-lookup"><span data-stu-id="4875d-121">Premium Disks Type</span></span>  | <span data-ttu-id="4875d-122">P4</span><span class="sxs-lookup"><span data-stu-id="4875d-122">P4</span></span>    | <span data-ttu-id="4875d-123">P6</span><span class="sxs-lookup"><span data-stu-id="4875d-123">P6</span></span>    | <span data-ttu-id="4875d-124">P10</span><span class="sxs-lookup"><span data-stu-id="4875d-124">P10</span></span>   | <span data-ttu-id="4875d-125">P20</span><span class="sxs-lookup"><span data-stu-id="4875d-125">P20</span></span>   | <span data-ttu-id="4875d-126">P30</span><span class="sxs-lookup"><span data-stu-id="4875d-126">P30</span></span>   | <span data-ttu-id="4875d-127">P40</span><span class="sxs-lookup"><span data-stu-id="4875d-127">P40</span></span>   | <span data-ttu-id="4875d-128">P50</span><span class="sxs-lookup"><span data-stu-id="4875d-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="4875d-129">Tamanho do disco</span><span class="sxs-lookup"><span data-stu-id="4875d-129">Disk size</span></span>           | <span data-ttu-id="4875d-130">128 GB</span><span class="sxs-lookup"><span data-stu-id="4875d-130">128 GB</span></span>| <span data-ttu-id="4875d-131">512 GB</span><span class="sxs-lookup"><span data-stu-id="4875d-131">512 GB</span></span>| <span data-ttu-id="4875d-132">128 GB</span><span class="sxs-lookup"><span data-stu-id="4875d-132">128 GB</span></span>| <span data-ttu-id="4875d-133">512 GB</span><span class="sxs-lookup"><span data-stu-id="4875d-133">512 GB</span></span>            | <span data-ttu-id="4875d-134">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="4875d-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="4875d-135">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="4875d-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="4875d-136">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="4875d-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="4875d-137">IOPS por disco</span><span class="sxs-lookup"><span data-stu-id="4875d-137">IOPS per disk</span></span>       | <span data-ttu-id="4875d-138">120</span><span class="sxs-lookup"><span data-stu-id="4875d-138">120</span></span>   | <span data-ttu-id="4875d-139">240</span><span class="sxs-lookup"><span data-stu-id="4875d-139">240</span></span>   | <span data-ttu-id="4875d-140">500</span><span class="sxs-lookup"><span data-stu-id="4875d-140">500</span></span>   | <span data-ttu-id="4875d-141">2.300</span><span class="sxs-lookup"><span data-stu-id="4875d-141">2300</span></span>              | <span data-ttu-id="4875d-142">5.000</span><span class="sxs-lookup"><span data-stu-id="4875d-142">5000</span></span>              | <span data-ttu-id="4875d-143">7500</span><span class="sxs-lookup"><span data-stu-id="4875d-143">7500</span></span>              | <span data-ttu-id="4875d-144">7500</span><span class="sxs-lookup"><span data-stu-id="4875d-144">7500</span></span>              | 
| <span data-ttu-id="4875d-145">Taxa de transferência por disco</span><span class="sxs-lookup"><span data-stu-id="4875d-145">Throughput per disk</span></span> | <span data-ttu-id="4875d-146">25 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="4875d-146">25 MB per second</span></span>  | <span data-ttu-id="4875d-147">50 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="4875d-147">50 MB per second</span></span>  | <span data-ttu-id="4875d-148">100 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="4875d-148">100 MB per second</span></span> | <span data-ttu-id="4875d-149">150 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="4875d-149">150 MB per second</span></span> | <span data-ttu-id="4875d-150">200 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="4875d-150">200 MB per second</span></span> | <span data-ttu-id="4875d-151">250 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="4875d-151">250 MB per second</span></span> | <span data-ttu-id="4875d-152">250 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="4875d-152">250 MB per second</span></span> | 

<span data-ttu-id="4875d-153">**Managed Disks Standard**</span><span class="sxs-lookup"><span data-stu-id="4875d-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="4875d-154">Há sete tipos de discos Gerenciados Padrão que podem ser usados com sua VM.</span><span class="sxs-lookup"><span data-stu-id="4875d-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="4875d-155">Cada um deles tem uma capacidade diferente, mas com os mesmos limites de taxa de transferência e IOPS.</span><span class="sxs-lookup"><span data-stu-id="4875d-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="4875d-156">Escolha o tipo de discos gerenciados Standard com base nas necessidades de capacidade do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4875d-156">Choose the type of Standard Managed disks based on the capacity needs of your application.</span></span>

| <span data-ttu-id="4875d-157">Tipo de disco Standard</span><span class="sxs-lookup"><span data-stu-id="4875d-157">Standard Disk Type</span></span>  | <span data-ttu-id="4875d-158">S4</span><span class="sxs-lookup"><span data-stu-id="4875d-158">S4</span></span>               | <span data-ttu-id="4875d-159">S6</span><span class="sxs-lookup"><span data-stu-id="4875d-159">S6</span></span>               | <span data-ttu-id="4875d-160">S10</span><span class="sxs-lookup"><span data-stu-id="4875d-160">S10</span></span>              | <span data-ttu-id="4875d-161">S20</span><span class="sxs-lookup"><span data-stu-id="4875d-161">S20</span></span>              | <span data-ttu-id="4875d-162">S30</span><span class="sxs-lookup"><span data-stu-id="4875d-162">S30</span></span>              | <span data-ttu-id="4875d-163">S40</span><span class="sxs-lookup"><span data-stu-id="4875d-163">S40</span></span>              | <span data-ttu-id="4875d-164">S50</span><span class="sxs-lookup"><span data-stu-id="4875d-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="4875d-165">Tamanho do disco</span><span class="sxs-lookup"><span data-stu-id="4875d-165">Disk size</span></span>           | <span data-ttu-id="4875d-166">30 GB</span><span class="sxs-lookup"><span data-stu-id="4875d-166">30 GB</span></span>            | <span data-ttu-id="4875d-167">64 GB</span><span class="sxs-lookup"><span data-stu-id="4875d-167">64 GB</span></span>            | <span data-ttu-id="4875d-168">128 GB</span><span class="sxs-lookup"><span data-stu-id="4875d-168">128 GB</span></span>           | <span data-ttu-id="4875d-169">512 GB</span><span class="sxs-lookup"><span data-stu-id="4875d-169">512 GB</span></span>           | <span data-ttu-id="4875d-170">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="4875d-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="4875d-171">2048 GB (2TB)</span><span class="sxs-lookup"><span data-stu-id="4875d-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="4875d-172">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="4875d-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="4875d-173">IOPS por disco</span><span class="sxs-lookup"><span data-stu-id="4875d-173">IOPS per disk</span></span>       | <span data-ttu-id="4875d-174">500</span><span class="sxs-lookup"><span data-stu-id="4875d-174">500</span></span>              | <span data-ttu-id="4875d-175">500</span><span class="sxs-lookup"><span data-stu-id="4875d-175">500</span></span>              | <span data-ttu-id="4875d-176">500</span><span class="sxs-lookup"><span data-stu-id="4875d-176">500</span></span>              | <span data-ttu-id="4875d-177">500</span><span class="sxs-lookup"><span data-stu-id="4875d-177">500</span></span>              | <span data-ttu-id="4875d-178">500</span><span class="sxs-lookup"><span data-stu-id="4875d-178">500</span></span>              | <span data-ttu-id="4875d-179">500</span><span class="sxs-lookup"><span data-stu-id="4875d-179">500</span></span>             | <span data-ttu-id="4875d-180">500</span><span class="sxs-lookup"><span data-stu-id="4875d-180">500</span></span>              | 
| <span data-ttu-id="4875d-181">Taxa de transferência por disco</span><span class="sxs-lookup"><span data-stu-id="4875d-181">Throughput per disk</span></span> | <span data-ttu-id="4875d-182">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="4875d-182">60 MB per second</span></span> | <span data-ttu-id="4875d-183">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="4875d-183">60 MB per second</span></span> | <span data-ttu-id="4875d-184">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="4875d-184">60 MB per second</span></span> | <span data-ttu-id="4875d-185">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="4875d-185">60 MB per second</span></span> | <span data-ttu-id="4875d-186">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="4875d-186">60 MB per second</span></span> | <span data-ttu-id="4875d-187">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="4875d-187">60 MB per second</span></span> | <span data-ttu-id="4875d-188">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="4875d-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="4875d-189">Política de cache de disco</span><span class="sxs-lookup"><span data-stu-id="4875d-189">Disk caching policy</span></span> 

<span data-ttu-id="4875d-190">**Managed Disks Premium**</span><span class="sxs-lookup"><span data-stu-id="4875d-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="4875d-191">Por padrão, a política de cache de disco é *Somente leitura* para todos os discos de dados Premium e *Leitura e gravação* para o disco de sistema operacional Premium anexado à VM.</span><span class="sxs-lookup"><span data-stu-id="4875d-191">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="4875d-192">Esta definição de configuração é recomendável para atingir o desempenho ideal de leituras de entrada e saída dos seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="4875d-192">This configuration setting is recommended to achieve the optimal performance for your application’s IOs.</span></span> <span data-ttu-id="4875d-193">Para discos de dados de gravação intensa ou somente gravação (como arquivos de log do SQL Server), desabilite o cache de disco para que possa obter o melhor desempenho do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4875d-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="4875d-194">Preços</span><span class="sxs-lookup"><span data-stu-id="4875d-194">Pricing</span></span>

<span data-ttu-id="4875d-195">Confira os [preços dos Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="4875d-195">Review the [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="4875d-196">Os preços dos Managed Disks Premium são iguais aos dos discos não gerenciados premium.</span><span class="sxs-lookup"><span data-stu-id="4875d-196">Pricing of Premium Managed Disks is same as the Premium Unmanaged Disks.</span></span> <span data-ttu-id="4875d-197">No entanto, os preços dos Managed Disks Standard são diferentes dos discos não gerenciados Standard.</span><span class="sxs-lookup"><span data-stu-id="4875d-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="4875d-198">Lista de verificação</span><span class="sxs-lookup"><span data-stu-id="4875d-198">Checklist</span></span>

1.  <span data-ttu-id="4875d-199">Se você estiver migrando para Managed Disks Premium, verifique se estão disponíveis na região para onde pretende migrar.</span><span class="sxs-lookup"><span data-stu-id="4875d-199">If you are migrating to Premium Managed Disks, make sure it is available in the region you are migrating to.</span></span>

2.  <span data-ttu-id="4875d-200">Decida qual nova série de VM você usará.</span><span class="sxs-lookup"><span data-stu-id="4875d-200">Decide the new VM series you will be using.</span></span> <span data-ttu-id="4875d-201">Se você estiver migrando para Managed Disks Premium, use uma capacidade de armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="4875d-201">It should be a Premium Storage capable if you are migrating to Premium Managed Disks.</span></span>

3.  <span data-ttu-id="4875d-202">Decida o tamanho exato da VM que será usada, a região para qual você migrará deve ter esse mesmo tamanho disponível.</span><span class="sxs-lookup"><span data-stu-id="4875d-202">Decide the exact VM size you will use which are available in the region you are migrating to.</span></span> <span data-ttu-id="4875d-203">O tamanho da VM precisa ser grande o suficiente para dar suporte ao número de discos de dados que você tem.</span><span class="sxs-lookup"><span data-stu-id="4875d-203">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="4875d-204">Por exemplo, se você tem quatro discos de dados, a VM deve ter dois ou mais núcleos.</span><span class="sxs-lookup"><span data-stu-id="4875d-204">For example, if you have four data disks, the VM must have two or more cores.</span></span> <span data-ttu-id="4875d-205">Considere também as necessidades de capacidade de processamento, memória e largura de banda de rede.</span><span class="sxs-lookup"><span data-stu-id="4875d-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="4875d-206">Tenha os detalhes da VM atual à mão, incluindo a lista de discos e blobs VHD correspondentes.</span><span class="sxs-lookup"><span data-stu-id="4875d-206">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="4875d-207">Prepare seu aplicativo para o tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="4875d-207">Prepare your application for downtime.</span></span> <span data-ttu-id="4875d-208">Para fazer uma migração limpa, você precisa interromper todo o processamento no sistema atual.</span><span class="sxs-lookup"><span data-stu-id="4875d-208">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="4875d-209">Só então você pode colocá-lo em estado consistente, podendo então migrar para a nova plataforma.</span><span class="sxs-lookup"><span data-stu-id="4875d-209">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="4875d-210">A duração do tempo de inatividade depende da quantidade de dados nos discos para migração.</span><span class="sxs-lookup"><span data-stu-id="4875d-210">Downtime duration depends on the amount of data in the disks to migrate.</span></span>


## <a name="migrate-the-vm"></a><span data-ttu-id="4875d-211">Migração da VM</span><span class="sxs-lookup"><span data-stu-id="4875d-211">Migrate the VM</span></span>

<span data-ttu-id="4875d-212">Prepare seu aplicativo para o tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="4875d-212">Prepare your application for downtime.</span></span> <span data-ttu-id="4875d-213">Para fazer uma migração limpa, você precisa interromper todo o processamento no sistema atual.</span><span class="sxs-lookup"><span data-stu-id="4875d-213">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="4875d-214">Só então você pode colocá-lo em estado consistente, podendo então migrar para a nova plataforma.</span><span class="sxs-lookup"><span data-stu-id="4875d-214">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="4875d-215">A duração do tempo de inatividade depende da quantidade de dados nos discos para migração.</span><span class="sxs-lookup"><span data-stu-id="4875d-215">Downtime duration depends the amount of data in the disks to migrate.</span></span>


1.  <span data-ttu-id="4875d-216">Primeiro, defina os parâmetros comuns:</span><span class="sxs-lookup"><span data-stu-id="4875d-216">First, set the common parameters:</span></span>

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  <span data-ttu-id="4875d-217">Crie um disco de sistema operacional gerenciado usando o VHD da VM de modelo clássico.</span><span class="sxs-lookup"><span data-stu-id="4875d-217">Create a managed OS disk using the VHD from the classic VM.</span></span>

    <span data-ttu-id="4875d-218">Confira se você forneceu o URI completo do VHD do sistema operacional para o parâmetro $osVhdUri.</span><span class="sxs-lookup"><span data-stu-id="4875d-218">Ensure that you have provided the complete URI of the OS VHD to the $osVhdUri parameter.</span></span> <span data-ttu-id="4875d-219">Além disso, insira **-AccountType** como **PremiumLRS** ou **StandardLRS** com base no tipo dos discos (Premium ou Standard) que você está migrando.</span><span class="sxs-lookup"><span data-stu-id="4875d-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="4875d-220">Anexe o disco do sistema operacional para a nova VM.</span><span class="sxs-lookup"><span data-stu-id="4875d-220">Attach the OS disk to the new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="4875d-221">Crie um disco de dados gerenciados do arquivo VHD de dados e o adicione à nova VM.</span><span class="sxs-lookup"><span data-stu-id="4875d-221">Create a managed data disk from the data VHD file and add it to the new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="4875d-222">Crie a nova VM definindo o IP público, a rede virtual e o NIC.</span><span class="sxs-lookup"><span data-stu-id="4875d-222">Create the new VM by setting public IP, Virtual Network and NIC.</span></span>

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
><span data-ttu-id="4875d-223">Pode haver etapas adicionais necessárias para dar suporte aos aplicativos que não são abrangidas por este guia.</span><span class="sxs-lookup"><span data-stu-id="4875d-223">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="4875d-224">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4875d-224">Next steps</span></span>

- <span data-ttu-id="4875d-225">Conectar-se à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4875d-225">Connect to the virtual machine.</span></span> <span data-ttu-id="4875d-226">Para obter instruções, consulte [Como se conectar e fazer logon em uma máquina virtual do Azure executando o Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4875d-226">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

