---
title: Azure Disk Encryption para VMs IaaS Windows e Linux | Microsoft Docs
description: "Este artigo fornece uma visão geral do Microsoft Azure Disk Encryption para VMs IaaS do Windows e Linux."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: a4f20fc19ae40561d042d5cff744a030014f75c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="4537f-103">Azure Disk Encryption para VMs IaaS Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="4537f-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="4537f-104">O Microsoft Azure tem o compromisso sério de garantir a privacidade e a soberania dos seus dados e permite que você controle os dados hospedados no Azure usando uma variedade de tecnologias para criptografar, controlar e gerenciar chaves de criptografia, bem como auditar e controlar o acesso aos dados.</span><span class="sxs-lookup"><span data-stu-id="4537f-104">Microsoft Azure is strongly committed to ensuring your data privacy, data sovereignty and enables you to control your Azure hosted data through a range of advanced technologies to encrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="4537f-105">Isso permite que os clientes do Azure tenham a flexibilidade de escolher a solução que melhor atenda às necessidades de negócios.</span><span class="sxs-lookup"><span data-stu-id="4537f-105">This provides Azure customers the flexibility to choose the solution that best meets their business needs.</span></span> <span data-ttu-id="4537f-106">Neste artigo, apresentaremos a você uma nova solução de tecnologia, "Azure Disk Encryption para VMs IaaS Windows e Linux" para ajudá-lo a proteger seus dados e atender às obrigações de conformidade e segurança da organização.</span><span class="sxs-lookup"><span data-stu-id="4537f-106">In this paper, we will introduce you to a new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” to help protect and safeguard your data to meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="4537f-107">O documento fornece orientações detalhadas sobre como usar os recursos de criptografia de disco do Azure, incluindo os cenários com suporte e as experiências de usuário.</span><span class="sxs-lookup"><span data-stu-id="4537f-107">The paper provides detailed guidance on how to use the Azure disk encryption features including the supported scenarios and the user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="4537f-108">Determinadas recomendações podem aumentar o uso de recursos de dados, rede ou computação, resultando em custos adicionais de licença ou inscrição.</span><span class="sxs-lookup"><span data-stu-id="4537f-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="4537f-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4537f-109">Overview</span></span>
<span data-ttu-id="4537f-110">o Azure Disk Encryption é um novo recurso que ajuda a criptografar os discos de suas máquinas virtuais IaaS Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="4537f-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="4537f-111">A Azure Disk Encryption aproveita o recurso padrão da indústria [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) do Windows e o recurso [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) do Linux para fornecer criptografia de volume para o SO e os discos de dados.</span><span class="sxs-lookup"><span data-stu-id="4537f-111">Azure Disk Encryption leverages the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux to provide volume encryption for the OS and the data disks.</span></span> <span data-ttu-id="4537f-112">A solução é integrada ao [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) para ajudá-lo a controlar e gerenciar as chaves de criptografia de disco e os segredos em sua assinatura de cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-112">The solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) to help you control and manage the disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="4537f-113">A solução também garante que todos os dados em discos da máquina virtual sejam criptografados em repouso no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4537f-113">The solution also ensures that all data on the virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="4537f-114">O Azure Disk Encryption para VMs IaaS do Windows e Linux agora está em **Disponibilidade Geral** em todas as regiões públicas do Azure e AzureGov para VMs Standard e VMs com armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="4537f-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="4537f-115">Cenários de criptografia</span><span class="sxs-lookup"><span data-stu-id="4537f-115">Encryption scenarios</span></span>
<span data-ttu-id="4537f-116">A solução Azure Disk Encryption dá suporte aos seguintes cenários do cliente:</span><span class="sxs-lookup"><span data-stu-id="4537f-116">The Azure Disk Encryption solution supports the following customer scenarios:</span></span>

* <span data-ttu-id="4537f-117">Habilitar a criptografia em novas VMs IaaS criadas com base em VHD pré-criptografado e chaves de criptografia</span><span class="sxs-lookup"><span data-stu-id="4537f-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="4537f-118">Habilitar criptografia em novas VMs de IaaS criadas a partir das imagens da Galeria do Azure com suporte</span><span class="sxs-lookup"><span data-stu-id="4537f-118">Enable encryption on new IaaS VMs created from the supported Azure Gallery images</span></span>
* <span data-ttu-id="4537f-119">Habilitar a criptografia em VMs IaaS existentes em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="4537f-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="4537f-120">Desabilitar a criptografia em VMs IaaS do Windows</span><span class="sxs-lookup"><span data-stu-id="4537f-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="4537f-121">Desabilitar a criptografia em unidades de dados para VMs IaaS do Linux</span><span class="sxs-lookup"><span data-stu-id="4537f-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="4537f-122">Ativar criptografia de VMs de disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="4537f-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="4537f-123">Atualizar configurações de criptografia de uma VM de armazenamento não premium criptografada existente</span><span class="sxs-lookup"><span data-stu-id="4537f-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="4537f-124">Backup e restauração de VMs criptografadas, criptografadas com chave de critografia de chave</span><span class="sxs-lookup"><span data-stu-id="4537f-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="4537f-125">A solução dá suporte aos seguintes cenários para VMs IaaS quando habilitados no Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="4537f-125">The solution supports the following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="4537f-126">Integração com o Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="4537f-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="4537f-127">VMs de camada padrão: [ A, D, DS, G, GS, F e VMs IaaS ](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="4537f-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="4537f-128">Habilitar criptografia em VMs de IaaS do Windows e Linux e VMs do disco gerenciado a partir das imagens da Galeria do Azure com suporte</span><span class="sxs-lookup"><span data-stu-id="4537f-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from the supported Azure Gallery images</span></span>
* <span data-ttu-id="4537f-129">Desativar criptografia no SO e nas unidades de dados para VMs da IaaS do Windows e VMs de disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="4537f-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="4537f-130">Desativar criptografia em unidades de dados para Linux Iaas VMs e VMs de disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="4537f-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="4537f-131">Habilitar a criptografia em VMs IaaS executando o sistema operacional Windows Client</span><span class="sxs-lookup"><span data-stu-id="4537f-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="4537f-132">Habilitar a criptografia em volumes com caminhos de montagem</span><span class="sxs-lookup"><span data-stu-id="4537f-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="4537f-133">Habilitar criptografia em VMs do Linux configuradas com disk striping (RAID) usando mdadm</span><span class="sxs-lookup"><span data-stu-id="4537f-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="4537f-134">Habilitar criptografia no Linux VMs utilizando LVM para discos de dados</span><span class="sxs-lookup"><span data-stu-id="4537f-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="4537f-135">Habilitar a criptografia em VMs do Windows configuradas com os Espaços de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="4537f-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="4537f-136">Atualizar configurações de criptografia de uma VM de armazenamento não premium criptografada existente</span><span class="sxs-lookup"><span data-stu-id="4537f-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="4537f-137">Para todas as regiões do Público do Azure e AzureGov há suporte</span><span class="sxs-lookup"><span data-stu-id="4537f-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="4537f-138">A solução não oferece suporte para seguintes cenários, recursos e tecnologia:</span><span class="sxs-lookup"><span data-stu-id="4537f-138">The solution does not support the following scenarios, features, and technology:</span></span>

* <span data-ttu-id="4537f-139">VMs IaaS da camada Básica</span><span class="sxs-lookup"><span data-stu-id="4537f-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="4537f-140">Como desabilitar a criptografia em unidades do sistema operacional para VMs IaaS do Linux</span><span class="sxs-lookup"><span data-stu-id="4537f-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="4537f-141">Desabilitar criptografia em uma unidade de dados se a unidade do SO estiver criptografada para VMs de IaaS do Linux</span><span class="sxs-lookup"><span data-stu-id="4537f-141">Disabling encryption on a data drive if the OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="4537f-142">VMs de IaaS que são criadas usando o método de criação de VM clássico</span><span class="sxs-lookup"><span data-stu-id="4537f-142">IaaS VMs that are created by using the classic VM creation method</span></span>
* <span data-ttu-id="4537f-143">Habilitar criptografia em imagens personalizadas do cliente de VMs de IaaS do Linux e Windows NÃO tem suporte.</span><span class="sxs-lookup"><span data-stu-id="4537f-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="4537f-144">Habilitar criptografia no disco do SO do LVM do Linux, atualmente não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="4537f-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="4537f-145">Este suporte será disponibilizado em breve.</span><span class="sxs-lookup"><span data-stu-id="4537f-145">This support will come soon.</span></span>
* <span data-ttu-id="4537f-146">Integração com o Serviço de Gerenciamento de Chaves no local</span><span class="sxs-lookup"><span data-stu-id="4537f-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="4537f-147">Arquivos do Azure (sistema de arquivos compartilhados), NFS (Network File System), volumes dinâmicos e VMs do Windows configuradas com Sistemas RAID baseados em software</span><span class="sxs-lookup"><span data-stu-id="4537f-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="4537f-148">Backup e restauração de VMs criptografadas, criptografadas com chave de criptografia de chave.</span><span class="sxs-lookup"><span data-stu-id="4537f-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="4537f-149">Atualize configurações de criptografia de um armazenamento VM existente criptografado premium.</span><span class="sxs-lookup"><span data-stu-id="4537f-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="4537f-150">O backup e a restauração de VMs criptografadas só têm suporte para VMs que são criptografadas com a configuração KEK.</span><span class="sxs-lookup"><span data-stu-id="4537f-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="4537f-151">Não há suporte em VMs que são criptografados sem KEK.</span><span class="sxs-lookup"><span data-stu-id="4537f-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="4537f-152">KEK é um parâmetro opcional que habilita a criptografia de VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="4537f-153">Esse suporte será oferecido em breve.</span><span class="sxs-lookup"><span data-stu-id="4537f-153">This support is coming soon.</span></span>
> <span data-ttu-id="4537f-154">Atualizar configurações de criptografia de uma VM de armazenamento não premium criptografada existente.</span><span class="sxs-lookup"><span data-stu-id="4537f-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="4537f-155">Esse suporte será oferecido em breve.</span><span class="sxs-lookup"><span data-stu-id="4537f-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="4537f-156">Recursos de criptografia</span><span class="sxs-lookup"><span data-stu-id="4537f-156">Encryption features</span></span>
<span data-ttu-id="4537f-157">Quando você habilita e a implanta o Azure Disk Encryption para VMs IaaS do Azure, os seguintes recursos são habilitados, dependendo da configuração fornecida:</span><span class="sxs-lookup"><span data-stu-id="4537f-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, the following capabilities are enabled, depending on the configuration provided:</span></span>

* <span data-ttu-id="4537f-158">Criptografia do volume do sistema operacional para proteger o volume de inicialização em repouso no armazenamento</span><span class="sxs-lookup"><span data-stu-id="4537f-158">Encryption of the OS volume to protect the boot volume at rest in your storage</span></span>
* <span data-ttu-id="4537f-159">Criptografia de volumes de dados para proteger os volumes de dados em repouso no armazenamento</span><span class="sxs-lookup"><span data-stu-id="4537f-159">Encryption of data volumes to protect the data volumes at rest in your storage</span></span>
* <span data-ttu-id="4537f-160">Como desabilitar a criptografia em unidades do sistema operacional e de dados para VMs IaaS do Windows</span><span class="sxs-lookup"><span data-stu-id="4537f-160">Disabling encryption on the OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="4537f-161">Desabilitar criptografia nas unidades de dados para VMs de IaaS do Linux (somente se a unidade do SO NÃO ESTIVER criptografada)</span><span class="sxs-lookup"><span data-stu-id="4537f-161">Disabling encryption on the data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="4537f-162">Proteger as chaves de criptografia e segredos em sua assinatura de cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="4537f-162">Safeguarding the encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="4537f-163">Comunicando o status de criptografia da VM IaaS criptografada</span><span class="sxs-lookup"><span data-stu-id="4537f-163">Reporting the encryption status of the encrypted IaaS VM</span></span>
* <span data-ttu-id="4537f-164">Remoção de definições de configuração de criptografia de disco da máquina virtual IaaS</span><span class="sxs-lookup"><span data-stu-id="4537f-164">Removal of disk-encryption configuration settings from the IaaS virtual machine</span></span>
* <span data-ttu-id="4537f-165">Backup e restauração de VMs criptografadas usando o serviço de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="4537f-165">Backup and restore of encrypted VMs by using the Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="4537f-166">O backup e a restauração de VMs criptografadas só têm suporte para VMs que são criptografadas com a configuração KEK.</span><span class="sxs-lookup"><span data-stu-id="4537f-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="4537f-167">Não há suporte em VMs que são criptografados sem KEK.</span><span class="sxs-lookup"><span data-stu-id="4537f-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="4537f-168">KEK é um parâmetro opcional que habilita a criptografia de VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="4537f-169">o Azure Disk Encryption para VMS IaaS para a solução Windows e Linux inclui:</span><span class="sxs-lookup"><span data-stu-id="4537f-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="4537f-170">A extensão de criptografia de disco para Windows.</span><span class="sxs-lookup"><span data-stu-id="4537f-170">The disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="4537f-171">A extensão de criptografia de disco para Linux.</span><span class="sxs-lookup"><span data-stu-id="4537f-171">The disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="4537f-172">Os cmdlets do PowerShell de criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="4537f-172">The disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="4537f-173">Os cmdlets da CLI (interface de linha de comando) do Azure para criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="4537f-173">The disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="4537f-174">Os modelos do Azure Resource Manager de criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="4537f-174">The disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="4537f-175">Há suporte para a solução de Azure Disk Encryption em VMs IaaS executando o Windows ou o sistema operacional Linux.</span><span class="sxs-lookup"><span data-stu-id="4537f-175">The Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="4537f-176">Para obter mais informações sobre os sistemas operacionais com suporte, confira a seção "Pré-requisitos".</span><span class="sxs-lookup"><span data-stu-id="4537f-176">For more information about the supported operating systems, see the "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="4537f-177">Não são cobradas taxas adicionais para a criptografia de discos de VM com o Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4537f-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="4537f-178">Proposta de valor</span><span class="sxs-lookup"><span data-stu-id="4537f-178">Value proposition</span></span>
<span data-ttu-id="4537f-179">Ao aplicar a solução de gerenciamento de Azure Disk Encryption, você pode atender às seguintes necessidades de negócios:</span><span class="sxs-lookup"><span data-stu-id="4537f-179">When you apply the Azure Disk Encryption-management solution, you can satisfy the following business needs:</span></span>

* <span data-ttu-id="4537f-180">As VMs IaaS ficam protegidas em repouso, pois você pode usar a tecnologia de criptografia padrão da indústria para tratar da segurança organizacional e de requisitos de conformidade.</span><span class="sxs-lookup"><span data-stu-id="4537f-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology to address organizational security and compliance requirements.</span></span>
* <span data-ttu-id="4537f-181">As VMs IaaS são inicializadas por meio de políticas e chaves controladas pelo cliente, e você pode auditar seu uso no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="4537f-182">Fluxo de trabalho de criptografia</span><span class="sxs-lookup"><span data-stu-id="4537f-182">Encryption workflow</span></span>
<span data-ttu-id="4537f-183">Para habilitar a criptografia de disco para VMs do Windows e Linux, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4537f-183">To enable disk encryption for Windows and Linux VMs, do the following:</span></span>

1. <span data-ttu-id="4537f-184">Escolha um cenário de criptografia entre os cenários de criptografia anteriores.</span><span class="sxs-lookup"><span data-stu-id="4537f-184">Choose an encryption scenario from among the preceding encryption scenarios.</span></span>
2. <span data-ttu-id="4537f-185">Opte por habilitar a criptografia de disco por meio do modelo do Gerenciador de Recursos de Azure Disk Encryption, cmdlets do PowerShell ou comando da CLI e especifique a configuração de criptografia.</span><span class="sxs-lookup"><span data-stu-id="4537f-185">Opt in to enabling disk encryption via the Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify the encryption configuration.</span></span>

   * <span data-ttu-id="4537f-186">Para o cenário do VHD criptografado pelo cliente, carregue o VHD criptografado para sua conta de armazenamento e o material de chave de criptografia para o cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-186">For the customer-encrypted VHD scenario, upload the encrypted VHD to your storage account and the encryption key material to your key vault.</span></span> <span data-ttu-id="4537f-187">Em seguida, forneça a configuração de criptografia para habilitar a criptografia em uma nova VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="4537f-187">Then, provide the encryption configuration to enable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="4537f-188">Para novas VMs que são criadas com base no Marketplace e VMs existentes que já estão em execução no Azure, forneça a configuração de criptografia para habilitar a criptografia na VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="4537f-188">For new VMs that are created from the Marketplace and existing VMs that are already running in Azure, provide the encryption configuration to enable encryption on the IaaS VM.</span></span>

