---
title: Usar o Armazenamento Premium do Azure com o SQL Server | Microsoft Docs
description: "Este artigo usa recursos criados com o modelo clássico de implantação e fornece orientação sobre como usar o Armazenamento Premium do Azure com o SQL Server em execução em máquinas virtuais do Azure."
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
ms.openlocfilehash: 6790db207fc7ec8a4b1546ef07c97ef30abe9513
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="e40b8-103">Usar o Armazenamento Premium do Azure com o SQL Server em máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="e40b8-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="e40b8-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e40b8-104">Overview</span></span>
<span data-ttu-id="e40b8-105">[Armazenamento Premium do Azure](../../../storage/common/storage-premium-storage.md) é o armazenamento de última geração que oferece baixa latência e E/S de taxa de transferência alta.</span><span class="sxs-lookup"><span data-stu-id="e40b8-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) is the next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="e40b8-106">Ele funciona melhor para cargas de trabalho de uso intensivo de E/S de chave, como [Máquinas Virtuais](https://azure.microsoft.com/services/virtual-machines/)do SQL Server no IaaS.</span><span class="sxs-lookup"><span data-stu-id="e40b8-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e40b8-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e40b8-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e40b8-108">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="e40b8-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="e40b8-109">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="e40b8-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="e40b8-110">Este artigo fornece informações de planejamento e diretrizes para migração de uma Máquina Virtual executando o SQL Server para usar o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server to use Premium Storage.</span></span> <span data-ttu-id="e40b8-111">Isso inclui a infraestrutura do Azure (rede, armazenamento) e as etapas de VM do Windows de convidado.</span><span class="sxs-lookup"><span data-stu-id="e40b8-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="e40b8-112">O exemplo no [Apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) mostra uma migração de ponta a ponta abrangente e completa para mover VMs maiores e aproveitar o armazenamento SSD local aprimorado com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e40b8-112">The example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end to end migration of how to move larger VMs to take advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="e40b8-113">É importante compreender o processo de ponta a ponta utilizando o Armazenamento Premium do Azure com o SQL Server em VMs IAAS.</span><span class="sxs-lookup"><span data-stu-id="e40b8-113">It is important to understand the end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="e40b8-114">Isso inclui:</span><span class="sxs-lookup"><span data-stu-id="e40b8-114">This includes:</span></span>

* <span data-ttu-id="e40b8-115">Identificação dos pré-requisitos para usar o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-115">Identification of the prerequisites to use Premium Storage.</span></span>
* <span data-ttu-id="e40b8-116">Exemplos de implantação do SQL Server no IaaS no Armazenamento Premium para novas implantações.</span><span class="sxs-lookup"><span data-stu-id="e40b8-116">Examples of deploying SQL Server on IaaS to Premium Storage for new deployments.</span></span>
* <span data-ttu-id="e40b8-117">Exemplos de migração de implantações existentes, de servidores autônomos e implantações usando grupos de disponibilidade SQL AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="e40b8-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="e40b8-118">Abordagens de migração possíveis.</span><span class="sxs-lookup"><span data-stu-id="e40b8-118">Possible migration approaches.</span></span>
* <span data-ttu-id="e40b8-119">Exemplo de ponta a ponta completo mostrando as etapas do Azure, do Windows e do SQL Server para a migração de uma implementação AlwaysOn existente.</span><span class="sxs-lookup"><span data-stu-id="e40b8-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for the migration of an existing Always On implementation.</span></span>

