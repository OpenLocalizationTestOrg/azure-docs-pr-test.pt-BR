---
title: aaaMigrating VMs tooAzure armazenamento Premium | Microsoft Docs
description: "Migre seu tooAzure de VMs armazenamento Premium existente. O Armazenamento Premium dá suporte ao disco de alto desempenho e baixa latência para cargas de trabalho que usam muita E/S em execução em máquinas virtuais do Azure."
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
ms.openlocfilehash: cd812bdbe39f43fe053a998d96788045d5a43258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a><span data-ttu-id="28be1-104">Migrando tooAzure Premium armazenamento (discos não gerenciado)</span><span class="sxs-lookup"><span data-stu-id="28be1-104">Migrating tooAzure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="28be1-105">Este artigo aborda como não gerenciado toomigrate uma VM que usa discos padrão não gerenciado tooa VM que usa discos premium.</span><span class="sxs-lookup"><span data-stu-id="28be1-105">This article discusses how toomigrate a VM that uses unmanaged standard disks tooa VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="28be1-106">É recomendável que você use discos gerenciado do Azure para novas VMs e que você converta os discos de toomanaged anterior discos não gerenciado.</span><span class="sxs-lookup"><span data-stu-id="28be1-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="28be1-107">Contas de armazenamento subjacentes do discos identificador Olá gerenciado para que você não precisa.</span><span class="sxs-lookup"><span data-stu-id="28be1-107">Managed Disks handle hello underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="28be1-108">Para saber mais, confira [Managed Disks Overview](storage-managed-disks-overview.md) (Visão geral do Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="28be1-108">For more information, please see our [Managed Disks Overview](storage-managed-disks-overview.md).</span></span>
>

<span data-ttu-id="28be1-109">O Armazenamento Premium do Azure dá suporte de disco de alto desempenho e baixa latência para máquinas virtuais executando cargas de trabalho intensivas para entradas e saídas.</span><span class="sxs-lookup"><span data-stu-id="28be1-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="28be1-110">Você pode tirar proveito de velocidade de saudação e o desempenho desses discos migrando tooAzure de discos VM do seu aplicativo armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="28be1-110">You can take advantage of hello speed and performance of these disks by migrating your application's VM disks tooAzure Premium Storage.</span></span>

<span data-ttu-id="28be1-111">Olá finalidade deste guia é toohelp novos usuários do armazenamento do Azure Premium melhor preparar toomake uma transição suave das sua tooPremium atual do sistema armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28be1-111">hello purpose of this guide is toohelp new users of Azure Premium Storage better prepare toomake a smooth transition from their current system tooPremium Storage.</span></span> <span data-ttu-id="28be1-112">Guia de saudação endereços três componentes principais do hello nesse processo:</span><span class="sxs-lookup"><span data-stu-id="28be1-112">hello guide addresses three of hello key components in this process:</span></span>

