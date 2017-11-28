---
title: aaaUse armazenamento Premium do Azure com o SQL Server | Microsoft Docs
description: "Este artigo usa recursos criados com o modelo de implantação clássico hello e fornece orientação sobre como usar o armazenamento Premium do Azure com o SQL Server em execução em máquinas virtuais do Azure."
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="918f0-103">Usar o Armazenamento Premium do Azure com o SQL Server em máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="918f0-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="918f0-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="918f0-104">Overview</span></span>
<span data-ttu-id="918f0-105">[Armazenamento Premium do Azure](../../../storage/common/storage-premium-storage.md) Olá a próxima geração de armazenamento que proporciona baixa latência e alta taxa de transferência e/s.</span><span class="sxs-lookup"><span data-stu-id="918f0-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) is hello next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="918f0-106">Ele funciona melhor para cargas de trabalho de uso intensivo de E/S de chave, como [Máquinas Virtuais](https://azure.microsoft.com/services/virtual-machines/)do SQL Server no IaaS.</span><span class="sxs-lookup"><span data-stu-id="918f0-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="918f0-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="918f0-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="918f0-108">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="918f0-109">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="918f0-110">Este artigo fornece planejamento e instruções sobre como migrar uma máquina Virtual que executa o SQL Server toouse armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="918f0-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server toouse Premium Storage.</span></span> <span data-ttu-id="918f0-111">Isso inclui a infraestrutura do Azure (rede, armazenamento) e as etapas de VM do Windows de convidado.</span><span class="sxs-lookup"><span data-stu-id="918f0-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="918f0-112">exemplo Hello Olá [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) mostra uma migração completa abrangente final tooend como toomove maior VMs tootake aproveitar melhor local armazenamento SSD com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="918f0-112">hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end tooend migration of how toomove larger VMs tootake advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="918f0-113">É importante toounderstand Olá ponta a ponta processo utilizando armazenamento do Premium do Azure com o SQL Server em VMs de IAAS.</span><span class="sxs-lookup"><span data-stu-id="918f0-113">It is important toounderstand hello end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="918f0-114">Isso inclui:</span><span class="sxs-lookup"><span data-stu-id="918f0-114">This includes:</span></span>

* <span data-ttu-id="918f0-115">Identificação da saudação pré-requisitos toouse armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="918f0-115">Identification of hello prerequisites toouse Premium Storage.</span></span>
* <span data-ttu-id="918f0-116">Exemplos de implantação do SQL Server no IaaS tooPremium armazenamento para novas implantações.</span><span class="sxs-lookup"><span data-stu-id="918f0-116">Examples of deploying SQL Server on IaaS tooPremium Storage for new deployments.</span></span>
* <span data-ttu-id="918f0-117">Exemplos de migração de implantações existentes, de servidores autônomos e implantações usando grupos de disponibilidade SQL AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="918f0-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="918f0-118">Abordagens de migração possíveis.</span><span class="sxs-lookup"><span data-stu-id="918f0-118">Possible migration approaches.</span></span>
* <span data-ttu-id="918f0-119">Exemplo completo de ponta a ponta, mostrando as etapas do Azure, Windows e SQL Server para a migração de saudação de uma implementação existente do AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="918f0-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for hello migration of an existing Always On implementation.</span></span>