<span data-ttu-id="e40b8-120">Para obter informações gerais sobre o SQL Server nas Máquinas Virtuais do Azure, consulte [SQL Server nas Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e40b8-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="e40b8-121">**Autor:** Daniel Sol **Revisores Técnicos:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span><span class="sxs-lookup"><span data-stu-id="e40b8-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="e40b8-122">Pré-requisitos para o Armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="e40b8-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="e40b8-123">Existem vários pré-requisitos para o uso do Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="e40b8-124">Tamanho do computador</span><span class="sxs-lookup"><span data-stu-id="e40b8-124">Machine size</span></span>
<span data-ttu-id="e40b8-125">Para usar o Armazenamento Premium, você precisará usar máquinas virtuais (VM) da série DS.</span><span class="sxs-lookup"><span data-stu-id="e40b8-125">For using Premium Storage you will need to use DS series Virtual Machines (VM).</span></span> <span data-ttu-id="e40b8-126">Se você não usou máquinas da série DS no seu serviço de nuvem antes, exclua a VM existente, mantenha os discos anexados e, em seguida, crie um novo serviço de nuvem antes de recriar a VM conforme o tamanho da função DS *.</span><span class="sxs-lookup"><span data-stu-id="e40b8-126">If you have not used DS Series machines in your cloud service before, you must delete the existing VM, keep the attached disks, and then create a new cloud service before recreating the VM as DS* role size.</span></span> <span data-ttu-id="e40b8-127">Para saber mais sobre os tamanhos das Máquinas Virtuais, consulte [Tamanhos da Máquina Virtual e do Serviço de Nuvem do Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e40b8-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="e40b8-128">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="e40b8-128">Cloud services</span></span>
<span data-ttu-id="e40b8-129">Você só poderá usar VMs DS* com Armazenamento Premium quando elas forem criadas em um novo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e40b8-129">You can only use DS* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="e40b8-130">Se você estiver usando o SQL Server AlwaysOn no Azure, o Ouvinte AlwaysOn fará referência ao endereço IP do Balanceador de Externo ou Interno de Carga do Azure que estiver associado a um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e40b8-130">If you are using SQL Server Always On in Azure, the Always On Listener will refer to the Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="e40b8-131">O foco deste artigo é explicar como migrar ao mesmo tempo em que a disponibilidade é mantida nesse cenário.</span><span class="sxs-lookup"><span data-stu-id="e40b8-131">This article focuses on how to migrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="e40b8-132">Uma série DS* deve ser a primeira VM implantada no novo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e40b8-132">A DS* Series must be the first VM that is deployed to the new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="e40b8-133">VNETS regionais</span><span class="sxs-lookup"><span data-stu-id="e40b8-133">Regional VNETS</span></span>
<span data-ttu-id="e40b8-134">Para VMs DS*, você deve configurar a VNET (Rede Virtual) que hospeda suas VMs como regional.</span><span class="sxs-lookup"><span data-stu-id="e40b8-134">For DS* VMs you must configure the Virtual Network (VNET) hosting your VMs to be regional.</span></span> <span data-ttu-id="e40b8-135">Essa "ampliação" da VNET tem a finalidade de permitir que VMs maiores sejam provisionadas em outros clusters e permitir a comunicação entre elas.</span><span class="sxs-lookup"><span data-stu-id="e40b8-135">This “widens” the VNET is to allow the larger VMs to be provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="e40b8-136">Na captura de tela a seguir, o local realçado mostra VNETs regionais, enquanto o primeiro resultado mostra uma VNET "estreita".</span><span class="sxs-lookup"><span data-stu-id="e40b8-136">In the following screenshot, the highlighted Location shows regional VNETs, whereas the first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="e40b8-138">Você pode gerar um tíquete de suporte da Microsoft para migrar para uma VNET regional, a Microsoft fará uma alteração e, em seguida, para concluir a migração para VNETs regionais, altere a propriedade AffinityGroup na configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="e40b8-138">You can raise a Microsoft support ticket to migrate to a regional VNET, Microsoft will make a change, then to complete the migration to regional VNETs, change the property AffinityGroup in the network configuration.</span></span> <span data-ttu-id="e40b8-139">Primeiro, exporte a Configuração da Rede no PowerShell, em seguida, substitua a propriedade **AffinityGroup** no elemento **VirtualNetworkSite** por uma propriedade **Location**.</span><span class="sxs-lookup"><span data-stu-id="e40b8-139">First export the Network Configuration in PowerShell, and then replace the **AffinityGroup** property in the **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="e40b8-140">Especifique `Location = XXXX` onde `XXXX` é uma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="e40b8-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="e40b8-141">Em seguida, importe a nova configuração.</span><span class="sxs-lookup"><span data-stu-id="e40b8-141">Then import the new configuration.</span></span>

<span data-ttu-id="e40b8-142">Por exemplo, considerando a seguinte configuração de VNET:</span><span class="sxs-lookup"><span data-stu-id="e40b8-142">For example, considering the following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="e40b8-143">Para movê-la para uma VNET regional na Europa Ocidental, altere a configuração para o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e40b8-143">To move this to a regional VNET in West Europe, change the configuration to the following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="e40b8-144">Contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e40b8-144">Storage accounts</span></span>
<span data-ttu-id="e40b8-145">Você precisará criar uma nova conta de armazenamento que seja configurada para Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-145">You will need to create a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="e40b8-146">Observe que o uso do Armazenamento Premium é definido na conta de armazenamento, não em VHDs individuais, no entanto, ao usar uma VM série DS*, você pode anexar VHDs de contas de Armazenamento Padrão e Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-146">Note that the use of Premium Storage is set at the storage account, not on individual VHDs, however when using a DS* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="e40b8-147">Você poderá considerar isso se não quiser colocar o VHD do sistema operacional na conta de Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-147">You may consider this if you do not want to place the OS VHD on to the Premium Storage account.</span></span>

<span data-ttu-id="e40b8-148">O seguinte comando **New-AzureStorageAccountPowerShell** com o Tipo **"Premium_LRS"** cria uma Conta de Armazenamento Premium:</span><span class="sxs-lookup"><span data-stu-id="e40b8-148">The following **New-AzureStorageAccountPowerShell** command with the "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="e40b8-149">Configurações de Cache de VHDs</span><span class="sxs-lookup"><span data-stu-id="e40b8-149">VHDs Cache Settings</span></span>
<span data-ttu-id="e40b8-150">A principal diferença entre a criação de discos que fazem parte de uma conta de Armazenamento Premium é a configuração de cache de disco.</span><span class="sxs-lookup"><span data-stu-id="e40b8-150">The main difference between creating disks that are part of a Premium Storage account is the disk cache setting.</span></span> <span data-ttu-id="e40b8-151">Para discos do volume SQL Server Data, recomendamos que você use ‘**Caching de Leitura**’.</span><span class="sxs-lookup"><span data-stu-id="e40b8-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="e40b8-152">Para volumes de log de transações, a configuração de cache de disco deve ser definida como ‘**Nenhum**’.</span><span class="sxs-lookup"><span data-stu-id="e40b8-152">For Transaction log volumes, the disk cache setting should be set to ‘**None**’.</span></span> <span data-ttu-id="e40b8-153">Isso é diferente das recomendações para contas de Armazenamento Padrão.</span><span class="sxs-lookup"><span data-stu-id="e40b8-153">This is different from the recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="e40b8-154">Depois que os VHDs forem anexados, a configuração de cache não poderá ser alterada.</span><span class="sxs-lookup"><span data-stu-id="e40b8-154">Once the VHDs have been attached, the cache setting cannot be altered.</span></span> <span data-ttu-id="e40b8-155">Você precisaria desanexar e anexar novamente o VHD com uma configuração de cache atualizada.</span><span class="sxs-lookup"><span data-stu-id="e40b8-155">You would need to detach and reattach the VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="e40b8-156">Espaços de armazenamento do Windows</span><span class="sxs-lookup"><span data-stu-id="e40b8-156">Windows storage spaces</span></span>
<span data-ttu-id="e40b8-157">Você pode usar os [Espaços de Armazenamento do Windows](https://technet.microsoft.com/library/hh831739.aspx) como fez com o Armazenamento Padrão anterior; isso permitirá que você migre uma VM que já utiliza os Espaços de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e40b8-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you to migrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="e40b8-158">O exemplo no [Apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (etapa 9 em diante) demonstra o código do Powershell para extrair e importar uma VM com vários VHDs anexados.</span><span class="sxs-lookup"><span data-stu-id="e40b8-158">The example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates the Powershell code to extract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="e40b8-159">Pools de Armazenamento foram usados com a conta de armazenamento do Azure Padrão para melhorar a taxa de transferência e reduzir a latência.</span><span class="sxs-lookup"><span data-stu-id="e40b8-159">Storage Pools were used with Standard Azure storage account to enhance throughput and reduce latency.</span></span> <span data-ttu-id="e40b8-160">Talvez você ache interessante testar Pools de Armazenamento com o Armazenamento Premium para novas implantações, mas isso agrega uma complexidade adicional com a configuração do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e40b8-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-to-find-which-azure-virtual-disks-map-to-storage-pools"></a><span data-ttu-id="e40b8-161">Como descobrir quais discos virtuais do Azure são mapeados para os pools de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e40b8-161">How to find which Azure Virtual Disks map to storage pools</span></span>
<span data-ttu-id="e40b8-162">Como há recomendações de configuração de cache diferentes para VHDs anexados, você pode optar por copiar os VHDs em uma conta de Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-162">As there are different cache setting recommendations for attached VHDs, you might decide to copy the VHDs to a Premium Storage account.</span></span> <span data-ttu-id="e40b8-163">No entanto, quando você anexá-los outra vez à nova VM da série DS, talvez seja necessário alterar as configurações de cache.</span><span class="sxs-lookup"><span data-stu-id="e40b8-163">However, when you reattach them to the new DS series VM, you might need to alter the cache settings.</span></span> <span data-ttu-id="e40b8-164">É mais simples aplicar as configurações de cache recomendadas do Armazenamento Premium quando há VHDs separados para arquivos do SQL Data e arquivos de log (em vez de um único VHD que contém ambos).</span><span class="sxs-lookup"><span data-stu-id="e40b8-164">It is simpler to apply the Premium Storage recommended cache settings when you have separate VHDs for the SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="e40b8-165">Se você tiver arquivos de log e de dados do SQL Server no mesmo volume, a opção de cache que escolher dependerá dos padrões de acesso de E/S para as cargas de trabalho de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e40b8-165">If you have SQL Server data and log files on the same volume, the caching option you choose depends on the IO access patterns for your database workloads.</span></span> <span data-ttu-id="e40b8-166">Apenas o teste pode demonstrar qual opção de cache é ideal para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="e40b8-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="e40b8-167">No entanto, se estiver usando Espaços de Armazenamento do Windows compostos de vários VHDs, você precisará examinar seus scripts originais para identificar quais VHDs anexados estão em qual pool específico, assim poderá definir as configurações de cache de acordo com cada disco.</span><span class="sxs-lookup"><span data-stu-id="e40b8-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need to look at your original scripts to identify which attached VHDs are in what specific pool, so you can then set the cache settings accordingly for each disk.</span></span>

<span data-ttu-id="e40b8-168">Se você não tiver o script original disponível para mostrar quais VHDs são mapeados para o pool de armazenamento, sia as próximas etapas para determinar o mapeamento de pool de disco/armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e40b8-168">If you do not have original script available to show you which VHDs map to the storage pool, you can use the following steps to determine the disk/storage pool mapping.</span></span>

<span data-ttu-id="e40b8-169">Para cada disco, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="e40b8-169">For each disk, use the following steps:</span></span>

1. <span data-ttu-id="e40b8-170">Obtenha a lista de discos anexados à VM com o comando **Get-AzureVM** :</span><span class="sxs-lookup"><span data-stu-id="e40b8-170">Get list of disks attached to VM with the **Get-AzureVM** command:</span></span>

    <span data-ttu-id="e40b8-171">Get-AzureVM -ServiceName <servicename> -Nome <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="e40b8-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="e40b8-172">Anote o Diskname e o LUN.</span><span class="sxs-lookup"><span data-stu-id="e40b8-172">Note the Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="e40b8-174">Área de trabalho remota na VM.</span><span class="sxs-lookup"><span data-stu-id="e40b8-174">Remote desktop into the VM.</span></span> <span data-ttu-id="e40b8-175">Em seguida, vá para **Gerenciamento do Computador** | **Gerenciador de Dispositivos** | **Unidades de Disco**.</span><span class="sxs-lookup"><span data-stu-id="e40b8-175">Then go to **Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="e40b8-176">Examine as propriedades de cada um dos 'Discos Virtuais da Microsoft'</span><span class="sxs-lookup"><span data-stu-id="e40b8-176">Look at the properties of each of the ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="e40b8-178">O número de LUNs aqui é uma referência para o número de LUNs que você especificar ao anexar o VHD à VM.</span><span class="sxs-lookup"><span data-stu-id="e40b8-178">The LUN number here is a reference to the LUN number you specify when attaching the VHD to the VM.</span></span>
5. <span data-ttu-id="e40b8-179">Para o 'Disco Virtual Microsoft', vá para a guia **Detalhes**, em seguida, na lista **Propriedade**, vá para **Chave do Driver**.</span><span class="sxs-lookup"><span data-stu-id="e40b8-179">For the ‘Microsoft Virtual Disk’ go to the **Details** tab, then in the **Property** list, go to **Driver Key**.</span></span> <span data-ttu-id="e40b8-180">Em **Valor**, observe o **Deslocamento**, que é 0002 na captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="e40b8-180">In the **Value**, note the **Offset**, which is 0002 in the following screenshot.</span></span> <span data-ttu-id="e40b8-181">O 0002 indica o PhysicalDisk2 que o pool de armazenamento referencia.</span><span class="sxs-lookup"><span data-stu-id="e40b8-181">The 0002 denotes the PhysicalDisk2 that the storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="e40b8-183">Para cada pool de armazenamento, despeje os discos associados:</span><span class="sxs-lookup"><span data-stu-id="e40b8-183">For each storage pool, dump out the associated disks:</span></span>

    <span data-ttu-id="e40b8-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="e40b8-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="e40b8-186">Agora você pode usar essas informações para associar VHDs anexados a discos físicos em pools de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e40b8-186">Now you can use this information to associate attached VHDs to Physical Disks in Storage Pools.</span></span>

<span data-ttu-id="e40b8-187">Após o mapeamento de VHDs para discos físicos nos pools de armazenamento, você poderá desanexá-los e copiá-los em uma conta de Armazenamento Premium e depois anexá-los com a configuração de cache correta.</span><span class="sxs-lookup"><span data-stu-id="e40b8-187">Once you have mapped VHDs to Physical Disks in Storage Pools you can then detach and copy them over to a Premium Storage account, then attach them with the correct cache setting.</span></span> <span data-ttu-id="e40b8-188">Veja o exemplo no [Apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), etapas 8 a 12.</span><span class="sxs-lookup"><span data-stu-id="e40b8-188">Please see the example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="e40b8-189">Essas etapas mostram como extrair uma configuração de disco VHD anexado à VM para um arquivo CSV, copiar os VHDs, alterar as configurações de cache de configuração do disco e finalmente reimplantar a VM como uma VM da série DS com todos os discos anexados.</span><span class="sxs-lookup"><span data-stu-id="e40b8-189">These steps show how to extract a VM-attached VHD disk configuration to a CSV file, copy the VHDs, alter the disk configuration cache settings, and finally redeploy the VM as a DS series VM with all the attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="e40b8-190">Largura de banda de armazenamento de VM e taxa de transferência de armazenamento de VHD</span><span class="sxs-lookup"><span data-stu-id="e40b8-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="e40b8-191">O desempenho de armazenamento depende do tamanho da VM DS* especificado e dos tamanhos de VHD.</span><span class="sxs-lookup"><span data-stu-id="e40b8-191">The amount of storage performance depends on the DS* VM size specified and the VHD sizes.</span></span> <span data-ttu-id="e40b8-192">As VMs têm concessões diferentes para o número de VHDs que podem ser anexados e a largura de banda máxima que aceitarão (MB/s).</span><span class="sxs-lookup"><span data-stu-id="e40b8-192">The VMs have different allowances for the number of VHDs that can be attached and the maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="e40b8-193">Para obter os números específicos da largura de banda, consulte [Tamanhos da Máquina Virtual e do Serviço de Nuvem do Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e40b8-193">For the specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="e40b8-194">Mais IOPS são obtidos com tamanhos de disco maiores.</span><span class="sxs-lookup"><span data-stu-id="e40b8-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="e40b8-195">Considere isso quando você pensar em seu caminho de migração.</span><span class="sxs-lookup"><span data-stu-id="e40b8-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="e40b8-196">Para obter detalhes, [consulte a tabela de IOPS e Tipos de Disco](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="e40b8-196">For details, [see the table for IOPS and Disk Types](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="e40b8-197">Por fim, considere que as VMs têm larguras de banda máxima de disco diferentes que aceitarão para todos os discos anexados.</span><span class="sxs-lookup"><span data-stu-id="e40b8-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="e40b8-198">Em cargas elevadas, você poderia saturar a largura de banda máxima de disco disponível para esse tamanho de função de VM.</span><span class="sxs-lookup"><span data-stu-id="e40b8-198">Under high load, you could saturate the maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="e40b8-199">Por exemplo, um Standard_DS14 oferecerá suporte a até 512 MB/s; portanto, com três discos P30 você poderia saturar a largura de banda do disco da VM.</span><span class="sxs-lookup"><span data-stu-id="e40b8-199">For example a Standard_DS14 will support up to 512MB/s; therefore, with three P30 disks you could saturate the disk bandwidth of the VM.</span></span> <span data-ttu-id="e40b8-200">Porém, neste exemplo, o limite de taxa de transferência poderia ser excedido dependendo da combinação de E/Ss de leitura e gravação.</span><span class="sxs-lookup"><span data-stu-id="e40b8-200">But in this example, the throughput limit could be exceeded depending on the mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="e40b8-201">Novas implantações</span><span class="sxs-lookup"><span data-stu-id="e40b8-201">New deployments</span></span>
<span data-ttu-id="e40b8-202">As próximas duas seções demonstram como você pode implantar VMs do SQL Server no Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-202">The next two sections demonstrate how you can deploy SQL Server VMs to Premium Storage.</span></span> <span data-ttu-id="e40b8-203">Como mencionado antes, você não precisa necessariamente colocar o disco do sistema operacional no Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-203">As mentioned before, you do not necessarily need to place the OS disk onto Premium storage.</span></span> <span data-ttu-id="e40b8-204">Você pode optar por fazer isso caso tenha a intenção de colocar cargas de trabalho intensivas de E/S no VHD do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="e40b8-204">You might choose to do this if you are intending to place any intensive IO workloads on the OS VHD.</span></span>

<span data-ttu-id="e40b8-205">O primeiro exemplo demonstra o uso de imagens da Galeria do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="e40b8-205">The first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="e40b8-206">O segundo exemplo mostra como usar uma imagem de VM personalizada em uma conta de armazenamento Padrão existente.</span><span class="sxs-lookup"><span data-stu-id="e40b8-206">The second example shows how to use a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="e40b8-207">Esses exemplos pressupõem que você já tenha criou um VNET regional.</span><span class="sxs-lookup"><span data-stu-id="e40b8-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="e40b8-208">Criar uma nova VM com Armazenamento Premium com Imagem da Galeria</span><span class="sxs-lookup"><span data-stu-id="e40b8-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="e40b8-209">O exemplo a seguir mostra como colocar o VHD do sistema operacional no armazenamento premium e anexar VHDs de Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-209">The example below shows how to place the OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="e40b8-210">No entanto, você também pode colocar o disco do sistema operacional em uma conta de Armazenamento Padrão e, em seguida, anexar VHDs que residem em uma conta de Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-210">However, you can also place the OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="e40b8-211">Ambos os cenários são demonstrados.</span><span class="sxs-lookup"><span data-stu-id="e40b8-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="e40b8-212">Etapa 1: criar uma conta de Armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="e40b8-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="e40b8-213">Etapa 2: criar um novo serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="e40b8-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="e40b8-214">Etapa 3: reservar um VIP de serviço de nuvem (opcional)</span><span class="sxs-lookup"><span data-stu-id="e40b8-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="e40b8-215">Etapa 4: criar um contêiner de VM</span><span class="sxs-lookup"><span data-stu-id="e40b8-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="e40b8-216">Etapa 5: colocar o VHD do sistema operacional no armazenamento Padrão ou Premium</span><span class="sxs-lookup"><span data-stu-id="e40b8-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used to place the OS VHD in

    #If you want to place the OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted to place the OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="e40b8-217">Etapa 6: criar uma VM</span><span class="sxs-lookup"><span data-stu-id="e40b8-217">Step 6: Create VM</span></span>
    #Get list of available SQL Server Images from the Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember to change to DS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks to VM Config
    #Note the size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising the Premium Storage enabled Storage account

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


### <a name="create-a-new-vm-to-use-premium-storage-with-a-custom-image"></a><span data-ttu-id="e40b8-218">Criar uma nova VM para usar o Armazenamento Premium com uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="e40b8-218">Create a new VM to use Premium Storage with a custom image</span></span>
<span data-ttu-id="e40b8-219">Este cenário demonstra onde você tem imagens personalizadas existentes que residem em uma conta de Armazenamento Padrão.</span><span class="sxs-lookup"><span data-stu-id="e40b8-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="e40b8-220">Como mencionado, se quiser colocar o VHD do sistema operacional no Armazenamento Premium, você precisará copiar a imagem que existe na conta de Armazenamento Padrão e transferi-la para um Armazenamento Premium antes que possa ser usada.</span><span class="sxs-lookup"><span data-stu-id="e40b8-220">As mentioned if you want to place the OS VHD on Premium Storage you will need to copy the image that exists in the Standard Storage account and transfer them to a Premium Storage before it can be used.</span></span> <span data-ttu-id="e40b8-221">Se você tiver uma imagem local, também poderá usar esse método para copiá-la diretamente para a conta de Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-221">If you have an image on-premises, you can also use this method to copy that directly to the Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="e40b8-222">Etapa 1: criar conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e40b8-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="e40b8-223">Etapa 2: criar serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="e40b8-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="e40b8-224">Etapa 3: Usar a imagem existente</span><span class="sxs-lookup"><span data-stu-id="e40b8-224">Step 3: Use existing image</span></span>
<span data-ttu-id="e40b8-225">Você pode usar uma imagem existente.</span><span class="sxs-lookup"><span data-stu-id="e40b8-225">You can use an existing image.</span></span> <span data-ttu-id="e40b8-226">Ou você também pode [capturar uma imagem de uma máquina existente](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e40b8-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="e40b8-227">Observe que o computador cuja imagem é criada não precisa ser um computador DS\*.</span><span class="sxs-lookup"><span data-stu-id="e40b8-227">Note the machine you image does not have to be DS* machine.</span></span> <span data-ttu-id="e40b8-228">Assim que tiver a imagem, as próximas etapas mostrarão como copiá-la para a conta de Armazenamento Premium com o commandlet **Start-AzureStorageBlobCopy** do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e40b8-228">Once you have the image, the following steps show how to copy it to the Premium Storage account with the **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for the storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="e40b8-229">Etapa 4: copiar o Blob entre contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e40b8-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="e40b8-230">Etapa 5: verificar regularmente o status da cópia:</span><span class="sxs-lookup"><span data-stu-id="e40b8-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-to-azure-disk-repository-in-subscription"></a><span data-ttu-id="e40b8-231">Etapa 6: adicionar o disco de imagem ao repositório de disco do Azure na assinatura</span><span class="sxs-lookup"><span data-stu-id="e40b8-231">Step 6: Add Image disk to Azure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="e40b8-232">Pode ser que mesmo com os relatórios de status mostrando sucesso, você ainda receba um erro de concessão de disco.</span><span class="sxs-lookup"><span data-stu-id="e40b8-232">You may find that even though the status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="e40b8-233">Nesse caso, espere cerca de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="e40b8-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-the-vm"></a><span data-ttu-id="e40b8-234">Etapa 7: criar a VM</span><span class="sxs-lookup"><span data-stu-id="e40b8-234">Step 7:  Build the VM</span></span>
<span data-ttu-id="e40b8-235">Aqui, você está criando a VM com base na sua imagem e anexando dois VHDs de Armazenamento Premium:</span><span class="sxs-lookup"><span data-stu-id="e40b8-235">Here you are building the VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need to be a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use to DS Series VM
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

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="e40b8-236">Implantações existentes que não usam grupos de disponibilidade AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="e40b8-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="e40b8-237">Para implantações existentes, primeiro consulte a seção [Pré-requisitos](#prerequisites-for-premium-storage) deste tópico.</span><span class="sxs-lookup"><span data-stu-id="e40b8-237">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="e40b8-238">Há considerações diferentes para implantações do SQL Server que não usam grupos de disponibilidade AlwaysOn e aquelas que usam.</span><span class="sxs-lookup"><span data-stu-id="e40b8-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="e40b8-239">Se não estiver usando AlwaysOn e tiver um SQL Server autônomo existente, você poderá atualizar para o Armazenamento Premium usando um novo serviço de nuvem e conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e40b8-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade to Premium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="e40b8-240">Considere as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="e40b8-240">Consider the following options:</span></span>

* <span data-ttu-id="e40b8-241">**Criar uma nova VM do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e40b8-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="e40b8-242">Você pode criar uma nova VM do SQL Server que usa uma conta de Armazenamento Premium, conforme documentado em Novas implantações.</span><span class="sxs-lookup"><span data-stu-id="e40b8-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="e40b8-243">Em seguida, faça uma operação de backup e restauração de seus bancos de dados de configuração e usuário do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e40b8-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="e40b8-244">Será necessário atualizar o aplicativo para referenciar o novo SQL Server se ele estiver sendo acessada interna ou externamente.</span><span class="sxs-lookup"><span data-stu-id="e40b8-244">The application will need to be updated to reference the new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="e40b8-245">Você precisa copiar todos os objetos 'fora do banco de dados' como se estivesse fazendo uma migração SxS (Lado a Lado) do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e40b8-245">You would need to copy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="e40b8-246">Isso inclui objetos como logons, certificados e servidores vinculados.</span><span class="sxs-lookup"><span data-stu-id="e40b8-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="e40b8-247">**Migrar uma VM existente do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e40b8-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="e40b8-248">Isso exigirá colocar a VM do SQL Server offline, depois transferi-la para um novo serviço de nuvem, o que inclui copiar todos os seus VHDs anexados para a conta de Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-248">This will require taking the SQL Server VM offline, then transferring it to a new cloud service, which includes copying all of its attached VHDs to the Premium Storage account.</span></span> <span data-ttu-id="e40b8-249">Quando a VM for colocada online, o aplicativo fará referência ao nome de host do servidor como antes.</span><span class="sxs-lookup"><span data-stu-id="e40b8-249">When the VM comes online, the application will reference the server host name as before.</span></span> <span data-ttu-id="e40b8-250">Lembre-se de que o tamanho do disco existente afetará as características de desempenho.</span><span class="sxs-lookup"><span data-stu-id="e40b8-250">Be aware that the size of the existing disk will affect the performance characteristics.</span></span> <span data-ttu-id="e40b8-251">Por exemplo, um disco de 400 GB é arredondado para um P20.</span><span class="sxs-lookup"><span data-stu-id="e40b8-251">For example, a 400 GB disk gets rounded up to a P20.</span></span> <span data-ttu-id="e40b8-252">Se você souber que não vai precisar do desempenho desse disco, poderá recriar a VM coo uma VM da série DS, e anexar VHDs de Armazenamento Premium com a especificação de tamanho/desempenho que quiser.</span><span class="sxs-lookup"><span data-stu-id="e40b8-252">If you know that you do not require that disk performance, then you could recreate the VM as a DS Series VM, and attach Premium Storage VHDs of the size/performance specification you require.</span></span> <span data-ttu-id="e40b8-253">Em seguida, você poderá desanexar e anexar novamente os arquivos de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e40b8-253">Then you could detach and reattach the SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="e40b8-254">Ao copiar os discos VHD, não se esqueça de considerar o tamanho, pois o tipo de Disco de Armazenamento Premium em que eles vão se enquadrar dependerá do tamanho e isso determina a especificação de desempenho de disco.</span><span class="sxs-lookup"><span data-stu-id="e40b8-254">When copying the VHD disks you should be aware of the size, depending on the size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="e40b8-255">O Azure arredondará para o tamanho de disco mais próximo, portanto, se você tiver um disco de 400 GB, ele será arredondado para um P20.</span><span class="sxs-lookup"><span data-stu-id="e40b8-255">Azure will round up to the nearest disk size, so if you have a 400GB disk, this will be rounded up to a P20.</span></span> <span data-ttu-id="e40b8-256">Dependendo dos requisitos de E/S existentes do VHD do sistema operacional, talvez não seja necessário migrá-lo para uma conta de Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-256">Depending on your existing IO requirements of the OS VHD, you might not need to migrate this to a Premium Storage account.</span></span>
>
>

<span data-ttu-id="e40b8-257">Se o SQL Server for acessado externamente, o VIP de serviço de nuvem será alterado.</span><span class="sxs-lookup"><span data-stu-id="e40b8-257">If your SQL Server is accessed externally, then the cloud service VIP will change.</span></span> <span data-ttu-id="e40b8-258">Você também terá que atualizar pontos de extremidade, ACLs e configurações de DNS.</span><span class="sxs-lookup"><span data-stu-id="e40b8-258">You will also have to update end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="e40b8-259">Implantações existentes que usam grupos de disponibilidade AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="e40b8-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="e40b8-260">Para implantações existentes, primeiro consulte a seção [Pré-requisitos](#prerequisites-for-premium-storage) deste tópico.</span><span class="sxs-lookup"><span data-stu-id="e40b8-260">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="e40b8-261">No início desta seção, vamos examinar como o AlwaysOn interage com a Rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="e40b8-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="e40b8-262">Em seguida, vamos dividir as migrações em dois cenários: migrações em que algum tempo de inatividade pode ser tolerado e migrações em que você deve obter o mínimo de tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="e40b8-262">We will then break down migrations in to two scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="e40b8-263">Os grupos de disponibilidade AlwaysOn locais do SQL Server usam um Ouvinte local que registra um nome DNS virtual junto com um endereço IP que é compartilhado entre um ou mais SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="e40b8-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="e40b8-264">Quando se conectam, os clientes são roteadas por meio do IP do ouvinte para o SQL Server Primário.</span><span class="sxs-lookup"><span data-stu-id="e40b8-264">When clients connect they are routed through the listener IP to the Primary SQL Server.</span></span> <span data-ttu-id="e40b8-265">Esse é o servidor que tem o recurso IP AlwaysOn no momento.</span><span class="sxs-lookup"><span data-stu-id="e40b8-265">This is the server that owns the Always On IP resource at that time.</span></span>

![DeploymentsUseAlways On][6]

<span data-ttu-id="e40b8-267">No Microsoft Azure, você pode ter apenas um endereço IP atribuído a uma NIC na máquina virtual, portanto, para atingir a mesma camada de abstração do local, o Azure utiliza o endereço IP que é atribuído aos balanceadores de carga internos ou externos (ILB/ELB).</span><span class="sxs-lookup"><span data-stu-id="e40b8-267">In Microsoft Azure you can have only one IP address assigned to a NIC on the VM, so in order to achieve the same layer of abstraction as on-premises, Azure utilizes the IP address that is assigned to the Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="e40b8-268">O recurso IP que é compartilhado entre os servidores é definido como o mesmo IP de ILB/ELB.</span><span class="sxs-lookup"><span data-stu-id="e40b8-268">The IP resource that is shared between the servers is set to the same IP as the ILB/ELB.</span></span> <span data-ttu-id="e40b8-269">Ele é publicado no DNS e o tráfego do cliente é transmitido por meio de ILB/ELB para a réplica do SQL Server Primário.</span><span class="sxs-lookup"><span data-stu-id="e40b8-269">This is published in the DNS, and client traffic is passed through the ILB/ELB to the Primary SQL Server replica.</span></span> <span data-ttu-id="e40b8-270">O ILB/ELB sabe qual SQL Server é o primário, pois ele usa testes para investigar o recurso IP AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="e40b8-270">The ILB/ELB knows which SQL Server is primary since it uses probes to probe the Always On IP resource.</span></span> <span data-ttu-id="e40b8-271">No exemplo anterior, ele investiga cada nó com um ponto de extremidade referenciado pelo ELB/ILB, aquele que responder será o SQL Server Primário.</span><span class="sxs-lookup"><span data-stu-id="e40b8-271">In the previous example, it probes each node that has an endpoint referenced by the ELB/ILB, whichever responds is the Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="e40b8-272">O ILB e o ELB são atribuídos a um serviço de nuvem do Azure específico, portanto, se ocorrer alguma migração de nuvem no Azure provavelmente isso significa que o IP do balanceador de carga será alterado.</span><span class="sxs-lookup"><span data-stu-id="e40b8-272">The ILB and ELB are both assigned to a particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that the Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="e40b8-273">Migrando implantações AlwaysOn que podem permitir algum tempo de inatividade</span><span class="sxs-lookup"><span data-stu-id="e40b8-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="e40b8-274">Existem duas estratégias para migrar as implantações AlwaysOn que permitem algum tempo de inatividade:</span><span class="sxs-lookup"><span data-stu-id="e40b8-274">There are two strategies to migrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="e40b8-275">**Adicionar mais réplicas secundárias a um cluster AlwaysOn existente**</span><span class="sxs-lookup"><span data-stu-id="e40b8-275">**Add more secondary replicas to an existing Always On Cluster**</span></span>
2. <span data-ttu-id="e40b8-276">**Migrar para um novo cluster AlwaysOn**</span><span class="sxs-lookup"><span data-stu-id="e40b8-276">**Migrate to a new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-to-an-existing-always-on-cluster"></a><span data-ttu-id="e40b8-277">1. Adicionar mais réplicas secundárias a um cluster AlwaysOn existente</span><span class="sxs-lookup"><span data-stu-id="e40b8-277">1. Add more Secondary Replicas to an Existing Always On Cluster</span></span>
<span data-ttu-id="e40b8-278">Uma estratégia é adicionar mais réplicas secundárias ao grupo de disponibilidade AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="e40b8-278">One strategy is to add more secondaries to the Always On Availability Group.</span></span> <span data-ttu-id="e40b8-279">Você precisa adicioná-las em um novo serviço de nuvem e atualizar o ouvinte com o novo IP do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="e40b8-279">You need to add these into a new cloud service and update the listener with the new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="e40b8-280">Pontos de tempo de inatividade:</span><span class="sxs-lookup"><span data-stu-id="e40b8-280">Points of downtime:</span></span>
* <span data-ttu-id="e40b8-281">Validação de cluster.</span><span class="sxs-lookup"><span data-stu-id="e40b8-281">Cluster Validation.</span></span>
* <span data-ttu-id="e40b8-282">Testando failovers AlwaysOn para secundárias novas.</span><span class="sxs-lookup"><span data-stu-id="e40b8-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="e40b8-283">Se você estiver usando Pools de Armazenamento do Windows na VM para obter uma taxa de transferência de E/S mais alta, eles serão colocados offline durante uma Validação de Cluster Completa.</span><span class="sxs-lookup"><span data-stu-id="e40b8-283">If you are using Windows Storage Pools within the VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="e40b8-284">O teste de validação é necessário quando você adiciona nós ao cluster.</span><span class="sxs-lookup"><span data-stu-id="e40b8-284">The validation test is required when you add nodes to the cluster.</span></span> <span data-ttu-id="e40b8-285">O tempo necessário para executar o teste pode variar, de modo que você deve testar isso em seu ambiente de teste representativo para obter um tempo aproximado para essa operação.</span><span class="sxs-lookup"><span data-stu-id="e40b8-285">The time it takes to run the test can vary, so you should test this in your representative test environment to get an approximate time of how long this will take.</span></span>

<span data-ttu-id="e40b8-286">Você deve provisionar o tempo em que é possível executar o failover manual e testes de caos nos nós adicionados recentemente para assegurar funções de Alta Disponibilidade AlwaysOn conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="e40b8-286">You should provision time where you can perform manual failover and chaos testing on the newly added nodes to ensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="e40b8-288">Você deve interromper todas as instâncias do SQL Server em que os Pools de Armazenamento forem usados antes de executar a Validação.</span><span class="sxs-lookup"><span data-stu-id="e40b8-288">You should stop all instances of SQL Server where the Storage Pools are used before the Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="e40b8-289">Etapas de alto nível</span><span class="sxs-lookup"><span data-stu-id="e40b8-289">High-level steps</span></span>
>

1. <span data-ttu-id="e40b8-290">Crie dois novos SQL Servers no novo serviço de nuvem com Armazenamento Premium anexado.</span><span class="sxs-lookup"><span data-stu-id="e40b8-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="e40b8-291">Copie sobre backups e restauração completos com **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="e40b8-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="e40b8-292">Copie sobre objetos dependentes de ‘banco de dados fora do usuário’, como logons etc.</span><span class="sxs-lookup"><span data-stu-id="e40b8-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="e40b8-293">Crie um novo ILB (balanceador de carga interno) ou use um ELB (balanceador de carga externo) e configure pontos de extremidade balanceados de carga em ambos os nós novos.</span><span class="sxs-lookup"><span data-stu-id="e40b8-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e40b8-294">Verifique se todos os nós têm a configuração do ponto de extremidade correta antes de continuar</span><span class="sxs-lookup"><span data-stu-id="e40b8-294">Check all Nodes have the correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="e40b8-295">Interrompa o acesso de usuário/aplicativo ao SQL Server (se você estiver usando pools de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="e40b8-295">Stop User/Application Access to the SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="e40b8-296">Interrompa serviços de mecanismo do SQL Server em todos os nós (se você estiver usando pools de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="e40b8-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="e40b8-297">Adicione novos nós ao cluster e execute a validação completa.</span><span class="sxs-lookup"><span data-stu-id="e40b8-297">Add new Nodes to cluster and run full validation.</span></span>
8. <span data-ttu-id="e40b8-298">Depois que a validação for bem-sucedida, inicie todos os Serviços do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e40b8-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="e40b8-299">Faça backup dos logs de transações e restaure os bancos de dados do usuário.</span><span class="sxs-lookup"><span data-stu-id="e40b8-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="e40b8-300">Adicione novos nós ao Grupo de Disponibilidade AlwaysOn e coloque a replicação em **Síncrono**.</span><span class="sxs-lookup"><span data-stu-id="e40b8-300">Add new nodes into the Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="e40b8-301">Adicione o recurso de endereço IP do novo ILB/ELB do serviço de nuvem por meio do PowerShell para AlwaysOn com base no exemplo de vários sites apresentado no [Apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="e40b8-301">Add the IP address resource of the new Cloud Service ILB/ELB through PowerShell for Always On based on the Multi-site example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="e40b8-302">No cluster do Windows, defina os **Possíveis proprietários** do recurso **Endereço IP** para os novos nós.</span><span class="sxs-lookup"><span data-stu-id="e40b8-302">In Windows clustering, set the **Possible owners** of the **IP Address** resource to the new nodes old.</span></span> <span data-ttu-id="e40b8-303">Consulte a seção "Adicionando o recurso de endereço IP na mesma sub-rede" do [Apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="e40b8-303">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="e40b8-304">Execute o failover para um dos novos nós.</span><span class="sxs-lookup"><span data-stu-id="e40b8-304">Failover to one of the new nodes.</span></span>
13. <span data-ttu-id="e40b8-305">Transforme os novos nós em Parceiros de Failover Automático e teste os failovers.</span><span class="sxs-lookup"><span data-stu-id="e40b8-305">Make the new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="e40b8-306">Remova os nós originais do grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="e40b8-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="e40b8-307">Vantagens</span><span class="sxs-lookup"><span data-stu-id="e40b8-307">Advantages</span></span>
* <span data-ttu-id="e40b8-308">Novos SQL Servers podem ser testados (SQL Server e aplicativo) antes de serem adicionados ao AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="e40b8-308">New SQL Servers can be tested (SQL Server and Application) before they are added to Always On.</span></span>
* <span data-ttu-id="e40b8-309">Você pode alterar o tamanho da VM e personalizar o armazenamento de acordo com seus requisitos exatos.</span><span class="sxs-lookup"><span data-stu-id="e40b8-309">You can change the VM size and customize the storage to your exact requirements.</span></span> <span data-ttu-id="e40b8-310">No entanto, seria vantajoso manter todos os caminhos de arquivo SQL iguais.</span><span class="sxs-lookup"><span data-stu-id="e40b8-310">However, it would be beneficial to keep all the SQL file paths the same.</span></span>
* <span data-ttu-id="e40b8-311">Você pode controlar quando a transferência dos backups de banco de dados para as réplicas secundárias será iniciado.</span><span class="sxs-lookup"><span data-stu-id="e40b8-311">You can control when the transfer of the DB backups to the Secondary Replicas are started.</span></span> <span data-ttu-id="e40b8-312">Isso é diferente de usar o commandlet do Azure **Start-AzureStorageBlobCopy** para copiar VHDs, pois essa é uma cópia assíncrona.</span><span class="sxs-lookup"><span data-stu-id="e40b8-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet to copy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="e40b8-313">Desvantagens</span><span class="sxs-lookup"><span data-stu-id="e40b8-313">Disadvantages</span></span>
* <span data-ttu-id="e40b8-314">Durante o uso de Pools de Armazenamento do Windows, há um tempo de inatividade de cluster na Validação de Cluster Completa para os novos nós adicionais.</span><span class="sxs-lookup"><span data-stu-id="e40b8-314">When using Windows Storage Pools, there is Cluster downtime during the Full Cluster Validation for the new additional nodes.</span></span>
* <span data-ttu-id="e40b8-315">Dependendo da versão do SQL Server e do número existente de réplicas secundárias, você não poderá adicionar mais réplicas secundárias sem remover as existentes.</span><span class="sxs-lookup"><span data-stu-id="e40b8-315">Depending on the SQL Server Version and the existing number of secondary replicas, you might not be able to add more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="e40b8-316">O tempo de transferência de dados SQL pode ser muito longo durante a configuração de réplicas secundárias.</span><span class="sxs-lookup"><span data-stu-id="e40b8-316">There could be long SQL data transfer time while setting up the secondaries.</span></span>
* <span data-ttu-id="e40b8-317">Há custos adicionais durante a migração quando há novas máquinas em execução em paralelo.</span><span class="sxs-lookup"><span data-stu-id="e40b8-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-to-a-new-always-on-cluster"></a><span data-ttu-id="e40b8-318">2. Migrar para um novo cluster AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="e40b8-318">2. Migrate to a new Always On Cluster</span></span>
<span data-ttu-id="e40b8-319">Outra estratégia é criar um novo cluster AlwaysOn com nós totalmente novos no novo serviço de nuvem e redirecionar os clientes para usá-lo.</span><span class="sxs-lookup"><span data-stu-id="e40b8-319">Another strategy is to create a brand new Always On Cluster with brand new nodes in new cloud service and then redirect the clients to use it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="e40b8-320">Pontos de tempo de inatividade</span><span class="sxs-lookup"><span data-stu-id="e40b8-320">Points of downtime</span></span>
<span data-ttu-id="e40b8-321">Há um tempo de inatividade quando você transfere aplicativos e usuários para o novo ouvinte AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="e40b8-321">There is downtime when you transfer applications and users to the new Always On listener.</span></span> <span data-ttu-id="e40b8-322">O tempo de inatividade depende do seguinte:</span><span class="sxs-lookup"><span data-stu-id="e40b8-322">The downtime depends on:</span></span>

* <span data-ttu-id="e40b8-323">Tempo necessário para restaurar backups de log de transações final para bancos de dados em novos servidores.</span><span class="sxs-lookup"><span data-stu-id="e40b8-323">The time taken to restore final transaction log backups to databases on new servers.</span></span>
* <span data-ttu-id="e40b8-324">Tempo necessário para atualizar os aplicativos cliente para usar o novo ouvinte AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="e40b8-324">The time taken to update client applications to use new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="e40b8-325">Vantagens</span><span class="sxs-lookup"><span data-stu-id="e40b8-325">Advantages</span></span>
* <span data-ttu-id="e40b8-326">Você pode testar o ambiente de produção real, o SQL Server e as alterações de compilação do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="e40b8-326">You can test the actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="e40b8-327">Você tem a opção de personalizar o armazenamento e reduzir o tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="e40b8-327">You have the option to customize the storage and to potentially reduce size of VM.</span></span> <span data-ttu-id="e40b8-328">Isso pode resultar na redução de custos.</span><span class="sxs-lookup"><span data-stu-id="e40b8-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="e40b8-329">Você pode atualizar sua compilação ou versão do SQL Server durante esse processo.</span><span class="sxs-lookup"><span data-stu-id="e40b8-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="e40b8-330">Você também pode atualizar o sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="e40b8-330">You can also upgrade the Operating System.</span></span>
* <span data-ttu-id="e40b8-331">O cluster AlwaysOn anterior pode atuar como um destino de reversão sólido.</span><span class="sxs-lookup"><span data-stu-id="e40b8-331">The previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="e40b8-332">Desvantagens</span><span class="sxs-lookup"><span data-stu-id="e40b8-332">Disadvantages</span></span>
* <span data-ttu-id="e40b8-333">Você precisará alterar o nome DNS do ouvinte se quiser que os dois clusters AlwaysOn sejam executados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="e40b8-333">You need to change the DNS name of the listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="e40b8-334">Isso adiciona sobrecarga administrativa durante a migração, pois as cadeias de caracteres de aplicativo cliente devem refletir o novo nome do ouvinte.</span><span class="sxs-lookup"><span data-stu-id="e40b8-334">This adds administration overhead during the migration as client application strings must reflect the new Listener name.</span></span>
* <span data-ttu-id="e40b8-335">Você deve implementar um mecanismo de sincronização entre os dois ambientes para mantê-los o mais próximo possível para minimizar os requisitos de sincronização final antes da migração.</span><span class="sxs-lookup"><span data-stu-id="e40b8-335">You must implement a synchronization mechanism between the two environments to keep them as close as possible to minimize the final synchronization requirements before migration.</span></span>
* <span data-ttu-id="e40b8-336">Há um custo adicional durante a migração com o novo ambiente em execução.</span><span class="sxs-lookup"><span data-stu-id="e40b8-336">There is added cost during migration while you have the new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="e40b8-337">Migrando implantações AlwaysOn para tempo de inatividade mínimo</span><span class="sxs-lookup"><span data-stu-id="e40b8-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="e40b8-338">Existem duas estratégias para migrar implantações AlwaysOn para o tempo de inatividade mínimo:</span><span class="sxs-lookup"><span data-stu-id="e40b8-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="e40b8-339">**Utilizar uma réplica secundária existente: site único**</span><span class="sxs-lookup"><span data-stu-id="e40b8-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="e40b8-340">**Utilizar réplicas secundárias existentes: vários sites**</span><span class="sxs-lookup"><span data-stu-id="e40b8-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="e40b8-341">1. Utilizar uma réplica secundária existente: site único</span><span class="sxs-lookup"><span data-stu-id="e40b8-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="e40b8-342">Uma estratégia para tempo de inatividade mínimo é usar uma réplica secundária de nuvem existente e removê-la do serviço de nuvem atual.</span><span class="sxs-lookup"><span data-stu-id="e40b8-342">One strategy for minimal downtime is to take an existing cloud secondary and remove it from the current cloud service.</span></span> <span data-ttu-id="e40b8-343">Em seguida, copie os VHDs para a nova conta de Armazenamento Premium e crie a VM no novo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e40b8-343">Then copy the VHDs to the new Premium Storage account, and create the VM in the new cloud service.</span></span> <span data-ttu-id="e40b8-344">Em seguida, atualize o ouvinte no clustering e failover.</span><span class="sxs-lookup"><span data-stu-id="e40b8-344">Then update the listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="e40b8-345">Pontos de tempo de inatividade</span><span class="sxs-lookup"><span data-stu-id="e40b8-345">Points of downtime</span></span>
* <span data-ttu-id="e40b8-346">Há um tempo de inatividade quando você atualiza o nó final com o ponto de extremidade de carga balanceada.</span><span class="sxs-lookup"><span data-stu-id="e40b8-346">There is downtime when you update the final node with the Load Balanced endpoint.</span></span>
* <span data-ttu-id="e40b8-347">A reconexão do cliente pode ser atrasada dependendo da configuração do cliente/DNS.</span><span class="sxs-lookup"><span data-stu-id="e40b8-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="e40b8-348">Haverá um tempo de inatividade adicional se você optar por colocar o grupo de cluster AlwaysOn offline para trocar os endereços IP.</span><span class="sxs-lookup"><span data-stu-id="e40b8-348">There is additional downtime if you choose to take the Always On Cluster group offline to swap out the IP addresses.</span></span> <span data-ttu-id="e40b8-349">Você pode evitar isso usando uma dependência OR e possíveis proprietários para o recurso de endereço IP adicionado.</span><span class="sxs-lookup"><span data-stu-id="e40b8-349">You can avoid this by using an OR dependency and Possible Owners for the added IP Address resource.</span></span> <span data-ttu-id="e40b8-350">Consulte a seção "Adicionando o recurso de endereço IP na mesma sub-rede" do [Apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="e40b8-350">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="e40b8-351">Quando quiser que o nó adicional participe como um parceiro de failover AlwaysOn, você precisará adicionar um ponto de extremidade do Azure com uma referência a um conjunto de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="e40b8-351">When you want the added node to partake in as an Always On Failover Partner, you need to add an Azure Endpoint with a reference to the Load Balanced Set.</span></span> <span data-ttu-id="e40b8-352">Quando você executa o comando **Add-AzureEndpoint** para fazer isso, as conexões atuais permanecem abertas, mas as novas conexões com o ouvinte não poderão ser estabelecidas até o balanceador de carga ser atualizado.</span><span class="sxs-lookup"><span data-stu-id="e40b8-352">When you run the **Add-AzureEndpoint** command to do this, current connections to remain open, but new connections to the listener will not be able to be established until the load balancer has updated.</span></span> <span data-ttu-id="e40b8-353">Em testes, observou-se que isso durava de 90 a 120 segundos, mas é necessário conferir.</span><span class="sxs-lookup"><span data-stu-id="e40b8-353">In testing this was seen to last 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="e40b8-354">Vantagens</span><span class="sxs-lookup"><span data-stu-id="e40b8-354">Advantages</span></span>
* <span data-ttu-id="e40b8-355">Sem custo extra incorrido durante a migração.</span><span class="sxs-lookup"><span data-stu-id="e40b8-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="e40b8-356">Uma migração um-para-um.</span><span class="sxs-lookup"><span data-stu-id="e40b8-356">A one-to-one migration.</span></span>
* <span data-ttu-id="e40b8-357">Redução da complexidade.</span><span class="sxs-lookup"><span data-stu-id="e40b8-357">Reduced complexity.</span></span>
* <span data-ttu-id="e40b8-358">Permite maior IOPS de SKUs de Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="e40b8-359">Quando os discos são desanexados da VM e copiados para o novo serviço de nuvem, uma ferramenta de terceiros pode ser usada para aumentar o tamanho do VHD, que oferece taxas de transferência mais altas.</span><span class="sxs-lookup"><span data-stu-id="e40b8-359">When the disks are detached from the VM and copied to the new cloud service, a 3rd party tool can be used to increase the VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="e40b8-360">Para tamanhos de VHD maiores, consulte este [fórum de discussão](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span><span class="sxs-lookup"><span data-stu-id="e40b8-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="e40b8-361">Desvantagens</span><span class="sxs-lookup"><span data-stu-id="e40b8-361">Disadvantages</span></span>
* <span data-ttu-id="e40b8-362">Há uma perda temporária de alta disponibilidade e recuperação de desastre durante a migração.</span><span class="sxs-lookup"><span data-stu-id="e40b8-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="e40b8-363">Como essa é uma migração 1:1, você terá que usar um tamanho mínimo de VM que dará suporte a seu número de VHDs, portanto, você não poderá diminuir suas VMs.</span><span class="sxs-lookup"><span data-stu-id="e40b8-363">As this is a 1:1 migration, you will have to use a minimum VM size that will support your number of VHDs, so you might not be able to downsize your VMs.</span></span>
* <span data-ttu-id="e40b8-364">Este cenário usa o commandlet Azure **Start-AzureStorageBlobCopy** , que é assíncrono.</span><span class="sxs-lookup"><span data-stu-id="e40b8-364">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="e40b8-365">Não há nenhum SLA na conclusão da cópia.</span><span class="sxs-lookup"><span data-stu-id="e40b8-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="e40b8-366">O tempo das cópias varia, embora isso dependa da espera na fila, também dependerá da quantidade de dados a ser transferida.</span><span class="sxs-lookup"><span data-stu-id="e40b8-366">The time of the copies varies, while this depends on wait in queue it will also depend on the amount of data to transfer.</span></span> <span data-ttu-id="e40b8-367">O tempo de cópia aumentará se a transferência for para outro data center do Azure que com suporte ao Armazenamento Premium em outra região.</span><span class="sxs-lookup"><span data-stu-id="e40b8-367">The copy time increases if the transfer is going to another Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="e40b8-368">Se você tiver apenas dois nós, considere uma possível redução, caso a cópia demore mais do que no teste.</span><span class="sxs-lookup"><span data-stu-id="e40b8-368">If you just have 2 nodes, consider a possible mitigation in case the copy takes longer than in testing.</span></span> <span data-ttu-id="e40b8-369">Isso pode incluir as ideias a seguir.</span><span class="sxs-lookup"><span data-stu-id="e40b8-369">This could include the following ideas.</span></span>
  * <span data-ttu-id="e40b8-370">Adicione um terceiro nó temporário do SQL Server para alta disponibilidade antes da migração com tempo de inatividade estabelecido.</span><span class="sxs-lookup"><span data-stu-id="e40b8-370">Add a temporary 3rd SQL Server node for HA before the migration with agreed downtime.</span></span>
  * <span data-ttu-id="e40b8-371">Execute a migração fora da manutenção programada do Azure.</span><span class="sxs-lookup"><span data-stu-id="e40b8-371">Run the migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="e40b8-372">Verifique se você configurou corretamente o quorum do cluster.</span><span class="sxs-lookup"><span data-stu-id="e40b8-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="e40b8-373">Etapas de alto nível</span><span class="sxs-lookup"><span data-stu-id="e40b8-373">High-level steps</span></span>
<span data-ttu-id="e40b8-374">Este documento não demonstra um exemplo completo de ponta a ponta, no entanto, o [Apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) fornece detalhes que podem ser usados para isso.</span><span class="sxs-lookup"><span data-stu-id="e40b8-374">This document does not demonstrate a complete end to end example, however the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged to perform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="e40b8-376">Obtenha a configuração de disco e remova o nó (não exclua VHDs anexados).</span><span class="sxs-lookup"><span data-stu-id="e40b8-376">Gather disk configuration, and remove the node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="e40b8-377">Crie uma conta de Armazenamento Premium e copie VHDs da conta de Armazenamento Padrão</span><span class="sxs-lookup"><span data-stu-id="e40b8-377">Create a Premium Storage account and copy VHDs from the Standard Storage account</span></span>
* <span data-ttu-id="e40b8-378">Crie um novo serviço de nuvem e reimplante a VM SQL2 no serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e40b8-378">Create new cloud service and redeploy the SQL2 VM in that cloud service.</span></span> <span data-ttu-id="e40b8-379">Crie a VM usando o VHD do sistema operacional original copiado e anexe VHDs copiados.</span><span class="sxs-lookup"><span data-stu-id="e40b8-379">Create the VM using the copied original OS VHD and attaching the copied VHDs.</span></span>
* <span data-ttu-id="e40b8-380">Configure o ILB / ELB e adicione pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="e40b8-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="e40b8-381">Siga um destes procedimentos para atualizar o ouvinte:</span><span class="sxs-lookup"><span data-stu-id="e40b8-381">Update Listener by either:</span></span>
  * <span data-ttu-id="e40b8-382">Coloque o grupo AlwaysOn offline e atualize o ouvinte AlwaysOn com o novo endereço IP ILB/ELB.</span><span class="sxs-lookup"><span data-stu-id="e40b8-382">Taking the Always On Group offline and updating the Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="e40b8-383">Ou adicione o recurso de endereço IP do novo ILB/ELB do serviço de nuvem por meio do PowerShell para clustering do Windows.</span><span class="sxs-lookup"><span data-stu-id="e40b8-383">Or adding the IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="e40b8-384">Em seguida, defina os possíveis proprietários do recurso de endereço IP para o nó migrado, o SQL2 e defina isso como dependência OR no nome da rede.</span><span class="sxs-lookup"><span data-stu-id="e40b8-384">Then set the Possible owners of the IP Address resource to the migrated node, SQL2, and set this as OR dependency in the Network Name.</span></span> <span data-ttu-id="e40b8-385">Consulte a seção "Adicionando o recurso de endereço IP na mesma sub-rede" do [Apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="e40b8-385">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="e40b8-386">Verifique a configuração/propagação DNS para os clientes.</span><span class="sxs-lookup"><span data-stu-id="e40b8-386">Check DNS configuration/propogation to the clients.</span></span>
* <span data-ttu-id="e40b8-387">Migre a VM do SQL1 e siga as etapas 2 a 4.</span><span class="sxs-lookup"><span data-stu-id="e40b8-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="e40b8-388">Se você seguir as etapas 5ii, adicione SQL1 como um possível proprietário para o recurso de endereço IP adicionado</span><span class="sxs-lookup"><span data-stu-id="e40b8-388">If using steps 5ii, then add SQL1 as a Possible Owner for the added IP Address Resource</span></span>
* <span data-ttu-id="e40b8-389">Failovers de teste.</span><span class="sxs-lookup"><span data-stu-id="e40b8-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="e40b8-390">2. Utilizar réplicas secundárias existentes: vários sites</span><span class="sxs-lookup"><span data-stu-id="e40b8-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="e40b8-391">Se tiver nós em mais de um DC (data center) do Azure ou se tiver um ambiente híbrido, você poderá usar uma configuração AlwaysOn nesse ambiente para minimizar o tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="e40b8-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment to minimize downtime.</span></span>

<span data-ttu-id="e40b8-392">A abordagem é alterar a sincronização AlwaysOn para Síncrona para o DC do Azure local ou secundário e executar o failover para esse SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e40b8-392">The approach is to change the Always On synchronization to Synchronous for the on-premises or secondary Azure DC, and then failover over to that SQL Server.</span></span> <span data-ttu-id="e40b8-393">Em seguida, copie os VHDs em uma conta de Armazenamento Premium e reimplante a máquina em um novo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e40b8-393">Then copy the VHDs to a Premium Storage account, and redeploy the machine into a new cloud service.</span></span> <span data-ttu-id="e40b8-394">Atualize o ouvinte e, em seguida, execute o failback.</span><span class="sxs-lookup"><span data-stu-id="e40b8-394">Update the listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="e40b8-395">Pontos de tempo de inatividade</span><span class="sxs-lookup"><span data-stu-id="e40b8-395">Points of downtime</span></span>
<span data-ttu-id="e40b8-396">O tempo de inatividade consiste no tempo para executar o failover para o controlador de domínio alternativo e voltar.</span><span class="sxs-lookup"><span data-stu-id="e40b8-396">The downtime consists of the time to failover to the alternative DC and back.</span></span> <span data-ttu-id="e40b8-397">Também depende da sua configuração cliente/DNS e a reconexão do cliente poder ser atrasada.</span><span class="sxs-lookup"><span data-stu-id="e40b8-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="e40b8-398">Considere o seguinte exemplo de uma configuração AlwaysOn híbrida:</span><span class="sxs-lookup"><span data-stu-id="e40b8-398">Consider the following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="e40b8-400">Vantagens</span><span class="sxs-lookup"><span data-stu-id="e40b8-400">Advantages</span></span>
* <span data-ttu-id="e40b8-401">Você pode utilizar a infraestrutura existente.</span><span class="sxs-lookup"><span data-stu-id="e40b8-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="e40b8-402">Você tem a opção de atualizar previamente o armazenamento do Azure no controlador de domínio do Azure DR pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="e40b8-402">You have the option to pre-upgrade the Azure storage on the DR Azure DC first.</span></span>
* <span data-ttu-id="e40b8-403">O armazenamento do controlador de domínio do Azure DR pode ser reconfigurado.</span><span class="sxs-lookup"><span data-stu-id="e40b8-403">The DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="e40b8-404">Há um mínimo de dois failovers durante a migração, excluindo failovers de teste.</span><span class="sxs-lookup"><span data-stu-id="e40b8-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="e40b8-405">Você não precisa mover dados do SQL Server com backup e restauração.</span><span class="sxs-lookup"><span data-stu-id="e40b8-405">You do not need to move SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="e40b8-406">Desvantagens</span><span class="sxs-lookup"><span data-stu-id="e40b8-406">Disadvantages</span></span>
* <span data-ttu-id="e40b8-407">Dependendo do acesso de cliente para o SQL Server, poderá haver latência aumentada quando o SQL Server estiver em execução em um controlador de domínio alternativo para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e40b8-407">Depending on client access to SQL Server, there might be increased latency when SQL Server is running in an alternative DC to the application.</span></span>
* <span data-ttu-id="e40b8-408">O tempo de cópia de VHDs de armazenamento Premium pode ser longo.</span><span class="sxs-lookup"><span data-stu-id="e40b8-408">The copy time of VHDs to Premium storage could be long.</span></span> <span data-ttu-id="e40b8-409">Isso poderá afetar sua decisão de manter o nó no grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="e40b8-409">This might affect your decision on whether to keep the node in the Availability Group.</span></span> <span data-ttu-id="e40b8-410">Considere isso para ocasiões em que a execução de cargas de trabalho com uso intensivo de log durante a migração for necessária, pois o nó primário terá que manter as transações não replicadas em seu log de transações.</span><span class="sxs-lookup"><span data-stu-id="e40b8-410">Consider this for when log intensive work loads are running during the migration is required, since the Primary node will have to keep the unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="e40b8-411">Portanto, isso pode crescer significativamente.</span><span class="sxs-lookup"><span data-stu-id="e40b8-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="e40b8-412">Este cenário usa o commandlet Azure **Start-AzureStorageBlobCopy** , que é assíncrono.</span><span class="sxs-lookup"><span data-stu-id="e40b8-412">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="e40b8-413">Não há nenhum SLA a concluir.</span><span class="sxs-lookup"><span data-stu-id="e40b8-413">There is no SLA on completion.</span></span> <span data-ttu-id="e40b8-414">O tempo das cópias varia, embora isso dependa da espera na fila, também dependerá da quantidade de dados a ser transferida.</span><span class="sxs-lookup"><span data-stu-id="e40b8-414">The time of the copies varies, while this depends on wait in queue, it will also depend on the amount of data to transfer.</span></span> <span data-ttu-id="e40b8-415">Portanto, você tem apenas um nó no segundo data center. Adote medidas de redução, caso a cópia demore mais do que no teste.</span><span class="sxs-lookup"><span data-stu-id="e40b8-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case the copy takes longer than in testing.</span></span> <span data-ttu-id="e40b8-416">Isso pode incluir as ideias a seguir.</span><span class="sxs-lookup"><span data-stu-id="e40b8-416">This could include the following ideas.</span></span>
  * <span data-ttu-id="e40b8-417">Adicione um segundo nó temporário do SQL para alta disponibilidade antes da migração com tempo de inatividade estabelecido.</span><span class="sxs-lookup"><span data-stu-id="e40b8-417">Add a temporary 2nd SQL node for HA before the migration with agreed downtime.</span></span>
  * <span data-ttu-id="e40b8-418">Execute a migração fora da manutenção programada do Azure.</span><span class="sxs-lookup"><span data-stu-id="e40b8-418">Run the migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="e40b8-419">Verifique se você configurou corretamente o quorum do cluster.</span><span class="sxs-lookup"><span data-stu-id="e40b8-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="e40b8-420">Esse cenário pressupõe que você documentou sua instalação e sabe como o armazenamento é mapeado para fazer alterações para as configurações de cache de disco ideais.</span><span class="sxs-lookup"><span data-stu-id="e40b8-420">This scenario assumes that you have documented your install and know how the storage is mapped in order to make changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="e40b8-421">Etapas de alto nível</span><span class="sxs-lookup"><span data-stu-id="e40b8-421">High-level steps</span></span>
![Multisite2][10]

* <span data-ttu-id="e40b8-423">Torne o controlador de domínio do Azure local / alternativo o SQL Server Primário e torne-o o outro AFP (Parceiro de Failover Automático).</span><span class="sxs-lookup"><span data-stu-id="e40b8-423">Make the on-premises / alternate Azure DC the SQL Server Primary, and make it the other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="e40b8-424">Obtenha as informações de configuração de disco do SQL2 e remova o nó (não exclua VHDs anexados).</span><span class="sxs-lookup"><span data-stu-id="e40b8-424">Gather disk configuration information from SQL2, and remove the node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="e40b8-425">Crie uma conta de Armazenamento Premium e copie VHDs da conta de Armazenamento Padrão.</span><span class="sxs-lookup"><span data-stu-id="e40b8-425">Create a Premium Storage account and copy VHDs from the Standard Storage account.</span></span>
* <span data-ttu-id="e40b8-426">Crie um novo serviço de nuvem e crie a VM SQL2 com seus discos de Armazenamento Premium anexados.</span><span class="sxs-lookup"><span data-stu-id="e40b8-426">Create a new cloud service and create the SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="e40b8-427">Configure o ILB / ELB e adicione pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="e40b8-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="e40b8-428">Atualize o ouvinte AlwaysOn com novos endereços IP ILB/ELB e failover de teste.</span><span class="sxs-lookup"><span data-stu-id="e40b8-428">Update the Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="e40b8-429">Verifique a configuração DNS.</span><span class="sxs-lookup"><span data-stu-id="e40b8-429">Check the DNS configuration.</span></span>
* <span data-ttu-id="e40b8-430">Altere o AFP para o SQL2, migre o SQL1 e execute as etapas 2 a 5.</span><span class="sxs-lookup"><span data-stu-id="e40b8-430">Change the AFP to SQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="e40b8-431">Failovers de teste.</span><span class="sxs-lookup"><span data-stu-id="e40b8-431">Test failovers.</span></span>
* <span data-ttu-id="e40b8-432">Alternar o AFP de volta para SQL1 e SQL2</span><span class="sxs-lookup"><span data-stu-id="e40b8-432">Switch the AFP back to SQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-to-premium-storage"></a><span data-ttu-id="e40b8-433">Apêndice: Migrando um cluster AlwaysOn de vários sites para o Armazenamento Premium</span><span class="sxs-lookup"><span data-stu-id="e40b8-433">Appendix: Migrating a Multisite Always On Cluster to Premium Storage</span></span>
<span data-ttu-id="e40b8-434">O restante deste tópico fornece um exemplo detalhado de conversão de um cluster AlwaysOn de vários sites para o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e40b8-434">The remainder of this topic provides a detailed example of converting a multi-site Always On cluster to Premium storage.</span></span> <span data-ttu-id="e40b8-435">Ele também converte o Ouvinte de usar um ELB (balanceador de carga externo) em um ILB (balanceador de carga interno).</span><span class="sxs-lookup"><span data-stu-id="e40b8-435">It also converts the Listener from using an external load balancer (ELB) to an internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="e40b8-436">Ambiente</span><span class="sxs-lookup"><span data-stu-id="e40b8-436">Environment</span></span>
* <span data-ttu-id="e40b8-437">Windows 2k12 / SQL 2k12</span><span class="sxs-lookup"><span data-stu-id="e40b8-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="e40b8-438">1 arquivo de banco de dados no SP</span><span class="sxs-lookup"><span data-stu-id="e40b8-438">1 DB Files on SP</span></span>
* <span data-ttu-id="e40b8-439">2 x pools de armazenamento por nó</span><span class="sxs-lookup"><span data-stu-id="e40b8-439">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="e40b8-441">VM:</span><span class="sxs-lookup"><span data-stu-id="e40b8-441">VM:</span></span>
<span data-ttu-id="e40b8-442">Neste exemplo, vamos demonstrar a movimentação de um ELB para ILB.</span><span class="sxs-lookup"><span data-stu-id="e40b8-442">In this example we are going to demonstrate moving from an ELB to ILB.</span></span> <span data-ttu-id="e40b8-443">O ELB estava disponível antes do ILB, então esse procedimento mostra como alternar para isso durante a migração.</span><span class="sxs-lookup"><span data-stu-id="e40b8-443">ELB was available before ILB, so this shows how to switch to this during the migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-to-subscription"></a><span data-ttu-id="e40b8-445">Pré-etapas: conectar-se à assinatura</span><span class="sxs-lookup"><span data-stu-id="e40b8-445">Pre Steps: Connect to Subscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="e40b8-446">Etapa 1: criar a nova conta de armazenamento e o serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="e40b8-446">Step 1: Create New Storage Account and Cloud Service</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where the vm to migrate resides
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

#### <a name="step-2-increase-the-permitted-failures-on-resources-optional"></a><span data-ttu-id="e40b8-447">Etapa 2: Aumentar as falhas permitidas nos recursos <Optional></span><span class="sxs-lookup"><span data-stu-id="e40b8-447">Step 2: Increase the permitted failures on resources <Optional></span></span>
<span data-ttu-id="e40b8-448">Em determinados recursos que pertencem ao seu grupo de disponibilidade AlwaysOn há limites no número de falhas que podem ocorrer em um período, em que o serviço de cluster tentará reiniciar o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e40b8-448">On certain resources that belong to your Always On Availability Group there are limits on how many failures that can occur in a period, where the cluster service will attempt to restart the resource group.</span></span> <span data-ttu-id="e40b8-449">É recomendável aumentar isso, durante a execução deste procedimento, pois se não você não executar manualmente o failover e disparar failovers desligando máquinas, poderá chegar perto desse limite.</span><span class="sxs-lookup"><span data-stu-id="e40b8-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close to this limit.</span></span>

<span data-ttu-id="e40b8-450">Aconselhamos a dobrar a concessão de falha. Para fazer isso no Gerenciador de Cluster de Failover, acesse as Propriedades do grupo de recursos AlwaysOn:</span><span class="sxs-lookup"><span data-stu-id="e40b8-450">It would be prudent to double the failure allowance, to do this in Failover Cluster Manager, go to the Properties of the Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="e40b8-452">Altere o Máximo de Falhas para 6.</span><span class="sxs-lookup"><span data-stu-id="e40b8-452">Change the Maximum Failures to 6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="e40b8-453">Etapa 3: Adição do recurso de endereço IP ao grupo de clusters <Optional></span><span class="sxs-lookup"><span data-stu-id="e40b8-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="e40b8-454">Se você tiver apenas um endereço IP para o grupo de clusters e ele estiver alinhado à sub-rede de nuvem, tome cuidado: se você acidentalmente colocar offline todos os nós de cluster na nuvem nessa rede, o recurso de IP de cluster e o nome de rede do cluster não poderão ficar online.</span><span class="sxs-lookup"><span data-stu-id="e40b8-454">If you have only one IP address for the Cluster Group and this is aligned to the cloud subnet, beware, if you accidentally take offline all cluster nodes in the cloud on that network then the Cluster IP resource and Cluster Network Name will not be able to come online.</span></span> <span data-ttu-id="e40b8-455">Caso isso ocorra, as atualizações serão impedidas para outros recursos de cluster.</span><span class="sxs-lookup"><span data-stu-id="e40b8-455">In the event of this it will prevent updates to other cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="e40b8-456">Etapa 4: Configuração de DNS</span><span class="sxs-lookup"><span data-stu-id="e40b8-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="e40b8-457">A implementação de uma transição suave depende de como o DNS está sendo utilizado e atualizado.</span><span class="sxs-lookup"><span data-stu-id="e40b8-457">To implement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="e40b8-458">Quando o AlwaysOn está instalado, ele cria um grupo de recursos de cluster do Windows. Se você abrir o Gerenciador de Cluster de Failover, verá que, no mínimo, ele terá três recursos, os dois aos que o documento se refere são:</span><span class="sxs-lookup"><span data-stu-id="e40b8-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, the two that the document refers to are:</span></span>

* <span data-ttu-id="e40b8-459">VNN (Nome da Rede Virtual): este é o nome DNS ao qual o cliente se conecta quando quer se conectar aos SQL Servers via AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="e40b8-459">Virtual Network Name (VNN) – This is the DNS name that client connect to when wanting to connect to SQL Servers via Always On.</span></span>
* <span data-ttu-id="e40b8-460">Recurso de endereço IP – Este é o endereço IP associado à VNN. Você pode ter mais de um e, em uma configuração de vários sites, terá um endereço IP por site/sub-rede.</span><span class="sxs-lookup"><span data-stu-id="e40b8-460">IP Address Resource – This is the IP address that associated with the VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="e40b8-461">Quando se conectar ao SQL Server, o driver do Cliente do SQL Server recuperará os registros DNS associados ao ouvinte e tentará se conectar a cada endereço IP AlwaysOn associado. Abaixo, discutiremos alguns fatores que podem influenciar isso.</span><span class="sxs-lookup"><span data-stu-id="e40b8-461">When connecting to SQL Server, the SQL Server Client driver will retrieve the DNS records associated with the listener and try to connect to each Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="e40b8-462">O número de registros DNS simultâneos associados ao nome do ouvinte depende não só do número de endereços IP associados, mas da configuração ‘RegisterAllIpProviders' no Clustering de Failover para o recurso de VNN AlwaysON.</span><span class="sxs-lookup"><span data-stu-id="e40b8-462">The number of concurrent DNS records that are associated with the listener name depends not only on the number of IP addresses associated, but the ‘RegisterAllIpProviders’setting in Failover Clustering for the Always ON VNN resource.</span></span>

<span data-ttu-id="e40b8-463">Quando você implanta o AlwaysOn no Azure, há diferentes etapas para criar os Endereços IP e o Ouvinte. É necessário configurar manualmente ‘RegisterAllIpProviders’ como 1 e isso é diferente para uma implantação local AlwaysOn em que já está definido como 1.</span><span class="sxs-lookup"><span data-stu-id="e40b8-463">When you deploy Always On in Azure there are different steps to create the Listener and IP Addresses, you have to manually configure the ‘RegisterAllIpProviders’ to 1, this is different to an on-premises Always On deployment where it is already set to 1.</span></span>

<span data-ttu-id="e40b8-464">Se 'RegisterAllIpProviders' for 0, você verá somente um registro DNS no DNS associado com o ouvinte:</span><span class="sxs-lookup"><span data-stu-id="e40b8-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with the Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="e40b8-466">Se 'RegisterAllIpProviders' for 1:</span><span class="sxs-lookup"><span data-stu-id="e40b8-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="e40b8-468">O código a seguir despejará as configurações de VNN e as definirá para você. Observe que, para que a alteração tenha efeito, será necessário colocar a VNN offline e novamente online, colocando offline o ouvinte que esteja causando interrupções de conectividade de cliente.</span><span class="sxs-lookup"><span data-stu-id="e40b8-468">The code below will dump out the VNN settings and set it for you, please note, for the change to take effect you will need to take the VNN offline and turn it back online, this taking the Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="e40b8-469">Em uma etapa de migração posterior, você precisará atualizar o ouvinte AlwaysOn com um endereço IP atualizado que fará referência a um balanceador de carga. Isso envolverá uma remoção e uma adição do recurso de endereço IP.</span><span class="sxs-lookup"><span data-stu-id="e40b8-469">In a later migration step you will need to update the Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="e40b8-470">Após a atualização IP, você precisa garantir que o novo endereço IP tenha sido atualizado na zona DNS e que os clientes estejam atualizando seu cache DNS local.</span><span class="sxs-lookup"><span data-stu-id="e40b8-470">After the IP update, you need to ensure the new IP address has been updated in DNS Zone and that the clients are updating their local DNS cache.</span></span>

<span data-ttu-id="e40b8-471">Se os clientes residirem em um segmento de rede diferente e referenciarem um servidor DNS diferente, você terá que considerar o que acontece com a transferência de zona DNS durante a migração, pois o tempo de reconexão de aplicativo será restrito por pelo menos o tempo de transferência de zona de quaisquer novos endereços IP para o ouvinte.</span><span class="sxs-lookup"><span data-stu-id="e40b8-471">If your clients reside in a different network segment and reference a different DNS server, you need to consider what happens about DNS Zone Transfer during the migration, as the application reconnect time will be constrained by at least the Zone Transfer Time of any new IP addresses for the listener.</span></span> <span data-ttu-id="e40b8-472">Se tiver pouco tempo aqui, você deverá discutir e testar forçar uma transferência de zona incremental com as equipes do Windows e definir o registro de host DNS para uma TTL (tempo de vida) menor, para atualização dos clientes.</span><span class="sxs-lookup"><span data-stu-id="e40b8-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put the DNS host record to a lower Time To Live (TTL), so the clients update.</span></span> <span data-ttu-id="e40b8-473">Para obter mais informações, consulte [Transferências de Zona Incrementais](https://technet.microsoft.com/library/cc958973.aspx) e [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span><span class="sxs-lookup"><span data-stu-id="e40b8-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="e40b8-474">Por padrão, a TTL do registro DNS que está associada ao ouvinte no AlwaysOn no Azure é de 1200 segundos.</span><span class="sxs-lookup"><span data-stu-id="e40b8-474">By default the TTL for DNS Record that is associated with the Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="e40b8-475">Talvez você queira reduzi-lo se houver restrições de tempo durante sua migração para assegurar que os clientes atualizem seu DNS com o endereço IP atualizado do ouvinte.</span><span class="sxs-lookup"><span data-stu-id="e40b8-475">You may wish to reduce this if you are under time constraint during your migration to ensure the clients update their DNS with the updated IP address for the listener.</span></span> <span data-ttu-id="e40b8-476">Você pode ver e modificar a configuração despejando a configuração de VNN:</span><span class="sxs-lookup"><span data-stu-id="e40b8-476">You can see and modify the configuration by dumping out the configuration of the VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="e40b8-477">Observe que, quanto menor for 'HostRecordTTL', ocorrerá uma maior quantidade de tráfego DNS.</span><span class="sxs-lookup"><span data-stu-id="e40b8-477">Please note, the lower the ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="e40b8-478">Configurações de aplicativo cliente</span><span class="sxs-lookup"><span data-stu-id="e40b8-478">Client application settings</span></span>
<span data-ttu-id="e40b8-479">Se seu aplicativo cliente do SQL der suporte ao .Net 4.5 SQLClient, você poderá usar a palavra-chave ‘MULTISUBNETFAILOVER=TRUE’. A aplicação dessa opção é recomendável, pois ela permite a conexão mais rápida com o grupo de disponibilidade AlwaysOn do SQL durante o failover.</span><span class="sxs-lookup"><span data-stu-id="e40b8-479">If your SQL client application supports the .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended to be applied as it allows for faster connection to SQL Always On Availability Group during failover.</span></span> <span data-ttu-id="e40b8-480">Isso enumera todos os endereços IP associados ao ouvinte AlwaysOn em paralelo e executa uma velocidade de repetição de conexão TCP mais agressiva durante um failover.</span><span class="sxs-lookup"><span data-stu-id="e40b8-480">It enumerates through all IP addresses associated with the Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="e40b8-481">Para saber mais sobre as configurações acima, confira [Palavra-chave MultiSubnetFailover e recursos associados](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span><span class="sxs-lookup"><span data-stu-id="e40b8-481">For more information regarding the settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="e40b8-482">Consulte também [Suporte do SqlClient para a Alta Disponibilidade e a Recuperação de Desastre](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="e40b8-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="e40b8-483">Etapa 5: Configurações de quórum do cluster</span><span class="sxs-lookup"><span data-stu-id="e40b8-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="e40b8-484">Como vai retirar pelo menos um SQL Server de cada vez, você deverá modificar a configuração de quorum do cluster. Se estiver usando FSW (File Share Witness) com 2 nós, você deverá definir o quorum para permitir a maioria dos nós e utilizar votação dinâmica e isso tem o objetivo de permitir que um único nó fique de pé.</span><span class="sxs-lookup"><span data-stu-id="e40b8-484">As you are going to be taking out at least one SQL Server down at a time, you should modify the cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set the quorum to allow node majority and utilize dynamic voting, and this is to allow for a single node to remain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="e40b8-485">Para saber mais sobre como gerenciar e configurar o quorum de cluster, confira [Configurar e gerenciar o quorum em um cluster de failover do Windows Server 2012](https://technet.microsoft.com/library/jj612870.aspx).</span><span class="sxs-lookup"><span data-stu-id="e40b8-485">For more information on managing and configuring the cluster quorum, please see [Configure and Manage the Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="e40b8-486">Etapa 6: extrair ACLs e pontos de extremidade existentes</span><span class="sxs-lookup"><span data-stu-id="e40b8-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for the Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="e40b8-487">Salve-os em um arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="e40b8-487">Save these to a text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="e40b8-488">Etapa 7: alterar parceiros de failover e modos de replicação</span><span class="sxs-lookup"><span data-stu-id="e40b8-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="e40b8-489">Se tiver mais de dois SQL Servers, você deverá alterar o failover de outra secundário em outro DC ou local para 'Síncrono' e torná-lo um AFP (Parceiro de Failover Automático), de modo a manter a alta disponibilidade durante as alterações.</span><span class="sxs-lookup"><span data-stu-id="e40b8-489">If you have more than 2 SQL Servers, you should change the failover of another secondary in another DC or on-premises to ‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="e40b8-490">Você pode fazer isso por meio do TSQL ou modificar por SSMS:</span><span class="sxs-lookup"><span data-stu-id="e40b8-490">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="e40b8-492">Etapa 8: Remover a VM secundária do serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="e40b8-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="e40b8-493">Você deve estar planejando a migração de um nó secundário de nuvem primeiro. Se esse for o primário no momento, você deve iniciar um failover manual.</span><span class="sxs-lookup"><span data-stu-id="e40b8-493">You should be planning to migrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

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

    #Check disk config, make sure below returns the disks associated with the VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild to new cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="e40b8-494">Etapa 9: Alterar as configurações de caching de disco no arquivo CSV e salvar</span><span class="sxs-lookup"><span data-stu-id="e40b8-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="e40b8-495">Para volumes de dados, isso deve ser definido como READONLY.</span><span class="sxs-lookup"><span data-stu-id="e40b8-495">For data volumes these should be set to READONLY.</span></span>

<span data-ttu-id="e40b8-496">Para volumes TLOG, isso deve ser definido como NONE.</span><span class="sxs-lookup"><span data-stu-id="e40b8-496">For TLOG volumes these should be set to NONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="e40b8-498">Etapa 10: copiar VHDS</span><span class="sxs-lookup"><span data-stu-id="e40b8-498">Step 10: Copy VHDS</span></span>
    #Ensure you have created the container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy to Premium Storage accoun
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



<span data-ttu-id="e40b8-499">Você pode verificar o status da cópia dos VHDs à conta de Armazenamento Premium:</span><span class="sxs-lookup"><span data-stu-id="e40b8-499">You can check the copy status of the VHDs to the Premium Storage account:</span></span>

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

<span data-ttu-id="e40b8-501">Aguarde até que todos esses itens sejam registrados como êxito.</span><span class="sxs-lookup"><span data-stu-id="e40b8-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="e40b8-502">Para obter informações para blobs individuais:</span><span class="sxs-lookup"><span data-stu-id="e40b8-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="e40b8-503">Etapa 11: Registrar o disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="e40b8-503">Step 11: Register OS disk</span></span>
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

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="e40b8-504">Etapa 12: Importar a réplica secundária para o novo serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="e40b8-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="e40b8-505">O código a seguir também usa a opção adicional em que é possível importar a máquina e usar o VIP preservável.</span><span class="sxs-lookup"><span data-stu-id="e40b8-505">The code below also uses the added option here you can import the machine and use the retainable VIP.</span></span>

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember to change to XIO
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

    ###Attaching disks to a VM during a deploy to a new cloud service and new storage account is different from just attaching VHDs to just a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="e40b8-506">Etapa 13: criar ILB no novo Svc de nuvem, adicionar pontos de extremidade de carga balanceada e ACLs</span><span class="sxs-lookup"><span data-stu-id="e40b8-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
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

#### <a name="step-14-update-always-on"></a><span data-ttu-id="e40b8-507">Etapa 14: Atualizar AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="e40b8-507">Step 14: Update Always On</span></span>
    #Code to be executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # the azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency to Listener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

<span data-ttu-id="e40b8-509">Agora, remova o endereço IP do serviço de nuvem antigo.</span><span class="sxs-lookup"><span data-stu-id="e40b8-509">Now remove the old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="e40b8-511">Etapa 15: Verificar a atualização do DNS</span><span class="sxs-lookup"><span data-stu-id="e40b8-511">Step 15: DNS update check</span></span>
<span data-ttu-id="e40b8-512">Agora você deve verificar os servidores DNS em suas redes cliente do SQL Server e assegurar que o clustering adicionou o registro do host extra ao endereço IP adicionado.</span><span class="sxs-lookup"><span data-stu-id="e40b8-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added the extra host record for the added IP address.</span></span> <span data-ttu-id="e40b8-513">Se os servidores DNS não foram atualizados, considere forçar uma transferência de zona DNS e garanta que os clientes nessa sub-rede podem ser resolvidos para os dois endereços IP AlwaysOn. Isso ocorre para que você não precise aguardar a replicação automática de DNS.</span><span class="sxs-lookup"><span data-stu-id="e40b8-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that the clients in there subnet are able to resolve to both Always On IP Addresses, this is so you do not need to wait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="e40b8-514">Etapa 16: Reconfigurar o AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="e40b8-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="e40b8-515">Neste ponto, você aguarda o secundário para o qual o nó foi migrado ressincronizar-se totalmente com o nó local e mudar para o nó de replicação síncrona e torná-lo o AFP.</span><span class="sxs-lookup"><span data-stu-id="e40b8-515">At this point you wait for the secondary that node that was migrated to fully resynchronize with the on-premises node and switch to synchronous replication node and make it the AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="e40b8-516">Etapa 17: Migrar o segundo nó</span><span class="sxs-lookup"><span data-stu-id="e40b8-516">Step 17: Migrate second node</span></span>
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

    #Drop machine and rebuild to new cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="e40b8-517">Etapa 18: Alterar as configurações de caching de disco no arquivo CSV e salvar</span><span class="sxs-lookup"><span data-stu-id="e40b8-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="e40b8-518">Para volumes de dados, isso deve ser definido como READONLY.</span><span class="sxs-lookup"><span data-stu-id="e40b8-518">For data volumes these should be set to READONLY.</span></span>

<span data-ttu-id="e40b8-519">Para volumes TLOG, isso deve ser definido como NONE.</span><span class="sxs-lookup"><span data-stu-id="e40b8-519">For TLOG volumes these should be set to NONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="e40b8-521">Etapa 19: criar a nova conta de armazenamento independente para o nó secundário</span><span class="sxs-lookup"><span data-stu-id="e40b8-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset the storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="e40b8-522">Etapa 20: copiar VHDs</span><span class="sxs-lookup"><span data-stu-id="e40b8-522">Step 20: Copy VHDS</span></span>
    #Ensure you have created the container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy to Premium Storage accoun
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


<span data-ttu-id="e40b8-523">Você pode verificar o status da cópia VHD para todos os VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span><span class="sxs-lookup"><span data-stu-id="e40b8-523">You can check the VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="e40b8-525">Aguarde até que todos esses itens sejam registrados como êxito.</span><span class="sxs-lookup"><span data-stu-id="e40b8-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="e40b8-526">Para obter informações para blobs individuais:</span><span class="sxs-lookup"><span data-stu-id="e40b8-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="e40b8-527">Etapa 21: Registrar o disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="e40b8-527">Step 21: Register OS disk</span></span>
    #change storage account to the new XIO storage account
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

    #Join to existing Avaiability Set

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

    ###This is different to just a straight cloud service change
    #note if you do not have a disk label the command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="e40b8-528">Etapa 22: adicionar pontos de extremidade de carga balanceada e ACLs</span><span class="sxs-lookup"><span data-stu-id="e40b8-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in the Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="e40b8-529">Etapa 23: Failover de teste</span><span class="sxs-lookup"><span data-stu-id="e40b8-529">Step 23: Test failover</span></span>
<span data-ttu-id="e40b8-530">Agora, você deve deixar o nó migrado sincronizar-se ao nó migrado com o nó AlwaysOn local, colocá-lo no modo de replicação síncrona e aguardar sua sincronização.</span><span class="sxs-lookup"><span data-stu-id="e40b8-530">You should now let the migrated node synchronize with the on-premises Always On node, place it in to synchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="e40b8-531">Em seguida, execute o failover do local para o primeiro nó migrado, que é o AFP.</span><span class="sxs-lookup"><span data-stu-id="e40b8-531">Then failover from on-prem to the first node migrated, which is the AFP.</span></span> <span data-ttu-id="e40b8-532">Depois que isso funcionar, altere o último nó migrado para o AFP.</span><span class="sxs-lookup"><span data-stu-id="e40b8-532">Once that has worked, change the last migrated node to the AFP.</span></span>

<span data-ttu-id="e40b8-533">Você deve testar failovers entre todos os nós e executar testes de caos para garantir que os failovers funcionem como esperado e de modo oportuno.</span><span class="sxs-lookup"><span data-stu-id="e40b8-533">You should test failovers between all nodes and run though chaos tests to ensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="e40b8-534">Etapa 24: colocar de volta configurações de quorum de cluster / TTL DNS / Failover de impressoras / Configurações de sincronização</span><span class="sxs-lookup"><span data-stu-id="e40b8-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="e40b8-535">Adicionando recurso de endereço IP na mesma sub-rede</span><span class="sxs-lookup"><span data-stu-id="e40b8-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="e40b8-536">Se você tiver apenas dois SQL Servers e quiser migrá-los para um novo serviço de nuvem, mas quiser mantê-los na mesma sub-rede, poderá evitar colocar o ouvinte offline para excluir o endereço IP AlwaysOn original e adicionar o novo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="e40b8-536">If you have only 2 SQL Servers and want to migrate them to a new cloud service, but want to keep them on the same subnet, you can avoid taking the listener offline to delete the original Always On IP Address and add the New IP Address.</span></span> <span data-ttu-id="e40b8-537">Se você estiver migrando as VMs para outra sub-rede, não será necessário fazer isso, pois haverá uma rede de cluster adicional que fará referência a essa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="e40b8-537">If you are migrating the VMs to another subnet you will not need to do this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="e40b8-538">Depois que você ativar a réplica secundária migrada e adicionar o novo recurso de endereço IP ao novo serviço de nuvem antes de executar o failover da réplica primária existente, deverá executar essas etapas no Gerenciador de Cluster de Failover:</span><span class="sxs-lookup"><span data-stu-id="e40b8-538">Once you have brought up the migrated secondary and added in the new IP Address resource for the new cloud service before failover the existing Primary, you should take these steps within the Cluster Failover Manager:</span></span>

<span data-ttu-id="e40b8-539">Para adicionar o endereço IP, confira o [Apêndice](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), etapa 14.</span><span class="sxs-lookup"><span data-stu-id="e40b8-539">To add in IP Address, see the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="e40b8-540">Para obter o recurso de endereço IP atual, altere o possível proprietário para ‘SQL Server Primário Existente’, no exemplo abaixo, ‘dansqlams4’:</span><span class="sxs-lookup"><span data-stu-id="e40b8-540">For the current IP Address resource, change the possible owner to ‘Existing Primary SQL Server’, in the example below, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="e40b8-542">Para obter o novo recurso de endereço IP, altere o possível proprietário para ‘SQL Server secundário migrado’, no exemplo abaixo, ‘dansqlams5’:</span><span class="sxs-lookup"><span data-stu-id="e40b8-542">For the new IP Address resource, change the possible owner to ‘Migrated secondary SQL Server’, in the example below, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="e40b8-544">Depois que isso for definido, você poderá executar o failover e, quando o último nó for migrado, os Possíveis Proprietários deverão ser editados para que esse nó seja adicionado como um Proprietário Possível:</span><span class="sxs-lookup"><span data-stu-id="e40b8-544">Once this is set you can failover, and when the last node is migrated the Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="e40b8-546">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e40b8-546">Additional resources</span></span>
* [<span data-ttu-id="e40b8-547">Armazenamento Premium do Azure</span><span class="sxs-lookup"><span data-stu-id="e40b8-547">Azure Premium Storage</span></span>](../../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="e40b8-548">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="e40b8-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="e40b8-549">SQL Server nas Máquinas Virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="e40b8-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

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