* [<span data-ttu-id="28be1-113">Planejar a migração de saudação tooPremium armazenamento</span><span class="sxs-lookup"><span data-stu-id="28be1-113">Plan for hello Migration tooPremium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="28be1-114">Preparar e cópia discos de rígidos virtuais (VHDs) tooPremium armazenamento</span><span class="sxs-lookup"><span data-stu-id="28be1-114">Prepare and Copy Virtual Hard Disks (VHDs) tooPremium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="28be1-115">Criar uma Máquina Virtual do Azure usando o Armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="28be1-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="28be1-116">Você pode migrar máquinas virtuais de outra plataformas tooAzure armazenamento Premium ou migrar máquinas virtuais do Azure existentes de armazenamento padrão tooPremium armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28be1-116">You can either migrate VMs from other platforms tooAzure Premium Storage or migrate existing Azure VMs from Standard Storage tooPremium Storage.</span></span> <span data-ttu-id="28be1-117">Este guia aborda as etapas para os dois cenários.</span><span class="sxs-lookup"><span data-stu-id="28be1-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="28be1-118">Siga as etapas de saudação especificadas na seção de relevantes Olá dependendo do cenário.</span><span class="sxs-lookup"><span data-stu-id="28be1-118">Follow hello steps specified in hello relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="28be1-119">Você pode encontrar uma visão geral de recursos e os preços do Armazenamento Premium em [Armazenamento Premium: Armazenamento de Alto Desempenho para Cargas de Trabalho de Máquina Virtual do Azure](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="28be1-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="28be1-120">É recomendável migrar qualquer disco de máquina virtual que requerem alta IOPS tooAzure armazenamento Premium para obter melhor desempenho para o seu aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-120">We recommend migrating any virtual machine disk requiring high IOPS tooAzure Premium Storage for hello best performance for your application.</span></span> <span data-ttu-id="28be1-121">Se o disco não requer IOPS alta, você pode limitar os custos mantendo-a no armazenamento padrão, que armazena dados de disco da máquina virtual em HDDs (unidades de disco rígido) em vez de SSDs.</span><span class="sxs-lookup"><span data-stu-id="28be1-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="28be1-122">Concluir o processo de migração de saudação em sua totalidade pode exigir ações adicionais antes e após Olá etapas fornecidas neste guia.</span><span class="sxs-lookup"><span data-stu-id="28be1-122">Completing hello migration process in its entirety may require additional actions both before and after hello steps provided in this guide.</span></span> <span data-ttu-id="28be1-123">Exemplos incluem a configuração de redes virtuais ou pontos de extremidade ou fazer alterações de código no hello próprio aplicativo que podem exigir algum tempo de inatividade em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="28be1-123">Examples include configuring virtual networks or endpoints or making code changes within hello application itself which may require some downtime in your application.</span></span> <span data-ttu-id="28be1-124">Essas ações são aplicativo tooeach exclusivo e deve ser concluída junto com hello etapas fornecidas neste guia toomake Olá transição completa tooPremium armazenamento de maneira mais uniforme possível.</span><span class="sxs-lookup"><span data-stu-id="28be1-124">These actions are unique tooeach application, and you should complete them along with hello steps provided in this guide toomake hello full transition tooPremium Storage as seamless as possible.</span></span>

## <span data-ttu-id="28be1-125"><a name="plan-the-migration-to-premium-storage"></a>Planejar a migração de saudação tooPremium armazenamento</span><span class="sxs-lookup"><span data-stu-id="28be1-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for hello migration tooPremium Storage</span></span>
<span data-ttu-id="28be1-126">Esta seção garante que são toofollow pronto etapas de migração Olá neste artigo e o ajuda a toomake Olá melhor decisão sobre tipos de VM e disco.</span><span class="sxs-lookup"><span data-stu-id="28be1-126">This section ensures that you are ready toofollow hello migration steps in this article, and helps you toomake hello best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="28be1-127">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="28be1-127">Prerequisites</span></span>
* <span data-ttu-id="28be1-128">Você também precisará de uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="28be1-128">You will need an Azure subscription.</span></span> <span data-ttu-id="28be1-129">Se você ainda não tiver uma, você poderá criar uma assinatura de [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/) de um mês ou visitar [Preços do Azure](https://azure.microsoft.com/pricing/) para obter mais opções.</span><span class="sxs-lookup"><span data-stu-id="28be1-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="28be1-130">tooexecute cmdlets do PowerShell, você precisará módulo do Microsoft Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-130">tooexecute PowerShell cmdlets, you will need hello Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="28be1-131">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para Olá instalar ponto e instruções de instalação.</span><span class="sxs-lookup"><span data-stu-id="28be1-131">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello install point and installation instructions.</span></span>
* <span data-ttu-id="28be1-132">Quando você planejar toouse Azure VMs em execução no armazenamento Premium, você precisa toouse Olá VMs com capacidade de armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="28be1-132">When you plan toouse Azure VMs running on Premium Storage, you need toouse hello Premium Storage capable VMs.</span></span> <span data-ttu-id="28be1-133">Você pode usar discos de Armazenamento Standard e Premium com VMs compatíveis com o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="28be1-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="28be1-134">Discos de armazenamento Premium estarão disponíveis com mais tipos de VM Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="28be1-134">Premium storage disks will be available with more VM types in hello future.</span></span> <span data-ttu-id="28be1-135">Para obter informações sobre todos os tamanhos e tipos de discos de VM do Azure disponíveis, veja [Tamanhos para máquinas virtuais](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [Tamanhos para Serviços de Nuvem](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="28be1-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="28be1-136">Considerações</span><span class="sxs-lookup"><span data-stu-id="28be1-136">Considerations</span></span>
<span data-ttu-id="28be1-137">Uma VM do Azure oferece suporte ao anexar vários discos de armazenamento Premium para que seus aplicativos podem ter até too256 TB de armazenamento por VM.</span><span class="sxs-lookup"><span data-stu-id="28be1-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up too256 TB of storage per VM.</span></span> <span data-ttu-id="28be1-138">Com o Armazenamento Premium, seus aplicativos podem atingir 80.000 IOPS (operações de entrada/saída por segundo) por VM e taxa de transferência de disco de 2.000 MB por segundo por VM com latências extremamente baixas para operações de leitura.</span><span class="sxs-lookup"><span data-stu-id="28be1-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="28be1-139">Você tem opções de várias VMs e Discos.</span><span class="sxs-lookup"><span data-stu-id="28be1-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="28be1-140">Esta seção é toohelp toofind uma opção mais adequada para sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="28be1-140">This section is toohelp you toofind an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="28be1-141">Tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="28be1-141">VM sizes</span></span>
<span data-ttu-id="28be1-142">especificações de tamanho de VM do Azure Olá são listadas na [tamanhos das máquinas virtuais](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="28be1-142">hello Azure VM size specifications are listed in [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="28be1-143">Examine as características de desempenho de saudação de máquinas virtuais que funcionam com o armazenamento Premium e escolha o tamanho VM mais apropriado hello mais adequada para sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="28be1-143">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="28be1-144">Certifique-se de que há largura de banda suficiente disponível no seu tráfego de disco VM toodrive hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-144">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="28be1-145">Tamanhos do disco</span><span class="sxs-lookup"><span data-stu-id="28be1-145">Disk sizes</span></span>
<span data-ttu-id="28be1-146">Há cinco tipos de discos que podem ser usados com a VM e cada um tem IOPs específicos e limites de taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="28be1-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="28be1-147">Leve em consideração esses limites quando escolhendo o tipo de disco Olá para sua VM com base em necessidades de saudação do seu aplicativo em termos de capacidade, escalabilidade e desempenho, e o horário de pico é carregado.</span><span class="sxs-lookup"><span data-stu-id="28be1-147">Take into consideration these limits when choosing hello disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="28be1-148">Tipo de discos premium</span><span class="sxs-lookup"><span data-stu-id="28be1-148">Premium Disks Type</span></span>  | <span data-ttu-id="28be1-149">P10</span><span class="sxs-lookup"><span data-stu-id="28be1-149">P10</span></span>   | <span data-ttu-id="28be1-150">P20</span><span class="sxs-lookup"><span data-stu-id="28be1-150">P20</span></span>   | <span data-ttu-id="28be1-151">P30</span><span class="sxs-lookup"><span data-stu-id="28be1-151">P30</span></span>            | <span data-ttu-id="28be1-152">P40</span><span class="sxs-lookup"><span data-stu-id="28be1-152">P40</span></span>            | <span data-ttu-id="28be1-153">P50</span><span class="sxs-lookup"><span data-stu-id="28be1-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="28be1-154">Tamanho do disco</span><span class="sxs-lookup"><span data-stu-id="28be1-154">Disk size</span></span>           | <span data-ttu-id="28be1-155">128 GB</span><span class="sxs-lookup"><span data-stu-id="28be1-155">128 GB</span></span>| <span data-ttu-id="28be1-156">512 GB</span><span class="sxs-lookup"><span data-stu-id="28be1-156">512 GB</span></span>| <span data-ttu-id="28be1-157">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="28be1-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="28be1-158">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="28be1-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="28be1-159">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="28be1-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="28be1-160">IOPS por disco</span><span class="sxs-lookup"><span data-stu-id="28be1-160">IOPS per disk</span></span>       | <span data-ttu-id="28be1-161">500</span><span class="sxs-lookup"><span data-stu-id="28be1-161">500</span></span>   | <span data-ttu-id="28be1-162">2.300</span><span class="sxs-lookup"><span data-stu-id="28be1-162">2300</span></span>  | <span data-ttu-id="28be1-163">5.000</span><span class="sxs-lookup"><span data-stu-id="28be1-163">5000</span></span>           | <span data-ttu-id="28be1-164">7500</span><span class="sxs-lookup"><span data-stu-id="28be1-164">7500</span></span>           | <span data-ttu-id="28be1-165">7500</span><span class="sxs-lookup"><span data-stu-id="28be1-165">7500</span></span>           | 
| <span data-ttu-id="28be1-166">Taxa de transferência por disco</span><span class="sxs-lookup"><span data-stu-id="28be1-166">Throughput per disk</span></span> | <span data-ttu-id="28be1-167">100 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="28be1-167">100 MB per second</span></span> | <span data-ttu-id="28be1-168">150 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="28be1-168">150 MB per second</span></span> | <span data-ttu-id="28be1-169">200 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="28be1-169">200 MB per second</span></span> | <span data-ttu-id="28be1-170">250 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="28be1-170">250 MB per second</span></span> | <span data-ttu-id="28be1-171">250 MB por segundo</span><span class="sxs-lookup"><span data-stu-id="28be1-171">250 MB per second</span></span> |

<span data-ttu-id="28be1-172">Dependendo da carga de trabalho, determine se discos de dados adicionais são necessários para sua VM.</span><span class="sxs-lookup"><span data-stu-id="28be1-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="28be1-173">Você pode anexar várias tooyour de discos de dados persistentes VM.</span><span class="sxs-lookup"><span data-stu-id="28be1-173">You can attach several persistent data disks tooyour VM.</span></span> <span data-ttu-id="28be1-174">Se necessário, você pode distribuir em capacidade de Olá Olá discos tooincrease e o desempenho do volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="28be1-174">If needed, you can stripe across hello disks tooincrease hello capacity and performance of hello volume.</span></span> <span data-ttu-id="28be1-175">(Veja o que é a distribuição de disco [aqui](storage-premium-storage-performance.md#disk-striping).) Se você distribuir discos de dados do Armazenamento Premium usando [Espaços de Armazenamento][4], deverá configurá-lo com uma coluna para cada disco usado.</span><span class="sxs-lookup"><span data-stu-id="28be1-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="28be1-176">Caso contrário, hello geral desempenho do volume de saudação distribuída pode ser menor do que o esperado devido toouneven distribuição do tráfego entre os discos de saudação.</span><span class="sxs-lookup"><span data-stu-id="28be1-176">Otherwise, hello overall performance of hello striped volume may be lower than expected due toouneven distribution of traffic across hello disks.</span></span> <span data-ttu-id="28be1-177">Para VMs do Linux, você pode usar o hello *mdadm* tooachieve utilitário Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="28be1-177">For Linux VMs you can use hello *mdadm* utility tooachieve hello same.</span></span> <span data-ttu-id="28be1-178">Consulte o artigo [Configurar o Software RAID no Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="28be1-178">See article [Configure Software RAID on Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="28be1-179">Metas de escalabilidade da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="28be1-179">Storage account scalability targets</span></span>
<span data-ttu-id="28be1-180">Contas de armazenamento Premium têm Olá seguintes metas de escalabilidade em adição toohello [escalabilidade do armazenamento do Azure e metas de desempenho](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="28be1-180">Premium Storage accounts have hello following scalability targets in addition toohello [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="28be1-181">Se seus requisitos de aplicativo excederem os destinos de escalabilidade de saudação de uma única conta de armazenamento, criar várias contas de armazenamento de seu aplicativo toouse e particionar seus dados entre as contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28be1-181">If your application requirements exceed hello scalability targets of a single storage account, build your application toouse multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="28be1-182">Capacidade total da conta</span><span class="sxs-lookup"><span data-stu-id="28be1-182">Total Account Capacity</span></span> | <span data-ttu-id="28be1-183">Largura de banda total para uma conta de armazenamento com redundância local</span><span class="sxs-lookup"><span data-stu-id="28be1-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="28be1-184">Capacidade de disco: 35 TB</span><span class="sxs-lookup"><span data-stu-id="28be1-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="28be1-185">Capacidade do instantâneo: 10 TB</span><span class="sxs-lookup"><span data-stu-id="28be1-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="28be1-186">Backup too50 gigabits por segundo para entrada + saída</span><span class="sxs-lookup"><span data-stu-id="28be1-186">Up too50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="28be1-187">Para obter mais informações sobre as especificações de armazenamento Premium Olá a, check-out [escalabilidade e metas de desempenho ao usar o armazenamento Premium](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="28be1-187">For hello more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="28be1-188">Política de cache de disco</span><span class="sxs-lookup"><span data-stu-id="28be1-188">Disk caching policy</span></span>
<span data-ttu-id="28be1-189">Por padrão, a política de cache de disco é *somente leitura* para todos os discos de dados Premium, de hello e *leitura-gravação* para o disco do sistema operacional Premium Olá anexado toohello VM.</span><span class="sxs-lookup"><span data-stu-id="28be1-189">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="28be1-190">Esta configuração é recomendável tooachieve Olá o desempenho ideal para IOs seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="28be1-190">This configuration setting is recommended tooachieve hello optimal performance for your application's IOs.</span></span> <span data-ttu-id="28be1-191">Para discos de dados de gravação intensa ou somente gravação (como arquivos de log do SQL Server), desabilite o cache de disco para que possa obter o melhor desempenho do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="28be1-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="28be1-192">configurações de cache de saudação para discos de dados existentes podem ser atualizadas usando [Portal do Azure](https://portal.azure.com) ou hello *- HostCaching* parâmetro hello *Set-AzureDataDisk* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="28be1-192">hello cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or hello *-HostCaching* parameter of hello *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="28be1-193">Local</span><span class="sxs-lookup"><span data-stu-id="28be1-193">Location</span></span>
<span data-ttu-id="28be1-194">Escolha um local onde o Armazenamento do Azure Premium está disponível.</span><span class="sxs-lookup"><span data-stu-id="28be1-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="28be1-195">Confira [Serviços do Azure por região](https://azure.microsoft.com/regions/#services) para obter informações atualizadas sobre as localizações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="28be1-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="28be1-196">Máquinas virtuais localizadas em Olá mesmo região como Olá conta de armazenamento que armazena Olá discos para Olá VM dará melhor desempenho que se eles estão em regiões separadas.</span><span class="sxs-lookup"><span data-stu-id="28be1-196">VMs located in hello same region as hello Storage account that stores hello disks for hello VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="28be1-197">Outras definições de configuração da VM do Azure</span><span class="sxs-lookup"><span data-stu-id="28be1-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="28be1-198">Ao criar uma VM do Azure, você será solicitado tooconfigure algumas de suas configurações.</span><span class="sxs-lookup"><span data-stu-id="28be1-198">When creating an Azure VM, you will be asked tooconfigure certain VM settings.</span></span> <span data-ttu-id="28be1-199">Lembre-se de que algumas configurações são fixas para tempo de vida de saudação do hello VM, enquanto você pode modificar ou adicionar outros mais tarde.</span><span class="sxs-lookup"><span data-stu-id="28be1-199">Remember, few settings are fixed for hello lifetime of hello VM, while you can modify or add others later.</span></span> <span data-ttu-id="28be1-200">Examine essas definições de configuração de máquina virtual do Azure e certifique-se de que eles são configurados apropriadamente toomatch seus requisitos de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="28be1-200">Review these Azure VM configuration settings and make sure that these are configured appropriately toomatch your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="28be1-201">Otimização</span><span class="sxs-lookup"><span data-stu-id="28be1-201">Optimization</span></span>
<span data-ttu-id="28be1-202">[Armazenamento Premium do Azure: design de alto desempenho](storage-premium-storage-performance.md) fornece diretrizes para criação de aplicativos de alto desempenho usando o Armazenamento Premium do Azure.</span><span class="sxs-lookup"><span data-stu-id="28be1-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="28be1-203">Você pode seguir as diretrizes de saudação combinadas com desempenho melhores práticas aplicável tootechnologies usados pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="28be1-203">You can follow hello guidelines combined with performance best practices applicable tootechnologies used by your application.</span></span>

## <span data-ttu-id="28be1-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Preparar e copiar os discos rígidos virtuais (VHDs) tooPremium armazenamento</span><span class="sxs-lookup"><span data-stu-id="28be1-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) tooPremium Storage</span></span>
<span data-ttu-id="28be1-205">Olá seção a seguir fornece diretrizes para preparar VHDs de sua VM e copiar VHDs tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28be1-205">hello following section provides guidelines for preparing VHDs from your VM and copying VHDs tooAzure Storage.</span></span>

* [<span data-ttu-id="28be1-206">Cenário 1: "Estou migrando tooAzure de máquinas virtuais do Azure existente armazenamento Premium."</span><span class="sxs-lookup"><span data-stu-id="28be1-206">Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="28be1-207">Cenário 2: "eu estou migrando VMs de outra plataformas tooAzure armazenamento Premium."</span><span class="sxs-lookup"><span data-stu-id="28be1-207">Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="28be1-208">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="28be1-208">Prerequisites</span></span>
<span data-ttu-id="28be1-209">Olá tooprepare VHDs para migração, você precisará:</span><span class="sxs-lookup"><span data-stu-id="28be1-209">tooprepare hello VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="28be1-210">Uma assinatura do Azure, uma conta de armazenamento e um contêiner em que o armazenamento de conta toowhich, você pode copiar o VHD.</span><span class="sxs-lookup"><span data-stu-id="28be1-210">An Azure subscription, a storage account, and a container in that storage account toowhich you can copy your VHD.</span></span> <span data-ttu-id="28be1-211">Observe que a conta de armazenamento de destino Olá pode ser uma conta de Standard ou Premium armazenamento dependendo do requisito.</span><span class="sxs-lookup"><span data-stu-id="28be1-211">Note that hello destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="28be1-212">Saudação de toogeneralize uma ferramenta VHD se você planejar toocreate várias instâncias VM dele.</span><span class="sxs-lookup"><span data-stu-id="28be1-212">A tool toogeneralize hello VHD if you plan toocreate multiple VM instances from it.</span></span> <span data-ttu-id="28be1-213">Por exemplo, o sysprep para Windows ou o virt-sysprep para Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="28be1-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="28be1-214">Uma ferramenta tooupload Olá VHD arquivo toohello conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28be1-214">A tool tooupload hello VHD file toohello Storage account.</span></span> <span data-ttu-id="28be1-215">Consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md) ou use um [Gerenciador de armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="28be1-215">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="28be1-216">Este guia descreve como copiar seu VHD usando a ferramenta de AzCopy hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-216">This guide describes copying your VHD using hello AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="28be1-217">Se você escolher a opção de cópia síncrona com AzCopy, para um desempenho ideal, copie o VHD executando uma dessas ferramentas em uma VM do Azure que está em Olá mesma região da conta de armazenamento de destino hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in hello same region as hello destination storage account.</span></span> <span data-ttu-id="28be1-218">Se você estiver copiando um VHD de uma VM do Azure em uma região diferente, o desempenho pode ser mais lento.</span><span class="sxs-lookup"><span data-stu-id="28be1-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="28be1-219">Para copiar uma grande quantidade de dados pela largura de banda limitada, considere [usando Olá importação/exportação do Azure serviço tootransfer dados tooBlob armazenamento](storage-import-export-service.md); Isso permite tootransfer seus dados por disco rígido de envio de unidades tooan do Azure Datacenter.</span><span class="sxs-lookup"><span data-stu-id="28be1-219">For copying a large amount of data over limited bandwidth, consider [using hello Azure Import/Export service tootransfer data tooBlob Storage](storage-import-export-service.md); this allows you tootransfer your data by shipping hard disk drives tooan Azure datacenter.</span></span> <span data-ttu-id="28be1-220">Você pode usar o hello importação/exportação do Azure serviço toocopy dados tooa conta de armazenamento padrão somente.</span><span class="sxs-lookup"><span data-stu-id="28be1-220">You can use hello Azure Import/Export service toocopy data tooa standard storage account only.</span></span> <span data-ttu-id="28be1-221">Dados saudação em sua conta de armazenamento padrão, você pode usar o hello [API de cópia de Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) ou conta de armazenamento do AzCopy tootransfer Olá dados tooyour premium.</span><span class="sxs-lookup"><span data-stu-id="28be1-221">Once hello data is in your standard storage account, you can use either hello [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy tootransfer hello data tooyour premium storage account.</span></span>
>
> <span data-ttu-id="28be1-222">Observe que o Microsoft Azure dá suporte apenas a arquivos VHD de tamanho fixo.</span><span class="sxs-lookup"><span data-stu-id="28be1-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="28be1-223">Os arquivos VHDX ou VHDs dinâmicos não têm suporte.</span><span class="sxs-lookup"><span data-stu-id="28be1-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="28be1-224">Se você tiver um VHD dinâmico, você pode convertê-la toofixed tamanho usando Olá [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="28be1-224">If you have a dynamic VHD, you can convert it toofixed size using hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="28be1-225"><a name="scenario1"></a>Cenário 1: "Estou migrando tooAzure de máquinas virtuais do Azure existente armazenamento Premium."</span><span class="sxs-lookup"><span data-stu-id="28be1-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>
<span data-ttu-id="28be1-226">Se você estiver migrando existente VMs do Azure, Olá parar VM, preparar VHDs por tipo de saudação do VHD que você deseja e copie Olá VHD com AzCopy ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="28be1-226">If you are migrating existing Azure VMs, stop hello VM, prepare VHDs per hello type of VHD you want, and then copy hello VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="28be1-227">Olá VM precisa toobe completamente inoperante toomigrate um estado limpo.</span><span class="sxs-lookup"><span data-stu-id="28be1-227">hello VM needs toobe completely down toomigrate a clean state.</span></span> <span data-ttu-id="28be1-228">Haverá um tempo de inatividade até a conclusão da migração de saudação.</span><span class="sxs-lookup"><span data-stu-id="28be1-228">There will be a downtime until hello migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="28be1-229">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="28be1-229">Step 1.</span></span> <span data-ttu-id="28be1-230">Preparar VHDs para migração</span><span class="sxs-lookup"><span data-stu-id="28be1-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="28be1-231">Se você estiver migrando tooPremium de máquinas virtuais do Azure existente armazenamento, o VHD pode ser:</span><span class="sxs-lookup"><span data-stu-id="28be1-231">If you are migrating existing Azure VMs tooPremium Storage, your VHD may be:</span></span>

* <span data-ttu-id="28be1-232">Uma imagem de sistema operacional generalizado</span><span class="sxs-lookup"><span data-stu-id="28be1-232">A generalized operating system image</span></span>
* <span data-ttu-id="28be1-233">Um disco de sistema operacional exclusivo</span><span class="sxs-lookup"><span data-stu-id="28be1-233">A unique operating system disk</span></span>
* <span data-ttu-id="28be1-234">Um disco de dados</span><span class="sxs-lookup"><span data-stu-id="28be1-234">A data disk</span></span>

<span data-ttu-id="28be1-235">Abaixo, percorremos estes três cenários para preparar o VHD.</span><span class="sxs-lookup"><span data-stu-id="28be1-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a><span data-ttu-id="28be1-236">Usar um toocreate VHD do sistema operacional generalizado várias instâncias VM</span><span class="sxs-lookup"><span data-stu-id="28be1-236">Use a generalized Operating System VHD toocreate multiple VM instances</span></span>
<span data-ttu-id="28be1-237">Se você estiver carregando um VHD que será usado toocreate várias instâncias de VM do Azure genéricas, você deve primeiro generalizar VHD usando um utilitário de sysprep.</span><span class="sxs-lookup"><span data-stu-id="28be1-237">If you are uploading a VHD that will be used toocreate multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="28be1-238">Isso se aplica a tooa VHD que é local ou na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-238">This applies tooa VHD that is on-premises or in hello cloud.</span></span> <span data-ttu-id="28be1-239">O Sysprep remove todas as informações específicas de computador Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="28be1-239">Sysprep removes any machine-specific information from hello VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28be1-240">Tire um instantâneo ou realize backup de sua VM antes de generalizá-lo.</span><span class="sxs-lookup"><span data-stu-id="28be1-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="28be1-241">Em execução de sysprep será parar e desalocar a instância VM hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-241">Running sysprep will stop and deallocate hello VM instance.</span></span> <span data-ttu-id="28be1-242">Siga as etapas abaixo toosysprep um VHD do sistema operacional Windows.</span><span class="sxs-lookup"><span data-stu-id="28be1-242">Follow steps below toosysprep a Windows OS VHD.</span></span> <span data-ttu-id="28be1-243">Observe que executar comando de Sysprep Olá exigirá você tooshut máquina virtual do hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-243">Note that running hello Sysprep command will require you tooshut down hello virtual machine.</span></span> <span data-ttu-id="28be1-244">Para saber mais sobre o Sysprep, consulte [Visão Geral do Sysprep](http://technet.microsoft.com/library/hh825209.aspx) ou [Referência Técnica do Sysprep](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="28be1-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="28be1-245">Abra uma janela de Prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="28be1-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="28be1-246">Digite hello tooopen comando Sysprep a seguir:</span><span class="sxs-lookup"><span data-stu-id="28be1-246">Enter hello following command tooopen Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="28be1-247">No Olá, ferramenta de preparação do sistema, selecione Enter System Out-of-Box Experience (OOBE), Olá selecione caixa de seleção de generalizar, selecione **desligamento**e, em seguida, clique em **Okey**, conforme mostrado na imagem de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="28be1-247">In hello System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select hello Generalize check box, select **Shutdown**, and then click **OK**, as shown in hello image below.</span></span> <span data-ttu-id="28be1-248">O Sysprep será generalizar o sistema operacional de saudação e desligar o sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="28be1-248">Sysprep will generalize hello operating system and shut down hello system.</span></span>

    ![][1]

<span data-ttu-id="28be1-249">Para uma VM Ubuntu, use sysprep virt tooachieve Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="28be1-249">For an Ubuntu VM, use virt-sysprep tooachieve hello same.</span></span> <span data-ttu-id="28be1-250">Consulte [virt sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="28be1-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="28be1-251">Consulte também alguns do código-fonte aberto Olá [software de provisionamento do servidor Linux](http://www.cyberciti.biz/tips/server-provisioning-software.html) para outros sistemas operacionais Linux.</span><span class="sxs-lookup"><span data-stu-id="28be1-251">See also some of hello open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a><span data-ttu-id="28be1-252">Usar um toocreate de VHD do sistema operacional exclusivo uma única instância VM</span><span class="sxs-lookup"><span data-stu-id="28be1-252">Use a unique Operating System VHD toocreate a single VM instance</span></span>
<span data-ttu-id="28be1-253">Se você tiver um aplicativo em execução no hello VM que exige que os dados específicos de máquina hello, não generalize Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="28be1-253">If you have an application running on hello VM which requires hello machine specific data, do not generalize hello VHD.</span></span> <span data-ttu-id="28be1-254">Um VHD não generalizado pode ser usado toocreate uma instância exclusiva da máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="28be1-254">A non-generalized VHD can be used toocreate a unique Azure VM instance.</span></span> <span data-ttu-id="28be1-255">Por exemplo, se você tiver um Controlador de Domínio em seu VHD, executar o sysprep irá torná-lo inútil como um Controlador de Domínio.</span><span class="sxs-lookup"><span data-stu-id="28be1-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="28be1-256">Revisar aplicativos Olá em execução no seu impacto VM e hello da execução de sysprep-los antes de generalizar Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="28be1-256">Review hello applications running on your VM and hello impact of running sysprep on them before generalizing hello VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="28be1-257">Registrar o VHD do disco de dados</span><span class="sxs-lookup"><span data-stu-id="28be1-257">Register data disk VHD</span></span>
<span data-ttu-id="28be1-258">Se você tiver discos de dados no Azure toobe migrados, você deve fazer se VMs Olá que usam esses dados discos serão desligados.</span><span class="sxs-lookup"><span data-stu-id="28be1-258">If you have data disks in Azure toobe migrated, you must make sure hello VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="28be1-259">Execute as etapas de saudação descritas abaixo toocopy VHD tooAzure armazenamento Premium e registrá-lo como um disco de dados provisionado.</span><span class="sxs-lookup"><span data-stu-id="28be1-259">Follow hello steps described below toocopy VHD tooAzure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="28be1-260">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="28be1-260">Step 2.</span></span> <span data-ttu-id="28be1-261">Criar hello de destino para o VHD</span><span class="sxs-lookup"><span data-stu-id="28be1-261">Create hello destination for your VHD</span></span>
<span data-ttu-id="28be1-262">Crie uma conta de armazenamento para manter seus VHDs.</span><span class="sxs-lookup"><span data-stu-id="28be1-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="28be1-263">Considere Olá pontos a seguir ao planejar onde toostore seus VHDs:</span><span class="sxs-lookup"><span data-stu-id="28be1-263">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="28be1-264">destino de saudação conta de armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="28be1-264">hello target Premium storage account.</span></span>
* <span data-ttu-id="28be1-265">local de conta de armazenamento Olá deve ser igual ao armazenamento Premium compatível com máquinas virtuais do Azure você criará no estágio final de saudação.</span><span class="sxs-lookup"><span data-stu-id="28be1-265">hello storage account location must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="28be1-266">Você poderá copiar a nova conta de armazenamento tooa ou saudação do plano toouse mesma conta de armazenamento com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="28be1-266">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="28be1-267">Copiar e salvar chave de conta de armazenamento Olá Olá destino da conta de armazenamento para o próximo estágio de saudação.</span><span class="sxs-lookup"><span data-stu-id="28be1-267">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="28be1-268">Para discos de dados, você pode escolher tookeep alguns discos de dados em uma conta de armazenamento padrão (por exemplo, discos que têm mais armazenamento), mas é altamente recomendável que você mover todos os dados para o armazenamento de premium de toouse de carga de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="28be1-268">For data disks, you can choose tookeep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <span data-ttu-id="28be1-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="28be1-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="28be1-270">Copiar o VHD com o AzCopy ou o PowerShell</span><span class="sxs-lookup"><span data-stu-id="28be1-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="28be1-271">Você precisará toofind seu caminho do contêiner e a conta chave tooprocess qualquer uma dessas duas opções de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28be1-271">You will need toofind your container path and storage account key tooprocess either of these two options.</span></span> <span data-ttu-id="28be1-272">A chave de conta de armazenamento e o caminho do contêiner podem ser encontrados em **Portal do Azure** > **Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="28be1-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="28be1-273">URL do contêiner Olá será como "https://myaccount.blob.core.windows.net/mycontainer/".</span><span class="sxs-lookup"><span data-stu-id="28be1-273">hello container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="28be1-274">Opção 1: copiar um VHD com o AzCopy (cópia assíncrona)</span><span class="sxs-lookup"><span data-stu-id="28be1-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="28be1-275">Usando AzCopy, você pode carregar facilmente Olá VHD sobre Olá da Internet.</span><span class="sxs-lookup"><span data-stu-id="28be1-275">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="28be1-276">Dependendo do tamanho de saudação do hello VHDs, isso pode levar tempo.</span><span class="sxs-lookup"><span data-stu-id="28be1-276">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="28be1-277">Lembre-se de entrada/saída limites da conta de armazenamento toocheck Olá ao usar essa opção.</span><span class="sxs-lookup"><span data-stu-id="28be1-277">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="28be1-278">Consulte [Metas de Desempenho e Escalabilidade do Armazenamento do Azure](storage-scalability-targets.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="28be1-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="28be1-279">Baixe e instale o AzCopy aqui: [Versão mais recente do AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="28be1-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="28be1-280">Abra o PowerShell do Azure e vá toohello pasta onde AzCopy é instalado.</span><span class="sxs-lookup"><span data-stu-id="28be1-280">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="28be1-281">Comando a seguir de saudação usar arquivo VHD Olá toocopy de "Origem" muito "Destino".</span><span class="sxs-lookup"><span data-stu-id="28be1-281">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="28be1-282">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="28be1-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="28be1-283">Aqui estão as descrições dos parâmetros de saudação usados em Olá AzCopy comando:</span><span class="sxs-lookup"><span data-stu-id="28be1-283">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="28be1-284">**/ Origem:  *&lt;fonte&gt;:***  local da pasta de saudação ou URL do contêiner de armazenamento que contém a saudação VHD.</span><span class="sxs-lookup"><span data-stu-id="28be1-284">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="28be1-285">**/ SourceKey:  *&lt;chave da conta de origem&gt;:***  chave de conta de armazenamento da conta de armazenamento de origem hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="28be1-286">**/ Dest:  *&lt;destino&gt;:***  toocopy de URL do contêiner de armazenamento Olá VHD para.</span><span class="sxs-lookup"><span data-stu-id="28be1-286">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="28be1-287">**/ DestKey:  *&lt;chave da conta de destino&gt;:***  chave de conta de armazenamento da conta de armazenamento de destino hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="28be1-288">**/ Padrão:  *&lt;nome de arquivo&gt;:***  especificar nome do arquivo hello de saudação VHD toocopy.</span><span class="sxs-lookup"><span data-stu-id="28be1-288">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="28be1-289">Para obter detalhes sobre como usar AzCopy ferramenta, consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="28be1-289">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="28be1-290">Opção 2: copiar um VHD com o PowerShell (cópia sincronizada)</span><span class="sxs-lookup"><span data-stu-id="28be1-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="28be1-291">Você também pode copiar o arquivo VHD hello usando o cmdlet do PowerShell Olá AzureStorageBlobCopy de início.</span><span class="sxs-lookup"><span data-stu-id="28be1-291">You can also copy hello VHD file using hello PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="28be1-292">Use Olá comando a seguir no Azure PowerShell toocopy VHD.</span><span class="sxs-lookup"><span data-stu-id="28be1-292">Use hello following command on Azure PowerShell toocopy VHD.</span></span> <span data-ttu-id="28be1-293">Substitua valores hello <> com valores correspondentes da sua conta de armazenamento de origem e de destino.</span><span class="sxs-lookup"><span data-stu-id="28be1-293">Replace hello values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="28be1-294">toouse esse comando, você deve ter um contêiner chamado vhds em sua conta de armazenamento de destino.</span><span class="sxs-lookup"><span data-stu-id="28be1-294">toouse this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="28be1-295">Se o contêiner Olá não existir, crie um antes de executar o comando hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-295">If hello container doesn't exist, create one before running hello command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="28be1-296">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="28be1-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="28be1-297"><a name="scenario2"></a>Cenário 2: "eu estou migrando VMs de outra plataformas tooAzure armazenamento Premium."</span><span class="sxs-lookup"><span data-stu-id="28be1-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>
<span data-ttu-id="28be1-298">Se você estiver migrando o VHD do Azure nuvem armazenamento tooAzure, você deve primeiro exportar pasta local do tooa Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="28be1-298">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="28be1-299">Tem caminho de origem completa de saudação do diretório local hello, onde o VHD é armazenado útil e, em seguida, usando AzCopy tooupload-tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28be1-299">Have hello complete source path of hello local directory where VHD is stored handy, and then using AzCopy tooupload it tooAzure Storage.</span></span>

#### <a name="step-1-export-vhd-tooa-local-directory"></a><span data-ttu-id="28be1-300">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="28be1-300">Step 1.</span></span> <span data-ttu-id="28be1-301">Exportar o diretório local do VHD tooa</span><span class="sxs-lookup"><span data-stu-id="28be1-301">Export VHD tooa local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="28be1-302">Copiar um VHD do AWS</span><span class="sxs-lookup"><span data-stu-id="28be1-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="28be1-303">Se você estiver usando AWS, exporte Olá EC2 instância tooa VHD em um bucket S3 da Amazon.</span><span class="sxs-lookup"><span data-stu-id="28be1-303">If you are using AWS, export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="28be1-304">Siga etapas Olá descritas Olá documentação do Amazon para ferramenta de interface de linha de comando (CLI) exportando instâncias do Amazon EC2 tooinstall Olá EC2 Amazon e execute o arquivo VHD Olá comando Criar-instância-export-tarefa tooexport Olá EC2 instância tooa.</span><span class="sxs-lookup"><span data-stu-id="28be1-304">Follow hello steps described in hello Amazon documentation for Exporting Amazon EC2 Instances tooinstall hello Amazon EC2 command-line interface (CLI) tool and run hello create-instance-export-task command tooexport hello EC2 instance tooa VHD file.</span></span> <span data-ttu-id="28be1-305">Ser toouse se **VHD** para Olá disco &#95; imagem &#95; Variável de formato ao executar Olá **criar-instância-export-tarefa** comando.</span><span class="sxs-lookup"><span data-stu-id="28be1-305">Be sure toouse **VHD** for hello DISK&#95;IMAGE&#95;FORMAT variable when running hello **create-instance-export-task** command.</span></span> <span data-ttu-id="28be1-306">Olá VHD arquivo exportado é salvo no bucket de saudação Amazon S3 que designar durante esse processo.</span><span class="sxs-lookup"><span data-stu-id="28be1-306">hello exported VHD file is saved in hello Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="28be1-307">Baixe o arquivo VHD de saudação do bucket de S3 hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-307">Download hello VHD file from hello S3 bucket.</span></span> <span data-ttu-id="28be1-308">Arquivo VHD de Select hello, em seguida, **ações** > **baixar**.</span><span class="sxs-lookup"><span data-stu-id="28be1-308">Select hello VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="28be1-309">Copiar um VHD de outra nuvem que não é do Azure</span><span class="sxs-lookup"><span data-stu-id="28be1-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="28be1-310">Se você estiver migrando o VHD do Azure nuvem armazenamento tooAzure, você deve primeiro exportar pasta local do tooa Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="28be1-310">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="28be1-311">Copiar o caminho do código-fonte completo saudação do diretório local hello, onde o VHD é armazenado.</span><span class="sxs-lookup"><span data-stu-id="28be1-311">Copy hello complete source path of hello local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="28be1-312">Copiar um VHD do local</span><span class="sxs-lookup"><span data-stu-id="28be1-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="28be1-313">Se você estiver migrando o VHD de um ambiente local, você precisará de caminho de origem completa Olá onde o VHD é armazenado.</span><span class="sxs-lookup"><span data-stu-id="28be1-313">If you are migrating VHD from an on-premises environment, you will need hello complete source path where VHD is stored.</span></span> <span data-ttu-id="28be1-314">caminho de origem Olá pode ser um compartilhamento de arquivo ou local do servidor.</span><span class="sxs-lookup"><span data-stu-id="28be1-314">hello source path could be a server location or file share.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="28be1-315">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="28be1-315">Step 2.</span></span> <span data-ttu-id="28be1-316">Criar hello de destino para o VHD</span><span class="sxs-lookup"><span data-stu-id="28be1-316">Create hello destination for your VHD</span></span>
<span data-ttu-id="28be1-317">Crie uma conta de armazenamento para manter seus VHDs.</span><span class="sxs-lookup"><span data-stu-id="28be1-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="28be1-318">Considere Olá pontos a seguir ao planejar onde toostore seus VHDs:</span><span class="sxs-lookup"><span data-stu-id="28be1-318">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="28be1-319">conta de armazenamento de destino Olá pode ser armazenamento standard ou premium, dependendo do requisito de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="28be1-319">hello target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="28be1-320">região da conta de armazenamento Olá deve ser igual ao armazenamento Premium compatível com máquinas virtuais do Azure você criará no estágio final de saudação.</span><span class="sxs-lookup"><span data-stu-id="28be1-320">hello storage account region must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="28be1-321">Você poderá copiar a nova conta de armazenamento tooa ou saudação do plano toouse mesma conta de armazenamento com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="28be1-321">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="28be1-322">Copiar e salvar chave de conta de armazenamento Olá Olá destino da conta de armazenamento para o próximo estágio de saudação.</span><span class="sxs-lookup"><span data-stu-id="28be1-322">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="28be1-323">É altamente recomendável que você mover todos os dados para o armazenamento de premium de toouse de carga de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="28be1-323">We strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a><span data-ttu-id="28be1-324">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="28be1-324">Step 3.</span></span> <span data-ttu-id="28be1-325">Carregar Olá VHD tooAzure armazenamento</span><span class="sxs-lookup"><span data-stu-id="28be1-325">Upload hello VHD tooAzure Storage</span></span>
<span data-ttu-id="28be1-326">Agora que você tem o VHD no diretório local hello, você pode usar AzCopy ou AzurePowerShell tooupload hello. vhd arquivo tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28be1-326">Now that you have your VHD in hello local directory, you can use AzCopy or AzurePowerShell tooupload hello .vhd file tooAzure Storage.</span></span> <span data-ttu-id="28be1-327">Ambas as opções são fornecidas aqui:</span><span class="sxs-lookup"><span data-stu-id="28be1-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a><span data-ttu-id="28be1-328">Opção 1: Usando o arquivo. vhd do Azure PowerShell Add-AzureVhd tooupload Olá</span><span class="sxs-lookup"><span data-stu-id="28be1-328">Option 1: Using Azure PowerShell Add-AzureVhd tooupload hello .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="28be1-329">Um exemplo <Uri> pode ser ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="28be1-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="28be1-330">Um exemplo <FileInfo> pode ser ***"C:\path\to\upload.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="28be1-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a><span data-ttu-id="28be1-331">Opção 2: Usando o arquivo. vhd do AzCopy tooupload Olá</span><span class="sxs-lookup"><span data-stu-id="28be1-331">Option 2: Using AzCopy tooupload hello .vhd file</span></span>
<span data-ttu-id="28be1-332">Usando AzCopy, você pode carregar facilmente Olá VHD sobre Olá da Internet.</span><span class="sxs-lookup"><span data-stu-id="28be1-332">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="28be1-333">Dependendo do tamanho de saudação do hello VHDs, isso pode levar tempo.</span><span class="sxs-lookup"><span data-stu-id="28be1-333">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="28be1-334">Lembre-se de entrada/saída limites da conta de armazenamento toocheck Olá ao usar essa opção.</span><span class="sxs-lookup"><span data-stu-id="28be1-334">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="28be1-335">Consulte [Metas de Desempenho e Escalabilidade do Armazenamento do Azure](storage-scalability-targets.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="28be1-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="28be1-336">Baixe e instale o AzCopy aqui: [Versão mais recente do AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="28be1-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="28be1-337">Abra o PowerShell do Azure e vá toohello pasta onde AzCopy é instalado.</span><span class="sxs-lookup"><span data-stu-id="28be1-337">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="28be1-338">Comando a seguir de saudação usar arquivo VHD Olá toocopy de "Origem" muito "Destino".</span><span class="sxs-lookup"><span data-stu-id="28be1-338">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="28be1-339">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="28be1-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="28be1-340">Aqui estão as descrições dos parâmetros de saudação usados em Olá AzCopy comando:</span><span class="sxs-lookup"><span data-stu-id="28be1-340">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="28be1-341">**/ Origem:  *&lt;fonte&gt;:***  local da pasta de saudação ou URL do contêiner de armazenamento que contém a saudação VHD.</span><span class="sxs-lookup"><span data-stu-id="28be1-341">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="28be1-342">**/ SourceKey:  *&lt;chave da conta de origem&gt;:***  chave de conta de armazenamento da conta de armazenamento de origem hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="28be1-343">**/ Dest:  *&lt;destino&gt;:***  toocopy de URL do contêiner de armazenamento Olá VHD para.</span><span class="sxs-lookup"><span data-stu-id="28be1-343">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="28be1-344">**/ DestKey:  *&lt;chave da conta de destino&gt;:***  chave de conta de armazenamento da conta de armazenamento de destino hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="28be1-345">**/ BlobType: página:** especifica esse destino Olá é um blob de página.</span><span class="sxs-lookup"><span data-stu-id="28be1-345">**/BlobType: page:** Specifies that hello destination is a page blob.</span></span>
   * <span data-ttu-id="28be1-346">**/ Padrão:  *&lt;nome de arquivo&gt;:***  especificar nome do arquivo hello de saudação VHD toocopy.</span><span class="sxs-lookup"><span data-stu-id="28be1-346">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="28be1-347">Para obter detalhes sobre como usar AzCopy ferramenta, consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="28be1-347">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="28be1-348">Outras opções para carregar um VHD</span><span class="sxs-lookup"><span data-stu-id="28be1-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="28be1-349">Você também pode carregar uma conta de armazenamento de tooyour VHD usando uma saudação significa a seguir:</span><span class="sxs-lookup"><span data-stu-id="28be1-349">You can also upload a VHD tooyour storage account using one of hello following means:</span></span>

* [<span data-ttu-id="28be1-350">API do Blob da Cópia de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="28be1-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="28be1-351">Carregamento de Blobs do Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="28be1-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="28be1-352">Referência de API REST do Serviço de Importação/Exportação do Armazenamento</span><span class="sxs-lookup"><span data-stu-id="28be1-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="28be1-353">É recomendável usar o Serviço de Importação/Exportação se o tempo de carregamento estimado é de mais de sete dias.</span><span class="sxs-lookup"><span data-stu-id="28be1-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="28be1-354">Você pode usar [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate tempo de saudação da unidade de tamanho e a transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="28be1-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="28be1-355">Importação/exportação pode ser usado a conta de armazenamento padrão de tooa toocopy.</span><span class="sxs-lookup"><span data-stu-id="28be1-355">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="28be1-356">Você precisará toocopy da conta de armazenamento toopremium de armazenamento padrão usando uma ferramenta como AzCopy.</span><span class="sxs-lookup"><span data-stu-id="28be1-356">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="28be1-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Criar máquinas virtuais do Azure usando o Armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="28be1-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="28be1-358">Após Olá VHD carregado ou copiado toohello desejado conta de armazenamento, siga as instruções de saudação em Olá de tooregister essa seção VHD como uma imagem do sistema operacional ou o disco do sistema operacional dependendo do cenário e, em seguida, criar uma instância de VM a partir dele.</span><span class="sxs-lookup"><span data-stu-id="28be1-358">After hello VHD is uploaded or copied toohello desired storage account, follow hello instructions in this section tooregister hello VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="28be1-359">disco de dados Olá VHD pode ser anexado toohello VM depois que ela é criada.</span><span class="sxs-lookup"><span data-stu-id="28be1-359">hello data disk VHD can be attached toohello VM once it is created.</span></span>
<span data-ttu-id="28be1-360">Um exemplo de script de migração é fornecido no final desta seção hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-360">A sample migration script is provided at hello end of this section.</span></span> <span data-ttu-id="28be1-361">Este script simples não corresponde a todos os cenários.</span><span class="sxs-lookup"><span data-stu-id="28be1-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="28be1-362">Talvez seja necessário tooupdate Olá script toomatch com seu cenário específico.</span><span class="sxs-lookup"><span data-stu-id="28be1-362">You may need tooupdate hello script toomatch with your specific scenario.</span></span> <span data-ttu-id="28be1-363">toosee se este script se aplica a tooyour cenário, consulte abaixo [um exemplo de Script de migração](#a-sample-migration-script).</span><span class="sxs-lookup"><span data-stu-id="28be1-363">toosee if this script applies tooyour scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="28be1-364">Lista de verificação</span><span class="sxs-lookup"><span data-stu-id="28be1-364">Checklist</span></span>
1. <span data-ttu-id="28be1-365">Aguarde até que todos os discos VHD Olá cópia seja concluída.</span><span class="sxs-lookup"><span data-stu-id="28be1-365">Wait until all hello VHD disks copying is complete.</span></span>
2. <span data-ttu-id="28be1-366">Certifique-se de que armazenamento Premium está disponível na região Olá que você está migrando.</span><span class="sxs-lookup"><span data-stu-id="28be1-366">Make sure Premium Storage is available in hello region you are migrating to.</span></span>
3. <span data-ttu-id="28be1-367">Decida Olá nova VM série que usará.</span><span class="sxs-lookup"><span data-stu-id="28be1-367">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="28be1-368">Ele deve ser uma capacidade de armazenamento Premium, e o tamanho de Olá deve ser dependendo da disponibilidade de saudação na região de saudação e com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="28be1-368">It should be a Premium Storage capable, and hello size should be depending on hello availability in hello region and based on your needs.</span></span>
4. <span data-ttu-id="28be1-369">Decida o tamanho VM exato Olá que você usará.</span><span class="sxs-lookup"><span data-stu-id="28be1-369">Decide hello exact VM size you will use.</span></span> <span data-ttu-id="28be1-370">Tamanho da VM precisa toobe toosupport grande o suficiente Olá quantos discos de dados que você tem.</span><span class="sxs-lookup"><span data-stu-id="28be1-370">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="28be1-371">Por exemplo</span><span class="sxs-lookup"><span data-stu-id="28be1-371">E.g.</span></span> <span data-ttu-id="28be1-372">Se você tiver 4 discos de dados, Olá VM deve ter de 2 ou mais núcleos.</span><span class="sxs-lookup"><span data-stu-id="28be1-372">if you have 4 data disks, hello VM must have 2 or more cores.</span></span> <span data-ttu-id="28be1-373">Considere também as necessidades de capacidade de processamento, memória e largura de banda de rede.</span><span class="sxs-lookup"><span data-stu-id="28be1-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="28be1-374">Crie uma conta de armazenamento Premium na região de destino hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-374">Create a Premium Storage account in hello target region.</span></span> <span data-ttu-id="28be1-375">Esta é a conta de saudação você usará para Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="28be1-375">This is hello account you will use for hello new VM.</span></span>
6. <span data-ttu-id="28be1-376">Ter Olá detalhes atuais de VM úteis, inclusive Olá lista de discos e blobs VHD correspondentes.</span><span class="sxs-lookup"><span data-stu-id="28be1-376">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="28be1-377">Prepare seu aplicativo para o tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="28be1-377">Prepare your application for downtime.</span></span> <span data-ttu-id="28be1-378">toodo uma migração limpa, você tem toostop todo o processamento Olá Olá atual sistema.</span><span class="sxs-lookup"><span data-stu-id="28be1-378">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="28be1-379">Somente então você poderá obtê-lo estado tooconsistent que você pode migrar toohello nova plataforma.</span><span class="sxs-lookup"><span data-stu-id="28be1-379">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="28be1-380">Duração do tempo de inatividade dependerá da quantidade de saudação de dados em Olá discos toomigrate.</span><span class="sxs-lookup"><span data-stu-id="28be1-380">Downtime duration will depend on hello amount of data in hello disks toomigrate.</span></span>

> [!NOTE]
> <span data-ttu-id="28be1-381">Se você estiver criando uma VM do Azure Resource Manager de um disco especializado do VHD, consulte muito[este modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) para implantar o Gerenciador de recursos de VM usando o disco existente.</span><span class="sxs-lookup"><span data-stu-id="28be1-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer too[this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="28be1-382">Registrar seu VHD</span><span class="sxs-lookup"><span data-stu-id="28be1-382">Register your VHD</span></span>
<span data-ttu-id="28be1-383">toocreate uma VM do VHD do sistema operacional ou tooattach um tooa de disco de dados nova VM, você deve primeiro registrá-los.</span><span class="sxs-lookup"><span data-stu-id="28be1-383">toocreate a VM from OS VHD or tooattach a data disk tooa new VM, you must first register them.</span></span> <span data-ttu-id="28be1-384">Siga as etapas abaixo, dependendo do cenário do VHD.</span><span class="sxs-lookup"><span data-stu-id="28be1-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="28be1-385">Generalizado VHD do sistema operacional toocreate várias instâncias de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="28be1-385">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="28be1-386">Após a imagem do sistema operacional generalizada VHD é carregado toohello conta de armazenamento, registrá-lo como um **a imagem da VM do Azure** para que você possa criar uma ou mais instâncias VM dele.</span><span class="sxs-lookup"><span data-stu-id="28be1-386">After generalized OS image VHD is uploaded toohello storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="28be1-387">Olá tooregister de cmdlets do PowerShell a seguir ao Use o VHD como uma imagem de sistema operacional da VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="28be1-387">Use hello following PowerShell cmdlets tooregister your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="28be1-388">Forneça a URL de contêiner completa de saudação onde o VHD foi copiado para.</span><span class="sxs-lookup"><span data-stu-id="28be1-388">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="28be1-389">Copie e salve o nome de saudação dessa nova imagem de VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="28be1-389">Copy and save hello name of this new Azure VM Image.</span></span> <span data-ttu-id="28be1-390">O exemplo hello acima, é *OSImageName*.</span><span class="sxs-lookup"><span data-stu-id="28be1-390">In hello example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="28be1-391">Toocreate de VHD do sistema operacional exclusivo uma única instância de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="28be1-391">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="28be1-392">Após Olá exclusivo VHD do sistema operacional é carregado toohello armazenamento de conta, registrá-lo como um **disco do sistema operacional Azure** para que você possa criar uma instância de VM dele.</span><span class="sxs-lookup"><span data-stu-id="28be1-392">After hello unique OS VHD is uploaded toohello storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="28be1-393">Use esses tooregister de cmdlets do PowerShell seu VHD como um disco do sistema operacional do Azure.</span><span class="sxs-lookup"><span data-stu-id="28be1-393">Use these PowerShell cmdlets tooregister your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="28be1-394">Forneça a URL de contêiner completa de saudação onde o VHD foi copiado para.</span><span class="sxs-lookup"><span data-stu-id="28be1-394">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="28be1-395">Copiar e salvar Olá nome desse novo disco de sistema operacional do Azure.</span><span class="sxs-lookup"><span data-stu-id="28be1-395">Copy and save hello name of this new Azure OS Disk.</span></span> <span data-ttu-id="28be1-396">O exemplo hello acima, é *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="28be1-396">In hello example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a><span data-ttu-id="28be1-397">Toobe VHD do disco de dados anexado toonew instâncias de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="28be1-397">Data disk VHD toobe attached toonew Azure VM instance(s)</span></span>
<span data-ttu-id="28be1-398">Depois de hello VHD do disco de dados carregado toostorage conta, registre-o como um disco de dados do Azure de para que ele possa ser anexado tooyour nova série DS, série DSv2 série ou instância de VM do Azure série GS.</span><span class="sxs-lookup"><span data-stu-id="28be1-398">After hello data disk VHD is uploaded toostorage account, register it as an Azure Data Disk so that it can be attached tooyour new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="28be1-399">Use esses tooregister de cmdlets do PowerShell seu VHD como um disco de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="28be1-399">Use these PowerShell cmdlets tooregister your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="28be1-400">Forneça a URL de contêiner completa de saudação onde o VHD foi copiado para.</span><span class="sxs-lookup"><span data-stu-id="28be1-400">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="28be1-401">Copiar e salvar Olá nome desse novo disco de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="28be1-401">Copy and save hello name of this new Azure Data Disk.</span></span> <span data-ttu-id="28be1-402">O exemplo hello acima, é *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="28be1-402">In hello example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="28be1-403">Criar uma VM com capacidade de Armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="28be1-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="28be1-404">Uma vez Olá imagem do sistema operacional ou o disco do sistema operacional são registrados, crie uma nova série DS, série dsv2 ou série GS VM.</span><span class="sxs-lookup"><span data-stu-id="28be1-404">Once hello OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="28be1-405">Você irá usar imagem do sistema operacional hello ou nome de disco do sistema operacional que você registrou.</span><span class="sxs-lookup"><span data-stu-id="28be1-405">You will be using hello operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="28be1-406">Selecione o tipo VM de saudação da camada de armazenamento Premium Olá.</span><span class="sxs-lookup"><span data-stu-id="28be1-406">Select hello VM type from hello Premium Storage tier.</span></span> <span data-ttu-id="28be1-407">No exemplo a seguir, estamos usando Olá *Standard_DS2* tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="28be1-407">In example below, we are using hello *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="28be1-408">Atualize toomake de tamanho de disco de saudação se que ele corresponde a sua capacidade e requisitos de desempenho e tamanhos de disco do Azure disponíveis hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-408">Update hello disk size toomake sure it matches your capacity and performance requirements and hello available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="28be1-409">Cmdlets do PowerShell seguem Olá passo a passo abaixo toocreate Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="28be1-409">Follow hello step by step PowerShell cmdlets below toocreate hello new VM.</span></span> <span data-ttu-id="28be1-410">Primeiro, defina os parâmetros comuns de saudação:</span><span class="sxs-lookup"><span data-stu-id="28be1-410">First, set hello common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="28be1-411">Primeiro, crie um serviço de nuvem em que você hospedará suas novas VMs.</span><span class="sxs-lookup"><span data-stu-id="28be1-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="28be1-412">Em seguida, dependendo do cenário, crie instância de VM do Azure Olá Olá imagem do sistema operacional ou disco do sistema operacional que você registrou.</span><span class="sxs-lookup"><span data-stu-id="28be1-412">Next, depending on your scenario, create hello Azure VM instance from either hello OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="28be1-413">Generalizado VHD do sistema operacional toocreate várias instâncias de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="28be1-413">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="28be1-414">Criar hello uma ou mais instâncias nova VM do Azure série DS usando Olá **imagem do sistema operacional Azure** registrado.</span><span class="sxs-lookup"><span data-stu-id="28be1-414">Create hello one or more new DS Series Azure VM instances using hello **Azure OS Image** that you registered.</span></span> <span data-ttu-id="28be1-415">Especifica esse nome de imagem do sistema operacional na configuração da VM Olá ao criar a nova VM conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="28be1-415">Specify this OS Image name in hello VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="28be1-416">Toocreate de VHD do sistema operacional exclusivo uma única instância de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="28be1-416">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="28be1-417">Criar uma nova instância de máquina virtual do Azure de série DS usando Olá **disco do sistema operacional Azure** registrado.</span><span class="sxs-lookup"><span data-stu-id="28be1-417">Create a new DS series Azure VM instance using hello **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="28be1-418">Especifica esse nome de disco do sistema operacional na configuração da VM hello quando criar hello nova VM, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="28be1-418">Specify this OS Disk name in hello VM configuration when creating hello new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="28be1-419">Especifique outras informações da VM do Azure, como um serviço de nuvem, região, conta de armazenamento, conjunto de disponibilidade e política de cache.</span><span class="sxs-lookup"><span data-stu-id="28be1-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="28be1-420">Observe que a instância VM Olá deve estar localizada com sistema operacional associado ou Olá de discos de dados, para a conta de serviço, região e armazenamento de nuvem Olá selecionada deve estar no mesmo local que Olá subjacente VHDs desses discos.</span><span class="sxs-lookup"><span data-stu-id="28be1-420">Note that hello VM instance must be co-located with associated operating system or data disks, so hello selected cloud service, region and storage account must all be in hello same location as hello underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="28be1-421">Anexar disco de dados</span><span class="sxs-lookup"><span data-stu-id="28be1-421">Attach data disk</span></span>
<span data-ttu-id="28be1-422">Por fim, se você tiver registrado dados disco VHDs, anexá-los toohello nova VM do Azure compatíveis com armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="28be1-422">Lastly, if you have registered data disk VHDs, attach them toohello new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="28be1-423">Usar as seguintes PowerShell cmdlet tooattach dados disco toohello nova VM e especifique Olá política de cache.</span><span class="sxs-lookup"><span data-stu-id="28be1-423">Use following PowerShell cmdlet tooattach data disk toohello new VM and specify hello caching policy.</span></span> <span data-ttu-id="28be1-424">No exemplo a seguir Olá política de cache está definida muito*ReadOnly*.</span><span class="sxs-lookup"><span data-stu-id="28be1-424">In example below hello caching policy is set too*ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="28be1-425">Pode haver toosupport necessárias etapas adicionais seu aplicativo não será coberto por este guia.</span><span class="sxs-lookup"><span data-stu-id="28be1-425">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="28be1-426">Verificação e planejamento de backup</span><span class="sxs-lookup"><span data-stu-id="28be1-426">Checking and plan backup</span></span>
<span data-ttu-id="28be1-427">Uma vez Olá nova máquina virtual está ativo e em execução, usando Olá mesmo id de logon e senha de acesso é como Olá VM original e verificar se tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="28be1-427">Once hello new VM is up and running, access it using hello same login id and password is as hello original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="28be1-428">Todas as configurações de hello, inclusive volumes de saudação distribuído, estaria presentes no hello nova VM.</span><span class="sxs-lookup"><span data-stu-id="28be1-428">All hello settings, including hello striped volumes, would be present in hello new VM.</span></span>

<span data-ttu-id="28be1-429">Olá última etapa é tooplan agendamento de backup e manutenção para Olá que nova VM com base nas necessidades do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-429">hello last step is tooplan backup and maintenance schedule for hello new VM based on hello application's needs.</span></span>

### <span data-ttu-id="28be1-430"><a name="a-sample-migration-script"></a>Um script de migração de exemplo</span><span class="sxs-lookup"><span data-stu-id="28be1-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="28be1-431">Se você tiver várias toomigrate de VMs, automação por scripts do PowerShell poderão ser úteis.</span><span class="sxs-lookup"><span data-stu-id="28be1-431">If you have multiple VMs toomigrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="28be1-432">A seguir está um exemplo de script que automatiza a migração de saudação de uma VM.</span><span class="sxs-lookup"><span data-stu-id="28be1-432">Following is a sample script that automates hello migration of a VM.</span></span> <span data-ttu-id="28be1-433">Observe que o script abaixo é apenas um exemplo e há algumas suposições feitas sobre discos de VM Olá atuais.</span><span class="sxs-lookup"><span data-stu-id="28be1-433">Note that below script is only an example, and there are few assumptions made about hello current VM disks.</span></span> <span data-ttu-id="28be1-434">Talvez seja necessário tooupdate Olá script toomatch com seu cenário específico.</span><span class="sxs-lookup"><span data-stu-id="28be1-434">You may need tooupdate hello script toomatch with your specific scenario.</span></span>

<span data-ttu-id="28be1-435">suposições Olá são:</span><span class="sxs-lookup"><span data-stu-id="28be1-435">hello assumptions are:</span></span>

* <span data-ttu-id="28be1-436">Você está criando VMs clássicas do Azure.</span><span class="sxs-lookup"><span data-stu-id="28be1-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="28be1-437">Seus Discos de origem do Sistema Operacional e Discos de Dados de origem estão na mesma conta de armazenamento e no mesmo contêiner.</span><span class="sxs-lookup"><span data-stu-id="28be1-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="28be1-438">Se os discos de sistema operacional e discos de dados não estão no hello mesmo colocar, você pode usar AzCopy ou o Azure PowerShell toocopy VHDs em contas de armazenamento e contêineres.</span><span class="sxs-lookup"><span data-stu-id="28be1-438">If your OS Disks and Data Disks are not in hello same place, you can use AzCopy or Azure PowerShell toocopy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="28be1-439">Consulte a etapa anterior toohello: [cópia VHD com AzCopy ou o PowerShell](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="28be1-439">Refer toohello previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="28be1-440">Editar este script toomeet seu cenário é outra opção, mas é recomendável usar AzCopy ou o PowerShell, pois ela é mais rápido e fácil.</span><span class="sxs-lookup"><span data-stu-id="28be1-440">Editing this script toomeet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="28be1-441">script de automação de saudação é fornecido abaixo.</span><span class="sxs-lookup"><span data-stu-id="28be1-441">hello automation script is provided below.</span></span> <span data-ttu-id="28be1-442">Substitua o texto com suas informações e atualize Olá script toomatch com seu cenário específico.</span><span class="sxs-lookup"><span data-stu-id="28be1-442">Replace text with your information and update hello script toomatch with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="28be1-443">Usar o script existente de saudação não preserva a configuração de rede de saudação do seu VM de origem.</span><span class="sxs-lookup"><span data-stu-id="28be1-443">Using hello existing script does not preserve hello network configuration of your source VM.</span></span> <span data-ttu-id="28be1-444">Você precisará toore-config as configurações de rede de saudação em suas VMs migrados.</span><span class="sxs-lookup"><span data-stu-id="28be1-444">You will need toore-config hello networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
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


    #Check hello Azure PowerShell module version
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
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
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
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
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
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="28be1-445"><a name="optimization"></a>Otimização</span><span class="sxs-lookup"><span data-stu-id="28be1-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="28be1-446">A configuração da VM atual pode ser personalizada especificamente toowork bem com discos padrão.</span><span class="sxs-lookup"><span data-stu-id="28be1-446">Your current VM configuration may be customized specifically toowork well with Standard disks.</span></span> <span data-ttu-id="28be1-447">Por exemplo, tooincrease Olá desempenho usando muitos discos em um volume distribuído.</span><span class="sxs-lookup"><span data-stu-id="28be1-447">For instance, tooincrease hello performance by using many disks in a striped volume.</span></span> <span data-ttu-id="28be1-448">Por exemplo, em vez de usar 4 discos separadamente no armazenamento Premium, você poderá toooptimize capaz de custo de saudação fazendo com que um único disco.</span><span class="sxs-lookup"><span data-stu-id="28be1-448">For example, instead of using 4 disks separately on Premium Storage, you may be able toooptimize hello cost by having a single disk.</span></span> <span data-ttu-id="28be1-449">Otimizações de como esse toobe necessidade tratado caso a caso e exigem etapas personalizadas após a migração de saudação.</span><span class="sxs-lookup"><span data-stu-id="28be1-449">Optimizations like this need toobe handled on a case by case basis and require custom steps after hello migration.</span></span> <span data-ttu-id="28be1-450">Além disso, observe que esse processo não pode funcionar bem para bancos de dados e aplicativos que dependem do layout de disco Olá definida na configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="28be1-450">Also, note that this process may not well work for databases and applications that depend on hello disk layout defined in hello setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="28be1-451">Preparação</span><span class="sxs-lookup"><span data-stu-id="28be1-451">Preparation</span></span>
1. <span data-ttu-id="28be1-452">Olá Concluir migração simples, conforme descrito em Olá anteriormente nesta seção.</span><span class="sxs-lookup"><span data-stu-id="28be1-452">Complete hello Simple Migration as described in hello earlier section.</span></span> <span data-ttu-id="28be1-453">Otimizações serão executadas no hello nova VM após a migração de saudação.</span><span class="sxs-lookup"><span data-stu-id="28be1-453">Optimizations will be performed on hello new VM after hello migration.</span></span>
2. <span data-ttu-id="28be1-454">Defina Olá novos tamanhos de disco necessários para configuração de saudação otimizada.</span><span class="sxs-lookup"><span data-stu-id="28be1-454">Define hello new disk sizes needed for hello optimized configuration.</span></span>
3. <span data-ttu-id="28be1-455">Determine o mapeamento de saudação atual volumes/discos toohello novo disco de especificações de.</span><span class="sxs-lookup"><span data-stu-id="28be1-455">Determine mapping of hello current disks/volumes toohello new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="28be1-456">Etapas de execução</span><span class="sxs-lookup"><span data-stu-id="28be1-456">Execution steps</span></span>
1. <span data-ttu-id="28be1-457">Crie hello novos discos com os tamanhos corretos de saudação em Olá VM de armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="28be1-457">Create hello new disks with hello right sizes on hello Premium Storage VM.</span></span>
2. <span data-ttu-id="28be1-458">Logon toohello VM e cópia Olá dados de saudação atual toohello novo disco de volume que mapeia toothat volume.</span><span class="sxs-lookup"><span data-stu-id="28be1-458">Login toohello VM and copy hello data from hello current volume toohello new disk that maps toothat volume.</span></span> <span data-ttu-id="28be1-459">Faça isso para todos os volumes de saudação atual que precisem toomap tooa novo disco.</span><span class="sxs-lookup"><span data-stu-id="28be1-459">Do this for all hello current volumes that need toomap tooa new disk.</span></span>
3. <span data-ttu-id="28be1-460">Em seguida, alterar Olá aplicativo configurações tooswitch toohello novos discos e desanexar volumes antigos hello.</span><span class="sxs-lookup"><span data-stu-id="28be1-460">Next, change hello application settings tooswitch toohello new disks, and detach hello old volumes.</span></span>

<span data-ttu-id="28be1-461">Para ajustar o aplicativo hello para melhorar o desempenho de disco, consulte muito[otimizando o desempenho do aplicativo](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="28be1-461">For tuning hello application for better disk performance, please refer too[Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="28be1-462">Migrações de aplicativos</span><span class="sxs-lookup"><span data-stu-id="28be1-462">Application migrations</span></span>
<span data-ttu-id="28be1-463">Bancos de dados e outros aplicativos complexos podem exigir etapas especiais, conforme definido pelo provedor de saudação do aplicativo para a migração de saudação.</span><span class="sxs-lookup"><span data-stu-id="28be1-463">Databases and other complex applications may require special steps as defined by hello application provider for hello migration.</span></span> <span data-ttu-id="28be1-464">Consulte a documentação do aplicativo toorespective.</span><span class="sxs-lookup"><span data-stu-id="28be1-464">Please refer toorespective application documentation.</span></span> <span data-ttu-id="28be1-465">Por exemplo</span><span class="sxs-lookup"><span data-stu-id="28be1-465">E.g.</span></span> <span data-ttu-id="28be1-466">, normalmente, bancos de dados podem ser migrados por meio de backup e restauração.</span><span class="sxs-lookup"><span data-stu-id="28be1-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28be1-467">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="28be1-467">Next steps</span></span>
<span data-ttu-id="28be1-468">Consulte Olá recursos para cenários específicos para migrar máquinas virtuais a seguir:</span><span class="sxs-lookup"><span data-stu-id="28be1-468">See hello following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="28be1-469">Migrar Máquinas Virtuais do Azure entre as Contas de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="28be1-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="28be1-470">Criar e carregar um VHD do Windows Server tooAzure.</span><span class="sxs-lookup"><span data-stu-id="28be1-470">Create and upload a Windows Server VHD tooAzure.</span></span>](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="28be1-471">Criando e carregando um disco rígido Virtual que contém Olá o sistema operacional Linux</span><span class="sxs-lookup"><span data-stu-id="28be1-471">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="28be1-472">Migração de máquinas virtuais do Amazon AWS tooMicrosoft do Azure</span><span class="sxs-lookup"><span data-stu-id="28be1-472">Migrating Virtual Machines from Amazon AWS tooMicrosoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="28be1-473">Além disso, consulte Olá recursos toolearn mais sobre o armazenamento do Azure e máquinas virtuais do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="28be1-473">Also, see hello following resources toolearn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="28be1-474">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="28be1-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="28be1-475">Máquinas Virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="28be1-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="28be1-476">Armazenamento Premium: Armazenamento de Alto Desempenho para as Cargas de Trabalho da Máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="28be1-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