<span data-ttu-id="918f0-120">Para obter informações gerais sobre o SQL Server nas Máquinas Virtuais do Azure, consulte [SQL Server nas Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="918f0-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="918f0-121">**Autor:** Daniel Sol **Revisores Técnicos:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span><span class="sxs-lookup"><span data-stu-id="918f0-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="918f0-122">Pré-requisitos para o Armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="918f0-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="918f0-123">Existem vários pré-requisitos para o uso do Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="918f0-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="918f0-124">Tamanho do computador</span><span class="sxs-lookup"><span data-stu-id="918f0-124">Machine size</span></span>
<span data-ttu-id="918f0-125">Para usar o armazenamento Premium, você precisará toouse DS série máquinas virtuais (VM).</span><span class="sxs-lookup"><span data-stu-id="918f0-125">For using Premium Storage you will need toouse DS series Virtual Machines (VM).</span></span> <span data-ttu-id="918f0-126">Se você não usou máquinas da série DS no seu serviço de nuvem antes, exclua Olá existente VM, mantenha os discos Olá anexado e, em seguida, criar um novo serviço de nuvem antes de recriar Olá VM como tamanho de função DS *.</span><span class="sxs-lookup"><span data-stu-id="918f0-126">If you have not used DS Series machines in your cloud service before, you must delete hello existing VM, keep hello attached disks, and then create a new cloud service before recreating hello VM as DS* role size.</span></span> <span data-ttu-id="918f0-127">Para saber mais sobre os tamanhos das Máquinas Virtuais, consulte [Tamanhos da Máquina Virtual e do Serviço de Nuvem do Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="918f0-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="918f0-128">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="918f0-128">Cloud services</span></span>
<span data-ttu-id="918f0-129">Você só poderá usar VMs DS* com Armazenamento Premium quando elas forem criadas em um novo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="918f0-129">You can only use DS* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="918f0-130">Se você estiver usando o SQL Server Always On no Azure, Olá sempre ouvinte fará referência toohello endereço interno do Azure ou de IP externo de Balanceador de carga que está associado um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="918f0-130">If you are using SQL Server Always On in Azure, hello Always On Listener will refer toohello Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="918f0-131">Este artigo se concentra em como toomigrate mantendo a disponibilidade nesse cenário.</span><span class="sxs-lookup"><span data-stu-id="918f0-131">This article focuses on how toomigrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="918f0-132">Uma série DS * deve ser Olá primeira VM é implantada toohello novo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="918f0-132">A DS* Series must be hello first VM that is deployed toohello new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="918f0-133">VNETS regionais</span><span class="sxs-lookup"><span data-stu-id="918f0-133">Regional VNETS</span></span>
<span data-ttu-id="918f0-134">Para VMs DS *, você deve configurar Olá rede Virtual (VNET) hospeda seu toobe VMs regional.</span><span class="sxs-lookup"><span data-stu-id="918f0-134">For DS* VMs you must configure hello Virtual Network (VNET) hosting your VMs toobe regional.</span></span> <span data-ttu-id="918f0-135">Este hello "amplia" VNET é tooallow Olá maior VMs toobe provisionado em outros clusters e permitir a comunicação entre eles.</span><span class="sxs-lookup"><span data-stu-id="918f0-135">This “widens” hello VNET is tooallow hello larger VMs toobe provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="918f0-136">Olá captura de tela a seguir, hello local realçado mostra VNETs regionais, enquanto o primeiro resultado de saudação mostra uma rede virtual "restrito".</span><span class="sxs-lookup"><span data-stu-id="918f0-136">In hello following screenshot, hello highlighted Location shows regional VNETs, whereas hello first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="918f0-138">Você pode gerar um tooa de toomigrate do tíquete de suporte Microsoft VNET regional, Microsoft fará uma alteração, então toocomplete Olá migração tooregional VNETs, altere a propriedade de Olá AffinityGroup na configuração de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-138">You can raise a Microsoft support ticket toomigrate tooa regional VNET, Microsoft will make a change, then toocomplete hello migration tooregional VNETs, change hello property AffinityGroup in hello network configuration.</span></span> <span data-ttu-id="918f0-139">Exportar primeiro Olá configuração de rede no PowerShell e substitua Olá **AffinityGroup** propriedade Olá **VirtualNetworkSite** elemento com um **local** propriedade.</span><span class="sxs-lookup"><span data-stu-id="918f0-139">First export hello Network Configuration in PowerShell, and then replace hello **AffinityGroup** property in hello **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="918f0-140">Especifique `Location = XXXX` onde `XXXX` é uma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="918f0-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="918f0-141">Importe configuração nova hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-141">Then import hello new configuration.</span></span>

<span data-ttu-id="918f0-142">Por exemplo, considerando Olá configuração da rede virtual a seguir:</span><span class="sxs-lookup"><span data-stu-id="918f0-142">For example, considering hello following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="918f0-143">toomove este tooa VNET regional na Europa Ocidental, alterar Olá toohello de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="918f0-143">toomove this tooa regional VNET in West Europe, change hello configuration toohello following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="918f0-144">Contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="918f0-144">Storage accounts</span></span>
<span data-ttu-id="918f0-145">Você precisará toocreate uma nova conta de armazenamento que está configurada para o armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="918f0-145">You will need toocreate a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="918f0-146">Observe que o uso de saudação do armazenamento Premium é definido na conta de armazenamento hello, não em VHDs individuais, no entanto, ao usar uma VM série DS * você pode anexar do VHD de contas de armazenamento padrão e Premium.</span><span class="sxs-lookup"><span data-stu-id="918f0-146">Note that hello use of Premium Storage is set at hello storage account, not on individual VHDs, however when using a DS* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="918f0-147">Você pode considerar isso se você não quiser tooplace Olá VHD do sistema operacional em toohello conta de armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="918f0-147">You may consider this if you do not want tooplace hello OS VHD on toohello Premium Storage account.</span></span>

<span data-ttu-id="918f0-148">a seguir Olá **New-AzureStorageAccountPowerShell** com hello "Premium_LRS" **tipo** cria uma conta de armazenamento Premium:</span><span class="sxs-lookup"><span data-stu-id="918f0-148">hello following **New-AzureStorageAccountPowerShell** command with hello "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="918f0-149">Configurações de Cache de VHDs</span><span class="sxs-lookup"><span data-stu-id="918f0-149">VHDs Cache Settings</span></span>
<span data-ttu-id="918f0-150">Olá principal diferença entre a criação de discos que fazem parte de uma conta de armazenamento Premium é configuração de cache de disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-150">hello main difference between creating disks that are part of a Premium Storage account is hello disk cache setting.</span></span> <span data-ttu-id="918f0-151">Para discos do volume SQL Server Data, recomendamos que você use ‘**Caching de Leitura**’.</span><span class="sxs-lookup"><span data-stu-id="918f0-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="918f0-152">Para volumes de log de transações, configuração de cache de disco de saudação deve ser definida muito '**nenhum**'.</span><span class="sxs-lookup"><span data-stu-id="918f0-152">For Transaction log volumes, hello disk cache setting should be set too‘**None**’.</span></span> <span data-ttu-id="918f0-153">Isso é diferente das recomendações Olá para contas de armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="918f0-153">This is different from hello recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="918f0-154">Depois que os VHDs Olá foram anexados, configuração de cache de saudação não pode ser alterada.</span><span class="sxs-lookup"><span data-stu-id="918f0-154">Once hello VHDs have been attached, hello cache setting cannot be altered.</span></span> <span data-ttu-id="918f0-155">Você precisa toodetach e reconecte Olá VHD com uma configuração de cache atualizado.</span><span class="sxs-lookup"><span data-stu-id="918f0-155">You would need toodetach and reattach hello VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="918f0-156">Espaços de armazenamento do Windows</span><span class="sxs-lookup"><span data-stu-id="918f0-156">Windows storage spaces</span></span>
<span data-ttu-id="918f0-157">Você pode usar [espaços de armazenamento do Windows](https://technet.microsoft.com/library/hh831739.aspx) como você fez com o armazenamento padrão anterior, isso permitirá que você toomigrate uma máquina virtual que já está usando espaços de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="918f0-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you toomigrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="918f0-158">exemplo Hello [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (etapa 9 e posteriores) demonstra Olá tooextract de código do Powershell e importar uma VM com vários VHDs anexados.</span><span class="sxs-lookup"><span data-stu-id="918f0-158">hello example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates hello Powershell code tooextract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="918f0-159">Pools de armazenamento foram usados com taxa de transferência tooenhance conta de armazenamento de Azure padrão e reduzem a latência.</span><span class="sxs-lookup"><span data-stu-id="918f0-159">Storage Pools were used with Standard Azure storage account tooenhance throughput and reduce latency.</span></span> <span data-ttu-id="918f0-160">Talvez você ache interessante testar Pools de Armazenamento com o Armazenamento Premium para novas implantações, mas isso agrega uma complexidade adicional com a configuração do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="918f0-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a><span data-ttu-id="918f0-161">Como toofind toostorage pools de mapear os discos virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="918f0-161">How toofind which Azure Virtual Disks map toostorage pools</span></span>
<span data-ttu-id="918f0-162">Como há recomendações de configuração de cache diferentes para VHDs anexados, você pode decidir toocopy Olá VHDs tooa conta de armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="918f0-162">As there are different cache setting recommendations for attached VHDs, you might decide toocopy hello VHDs tooa Premium Storage account.</span></span> <span data-ttu-id="918f0-163">No entanto, quando você reconectá-las toohello nova série DS VM, talvez seja necessário tooalter as configurações de cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-163">However, when you reattach them toohello new DS series VM, you might need tooalter hello cache settings.</span></span> <span data-ttu-id="918f0-164">É mais simples Olá tooapply que armazenamento Premium recomendada as configurações de cache quando houver VHDs separados para Olá de dados do SQL arquivos e log arquivos (em vez de um único VHD que contém ambos).</span><span class="sxs-lookup"><span data-stu-id="918f0-164">It is simpler tooapply hello Premium Storage recommended cache settings when you have separate VHDs for hello SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="918f0-165">Se você tiver arquivos de log e de dados do SQL Server no mesmo volume, Olá cache opção que você escolher depende de padrões de acesso de e/s de saudação para suas cargas de trabalho do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-165">If you have SQL Server data and log files on hello same volume, hello caching option you choose depends on hello IO access patterns for your database workloads.</span></span> <span data-ttu-id="918f0-166">Apenas o teste pode demonstrar qual opção de cache é ideal para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="918f0-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="918f0-167">No entanto, se você estiver usando espaços de armazenamento do Windows que são compostos de vários VHDs, você precisará toolook no seu tooidentify scripts originais que VHDs anexos são em qual pool específico, então você pode definir as configurações de cache Olá adequadamente para cada disco.</span><span class="sxs-lookup"><span data-stu-id="918f0-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need toolook at your original scripts tooidentify which attached VHDs are in what specific pool, so you can then set hello cache settings accordingly for each disk.</span></span>

<span data-ttu-id="918f0-168">Se você não tiver original tooshow disponíveis do script qual mapeiam VHDs toohello pool de armazenamento, você pode usar o hello mapeamento de pool de armazenamento em disco/etapas toodetermine Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="918f0-168">If you do not have original script available tooshow you which VHDs map toohello storage pool, you can use hello following steps toodetermine hello disk/storage pool mapping.</span></span>

<span data-ttu-id="918f0-169">Para cada disco, use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="918f0-169">For each disk, use hello following steps:</span></span>

1. <span data-ttu-id="918f0-170">Obter uma lista de discos anexados tooVM com hello **Get-AzureVM** comando:</span><span class="sxs-lookup"><span data-stu-id="918f0-170">Get list of disks attached tooVM with hello **Get-AzureVM** command:</span></span>

    <span data-ttu-id="918f0-171">Get-AzureVM -ServiceName <servicename> -Nome <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="918f0-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="918f0-172">Observe hello Diskname e LUN.</span><span class="sxs-lookup"><span data-stu-id="918f0-172">Note hello Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="918f0-174">Área de trabalho remota Olá VM.</span><span class="sxs-lookup"><span data-stu-id="918f0-174">Remote desktop into hello VM.</span></span> <span data-ttu-id="918f0-175">Em seguida, acesse muito**gerenciamento do computador** | **Gerenciador de dispositivos** | **unidades de disco**.</span><span class="sxs-lookup"><span data-stu-id="918f0-175">Then go too**Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="918f0-176">Examinar as propriedades de saudação de cada Olá 'Microsoft discos virtuais'</span><span class="sxs-lookup"><span data-stu-id="918f0-176">Look at hello properties of each of hello ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="918f0-178">número LUN Olá aqui é um número LUN de toohello referência que você especificar ao anexar o VHD de saudação toohello VM.</span><span class="sxs-lookup"><span data-stu-id="918f0-178">hello LUN number here is a reference toohello LUN number you specify when attaching hello VHD toohello VM.</span></span>
5. <span data-ttu-id="918f0-179">Para Olá 'Microsoft Virtual Disk' go toohello **detalhes** guia e, em seguida, na Olá **propriedade** lista, vá muito**chave Driver**.</span><span class="sxs-lookup"><span data-stu-id="918f0-179">For hello ‘Microsoft Virtual Disk’ go toohello **Details** tab, then in hello **Property** list, go too**Driver Key**.</span></span> <span data-ttu-id="918f0-180">Em Olá **valor**, Olá Observação **deslocamento**, que é 0002 em Olá captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="918f0-180">In hello **Value**, note hello **Offset**, which is 0002 in hello following screenshot.</span></span> <span data-ttu-id="918f0-181">Olá 0002 denota hello PhysicalDisk2 Olá referências de pool de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="918f0-181">hello 0002 denotes hello PhysicalDisk2 that hello storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="918f0-183">Para cada pool de armazenamento, o despejo de saudação associado discos:</span><span class="sxs-lookup"><span data-stu-id="918f0-183">For each storage pool, dump out hello associated disks:</span></span>

    <span data-ttu-id="918f0-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="918f0-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="918f0-186">Agora você pode usar este tooassociate informações anexado VHDs tooPhysical discos em Pools de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="918f0-186">Now you can use this information tooassociate attached VHDs tooPhysical Disks in Storage Pools.</span></span>

<span data-ttu-id="918f0-187">Depois que você mapeou VHDs tooPhysical discos em Pools de armazenamento, em seguida, você pode desanexar e copiá-los em tooa conta de armazenamento Premium, em seguida, anexá-los com configuração de cache correto hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-187">Once you have mapped VHDs tooPhysical Disks in Storage Pools you can then detach and copy them over tooa Premium Storage account, then attach them with hello correct cache setting.</span></span> <span data-ttu-id="918f0-188">Consulte o exemplo hello em hello [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), as etapas de 8 a 12.</span><span class="sxs-lookup"><span data-stu-id="918f0-188">Please see hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="918f0-189">Estas etapas mostram como tooextract um VHD anexado VMs disco tooa CSV arquivo de configuração copiar VHDs hello, alterar configurações de cache de configuração de disco hello e finalmente reimplantar Olá VM como conectado de uma VM da série DS com hello todos os discos.</span><span class="sxs-lookup"><span data-stu-id="918f0-189">These steps show how tooextract a VM-attached VHD disk configuration tooa CSV file, copy hello VHDs, alter hello disk configuration cache settings, and finally redeploy hello VM as a DS series VM with all hello attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="918f0-190">Largura de banda de armazenamento de VM e taxa de transferência de armazenamento de VHD</span><span class="sxs-lookup"><span data-stu-id="918f0-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="918f0-191">saudação de desempenho de armazenamento depende Olá tamanho de DS * VM especificado e Olá tamanhos VHD.</span><span class="sxs-lookup"><span data-stu-id="918f0-191">hello amount of storage performance depends on hello DS* VM size specified and hello VHD sizes.</span></span> <span data-ttu-id="918f0-192">Olá VMs tem permissões diferentes para o número de saudação de VHDs que podem ser anexados e Olá largura de banda máxima (MB/s) será oferecido suporte.</span><span class="sxs-lookup"><span data-stu-id="918f0-192">hello VMs have different allowances for hello number of VHDs that can be attached and hello maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="918f0-193">Para números de largura de banda específica hello, consulte [Máquina Virtual e tamanhos de serviço de nuvem para Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="918f0-193">For hello specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="918f0-194">Mais IOPS são obtidos com tamanhos de disco maiores.</span><span class="sxs-lookup"><span data-stu-id="918f0-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="918f0-195">Considere isso quando você pensar em seu caminho de migração.</span><span class="sxs-lookup"><span data-stu-id="918f0-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="918f0-196">Para obter detalhes, [consulte tabela Olá para tipos de disco de IOPS e](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="918f0-196">For details, [see hello table for IOPS and Disk Types](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="918f0-197">Por fim, considere que as VMs têm larguras de banda máxima de disco diferentes que aceitarão para todos os discos anexados.</span><span class="sxs-lookup"><span data-stu-id="918f0-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="918f0-198">Sob alta carga, você pode saturar Olá disco máxima largura de banda disponível para esse tamanho de função VM.</span><span class="sxs-lookup"><span data-stu-id="918f0-198">Under high load, you could saturate hello maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="918f0-199">Por exemplo um Standard_DS14 dará suporte a too512MB/s. Portanto, com três discos P30 você poderia saturar a largura de banda de disco de saudação do hello VM.</span><span class="sxs-lookup"><span data-stu-id="918f0-199">For example a Standard_DS14 will support up too512MB/s; therefore, with three P30 disks you could saturate hello disk bandwidth of hello VM.</span></span> <span data-ttu-id="918f0-200">Mas, neste exemplo, o limite de taxa de transferência Olá poderá ser excedido dependendo da combinação de saudação de leitura e gravação de IOs.</span><span class="sxs-lookup"><span data-stu-id="918f0-200">But in this example, hello throughput limit could be exceeded depending on hello mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="918f0-201">Novas implantações</span><span class="sxs-lookup"><span data-stu-id="918f0-201">New deployments</span></span>
<span data-ttu-id="918f0-202">duas seções seguintes Olá demonstram como você pode implantar VMs do SQL Server tooPremium armazenamento.</span><span class="sxs-lookup"><span data-stu-id="918f0-202">hello next two sections demonstrate how you can deploy SQL Server VMs tooPremium Storage.</span></span> <span data-ttu-id="918f0-203">Como mencionado anteriormente, não é necessariamente necessário disco do sistema operacional Olá tooplace em armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="918f0-203">As mentioned before, you do not necessarily need tooplace hello OS disk onto Premium storage.</span></span> <span data-ttu-id="918f0-204">Você pode escolher toodo isso se você estiver pretendendo tooplace qualquer cargas de trabalho intensivas de e/s em Olá VHD do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="918f0-204">You might choose toodo this if you are intending tooplace any intensive IO workloads on hello OS VHD.</span></span>

<span data-ttu-id="918f0-205">Olá primeiro exemplo demonstra o uso de imagens da galeria existente do Azure.</span><span class="sxs-lookup"><span data-stu-id="918f0-205">hello first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="918f0-206">Olá segundo exemplo mostra como toouse uma VM personalizada da imagem que você tem em uma conta de armazenamento padrão existente.</span><span class="sxs-lookup"><span data-stu-id="918f0-206">hello second example shows how toouse a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="918f0-207">Esses exemplos pressupõem que você já tenha criou um VNET regional.</span><span class="sxs-lookup"><span data-stu-id="918f0-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="918f0-208">Criar uma nova VM com Armazenamento Premium com Imagem da Galeria</span><span class="sxs-lookup"><span data-stu-id="918f0-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="918f0-209">exemplo Hello abaixo mostra como tooplace Olá VHD do sistema operacional para o armazenamento premium e anexar VHDs de armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="918f0-209">hello example below shows how tooplace hello OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="918f0-210">No entanto, você pode também colocar o disco do sistema operacional Olá em uma conta de armazenamento padrão e, em seguida, anexar VHDs que residem em uma conta de armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="918f0-210">However, you can also place hello OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="918f0-211">Ambos os cenários são demonstrados.</span><span class="sxs-lookup"><span data-stu-id="918f0-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="918f0-212">Etapa 1: criar uma conta de Armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="918f0-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="918f0-213">Etapa 2: criar um novo serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="918f0-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="918f0-214">Etapa 3: reservar um VIP de serviço de nuvem (opcional)</span><span class="sxs-lookup"><span data-stu-id="918f0-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="918f0-215">Etapa 4: criar um contêiner de VM</span><span class="sxs-lookup"><span data-stu-id="918f0-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="918f0-216">Etapa 5: colocar o VHD do sistema operacional no armazenamento Padrão ou Premium</span><span class="sxs-lookup"><span data-stu-id="918f0-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="918f0-217">Etapa 6: criar uma VM</span><span class="sxs-lookup"><span data-stu-id="918f0-217">Step 6: Create VM</span></span>
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a><span data-ttu-id="918f0-218">Criar um novo toouse VM armazenamento Premium com uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="918f0-218">Create a new VM toouse Premium Storage with a custom image</span></span>
<span data-ttu-id="918f0-219">Este cenário demonstra onde você tem imagens personalizadas existentes que residem em uma conta de Armazenamento Padrão.</span><span class="sxs-lookup"><span data-stu-id="918f0-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="918f0-220">Conforme mencionado se você quiser tooplace Olá VHD do sistema operacional no armazenamento Premium que você precisará toocopy Olá imagem que existe na conta de armazenamento padrão de saudação e transferi-las tooa armazenamento Premium antes de ser usada.</span><span class="sxs-lookup"><span data-stu-id="918f0-220">As mentioned if you want tooplace hello OS VHD on Premium Storage you will need toocopy hello image that exists in hello Standard Storage account and transfer them tooa Premium Storage before it can be used.</span></span> <span data-ttu-id="918f0-221">Se você tiver uma imagem no local, você pode também usar esse método toocopy diretamente toohello conta de armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="918f0-221">If you have an image on-premises, you can also use this method toocopy that directly toohello Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="918f0-222">Etapa 1: criar conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="918f0-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="918f0-223">Etapa 2: criar serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="918f0-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="918f0-224">Etapa 3: Usar a imagem existente</span><span class="sxs-lookup"><span data-stu-id="918f0-224">Step 3: Use existing image</span></span>
<span data-ttu-id="918f0-225">Você pode usar uma imagem existente.</span><span class="sxs-lookup"><span data-stu-id="918f0-225">You can use an existing image.</span></span> <span data-ttu-id="918f0-226">Ou você também pode [capturar uma imagem de uma máquina existente](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="918f0-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="918f0-227">Máquina de saudação Observação que você a imagem não tem toobe DS * máquina.</span><span class="sxs-lookup"><span data-stu-id="918f0-227">Note hello machine you image does not have toobe DS* machine.</span></span> <span data-ttu-id="918f0-228">Uma vez que a imagem de hello, Olá mostram as etapas a seguir como toocopy-toohello conta de armazenamento Premium Olá **AzureStorageBlobCopy início** commandlet PowerShell.</span><span class="sxs-lookup"><span data-stu-id="918f0-228">Once you have hello image, hello following steps show how toocopy it toohello Premium Storage account with hello **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="918f0-229">Etapa 4: copiar o Blob entre contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="918f0-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="918f0-230">Etapa 5: verificar regularmente o status da cópia:</span><span class="sxs-lookup"><span data-stu-id="918f0-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a><span data-ttu-id="918f0-231">Etapa 6: Adicionar tooAzure de disco imagem repositório na assinatura</span><span class="sxs-lookup"><span data-stu-id="918f0-231">Step 6: Add Image disk tooAzure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="918f0-232">Você pode achar que, embora os relatórios de status de saudação como êxito, você pode obter um erro de concessão de disco.</span><span class="sxs-lookup"><span data-stu-id="918f0-232">You may find that even though hello status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="918f0-233">Nesse caso, espere cerca de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="918f0-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-hello-vm"></a><span data-ttu-id="918f0-234">Etapa 7: Criar hello VM</span><span class="sxs-lookup"><span data-stu-id="918f0-234">Step 7:  Build hello VM</span></span>
<span data-ttu-id="918f0-235">Aqui, você está criando Olá VM de sua imagem e anexar dois VHDs de armazenamento Premium:</span><span class="sxs-lookup"><span data-stu-id="918f0-235">Here you are building hello VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="918f0-236">Implantações existentes que não usam grupos de disponibilidade AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="918f0-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="918f0-237">Para as implantações existentes, consulte primeiro Olá [pré-requisitos](#prerequisites-for-premium-storage) seção deste tópico.</span><span class="sxs-lookup"><span data-stu-id="918f0-237">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="918f0-238">Há considerações diferentes para implantações do SQL Server que não usam grupos de disponibilidade AlwaysOn e aquelas que usam.</span><span class="sxs-lookup"><span data-stu-id="918f0-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="918f0-239">Se você não estiver usando o AlwaysOn e tiver um autônomo existente do SQL Server, você pode atualizar tooPremium armazenamento usando uma nova conta de armazenamento e serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="918f0-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade tooPremium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="918f0-240">Considere Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="918f0-240">Consider hello following options:</span></span>

* <span data-ttu-id="918f0-241">**Criar uma nova VM do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="918f0-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="918f0-242">Você pode criar uma nova VM do SQL Server que usa uma conta de Armazenamento Premium, conforme documentado em Novas implantações.</span><span class="sxs-lookup"><span data-stu-id="918f0-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="918f0-243">Em seguida, faça uma operação de backup e restauração de seus bancos de dados de configuração e usuário do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="918f0-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="918f0-244">Olá aplicativo precisará toobe atualizado tooreference Olá novo SQL Server se ele estiver sendo acessado interna ou externamente.</span><span class="sxs-lookup"><span data-stu-id="918f0-244">hello application will need toobe updated tooreference hello new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="918f0-245">Você precisaria toocopy todos os objetos 'fora do banco de dados' como se fosse uma migração do lado a lado (SxS) SQL Server.</span><span class="sxs-lookup"><span data-stu-id="918f0-245">You would need toocopy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="918f0-246">Isso inclui objetos como logons, certificados e servidores vinculados.</span><span class="sxs-lookup"><span data-stu-id="918f0-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="918f0-247">**Migrar uma VM existente do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="918f0-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="918f0-248">Isso exigirá colocar offline o hello VM do SQL Server e, em seguida, transferi-lo tooa novo serviço de nuvem, que inclui a cópia de todos os seu toohello de VHDs anexado conta de armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="918f0-248">This will require taking hello SQL Server VM offline, then transferring it tooa new cloud service, which includes copying all of its attached VHDs toohello Premium Storage account.</span></span> <span data-ttu-id="918f0-249">Quando Olá VM fica online, aplicativo hello fará referência a nome de host de servidor hello como antes.</span><span class="sxs-lookup"><span data-stu-id="918f0-249">When hello VM comes online, hello application will reference hello server host name as before.</span></span> <span data-ttu-id="918f0-250">Lembre-se de que o tamanho Olá de disco existente Olá afetará características de desempenho de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-250">Be aware that hello size of hello existing disk will affect hello performance characteristics.</span></span> <span data-ttu-id="918f0-251">Por exemplo, um disco de 400 GB obtém arredondado tooa P20.</span><span class="sxs-lookup"><span data-stu-id="918f0-251">For example, a 400 GB disk gets rounded up tooa P20.</span></span> <span data-ttu-id="918f0-252">Se você souber que você não precisa que o desempenho do disco, você pode recriar Olá VM como uma VM da série DS e anexar VHDs de armazenamento Premium da especificação de tamanho e desempenho Olá que precisar.</span><span class="sxs-lookup"><span data-stu-id="918f0-252">If you know that you do not require that disk performance, then you could recreate hello VM as a DS Series VM, and attach Premium Storage VHDs of hello size/performance specification you require.</span></span> <span data-ttu-id="918f0-253">Em seguida, você pode desanexar e anexar novamente os arquivos de banco de dados SQL Olá.</span><span class="sxs-lookup"><span data-stu-id="918f0-253">Then you could detach and reattach hello SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="918f0-254">Ao copiar os discos VHD de saudação, você deve estar ciente do tamanho hello, dependendo do tamanho da saudação significa que o tipo de disco de armazenamento Premium eles se encaixam, isso determina a especificação de desempenho de disco.</span><span class="sxs-lookup"><span data-stu-id="918f0-254">When copying hello VHD disks you should be aware of hello size, depending on hello size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="918f0-255">Tamanho do Azure será arredondado backup toohello mais próximo do disco, para que se você tiver um disco de 400 GB, isso será arredondado tooa P20.</span><span class="sxs-lookup"><span data-stu-id="918f0-255">Azure will round up toohello nearest disk size, so if you have a 400GB disk, this will be rounded up tooa P20.</span></span> <span data-ttu-id="918f0-256">Dependendo dos requisitos de e/s existentes de saudação VHD do sistema operacional, talvez não seja necessário toomigrate este tooa conta de armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="918f0-256">Depending on your existing IO requirements of hello OS VHD, you might not need toomigrate this tooa Premium Storage account.</span></span>
>
>

<span data-ttu-id="918f0-257">Se o SQL Server for acessado externamente, Olá VIP de serviço de nuvem será alterado.</span><span class="sxs-lookup"><span data-stu-id="918f0-257">If your SQL Server is accessed externally, then hello cloud service VIP will change.</span></span> <span data-ttu-id="918f0-258">Você também terá DNS, as ACLs e pontos de extremidade tooupdate configurações.</span><span class="sxs-lookup"><span data-stu-id="918f0-258">You will also have tooupdate end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="918f0-259">Implantações existentes que usam grupos de disponibilidade AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="918f0-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="918f0-260">Para as implantações existentes, consulte primeiro Olá [pré-requisitos](#prerequisites-for-premium-storage) seção deste tópico.</span><span class="sxs-lookup"><span data-stu-id="918f0-260">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="918f0-261">No início desta seção, vamos examinar como o AlwaysOn interage com a Rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="918f0-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="918f0-262">Em seguida, dividiremos migrações em cenários de tootwo: migrações onde algum tempo de inatividade pode ser tolerado e migrações onde você deve obter o tempo de inatividade mínimo.</span><span class="sxs-lookup"><span data-stu-id="918f0-262">We will then break down migrations in tootwo scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="918f0-263">Os grupos de disponibilidade AlwaysOn locais do SQL Server usam um Ouvinte local que registra um nome DNS virtual junto com um endereço IP que é compartilhado entre um ou mais SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="918f0-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="918f0-264">Quando os clientes se conectam sejam roteadas por meio de saudação ouvinte IP toohello principal do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="918f0-264">When clients connect they are routed through hello listener IP toohello Primary SQL Server.</span></span> <span data-ttu-id="918f0-265">Este é o servidor de saudação que possui Olá recurso sempre IP nesse momento.</span><span class="sxs-lookup"><span data-stu-id="918f0-265">This is hello server that owns hello Always On IP resource at that time.</span></span>

![DeploymentsUseAlways On][6]

<span data-ttu-id="918f0-267">No Microsoft Azure, você pode ter tooa de endereço atribuído apenas um IP NIC em Olá VM, na ordem tooachieve Olá mesma camada de abstração, como local, Azure utiliza o endereço IP de saudação que é atribuído a balanceadores de carga interno ou externo toohello ILB/ELB ().</span><span class="sxs-lookup"><span data-stu-id="918f0-267">In Microsoft Azure you can have only one IP address assigned tooa NIC on hello VM, so in order tooachieve hello same layer of abstraction as on-premises, Azure utilizes hello IP address that is assigned toohello Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="918f0-268">o recurso IP Hello que é compartilhado entre servidores hello está definido toohello mesmo IP como Olá ILB/ELB.</span><span class="sxs-lookup"><span data-stu-id="918f0-268">hello IP resource that is shared between hello servers is set toohello same IP as hello ILB/ELB.</span></span> <span data-ttu-id="918f0-269">Isso é publicado no hello DNS, e o tráfego do cliente é passado por meio de réplica do hello ILB/ELB toohello SQL Server primário.</span><span class="sxs-lookup"><span data-stu-id="918f0-269">This is published in hello DNS, and client traffic is passed through hello ILB/ELB toohello Primary SQL Server replica.</span></span> <span data-ttu-id="918f0-270">Olá ILB/ELB sabe a qual o SQL Server é primário desde que ele usa testes tooprobe Olá sempre IP recursos.</span><span class="sxs-lookup"><span data-stu-id="918f0-270">hello ILB/ELB knows which SQL Server is primary since it uses probes tooprobe hello Always On IP resource.</span></span> <span data-ttu-id="918f0-271">No exemplo anterior de saudação, sondas de cada nó que possui um ponto de extremidade referenciado por Olá ELB/ILB, aquele que responde é Olá principal do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="918f0-271">In hello previous example, it probes each node that has an endpoint referenced by hello ELB/ILB, whichever responds is hello Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="918f0-272">Olá ILB e ELB forem atribuídos tooa serviço de nuvem do Azure específica, portanto qualquer migração para a nuvem no Azure provavelmente significa que Olá que IP do balanceador de carga será alterado.</span><span class="sxs-lookup"><span data-stu-id="918f0-272">hello ILB and ELB are both assigned tooa particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that hello Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="918f0-273">Migrando implantações AlwaysOn que podem permitir algum tempo de inatividade</span><span class="sxs-lookup"><span data-stu-id="918f0-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="918f0-274">Há duas estratégias toomigrate sempre em implantações que permitem a algum tempo de inatividade:</span><span class="sxs-lookup"><span data-stu-id="918f0-274">There are two strategies toomigrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="918f0-275">**Adicionar mais tooan réplicas secundárias existentes sempre em Cluster**</span><span class="sxs-lookup"><span data-stu-id="918f0-275">**Add more secondary replicas tooan existing Always On Cluster**</span></span>
2. <span data-ttu-id="918f0-276">**Migrar tooa sempre no Cluster novo**</span><span class="sxs-lookup"><span data-stu-id="918f0-276">**Migrate tooa new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a><span data-ttu-id="918f0-277">1. Adicionar mais tooan de réplicas secundárias existentes sempre Cluster</span><span class="sxs-lookup"><span data-stu-id="918f0-277">1. Add more Secondary Replicas tooan Existing Always On Cluster</span></span>
<span data-ttu-id="918f0-278">Uma estratégia é tooadd mais secundários toohello grupo de disponibilidade AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="918f0-278">One strategy is tooadd more secondaries toohello Always On Availability Group.</span></span> <span data-ttu-id="918f0-279">Você precisa tooadd em um novo serviço de nuvem e atualize o ouvinte Olá com hello novo IP do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="918f0-279">You need tooadd these into a new cloud service and update hello listener with hello new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="918f0-280">Pontos de tempo de inatividade:</span><span class="sxs-lookup"><span data-stu-id="918f0-280">Points of downtime:</span></span>
* <span data-ttu-id="918f0-281">Validação de cluster.</span><span class="sxs-lookup"><span data-stu-id="918f0-281">Cluster Validation.</span></span>
* <span data-ttu-id="918f0-282">Testando failovers AlwaysOn para secundárias novas.</span><span class="sxs-lookup"><span data-stu-id="918f0-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="918f0-283">Se você estiver usando Pools de armazenamento do Windows em Olá VM para maior taxa de transferência de e/s, em seguida, eles serão colocados offline durante uma validação completa de Cluster.</span><span class="sxs-lookup"><span data-stu-id="918f0-283">If you are using Windows Storage Pools within hello VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="918f0-284">é necessário um teste de validação de Hello quando você adicionar nós toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="918f0-284">hello validation test is required when you add nodes toohello cluster.</span></span> <span data-ttu-id="918f0-285">Olá tempo toorun teste de saudação pode variar, você deve testar isso em seu tooget do ambiente de teste representativo uma hora aproximada de quanto tempo isso leva.</span><span class="sxs-lookup"><span data-stu-id="918f0-285">hello time it takes toorun hello test can vary, so you should test this in your representative test environment tooget an approximate time of how long this will take.</span></span>

<span data-ttu-id="918f0-286">Você deve provisionar o tempo em que você pode executar o failover manual e caos testes em Olá recentemente adicionado nós tooensure sempre em funções de alta disponibilidade, conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="918f0-286">You should provision time where you can perform manual failover and chaos testing on hello newly added nodes tooensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="918f0-288">Você deve interromper todas as instâncias do SQL Server onde Olá Pools de armazenamento são usados antes hello validação é executada.</span><span class="sxs-lookup"><span data-stu-id="918f0-288">You should stop all instances of SQL Server where hello Storage Pools are used before hello Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="918f0-289">Etapas de alto nível</span><span class="sxs-lookup"><span data-stu-id="918f0-289">High-level steps</span></span>
>

1. <span data-ttu-id="918f0-290">Crie dois novos SQL Servers no novo serviço de nuvem com Armazenamento Premium anexado.</span><span class="sxs-lookup"><span data-stu-id="918f0-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="918f0-291">Copie sobre backups e restauração completos com **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="918f0-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="918f0-292">Copie sobre objetos dependentes de ‘banco de dados fora do usuário’, como logons etc.</span><span class="sxs-lookup"><span data-stu-id="918f0-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="918f0-293">Crie um novo ILB (balanceador de carga interno) ou use um ELB (balanceador de carga externo) e configure pontos de extremidade balanceados de carga em ambos os nós novos.</span><span class="sxs-lookup"><span data-stu-id="918f0-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="918f0-294">Verificar que todos os nós têm a configuração de ponto de extremidade correto Olá antes de continuar</span><span class="sxs-lookup"><span data-stu-id="918f0-294">Check all Nodes have hello correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="918f0-295">Pare toohello de acesso de usuário e de aplicativo do SQL Server (se estiver usando Pools de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="918f0-295">Stop User/Application Access toohello SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="918f0-296">Interrompa serviços de mecanismo do SQL Server em todos os nós (se você estiver usando pools de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="918f0-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="918f0-297">Adicionar novo toocluster de nós e execute a validação completa.</span><span class="sxs-lookup"><span data-stu-id="918f0-297">Add new Nodes toocluster and run full validation.</span></span>
8. <span data-ttu-id="918f0-298">Depois que a validação for bem-sucedida, inicie todos os Serviços do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="918f0-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="918f0-299">Faça backup dos logs de transações e restaure os bancos de dados do usuário.</span><span class="sxs-lookup"><span data-stu-id="918f0-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="918f0-300">Adicione novos nós Olá grupo de disponibilidade AlwaysOn e colocar a replicação em **síncrona**.</span><span class="sxs-lookup"><span data-stu-id="918f0-300">Add new nodes into hello Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="918f0-301">Adicionar IP hello recurso de endereço de saudação serviço de nuvem novo ILB/ELB por meio do PowerShell do AlwaysOn com base no exemplo de multissite Olá Olá [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="918f0-301">Add hello IP address resource of hello new Cloud Service ILB/ELB through PowerShell for Always On based on hello Multi-site example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="918f0-302">No cluster do Windows, defina Olá **possíveis proprietários** de saudação **endereço IP** recurso toohello novos nós antigos.</span><span class="sxs-lookup"><span data-stu-id="918f0-302">In Windows clustering, set hello **Possible owners** of hello **IP Address** resource toohello new nodes old.</span></span> <span data-ttu-id="918f0-303">Consulte a seção 'Adicionar recurso de endereço IP na mesma sub-rede' hello de saudação [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="918f0-303">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="918f0-304">Tooone de failover de nós de novo hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-304">Failover tooone of hello new nodes.</span></span>
13. <span data-ttu-id="918f0-305">Faça Olá novos nós parceiros de Failover automático e failovers de teste.</span><span class="sxs-lookup"><span data-stu-id="918f0-305">Make hello new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="918f0-306">Remova os nós originais do grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="918f0-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="918f0-307">Vantagens</span><span class="sxs-lookup"><span data-stu-id="918f0-307">Advantages</span></span>
* <span data-ttu-id="918f0-308">Novos servidores SQL pode ser testado (SQL Server e aplicativo) antes de serem adicionados tooAlways em.</span><span class="sxs-lookup"><span data-stu-id="918f0-308">New SQL Servers can be tested (SQL Server and Application) before they are added tooAlways On.</span></span>
* <span data-ttu-id="918f0-309">Você pode alterar o tamanho da VM hello e personalizar os requisitos exatos do hello armazenamento tooyour.</span><span class="sxs-lookup"><span data-stu-id="918f0-309">You can change hello VM size and customize hello storage tooyour exact requirements.</span></span> <span data-ttu-id="918f0-310">No entanto, seria útil tookeep todos os caminhos de arquivo SQL Olá Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="918f0-310">However, it would be beneficial tookeep all hello SQL file paths hello same.</span></span>
* <span data-ttu-id="918f0-311">Você pode controlar quando a transferência de saudação do toohello de backups de banco de dados de saudação réplicas secundárias são iniciados.</span><span class="sxs-lookup"><span data-stu-id="918f0-311">You can control when hello transfer of hello DB backups toohello Secondary Replicas are started.</span></span> <span data-ttu-id="918f0-312">Isso é diferente de usar o Azure **AzureStorageBlobCopy início** toocopy commandlet VHDs, pois é uma cópia assíncrona.</span><span class="sxs-lookup"><span data-stu-id="918f0-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet toocopy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="918f0-313">Desvantagens</span><span class="sxs-lookup"><span data-stu-id="918f0-313">Disadvantages</span></span>
* <span data-ttu-id="918f0-314">Ao usar Pools de armazenamento do Windows, há um tempo de inatividade do Cluster durante a saudação validação completa de Cluster para nós adicionais do novo hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-314">When using Windows Storage Pools, there is Cluster downtime during hello Full Cluster Validation for hello new additional nodes.</span></span>
* <span data-ttu-id="918f0-315">Dependendo Olá versão do SQL Server e do número de existente Olá das réplicas secundárias, você pode não ser capaz de tooadd mais réplicas secundárias sem remover secundários existentes.</span><span class="sxs-lookup"><span data-stu-id="918f0-315">Depending on hello SQL Server Version and hello existing number of secondary replicas, you might not be able tooadd more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="918f0-316">Pode haver muito tempo de transferência de dados SQL durante a configuração secundários hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-316">There could be long SQL data transfer time while setting up hello secondaries.</span></span>
* <span data-ttu-id="918f0-317">Há custos adicionais durante a migração quando há novas máquinas em execução em paralelo.</span><span class="sxs-lookup"><span data-stu-id="918f0-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-tooa-new-always-on-cluster"></a><span data-ttu-id="918f0-318">2. Migrar tooa sempre no Cluster novo</span><span class="sxs-lookup"><span data-stu-id="918f0-318">2. Migrate tooa new Always On Cluster</span></span>
<span data-ttu-id="918f0-319">Outra estratégia é toocreate uma nova sempre em Cluster conosco de novos no novo serviço de nuvem e, em seguida, redirecione Olá clientes toouse-lo.</span><span class="sxs-lookup"><span data-stu-id="918f0-319">Another strategy is toocreate a brand new Always On Cluster with brand new nodes in new cloud service and then redirect hello clients toouse it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="918f0-320">Pontos de tempo de inatividade</span><span class="sxs-lookup"><span data-stu-id="918f0-320">Points of downtime</span></span>
<span data-ttu-id="918f0-321">Não há tempo de inatividade durante a transferência de aplicativos e usuários toohello novo sempre no ouvinte.</span><span class="sxs-lookup"><span data-stu-id="918f0-321">There is downtime when you transfer applications and users toohello new Always On listener.</span></span> <span data-ttu-id="918f0-322">tempo de inatividade Olá depende:</span><span class="sxs-lookup"><span data-stu-id="918f0-322">hello downtime depends on:</span></span>

* <span data-ttu-id="918f0-323">Olá tempo toorestore toodatabases de backups de log de transações final em novos servidores.</span><span class="sxs-lookup"><span data-stu-id="918f0-323">hello time taken toorestore final transaction log backups toodatabases on new servers.</span></span>
* <span data-ttu-id="918f0-324">Olá tempo tooupdate cliente aplicativos toouse novo sempre no ouvinte.</span><span class="sxs-lookup"><span data-stu-id="918f0-324">hello time taken tooupdate client applications toouse new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="918f0-325">Vantagens</span><span class="sxs-lookup"><span data-stu-id="918f0-325">Advantages</span></span>
* <span data-ttu-id="918f0-326">Você pode testar o ambiente de produção real hello, SQL Server, e alterações de build do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="918f0-326">You can test hello actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="918f0-327">Você tem o armazenamento de Olá Olá opção toocustomize e toopotentially reduzir o tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="918f0-327">You have hello option toocustomize hello storage and toopotentially reduce size of VM.</span></span> <span data-ttu-id="918f0-328">Isso pode resultar na redução de custos.</span><span class="sxs-lookup"><span data-stu-id="918f0-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="918f0-329">Você pode atualizar sua compilação ou versão do SQL Server durante esse processo.</span><span class="sxs-lookup"><span data-stu-id="918f0-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="918f0-330">Você também pode atualizar o sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-330">You can also upgrade hello Operating System.</span></span>
* <span data-ttu-id="918f0-331">Olá que anterior sempre Cluster pode agir como um destino de reversão sólido.</span><span class="sxs-lookup"><span data-stu-id="918f0-331">hello previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="918f0-332">Desvantagens</span><span class="sxs-lookup"><span data-stu-id="918f0-332">Disadvantages</span></span>
* <span data-ttu-id="918f0-333">Se você quiser que ambos os clusters sempre em execução simultaneamente, é necessário toochange nome DNS de saudação do ouvinte de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-333">You need toochange hello DNS name of hello listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="918f0-334">Isso adiciona administração sobrecarga durante a migração de saudação como cadeias de caracteres de aplicativo cliente devem refletir o novo nome de ouvinte hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-334">This adds administration overhead during hello migration as client application strings must reflect hello new Listener name.</span></span>
* <span data-ttu-id="918f0-335">Você deve implementar um mecanismo de sincronização entre Olá dois ambientes tookeep-los como fechar como requisitos de sincronização final Olá toominimize possíveis antes da migração.</span><span class="sxs-lookup"><span data-stu-id="918f0-335">You must implement a synchronization mechanism between hello two environments tookeep them as close as possible toominimize hello final synchronization requirements before migration.</span></span>
* <span data-ttu-id="918f0-336">Há adicionada custo durante a migração enquanto você tem o novo ambiente de saudação em execução.</span><span class="sxs-lookup"><span data-stu-id="918f0-336">There is added cost during migration while you have hello new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="918f0-337">Migrando implantações AlwaysOn para tempo de inatividade mínimo</span><span class="sxs-lookup"><span data-stu-id="918f0-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="918f0-338">Existem duas estratégias para migrar implantações AlwaysOn para o tempo de inatividade mínimo:</span><span class="sxs-lookup"><span data-stu-id="918f0-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="918f0-339">**Utilizar uma réplica secundária existente: site único**</span><span class="sxs-lookup"><span data-stu-id="918f0-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="918f0-340">**Utilizar réplicas secundárias existentes: vários sites**</span><span class="sxs-lookup"><span data-stu-id="918f0-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="918f0-341">1. Utilizar uma réplica secundária existente: site único</span><span class="sxs-lookup"><span data-stu-id="918f0-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="918f0-342">Uma estratégia para o tempo de inatividade mínimo é tootake uma nuvem existente secundária e removê-lo Olá atual do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="918f0-342">One strategy for minimal downtime is tootake an existing cloud secondary and remove it from hello current cloud service.</span></span> <span data-ttu-id="918f0-343">Copie Olá VHDs toohello nova conta de armazenamento Premium e crie Olá VM no novo serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-343">Then copy hello VHDs toohello new Premium Storage account, and create hello VM in hello new cloud service.</span></span> <span data-ttu-id="918f0-344">Em seguida, atualize o ouvinte Olá em cluster e o failover.</span><span class="sxs-lookup"><span data-stu-id="918f0-344">Then update hello listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="918f0-345">Pontos de tempo de inatividade</span><span class="sxs-lookup"><span data-stu-id="918f0-345">Points of downtime</span></span>
* <span data-ttu-id="918f0-346">Não há tempo de inatividade quando você atualiza o nó final Olá com ponto de extremidade com balanceamento de carga do hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-346">There is downtime when you update hello final node with hello Load Balanced endpoint.</span></span>
* <span data-ttu-id="918f0-347">A reconexão do cliente pode ser atrasada dependendo da configuração do cliente/DNS.</span><span class="sxs-lookup"><span data-stu-id="918f0-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="918f0-348">Não há tempo de inatividade adicional se você escolher o grupo tootake Olá sempre Cluster offline tooswap endereços de IP hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-348">There is additional downtime if you choose tootake hello Always On Cluster group offline tooswap out hello IP addresses.</span></span> <span data-ttu-id="918f0-349">Você pode evitar isso usando uma dependência ou e proprietários possíveis para Olá adicionou o recurso de endereço IP.</span><span class="sxs-lookup"><span data-stu-id="918f0-349">You can avoid this by using an OR dependency and Possible Owners for hello added IP Address resource.</span></span> <span data-ttu-id="918f0-350">Consulte a seção 'Adicionar recurso de endereço IP na mesma sub-rede' hello de saudação [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="918f0-350">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="918f0-351">Quando você quiser Olá toopartake nó adicionado no como um sempre no parceiro de Failover, você precisa tooadd um ponto de extremidade do Azure com um toohello de referência de carga balanceada definido.</span><span class="sxs-lookup"><span data-stu-id="918f0-351">When you want hello added node toopartake in as an Always On Failover Partner, you need tooadd an Azure Endpoint with a reference toohello Load Balanced Set.</span></span> <span data-ttu-id="918f0-352">Quando você executa Olá **Add-AzureEndpoint** comando toodo, tooremain atual de conexões aberta, mas o novo ouvinte de toohello conexões não será capaz de toobe estabelecido balanceador de carga Olá foi atualizado.</span><span class="sxs-lookup"><span data-stu-id="918f0-352">When you run hello **Add-AzureEndpoint** command toodo this, current connections tooremain open, but new connections toohello listener will not be able toobe established until hello load balancer has updated.</span></span> <span data-ttu-id="918f0-353">No teste foi visto toolast 90-120seconds, isso deve ser testado.</span><span class="sxs-lookup"><span data-stu-id="918f0-353">In testing this was seen toolast 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="918f0-354">Vantagens</span><span class="sxs-lookup"><span data-stu-id="918f0-354">Advantages</span></span>
* <span data-ttu-id="918f0-355">Sem custo extra incorrido durante a migração.</span><span class="sxs-lookup"><span data-stu-id="918f0-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="918f0-356">Uma migração um-para-um.</span><span class="sxs-lookup"><span data-stu-id="918f0-356">A one-to-one migration.</span></span>
* <span data-ttu-id="918f0-357">Redução da complexidade.</span><span class="sxs-lookup"><span data-stu-id="918f0-357">Reduced complexity.</span></span>
* <span data-ttu-id="918f0-358">Permite maior IOPS de SKUs de Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="918f0-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="918f0-359">Quando parte de um 3º Olá discos são desanexados de saudação VM e copiados toohello novo serviço de nuvem, a ferramenta pode ser usado tooincrease Olá tamanho do VHD, que fornece a taxas de transferência mais altas.</span><span class="sxs-lookup"><span data-stu-id="918f0-359">When hello disks are detached from hello VM and copied toohello new cloud service, a 3rd party tool can be used tooincrease hello VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="918f0-360">Para tamanhos de VHD maiores, consulte este [fórum de discussão](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span><span class="sxs-lookup"><span data-stu-id="918f0-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="918f0-361">Desvantagens</span><span class="sxs-lookup"><span data-stu-id="918f0-361">Disadvantages</span></span>
* <span data-ttu-id="918f0-362">Há uma perda temporária de alta disponibilidade e recuperação de desastre durante a migração.</span><span class="sxs-lookup"><span data-stu-id="918f0-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="918f0-363">Como esta é uma migração 1:1, você terá toouse um tamanho de VM mínimo que oferecerá suporte ao seu número de VHDs, portanto você pode não ser capaz de toodownsize suas VMs.</span><span class="sxs-lookup"><span data-stu-id="918f0-363">As this is a 1:1 migration, you will have toouse a minimum VM size that will support your number of VHDs, so you might not be able toodownsize your VMs.</span></span>
* <span data-ttu-id="918f0-364">Esse cenário usa hello Azure **AzureStorageBlobCopy início** commandlet, que é assíncrona.</span><span class="sxs-lookup"><span data-stu-id="918f0-364">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="918f0-365">Não há nenhum SLA na conclusão da cópia.</span><span class="sxs-lookup"><span data-stu-id="918f0-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="918f0-366">tempo de saudação de cópias de saudação varia, enquanto isso depende de espera em fila também depende de quantidade de saudação do tootransfer de dados.</span><span class="sxs-lookup"><span data-stu-id="918f0-366">hello time of hello copies varies, while this depends on wait in queue it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="918f0-367">tempo de cópia de saudação aumenta se a transferência de saudação for tooanother data center do Azure que dá suporte ao armazenamento Premium em outra região.</span><span class="sxs-lookup"><span data-stu-id="918f0-367">hello copy time increases if hello transfer is going tooanother Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="918f0-368">Se você tiver apenas 2 nós, considere uma possível redução no caso de cópia Olá demora mais do que no teste.</span><span class="sxs-lookup"><span data-stu-id="918f0-368">If you just have 2 nodes, consider a possible mitigation in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="918f0-369">Isso pode incluir Olá ideias a seguir.</span><span class="sxs-lookup"><span data-stu-id="918f0-369">This could include hello following ideas.</span></span>
  * <span data-ttu-id="918f0-370">Adicione um nó do SQL Server 3º temporário para HA antes da migração de saudação com tempo de inatividade acordada.</span><span class="sxs-lookup"><span data-stu-id="918f0-370">Add a temporary 3rd SQL Server node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="918f0-371">Execute a migração Olá fora do Azure manutenção agendada.</span><span class="sxs-lookup"><span data-stu-id="918f0-371">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="918f0-372">Verifique se você configurou corretamente o quorum do cluster.</span><span class="sxs-lookup"><span data-stu-id="918f0-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="918f0-373">Etapas de alto nível</span><span class="sxs-lookup"><span data-stu-id="918f0-373">High-level steps</span></span>
<span data-ttu-id="918f0-374">Este documento demonstra um exemplo de tooend final completa, porém Olá [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) fornece detalhes que podem ser utilizado tooperform isso.</span><span class="sxs-lookup"><span data-stu-id="918f0-374">This document does not demonstrate a complete end tooend example, however hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged tooperform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="918f0-376">Obter configuração de disco e remover nó de saudação (não excluir VHDs anexados).</span><span class="sxs-lookup"><span data-stu-id="918f0-376">Gather disk configuration, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="918f0-377">Crie uma conta de armazenamento Premium e copiar VHDs de saudação conta de armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="918f0-377">Create a Premium Storage account and copy VHDs from hello Standard Storage account</span></span>
* <span data-ttu-id="918f0-378">Criar novo serviço de nuvem e reimplantar Olá VM SQL2 no serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="918f0-378">Create new cloud service and redeploy hello SQL2 VM in that cloud service.</span></span> <span data-ttu-id="918f0-379">Criar hello VM usar Olá copiados VHD original do sistema operacional e anexar Olá copiados VHDs.</span><span class="sxs-lookup"><span data-stu-id="918f0-379">Create hello VM using hello copied original OS VHD and attaching hello copied VHDs.</span></span>
* <span data-ttu-id="918f0-380">Configure o ILB / ELB e adicione pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="918f0-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="918f0-381">Siga um destes procedimentos para atualizar o ouvinte:</span><span class="sxs-lookup"><span data-stu-id="918f0-381">Update Listener by either:</span></span>
  * <span data-ttu-id="918f0-382">Levando Olá sempre grupo off-line e atualização Olá sempre no ouvinte com o novo ILB / endereço IP ELB.</span><span class="sxs-lookup"><span data-stu-id="918f0-382">Taking hello Always On Group offline and updating hello Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="918f0-383">Ou adicionar o recurso de endereço IP hello da nova nuvem serviço ILB/ELB por meio do PowerShell para clusters do Windows.</span><span class="sxs-lookup"><span data-stu-id="918f0-383">Or adding hello IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="918f0-384">Em seguida, conjunto Olá possíveis proprietários de saudação toohello de recurso de endereço IP migrados nó, SQL2 e defini-lo como dependência OR em Olá nome de rede.</span><span class="sxs-lookup"><span data-stu-id="918f0-384">Then set hello Possible owners of hello IP Address resource toohello migrated node, SQL2, and set this as OR dependency in hello Network Name.</span></span> <span data-ttu-id="918f0-385">Consulte a seção 'Adicionar recurso de endereço IP na mesma sub-rede' hello de saudação [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="918f0-385">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="918f0-386">Verifique se os clientes toohello de configuração/propagação DNS.</span><span class="sxs-lookup"><span data-stu-id="918f0-386">Check DNS configuration/propogation toohello clients.</span></span>
* <span data-ttu-id="918f0-387">Migre a VM do SQL1 e siga as etapas 2 a 4.</span><span class="sxs-lookup"><span data-stu-id="918f0-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="918f0-388">Se usar as etapas 5ii, em seguida, adicione SQL1 como um possível proprietário de saudação adicionado o recurso de endereço IP</span><span class="sxs-lookup"><span data-stu-id="918f0-388">If using steps 5ii, then add SQL1 as a Possible Owner for hello added IP Address Resource</span></span>
* <span data-ttu-id="918f0-389">Failovers de teste.</span><span class="sxs-lookup"><span data-stu-id="918f0-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="918f0-390">2. Utilizar réplicas secundárias existentes: vários sites</span><span class="sxs-lookup"><span data-stu-id="918f0-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="918f0-391">Se você tiver nós em mais de um datacenter do Azure (controlador de domínio) ou se você tiver um ambiente híbrido, você pode usar uma configuração de AlwaysOn esse tempo de inatividade do ambiente toominimize.</span><span class="sxs-lookup"><span data-stu-id="918f0-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment toominimize downtime.</span></span>

<span data-ttu-id="918f0-392">abordagem de saudação é toochange Olá sempre em sincronização tooSynchronous para Olá local ou controlador de domínio secundário do Azure e failover toothat do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="918f0-392">hello approach is toochange hello Always On synchronization tooSynchronous for hello on-premises or secondary Azure DC, and then failover over toothat SQL Server.</span></span> <span data-ttu-id="918f0-393">Copie Olá VHDs tooa conta de armazenamento Premium e reimplantar a máquina de saudação em um novo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="918f0-393">Then copy hello VHDs tooa Premium Storage account, and redeploy hello machine into a new cloud service.</span></span> <span data-ttu-id="918f0-394">Atualize o ouvinte hello e, em seguida, execute o failback.</span><span class="sxs-lookup"><span data-stu-id="918f0-394">Update hello listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="918f0-395">Pontos de tempo de inatividade</span><span class="sxs-lookup"><span data-stu-id="918f0-395">Points of downtime</span></span>
<span data-ttu-id="918f0-396">tempo de inatividade Olá consiste em toofailover toohello alternativa DC do hello tempo e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="918f0-396">hello downtime consists of hello time toofailover toohello alternative DC and back.</span></span> <span data-ttu-id="918f0-397">Também depende da sua configuração cliente/DNS e a reconexão do cliente poder ser atrasada.</span><span class="sxs-lookup"><span data-stu-id="918f0-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="918f0-398">Considere Olá seguinte exemplo de uma configuração híbrida AlwaysOn:</span><span class="sxs-lookup"><span data-stu-id="918f0-398">Consider hello following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="918f0-400">Vantagens</span><span class="sxs-lookup"><span data-stu-id="918f0-400">Advantages</span></span>
* <span data-ttu-id="918f0-401">Você pode utilizar a infraestrutura existente.</span><span class="sxs-lookup"><span data-stu-id="918f0-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="918f0-402">Você tem Olá toopre a atualização da opção Olá armazenamento do Azure em hello Azure DR DC primeiro.</span><span class="sxs-lookup"><span data-stu-id="918f0-402">You have hello option toopre-upgrade hello Azure storage on hello DR Azure DC first.</span></span>
* <span data-ttu-id="918f0-403">saudação de armazenamento do Azure DR DC pode ser reconfigurada.</span><span class="sxs-lookup"><span data-stu-id="918f0-403">hello DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="918f0-404">Há um mínimo de dois failovers durante a migração, excluindo failovers de teste.</span><span class="sxs-lookup"><span data-stu-id="918f0-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="918f0-405">Você não precisa de dados do SQL Server toomove com backup e restauração.</span><span class="sxs-lookup"><span data-stu-id="918f0-405">You do not need toomove SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="918f0-406">Desvantagens</span><span class="sxs-lookup"><span data-stu-id="918f0-406">Disadvantages</span></span>
* <span data-ttu-id="918f0-407">Dependendo tooSQL de acesso de cliente servidor, pode haver latência aumentada quando o SQL Server está em execução em um aplicativo de toohello do controlador de domínio alternativo.</span><span class="sxs-lookup"><span data-stu-id="918f0-407">Depending on client access tooSQL Server, there might be increased latency when SQL Server is running in an alternative DC toohello application.</span></span>
* <span data-ttu-id="918f0-408">tempo de cópia de saudação de VHDs tooPremium armazenamento pode ser longo.</span><span class="sxs-lookup"><span data-stu-id="918f0-408">hello copy time of VHDs tooPremium storage could be long.</span></span> <span data-ttu-id="918f0-409">Isso pode afetar sua decisão sobre se tookeep Olá Olá grupo de disponibilidade do nó.</span><span class="sxs-lookup"><span data-stu-id="918f0-409">This might affect your decision on whether tookeep hello node in hello Availability Group.</span></span> <span data-ttu-id="918f0-410">Considere o seguinte para quando o trabalho intensivas de log cargas estão em execução durante a migração de saudação é necessário, desde que o nó primário Olá terá tookeep Olá transações não replicadas no log de transações.</span><span class="sxs-lookup"><span data-stu-id="918f0-410">Consider this for when log intensive work loads are running during hello migration is required, since hello Primary node will have tookeep hello unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="918f0-411">Portanto, isso pode crescer significativamente.</span><span class="sxs-lookup"><span data-stu-id="918f0-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="918f0-412">Esse cenário usa hello Azure **AzureStorageBlobCopy início** commandlet, que é assíncrona.</span><span class="sxs-lookup"><span data-stu-id="918f0-412">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="918f0-413">Não há nenhum SLA a concluir.</span><span class="sxs-lookup"><span data-stu-id="918f0-413">There is no SLA on completion.</span></span> <span data-ttu-id="918f0-414">Olá tempo de saudação cópias varia, enquanto isso depende de espera na fila, também depende de quantidade de saudação do tootransfer de dados.</span><span class="sxs-lookup"><span data-stu-id="918f0-414">hello time of hello copies varies, while this depends on wait in queue, it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="918f0-415">Portanto você tiver apenas um nó em seu data center 2, você deve executar etapas de mitigação no caso de cópia Olá demora mais do que no teste.</span><span class="sxs-lookup"><span data-stu-id="918f0-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="918f0-416">Isso pode incluir Olá ideias a seguir.</span><span class="sxs-lookup"><span data-stu-id="918f0-416">This could include hello following ideas.</span></span>
  * <span data-ttu-id="918f0-417">Adicione um nó SQL 2º temporário para HA antes da migração de saudação com tempo de inatividade acordada.</span><span class="sxs-lookup"><span data-stu-id="918f0-417">Add a temporary 2nd SQL node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="918f0-418">Execute a migração Olá fora do Azure manutenção agendada.</span><span class="sxs-lookup"><span data-stu-id="918f0-418">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="918f0-419">Verifique se você configurou corretamente o quorum do cluster.</span><span class="sxs-lookup"><span data-stu-id="918f0-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="918f0-420">Este cenário pressupõe que você deixe de documentar a instalação e sabe como armazenamento Olá é mapeado em ordem toomake será alterado para configurações de cache ideais.</span><span class="sxs-lookup"><span data-stu-id="918f0-420">This scenario assumes that you have documented your install and know how hello storage is mapped in order toomake changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="918f0-421">Etapas de alto nível</span><span class="sxs-lookup"><span data-stu-id="918f0-421">High-level steps</span></span>
![Multisite2][10]

* <span data-ttu-id="918f0-423">Tornar Olá local / alternativa saudação do controlador de domínio do Azure SQL Server primário e torná-lo Olá outros parceiro de Failover automático (AFP).</span><span class="sxs-lookup"><span data-stu-id="918f0-423">Make hello on-premises / alternate Azure DC hello SQL Server Primary, and make it hello other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="918f0-424">Coletar informações de configuração de disco do SQL2 e remover nó de saudação (não excluir VHDs anexados).</span><span class="sxs-lookup"><span data-stu-id="918f0-424">Gather disk configuration information from SQL2, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="918f0-425">Crie uma conta de armazenamento Premium e copiar VHDs de saudação conta de armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="918f0-425">Create a Premium Storage account and copy VHDs from hello Standard Storage account.</span></span>
* <span data-ttu-id="918f0-426">Criar um novo serviço de nuvem e crie Olá VM SQL2 com seus discos de armazenamento gratificações anexados.</span><span class="sxs-lookup"><span data-stu-id="918f0-426">Create a new cloud service and create hello SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="918f0-427">Configure o ILB / ELB e adicione pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="918f0-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="918f0-428">Saudação de atualização sempre no ouvinte com o novo ILB / failover de teste e o endereço IP ELB.</span><span class="sxs-lookup"><span data-stu-id="918f0-428">Update hello Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="918f0-429">Verifique a configuração de DNS hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-429">Check hello DNS configuration.</span></span>
* <span data-ttu-id="918f0-430">Alterar Olá AFP tooSQL2 e, em seguida, migrar SQL1 e percorrer as etapas 2 a 5.</span><span class="sxs-lookup"><span data-stu-id="918f0-430">Change hello AFP tooSQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="918f0-431">Failovers de teste.</span><span class="sxs-lookup"><span data-stu-id="918f0-431">Test failovers.</span></span>
* <span data-ttu-id="918f0-432">Alternar tooSQL1 back Olá AFP e SQL2</span><span class="sxs-lookup"><span data-stu-id="918f0-432">Switch hello AFP back tooSQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a><span data-ttu-id="918f0-433">Apêndice: Migrar um armazenamento de tooPremium de multissite sempre em Cluster</span><span class="sxs-lookup"><span data-stu-id="918f0-433">Appendix: Migrating a Multisite Always On Cluster tooPremium Storage</span></span>
<span data-ttu-id="918f0-434">Olá restante este tópico fornece um exemplo detalhado de conversão de um armazenamento de multissite AlwaysOn cluster tooPremium.</span><span class="sxs-lookup"><span data-stu-id="918f0-434">hello remainder of this topic provides a detailed example of converting a multi-site Always On cluster tooPremium storage.</span></span> <span data-ttu-id="918f0-435">Ele também converte Olá ouvinte usa um balanceador de carga interno de tooan (ELB) do balanceador externo de carga (ILB).</span><span class="sxs-lookup"><span data-stu-id="918f0-435">It also converts hello Listener from using an external load balancer (ELB) tooan internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="918f0-436">Ambiente</span><span class="sxs-lookup"><span data-stu-id="918f0-436">Environment</span></span>
* <span data-ttu-id="918f0-437">Windows 2k12 / SQL 2k12</span><span class="sxs-lookup"><span data-stu-id="918f0-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="918f0-438">1 arquivo de banco de dados no SP</span><span class="sxs-lookup"><span data-stu-id="918f0-438">1 DB Files on SP</span></span>
* <span data-ttu-id="918f0-439">2 x pools de armazenamento por nó</span><span class="sxs-lookup"><span data-stu-id="918f0-439">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="918f0-441">VM:</span><span class="sxs-lookup"><span data-stu-id="918f0-441">VM:</span></span>
<span data-ttu-id="918f0-442">Neste exemplo, vamos toodemonstrate mover de um tooILB ELB.</span><span class="sxs-lookup"><span data-stu-id="918f0-442">In this example we are going toodemonstrate moving from an ELB tooILB.</span></span> <span data-ttu-id="918f0-443">ELB estava disponível antes de ILB, então isso mostra como toothis tooswitch durante Olá migração.</span><span class="sxs-lookup"><span data-stu-id="918f0-443">ELB was available before ILB, so this shows how tooswitch toothis during hello migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a><span data-ttu-id="918f0-445">As etapas anteriores: Conectar tooSubscription</span><span class="sxs-lookup"><span data-stu-id="918f0-445">Pre Steps: Connect tooSubscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="918f0-446">Etapa 1: criar a nova conta de armazenamento e o serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="918f0-446">Step 1: Create New Storage Account and Cloud Service</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a><span data-ttu-id="918f0-447">Etapa 2: Saudação de aumento permitida falhas nos recursos<Optional></span><span class="sxs-lookup"><span data-stu-id="918f0-447">Step 2: Increase hello permitted failures on resources <Optional></span></span>
<span data-ttu-id="918f0-448">Em determinados recursos que pertencem a tooyour grupo de disponibilidade AlwaysOn, há limites no quantas falhas que podem ocorrer em um período, em que o serviço de cluster Olá tentará toorestart grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-448">On certain resources that belong tooyour Always On Availability Group there are limits on how many failures that can occur in a period, where hello cluster service will attempt toorestart hello resource group.</span></span> <span data-ttu-id="918f0-449">É recomendável que aumentar esse enquanto são acompanhará neste procedimento, pois se você não manualmente failovers de failover e gatilho desligando máquinas você pode obter o limite de toothis fechar.</span><span class="sxs-lookup"><span data-stu-id="918f0-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close toothis limit.</span></span>

<span data-ttu-id="918f0-450">Ele seria ser limite de falha de Olá toodouble prudente, toodo isso no Gerenciador de Cluster de Failover, consulte Propriedades toohello Olá AlwaysOn do grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="918f0-450">It would be prudent toodouble hello failure allowance, toodo this in Failover Cluster Manager, go toohello Properties of hello Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="918f0-452">Altere Olá too6 máximo de falhas.</span><span class="sxs-lookup"><span data-stu-id="918f0-452">Change hello Maximum Failures too6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="918f0-453">Etapa 3: Adição do recurso de endereço IP ao grupo de clusters <Optional></span><span class="sxs-lookup"><span data-stu-id="918f0-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="918f0-454">Se você tiver apenas um endereço IP para Olá grupo de clusters e isso é alinhado toohello nuvem sub-rede, lembre-se, se você acidentalmente coloca offline todos os nós de cluster na nuvem de saudação que rede e recursos de Cluster IP hello e nome de rede do Cluster não será capaz de toocome on-line.</span><span class="sxs-lookup"><span data-stu-id="918f0-454">If you have only one IP address for hello Cluster Group and this is aligned toohello cloud subnet, beware, if you accidentally take offline all cluster nodes in hello cloud on that network then hello Cluster IP resource and Cluster Network Name will not be able toocome online.</span></span> <span data-ttu-id="918f0-455">Olá evento isso impedirá atualiza tooother os recursos de cluster.</span><span class="sxs-lookup"><span data-stu-id="918f0-455">In hello event of this it will prevent updates tooother cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="918f0-456">Etapa 4: Configuração de DNS</span><span class="sxs-lookup"><span data-stu-id="918f0-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="918f0-457">tooimplement uma transição suave depende de como o DNS está sendo utilizado e atualizado.</span><span class="sxs-lookup"><span data-stu-id="918f0-457">tooimplement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="918f0-458">Quando AlwaysOn é instalado, ele cria um grupo de recursos de Cluster do Windows, se você abrir o Gerenciador de Cluster de Failover, você verá que, no mínimo, ele terá três recursos, Olá dois que Olá documento se refere a tooare:</span><span class="sxs-lookup"><span data-stu-id="918f0-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, hello two that hello document refers tooare:</span></span>

* <span data-ttu-id="918f0-459">Nome de rede virtual (VNN) – Este é Olá DNS nome que o cliente se conectar toowhen desejarem tooconnect tooSQL servidores por meio do AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="918f0-459">Virtual Network Name (VNN) – This is hello DNS name that client connect toowhen wanting tooconnect tooSQL Servers via Always On.</span></span>
* <span data-ttu-id="918f0-460">Recurso de endereço IP – isso é Olá de endereços IP que associado Olá VNN, você pode ter mais de um e uma configuração multissite, você terá um endereço IP por sub-rede/site.</span><span class="sxs-lookup"><span data-stu-id="918f0-460">IP Address Resource – This is hello IP address that associated with hello VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="918f0-461">Ao conectar tooSQL Server, o driver do SQL Server Client Olá será recuperar os registros DNS Olá associados ouvinte hello e tente tooconnect tooeach AlwaysOn associado endereço IP, abaixo, discutiremos alguns fatores que podem influenciar a isso.</span><span class="sxs-lookup"><span data-stu-id="918f0-461">When connecting tooSQL Server, hello SQL Server Client driver will retrieve hello DNS records associated with hello listener and try tooconnect tooeach Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="918f0-462">Olá número de registros DNS simultâneos que estão associados com o nome do ouvinte Olá depende não apenas número de saudação de endereços IP associados, mas Olá ' RegisterAllIpProviders'setting no cluster de Failover para Olá recursos sempre ON VNN.</span><span class="sxs-lookup"><span data-stu-id="918f0-462">hello number of concurrent DNS records that are associated with hello listener name depends not only on hello number of IP addresses associated, but hello ‘RegisterAllIpProviders’setting in Failover Clustering for hello Always ON VNN resource.</span></span>

<span data-ttu-id="918f0-463">Quando você implanta sempre ativa no Azure há etapas diferentes toocreate Olá ouvinte e endereços IP, toomanually configurar Olá 'RegisterAllIpProviders' too1, isso é tooan diferentes locais sempre na implantação em que ele já está definido too1.</span><span class="sxs-lookup"><span data-stu-id="918f0-463">When you deploy Always On in Azure there are different steps toocreate hello Listener and IP Addresses, you have toomanually configure hello ‘RegisterAllIpProviders’ too1, this is different tooan on-premises Always On deployment where it is already set too1.</span></span>

<span data-ttu-id="918f0-464">Se 'RegisterAllIpProviders' for 0, em seguida, você só verá o registro DNS no DNS associado Olá ouvinte:</span><span class="sxs-lookup"><span data-stu-id="918f0-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with hello Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="918f0-466">Se 'RegisterAllIpProviders' for 1:</span><span class="sxs-lookup"><span data-stu-id="918f0-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="918f0-468">Olá código abaixo despejar Olá configurações VNN e defina-a para você,. Observe que, para hello alterar tootake efeito você precisará tootake Olá VNN off-line e ligue-o novamente online, essa colocando Olá offline interrupção causando conectividade de cliente ouvinte.</span><span class="sxs-lookup"><span data-stu-id="918f0-468">hello code below will dump out hello VNN settings and set it for you, please note, for hello change tootake effect you will need tootake hello VNN offline and turn it back online, this taking hello Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="918f0-469">Em uma etapa posterior da migração, você precisará tooupdate Olá sempre no ouvinte com um endereço IP atualizado que fazem referência a um balanceador de carga, isso envolverá uma remoção do recurso de endereço IP e a adição.</span><span class="sxs-lookup"><span data-stu-id="918f0-469">In a later migration step you will need tooupdate hello Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="918f0-470">Após a atualização IP hello, é necessário tooensure Olá novo endereço IP foi atualizado na zona DNS e que os clientes de saudação estão atualizando seu cache DNS local.</span><span class="sxs-lookup"><span data-stu-id="918f0-470">After hello IP update, you need tooensure hello new IP address has been updated in DNS Zone and that hello clients are updating their local DNS cache.</span></span>

<span data-ttu-id="918f0-471">Se os clientes residem em um segmento de rede diferente e fazer referência a um servidor DNS diferente, será necessário tooconsider o que acontece com transferência de zona DNS durante a migração de saudação hello aplicativo reconectá tempo será limitado pelo menos Olá tempo de transferência de zona de qualquer novos endereços IP de ouvinte de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-471">If your clients reside in a different network segment and reference a different DNS server, you need tooconsider what happens about DNS Zone Transfer during hello migration, as hello application reconnect time will be constrained by at least hello Zone Transfer Time of any new IP addresses for hello listener.</span></span> <span data-ttu-id="918f0-472">Se você estiver na restrição de tempo aqui, você deve discutir e testar a imposição de uma transferência de zona incremental com as equipes de Windows, e também colocar Olá DNS tooa de registro de host reduzir tempo tooLive (TTL), para atualizam clientes de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put hello DNS host record tooa lower Time tooLive (TTL), so hello clients update.</span></span> <span data-ttu-id="918f0-473">Para obter mais informações, consulte [Transferências de Zona Incrementais](https://technet.microsoft.com/library/cc958973.aspx) e [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span><span class="sxs-lookup"><span data-stu-id="918f0-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="918f0-474">Por saudação padrão TTL de registro de DNS que está associado a saudação ouvinte AlwaysOn no Azure é 1200 segundos.</span><span class="sxs-lookup"><span data-stu-id="918f0-474">By default hello TTL for DNS Record that is associated with hello Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="918f0-475">Talvez você queira tooreduce isso se você estiver na restrição de tempo durante a atualização de clientes migração tooensure Olá seus DNS com IP hello atualizado o endereço para o ouvinte de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-475">You may wish tooreduce this if you are under time constraint during your migration tooensure hello clients update their DNS with hello updated IP address for hello listener.</span></span> <span data-ttu-id="918f0-476">Você pode ver e modificar a configuração de saudação despejando configuração de saudação do hello VNN:</span><span class="sxs-lookup"><span data-stu-id="918f0-476">You can see and modify hello configuration by dumping out hello configuration of hello VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="918f0-477">Observe, Olá Olá inferior 'HostRecordTTL', ocorrerá uma quantidade maior de tráfego DNS.</span><span class="sxs-lookup"><span data-stu-id="918f0-477">Please note, hello lower hello ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="918f0-478">Configurações de aplicativo cliente</span><span class="sxs-lookup"><span data-stu-id="918f0-478">Client application settings</span></span>
<span data-ttu-id="918f0-479">Se seu aplicativo de cliente SQL oferece suporte Olá .net 4.5 SQLClient, em seguida, você pode usar ' MULTISUBNETFAILOVER = TRUE' palavra-chave, isso é recomendado toobe aplicada conforme permite tooSQL mais rápido de conexão sempre no grupo de disponibilidade durante o failover.</span><span class="sxs-lookup"><span data-stu-id="918f0-479">If your SQL client application supports hello .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended toobe applied as it allows for faster connection tooSQL Always On Availability Group during failover.</span></span> <span data-ttu-id="918f0-480">Ele enumera através de todos os endereços IP associados Olá sempre no ouvinte de em paralelo e executa uma velocidade de repetição de conexão TCP mais agressiva durante um failover.</span><span class="sxs-lookup"><span data-stu-id="918f0-480">It enumerates through all IP addresses associated with hello Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="918f0-481">Para obter mais informações sobre configurações de saudação acima, consulte [palavra-chave MultiSubnetFailover e recursos associados ao](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span><span class="sxs-lookup"><span data-stu-id="918f0-481">For more information regarding hello settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="918f0-482">Consulte também [Suporte do SqlClient para a Alta Disponibilidade e a Recuperação de Desastre](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="918f0-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="918f0-483">Etapa 5: Configurações de quórum do cluster</span><span class="sxs-lookup"><span data-stu-id="918f0-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="918f0-484">Como você vai toobe fazer pelo menos um SQL Server para baixo em um momento, você deve modificar a configuração de quorum do cluster hello, se usar testemunha de compartilhamento de arquivo (FSW) com 2 nós, você deve definir a maioria de nós Olá quorum tooallow e utilizar votação dinâmico, e isso é tooallow para constantes de tooremain um único nó.</span><span class="sxs-lookup"><span data-stu-id="918f0-484">As you are going toobe taking out at least one SQL Server down at a time, you should modify hello cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set hello quorum tooallow node majority and utilize dynamic voting, and this is tooallow for a single node tooremain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="918f0-485">Para obter mais informações sobre como gerenciar e configurar quorum do cluster hello, consulte [Olá a configurar e gerenciar o Quorum em um Cluster de Failover do Windows Server 2012](https://technet.microsoft.com/library/jj612870.aspx).</span><span class="sxs-lookup"><span data-stu-id="918f0-485">For more information on managing and configuring hello cluster quorum, please see [Configure and Manage hello Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="918f0-486">Etapa 6: extrair ACLs e pontos de extremidade existentes</span><span class="sxs-lookup"><span data-stu-id="918f0-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="918f0-487">Salve esses arquivos de texto tooa.</span><span class="sxs-lookup"><span data-stu-id="918f0-487">Save these tooa text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="918f0-488">Etapa 7: alterar parceiros de failover e modos de replicação</span><span class="sxs-lookup"><span data-stu-id="918f0-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="918f0-489">Se você tiver mais de 2 servidores do SQL, você deve alterar o failover de saudação da outra réplica secundária em outro controlador de domínio ou local 'too'Synchronous e torná-lo um parceiro de Failover automático (AFP), isso é para manter alta disponibilidade enquanto você estiver fazendo alterações.</span><span class="sxs-lookup"><span data-stu-id="918f0-489">If you have more than 2 SQL Servers, you should change hello failover of another secondary in another DC or on-premises too‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="918f0-490">Você pode fazer isso por meio do TSQL ou modificar por SSMS:</span><span class="sxs-lookup"><span data-stu-id="918f0-490">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="918f0-492">Etapa 8: Remover a VM secundária do serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="918f0-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="918f0-493">Você deve estar planejando toomigrate um nó secundário nuvem pela primeira vez, se isso for primário no momento, você deve iniciar um failover manual.</span><span class="sxs-lookup"><span data-stu-id="918f0-493">You should be planning toomigrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="918f0-494">Etapa 9: Alterar as configurações de caching de disco no arquivo CSV e salvar</span><span class="sxs-lookup"><span data-stu-id="918f0-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="918f0-495">Para volumes de dados essas devem ser definidas tooREADONLY.</span><span class="sxs-lookup"><span data-stu-id="918f0-495">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="918f0-496">Para volumes TLOG esses devem ser definidos tooNONE.</span><span class="sxs-lookup"><span data-stu-id="918f0-496">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="918f0-498">Etapa 10: copiar VHDS</span><span class="sxs-lookup"><span data-stu-id="918f0-498">Step 10: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



<span data-ttu-id="918f0-499">Você pode verificar o status da cópia Olá de saudação VHDs toohello conta de armazenamento Premium:</span><span class="sxs-lookup"><span data-stu-id="918f0-499">You can check hello copy status of hello VHDs toohello Premium Storage account:</span></span>

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

<span data-ttu-id="918f0-501">Aguarde até que todos esses itens sejam registrados como êxito.</span><span class="sxs-lookup"><span data-stu-id="918f0-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="918f0-502">Para obter informações para blobs individuais:</span><span class="sxs-lookup"><span data-stu-id="918f0-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="918f0-503">Etapa 11: Registrar o disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="918f0-503">Step 11: Register OS disk</span></span>
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="918f0-504">Etapa 12: Importar a réplica secundária para o novo serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="918f0-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="918f0-505">opção de código Olá abaixo também Olá usa adicionado aqui você pode importar máquina hello e use o VIP devem ser retidos hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-505">hello code below also uses hello added option here you can import hello machine and use hello retainable VIP.</span></span>

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="918f0-506">Etapa 13: criar ILB no novo Svc de nuvem, adicionar pontos de extremidade de carga balanceada e ACLs</span><span class="sxs-lookup"><span data-stu-id="918f0-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a><span data-ttu-id="918f0-507">Etapa 14: Atualizar AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="918f0-507">Step 14: Update Always On</span></span>
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

<span data-ttu-id="918f0-509">Agora, remova o serviço de nuvem antigo Olá endereço IP.</span><span class="sxs-lookup"><span data-stu-id="918f0-509">Now remove hello old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="918f0-511">Etapa 15: Verificar a atualização do DNS</span><span class="sxs-lookup"><span data-stu-id="918f0-511">Step 15: DNS update check</span></span>
<span data-ttu-id="918f0-512">Agora, verifique os servidores DNS em suas redes de cliente do SQL Server e certifique-se de que o cluster adicionou Olá registro de host adicionais para Olá adicionou o endereço IP.</span><span class="sxs-lookup"><span data-stu-id="918f0-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added hello extra host record for hello added IP address.</span></span> <span data-ttu-id="918f0-513">Se os servidores DNS não atualizou, considere forçar uma transferência de zona DNS e garantir que os clientes na sub-rede há hello são capazes de tooresolve tooboth sempre em endereços IP, isso é para que você não precisa toowait para a replicação automática do DNS.</span><span class="sxs-lookup"><span data-stu-id="918f0-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that hello clients in there subnet are able tooresolve tooboth Always On IP Addresses, this is so you do not need toowait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="918f0-514">Etapa 16: Reconfigurar o AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="918f0-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="918f0-515">Neste ponto você aguardar Olá secundária desse nó que foi migrado toofully ressincronizar com o nó local do hello e alternar o nó de replicação toosynchronous e torná-lo Olá AFP.</span><span class="sxs-lookup"><span data-stu-id="918f0-515">At this point you wait for hello secondary that node that was migrated toofully resynchronize with hello on-premises node and switch toosynchronous replication node and make it hello AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="918f0-516">Etapa 17: Migrar o segundo nó</span><span class="sxs-lookup"><span data-stu-id="918f0-516">Step 17: Migrate second node</span></span>
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="918f0-517">Etapa 18: Alterar as configurações de caching de disco no arquivo CSV e salvar</span><span class="sxs-lookup"><span data-stu-id="918f0-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="918f0-518">Para volumes de dados essas devem ser definidas tooREADONLY.</span><span class="sxs-lookup"><span data-stu-id="918f0-518">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="918f0-519">Para volumes TLOG esses devem ser definidos tooNONE.</span><span class="sxs-lookup"><span data-stu-id="918f0-519">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="918f0-521">Etapa 19: criar a nova conta de armazenamento independente para o nó secundário</span><span class="sxs-lookup"><span data-stu-id="918f0-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="918f0-522">Etapa 20: copiar VHDs</span><span class="sxs-lookup"><span data-stu-id="918f0-522">Step 20: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


<span data-ttu-id="918f0-523">Você pode verificar o status da cópia do VHD Olá para todos os VHDs: ForEach ($disk em $diskobjects) {$lun = $disk. LUN $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. Etiqueta de disco $diskName = $disk. DiskName</span><span class="sxs-lookup"><span data-stu-id="918f0-523">You can check hello VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="918f0-525">Aguarde até que todos esses itens sejam registrados como êxito.</span><span class="sxs-lookup"><span data-stu-id="918f0-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="918f0-526">Para obter informações para blobs individuais:</span><span class="sxs-lookup"><span data-stu-id="918f0-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="918f0-527">Etapa 21: Registrar o disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="918f0-527">Step 21: Register OS disk</span></span>
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="918f0-528">Etapa 22: adicionar pontos de extremidade de carga balanceada e ACLs</span><span class="sxs-lookup"><span data-stu-id="918f0-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="918f0-529">Etapa 23: Failover de teste</span><span class="sxs-lookup"><span data-stu-id="918f0-529">Step 23: Test failover</span></span>
<span data-ttu-id="918f0-530">Você agora deve permitir que nós migrados Olá sincronizar com o nó local do AlwaysOn hello, colocá-lo no modo de replicação toosynchronous e aguarde até que ele seja sincronizado.</span><span class="sxs-lookup"><span data-stu-id="918f0-530">You should now let hello migrated node synchronize with hello on-premises Always On node, place it in toosynchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="918f0-531">Em seguida, o failover de local toohello primeiro nó migrado, que é Olá AFP.</span><span class="sxs-lookup"><span data-stu-id="918f0-531">Then failover from on-prem toohello first node migrated, which is hello AFP.</span></span> <span data-ttu-id="918f0-532">Depois que funcionou, alteração Olá migrados pela última vez nó toohello AFP.</span><span class="sxs-lookup"><span data-stu-id="918f0-532">Once that has worked, change hello last migrated node toohello AFP.</span></span>

<span data-ttu-id="918f0-533">Você deve testar failovers entre todos os nós e executar Embora testes caos tooensure failovers funcionam como esperado e em um tempo manor.</span><span class="sxs-lookup"><span data-stu-id="918f0-533">You should test failovers between all nodes and run though chaos tests tooensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="918f0-534">Etapa 24: colocar de volta configurações de quorum de cluster / TTL DNS / Failover de impressoras / Configurações de sincronização</span><span class="sxs-lookup"><span data-stu-id="918f0-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="918f0-535">Adicionando recurso de endereço IP na mesma sub-rede</span><span class="sxs-lookup"><span data-stu-id="918f0-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="918f0-536">Se você tiver apenas 2 servidores SQL e quiser toomigrate-los tooa novo serviço de nuvem, mas deseja tookeep-los em Olá mesma sub-rede, você pode evitar deixar ouvinte Olá original de saudação toodelete off-line sempre no endereço IP e adicionar Olá novo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="918f0-536">If you have only 2 SQL Servers and want toomigrate them tooa new cloud service, but want tookeep them on hello same subnet, you can avoid taking hello listener offline toodelete hello original Always On IP Address and add hello New IP Address.</span></span> <span data-ttu-id="918f0-537">Se você estiver migrando Olá VMs tooanother subrede não será necessário toodo isso, haverá uma rede de cluster adicionais que fazem referência a essa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="918f0-537">If you are migrating hello VMs tooanother subnet you will not need toodo this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="918f0-538">Depois de abrir hello migrados secundário e adicionado ao novo recurso de endereço IP Olá Olá novo serviço de nuvem antes de failover Olá primário existente, você deve executar essas etapas em Olá Gerenciador de Cluster de Failover:</span><span class="sxs-lookup"><span data-stu-id="918f0-538">Once you have brought up hello migrated secondary and added in hello new IP Address resource for hello new cloud service before failover hello existing Primary, you should take these steps within hello Cluster Failover Manager:</span></span>

<span data-ttu-id="918f0-539">tooadd no endereço IP, consulte Olá [apêndice](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), etapa 14.</span><span class="sxs-lookup"><span data-stu-id="918f0-539">tooadd in IP Address, see hello [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="918f0-540">Para o recurso de endereço IP atual hello, alterar Olá possível proprietário too'Existing SQL Server primário ', no exemplo hello abaixo 'dansqlams4':</span><span class="sxs-lookup"><span data-stu-id="918f0-540">For hello current IP Address resource, change hello possible owner too‘Existing Primary SQL Server’, in hello example below, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="918f0-542">Para o novo recurso de endereço IP hello alterar Olá possível proprietário too'Migrated secundário do SQL Server', no exemplo hello abaixo 'dansqlams5':</span><span class="sxs-lookup"><span data-stu-id="918f0-542">For hello new IP Address resource, change hello possible owner too‘Migrated secondary SQL Server’, in hello example below, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="918f0-544">Depois que isso for definido, você poderá realizar failover, e quando é migrado do último nó Olá Olá possíveis proprietários devem ser editados para que esse nó é adicionado como um possível proprietário:</span><span class="sxs-lookup"><span data-stu-id="918f0-544">Once this is set you can failover, and when hello last node is migrated hello Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="918f0-546">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="918f0-546">Additional resources</span></span>
* [<span data-ttu-id="918f0-547">Armazenamento Premium do Azure</span><span class="sxs-lookup"><span data-stu-id="918f0-547">Azure Premium Storage</span></span>](../../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="918f0-548">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="918f0-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="918f0-549">SQL Server nas Máquinas Virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="918f0-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