3. <span data-ttu-id="4537f-189">Conceda acesso à plataforma Azure para ler o material de chave de criptografia (chaves de criptografia BitLocker para sistemas Windows e frase secreta para Linux) de seu cofre de chaves para habilitar a criptografia na VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="4537f-189">Grant access to the Azure platform to read the encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault to enable encryption on the IaaS VM.</span></span>

4. <span data-ttu-id="4537f-190">Forneça a identidade de aplicativo Azure AD (Azure Active Directory) para gravar o material de chave de criptografia no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-190">Provide the Azure Active Directory (Azure AD) application identity to write the encryption key material to your key vault.</span></span> <span data-ttu-id="4537f-191">Isso permite a criptografia na VM IaaS para os cenários mencionados na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="4537f-191">Doing so enables encryption on the IaaS VM for the scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="4537f-192">O Azure atualiza o modelo de serviço de VM com a configuração do cofre de chaves e a criptografia e define sua VM criptografada.</span><span class="sxs-lookup"><span data-stu-id="4537f-192">Azure updates the VM service model with encryption and the key vault configuration, and sets up your encrypted VM.</span></span>

 ![Microsoft Antimalware no Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="4537f-194">Fluxo de trabalho de descriptografia</span><span class="sxs-lookup"><span data-stu-id="4537f-194">Decryption workflow</span></span>
<span data-ttu-id="4537f-195">Para desabilitar a criptografia de disco para VMs IaaS, conclua as seguintes etapas de alto nível:</span><span class="sxs-lookup"><span data-stu-id="4537f-195">To disable disk encryption for IaaS VMs, complete the following high-level steps:</span></span>

1. <span data-ttu-id="4537f-196">Opte por desabilitar a criptografia (descriptografia) em uma VM IaaS em execução no Azure por meio do modelo do Resource Manager do Azure Disk Encryption ou de cmdlets do PowerShell e especifique a configuração da descriptografia.</span><span class="sxs-lookup"><span data-stu-id="4537f-196">Choose to disable encryption (decryption) on a running IaaS VM in Azure via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify the decryption configuration.</span></span>

 <span data-ttu-id="4537f-197">Esta etapa desabilitará a criptografia do sistema operacional ou o volume de dados ou ambos na VM IaaS do Windows em execução.</span><span class="sxs-lookup"><span data-stu-id="4537f-197">This step disables encryption of the OS or the data volume or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="4537f-198">No entanto, como mencionado na seção anterior, não há suporte para desabilitar a criptografia de disco do sistema operacional para Linux.</span><span class="sxs-lookup"><span data-stu-id="4537f-198">However, as mentioned in the previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="4537f-199">A etapa de descriptografia é permitida apenas para unidades de dados em VMs do Linux, desde que o disco do SO não esteja criptografado.</span><span class="sxs-lookup"><span data-stu-id="4537f-199">The decryption step is allowed only for data drives on Linux VMs as long as the OS disk is not encrypted.</span></span>
2. <span data-ttu-id="4537f-200">O Azure atualiza o modelo de serviço da VM e a VM IaaS é marcada como descriptografada.</span><span class="sxs-lookup"><span data-stu-id="4537f-200">Azure updates the VM service model, and the IaaS VM is marked decrypted.</span></span> <span data-ttu-id="4537f-201">O conteúdo da VM não está criptografado em repouso.</span><span class="sxs-lookup"><span data-stu-id="4537f-201">The contents of the VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="4537f-202">A operação de desabilitação da criptografia não exclui seu cofre de chaves nem o material da chave de criptografia (chaves de criptografia do BitLocker para sistemas Windows ou a Frase secreta para Linux).</span><span class="sxs-lookup"><span data-stu-id="4537f-202">The disable-encryption operation does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="4537f-203">Não há suporte para desativação de criptografia de disco de OS para Linux.</span><span class="sxs-lookup"><span data-stu-id="4537f-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="4537f-204">A etapa de descriptografia é permitida somente para unidades de dados em VMs Linux.</span><span class="sxs-lookup"><span data-stu-id="4537f-204">The decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="4537f-205">Desabilitar criptografia do disco de dados para Linux não tem suporte se a unidade do SO estiver criptografada.</span><span class="sxs-lookup"><span data-stu-id="4537f-205">Disabling data disk encryption for Linux is not supported if the OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4537f-206">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4537f-206">Prerequisites</span></span>
<span data-ttu-id="4537f-207">Antes de habilitar o Azure Disk Encryption em VMs IaaS do Azure para os cenários com suporte que foram discutidos na seção "Visão geral", confira os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="4537f-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for the supported scenarios that were discussed in the "Overview" section, see the following prerequisites:</span></span>

* <span data-ttu-id="4537f-208">Você deve ter uma assinatura ativa válida do Azure para criar recursos no Azure nas regiões com suporte.</span><span class="sxs-lookup"><span data-stu-id="4537f-208">You must have a valid active Azure subscription to create resources in Azure in the supported regions.</span></span>
* <span data-ttu-id="4537f-209">A Azure Disk Encryption tem suporte nas seguintes versões do Windows Server: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="4537f-209">Azure Disk Encryption is supported on the following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="4537f-210">O Azure Disk Encryption tem suporte nas seguintes versões de cliente Windows: cliente Windows 8 e cliente Windows 10.</span><span class="sxs-lookup"><span data-stu-id="4537f-210">Azure Disk Encryption is supported on the following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="4537f-211">Para o Windows Server 2008 R2, você deve ter o .NET Framework 4.5 instalado antes de habilitar a criptografia no Azure.</span><span class="sxs-lookup"><span data-stu-id="4537f-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="4537f-212">Você pode instalá-lo com o Windows Update, instalando a atualização opcional Microsoft .NET Framework 4.5.2 para sistemas Windows Server 2008 R2 baseados em x64 ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="4537f-212">You can install it from Windows Update by installing the optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="4537f-213">O Azure Disk Encryption tem suporte nas seguintes versões e distribuições do servidor Linux baseado na Galeria do Azure:</span><span class="sxs-lookup"><span data-stu-id="4537f-213">Azure Disk Encryption is supported on the following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="4537f-214">Distribuição Linux</span><span class="sxs-lookup"><span data-stu-id="4537f-214">Linux Distribution</span></span> | <span data-ttu-id="4537f-215">Versão</span><span class="sxs-lookup"><span data-stu-id="4537f-215">Version</span></span> | <span data-ttu-id="4537f-216">Tipo de Volume com Suporte para Criptografia</span><span class="sxs-lookup"><span data-stu-id="4537f-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="4537f-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4537f-217">Ubuntu</span></span> | <span data-ttu-id="4537f-218">16.04-LTS-DIÁRIO</span><span class="sxs-lookup"><span data-stu-id="4537f-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="4537f-219">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="4537f-219">OS and Data disk</span></span> |
| <span data-ttu-id="4537f-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4537f-220">Ubuntu</span></span> | <span data-ttu-id="4537f-221">14.04.5-LTS-DIÁRIO</span><span class="sxs-lookup"><span data-stu-id="4537f-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="4537f-222">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="4537f-222">OS and Data disk</span></span> |
| <span data-ttu-id="4537f-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4537f-223">Ubuntu</span></span> | <span data-ttu-id="4537f-224">12.10</span><span class="sxs-lookup"><span data-stu-id="4537f-224">12.10</span></span> | <span data-ttu-id="4537f-225">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4537f-225">Data disk</span></span> |
| <span data-ttu-id="4537f-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4537f-226">Ubuntu</span></span> | <span data-ttu-id="4537f-227">12.04</span><span class="sxs-lookup"><span data-stu-id="4537f-227">12.04</span></span> | <span data-ttu-id="4537f-228">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4537f-228">Data disk</span></span> |
| <span data-ttu-id="4537f-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="4537f-229">RHEL</span></span> | <span data-ttu-id="4537f-230">7.3</span><span class="sxs-lookup"><span data-stu-id="4537f-230">7.3</span></span> | <span data-ttu-id="4537f-231">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="4537f-231">OS and Data disk</span></span> |
| <span data-ttu-id="4537f-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="4537f-232">RHEL</span></span> | <span data-ttu-id="4537f-233">7,2</span><span class="sxs-lookup"><span data-stu-id="4537f-233">7.2</span></span> | <span data-ttu-id="4537f-234">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="4537f-234">OS and Data disk</span></span> |
| <span data-ttu-id="4537f-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="4537f-235">RHEL</span></span> | <span data-ttu-id="4537f-236">6,8</span><span class="sxs-lookup"><span data-stu-id="4537f-236">6.8</span></span> | <span data-ttu-id="4537f-237">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="4537f-237">OS and Data disk</span></span> |
| <span data-ttu-id="4537f-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="4537f-238">RHEL</span></span> | <span data-ttu-id="4537f-239">6.7</span><span class="sxs-lookup"><span data-stu-id="4537f-239">6.7</span></span> | <span data-ttu-id="4537f-240">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4537f-240">Data disk</span></span> |
| <span data-ttu-id="4537f-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="4537f-241">CentOS</span></span> | <span data-ttu-id="4537f-242">7.3</span><span class="sxs-lookup"><span data-stu-id="4537f-242">7.3</span></span> | <span data-ttu-id="4537f-243">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="4537f-243">OS and Data disk</span></span> |
| <span data-ttu-id="4537f-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="4537f-244">CentOS</span></span> | <span data-ttu-id="4537f-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="4537f-245">7.2n</span></span> | <span data-ttu-id="4537f-246">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="4537f-246">OS and Data disk</span></span> |
| <span data-ttu-id="4537f-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="4537f-247">CentOS</span></span> | <span data-ttu-id="4537f-248">6,8</span><span class="sxs-lookup"><span data-stu-id="4537f-248">6.8</span></span> | <span data-ttu-id="4537f-249">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="4537f-249">OS and Data disk</span></span> |
| <span data-ttu-id="4537f-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="4537f-250">CentOS</span></span> | <span data-ttu-id="4537f-251">7.1</span><span class="sxs-lookup"><span data-stu-id="4537f-251">7.1</span></span> | <span data-ttu-id="4537f-252">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4537f-252">Data disk</span></span> |
| <span data-ttu-id="4537f-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="4537f-253">CentOS</span></span> | <span data-ttu-id="4537f-254">7.0</span><span class="sxs-lookup"><span data-stu-id="4537f-254">7.0</span></span> | <span data-ttu-id="4537f-255">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4537f-255">Data disk</span></span> |
| <span data-ttu-id="4537f-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="4537f-256">CentOS</span></span> | <span data-ttu-id="4537f-257">6.7</span><span class="sxs-lookup"><span data-stu-id="4537f-257">6.7</span></span> | <span data-ttu-id="4537f-258">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4537f-258">Data disk</span></span> |
| <span data-ttu-id="4537f-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="4537f-259">CentOS</span></span> | <span data-ttu-id="4537f-260">6.6</span><span class="sxs-lookup"><span data-stu-id="4537f-260">6.6</span></span> | <span data-ttu-id="4537f-261">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4537f-261">Data disk</span></span> |
| <span data-ttu-id="4537f-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="4537f-262">CentOS</span></span> | <span data-ttu-id="4537f-263">6.5</span><span class="sxs-lookup"><span data-stu-id="4537f-263">6.5</span></span> | <span data-ttu-id="4537f-264">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4537f-264">Data disk</span></span> |
| <span data-ttu-id="4537f-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="4537f-265">openSUSE</span></span> | <span data-ttu-id="4537f-266">13.2</span><span class="sxs-lookup"><span data-stu-id="4537f-266">13.2</span></span> | <span data-ttu-id="4537f-267">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4537f-267">Data disk</span></span> |
| <span data-ttu-id="4537f-268">SLES</span><span class="sxs-lookup"><span data-stu-id="4537f-268">SLES</span></span> | <span data-ttu-id="4537f-269">12 SP1</span><span class="sxs-lookup"><span data-stu-id="4537f-269">12 SP1</span></span> | <span data-ttu-id="4537f-270">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4537f-270">Data disk</span></span> |
| <span data-ttu-id="4537f-271">SLES</span><span class="sxs-lookup"><span data-stu-id="4537f-271">SLES</span></span> | <span data-ttu-id="4537f-272">12-SP1 (Premium)</span><span class="sxs-lookup"><span data-stu-id="4537f-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="4537f-273">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4537f-273">Data disk</span></span> |
| <span data-ttu-id="4537f-274">SLES</span><span class="sxs-lookup"><span data-stu-id="4537f-274">SLES</span></span> | <span data-ttu-id="4537f-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="4537f-275">HPC 12</span></span> | <span data-ttu-id="4537f-276">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4537f-276">Data disk</span></span> |
| <span data-ttu-id="4537f-277">SLES</span><span class="sxs-lookup"><span data-stu-id="4537f-277">SLES</span></span> | <span data-ttu-id="4537f-278">11-SP4 (Premium)</span><span class="sxs-lookup"><span data-stu-id="4537f-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="4537f-279">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4537f-279">Data disk</span></span> |
| <span data-ttu-id="4537f-280">SLES</span><span class="sxs-lookup"><span data-stu-id="4537f-280">SLES</span></span> | <span data-ttu-id="4537f-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="4537f-281">11 SP4</span></span> | <span data-ttu-id="4537f-282">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="4537f-282">Data disk</span></span> |

* <span data-ttu-id="4537f-283">O Azure Disk Encryption exige que seu cofre de chaves e as VMs residam na mesma região e assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="4537f-283">Azure Disk Encryption requires that your key vault and VMs reside in the same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="4537f-284">Configurá os recursos em regiões separadas causa uma falha na habilitação do recurso de Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4537f-284">Configuring the resources in separate regions causes a failure in enabling the Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="4537f-285">Para instalar e configurar o cofre de chaves para o Azure Disk Encryption, consulte a seção **Definir e configurar o cofre de chaves para o Azure Disk Encryption** na seção *Pré-requisitos* deste artigo.</span><span class="sxs-lookup"><span data-stu-id="4537f-285">To set up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="4537f-286">Para instalar e configurar o aplicativo Azure AD no Azure Active Directory para Azure Disk Encryption, consulte a seção **Configurar o aplicativo Azure AD no Azure Active Directory** na seção de *Pré-requisitos* deste artigo.</span><span class="sxs-lookup"><span data-stu-id="4537f-286">To set up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up the Azure AD application in Azure Active Directory** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="4537f-287">Para instalar e configurar a política de acesso do cofre de chaves para o aplicativo Azure AD, consulte a seção **Configurando a política de acesso ao cofre de chaves para o aplicativo Azure AD** na seção de *Pré-requisitos* deste artigo.</span><span class="sxs-lookup"><span data-stu-id="4537f-287">To set up and configure the key vault access policy for the Azure AD application, see section **Set up the key vault access policy for the Azure AD application** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="4537f-288">Para preparar um VHD do Windows criptografado previamente, consulte a seção  **Preparar um VHD do Windows criptografado previamente**  no  *Apêndice* .</span><span class="sxs-lookup"><span data-stu-id="4537f-288">To prepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="4537f-289">Para preparar um VHD do Linux criptografado previamente, consulte a seção  **Preparar um VHD do Linux criptografado previamente**  no  *Apêndice* .</span><span class="sxs-lookup"><span data-stu-id="4537f-289">To prepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="4537f-290">A plataforma Azure precisa acessar as chaves de criptografia ou os segredos no cofre de chaves para torná-los disponíveis para a máquina virtual quando ela for inicializada e descriptografar o volume de sistema operacional da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4537f-290">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the virtual machine when it boots and decrypts the virtual machine OS volume.</span></span> <span data-ttu-id="4537f-291">Para conceder permissões para a plataforma Windows Azure, defina a propriedade **EnabledForDiskEncryption** no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-291">To grant permissions to Azure platform, set the **EnabledForDiskEncryption** property in the key vault.</span></span> <span data-ttu-id="4537f-292">Para obter mais infprmações, consulte **Definir e configurar o cofre de chaves de Azure Disk Encryption** no Apêndice.</span><span class="sxs-lookup"><span data-stu-id="4537f-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in the Appendix.</span></span>
* <span data-ttu-id="4537f-293">O segredo do cofre de chaves e as URLs KEK devem ter controle de versão.</span><span class="sxs-lookup"><span data-stu-id="4537f-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="4537f-294">O Azure impõe essa restrição de controle de versão.</span><span class="sxs-lookup"><span data-stu-id="4537f-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="4537f-295">Para um segredo válido e URLs KEK, confira os seguintes exemplos:</span><span class="sxs-lookup"><span data-stu-id="4537f-295">For valid secret and KEK URLs, see the following examples:</span></span>

  * <span data-ttu-id="4537f-296">Exemplo de URL de segredo válida: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="4537f-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="4537f-297">Exemplo de URL KEK válida: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="4537f-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="4537f-298">o Azure Disk Encryption não dá suporte à especificação de números de portas como parte de segredos do cofre de chaves e URLs KEK.</span><span class="sxs-lookup"><span data-stu-id="4537f-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="4537f-299">Para exemplos de URLs do Key Vault com e sem suporte, consulte:</span><span class="sxs-lookup"><span data-stu-id="4537f-299">For examples of non-supported and supported key vault URLs, see the following:</span></span>

  * <span data-ttu-id="4537f-300">URL do cofre de chaves inaceitável *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="4537f-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="4537f-301">URL do cofre de chaves aceitável: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="4537f-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="4537f-302">Para habilitar o recurso de Azure Disk Encryption, as VMs IaaS devem atender aos seguintes requisitos de configuração do ponto de extremidade de rede:</span><span class="sxs-lookup"><span data-stu-id="4537f-302">To enable the Azure Disk Encryption feature, the IaaS VMs must meet the following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="4537f-303">Para obter um token para se conectar ao seu cofre de chaves, a VM IaaS deve ser capaz de se conectar a um ponto de extremidade do Azure Active Directory, \[login.microsoftonline.com\].</span><span class="sxs-lookup"><span data-stu-id="4537f-303">To get a token to connect to your key vault, the IaaS VM must be able to connect to an Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="4537f-304">Para gravar as chaves de criptografia no cofre de chaves, a VM IaaS deve ser capaz de se conectar ao ponto de extremidade do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-304">To write the encryption keys to your key vault, the IaaS VM must be able to connect to the key vault endpoint.</span></span>
  * <span data-ttu-id="4537f-305">A VM IaaS deve ser capaz de se conectar a um ponto de extremidade do armazenamento do Azure que hospeda o repositório de extensão do Azure e uma conta de armazenamento do Azure que hospeda os arquivos VHD.</span><span class="sxs-lookup"><span data-stu-id="4537f-305">The IaaS VM must be able to connect to an Azure storage endpoint that hosts the Azure extension repository and an Azure storage account that hosts the VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="4537f-306">Se a política de segurança limita o acesso de VMs do Azure à Internet, você pode resolver o URI anterior e configurar uma regra específica para permitir a conectividade de saída para os IPs.</span><span class="sxs-lookup"><span data-stu-id="4537f-306">If your security policy limits access from Azure VMs to the Internet, you can resolve the preceding URI and configure a specific rule to allow outbound connectivity to the IPs.</span></span>
  >
  ><span data-ttu-id="4537f-307">Para configurar e acessar Azure Key Vault protegido por um firewall (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="4537f-307">To configure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="4537f-308">Use a versão mais recente do SDK do Azure PowerShell para configurar o Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4537f-308">Use the latest version of Azure PowerShell SDK version to configure Azure Disk Encryption.</span></span> <span data-ttu-id="4537f-309">Baixe a última versão do [Azure PowerShell](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="4537f-309">Download the latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="4537f-310">Não há suporte para o Azure Disk Encryption no [SDK do Azure PowerShell versão 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span><span class="sxs-lookup"><span data-stu-id="4537f-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="4537f-311">Se estiver recebendo um erro relacionado ao uso do PowerShell 1.1.0, confira [Erro do Azure Disk Encryption relacionado ao Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span><span class="sxs-lookup"><span data-stu-id="4537f-311">If you are receiving an error related to using Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related to Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="4537f-312">Para executar qualquer comando da CLI do Azure e associá-lo à sua assinatura do Azure, primeiro você deve instalar a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="4537f-312">To run any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="4537f-313">Para instalar a CLI do Azure e associá-la à sua assinatura do Azure, confira [Como instalar e configurar a CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4537f-313">To install Azure CLI and associate it with your Azure subscription, see [How to install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="4537f-314">Para usar a CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager, confira [Comandos da CLI do Azure no modo do Gerenciador de Recursos](../virtual-machines/azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="4537f-314">To use Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="4537f-315">Ao criptografar um disco gerenciado, é um pré-requisito obrigatório tirar um instantâneo do disco gerenciado ou então fazer um backup do disco fora do Azure Disk Encryption antes de habilitar a criptografia.</span><span class="sxs-lookup"><span data-stu-id="4537f-315">When encrypting a managed disk, it is mandatory prerequisite to take a snapshot of the managed disk or a backup of the disk outside of Azure Disk Encryption prior to enabling encryption.</span></span>  <span data-ttu-id="4537f-316">Sem um backup em vigor, qualquer falha inesperada durante a criptografia pode tornar o disco e a VM inacessíveis e sem uma opção de recuperação.</span><span class="sxs-lookup"><span data-stu-id="4537f-316">Without a backup in place, any unexpected failure during encryption may render the disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="4537f-317">Set-AzureRmVMDiskEncryptionExtension atualmente não faz backup de Managed Disks e gerará um erro se usado em um disco gerenciado, a menos que o parâmetro -skipVmBackup tenha sido especificado.</span><span class="sxs-lookup"><span data-stu-id="4537f-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless the -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="4537f-318">O uso desse parâmetro não é seguro, a menos que um backup já tenha sido feito fora do Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4537f-318">This parameter is unsafe to use unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="4537f-319">Quando o parâmetro -skipVmBackup é especificado, o cmdlet não faz um backup do disco gerenciado antes da criptografia.</span><span class="sxs-lookup"><span data-stu-id="4537f-319">When the -skipVmBackup parameter is specified, the cmdlet will not make a backup of the managed disk prior to encryption.</span></span>  <span data-ttu-id="4537f-320">Por esse motivo, ele é considerado um pré-requisito obrigatório para verificar se de um backup da VM com disco gerenciado está em vigor antes de habilitar o Azure Disk Encryption, caso uma recuperação posterior seja necessária.</span><span class="sxs-lookup"><span data-stu-id="4537f-320">For this reason, it is considered a mandatory prerequisite to make sure a backup of the managed disk VM is in place prior to enabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="4537f-321">O parâmetro -skipVmBackup nunca deve ser usado, a menos que um instantâneo ou backup já tenham sido feitos fora do Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4537f-321">The -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="4537f-322">A solução de Azure Disk Encryption usa o protetor de chave externa BitLocker para VMs IaaS do Windows.</span><span class="sxs-lookup"><span data-stu-id="4537f-322">The Azure Disk Encryption solution uses the BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="4537f-323">Para VMs ingressadas no domínio, NÃO envie nenhuma política de grupo que imponha protetores de TPM.</span><span class="sxs-lookup"><span data-stu-id="4537f-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="4537f-324">Para obter informações sobre a política de grupo "Permitir BitLocker sem um TPM compatível", confira [Referência de política de grupo do BitLocker](https://technet.microsoft.com/library/ee706521).</span><span class="sxs-lookup"><span data-stu-id="4537f-324">For information about the group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="4537f-325">A política do BitLocker para máquinas virtuais ingressadas no domínio com a política de grupo personalizado deve incluir a seguinte configuração: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` o Azure Disk Encryption falhará quando as configurações de política de grupo personalizadas para o Bitlocker forem incompatíveis.</span><span class="sxs-lookup"><span data-stu-id="4537f-325">Bitlocker policy on domain joined virtual machines with custom group policy must include the following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="4537f-326">Em computadores que não tinham a configuração de política correta, pode ser necessário aplicar a nova política, forçar a atualização da nova política (gpupdate.exe /force) e, em seguida, reiniciar.</span><span class="sxs-lookup"><span data-stu-id="4537f-326">On machines that did not have the correct policy setting, applying the new policy, forcing the new policy to update (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="4537f-327">Para criar um aplicativo Azure AD, criar um cofre de chaves ou configurar um cofre de chaves existente e habilitar a criptografia, confira o [script do PowerShell de pré-requisito de Azure Disk Encryption](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span><span class="sxs-lookup"><span data-stu-id="4537f-327">To create an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see the [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="4537f-328">Para configurar os pré-requisitos de criptografia de disco usando a CLI do Azure, confira [este script Bash](https://github.com/ejarvi/ade-cli-getting-started).</span><span class="sxs-lookup"><span data-stu-id="4537f-328">To configure disk-encryption prerequisites using the Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="4537f-329">Para usar o serviço de Backup do Azure para fazer backup e restaurar VMs criptografadas quando a criptografia estiver habilitada com o Azure Disk Encryption, criptografe as VMs usando a configuração da chave de Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4537f-329">To use the Azure Backup service to back up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using the Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="4537f-330">O serviço de Backup dá suporte a VMs que são criptografadas usando apenas a configuração KEK.</span><span class="sxs-lookup"><span data-stu-id="4537f-330">The Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="4537f-331">Consulte [Como fazer backup e restaurar máquinas virtuais criptografadas com criptografia do Backup do Azure ](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span><span class="sxs-lookup"><span data-stu-id="4537f-331">See [How to back up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="4537f-332">Ao criptografar um volume do sistema operacional Linux, observe que atualmente uma reinicialização de VM é necessária no final do processo.</span><span class="sxs-lookup"><span data-stu-id="4537f-332">When encrypting a Linux OS volume, note that a VM restart is currently required at the end of the process.</span></span> <span data-ttu-id="4537f-333">Isso pode ser feito por meio do portal, do PowerShell ou da CLI.</span><span class="sxs-lookup"><span data-stu-id="4537f-333">This can be done via the portal, powershell, or CLI.</span></span>   <span data-ttu-id="4537f-334">Para acompanhar o progresso de criptografia, sonde periodicamente a mensagem de status retornada por Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span><span class="sxs-lookup"><span data-stu-id="4537f-334">To track the progress of encryption, periodically poll the status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="4537f-335">Uma vez concluída a criptografia, a mensagem de status retornada por este comando indicará isso.</span><span class="sxs-lookup"><span data-stu-id="4537f-335">Once encryption is complete, the the status message returned by this command will indicate this.</span></span>  <span data-ttu-id="4537f-336">Por exemplo, "ProgressMessage: disco do sistema operacional criptografado com êxito, reinicialize a VM", Nesse ponto, a VM pode ser reiniciada e usada.</span><span class="sxs-lookup"><span data-stu-id="4537f-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot the VM"  At this point the VM can be restarted and used.</span></span>  

* <span data-ttu-id="4537f-337">O Azure Disk Encryption para Linux requer que os discos de dados tenham um sistema de arquivos montado em Linux antes da criptografia</span><span class="sxs-lookup"><span data-stu-id="4537f-337">Azure Disk Encryption for Linux requires data disks to have a mounted file system in Linux prior to encryption</span></span>

* <span data-ttu-id="4537f-338">Discos de dados montados recursivamente não têm suporte pelo Azure Disk Encryption para Linux.</span><span class="sxs-lookup"><span data-stu-id="4537f-338">Recursively mounted data disks are not supported by the Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="4537f-339">Por exemplo, se o sistema de destino tiver montado um disco em foo/bar e, em seguida, outro em /foo/bar/baz, a criptografia de /foo/bar/baz terá êxito, mas haverá falha na criptografia de foo/bar.</span><span class="sxs-lookup"><span data-stu-id="4537f-339">For example, if the target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, the encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="4537f-340">Somente haverá suporte para o Azure Disk Encryption nas imagens com suporte da galeria do Azure que atenderem aos pré-requisitos acima mencionados.</span><span class="sxs-lookup"><span data-stu-id="4537f-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet the aforementioned prerequisites.</span></span> <span data-ttu-id="4537f-341">Imagens personalizadas do cliente não têm suporte devido a esquemas de partição personalizados e comportamentos de processo que podem existir nessas imagens.</span><span class="sxs-lookup"><span data-stu-id="4537f-341">Customer custom images are not supported due to custom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="4537f-342">Além disso, até mesmo VMs baseadas em imagem de galeria que inicialmente atendiam aos pré-requisitos, mas que foram modificadas após a criação, podem ser incompatíveis.</span><span class="sxs-lookup"><span data-stu-id="4537f-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="4537f-343">Por esse motivo, o procedimento sugerido para criptografar uma VM Linux é iniciar de uma imagem da galeria limpa, criptografar a VM e, em seguida, adicionar software personalizado ou dados à VM conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="4537f-343">For that reason, the suggested procedure for encrypting a Linux VM is to start from a clean gallery image, encrypt the VM, and then add custom software or data to the VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="4537f-344">O backup e a restauração de VMs criptografadas só têm suporte para VMs que são criptografadas com a configuração KEK.</span><span class="sxs-lookup"><span data-stu-id="4537f-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="4537f-345">Não há suporte em VMs que são criptografados sem KEK.</span><span class="sxs-lookup"><span data-stu-id="4537f-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="4537f-346">KEK é um parâmetro opcional que permite VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-the-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="4537f-347">Configurar o aplicativo Azure AD no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4537f-347">Set up the Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="4537f-348">Quando você precisa habilitar a criptografia em uma VM em execução no Azure, o Azure Disk Encryption gera e grava as chaves de criptografia no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-348">When you need encryption to be enabled on a running VM in Azure, Azure Disk Encryption generates and writes the encryption keys to your key vault.</span></span> <span data-ttu-id="4537f-349">O gerenciamento de chaves de criptografia no cofre de chaves requer a autenticação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4537f-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="4537f-350">Para essa finalidade, crie um aplicativo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4537f-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="4537f-351">Você pode encontrar etapas detalhadas para registrar um aplicativo na seção "Obter uma identidade para o aplicativo" da postagem de blog [Azure Key Vault - passo a passo](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="4537f-351">You can find detailed steps for registering an application in the “Get an Identity for the Application” section of the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="4537f-352">Esta postagem também contém vários exemplos úteis para configurar o cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="4537f-353">Para fins de autenticação, você pode usar a autenticação baseada em segredo do cliente ou a autenticação Azure AD baseada em certificado do cliente.</span><span class="sxs-lookup"><span data-stu-id="4537f-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="4537f-354">Autenticação do Azure AD baseada em segredo do cliente</span><span class="sxs-lookup"><span data-stu-id="4537f-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="4537f-355">As seções a seguir podem ajudá-lo a configurar uma autenticação baseada em segredo do cliente para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4537f-355">The sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="4537f-356">Criar um aplicativo Azure AD usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4537f-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="4537f-357">Use o seguinte cmdlet do PowerShell para criar um aplicativo Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4537f-357">Use the following PowerShell cmdlet to create an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="4537f-358">$azureAdApplication.ApplicationId é o ClientID do Azure AD e $aadClientSecret é o segredo do cliente que deve ser usado posteriormente para habilitar o Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4537f-358">$azureAdApplication.ApplicationId is the Azure AD ClientID and $aadClientSecret is the client secret that you should use later to enable Azure Disk Encryption.</span></span> <span data-ttu-id="4537f-359">Proteja adequadamente o segredo do cliente no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4537f-359">Safeguard the Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-the-azure-ad-client-id-and-secret-from-the-azure-classic-portal"></a><span data-ttu-id="4537f-360">Configurando a ID do cliente do Azure AD e o segredo do portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="4537f-360">Setting up the Azure AD client ID and secret from the Azure classic portal</span></span>
<span data-ttu-id="4537f-361">Você também pode configurar a ID de cliente do Azure AD e o segredo usando o [portal clássico do Azure]( https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4537f-361">You can also set up your Azure AD client ID and secret by using the [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="4537f-362">Para executar essa tarefa, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4537f-362">To perform this task, do the following:</span></span>

1. <span data-ttu-id="4537f-363">Clique na guia **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4537f-363">Click the **Active Directory** tab.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="4537f-365">Clique em **Adicionar Aplicativo** e digite o nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4537f-365">Click **Add Application**, and then type the application name.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="4537f-367">Clique no botão de seta e configure as propriedades do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4537f-367">Click the arrow button, and then configure the application properties.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="4537f-369">Clique na marca de seleção no canto inferior esquerdo para concluir.</span><span class="sxs-lookup"><span data-stu-id="4537f-369">Click the check mark in the lower left corner to finish.</span></span> <span data-ttu-id="4537f-370">A página de configuração de aplicativo é exibida, e a ID de cliente do Azure AD é exibida na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="4537f-370">The application configuration page appears, and the Azure AD client ID is displayed at the bottom of the page.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="4537f-372">5. Salve o segredo do cliente do Azure AD clicando no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4537f-372">Save the Azure AD client secret by clicking the **Save** button.</span></span> <span data-ttu-id="4537f-373">Observe o segredo do cliente do Azure AD na caixa de texto de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-373">Note the Azure AD client secret in the keys text box.</span></span> <span data-ttu-id="4537f-374">Proteja-o adequadamente.</span><span class="sxs-lookup"><span data-stu-id="4537f-374">Safeguard it appropriately.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="4537f-376">O fluxo anterior não tem suporte no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="4537f-376">The preceding flow is not supported on the Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="4537f-377">Usar um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="4537f-377">Use an existing application</span></span>
<span data-ttu-id="4537f-378">Para executar os seguintes comandos, obtenha e use o [módulo do Azure AD PowerShell](https://technet.microsoft.com/library/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="4537f-378">To execute the following commands, obtain and use the [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="4537f-379">Os comandos a seguir devem ser executados em uma nova janela do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4537f-379">The following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="4537f-380">Não use o Azure PowerShell ou a janela do Azure Resource Manager para executar os comandos.</span><span class="sxs-lookup"><span data-stu-id="4537f-380">Do not use Azure PowerShell or the Azure Resource Manager window to execute the commands.</span></span> <span data-ttu-id="4537f-381">Recomendamos essa abordagem porque esses cmdlets estão no módulo MSOnline ou no Azure PowerShell AD.</span><span class="sxs-lookup"><span data-stu-id="4537f-381">We recommend this approach because these cmdlets are in the MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="4537f-382">Autenticação baseada em certificado do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4537f-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="4537f-383">No momento, não há suporte para a autenticação baseada em certificado do Azure AD em VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="4537f-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="4537f-384">As seções a seguir mostram como configurar uma autenticação baseada em certificado para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4537f-384">The sections that follow show how to configure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="4537f-385">Criar um aplicativo Azure AD</span><span class="sxs-lookup"><span data-stu-id="4537f-385">Create an Azure AD application</span></span>
<span data-ttu-id="4537f-386">Para criar um aplicativo Azure AD, execute os seguintes cmdlets do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4537f-386">To create an Azure AD application, execute the following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="4537f-387">Substitua a cadeia de caracteres `yourpassword` a seguir por sua senha segura e proteja a senha.</span><span class="sxs-lookup"><span data-stu-id="4537f-387">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="4537f-388">Depois de concluir essa etapa, carregue um arquivo PFX no cofre de chaves e habilite a política de acesso necessária para implantar esse certificado em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4537f-388">After you finish this step, upload a PFX file to your key vault and enable the access policy needed to deploy that certificate to a VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="4537f-389">Usar um aplicativo existente do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4537f-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="4537f-390">Se estiver configurando a autenticação baseada em certificado para um aplicativo existente, use os cmdlets do PowerShell mostrados aqui.</span><span class="sxs-lookup"><span data-stu-id="4537f-390">If you are configuring certificate-based authentication for an existing application, use the PowerShell cmdlets shown here.</span></span> <span data-ttu-id="4537f-391">Execute-os em uma nova janela do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4537f-391">Be sure to execute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="4537f-392">Depois de concluir esta etapa, carregue um arquivo PFX para o cofre de chaves e habilite a política de acesso necessária para implantar o certificado em uma VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-392">After you finish this step, upload a PFX file to your key vault and enable the access policy that's needed to deploy the certificate to a VM.</span></span>

##### <a name="upload-a-pfx-file-to-your-key-vault"></a><span data-ttu-id="4537f-393">Carregar um arquivo PFX no cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="4537f-393">Upload a PFX file to your key vault</span></span>
<span data-ttu-id="4537f-394">Para obter uma explicação detalhada desse processo, confira o [Blog oficial da equipe do Azure Key Vault](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span><span class="sxs-lookup"><span data-stu-id="4537f-394">For a detailed explanation of this process, see [The Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="4537f-395">No entanto, os seguintes cmdlets do PowerShell são tudo de que você precisa para a tarefa.</span><span class="sxs-lookup"><span data-stu-id="4537f-395">However, the following PowerShell cmdlets are all you need for the task.</span></span> <span data-ttu-id="4537f-396">Execute-os no console do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4537f-396">Be sure to execute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="4537f-397">Substitua a cadeia de caracteres `yourpassword` a seguir por sua senha segura e proteja a senha.</span><span class="sxs-lookup"><span data-stu-id="4537f-397">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-to-an-existing-vm"></a><span data-ttu-id="4537f-398">Implante um certificado no cofre de chaves em uma VM existente</span><span class="sxs-lookup"><span data-stu-id="4537f-398">Deploy a certificate in your key vault to an existing VM</span></span>
<span data-ttu-id="4537f-399">Depois de terminar de carregar o PFX, implante um certificado no cofre de chaves em uma VM existente com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4537f-399">After you finish uploading the PFX, deploy a certificate in the key vault to an existing VM with the following:</span></span>
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-the-key-vault-access-policy-for-the-azure-ad-application"></a><span data-ttu-id="4537f-400">Configurar a política de acesso do cofre de chaves para o aplicativo Azure AD</span><span class="sxs-lookup"><span data-stu-id="4537f-400">Set up the key vault access policy for the Azure AD application</span></span>
<span data-ttu-id="4537f-401">Seu aplicativo Azure AD precisa de direitos para acessar as chaves ou os segredos no cofre.</span><span class="sxs-lookup"><span data-stu-id="4537f-401">Your Azure AD application needs rights to access the keys or secrets in the vault.</span></span> <span data-ttu-id="4537f-402">Use o cmdlet [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) para conceder permissões para o aplicativo usando a ID do cliente (que foi gerada quando o aplicativo foi registrado) como o valor do parâmetro _–ServicePrincipalName_.</span><span class="sxs-lookup"><span data-stu-id="4537f-402">Use the [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet to grant permissions to the application, using the client ID (which was generated when the application was registered) as the _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="4537f-403">Para saber mais, confira a postagem de blog [Azure Key Vault - passo a passo](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="4537f-403">To learn more, see the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="4537f-404">Aqui está um exemplo de como executar essa tarefa por meio do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4537f-404">Here is an example of how to perform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="4537f-405">o Azure Disk Encryption exige que você configure as seguintes políticas de acesso ao aplicativo de cliente do Azure AD: permissões _WrapKey_ e _Set_.</span><span class="sxs-lookup"><span data-stu-id="4537f-405">Azure Disk Encryption requires you to configure the following access policies to your Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="4537f-406">Terminologia</span><span class="sxs-lookup"><span data-stu-id="4537f-406">Terminology</span></span>
<span data-ttu-id="4537f-407">Para entender alguns dos termos comuns usados por essa tecnologia, use a seguinte tabela de terminologia:</span><span class="sxs-lookup"><span data-stu-id="4537f-407">To understand some of the common terms used by this technology, use the following terminology table:</span></span>

| <span data-ttu-id="4537f-408">Terminologia</span><span class="sxs-lookup"><span data-stu-id="4537f-408">Terminology</span></span> | <span data-ttu-id="4537f-409">Definição</span><span class="sxs-lookup"><span data-stu-id="4537f-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="4537f-410">AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4537f-410">Azure AD</span></span> | <span data-ttu-id="4537f-411">Azure AD significa [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="4537f-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="4537f-412">Uma conta do Azure AD é um pré-requisito para autenticar, armazenar e recuperar segredos do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="4537f-413">Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="4537f-413">Azure Key Vault</span></span> | <span data-ttu-id="4537f-414">O Key Vault é um serviço de gerenciamento de chaves criptográfico baseado em módulos de segurança de hardware validados pelo FIPS (Federal Information Processing Standards), que ajuda a proteger as chaves criptográficas e os segredos confidenciais.</span><span class="sxs-lookup"><span data-stu-id="4537f-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="4537f-415">Para obter mais informações, confira a documentação do [Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="4537f-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="4537f-416">ARM</span><span class="sxs-lookup"><span data-stu-id="4537f-416">ARM</span></span> | <span data-ttu-id="4537f-417">Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="4537f-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="4537f-418">BitLocker</span><span class="sxs-lookup"><span data-stu-id="4537f-418">BitLocker</span></span> |<span data-ttu-id="4537f-419">O [BitLocker](https://technet.microsoft.com/library/hh831713.aspx) é uma tecnologia de criptografia de volume do Windows reconhecida pela indústria e usada para habilitar a criptografia de disco em VMs de IaaS do Windows.</span><span class="sxs-lookup"><span data-stu-id="4537f-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used to enable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="4537f-420">BEK</span><span class="sxs-lookup"><span data-stu-id="4537f-420">BEK</span></span> | <span data-ttu-id="4537f-421">As chaves de criptografia do BitLocker são usadas para criptografar o volume de inicialização do sistema operacional e os volumes de dados.</span><span class="sxs-lookup"><span data-stu-id="4537f-421">BitLocker encryption keys are used to encrypt the OS boot volume and data volumes.</span></span> <span data-ttu-id="4537f-422">As chaves do BitLocker são protegidas em um cofre de chaves como segredos.</span><span class="sxs-lookup"><span data-stu-id="4537f-422">The BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="4537f-423">CLI</span><span class="sxs-lookup"><span data-stu-id="4537f-423">CLI</span></span> | <span data-ttu-id="4537f-424">Confira [Interface de linha de comando do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4537f-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="4537f-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="4537f-425">DM-Crypt</span></span> |<span data-ttu-id="4537f-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) é o subsistema de criptografia de disco transparente baseado em Linux usado para habilitar a criptografia de disco nas VMs de IaaS do Linux.</span><span class="sxs-lookup"><span data-stu-id="4537f-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is the Linux-based, transparent disk-encryption subsystem that's used to enable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="4537f-427">KEK</span><span class="sxs-lookup"><span data-stu-id="4537f-427">KEK</span></span> | <span data-ttu-id="4537f-428">A criptografia de chave é a chave assimétrica (RSA 2048) que pode ser usada para proteger ou encapsular o segredo.</span><span class="sxs-lookup"><span data-stu-id="4537f-428">Key encryption key is the asymmetric key (RSA 2048) that you can use to protect or wrap the secret.</span></span> <span data-ttu-id="4537f-429">Você pode fornecer uma chave protegida por HSM (módulos de segurança de hardware) ou uma chave protegida por software.</span><span class="sxs-lookup"><span data-stu-id="4537f-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="4537f-430">Para obter mais detalhes, confira a [documentação do Azure Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="4537f-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="4537f-431">Cmdlets de DNS</span><span class="sxs-lookup"><span data-stu-id="4537f-431">PS cmdlets</span></span> | <span data-ttu-id="4537f-432">Confira [Cmdlets do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4537f-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="4537f-433">Instalar e configurar o cofre de chaves de Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="4537f-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="4537f-434">o Azure Disk Encryption ajuda a proteger as chaves e os segredos da criptografia de disco no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-434">Azure Disk Encryption helps safeguard the disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="4537f-435">Para configurar o cofre de chaves para o Azure Disk Encryption, conclua as etapas em cada uma das seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="4537f-435">To set up your key vault for Azure Disk Encryption, complete the steps in each of the following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="4537f-436">Criar um cofre de chave</span><span class="sxs-lookup"><span data-stu-id="4537f-436">Create a key vault</span></span>
<span data-ttu-id="4537f-437">Para criar um cofre de chaves, use uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="4537f-437">To create a key vault, use one of the following options:</span></span>

* [<span data-ttu-id="4537f-438">Modelo "101-Key-Vault-Create" do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4537f-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="4537f-439">Cmdlets do cofre de chaves do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4537f-439">Azure PowerShell key vault cmdlets</span></span>](/powershell/module/azurerm.keyvault/#key_vault)
* <span data-ttu-id="4537f-440">Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="4537f-440">Azure Resource Manager</span></span>
* <span data-ttu-id="4537f-441">Como [ Proteger o key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="4537f-441">How to [Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="4537f-442">Se já tiver configurado um cofre de chaves para sua assinatura, vá para a próxima seção.</span><span class="sxs-lookup"><span data-stu-id="4537f-442">If you have already set up a key vault for your subscription, skip to the next section.</span></span>

![Cofre da Chave do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="4537f-444">Configurar uma chave de criptografia de chave (opcional)</span><span class="sxs-lookup"><span data-stu-id="4537f-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="4537f-445">Se quiser usar um KEK para uma camada adicional de segurança para as chaves de criptografia do BitLocker, adicione o KEK ao cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-445">If you want to use a KEK for an additional layer of security for the BitLocker encryption keys, add a KEK to your key vault.</span></span> <span data-ttu-id="4537f-446">Use o cmdlet [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) para criar uma chave de criptografia de chave no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-446">Use the [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet to create a key encryption key in the key vault.</span></span> <span data-ttu-id="4537f-447">Você também pode importar a KEK do HSM do gerenciamento de chaves local.</span><span class="sxs-lookup"><span data-stu-id="4537f-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="4537f-448">Para obter mais detalhes, confira a [Documentação do Key Vault](https://azure.microsoft.com/documentation/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="4537f-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="4537f-449">Você pode adicionar o KEK indo para o Azure Resource Manager ou usando a interface do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-449">You can add the KEK by going to Azure Resource Manager or by using your key vault interface.</span></span>

![Cofre da Chave do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="4537f-451">Definir permissões de cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="4537f-451">Set key vault permissions</span></span>
<span data-ttu-id="4537f-452">A plataforma Azure precisa acessar as chaves de criptografia ou os segredos no cofre de chaves para disponibilizá-los para a máquina virtual para inicialização e descriptografar os volumes.</span><span class="sxs-lookup"><span data-stu-id="4537f-452">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the VM for booting and decrypting the volumes.</span></span> <span data-ttu-id="4537f-453">Para conceder permissões para a plataforma Windows Azure, defina a propriedade **EnabledForDiskEncryption** no cofre de chaves usando o cmdlet do PowerShell do cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="4537f-453">To grant permissions to the Azure platform, set the **EnabledForDiskEncryption** property in the key vault by using the key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="4537f-454">Você também pode definir a propriedade **EnabledForDiskEncryption** acessando o [Explorador de Recursos do Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4537f-454">You can also set the **EnabledForDiskEncryption** property by visiting the [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="4537f-455">Como mencionado anteriormente, você deve definir a propriedade **EnabledForDiskEncryption** em seu cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-455">As mentioned earlier, you must set the **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="4537f-456">Caso contrário, a implantação falhará.</span><span class="sxs-lookup"><span data-stu-id="4537f-456">Otherwise, the deployment will fail.</span></span>

<span data-ttu-id="4537f-457">Você pode configurar políticas de acesso para o aplicativo Azure AD na interface do cofre de chaves, como mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="4537f-457">You can set up access policies for your Azure AD application from the key vault interface, as shown here:</span></span>

![Cofre da Chave do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Cofre da Chave do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="4537f-460">Na guia **Políticas de acesso avançado**, verifique se o cofre de chaves está habilitado para o Azure Disk Encryption:</span><span class="sxs-lookup"><span data-stu-id="4537f-460">On the **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Cofre de chaves do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="4537f-462">Cenários de implantação de criptografia de disco e experiências de usuário</span><span class="sxs-lookup"><span data-stu-id="4537f-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="4537f-463">Você pode habilitar muitos cenários de criptografia de disco, e as etapas podem variar de acordo com o cenário.</span><span class="sxs-lookup"><span data-stu-id="4537f-463">You can enable many disk-encryption scenarios, and the steps may vary according to the scenario.</span></span> <span data-ttu-id="4537f-464">As seções a seguir abordam os cenários mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="4537f-464">The following sections cover the scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-the-marketplace"></a><span data-ttu-id="4537f-465">Habilitar a criptografia em novas VMs IaaS criadas por meio do Marketplace</span><span class="sxs-lookup"><span data-stu-id="4537f-465">Enable encryption on new IaaS VMs that are created from the Marketplace</span></span>
<span data-ttu-id="4537f-466">Você pode habilitar a criptografia de disco em uma nova VM IaaS Windows por meio do Marketplace no Azure usando o [modelo do Gerenciador de Recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span><span class="sxs-lookup"><span data-stu-id="4537f-466">You can enable disk encryption on new IaaS Windows VM from the Marketplace in Azure by using the  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="4537f-467">No modelo de início rápido do Azure, clique em **Implantar no Azure**, insira a configuração de criptografia na folha **Parâmetros** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4537f-467">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="4537f-468">Selecione a assinatura, o grupo de recursos, o local do grupo de recursos, os termos legais e o contrato e clique em **Criar** para habilitar a criptografia na VM IaaS nova.</span><span class="sxs-lookup"><span data-stu-id="4537f-468">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="4537f-469">Esse modelo cria uma nova VM do Windows criptografada que usa a imagem de galeria do Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="4537f-469">This template creates a new encrypted Windows VM that uses the Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="4537f-470">Você pode habilitar a criptografia de disco em uma nova VM IaaS do RedHat Linux 7.2 com uma matriz RAID 0 de 200 GB usando esse [modelo do Gerenciador de Recursos](https://aka.ms/fde-rhel).</span><span class="sxs-lookup"><span data-stu-id="4537f-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="4537f-471">Após implantar o modelo, verifique o status de criptografia da VM usando o cmdlet `Get-AzureRmVmDiskEncryptionStatus`, conforme descrito em [Criptografando unidade do SO em uma VM do Linux em execução](#encrypting-os-drive-on-a-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="4537f-471">After you deploy the template, verify the VM encryption status by using the `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="4537f-472">Quando o computador retornar um status _VMRestartPending_, reinicie a VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-472">When the machine returns a status of _VMRestartPending_, restart the VM.</span></span>

<span data-ttu-id="4537f-473">A tabela a seguir lista os parâmetros de modelo do Gerenciador de Recursos para novas VMs do cenário do Marketplace usando a ID de cliente do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4537f-473">The following table lists the Resource Manager template parameters for new VMs from the Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="4537f-474">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="4537f-474">Parameter</span></span> | <span data-ttu-id="4537f-475">Descrição</span><span class="sxs-lookup"><span data-stu-id="4537f-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4537f-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="4537f-476">adminUserName</span></span> | <span data-ttu-id="4537f-477">Especifique um nome de usuário para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4537f-477">Admin user name for the virtual machine.</span></span> |
| <span data-ttu-id="4537f-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="4537f-478">adminPassword</span></span> | <span data-ttu-id="4537f-479">Senha de usuário administrador para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4537f-479">Admin user password for the virtual machine.</span></span> |
| <span data-ttu-id="4537f-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="4537f-480">newStorageAccountName</span></span> | <span data-ttu-id="4537f-481">Nome da conta de armazenamento para armazenar VHDs do sistema operacional e de dados.</span><span class="sxs-lookup"><span data-stu-id="4537f-481">Name of the storage account to store OS and data VHDs.</span></span> |
| <span data-ttu-id="4537f-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="4537f-482">vmSize</span></span> | <span data-ttu-id="4537f-483">O tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-483">Size of the VM.</span></span> <span data-ttu-id="4537f-484">Atualmente, há suporte somente para séries Standard A, D e G.</span><span class="sxs-lookup"><span data-stu-id="4537f-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="4537f-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="4537f-485">virtualNetworkName</span></span> | <span data-ttu-id="4537f-486">Nome da VNet à qual a NIC da VM deve pertencer.</span><span class="sxs-lookup"><span data-stu-id="4537f-486">Name of the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="4537f-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="4537f-487">subnetName</span></span> | <span data-ttu-id="4537f-488">Nome da sub-rede na VNet à qual a NIC da VM deve pertencer.</span><span class="sxs-lookup"><span data-stu-id="4537f-488">Name of the subnet in the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="4537f-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="4537f-489">AADClientID</span></span> | <span data-ttu-id="4537f-490">A ID do cliente do aplicativo Azure AD que tem permissões para gravar segredos no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-490">Client ID of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="4537f-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="4537f-491">AADClientSecret</span></span> | <span data-ttu-id="4537f-492">Segredo do cliente do aplicativo AD do Azure que tem permissões para gravar segredos para o cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-492">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="4537f-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="4537f-493">keyVaultURL</span></span> | <span data-ttu-id="4537f-494">URL do cofre de chaves no qual a chave do BitLocker deve ser carregada.</span><span class="sxs-lookup"><span data-stu-id="4537f-494">URL of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="4537f-495">Você pode obtê-lo usando o cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span><span class="sxs-lookup"><span data-stu-id="4537f-495">You can get it by using the cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="4537f-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="4537f-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="4537f-497">URL da chave de criptografia de chave que é usada para criptografar a chave gerada do BitLocker (opcional).</span><span class="sxs-lookup"><span data-stu-id="4537f-497">URL of the key encryption key that's used to encrypt the generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="4537f-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4537f-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="4537f-499">Grupo de recursos do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-499">Resource group of the key vault.</span></span> |
| <span data-ttu-id="4537f-500">vmName</span><span class="sxs-lookup"><span data-stu-id="4537f-500">vmName</span></span> | <span data-ttu-id="4537f-501">Nome da VM em que a operação de criptografia deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="4537f-501">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="4537f-502">_KeyEncryptionKeyURL_ é um parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="4537f-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="4537f-503">Você pode usar seu próprio KEK para proteger ainda mais a chave de criptografia de dados (frase secreta) no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-503">You can bring your own KEK to further safeguard the data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="4537f-504">Habilite a criptografia na nova VM IaaS criada usando VHD criptografado pelo cliente e chaves de criptografia</span><span class="sxs-lookup"><span data-stu-id="4537f-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="4537f-505">Nesse cenário, você pode habilitar a criptografia usando o modelo do Resource Manager, cmdlets do PowerShell ou comandos da CLI.</span><span class="sxs-lookup"><span data-stu-id="4537f-505">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="4537f-506">As seções a seguir explicam detalhadamente o modelo do Gerenciador de Recursos e comandos da CLI.</span><span class="sxs-lookup"><span data-stu-id="4537f-506">The following sections explain in greater detail the Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="4537f-507">Siga as instruções em uma dessas seções para preparar as imagens pré-criptografadas que podem ser usadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="4537f-507">Follow the instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="4537f-508">Depois que a imagem for criada, você poderá usar as etapas na próxima seção para criar uma VM do Azure criptografada.</span><span class="sxs-lookup"><span data-stu-id="4537f-508">After the image is created, you can use the steps in the next section to create an encrypted Azure VM.</span></span>

* [<span data-ttu-id="4537f-509">Preparar um VHD do Windows previamente criptografado</span><span class="sxs-lookup"><span data-stu-id="4537f-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="4537f-510">Preparar um VHD Linux previamente criptografado</span><span class="sxs-lookup"><span data-stu-id="4537f-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="4537f-511">Usando o modelo do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="4537f-511">Using the Resource Manager template</span></span>
<span data-ttu-id="4537f-512">Você pode habilitar a criptografia de disco em seu VHD criptografado usando o [modelo do Gerenciador de Recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span><span class="sxs-lookup"><span data-stu-id="4537f-512">You can enable disk encryption on your encrypted VHD by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="4537f-513">No modelo de início rápido do Azure, clique em **Implantar no Azure**, insira a configuração de criptografia na folha **Parâmetros** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4537f-513">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="4537f-514">Selecione a assinatura, o grupo de recursos, o local do grupo de recursos, os termos legais e o contrato e clique no botão **Criar** para habilitar a criptografia na VM IaaS nova.</span><span class="sxs-lookup"><span data-stu-id="4537f-514">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the new IaaS VM.</span></span>

<span data-ttu-id="4537f-515">A tabela a seguir lista os parâmetros de modelo do Gerenciador de Recursos para seu VHD criptografado:</span><span class="sxs-lookup"><span data-stu-id="4537f-515">The following table lists the Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="4537f-516">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="4537f-516">Parameter</span></span> | <span data-ttu-id="4537f-517">Descrição</span><span class="sxs-lookup"><span data-stu-id="4537f-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4537f-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="4537f-518">newStorageAccountName</span></span> | <span data-ttu-id="4537f-519">Nome da conta de armazenamento para armazenar o VHD de sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="4537f-519">Name of the storage account to store the encrypted OS VHD.</span></span> <span data-ttu-id="4537f-520">Esta conta de armazenamento já deve ter sido criada no mesmo grupo de recursos e no mesmo local da VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-520">This storage account should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="4537f-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="4537f-521">osVhdUri</span></span> | <span data-ttu-id="4537f-522">URI do VHD do sistema operacional da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4537f-522">URI of the OS VHD from the storage account.</span></span> |
| <span data-ttu-id="4537f-523">osType</span><span class="sxs-lookup"><span data-stu-id="4537f-523">osType</span></span> | <span data-ttu-id="4537f-524">Tipo de produto do sistema operacional (Windows/Linux).</span><span class="sxs-lookup"><span data-stu-id="4537f-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="4537f-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="4537f-525">virtualNetworkName</span></span> | <span data-ttu-id="4537f-526">Nome da VNet à qual a NIC da VM deve pertencer.</span><span class="sxs-lookup"><span data-stu-id="4537f-526">Name of the VNet that the VM NIC should belong to.</span></span> <span data-ttu-id="4537f-527">O nome já deve ter sido criado no mesmo grupo de recursos e no mesmo local que a VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-527">The name should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="4537f-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="4537f-528">subnetName</span></span> | <span data-ttu-id="4537f-529">O nome da sub-rede na VNet à qual a VM NIC deve pertencer.</span><span class="sxs-lookup"><span data-stu-id="4537f-529">Name of the subnet on the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="4537f-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="4537f-530">vmSize</span></span> | <span data-ttu-id="4537f-531">O tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-531">Size of the VM.</span></span> <span data-ttu-id="4537f-532">Atualmente, há suporte somente para séries Standard A, D e G.</span><span class="sxs-lookup"><span data-stu-id="4537f-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="4537f-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="4537f-533">keyVaultResourceID</span></span> | <span data-ttu-id="4537f-534">O ResourceID que identifica o recurso de cofre de chaves no Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4537f-534">The ResourceID that identifies the key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="4537f-535">Você pode obtê-lo usando o cmdlet do PowerShell `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span><span class="sxs-lookup"><span data-stu-id="4537f-535">You can get it by using the PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="4537f-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="4537f-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="4537f-537">URL da chave de criptografia de disco que é configurada no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-537">URL of the disk-encryption key that's set up in the key vault.</span></span> |
| <span data-ttu-id="4537f-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="4537f-538">keyVaultKekUrl</span></span> | <span data-ttu-id="4537f-539">URL da chave de criptografia de chave para criptografar a chave de criptografia de disco gerada.</span><span class="sxs-lookup"><span data-stu-id="4537f-539">URL of the key encryption key for encrypting the generated disk-encryption key.</span></span> |
| <span data-ttu-id="4537f-540">vmName</span><span class="sxs-lookup"><span data-stu-id="4537f-540">vmName</span></span> | <span data-ttu-id="4537f-541">Nome da VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="4537f-541">Name of the IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="4537f-542">Usando os cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="4537f-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="4537f-543">Você pode habilitar a criptografia de disco em seu VHD criptografado usando o cmdlet do PowerShell [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="4537f-543">You can enable disk encryption on your encrypted VHD by using the PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="4537f-544">Usando comandos da CLI</span><span class="sxs-lookup"><span data-stu-id="4537f-544">Using CLI commands</span></span>
<span data-ttu-id="4537f-545">Para habilitar a criptografia de disco para esse cenário usando os comandos da CLI, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4537f-545">To enable disk encryption for this scenario by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="4537f-546">Definir políticas de acesso no cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="4537f-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="4537f-547">Defina o sinalizador **EnabledForDiskEncryption**:</span><span class="sxs-lookup"><span data-stu-id="4537f-547">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="4537f-548">Defina permissões para o aplicativo Azure AD para gravar segredos no cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="4537f-548">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="4537f-549">Para habilitar a criptografia em uma VM existente/em execução, digite:</span><span class="sxs-lookup"><span data-stu-id="4537f-549">To enable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="4537f-550">Obtenha o status de criptografia:</span><span class="sxs-lookup"><span data-stu-id="4537f-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="4537f-551">Para habilitar a criptografia em uma nova VM de seu VHD criptografado, use os seguintes parâmetros com o comando `azure vm create`:</span><span class="sxs-lookup"><span data-stu-id="4537f-551">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="4537f-552">Habilitar a criptografia na VM IaaS do Windows existente ou em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="4537f-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="4537f-553">Nesse cenário, você pode habilitar a criptografia usando o modelo do Resource Manager, cmdlets do PowerShell ou comandos da CLI.</span><span class="sxs-lookup"><span data-stu-id="4537f-553">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="4537f-554">As seções a seguir explicam detalhadamente como habilitá-lo usando o modelo do Gerenciador de Recursos e comandos da CLI.</span><span class="sxs-lookup"><span data-stu-id="4537f-554">The following sections explain in greater detail how to enable it by using the Resource Manager template and CLI commands.</span></span>

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="4537f-555">Usando o modelo do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="4537f-555">Using the Resource Manager template</span></span>
<span data-ttu-id="4537f-556">Você pode habilitar a criptografia de disco em VMs Windows IaaS existentes ou em execução no Azure usando o [modelo do Gerenciador de Recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="4537f-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="4537f-557">No modelo de início rápido do Azure, clique em **Implantar no Azure**, insira a configuração de criptografia na folha **Parâmetros** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4537f-557">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="4537f-558">Selecione a assinatura, o grupo de recursos, o local do grupo de recursos, os termos legais e o contrato e clique em **Criar** para habilitar a criptografia em VM IaaS existente ou em execução.</span><span class="sxs-lookup"><span data-stu-id="4537f-558">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="4537f-559">A tabela a seguir lista os parâmetros de modelo do Gerenciador de Recursos existente ou VMs em execução que usam uma ID de cliente do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4537f-559">The following table lists the Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="4537f-560">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="4537f-560">Parameter</span></span> | <span data-ttu-id="4537f-561">Descrição</span><span class="sxs-lookup"><span data-stu-id="4537f-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4537f-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="4537f-562">AADClientID</span></span> | <span data-ttu-id="4537f-563">ID do cliente do aplicativo Azure AD que tem permissões para gravar segredos no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-563">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="4537f-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="4537f-564">AADClientSecret</span></span> | <span data-ttu-id="4537f-565">Segredo do cliente do aplicativo Azure AD que tem permissões para gravar segredos no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-565">Client secret of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="4537f-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="4537f-566">keyVaultName</span></span> | <span data-ttu-id="4537f-567">Nome do cofre de chaves no qual a chave do BitLocker deve ser carregada.</span><span class="sxs-lookup"><span data-stu-id="4537f-567">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="4537f-568">Você pode obtê-lo usando o cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="4537f-568">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="4537f-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="4537f-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="4537f-570">URL da chave de criptografia de chaves que é usada para criptografar a chave gerada do BitLocker.</span><span class="sxs-lookup"><span data-stu-id="4537f-570">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="4537f-571">Esse parâmetro será opcional se você selecionar **nokek** na lista suspensa UseExistingKek.</span><span class="sxs-lookup"><span data-stu-id="4537f-571">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="4537f-572">Se selecionar **kek** na lista suspensa UseExistingKek, você deverá inserir o valor _keyEncryptionKeyURL_.</span><span class="sxs-lookup"><span data-stu-id="4537f-572">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="4537f-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="4537f-573">volumeType</span></span> | <span data-ttu-id="4537f-574">Tipo de volume em que a operação de criptografia é executada.</span><span class="sxs-lookup"><span data-stu-id="4537f-574">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="4537f-575">Os valores válidos são _OS_, _Data_ e _All_.</span><span class="sxs-lookup"><span data-stu-id="4537f-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="4537f-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="4537f-576">sequenceVersion</span></span> | <span data-ttu-id="4537f-577">Versão de sequência da operação de BitLocker.</span><span class="sxs-lookup"><span data-stu-id="4537f-577">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="4537f-578">Aumente esse número de versão sempre que uma operação de criptografia de disco for executada na mesma VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-578">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="4537f-579">vmName</span><span class="sxs-lookup"><span data-stu-id="4537f-579">vmName</span></span> | <span data-ttu-id="4537f-580">Nome da VM em que a operação de criptografia deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="4537f-580">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="4537f-581">_KeyEncryptionKeyURL_ é um parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="4537f-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="4537f-582">Você pode usar seu próprio KEK para proteger ainda mais a chave de criptografia de dados (segredo de criptografia BitLocker) no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-582">You can bring your own KEK to further safeguard the data encryption key (BitLocker encryption secret) in the key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="4537f-583">Usando os cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="4537f-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="4537f-584">Para obter informações sobre como habilitar a criptografia com o Azure Disk Encryption usando cmdlets do PowerShell, confira as postagens de blog [Explorar Azure Disk Encryption com o Azure PowerShell - parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) e [Explorar Azure Disk Encryption com o Azure PowerShell - parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="4537f-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="4537f-585">Usando comandos da CLI</span><span class="sxs-lookup"><span data-stu-id="4537f-585">Using CLI commands</span></span>
<span data-ttu-id="4537f-586">Para habilitar a criptografia em uma VM IaaS do Windows existente ou em execução no Azure usando os comandos da CLI, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4537f-586">To enable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do the following:</span></span>

1. <span data-ttu-id="4537f-587">Para definir políticas de acesso no cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="4537f-587">To set access policies in the key vault:</span></span>
   * <span data-ttu-id="4537f-588">Defina o sinalizador **EnabledForDiskEncryption**:</span><span class="sxs-lookup"><span data-stu-id="4537f-588">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="4537f-589">Defina permissões para o aplicativo Azure AD para gravar segredos no cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="4537f-589">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="4537f-590">Para habilitar a criptografia em uma VM existente ou em execução:</span><span class="sxs-lookup"><span data-stu-id="4537f-590">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="4537f-591">Para obter o status de criptografia:</span><span class="sxs-lookup"><span data-stu-id="4537f-591">To get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="4537f-592">Para habilitar a criptografia em uma nova VM de seu VHD criptografado, use os seguintes parâmetros com o comando `azure vm create`:</span><span class="sxs-lookup"><span data-stu-id="4537f-592">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="4537f-593">Habilitar a criptografia em uma VM IaaS do Linux existente ou em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="4537f-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="4537f-594">Você pode habilitar a criptografia de disco em uma VM Linux IaaS existente ou em execução no Azure usando o [modelo do Gerenciador de Recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="4537f-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="4537f-595">Clique em **Implantar no Azure** no modelo de início rápido do Azure, insira a configuração de criptografia na folha **Parâmetros** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4537f-595">Click **Deploy to Azure** on the Azure quick-start template, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="4537f-596">Selecione a assinatura, o grupo de recursos, o local do grupo de recursos, os termos legais e o contrato e clique em **Criar** para habilitar a criptografia em VM IaaS existente ou em execução.</span><span class="sxs-lookup"><span data-stu-id="4537f-596">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="4537f-597">A tabela a seguir lista os parâmetros de modelo do Gerenciador de Recursos existente ou VMs em execução que usam uma ID de cliente do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4537f-597">The following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="4537f-598">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="4537f-598">Parameter</span></span> | <span data-ttu-id="4537f-599">Descrição</span><span class="sxs-lookup"><span data-stu-id="4537f-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4537f-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="4537f-600">AADClientID</span></span> | <span data-ttu-id="4537f-601">ID do cliente do aplicativo Azure AD que tem permissões para gravar segredos no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-601">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="4537f-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="4537f-602">AADClientSecret</span></span> | <span data-ttu-id="4537f-603">Segredo do cliente do aplicativo AD do Azure que tem permissões para gravar segredos para o cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-603">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="4537f-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="4537f-604">keyVaultName</span></span> | <span data-ttu-id="4537f-605">Nome do cofre de chaves no qual a chave do BitLocker deve ser carregada.</span><span class="sxs-lookup"><span data-stu-id="4537f-605">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="4537f-606">Você pode obtê-lo usando o cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="4537f-606">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="4537f-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="4537f-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="4537f-608">URL da chave de criptografia de chaves que é usada para criptografar a chave gerada do BitLocker.</span><span class="sxs-lookup"><span data-stu-id="4537f-608">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="4537f-609">Esse parâmetro será opcional se você selecionar **nokek** na lista suspensa UseExistingKek.</span><span class="sxs-lookup"><span data-stu-id="4537f-609">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="4537f-610">Se selecionar **kek** na lista suspensa UseExistingKek, você deverá inserir o valor _keyEncryptionKeyURL_.</span><span class="sxs-lookup"><span data-stu-id="4537f-610">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="4537f-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="4537f-611">volumeType</span></span> | <span data-ttu-id="4537f-612">Tipo de volume em que a operação de criptografia é executada.</span><span class="sxs-lookup"><span data-stu-id="4537f-612">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="4537f-613">Os valores válidos com suporte são _OS_ ou _Todos_ (para RHEL 7.2, CentOS 7.2 e Ubuntu 16.04) e _Dados_ (para todas as outras distribuições).</span><span class="sxs-lookup"><span data-stu-id="4537f-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="4537f-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="4537f-614">sequenceVersion</span></span> | <span data-ttu-id="4537f-615">Versão de sequência da operação de BitLocker.</span><span class="sxs-lookup"><span data-stu-id="4537f-615">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="4537f-616">Aumente esse número de versão sempre que uma operação de criptografia de disco for executada na mesma VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-616">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="4537f-617">vmName</span><span class="sxs-lookup"><span data-stu-id="4537f-617">vmName</span></span> | <span data-ttu-id="4537f-618">Nome da VM em que a operação de criptografia deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="4537f-618">Name of the VM that the encryption operation is to be performed on.</span></span> |
| <span data-ttu-id="4537f-619">Senha</span><span class="sxs-lookup"><span data-stu-id="4537f-619">passPhrase</span></span> | <span data-ttu-id="4537f-620">Digite uma frase secreta forte como chave de criptografia de dados.</span><span class="sxs-lookup"><span data-stu-id="4537f-620">Type a strong passphrase as the data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="4537f-621">_KeyEncryptionKeyURL_ é um parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="4537f-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="4537f-622">Você pode usar seu próprio KEK para proteger ainda mais a chave de criptografia de dados (frase secreta) no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-622">You can bring your own KEK to further safeguard the data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="4537f-623">Comandos de CLI</span><span class="sxs-lookup"><span data-stu-id="4537f-623">CLI commands</span></span>
<span data-ttu-id="4537f-624">Você pode habilitar a criptografia de disco em seu VHD criptografado instalando e usando o [comando da CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4537f-624">You can enable disk encryption on your encrypted VHD by installing and using the [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="4537f-625">Para habilitar a criptografia em VMs IaaS Linux existentes ou em execução no Azure usando os comandos da CLI, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4537f-625">To enable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="4537f-626">Definir políticas de acesso no cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="4537f-626">Set access policies in the key vault:</span></span>

 * <span data-ttu-id="4537f-627">Defina o sinalizador **EnabledForDiskEncryption**:</span><span class="sxs-lookup"><span data-stu-id="4537f-627">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="4537f-628">Defina permissões para o aplicativo Azure AD para gravar segredos no cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="4537f-628">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="4537f-629">Para habilitar a criptografia em uma VM existente ou em execução:</span><span class="sxs-lookup"><span data-stu-id="4537f-629">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="4537f-630">Obtenha o status de criptografia:</span><span class="sxs-lookup"><span data-stu-id="4537f-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="4537f-631">Para habilitar a criptografia em uma nova VM de seu VHD criptografado, use os seguintes parâmetros com o comando `azure vm create`:</span><span class="sxs-lookup"><span data-stu-id="4537f-631">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-the-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="4537f-632">Obter o status da criptografia de uma VM IaaS criptografada</span><span class="sxs-lookup"><span data-stu-id="4537f-632">Get the encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="4537f-633">É possível obter o status da criptografia usando o Azure Resource Manager, [cmdlets do PowerShell](/powershell/azure/overview) ou comandos da CLI.</span><span class="sxs-lookup"><span data-stu-id="4537f-633">You can get the encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="4537f-634">As seções a seguir explicam como usar o portal clássico do Azure e os comandos da CLI para obter o status de criptografia.</span><span class="sxs-lookup"><span data-stu-id="4537f-634">The following sections explain how to use the Azure classic portal and CLI commands to get the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="4537f-635">Obter o status da criptografia de uma VM do Windows criptografada usando o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4537f-635">Get the encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="4537f-636">Você pode obter o status de criptografia da VM IaaS do Azure Resource Manager fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4537f-636">You can get the encryption status of the IaaS VM from Azure Resource Manager by doing the following:</span></span>

1. <span data-ttu-id="4537f-637">Entre no [portal clássico do Azure](https://portal.azure.com/) e clique em **Máquinas virtuais** no painel esquerdo para ver uma exibição resumida das máquinas virtuais em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="4537f-637">Sign in to the [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in the left pane to see a summary view of the virtual machines in your subscription.</span></span> <span data-ttu-id="4537f-638">Você pode filtrar a exibição de máquinas virtuais selecionando o nome da assinatura na lista suspensa **Assinatura**.</span><span class="sxs-lookup"><span data-stu-id="4537f-638">You can filter the virtual machines view by selecting the subscription name in the **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="4537f-639">Na parte superior da página **Máquinas virtuais**, clique em **Colunas**.</span><span class="sxs-lookup"><span data-stu-id="4537f-639">At the top of the **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="4537f-640">Na folha **Escolher coluna**, selecione **Criptografia de Disco**e clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="4537f-640">On the **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="4537f-641">Você deve ver a coluna de criptografia de disco mostrando o estado de criptografia _Habilitado_ ou _Desabilitado_ para cada VM conforme mostrado na seguinte figura:</span><span class="sxs-lookup"><span data-stu-id="4537f-641">You should see the disk-encryption column showing the encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in the following figure:</span></span>

 ![Microsoft Antimalware no Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-the-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-the-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="4537f-643">Obter o status de criptografia de uma VM IaaS (Windows/Linux) criptografada usando o cmdlet do PowerShell de criptografia de disco</span><span class="sxs-lookup"><span data-stu-id="4537f-643">Get the encryption status of an encrypted (Windows/Linux) IaaS VM by using the disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="4537f-644">Você pode obter o status de criptografia da VM IaaS por meio do cmdlet do PowerShell de criptografia de disco `Get-AzureRmVMDiskEncryptionStatus`.</span><span class="sxs-lookup"><span data-stu-id="4537f-644">You can get the encryption status of the IaaS VM from the disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="4537f-645">Para obter as configurações de criptografia para sua VM, digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4537f-645">To get the encryption settings for your VM, enter the following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="4537f-646">Você pode inspecionar a saída de _Get-AzureRmVMDiskEncryptionStatus_ para obter URLs de criptografia de chave.</span><span class="sxs-lookup"><span data-stu-id="4537f-646">You can inspect the output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

<span data-ttu-id="4537f-647">O valor das configurações OSVolumeEncrypted e DataVolumesEncrypted é definido como _Encrypted_, mostrando que ambos os volumes são criptografados com o Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="4537f-647">The OSVolumeEncrypted and DataVolumesEncrypted settings values are set to _Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="4537f-648">Para obter informações sobre como habilitar a criptografia com o Azure Disk Encryption usando cmdlets do PowerShell, confira as postagens de blog [Explorar Azure Disk Encryption com o Azure PowerShell - parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) e [Explorar Azure Disk Encryption com o Azure PowerShell - parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="4537f-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="4537f-649">Em VMs Linux, leva três ou quatro minutos para que o cmdlet `Get-AzureRmVMDiskEncryptionStatus` relate o status de criptografia.</span><span class="sxs-lookup"><span data-stu-id="4537f-649">On Linux VMs, it takes three to four minutes for the `Get-AzureRmVMDiskEncryptionStatus` cmdlet to report the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-the-iaas-vm-from-the-disk-encryption-cli-command"></a><span data-ttu-id="4537f-650">Obter status da criptografia da VM IaaS do comando CLI de criptografia de disco</span><span class="sxs-lookup"><span data-stu-id="4537f-650">Get the encryption status of the IaaS VM from the disk-encryption CLI command</span></span>
<span data-ttu-id="4537f-651">Você pode obter o status de criptografia da VM IaaS usando o comando da CLI de criptografia de disco `azure vm show-disk-encryption-status`.</span><span class="sxs-lookup"><span data-stu-id="4537f-651">You can get the encryption status of the IaaS VM by using the disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="4537f-652">Para obter as configurações de criptografia de sua VM, digite na sessão do Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="4537f-652">To get the encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="4537f-653">Desabilitar a criptografia em VMs IaaS do Windows em execução</span><span class="sxs-lookup"><span data-stu-id="4537f-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="4537f-654">Você pode desabilitar a criptografia em uma VM IaaS do Windows ou Linux em execução por meio do modelo do Resource Manager do Azure Disk Encryption ou de cmdlets do PowerShell e especificar a configuração da descriptografia.</span><span class="sxs-lookup"><span data-stu-id="4537f-654">You can disable encryption on a running Windows or Linux IaaS VM via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify the decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="4537f-655">VM Windows</span><span class="sxs-lookup"><span data-stu-id="4537f-655">Windows VM</span></span>
<span data-ttu-id="4537f-656">A etapa de desabilitar a criptografia desabilita a criptografia do sistema operacional ou volume de dados na VM IaaS do Windows em execução.</span><span class="sxs-lookup"><span data-stu-id="4537f-656">The disable-encryption step disables encryption of the OS, the data volume, or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="4537f-657">Você não pode desabilitar o volume do sistema operacional e deixar o volume de dados criptografado.</span><span class="sxs-lookup"><span data-stu-id="4537f-657">You cannot disable the OS volume and leave the data volume encrypted.</span></span> <span data-ttu-id="4537f-658">Quando a etapa de desabilitação da criptografia for executada, o modelo de implantação clássico do Azure atualizará o modelo de serviço da VM e a VM IaaS do Windows é marcada como descriptografada.</span><span class="sxs-lookup"><span data-stu-id="4537f-658">When the disable-encryption step is performed, the Azure classic deployment model updates the VM service model, and the Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="4537f-659">O conteúdo da VM não está criptografado em repouso.</span><span class="sxs-lookup"><span data-stu-id="4537f-659">The contents of the VM are no longer encrypted at rest.</span></span> <span data-ttu-id="4537f-660">A descriptografia não exclui o cofre de chaves e o material da chave de criptografia (chaves de criptografia do BitLocker para Windows e frase secreta para Linux).</span><span class="sxs-lookup"><span data-stu-id="4537f-660">The decryption does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="4537f-661">VM Linux</span><span class="sxs-lookup"><span data-stu-id="4537f-661">Linux VM</span></span>
<span data-ttu-id="4537f-662">A etapa de desabilitação da criptografia desabilita a criptografia do volume de dados na VM IaaS do Linux em execução.</span><span class="sxs-lookup"><span data-stu-id="4537f-662">The disable-encryption step disables encryption of the data volume on the running Linux IaaS VM.</span></span> <span data-ttu-id="4537f-663">Esta etapa somente funciona se o disco do OS não estiver criptografado.</span><span class="sxs-lookup"><span data-stu-id="4537f-663">This step only works if the OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="4537f-664">Não é permitido desabilitar a criptografia no disco do sistema operacional em VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="4537f-664">Disabling encryption on the OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="4537f-665">Desabilitar a criptografia em uma VM IaaS existente ou em execução</span><span class="sxs-lookup"><span data-stu-id="4537f-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="4537f-666">Você pode desabilitar a criptografia de disco em VMs IaaS do Windows em execução usando o [modelo do Gerenciador de Recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="4537f-666">You can disable disk encryption on running Windows IaaS VMs by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="4537f-667">No modelo de início rápido do Azure, clique em **Implantar no Azure**, insira a configuração de descriptografia na folha **Parâmetros** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4537f-667">On the Azure quick-start template, click **Deploy to Azure**, enter the decryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="4537f-668">Selecione a assinatura, o grupo de recursos, o local do grupo de recursos, os termos legais e o contrato e clique em **Criar** para habilitar a criptografia na VM IaaS nova.</span><span class="sxs-lookup"><span data-stu-id="4537f-668">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="4537f-669">Para VMs do Linux, você pode desabilitar a criptografia usando o modelo [Desabilitar a criptografia em uma VM do Linux em execução](https://aka.ms/decrypt-linuxvm).</span><span class="sxs-lookup"><span data-stu-id="4537f-669">For Linux VMs, you can disable encryption by using the [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="4537f-670">A tabela a seguir lista os parâmetros de modelo do Gerenciador de Recursos para desabilitar a criptografia em uma VM IaaS em execução:</span><span class="sxs-lookup"><span data-stu-id="4537f-670">The following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="4537f-671">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="4537f-671">Parameter</span></span> | <span data-ttu-id="4537f-672">Descrição</span><span class="sxs-lookup"><span data-stu-id="4537f-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4537f-673">vmName</span><span class="sxs-lookup"><span data-stu-id="4537f-673">vmName</span></span> | <span data-ttu-id="4537f-674">Nome da VM em que a operação de criptografia deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="4537f-674">Name of the VM that the encryption operation is to be performed on.</span></span>
| <span data-ttu-id="4537f-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="4537f-675">volumeType</span></span> | <span data-ttu-id="4537f-676">Tipo de volume em que uma operação de descriptografia é executada.</span><span class="sxs-lookup"><span data-stu-id="4537f-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="4537f-677">Os valores válidos são _OS_, _Data_ e _All_.</span><span class="sxs-lookup"><span data-stu-id="4537f-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="4537f-678">Não é possível desabilitar a criptografia no volume de inicialização/sistema operacional da VM IaaS do Windows em execução sem desabilitar a criptografia no volume _Data_.</span><span class="sxs-lookup"><span data-stu-id="4537f-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on the _Data_ volume.</span></span> <span data-ttu-id="4537f-679">Observe também que não é permitido desabilitar a criptografia no disco do sistema operacional em VMs Linux.</span><span class="sxs-lookup"><span data-stu-id="4537f-679">Also note that disabling encryption on the OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="4537f-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="4537f-680">sequenceVersion</span></span> | <span data-ttu-id="4537f-681">Versão de sequência da operação de BitLocker.</span><span class="sxs-lookup"><span data-stu-id="4537f-681">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="4537f-682">Aumente esse número de versão cada vez que uma operação de descriptografia de disco for executada na mesma VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-682">Increment this version number every time a disk decryption operation is performed on the same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="4537f-683">Desabilitar a criptografia em uma VM IaaS existente ou em execução</span><span class="sxs-lookup"><span data-stu-id="4537f-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="4537f-684">Para desabilitar a criptografia em uma VM IaaS existente ou em execução usando o cmdlet do PowerShell, confira [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span><span class="sxs-lookup"><span data-stu-id="4537f-684">To disable encryption on an existing or running IaaS VM by using the PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="4537f-685">Esse cmdlet dá suporte a VMs do Linux e do Windows.</span><span class="sxs-lookup"><span data-stu-id="4537f-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="4537f-686">Para desabilitar a criptografia, ele instala uma extensão na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4537f-686">To disable encryption, it installs an extension on the virtual machine.</span></span> <span data-ttu-id="4537f-687">Se o parâmetro _Name_ não for especificado, será criada uma extensão com o nome padrão _AzureDiskEncryption for Windows VMs_.</span><span class="sxs-lookup"><span data-stu-id="4537f-687">If the _Name_ parameter is not specified, an extension with the default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="4537f-688">Em VMs do Linux, a extensão AzureDiskEncryptionForLinux é usada.</span><span class="sxs-lookup"><span data-stu-id="4537f-688">On Linux VMs, the AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="4537f-689">Este cmdlet reinicia a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4537f-689">This cmdlet reboots the virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="4537f-690">Habilitar criptografia na VM da IaaS criptografada previamente com o Azure Managed Disk</span><span class="sxs-lookup"><span data-stu-id="4537f-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="4537f-691">Use o modelo ARM do Azure Managed Disk para criar uma VM criptografada a partir de um VHD criptografado previamente usando o modelo ARM localizado em</span><span class="sxs-lookup"><span data-stu-id="4537f-691">Use the Azure Managed Disk ARM template to create a encrypted VM from a pre-encrypted VHD using the ARM template located at</span></span>   
<span data-ttu-id="4537f-692">[Criar um novo disco gerenciado criptografado a partir de um blob de armazenamento/VHD criptografado] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="4537f-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="4537f-693">Habilitar criptografia em uma nova VM de IaaS Linux com o Azure Managed Disk</span><span class="sxs-lookup"><span data-stu-id="4537f-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="4537f-694">Use o modelo ARM do Azure Managed para criar uma nova VM de IaaS Linux criptografada usando o modelo ARM localizado em</span><span class="sxs-lookup"><span data-stu-id="4537f-694">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
<span data-ttu-id="4537f-695">[Implantação do RHEL 7.2 com criptografia de disco completo] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="4537f-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="4537f-696">Habilitar criptografia em uma nova VM de IaaS do Windows com o Azure Managed Disk</span><span class="sxs-lookup"><span data-stu-id="4537f-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="4537f-697">Use o modelo ARM do Azure Managed para criar uma nova VM de IaaS Linux criptografada usando o modelo ARM localizado em</span><span class="sxs-lookup"><span data-stu-id="4537f-697">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
 <span data-ttu-id="4537f-698">[Criar uma nova VM do Disco Gerenciado de IaaS do Windows a partir da imagem da galeria] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="4537f-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="4537f-699">É obrigatório criar um instantâneo e/ou fazer backup de uma instância VM baseada em disco gerenciado fora do Azure Disk Encryption e antes de habilitá-lo.</span><span class="sxs-lookup"><span data-stu-id="4537f-699">It is mandatory to snapshot and/or backup a managed disk based VM instance outside of and prior to enabling Azure Disk Encryption.</span></span>  <span data-ttu-id="4537f-700">Um instantâneo do disco gerenciado pode ser criado do portal ou usando o Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="4537f-700">A snapshot of the managed disk can be taken from the portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="4537f-701">Backups asseguram que uma opção de recuperação é possível no caso de qualquer falha inesperada durante a criptografia.</span><span class="sxs-lookup"><span data-stu-id="4537f-701">Backups ensure that a recovery option is possible in the case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="4537f-702">Depois que um backup é feito, o cmdlet Set-AzureRmVMDiskEncryptionExtension pode ser usado para criptografar Managed Disks especificando o parâmetro -skipVmBackup.</span><span class="sxs-lookup"><span data-stu-id="4537f-702">Once a backup is made, the Set-AzureRmVMDiskEncryptionExtension cmdlet can be used to encrypt managed disks by specifying the -skipVmBackup parameter.</span></span>  <span data-ttu-id="4537f-703">Este comando falhará em VMs baseadas em disco gerenciado até que um backup tenha sido feito e esse parâmetro tenha sido especificado.</span><span class="sxs-lookup"><span data-stu-id="4537f-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="4537f-704">Atualizar configurações de criptografia de uma VM de armazenamento não premium criptografada existente</span><span class="sxs-lookup"><span data-stu-id="4537f-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="4537f-705">Use interfaces com suporte de criptografia de disco do Azure existentes para executar VM [modelos ARM, PS cmdlets ou CLI] para atualizar as configurações de criptografia como segredo/ID de cliente AAD, chave de criptografia chave [KEK], chave de criptografia BitLocker para VM do Windows ou frase secreta para VM do Linux, etc. A configuração de criptografia de atualização oferece suporte apenas para VMs com suporte de armazenamento não premium.</span><span class="sxs-lookup"><span data-stu-id="4537f-705">Use the existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] to update the encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. The update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="4537f-706">Não oferece suporte para VMs com suporte de armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="4537f-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="4537f-707">Apêndice</span><span class="sxs-lookup"><span data-stu-id="4537f-707">Appendix</span></span>
### <a name="connect-to-your-subscription"></a><span data-ttu-id="4537f-708">Conecte-se as suas assinaturas</span><span class="sxs-lookup"><span data-stu-id="4537f-708">Connect to your subscription</span></span>
<span data-ttu-id="4537f-709">Antes de prosseguir, revise a seção  *Pré-requisitos*  neste artigo.</span><span class="sxs-lookup"><span data-stu-id="4537f-709">Before you proceed, review the *Prerequisites* section in this article.</span></span> <span data-ttu-id="4537f-710">Depois de garantir que todos os pré-requisitos foram atendidos, conecte-se à sua assinatura fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4537f-710">After you ensure that all prerequisites have been met, connect to your subscription by doing the following:</span></span>

1. <span data-ttu-id="4537f-711">Inicie uma sessão do Azure PowerShell e entre em sua conta do Azure com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4537f-711">Start an Azure PowerShell session, and sign in to your Azure account with the following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="4537f-712">Se tiver várias assinaturas e quiser especificar uma a ser usada, digite o seguinte para ver as assinaturas da sua conta:</span><span class="sxs-lookup"><span data-stu-id="4537f-712">If you have multiple subscriptions and want to specify one to use, type the following to see the subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="4537f-713">Para especificar a assinatura que você quer usar, digite:</span><span class="sxs-lookup"><span data-stu-id="4537f-713">To specify the subscription you want to use, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="4537f-714">Para verificar se a assinatura configurada está correta, digite:</span><span class="sxs-lookup"><span data-stu-id="4537f-714">To verify that the subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="4537f-715">Para confirmar que os cmdlets de Azure Disk Encryption estão instalados, digite:</span><span class="sxs-lookup"><span data-stu-id="4537f-715">To confirm the Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="4537f-716">A saída a seguir confirma a instalação do PowerShell de Azure Disk Encryption:</span><span class="sxs-lookup"><span data-stu-id="4537f-716">The following output confirms the Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="4537f-717">Preparar um VHD do Windows previamente criptografado</span><span class="sxs-lookup"><span data-stu-id="4537f-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="4537f-718">As seções a seguir são necessárias para preparar um VHD do Windows previamente criptografado para implantação como um VHD criptografado no Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="4537f-718">The sections that follow are necessary to prepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="4537f-719">Use as informações para preparar e inicializar uma nova VHD (VM do Windows) no Azure Site Recovery ou no Azure.</span><span class="sxs-lookup"><span data-stu-id="4537f-719">Use the information to prepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-to-allow-non-tpm-for-os-protection"></a><span data-ttu-id="4537f-720">Atualizar a política de grupo para permitir não TPM na proteção do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="4537f-720">Update group policy to allow non-TPM for OS protection</span></span>
<span data-ttu-id="4537f-721">Configure a política de grupo do BitLocker **Criptografia de Unidade de Disco BitLocker**, que você encontrará em **Política de Computador Local** > **Configuração do Computador** > **Modelos Administrativos** > **Componentes do Windows**.</span><span class="sxs-lookup"><span data-stu-id="4537f-721">Configure the BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="4537f-722">Altere essa configuração para: **Unidades do Sistema Operacional** > **Exigir autenticação adicional na inicialização** > **Permitir BitLocker sem TPM compatível**, como mostrado na seguinte figura:</span><span class="sxs-lookup"><span data-stu-id="4537f-722">Change this setting to **Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in the following figure:</span></span>

![Microsoft Antimalware no Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="4537f-724">Instalar componentes de recursos do BitLocker</span><span class="sxs-lookup"><span data-stu-id="4537f-724">Install BitLocker feature components</span></span>
<span data-ttu-id="4537f-725">Para o Windows Server 2012 e versões posteriores, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4537f-725">For Windows Server 2012 and later, use the following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="4537f-726">Para o Windows Server 2008 R2, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4537f-726">For Windows Server 2008 R2, use the following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-the-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="4537f-727">Preparar o volume do sistema operacional para o BitLocker usando `bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="4537f-727">Prepare the OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="4537f-728">Para compactar a partição do sistema operacional e preparar o computador para o BitLocker, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4537f-728">To compress the OS partition and prepare the machine for BitLocker, execute the following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-the-os-volume-by-using-bitlocker"></a><span data-ttu-id="4537f-729">Proteger o volume do sistema operacional usando o BitLocker</span><span class="sxs-lookup"><span data-stu-id="4537f-729">Protect the OS volume by using BitLocker</span></span>
<span data-ttu-id="4537f-730">Use o comando [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) para habilitar a criptografia no volume de inicialização usando um protetor de chave externo.</span><span class="sxs-lookup"><span data-stu-id="4537f-730">Use the [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command to enable encryption on the boot volume using an external key protector.</span></span> <span data-ttu-id="4537f-731">Também coloque a chave externa (arquivo .bek) na unidade ou no volume.</span><span class="sxs-lookup"><span data-stu-id="4537f-731">Also place the external key (.bek file) on the external drive or volume.</span></span> <span data-ttu-id="4537f-732">A criptografia é habilitada no volume de inicialização/sistema após a próxima reinicialização.</span><span class="sxs-lookup"><span data-stu-id="4537f-732">Encryption is enabled on the system/boot volume after the next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="4537f-733">Prepare a VM com um VHD de dados/recursos separado para obter a chave externa usando o BitLocker.</span><span class="sxs-lookup"><span data-stu-id="4537f-733">Prepare the VM with a separate data/resource VHD for getting the external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="4537f-734">Criptografando uma unidade do sistema operacional em uma VM do Linux em execução</span><span class="sxs-lookup"><span data-stu-id="4537f-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="4537f-735">Há suporte para a criptografia da unidade do sistema operacional em uma VM do Linux em execução nas seguintes distribuições:</span><span class="sxs-lookup"><span data-stu-id="4537f-735">Encryption of an OS drive on a running Linux VM is supported on the following distributions:</span></span>

* <span data-ttu-id="4537f-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="4537f-736">RHEL 7.2</span></span>
* <span data-ttu-id="4537f-737">CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="4537f-737">CentOS 7.2</span></span>
* <span data-ttu-id="4537f-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="4537f-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="4537f-739">Pré-requisitos para a criptografia de disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="4537f-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="4537f-740">A VM deve ser criada com base na imagem do Marketplace no Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4537f-740">The VM must be created from the Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="4537f-741">VM do Azure com, no mínimo, 4 GB de RAM (o tamanho recomendável é de 7 GB).</span><span class="sxs-lookup"><span data-stu-id="4537f-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="4537f-742">(Para RHEL e CentOS) Desabilite o SELinux.</span><span class="sxs-lookup"><span data-stu-id="4537f-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="4537f-743">Para desabilitar SELinux, confira "4.4.2.</span><span class="sxs-lookup"><span data-stu-id="4537f-743">To disable SELinux, see "4.4.2.</span></span> <span data-ttu-id="4537f-744">Desabilitando o SELinux" no [Guia do Administrador e Usuário do SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) na VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-744">Disabling SELinux" in the [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on the VM.</span></span>
* <span data-ttu-id="4537f-745">Depois de desabilitar o SELinux, reinicialize a VM pelo menos uma vez.</span><span class="sxs-lookup"><span data-stu-id="4537f-745">After you disable SELinux, reboot the VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="4537f-746">Etapas</span><span class="sxs-lookup"><span data-stu-id="4537f-746">Steps</span></span>
1. <span data-ttu-id="4537f-747">Crie uma VM usando uma das distribuições especificadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4537f-747">Create a VM by using one of the distributions specified previously.</span></span>

 <span data-ttu-id="4537f-748">Para o CentOS 7.2, há suporte para a criptografia de disco do sistema operacional por meio de uma imagem especial.</span><span class="sxs-lookup"><span data-stu-id="4537f-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="4537f-749">Para usar essa imagem, especifique "7.2n" como o SKU quando você criar a VM:</span><span class="sxs-lookup"><span data-stu-id="4537f-749">To use this image, specify "7.2n" as the SKU when you create the VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="4537f-750">Configure a VM de acordo com suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="4537f-750">Configure the VM according to your needs.</span></span> <span data-ttu-id="4537f-751">Se for criptografar todas as unidades (sistema operacional + dados), as unidades de dados precisarão ser especificadas e deverão ser montadas em /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="4537f-751">If you are going to encrypt all the (OS + data) drives, the data drives need to be specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="4537f-752">Use UUID=... para especificar unidades de dados em/etc/fstab em vez de especificar o nome do dispositivo de blocos (por exemplo, /dev/sdb1).</span><span class="sxs-lookup"><span data-stu-id="4537f-752">Use UUID=... to specify data drives in /etc/fstab instead of specifying the block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="4537f-753">Durante a criptografia, a ordem das é alterada na VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-753">During encryption, the order of drives changes on the VM.</span></span> <span data-ttu-id="4537f-754">Se a VM se basear em uma ordem específica de dispositivos de blocos, ela não conseguirá montá-los após a criptografia.</span><span class="sxs-lookup"><span data-stu-id="4537f-754">If your VM relies on a specific order of block devices, it will fail to mount them after encryption.</span></span>

3. <span data-ttu-id="4537f-755">Saia das sessões do SSH.</span><span class="sxs-lookup"><span data-stu-id="4537f-755">Sign out of the SSH sessions.</span></span>

4. <span data-ttu-id="4537f-756">Para criptografar o sistema operacional, especifique volumeType como **All** ou **OS** ao [habilitar a criptografia](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span><span class="sxs-lookup"><span data-stu-id="4537f-756">To encrypt the OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="4537f-757">Todos os processos de espaço de usuário que não estão sendo executados como serviços `systemd` deverão ser encerrados com um `SIGKILL`.</span><span class="sxs-lookup"><span data-stu-id="4537f-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="4537f-758">Reinicialize a VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-758">Reboot the VM.</span></span> <span data-ttu-id="4537f-759">Ao habilitar a criptografia de disco do sistema operacional em uma VM em execução, planeje o tempo de inatividade da VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="4537f-760">Periodicamente, monitore o progresso da criptografia usando as instruções da [próxima seção](#monitoring-os-encryption-progress).</span><span class="sxs-lookup"><span data-stu-id="4537f-760">Periodically monitor the progress of encryption by using the instructions in the [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="4537f-761">Depois que Get-AzureRmVmDiskEncryptionStatus mostrar "VMRestartPending", reinicie a VM entrando ou usando o portal, o PowerShell ou a CLI.</span><span class="sxs-lookup"><span data-stu-id="4537f-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in to it or by using the portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot the VM
    ```
<span data-ttu-id="4537f-762">Antes de reinicializar, recomendamos que você salve os [diagnósticos de inicialização](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) da VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of the VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="4537f-763">Monitorando o progresso da criptografia do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="4537f-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="4537f-764">Você pode monitorar o progresso de criptografia do sistema operacional de três maneiras:</span><span class="sxs-lookup"><span data-stu-id="4537f-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="4537f-765">Use o cmdlet `Get-AzureRmVmDiskEncryptionStatus` e verifique o campo ProgressMessage:</span><span class="sxs-lookup"><span data-stu-id="4537f-765">Use the `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect the ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="4537f-766">Depois que a VM atingir "Criptografia de disco do sistema operacional iniciada", levará cerca de 40 a 50 minutos em uma VM com suporte do armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="4537f-766">After the VM reaches "OS disk encryption started," it takes about 40 to 50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="4537f-767">Devido ao [problema 388](https://github.com/Azure/WALinuxAgent/issues/388) no WALinuxAgent, `OsVolumeEncrypted` e `DataVolumesEncrypted` são mostrados como `Unknown` em algumas distribuições.</span><span class="sxs-lookup"><span data-stu-id="4537f-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="4537f-768">Com a versão 2.1.5 WALinuxAgent e posterior, esse problema é corrigido automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4537f-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="4537f-769">Caso você veja `Unknown` na saída, poderá verificar o status da criptografia de disco usando o Explorador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4537f-769">If you see `Unknown` in the output, you can verify disk-encryption status by using the Azure Resource Explorer.</span></span>

 <span data-ttu-id="4537f-770">Vá para [Explorador de Recursos do Azure](https://resources.azure.com/) e expanda essa hierarquia no painel de seleção à esquerda:</span><span class="sxs-lookup"><span data-stu-id="4537f-770">Go to [Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in the selection panel on left:</span></span>

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 <span data-ttu-id="4537f-771">Em InstanceView, role a tela para baixo para ver o status da criptografia das unidades.</span><span class="sxs-lookup"><span data-stu-id="4537f-771">In the InstanceView, scroll down to see the encryption status of your drives.</span></span>

 ![Exibição de instância VM](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="4537f-773">Examine o [diagnóstico de inicialização](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="4537f-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="4537f-774">As mensagens da extensão ADE devem ser prefixadas com `[AzureDiskEncryption]`.</span><span class="sxs-lookup"><span data-stu-id="4537f-774">Messages from the ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="4537f-775">Entre na VM via SSH e obtenha o log de extensão de:</span><span class="sxs-lookup"><span data-stu-id="4537f-775">Sign in to the VM via SSH, and get the extension log from:</span></span>

    <span data-ttu-id="4537f-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="4537f-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="4537f-777">É recomendável que você não entre na máquina virtual enquanto a criptografia de sistema operacional estiver em andamento.</span><span class="sxs-lookup"><span data-stu-id="4537f-777">We recommend that you do not sign in to the VM while OS encryption is in progress.</span></span> <span data-ttu-id="4537f-778">Copie os logs apenas quando os outros dois métodos falharem.</span><span class="sxs-lookup"><span data-stu-id="4537f-778">Copy the logs only when the other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="4537f-779">Preparar um VHD Linux previamente criptografado</span><span class="sxs-lookup"><span data-stu-id="4537f-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="4537f-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="4537f-780">Ubuntu 16</span></span>
<span data-ttu-id="4537f-781">Configure a criptografia durante a instalação da distribuição fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4537f-781">Configure encryption during the distribution installation by doing the following:</span></span>

1. <span data-ttu-id="4537f-782">Selecione **Configurar volumes criptografados** ao particionar os discos.</span><span class="sxs-lookup"><span data-stu-id="4537f-782">Select **Configure encrypted volumes** when you partition the disks.</span></span>

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="4537f-784">Crie uma unidade de inicialização separada que não deverá ser criptografada.</span><span class="sxs-lookup"><span data-stu-id="4537f-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="4537f-785">Criptografe a unidade de inicialização.</span><span class="sxs-lookup"><span data-stu-id="4537f-785">Encrypt your root drive.</span></span>

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="4537f-787">Forneça uma senha.</span><span class="sxs-lookup"><span data-stu-id="4537f-787">Provide a passphrase.</span></span> <span data-ttu-id="4537f-788">Essa é a frase secreta que você carrega no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-788">This is the passphrase that you upload to the key vault.</span></span>

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="4537f-790">Conclua o particionamento.</span><span class="sxs-lookup"><span data-stu-id="4537f-790">Finish partitioning.</span></span>

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="4537f-792">Quando você inicializar a VM e precisar fornecer uma frase secreta, use a frase secreta que forneceu na etapa 3.</span><span class="sxs-lookup"><span data-stu-id="4537f-792">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="4537f-794">Prepare a VM para upload no Azure usando [estas instruções](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="4537f-794">Prepare the VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="4537f-795">Não execute a última etapa (desprovisionamento da VM) ainda.</span><span class="sxs-lookup"><span data-stu-id="4537f-795">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="4537f-796">Configure a criptografia para trabalhar com o Azure fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4537f-796">Configure encryption to work with Azure by doing the following:</span></span>

1. <span data-ttu-id="4537f-797">Crie um arquivo em /usr/local/sbin/azure_crypt_key.sh com o conteúdo no script a seguir.</span><span class="sxs-lookup"><span data-stu-id="4537f-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with the content in the following script.</span></span> <span data-ttu-id="4537f-798">Preste atenção ao KeyFileName, pois ele é o nome do arquivo de frase secreta usado pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="4537f-798">Pay attention to the KeyFileName, because it is the passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED to find suitable passphrase file ..." >&2
        echo -n "Try to enter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="4537f-799">Altere a configuração de criptografia em */etc/crypttab*.</span><span class="sxs-lookup"><span data-stu-id="4537f-799">Change the crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="4537f-800">O resultado deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="4537f-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="4537f-801">Se você estiver editando *azure_crypt_key.sh* no Windows e o tiver copiado para o Linux, execute `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span><span class="sxs-lookup"><span data-stu-id="4537f-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it to Linux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="4537f-802">Adicione permissões executáveis ao script:</span><span class="sxs-lookup"><span data-stu-id="4537f-802">Add executable permissions to the script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="4537f-803">Edite */etc/initramfs-tools/modules* acrescentando linha:</span><span class="sxs-lookup"><span data-stu-id="4537f-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="4537f-804">Execute `update-initramfs -u -k all` para atualizar o initramfs para fazer com que o `keyscript` entre em vigor.</span><span class="sxs-lookup"><span data-stu-id="4537f-804">Run `update-initramfs -u -k all` to update the initramfs to make the `keyscript` take effect.</span></span>

7. <span data-ttu-id="4537f-805">Agora, você poderá desprovisionar a VM.</span><span class="sxs-lookup"><span data-stu-id="4537f-805">Now you can deprovision the VM.</span></span>

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="4537f-807">Continue na próxima etapa e [carregue o VHD](#upload-encrypted-vhd-to-an-azure-storage-account) no Azure.</span><span class="sxs-lookup"><span data-stu-id="4537f-807">Continue to the next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="4537f-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="4537f-808">openSUSE 13.2</span></span>
<span data-ttu-id="4537f-809">Para configurar a criptografia durante a instalação de distribuição, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4537f-809">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="4537f-810">Ao particionar os discos, selecione **Criptografar o Grupo de Volumes** e digite uma senha.</span><span class="sxs-lookup"><span data-stu-id="4537f-810">When you partition the disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="4537f-811">Esta é a senha que você carregará no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-811">This is the password that you will upload to your key vault.</span></span>

 ![Instalação do openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="4537f-813">Inicialize a VM usando uma senha.</span><span class="sxs-lookup"><span data-stu-id="4537f-813">Boot the VM using your password.</span></span>

 ![Instalação do openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="4537f-815">Prepare a VM para carregamento no Azure seguindo as instruções em [Preparar uma máquina virtual do SLES ou openSUSE para o Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span><span class="sxs-lookup"><span data-stu-id="4537f-815">Prepare the VM for uploading to Azure by following the instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="4537f-816">Não execute a última etapa (desprovisionamento da VM) ainda.</span><span class="sxs-lookup"><span data-stu-id="4537f-816">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="4537f-817">Para configurar a criptografia para trabalhar com o Azure, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4537f-817">To configure encryption to work with Azure, do the following:</span></span>
1. <span data-ttu-id="4537f-818">Edite o /etc/dracut.conf e adicione a seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="4537f-818">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="4537f-819">Comente essas linhas ao final do arquivo /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="4537f-819">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. <span data-ttu-id="4537f-820">Acrescente a seguinte linha no início do arquivo /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span><span class="sxs-lookup"><span data-stu-id="4537f-820">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="4537f-821">E altere todas as ocorrências de:</span><span class="sxs-lookup"><span data-stu-id="4537f-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="4537f-822">para:</span><span class="sxs-lookup"><span data-stu-id="4537f-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="4537f-823">Edite /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e acrescente-o depois de “# Open LUKS device”:</span><span class="sxs-lookup"><span data-stu-id="4537f-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it to “# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. <span data-ttu-id="4537f-824">Execute `/usr/sbin/dracut -f -v` para atualizar o initrd.</span><span class="sxs-lookup"><span data-stu-id="4537f-824">Run `/usr/sbin/dracut -f -v` to update the initrd.</span></span>

6. <span data-ttu-id="4537f-825">Agora você pode desprovisionar a VM e [carregar o VHD](#upload-encrypted-vhd-to-an-azure-storage-account) no Azure.</span><span class="sxs-lookup"><span data-stu-id="4537f-825">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="4537f-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="4537f-826">CentOS 7</span></span>
<span data-ttu-id="4537f-827">Para configurar a criptografia durante a instalação de distribuição, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4537f-827">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="4537f-828">Selecione **Criptografar meus dados** ao particionar os discos.</span><span class="sxs-lookup"><span data-stu-id="4537f-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![Instalação do CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="4537f-830">Verifique se a opção **Criptografar** está selecionada para a partição raiz.</span><span class="sxs-lookup"><span data-stu-id="4537f-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![Instalação do CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="4537f-832">Forneça uma frase secreta.</span><span class="sxs-lookup"><span data-stu-id="4537f-832">Provide a passphrase.</span></span> <span data-ttu-id="4537f-833">Essa é a frase secreta que você carregará no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-833">This is the passphrase that you will upload to your key vault.</span></span>

 ![Instalação do CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="4537f-835">Quando você inicializar a VM e precisar fornecer uma frase secreta, use a senha que forneceu na etapa 3.</span><span class="sxs-lookup"><span data-stu-id="4537f-835">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![Instalação do CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="4537f-837">Prepare a VM para carregamento no Azure usando as instruções de "CentOS 7.0+" em [Preparar uma máquina virtual baseada em CentOS para o Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span><span class="sxs-lookup"><span data-stu-id="4537f-837">Prepare the VM for uploading into Azure by using the "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="4537f-838">Não execute a última etapa (desprovisionamento da VM) ainda.</span><span class="sxs-lookup"><span data-stu-id="4537f-838">Do not run the last step (deprovisioning the VM) yet.</span></span>

6. <span data-ttu-id="4537f-839">Agora você pode desprovisionar a VM e [carregar o VHD](#upload-encrypted-vhd-to-an-azure-storage-account) no Azure.</span><span class="sxs-lookup"><span data-stu-id="4537f-839">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="4537f-840">Para configurar a criptografia para trabalhar com o Azure, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4537f-840">To configure encryption to work with Azure, do the following:</span></span>

1. <span data-ttu-id="4537f-841">Edite o /etc/dracut.conf e adicione a seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="4537f-841">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="4537f-842">Comente essas linhas ao final do arquivo /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="4537f-842">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. <span data-ttu-id="4537f-843">Acrescente a seguinte linha no início do arquivo /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span><span class="sxs-lookup"><span data-stu-id="4537f-843">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="4537f-844">E altere todas as ocorrências de:</span><span class="sxs-lookup"><span data-stu-id="4537f-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="4537f-845">para</span><span class="sxs-lookup"><span data-stu-id="4537f-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="4537f-846">Edite /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e acrescente-o depois de “# Open LUKS device”:</span><span class="sxs-lookup"><span data-stu-id="4537f-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after the “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. <span data-ttu-id="4537f-847">Execute o “/usr/sbin/dracut -f -v” para atualizar o initrd.</span><span class="sxs-lookup"><span data-stu-id="4537f-847">Run the “/usr/sbin/dracut -f -v” to update the initrd.</span></span>

![Instalação do CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-to-an-azure-storage-account"></a><span data-ttu-id="4537f-849">Carregue o VHD criptografado para uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="4537f-849">Upload encrypted VHD to an Azure storage account</span></span>
<span data-ttu-id="4537f-850">Depois que a criptografia BitLocker ou criptografia DM-Crypt estiver habilitada, o VHD criptografado local precisará ser carregado para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4537f-850">After BitLocker encryption or DM-Crypt encryption is enabled, the local encrypted VHD needs to be uploaded to your storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-the-disk-encryption-secret-for-the-pre-encrypted-vm-to-your-key-vault"></a><span data-ttu-id="4537f-851">Carregar o segredo de criptografia de disco da VM previamente criptografada no cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="4537f-851">Upload the disk-encryption secret for the pre-encrypted VM to your key vault</span></span>
<span data-ttu-id="4537f-852">O segredo de criptografia de disco que você obteve anteriormente deve ser carregado como um segredo no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-852">The disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="4537f-853">O cofre de chaves deve ter criptografia de disco e permissões habilitadas para o cliente do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4537f-853">The key vault needs to have disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="4537f-854">Segredo de criptografia de disco não criptografado com uma KEK</span><span class="sxs-lookup"><span data-stu-id="4537f-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="4537f-855">Para configurar o segredo no cofre de chaves, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="4537f-855">To set up the secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="4537f-856">Se você tem uma máquina virtual do Windows, o arquivo bek é codificado como uma cadeia de caracteres em base64 e carregado no cofre de chaves usando o cmdlet `Set-AzureKeyVaultSecret`.</span><span class="sxs-lookup"><span data-stu-id="4537f-856">If you have a Windows virtual machine, the bek file is encoded as a base64 string and then uploaded to your key vault using the `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="4537f-857">Para o Linux, a frase secreta é codificada como uma cadeia de caracteres base64 e carregada para o cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-857">For Linux, the passphrase is encoded as a base64 string and then uploaded to the key vault.</span></span> <span data-ttu-id="4537f-858">Além disso, verifique se as seguintes marcas estão definidas ao criar o segredo no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4537f-858">In addition, make sure that the following tags are set when you create the secret in the key vault.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="4537f-859">Use o `$secretUrl` na próxima etapa para [anexar o disco do sistema operacional sem usar KEK](#without-using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="4537f-859">Use the `$secretUrl` in the next step for [attaching the OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="4537f-860">Segredo de criptografia de disco criptografado com uma KEK</span><span class="sxs-lookup"><span data-stu-id="4537f-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="4537f-861">Antes de carregar o segredo no cofre de chaves, opcionalmente, você pode criptografá-lo usando uma chave de criptografia de chave.</span><span class="sxs-lookup"><span data-stu-id="4537f-861">Before you upload the secret to the key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="4537f-862">Use a [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) de encapsulamento para primeiro criptografar o segredo usando a chave de criptografia de chave.</span><span class="sxs-lookup"><span data-stu-id="4537f-862">Use the wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) to first encrypt the secret using the key encryption key.</span></span> <span data-ttu-id="4537f-863">A saída dessa operação wrap é uma cadeia de caracteres de URL codificada em base64, que você pode carregar como um segredo usando o cmdlet [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="4537f-863">The output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using the [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

<span data-ttu-id="4537f-864">Use `$KeyEncryptionKey` e `$secretUrl` na próxima etapa para [anexar o disco do sistema operacional usando KEK](#using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="4537f-864">Use `$KeyEncryptionKey` and `$secretUrl` in the next step for [attaching the OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="4537f-865">Especificar uma URL secreta ao anexar um disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="4537f-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="4537f-866">Sem usar uma KEK</span><span class="sxs-lookup"><span data-stu-id="4537f-866">Without using a KEK</span></span>
<span data-ttu-id="4537f-867">Ao anexar o disco do sistema operacional, você precisa passar `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="4537f-867">While you are attaching the OS disk, you need to pass `$secretUrl`.</span></span> <span data-ttu-id="4537f-868">A URL foi gerada na seção "Segredo de criptografia de disco não criptografado com uma KEK".</span><span class="sxs-lookup"><span data-stu-id="4537f-868">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="4537f-869">Usando uma KEK</span><span class="sxs-lookup"><span data-stu-id="4537f-869">Using a KEK</span></span>
<span data-ttu-id="4537f-870">Ao anexar o disco do sistema operacional, passe `$KeyEncryptionKey` e `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="4537f-870">When you attach the OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="4537f-871">A URL foi gerada na seção "Segredo de criptografia de disco não criptografado com uma KEK".</span><span class="sxs-lookup"><span data-stu-id="4537f-871">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a><span data-ttu-id="4537f-872">Baixar este guia</span><span class="sxs-lookup"><span data-stu-id="4537f-872">Download this guide</span></span>
<span data-ttu-id="4537f-873">Você pode baixar este guia na [Galeria do TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span><span class="sxs-lookup"><span data-stu-id="4537f-873">You can download this guide from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="4537f-874">Para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="4537f-874">For more information</span></span>
[<span data-ttu-id="4537f-875">Explorar a Azure Disk Encryption com o Azure PowerShell - Parte 1</span><span class="sxs-lookup"><span data-stu-id="4537f-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="4537f-876">Explorar a Azure Disk Encryption com o Azure PowerShell - Parte 2</span><span class="sxs-lookup"><span data-stu-id="4537f-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
