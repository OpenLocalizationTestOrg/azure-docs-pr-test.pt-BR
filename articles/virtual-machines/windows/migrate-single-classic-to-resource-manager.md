---
title: "aaaMigrate tooan uma VM clássico VM do ARM gerenciados disco | Microsoft Docs"
description: "Migrar uma VM do Azure de implantação clássico Olá tooManaged discos no modelo de implantação do Gerenciador de recursos de saudação do modelo."
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
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a><span data-ttu-id="74741-103">Migrar manualmente um VM clássico tooa nova ARM gerenciados disco VM da saudação VHD</span><span class="sxs-lookup"><span data-stu-id="74741-103">Manually migrate a Classic VM tooa new ARM Managed Disk VM from hello VHD</span></span> 


<span data-ttu-id="74741-104">Esta seção ajuda você toomigrate suas VMs do Azure existente do modelo de implantação clássico Olá muito[discos gerenciados](managed-disks-overview.md) no modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="74741-104">This section helps you toomigrate your existing Azure VMs from hello classic deployment model too[Managed Disks](managed-disks-overview.md) in hello Resource Manager deployment model.</span></span>


## <a name="plan-for-hello-migration-toomanaged-disks"></a><span data-ttu-id="74741-105">Planejar a migração de saudação do tooManaged discos</span><span class="sxs-lookup"><span data-stu-id="74741-105">Plan for hello migration tooManaged Disks</span></span>

<span data-ttu-id="74741-106">Esta seção Ajuda toomake Olá melhor decisão sobre tipos de VM e disco.</span><span class="sxs-lookup"><span data-stu-id="74741-106">This section helps you toomake hello best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="74741-107">Local</span><span class="sxs-lookup"><span data-stu-id="74741-107">Location</span></span>

<span data-ttu-id="74741-108">Escolha um local onde o Azure Managed Disks estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="74741-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="74741-109">Se você estiver migrando tooPremium gerenciados discos, também Verifique se o armazenamento Premium está disponível na região Olá onde você está planejando toomigrate para.</span><span class="sxs-lookup"><span data-stu-id="74741-109">If you are migrating tooPremium Managed Disks, also ensure that Premium storage is available in hello region where you are planning toomigrate to.</span></span> <span data-ttu-id="74741-110">Confira [Serviços do Azure por região](https://azure.microsoft.com/regions/#services) para obter informações atualizadas sobre as localizações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="74741-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="74741-111">Tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="74741-111">VM sizes</span></span>

<span data-ttu-id="74741-112">Se você estiver migrando tooPremium gerenciados discos, você tem tooupdate tamanho de saudação do hello VM tooPremium tamanho com capacidade de armazenamento disponível na região Olá onde a VM está localizada.</span><span class="sxs-lookup"><span data-stu-id="74741-112">If you are migrating tooPremium Managed Disks, you have tooupdate hello size of hello VM tooPremium Storage capable size available in hello region where VM is located.</span></span> <span data-ttu-id="74741-113">Examine os tamanhos de VM Olá que são compatíveis com um armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="74741-113">Review hello VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="74741-114">especificações de tamanho de VM do Azure Olá são listadas na [tamanhos das máquinas virtuais](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="74741-114">hello Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="74741-115">Examine as características de desempenho de saudação de máquinas virtuais que funcionam com o armazenamento Premium e escolha o tamanho VM mais apropriado hello mais adequada para sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="74741-115">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="74741-116">Certifique-se de que há largura de banda suficiente disponível no seu tráfego de disco VM toodrive hello.</span><span class="sxs-lookup"><span data-stu-id="74741-116">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="74741-117">Tamanhos do disco</span><span class="sxs-lookup"><span data-stu-id="74741-117">Disk sizes</span></span>

<span data-ttu-id="74741-118">**Managed Disks Premium**</span><span class="sxs-lookup"><span data-stu-id="74741-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="74741-119">Há sete tipos de discos Gerenciados premium que podem ser usados com sua VM e cada um tem IOPs e limites de taxa de transferência específicos.</span><span class="sxs-lookup"><span data-stu-id="74741-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="74741-120">Considere esses limites ao escolher Olá tipo de disco Premium para sua VM com base nas necessidades de saudação do seu aplicativo em termos de capacidade, escalabilidade e desempenho e cargas de pico.</span><span class="sxs-lookup"><span data-stu-id="74741-120">Consider these limits when choosing hello Premium disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="74741-121">Tipo de discos premium</span><span class="sxs-lookup"><span data-stu-id="74741-121">Premium Disks Type</span></span>  | <span data-ttu-id="74741-122">P4</span><span class="sxs-lookup"><span data-stu-id="74741-122">P4</span></span>    | <span data-ttu-id="74741-123">P6</span><span class="sxs-lookup"><span data-stu-id="74741-123">P6</span></span>    | <span data-ttu-id="74741-124">P10</span><span class="sxs-lookup"><span data-stu-id="74741-124">P10</span></span>   | <span data-ttu-id="74741-125">P20</span><span class="sxs-lookup"><span data-stu-id="74741-125">P20</span></span>   | <span data-ttu-id="74741-126">P30</span><span class="sxs-lookup"><span data-stu-id="74741-126">P30</span></span>   | <span data-ttu-id="74741-127">P40</span><span class="sxs-lookup"><span data-stu-id="74741-127">P40</span></span>   | <span data-ttu-id="74741-128">P50</span><span class="sxs-lookup"><span data-stu-id="74741-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="74741-129">Tamanho do disco</span><span class="sxs-lookup"><span data-stu-id="74741-129">Disk size</span></span>           | <span data-ttu-id="74741-130">128 GB</span><span class="sxs-lookup"><span data-stu-id="74741-130">128 GB</span></span>| <span data-ttu-id="74741-131">512 GB</span><span class="sxs-lookup"><span data-stu-id="74741-131">512 GB</span></span>| <span data-ttu-id="74741-132">128 GB</span><span class="sxs-lookup"><span data-stu-id="74741-132">128 GB</span></span>| <span data-ttu-id="74741-133">512 GB</span><span class="sxs-lookup"><span data-stu-id="74741-133">512 GB</span></span>            | <span data-ttu-id="74741-134">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="74741-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="74741-135">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="74741-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="74741-136">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="74741-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="74741-137">IOPS por disco</span><span class="sxs-lookup"><span data-stu-id="74741-137">IOPS per disk</span></span>       | <span data-ttu-id="74741-138">120</span><span class="sxs-lookup"><span data-stu-id="74741-138">120</span></span>   | <span data-ttu-id="74741-139">240</span><span class="sxs-lookup"><span data-stu-id="74741-139">240</span></span>   | <span data-ttu-id="74741-140">500</span><span class="sxs-lookup"><span data-stu-id="74741-140">500</span></span>   | <span data-ttu-id="74741-141">2.300</span><span class="sxs-lookup"><span data-stu-id="74741-141">2300</span></span>              | <span data-ttu-id="74741-142">5.000</span><span class="sxs-lookup"><span data-stu-id="74741-142">5000</span></span>              | <span data-ttu-id="74741-143">7500</span><span class="sxs-lookup"><span data-stu-id="74741-143">7500</span></span>              | <span data-ttu-id="74741-144">7500</span><span class="sxs-lookup"><span data-stu-id="74741-144">7500</span></span>              | 
| <span data-ttu-id="74741-145">Taxa de transferência por disco</span><span class="sxs-lookup"><span data-stu-id="74741-145">Throughput per disk</span></span> | <span data-ttu-id="74741-146">25 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="74741-146">25 MB per second</span></span>  | <span data-ttu-id="74741-147">50 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="74741-147">50 MB per second</span></span>  | <span data-ttu-id="74741-148">100 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="74741-148">100 MB per second</span></span> | <span data-ttu-id="74741-149">150 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="74741-149">150 MB per second</span></span> | <span data-ttu-id="74741-150">200 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="74741-150">200 MB per second</span></span> | <span data-ttu-id="74741-151">250 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="74741-151">250 MB per second</span></span> | <span data-ttu-id="74741-152">250 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="74741-152">250 MB per second</span></span> | 

<span data-ttu-id="74741-153">**Managed Disks Standard**</span><span class="sxs-lookup"><span data-stu-id="74741-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="74741-154">Há sete tipos de discos Gerenciados Padrão que podem ser usados com sua VM.</span><span class="sxs-lookup"><span data-stu-id="74741-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="74741-155">Cada um deles tem uma capacidade diferente, mas com os mesmos limites de taxa de transferência e IOPS.</span><span class="sxs-lookup"><span data-stu-id="74741-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="74741-156">Escolha o tipo de saudação de discos gerenciados padrão com base nas necessidades de capacidade de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74741-156">Choose hello type of Standard Managed disks based on hello capacity needs of your application.</span></span>

| <span data-ttu-id="74741-157">Tipo de disco Standard</span><span class="sxs-lookup"><span data-stu-id="74741-157">Standard Disk Type</span></span>  | <span data-ttu-id="74741-158">S4</span><span class="sxs-lookup"><span data-stu-id="74741-158">S4</span></span>               | <span data-ttu-id="74741-159">S6</span><span class="sxs-lookup"><span data-stu-id="74741-159">S6</span></span>               | <span data-ttu-id="74741-160">S10</span><span class="sxs-lookup"><span data-stu-id="74741-160">S10</span></span>              | <span data-ttu-id="74741-161">S20</span><span class="sxs-lookup"><span data-stu-id="74741-161">S20</span></span>              | <span data-ttu-id="74741-162">S30</span><span class="sxs-lookup"><span data-stu-id="74741-162">S30</span></span>              | <span data-ttu-id="74741-163">S40</span><span class="sxs-lookup"><span data-stu-id="74741-163">S40</span></span>              | <span data-ttu-id="74741-164">S50</span><span class="sxs-lookup"><span data-stu-id="74741-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="74741-165">Tamanho do disco</span><span class="sxs-lookup"><span data-stu-id="74741-165">Disk size</span></span>           | <span data-ttu-id="74741-166">30 GB</span><span class="sxs-lookup"><span data-stu-id="74741-166">30 GB</span></span>            | <span data-ttu-id="74741-167">64 GB</span><span class="sxs-lookup"><span data-stu-id="74741-167">64 GB</span></span>            | <span data-ttu-id="74741-168">128 GB</span><span class="sxs-lookup"><span data-stu-id="74741-168">128 GB</span></span>           | <span data-ttu-id="74741-169">512 GB</span><span class="sxs-lookup"><span data-stu-id="74741-169">512 GB</span></span>           | <span data-ttu-id="74741-170">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="74741-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="74741-171">2048 GB (2TB)</span><span class="sxs-lookup"><span data-stu-id="74741-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="74741-172">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="74741-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="74741-173">IOPS por disco</span><span class="sxs-lookup"><span data-stu-id="74741-173">IOPS per disk</span></span>       | <span data-ttu-id="74741-174">500</span><span class="sxs-lookup"><span data-stu-id="74741-174">500</span></span>              | <span data-ttu-id="74741-175">500</span><span class="sxs-lookup"><span data-stu-id="74741-175">500</span></span>              | <span data-ttu-id="74741-176">500</span><span class="sxs-lookup"><span data-stu-id="74741-176">500</span></span>              | <span data-ttu-id="74741-177">500</span><span class="sxs-lookup"><span data-stu-id="74741-177">500</span></span>              | <span data-ttu-id="74741-178">500</span><span class="sxs-lookup"><span data-stu-id="74741-178">500</span></span>              | <span data-ttu-id="74741-179">500</span><span class="sxs-lookup"><span data-stu-id="74741-179">500</span></span>             | <span data-ttu-id="74741-180">500</span><span class="sxs-lookup"><span data-stu-id="74741-180">500</span></span>              | 
| <span data-ttu-id="74741-181">Taxa de transferência por disco</span><span class="sxs-lookup"><span data-stu-id="74741-181">Throughput per disk</span></span> | <span data-ttu-id="74741-182">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="74741-182">60 MB per second</span></span> | <span data-ttu-id="74741-183">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="74741-183">60 MB per second</span></span> | <span data-ttu-id="74741-184">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="74741-184">60 MB per second</span></span> | <span data-ttu-id="74741-185">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="74741-185">60 MB per second</span></span> | <span data-ttu-id="74741-186">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="74741-186">60 MB per second</span></span> | <span data-ttu-id="74741-187">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="74741-187">60 MB per second</span></span> | <span data-ttu-id="74741-188">60 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="74741-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="74741-189">Política de cache de disco</span><span class="sxs-lookup"><span data-stu-id="74741-189">Disk caching policy</span></span> 

<span data-ttu-id="74741-190">**Managed Disks Premium**</span><span class="sxs-lookup"><span data-stu-id="74741-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="74741-191">Por padrão, a política de cache de disco é *somente leitura* para todos os discos de dados Premium, de hello e *leitura-gravação* para o disco do sistema operacional Premium Olá anexado toohello VM.</span><span class="sxs-lookup"><span data-stu-id="74741-191">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="74741-192">Esta configuração é recomendável tooachieve Olá o desempenho ideal para IOs seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74741-192">This configuration setting is recommended tooachieve hello optimal performance for your application’s IOs.</span></span> <span data-ttu-id="74741-193">Para discos de dados de gravação intensa ou somente gravação (como arquivos de log do SQL Server), desabilite o cache de disco para que possa obter o melhor desempenho do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74741-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="74741-194">Preços</span><span class="sxs-lookup"><span data-stu-id="74741-194">Pricing</span></span>

<span data-ttu-id="74741-195">Saudação de revisão [preços para discos gerenciados](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="74741-195">Review hello [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="74741-196">Preços de discos gerenciados do Premium são igual a saudação discos de Premium não gerenciado.</span><span class="sxs-lookup"><span data-stu-id="74741-196">Pricing of Premium Managed Disks is same as hello Premium Unmanaged Disks.</span></span> <span data-ttu-id="74741-197">No entanto, os preços do Standard Managed Disks são diferentes dos preços do Standard Unmanaged Disks.</span><span class="sxs-lookup"><span data-stu-id="74741-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="74741-198">Lista de verificação</span><span class="sxs-lookup"><span data-stu-id="74741-198">Checklist</span></span>

1.  <span data-ttu-id="74741-199">Se você estiver migrando tooPremium gerenciados discos, verifique se que ele está disponível na região Olá que você estiver migrando para o.</span><span class="sxs-lookup"><span data-stu-id="74741-199">If you are migrating tooPremium Managed Disks, make sure it is available in hello region you are migrating to.</span></span>

2.  <span data-ttu-id="74741-200">Decida Olá nova VM série que usará.</span><span class="sxs-lookup"><span data-stu-id="74741-200">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="74741-201">Se você estiver migrando tooPremium gerenciados discos, ele deve ser uma capacidade de armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="74741-201">It should be a Premium Storage capable if you are migrating tooPremium Managed Disks.</span></span>

3.  <span data-ttu-id="74741-202">Decida Olá VM tamanho exato você usará que estão disponíveis na região Olá que você estiver migrando para o.</span><span class="sxs-lookup"><span data-stu-id="74741-202">Decide hello exact VM size you will use which are available in hello region you are migrating to.</span></span> <span data-ttu-id="74741-203">Tamanho da VM precisa toobe toosupport grande o suficiente Olá quantos discos de dados que você tem.</span><span class="sxs-lookup"><span data-stu-id="74741-203">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="74741-204">Por exemplo, se você tiver quatro discos de dados, Olá VM deve ter dois ou mais núcleos.</span><span class="sxs-lookup"><span data-stu-id="74741-204">For example, if you have four data disks, hello VM must have two or more cores.</span></span> <span data-ttu-id="74741-205">Considere também as necessidades de capacidade de processamento, memória e largura de banda de rede.</span><span class="sxs-lookup"><span data-stu-id="74741-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="74741-206">Ter Olá detalhes atuais de VM úteis, inclusive Olá lista de discos e blobs VHD correspondentes.</span><span class="sxs-lookup"><span data-stu-id="74741-206">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="74741-207">Prepare seu aplicativo para o tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="74741-207">Prepare your application for downtime.</span></span> <span data-ttu-id="74741-208">toodo uma migração limpa, você tem toostop todo o processamento Olá Olá atual sistema.</span><span class="sxs-lookup"><span data-stu-id="74741-208">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="74741-209">Somente então você poderá obtê-lo estado tooconsistent que você pode migrar toohello nova plataforma.</span><span class="sxs-lookup"><span data-stu-id="74741-209">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="74741-210">Duração de tempo de inatividade depende da quantidade de saudação de dados em Olá discos toomigrate.</span><span class="sxs-lookup"><span data-stu-id="74741-210">Downtime duration depends on hello amount of data in hello disks toomigrate.</span></span>


## <a name="migrate-hello-vm"></a><span data-ttu-id="74741-211">Migrar Olá VM</span><span class="sxs-lookup"><span data-stu-id="74741-211">Migrate hello VM</span></span>

<span data-ttu-id="74741-212">Prepare seu aplicativo para o tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="74741-212">Prepare your application for downtime.</span></span> <span data-ttu-id="74741-213">toodo uma migração limpa, você tem toostop todo o processamento Olá Olá atual sistema.</span><span class="sxs-lookup"><span data-stu-id="74741-213">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="74741-214">Somente então você poderá obtê-lo estado tooconsistent que você pode migrar toohello nova plataforma.</span><span class="sxs-lookup"><span data-stu-id="74741-214">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="74741-215">Duração do tempo de inatividade depende da quantidade de saudação de dados em Olá discos toomigrate.</span><span class="sxs-lookup"><span data-stu-id="74741-215">Downtime duration depends hello amount of data in hello disks toomigrate.</span></span>


1.  <span data-ttu-id="74741-216">Primeiro, defina os parâmetros comuns de saudação:</span><span class="sxs-lookup"><span data-stu-id="74741-216">First, set hello common parameters:</span></span>

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

2.  <span data-ttu-id="74741-217">Criar um disco do sistema operacional gerenciado usando Olá VHD do hello VM clássico.</span><span class="sxs-lookup"><span data-stu-id="74741-217">Create a managed OS disk using hello VHD from hello classic VM.</span></span>

    <span data-ttu-id="74741-218">Certifique-se de que você tenha fornecido Olá completar URI de saudação parâmetro toohello $osVhdUri de VHD do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="74741-218">Ensure that you have provided hello complete URI of hello OS VHD toohello $osVhdUri parameter.</span></span> <span data-ttu-id="74741-219">Além disso, insira **-AccountType** como **PremiumLRS** ou **StandardLRS** com base no tipo dos discos (Premium ou Standard) que você está migrando.</span><span class="sxs-lookup"><span data-stu-id="74741-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="74741-220">Anexar Olá OS disco toohello nova VM.</span><span class="sxs-lookup"><span data-stu-id="74741-220">Attach hello OS disk toohello new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="74741-221">Criar um disco de dados gerenciado Olá VHD do arquivo de dados e adicioná-lo toohello nova VM.</span><span class="sxs-lookup"><span data-stu-id="74741-221">Create a managed data disk from hello data VHD file and add it toohello new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="74741-222">Criar hello nova VM, definindo o IP público, rede Virtual e NIC.</span><span class="sxs-lookup"><span data-stu-id="74741-222">Create hello new VM by setting public IP, Virtual Network and NIC.</span></span>

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
><span data-ttu-id="74741-223">Pode haver toosupport necessárias etapas adicionais seu aplicativo não será coberto por este guia.</span><span class="sxs-lookup"><span data-stu-id="74741-223">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="74741-224">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74741-224">Next steps</span></span>

- <span data-ttu-id="74741-225">Conecte-se a máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="74741-225">Connect toohello virtual machine.</span></span> <span data-ttu-id="74741-226">Para obter instruções, consulte [como tooconnect e logon tooan virtuais do Azure do computador que executa o Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="74741-226">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

