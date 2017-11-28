---
title: aaaAzure criptografia de disco para o Windows e Linux VMs de IaaS | Microsoft Docs
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
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="c7ca9-103">Azure Disk Encryption para VMs IaaS Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="c7ca9-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="c7ca9-104">Microsoft Azure está fortemente comprometido tooensuring a privacidade dos dados, Soberania de dados e permite que você toocontrol hospedado do Azure dados por meio de uma variedade de tecnologias avançadas tooencrypt, controlar e gerenciar chaves de criptografia, auditoria e controle de acesso de dados.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-104">Microsoft Azure is strongly committed tooensuring your data privacy, data sovereignty and enables you toocontrol your Azure hosted data through a range of advanced technologies tooencrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="c7ca9-105">Isso oferece aos clientes do Azure Olá flexibilidade toochoose Olá solução melhor atende às suas necessidades de negócios.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-105">This provides Azure customers hello flexibility toochoose hello solution that best meets their business needs.</span></span> <span data-ttu-id="c7ca9-106">Neste documento, apresentaremos você tooa nova solução de tecnologia "Criptografia de disco do Azure para Windows e de Linux IaaS VM" toohelp proteger e proteger seu dados toomeet seus compromissos de segurança e conformidade organizacionais.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-106">In this paper, we will introduce you tooa new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” toohelp protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="c7ca9-107">papel Olá oferece orientação detalhada sobre como recursos de criptografia do disco do Azure Olá toouse incluindo Olá suporte para cenários e as experiências do usuário Olá.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-107">hello paper provides detailed guidance on how toouse hello Azure disk encryption features including hello supported scenarios and hello user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-108">Determinadas recomendações podem aumentar o uso de recursos de dados, rede ou computação, resultando em custos adicionais de licença ou inscrição.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="c7ca9-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c7ca9-109">Overview</span></span>
<span data-ttu-id="c7ca9-110">o Azure Disk Encryption é um novo recurso que ajuda a criptografar os discos de suas máquinas virtuais IaaS Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="c7ca9-111">Criptografia de disco do Azure utiliza o padrão da indústria Olá [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) recurso do Windows e hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) recurso de criptografia de volume tooprovide Linux para hello SO e discos de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-111">Azure Disk Encryption leverages hello industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux tooprovide volume encryption for hello OS and hello data disks.</span></span> <span data-ttu-id="c7ca9-112">Olá solução é integrada com [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp controlar e gerenciar chaves de criptografia de disco hello e segredos em sua assinatura do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-112">hello solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp you control and manage hello disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="c7ca9-113">solução de saudação também garante que todos os dados em discos de máquina virtual Olá sejam criptografados em repouso no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-113">hello solution also ensures that all data on hello virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="c7ca9-114">O Azure Disk Encryption para VMs IaaS do Windows e Linux agora está em **Disponibilidade Geral** em todas as regiões públicas do Azure e AzureGov para VMs Standard e VMs com armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="c7ca9-115">Cenários de criptografia</span><span class="sxs-lookup"><span data-stu-id="c7ca9-115">Encryption scenarios</span></span>
<span data-ttu-id="c7ca9-116">Olá solução de criptografia de disco do Azure dá suporte a saudação os seguintes cenários de cliente:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-116">hello Azure Disk Encryption solution supports hello following customer scenarios:</span></span>

* <span data-ttu-id="c7ca9-117">Habilitar a criptografia em novas VMs IaaS criadas com base em VHD pré-criptografado e chaves de criptografia</span><span class="sxs-lookup"><span data-stu-id="c7ca9-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="c7ca9-118">Habilitar a criptografia em novas VMs de IaaS criado a partir de imagens de galeria do Azure Olá com suporte</span><span class="sxs-lookup"><span data-stu-id="c7ca9-118">Enable encryption on new IaaS VMs created from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="c7ca9-119">Habilitar a criptografia em VMs IaaS existentes em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="c7ca9-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="c7ca9-120">Desabilitar a criptografia em VMs IaaS do Windows</span><span class="sxs-lookup"><span data-stu-id="c7ca9-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="c7ca9-121">Desabilitar a criptografia em unidades de dados para VMs IaaS do Linux</span><span class="sxs-lookup"><span data-stu-id="c7ca9-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="c7ca9-122">Ativar criptografia de VMs de disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="c7ca9-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="c7ca9-123">Atualizar configurações de criptografia de uma VM de armazenamento não premium criptografada existente</span><span class="sxs-lookup"><span data-stu-id="c7ca9-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="c7ca9-124">Backup e restauração de VMs criptografadas, criptografadas com chave de critografia de chave</span><span class="sxs-lookup"><span data-stu-id="c7ca9-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="c7ca9-125">solução de saudação dá suporte à saudação os seguintes cenários para VMs de IaaS quando eles estão habilitados no Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-125">hello solution supports hello following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="c7ca9-126">Integração com o Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ca9-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="c7ca9-127">VMs de camada padrão: [ A, D, DS, G, GS, F e VMs IaaS ](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="c7ca9-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="c7ca9-128">Habilitar a criptografia em Windows e VMs de IaaS Linux e máquinas virtuais de disco gerenciado de saudação suporte para imagens da Galeria do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ca9-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="c7ca9-129">Desativar criptografia no SO e nas unidades de dados para VMs da IaaS do Windows e VMs de disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="c7ca9-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="c7ca9-130">Desativar criptografia em unidades de dados para Linux Iaas VMs e VMs de disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="c7ca9-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="c7ca9-131">Habilitar a criptografia em VMs IaaS executando o sistema operacional Windows Client</span><span class="sxs-lookup"><span data-stu-id="c7ca9-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="c7ca9-132">Habilitar a criptografia em volumes com caminhos de montagem</span><span class="sxs-lookup"><span data-stu-id="c7ca9-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="c7ca9-133">Habilitar criptografia em VMs do Linux configuradas com disk striping (RAID) usando mdadm</span><span class="sxs-lookup"><span data-stu-id="c7ca9-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="c7ca9-134">Habilitar criptografia no Linux VMs utilizando LVM para discos de dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="c7ca9-135">Habilitar a criptografia em VMs do Windows configuradas com os Espaços de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="c7ca9-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="c7ca9-136">Atualizar configurações de criptografia de uma VM de armazenamento não premium criptografada existente</span><span class="sxs-lookup"><span data-stu-id="c7ca9-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="c7ca9-137">Para todas as regiões do Público do Azure e AzureGov há suporte</span><span class="sxs-lookup"><span data-stu-id="c7ca9-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="c7ca9-138">solução de saudação não oferece suporte a saudação cenários, recursos e tecnologias a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-138">hello solution does not support hello following scenarios, features, and technology:</span></span>

* <span data-ttu-id="c7ca9-139">VMs IaaS da camada Básica</span><span class="sxs-lookup"><span data-stu-id="c7ca9-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="c7ca9-140">Como desabilitar a criptografia em unidades do sistema operacional para VMs IaaS do Linux</span><span class="sxs-lookup"><span data-stu-id="c7ca9-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="c7ca9-141">Desabilitar a criptografia em uma unidade de dados se Olá unidade do sistema operacional for criptografada para VMs de Iaas Linux</span><span class="sxs-lookup"><span data-stu-id="c7ca9-141">Disabling encryption on a data drive if hello OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="c7ca9-142">VMs de IaaS que são criadas usando o método de criação de VM clássico Olá</span><span class="sxs-lookup"><span data-stu-id="c7ca9-142">IaaS VMs that are created by using hello classic VM creation method</span></span>
* <span data-ttu-id="c7ca9-143">Habilitar criptografia em imagens personalizadas do cliente de VMs de IaaS do Linux e Windows NÃO tem suporte.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="c7ca9-144">Habilitar criptografia no disco do SO do LVM do Linux, atualmente não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="c7ca9-145">Este suporte será disponibilizado em breve.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-145">This support will come soon.</span></span>
* <span data-ttu-id="c7ca9-146">Integração com o Serviço de Gerenciamento de Chaves no local</span><span class="sxs-lookup"><span data-stu-id="c7ca9-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="c7ca9-147">Arquivos do Azure (sistema de arquivos compartilhados), NFS (Network File System), volumes dinâmicos e VMs do Windows configuradas com Sistemas RAID baseados em software</span><span class="sxs-lookup"><span data-stu-id="c7ca9-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="c7ca9-148">Backup e restauração de VMs criptografadas, criptografadas com chave de criptografia de chave.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="c7ca9-149">Atualize configurações de criptografia de um armazenamento VM existente criptografado premium.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-150">Backup e restauração de VMs criptografadas com suporte apenas para VMs que são criptografados com a configuração de KEK hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="c7ca9-151">Não há suporte em VMs que são criptografados sem KEK.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="c7ca9-152">KEK é um parâmetro opcional que habilita a criptografia de VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="c7ca9-153">Esse suporte será oferecido em breve.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-153">This support is coming soon.</span></span>
> <span data-ttu-id="c7ca9-154">Atualizar configurações de criptografia de uma VM de armazenamento não premium criptografada existente.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="c7ca9-155">Esse suporte será oferecido em breve.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="c7ca9-156">Recursos de criptografia</span><span class="sxs-lookup"><span data-stu-id="c7ca9-156">Encryption features</span></span>
<span data-ttu-id="c7ca9-157">Quando você habilita e implanta a criptografia de disco do Azure para VMs de IaaS do Azure, hello seguintes recursos estão habilitados, dependendo da configuração de saudação fornecida:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, hello following capabilities are enabled, depending on hello configuration provided:</span></span>

* <span data-ttu-id="c7ca9-158">Criptografia de volume de inicialização de Olá Olá SO volume tooprotect em repouso no armazenamento</span><span class="sxs-lookup"><span data-stu-id="c7ca9-158">Encryption of hello OS volume tooprotect hello boot volume at rest in your storage</span></span>
* <span data-ttu-id="c7ca9-159">Criptografia de dados volumes tooprotect Olá os volumes de dados em repouso no armazenamento</span><span class="sxs-lookup"><span data-stu-id="c7ca9-159">Encryption of data volumes tooprotect hello data volumes at rest in your storage</span></span>
* <span data-ttu-id="c7ca9-160">Desabilitar a criptografia em hello sistema operacional e dados unidades para as VMs de IaaS do Windows</span><span class="sxs-lookup"><span data-stu-id="c7ca9-160">Disabling encryption on hello OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="c7ca9-161">Desabilitar a criptografia em dados Olá unidades para as VMs de IaaS Linux (somente se o sistema operacional da unidade não é criptografado)</span><span class="sxs-lookup"><span data-stu-id="c7ca9-161">Disabling encryption on hello data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="c7ca9-162">Protegendo chaves de criptografia de saudação e segredos em sua assinatura do Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="c7ca9-162">Safeguarding hello encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="c7ca9-163">Relatar o status de criptografia de saudação do hello criptografado IaaS VM</span><span class="sxs-lookup"><span data-stu-id="c7ca9-163">Reporting hello encryption status of hello encrypted IaaS VM</span></span>
* <span data-ttu-id="c7ca9-164">Remoção de configurações de criptografia de disco da máquina de virtual IaaS Olá</span><span class="sxs-lookup"><span data-stu-id="c7ca9-164">Removal of disk-encryption configuration settings from hello IaaS virtual machine</span></span>
* <span data-ttu-id="c7ca9-165">Backup e restauração de VMs criptografadas usando o serviço de Backup do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="c7ca9-165">Backup and restore of encrypted VMs by using hello Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-166">Backup e restauração de VMs criptografadas com suporte apenas para VMs que são criptografados com a configuração de KEK hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="c7ca9-167">Não há suporte em VMs que são criptografados sem KEK.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="c7ca9-168">KEK é um parâmetro opcional que habilita a criptografia de VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="c7ca9-169">o Azure Disk Encryption para VMS IaaS para a solução Windows e Linux inclui:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="c7ca9-170">extensão de criptografia de disco Olá para Windows.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-170">hello disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="c7ca9-171">extensão de criptografia de disco Olá para Linux.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-171">hello disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="c7ca9-172">Olá cmdlets do PowerShell de criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-172">hello disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="c7ca9-173">Olá cmdlets de interface de linha de comando (CLI) do Azure de criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-173">hello disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="c7ca9-174">Olá modelos do Gerenciador de recursos do Azure de criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-174">hello disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="c7ca9-175">Olá solução de criptografia de disco do Azure tem suporte em VMs de IaaS que estejam executando o SO Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-175">hello Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="c7ca9-176">Para obter mais informações sobre sistemas operacionais de saudação com suporte, consulte hello "pré-requisitos" seção.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-176">For more information about hello supported operating systems, see hello "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-177">Não são cobradas taxas adicionais para a criptografia de discos de VM com o Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="c7ca9-178">Proposta de valor</span><span class="sxs-lookup"><span data-stu-id="c7ca9-178">Value proposition</span></span>
<span data-ttu-id="c7ca9-179">Quando você aplica solução Olá gerenciamento de criptografia de disco do Azure, você pode atender Olá necessidades de negócios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-179">When you apply hello Azure Disk Encryption-management solution, you can satisfy hello following business needs:</span></span>

* <span data-ttu-id="c7ca9-180">As VMs de IaaS são protegidas no restante, porque você pode usar a criptografia padrão da indústria tecnologia tooaddress segurança e conformidade requisitos organizacionais.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology tooaddress organizational security and compliance requirements.</span></span>
* <span data-ttu-id="c7ca9-181">As VMs IaaS são inicializadas por meio de políticas e chaves controladas pelo cliente, e você pode auditar seu uso no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="c7ca9-182">Fluxo de trabalho de criptografia</span><span class="sxs-lookup"><span data-stu-id="c7ca9-182">Encryption workflow</span></span>
<span data-ttu-id="c7ca9-183">criptografia de disco tooenable para Windows e VMs do Linux, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-183">tooenable disk encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="c7ca9-184">Escolha um cenário de criptografia entre Olá anterior cenários de criptografia.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-184">Choose an encryption scenario from among hello preceding encryption scenarios.</span></span>
2. <span data-ttu-id="c7ca9-185">Ativar criptografia de disco tooenabling por meio do modelo do Gerenciador de recursos de criptografia de disco do Azure hello, cmdlets do PowerShell ou comando CLI e especificar a configuração de criptografia de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-185">Opt in tooenabling disk encryption via hello Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify hello encryption configuration.</span></span>

   * <span data-ttu-id="c7ca9-186">Para cenário VHD criptografado cliente hello, carregar conta de armazenamento Olá criptografado VHD tooyour e cofre da chave Olá criptografia tooyour material de chave.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-186">For hello customer-encrypted VHD scenario, upload hello encrypted VHD tooyour storage account and hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="c7ca9-187">Em seguida, fornece Olá criptografia configuração tooenable criptografia em uma nova VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-187">Then, provide hello encryption configuration tooenable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="c7ca9-188">Para novas VMs que são criados a partir Olá Marketplace e VMs existentes que já estão em execução no Azure, fornecem criptografia de tooenable de configuração de criptografia Olá sobre Olá IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-188">For new VMs that are created from hello Marketplace and existing VMs that are already running in Azure, provide hello encryption configuration tooenable encryption on hello IaaS VM.</span></span>

3. <span data-ttu-id="c7ca9-189">Conceder acesso toohello plataforma Windows Azure tooread Olá chave de criptografia material (chaves de criptografia do BitLocker para os sistemas Windows) e a frase secreta para Linux da criptografia de tooenable seu Cofre de chaves em Olá IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-189">Grant access toohello Azure platform tooread hello encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault tooenable encryption on hello IaaS VM.</span></span>

4. <span data-ttu-id="c7ca9-190">Fornece hello Azure Active Directory (AD do Azure) aplicativo identidade toowrite Olá criptografia tooyour material de chave Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-190">Provide hello Azure Active Directory (Azure AD) application identity toowrite hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="c7ca9-191">Isso habilita a criptografia em hello IaaS VM para cenários de saudação mencionado na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-191">Doing so enables encryption on hello IaaS VM for hello scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="c7ca9-192">Azure atualiza o modelo de serviço VM Olá com criptografia e a configuração do Cofre de chaves de Olá e define sua VM criptografado.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-192">Azure updates hello VM service model with encryption and hello key vault configuration, and sets up your encrypted VM.</span></span>

 ![Microsoft Antimalware no Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="c7ca9-194">Fluxo de trabalho de descriptografia</span><span class="sxs-lookup"><span data-stu-id="c7ca9-194">Decryption workflow</span></span>
<span data-ttu-id="c7ca9-195">criptografia de disco toodisable para VMs de IaaS, Olá completo seguindo as etapas de alto nível:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-195">toodisable disk encryption for IaaS VMs, complete hello following high-level steps:</span></span>

1. <span data-ttu-id="c7ca9-196">Escolha toodisable criptografia (decodificação) em uma VM IaaS em execução no Azure por meio do modelo do Gerenciador de recursos de criptografia de disco do Azure hello ou cmdlets do PowerShell e especificar a configuração de descriptografia hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-196">Choose toodisable encryption (decryption) on a running IaaS VM in Azure via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify hello decryption configuration.</span></span>

 <span data-ttu-id="c7ca9-197">Esta etapa desabilitará a criptografia do volume de dados de sistema operacional ou Olá Olá ou ambos em Olá executando Windows IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-197">This step disables encryption of hello OS or hello data volume or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="c7ca9-198">No entanto, como mencionado na seção anterior hello, desabilitando a criptografia de disco do sistema operacional para Linux não há suporte.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-198">However, as mentioned in hello previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="c7ca9-199">etapa de descriptografia Olá só é permitida para unidades de dados em VMs do Linux desde que o disco do sistema operacional Olá não está criptografado.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-199">hello decryption step is allowed only for data drives on Linux VMs as long as hello OS disk is not encrypted.</span></span>
2. <span data-ttu-id="c7ca9-200">Atualizações do Azure Olá modelo de serviço VM e Olá IaaS VM está marcado como descriptografada.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-200">Azure updates hello VM service model, and hello IaaS VM is marked decrypted.</span></span> <span data-ttu-id="c7ca9-201">conteúdo de saudação do hello VM não é criptografado em repouso.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-201">hello contents of hello VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-202">operação de criptografia desabilitar Olá não exclui o cofre e hello criptografia chave material de chave (chaves de criptografia do BitLocker para os sistemas Windows) ou a senha para Linux.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-202">hello disable-encryption operation does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="c7ca9-203">Não há suporte para desativação de criptografia de disco de OS para Linux.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="c7ca9-204">etapa de descriptografia Olá só é permitida para unidades de dados em VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-204">hello decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="c7ca9-205">Não há suporte para a desabilitação da criptografia de disco de dados para Linux se Olá unidade do sistema operacional está criptografado.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-205">Disabling data disk encryption for Linux is not supported if hello OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7ca9-206">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c7ca9-206">Prerequisites</span></span>
<span data-ttu-id="c7ca9-207">Antes de habilitar a criptografia de disco do Azure em VMs de IaaS do Azure para cenários de saudação suporte discutidas Olá seção "Visão geral", consulte Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for hello supported scenarios that were discussed in hello "Overview" section, see hello following prerequisites:</span></span>

* <span data-ttu-id="c7ca9-208">Você deve ter um recurso de toocreate válido de assinatura ativa do Azure no Azure em regiões Olá com suporte.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-208">You must have a valid active Azure subscription toocreate resources in Azure in hello supported regions.</span></span>
* <span data-ttu-id="c7ca9-209">Criptografia de disco do Azure tem suporte em Olá seguintes versões do Windows Server: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-209">Azure Disk Encryption is supported on hello following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="c7ca9-210">Criptografia de disco do Azure tem suporte em Olá versões cliente do Windows a seguir: cliente Windows 8 e Windows 10.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-210">Azure Disk Encryption is supported on hello following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-211">Para o Windows Server 2008 R2, você deve ter o .NET Framework 4.5 instalado antes de habilitar a criptografia no Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="c7ca9-212">Você pode instalá-lo a partir do Windows Update pela instalação de atualização opcional de saudação Microsoft .NET Framework 4.5.2 para sistemas baseados em x64 do Windows Server 2008 R2 ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-212">You can install it from Windows Update by installing hello optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="c7ca9-213">Há suporte para criptografia de disco do Azure em Olá seguindo a Galeria do Azure com base em versões e distribuições do Linux server:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-213">Azure Disk Encryption is supported on hello following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="c7ca9-214">Distribuição Linux</span><span class="sxs-lookup"><span data-stu-id="c7ca9-214">Linux Distribution</span></span> | <span data-ttu-id="c7ca9-215">Versão</span><span class="sxs-lookup"><span data-stu-id="c7ca9-215">Version</span></span> | <span data-ttu-id="c7ca9-216">Tipo de Volume com Suporte para Criptografia</span><span class="sxs-lookup"><span data-stu-id="c7ca9-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="c7ca9-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c7ca9-217">Ubuntu</span></span> | <span data-ttu-id="c7ca9-218">16.04-LTS-DIÁRIO</span><span class="sxs-lookup"><span data-stu-id="c7ca9-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="c7ca9-219">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-219">OS and Data disk</span></span> |
| <span data-ttu-id="c7ca9-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c7ca9-220">Ubuntu</span></span> | <span data-ttu-id="c7ca9-221">14.04.5-LTS-DIÁRIO</span><span class="sxs-lookup"><span data-stu-id="c7ca9-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="c7ca9-222">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-222">OS and Data disk</span></span> |
| <span data-ttu-id="c7ca9-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c7ca9-223">Ubuntu</span></span> | <span data-ttu-id="c7ca9-224">12.10</span><span class="sxs-lookup"><span data-stu-id="c7ca9-224">12.10</span></span> | <span data-ttu-id="c7ca9-225">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-225">Data disk</span></span> |
| <span data-ttu-id="c7ca9-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c7ca9-226">Ubuntu</span></span> | <span data-ttu-id="c7ca9-227">12.04</span><span class="sxs-lookup"><span data-stu-id="c7ca9-227">12.04</span></span> | <span data-ttu-id="c7ca9-228">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-228">Data disk</span></span> |
| <span data-ttu-id="c7ca9-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="c7ca9-229">RHEL</span></span> | <span data-ttu-id="c7ca9-230">7.3</span><span class="sxs-lookup"><span data-stu-id="c7ca9-230">7.3</span></span> | <span data-ttu-id="c7ca9-231">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-231">OS and Data disk</span></span> |
| <span data-ttu-id="c7ca9-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="c7ca9-232">RHEL</span></span> | <span data-ttu-id="c7ca9-233">7,2</span><span class="sxs-lookup"><span data-stu-id="c7ca9-233">7.2</span></span> | <span data-ttu-id="c7ca9-234">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-234">OS and Data disk</span></span> |
| <span data-ttu-id="c7ca9-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="c7ca9-235">RHEL</span></span> | <span data-ttu-id="c7ca9-236">6,8</span><span class="sxs-lookup"><span data-stu-id="c7ca9-236">6.8</span></span> | <span data-ttu-id="c7ca9-237">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-237">OS and Data disk</span></span> |
| <span data-ttu-id="c7ca9-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="c7ca9-238">RHEL</span></span> | <span data-ttu-id="c7ca9-239">6.7</span><span class="sxs-lookup"><span data-stu-id="c7ca9-239">6.7</span></span> | <span data-ttu-id="c7ca9-240">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-240">Data disk</span></span> |
| <span data-ttu-id="c7ca9-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7ca9-241">CentOS</span></span> | <span data-ttu-id="c7ca9-242">7.3</span><span class="sxs-lookup"><span data-stu-id="c7ca9-242">7.3</span></span> | <span data-ttu-id="c7ca9-243">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-243">OS and Data disk</span></span> |
| <span data-ttu-id="c7ca9-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7ca9-244">CentOS</span></span> | <span data-ttu-id="c7ca9-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="c7ca9-245">7.2n</span></span> | <span data-ttu-id="c7ca9-246">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-246">OS and Data disk</span></span> |
| <span data-ttu-id="c7ca9-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7ca9-247">CentOS</span></span> | <span data-ttu-id="c7ca9-248">6,8</span><span class="sxs-lookup"><span data-stu-id="c7ca9-248">6.8</span></span> | <span data-ttu-id="c7ca9-249">SO e Disco de Dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-249">OS and Data disk</span></span> |
| <span data-ttu-id="c7ca9-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7ca9-250">CentOS</span></span> | <span data-ttu-id="c7ca9-251">7.1</span><span class="sxs-lookup"><span data-stu-id="c7ca9-251">7.1</span></span> | <span data-ttu-id="c7ca9-252">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-252">Data disk</span></span> |
| <span data-ttu-id="c7ca9-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7ca9-253">CentOS</span></span> | <span data-ttu-id="c7ca9-254">7.0</span><span class="sxs-lookup"><span data-stu-id="c7ca9-254">7.0</span></span> | <span data-ttu-id="c7ca9-255">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-255">Data disk</span></span> |
| <span data-ttu-id="c7ca9-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7ca9-256">CentOS</span></span> | <span data-ttu-id="c7ca9-257">6.7</span><span class="sxs-lookup"><span data-stu-id="c7ca9-257">6.7</span></span> | <span data-ttu-id="c7ca9-258">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-258">Data disk</span></span> |
| <span data-ttu-id="c7ca9-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7ca9-259">CentOS</span></span> | <span data-ttu-id="c7ca9-260">6.6</span><span class="sxs-lookup"><span data-stu-id="c7ca9-260">6.6</span></span> | <span data-ttu-id="c7ca9-261">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-261">Data disk</span></span> |
| <span data-ttu-id="c7ca9-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="c7ca9-262">CentOS</span></span> | <span data-ttu-id="c7ca9-263">6.5</span><span class="sxs-lookup"><span data-stu-id="c7ca9-263">6.5</span></span> | <span data-ttu-id="c7ca9-264">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-264">Data disk</span></span> |
| <span data-ttu-id="c7ca9-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="c7ca9-265">openSUSE</span></span> | <span data-ttu-id="c7ca9-266">13.2</span><span class="sxs-lookup"><span data-stu-id="c7ca9-266">13.2</span></span> | <span data-ttu-id="c7ca9-267">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-267">Data disk</span></span> |
| <span data-ttu-id="c7ca9-268">SLES</span><span class="sxs-lookup"><span data-stu-id="c7ca9-268">SLES</span></span> | <span data-ttu-id="c7ca9-269">12 SP1</span><span class="sxs-lookup"><span data-stu-id="c7ca9-269">12 SP1</span></span> | <span data-ttu-id="c7ca9-270">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-270">Data disk</span></span> |
| <span data-ttu-id="c7ca9-271">SLES</span><span class="sxs-lookup"><span data-stu-id="c7ca9-271">SLES</span></span> | <span data-ttu-id="c7ca9-272">12-SP1 (Premium)</span><span class="sxs-lookup"><span data-stu-id="c7ca9-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="c7ca9-273">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-273">Data disk</span></span> |
| <span data-ttu-id="c7ca9-274">SLES</span><span class="sxs-lookup"><span data-stu-id="c7ca9-274">SLES</span></span> | <span data-ttu-id="c7ca9-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="c7ca9-275">HPC 12</span></span> | <span data-ttu-id="c7ca9-276">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-276">Data disk</span></span> |
| <span data-ttu-id="c7ca9-277">SLES</span><span class="sxs-lookup"><span data-stu-id="c7ca9-277">SLES</span></span> | <span data-ttu-id="c7ca9-278">11-SP4 (Premium)</span><span class="sxs-lookup"><span data-stu-id="c7ca9-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="c7ca9-279">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-279">Data disk</span></span> |
| <span data-ttu-id="c7ca9-280">SLES</span><span class="sxs-lookup"><span data-stu-id="c7ca9-280">SLES</span></span> | <span data-ttu-id="c7ca9-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="c7ca9-281">11 SP4</span></span> | <span data-ttu-id="c7ca9-282">Disco de dados</span><span class="sxs-lookup"><span data-stu-id="c7ca9-282">Data disk</span></span> |

* <span data-ttu-id="c7ca9-283">Criptografia de disco do Azure requer que seu Cofre de chaves e VMs residam em Olá mesma região do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-283">Azure Disk Encryption requires that your key vault and VMs reside in hello same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-284">Configurando recursos de saudação em regiões separadas faz com que uma falha na habilitação do recurso de criptografia de disco do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-284">Configuring hello resources in separate regions causes a failure in enabling hello Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="c7ca9-285">tooset backup e configurar o Cofre de chaves de criptografia de disco do Azure, consulte a seção **definir e configurar o Cofre de chaves de criptografia de disco do Azure** em Olá *pré-requisitos* deste artigo.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-285">tooset up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="c7ca9-286">tooset backup e configurar o aplicativo do AD do Azure no Azure Active directory para criptografia de disco do Azure, consulte a seção **configurar o aplicativo hello AD do Azure no Azure Active Directory** em Olá *pré-requisitos* seção deste artigo.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-286">tooset up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up hello Azure AD application in Azure Active Directory** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="c7ca9-287">tooset backup e configurar política de acesso do Cofre de chaves Olá para o aplicativo hello AD do Azure, consulte a seção **configurar política de acesso do Cofre de chaves Olá para o aplicativo hello AD do Azure** em Olá *pré-requisitos* seção Este artigo.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-287">tooset up and configure hello key vault access policy for hello Azure AD application, see section **Set up hello key vault access policy for hello Azure AD application** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="c7ca9-288">tooprepare um VHD do Windows previamente criptografado, consulte a seção **preparar um VHD do Windows previamente criptografado** em Olá *apêndice*.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-288">tooprepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="c7ca9-289">tooprepare um VHD Linux previamente criptografado, consulte a seção **preparar um VHD Linux pré-criptografado** em Olá *apêndice*.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-289">tooprepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="c7ca9-290">Olá plataforma Windows Azure precisa de chaves de criptografia do acesso toohello ou segredos em seu Cofre de chaves toomake-los disponíveis toohello máquina de virtual quando ele é inicializado e descriptografa o volume do sistema operacional da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-290">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello virtual machine when it boots and decrypts hello virtual machine OS volume.</span></span> <span data-ttu-id="c7ca9-291">plataforma de tooAzure permissões toogrant, Olá conjunto **EnabledForDiskEncryption** propriedade no cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-291">toogrant permissions tooAzure platform, set hello **EnabledForDiskEncryption** property in hello key vault.</span></span> <span data-ttu-id="c7ca9-292">Para obter mais informações, consulte **definir e configurar o Cofre de chaves de criptografia de disco do Azure** em Olá apêndice.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in hello Appendix.</span></span>
* <span data-ttu-id="c7ca9-293">O segredo do cofre de chaves e as URLs KEK devem ter controle de versão.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="c7ca9-294">O Azure impõe essa restrição de controle de versão.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="c7ca9-295">Para um segredo válido e KEK URLs, consulte Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-295">For valid secret and KEK URLs, see hello following examples:</span></span>

  * <span data-ttu-id="c7ca9-296">Exemplo de URL de segredo válida: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="c7ca9-297">Exemplo de URL KEK válida: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="c7ca9-298">o Azure Disk Encryption não dá suporte à especificação de números de portas como parte de segredos do cofre de chaves e URLs KEK.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="c7ca9-299">Para obter exemplos de URLs de Cofre de chaves com suporte e sem suporte, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-299">For examples of non-supported and supported key vault URLs, see hello following:</span></span>

  * <span data-ttu-id="c7ca9-300">URL do cofre de chaves inaceitável *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="c7ca9-301">URL do cofre de chaves aceitável: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="c7ca9-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="c7ca9-302">recurso de criptografia de disco do Azure do tooenable hello, Olá VMs de IaaS deve atender aos Olá seguindo os requisitos de configuração de ponto de extremidade de rede:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-302">tooenable hello Azure Disk Encryption feature, hello IaaS VMs must meet hello following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="c7ca9-303">tooget um cofre de chaves token tooconnect tooyour, Olá IaaS VM deve ser capaz de tooconnect tooan Active Directory do Azure ponto de extremidade \[login.microsoftonline.com\].</span><span class="sxs-lookup"><span data-stu-id="c7ca9-303">tooget a token tooconnect tooyour key vault, hello IaaS VM must be able tooconnect tooan Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="c7ca9-304">toowrite Olá criptografia chaves tooyour Cofre de chaves, Olá IaaS VM deve ser o ponto de extremidade de Cofre de chaves de toohello tooconnect possível.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-304">toowrite hello encryption keys tooyour key vault, hello IaaS VM must be able tooconnect toohello key vault endpoint.</span></span>
  * <span data-ttu-id="c7ca9-305">Olá IaaS VM deve ser capaz de tooconnect tooan armazenamento do Azure ponto de extremidade que hosts Olá repositório de extensão do Azure e uma conta de armazenamento do Azure que hospeda Olá arquivos VHD.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-305">hello IaaS VM must be able tooconnect tooan Azure storage endpoint that hosts hello Azure extension repository and an Azure storage account that hosts hello VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c7ca9-306">Se a política de segurança limita o acesso de VMs do Azure toohello da Internet, poderá resolver Olá precede o URI e configurar toohello de conectividade de saída de tooallow uma regra específica IPs.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-306">If your security policy limits access from Azure VMs toohello Internet, you can resolve hello preceding URI and configure a specific rule tooallow outbound connectivity toohello IPs.</span></span>
  >
  ><span data-ttu-id="c7ca9-307">tooconfigure e acessar o Cofre de chaves do Azure atrás de um firewall (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="c7ca9-307">tooconfigure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="c7ca9-308">Use a versão mais recente de saudação do SDK do Azure PowerShell versão tooconfigure criptografia de disco do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-308">Use hello latest version of Azure PowerShell SDK version tooconfigure Azure Disk Encryption.</span></span> <span data-ttu-id="c7ca9-309">Baixar a versão mais recente de saudação do [versão do PowerShell do Azure](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="c7ca9-309">Download hello latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="c7ca9-310">Não há suporte para o Azure Disk Encryption no [SDK do Azure PowerShell versão 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="c7ca9-311">Se você estiver recebendo um erro relacionado toousing Azure PowerShell 1.1.0, consulte [tooAzure relacionados para erro de criptografia do disco do Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-311">If you are receiving an error related toousing Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="c7ca9-312">toorun qualquer comando CLI do Azure e associá-lo a sua assinatura do Azure, você deve primeiro instalar a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-312">toorun any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="c7ca9-313">tooinstall CLI do Azure e associá-lo a sua assinatura do Azure, consulte [como tooinstall e configurar a CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-313">tooinstall Azure CLI and associate it with your Azure subscription, see [How tooinstall and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="c7ca9-314">toouse CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager, consulte [comandos de CLI do Azure no Gerenciador de recursos de modo](../virtual-machines/azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-314">toouse Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="c7ca9-315">Ao criptografar um disco gerenciado, é obrigatório tootake pré-requisito um instantâneo do disco Olá gerenciado ou um backup de disco Olá fora de criptografia de tooenabling anterior de criptografia de disco do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-315">When encrypting a managed disk, it is mandatory prerequisite tootake a snapshot of hello managed disk or a backup of hello disk outside of Azure Disk Encryption prior tooenabling encryption.</span></span>  <span data-ttu-id="c7ca9-316">Sem um backup em vigor, qualquer falha inesperada durante a criptografia pode renderizar disco hello e VM inacessível sem uma opção de recuperação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-316">Without a backup in place, any unexpected failure during encryption may render hello disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="c7ca9-317">Conjunto AzureRmVMDiskEncryptionExtension atualmente não fazer backup de discos gerenciados e gerarão um erro se usado em um disco gerenciado, a menos que Olá - skipVmBackup parâmetro foi especificado.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless hello -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="c7ca9-318">Esse parâmetro é toouse unsafe, a menos que um backup já foi feito fora de criptografia de disco do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-318">This parameter is unsafe toouse unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="c7ca9-319">Quando Olá - skipVmBackup parâmetro for especificado, Olá cmdlet não fará um backup de tooencryption anterior de disco Olá gerenciado.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-319">When hello -skipVmBackup parameter is specified, hello cmdlet will not make a backup of hello managed disk prior tooencryption.</span></span>  <span data-ttu-id="c7ca9-320">Por esse motivo, é considerada um toomake pré-requisito obrigatório se um backup de disco gerenciado de saudação que VM está em vigor anterior tooenabling criptografia de disco do Azure no caso de recuperação é posterior é necessária.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-320">For this reason, it is considered a mandatory prerequisite toomake sure a backup of hello managed disk VM is in place prior tooenabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="c7ca9-321">parâmetro de skipVmBackup - Olá nunca deve ser usado, a menos que um instantâneo ou backup já foram feito fora de criptografia de disco do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-321">hello -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="c7ca9-322">Olá solução de criptografia de disco do Azure usa o protetor de chave externo Olá BitLocker para VMs de IaaS do Windows.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-322">hello Azure Disk Encryption solution uses hello BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="c7ca9-323">Para VMs ingressadas no domínio, NÃO envie nenhuma política de grupo que imponha protetores de TPM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="c7ca9-324">Para obter informações sobre a política de grupo hello "Permitir BitLocker sem um TPM compatível", consulte [referência de política de grupo do BitLocker](https://technet.microsoft.com/library/ee706521).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-324">For information about hello group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="c7ca9-325">Política do BitLocker em máquinas virtuais de domínio associado com a política de grupo personalizado deve incluir Olá configuração a seguir: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` criptografia de disco do Azure falhará quando as configurações de diretiva de grupo personalizado para o Bitlocker são incompatíveis.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-325">Bitlocker policy on domain joined virtual machines with custom group policy must include hello following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="c7ca9-326">Em computadores que não tinham Olá a configuração de política correta, aplicar a nova política de hello, forçando Olá de nova política tooupdate (gpupdate.exe /force) e, em seguida, reiniciar pode ser necessária.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-326">On machines that did not have hello correct policy setting, applying hello new policy, forcing hello new policy tooupdate (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="c7ca9-327">toocreate um aplicativo do AD do Azure, criar um cofre de chaves, ou configurar um cofre de chave existente e habilitar a criptografia, consulte Olá [script do PowerShell pré-requisito de criptografia de disco do Azure](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-327">toocreate an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see hello [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="c7ca9-328">os pré-requisitos de criptografia de disco tooconfigure usando Olá CLI do Azure, consulte [esse script Bash](https://github.com/ejarvi/ade-cli-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-328">tooconfigure disk-encryption prerequisites using hello Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="c7ca9-329">toouse hello Azure Backup service tooback backup e restauração criptografada VMs, quando a criptografia está habilitada com a criptografia de disco do Azure, criptografam suas VMs usando configuração de chave de criptografia de disco do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-329">toouse hello Azure Backup service tooback up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using hello Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="c7ca9-330">saudação de serviço de Backup oferece suporte a máquinas virtuais que são criptografadas usando apenas a configuração de KEK.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-330">hello Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="c7ca9-331">Consulte [como tooback backup e restauração criptografada máquinas virtuais com criptografia de Backup do Azure](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-331">See [How tooback up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="c7ca9-332">Ao criptografar um volume do sistema operacional Linux, observe que uma reinicialização VM é necessária no final de saudação do processo de saudação no momento.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-332">When encrypting a Linux OS volume, note that a VM restart is currently required at hello end of hello process.</span></span> <span data-ttu-id="c7ca9-333">Isso pode ser feito por meio do portal de hello, powershell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-333">This can be done via hello portal, powershell, or CLI.</span></span>   <span data-ttu-id="c7ca9-334">progresso de saudação tootrack de criptografia, sondar periodicamente a mensagem de saudação do status retornada por Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-334">tootrack hello progress of encryption, periodically poll hello status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="c7ca9-335">Após a conclusão da criptografia, a mensagem de status de Olá Olá retornada por este comando indicará isso.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-335">Once encryption is complete, hello hello status message returned by this command will indicate this.</span></span>  <span data-ttu-id="c7ca9-336">Por exemplo, "ProgressMessage: disco do sistema operacional criptografado com êxito, reinicialize Olá VM" no hello ponto de VM pode ser reiniciada e usada.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot hello VM"  At this point hello VM can be restarted and used.</span></span>  

* <span data-ttu-id="c7ca9-337">Criptografia de disco do Azure para Linux requer dados discos toohave um sistema de arquivos montados em tooencryption anterior do Linux</span><span class="sxs-lookup"><span data-stu-id="c7ca9-337">Azure Disk Encryption for Linux requires data disks toohave a mounted file system in Linux prior tooencryption</span></span>

* <span data-ttu-id="c7ca9-338">Recursivamente discos de dados montados não são suportados pelo Olá criptografia de disco do Azure para Linux.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-338">Recursively mounted data disks are not supported by hello Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="c7ca9-339">Por exemplo, se hello sistema de destino foi montado em um disco em /foo/bar e, em seguida, outro na /foo/bar/baz, criptografia de saudação do /foo/bar/baz terá êxito, mas a criptografia da barra/foo/falhará.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-339">For example, if hello target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, hello encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="c7ca9-340">Imagens da Galeria do Azure com suporte que atendem aos pré-requisitos mencionados acima Olá somente há suporte para criptografia de disco do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet hello aforementioned prerequisites.</span></span> <span data-ttu-id="c7ca9-341">Não há suporte para imagens personalizadas do cliente devido toocustom esquemas de partição e comportamentos de processo que podem existir nessas imagens.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-341">Customer custom images are not supported due toocustom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="c7ca9-342">Além disso, até mesmo VMs baseadas em imagem de galeria que inicialmente atendiam aos pré-requisitos, mas que foram modificadas após a criação, podem ser incompatíveis.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="c7ca9-343">Para que motivo, Olá sugerido procedimento usado para criptografar uma VM do Linux é toostart de uma imagem da Galeria limpa, criptografar Olá VM e, em seguida, adicionar software personalizado ou dados toohello VM conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-343">For that reason, hello suggested procedure for encrypting a Linux VM is toostart from a clean gallery image, encrypt hello VM, and then add custom software or data toohello VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="c7ca9-344">Backup e restauração de VMs criptografadas com suporte apenas para VMs que são criptografados com a configuração de KEK hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="c7ca9-345">Não há suporte em VMs que são criptografados sem KEK.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="c7ca9-346">KEK é um parâmetro opcional que permite VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="c7ca9-347">Configurar Olá aplicativo AD do Azure no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7ca9-347">Set up hello Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="c7ca9-348">Quando você precisar toobe criptografia habilitada em uma VM em execução no Azure, a criptografia de disco do Azure gera e grava o Cofre de chaves do hello criptografia chaves tooyour.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-348">When you need encryption toobe enabled on a running VM in Azure, Azure Disk Encryption generates and writes hello encryption keys tooyour key vault.</span></span> <span data-ttu-id="c7ca9-349">O gerenciamento de chaves de criptografia no cofre de chaves requer a autenticação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="c7ca9-350">Para essa finalidade, crie um aplicativo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="c7ca9-351">Você pode encontrar etapas detalhadas para registrar um aplicativo na seção de "Obter uma identidade Olá aplicativo" hello de postagem de blog Olá [Cofre de chaves do Azure - passo](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-351">You can find detailed steps for registering an application in hello “Get an Identity for hello Application” section of hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="c7ca9-352">Esta postagem também contém vários exemplos úteis para configurar o cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="c7ca9-353">Para fins de autenticação, você pode usar a autenticação baseada em segredo do cliente ou a autenticação Azure AD baseada em certificado do cliente.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="c7ca9-354">Autenticação do Azure AD baseada em segredo do cliente</span><span class="sxs-lookup"><span data-stu-id="c7ca9-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="c7ca9-355">seções Olá a seguir podem ajudá-lo a configurar uma autenticação com base em segredo do cliente do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-355">hello sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="c7ca9-356">Criar um aplicativo Azure AD usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7ca9-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="c7ca9-357">Use Olá toocreate de cmdlet do PowerShell um aplicativo do AD do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-357">Use hello following PowerShell cmdlet toocreate an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="c7ca9-358">$azureAdApplication.ApplicationId é hello ClientID do AD do Azure e $aadClientSecret é o segredo do cliente Olá que você deve usar tooenable posterior a criptografia de disco do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-358">$azureAdApplication.ApplicationId is hello Azure AD ClientID and $aadClientSecret is hello client secret that you should use later tooenable Azure Disk Encryption.</span></span> <span data-ttu-id="c7ca9-359">Proteger adequadamente o segredo do cliente de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-359">Safeguard hello Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a><span data-ttu-id="c7ca9-360">Configuração de ID de cliente de saudação do AD do Azure e o segredo de saudação portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ca9-360">Setting up hello Azure AD client ID and secret from hello Azure classic portal</span></span>
<span data-ttu-id="c7ca9-361">Você também pode configurar sua ID de cliente do AD do Azure e o segredo usando Olá [portal clássico do Azure]( https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-361">You can also set up your Azure AD client ID and secret by using hello [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="c7ca9-362">tooperform task, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-362">tooperform this task, do hello following:</span></span>

1. <span data-ttu-id="c7ca9-363">Clique em Olá **do Active Directory** guia.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-363">Click hello **Active Directory** tab.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="c7ca9-365">Clique em **Adicionar aplicativo**e, em seguida, tipo hello nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-365">Click **Add Application**, and then type hello application name.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="c7ca9-367">Clique o botão de seta hello e, em seguida, configurar propriedades do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-367">Click hello arrow button, and then configure hello application properties.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="c7ca9-369">Clique em marca de seleção Olá Olá toofinish de canto esquerdo inferior.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-369">Click hello check mark in hello lower left corner toofinish.</span></span> <span data-ttu-id="c7ca9-370">página de configuração de aplicativo Hello aparece e ID de cliente do AD do Azure Olá é exibida na parte inferior da saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-370">hello application configuration page appears, and hello Azure AD client ID is displayed at hello bottom of hello page.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="c7ca9-372">Salve o segredo do cliente de saudação do AD do Azure clicando em Olá **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-372">Save hello Azure AD client secret by clicking hello **Save** button.</span></span> <span data-ttu-id="c7ca9-373">Observe o segredo do cliente de saudação do AD do Azure na caixa de texto Olá chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-373">Note hello Azure AD client secret in hello keys text box.</span></span> <span data-ttu-id="c7ca9-374">Proteja-o adequadamente.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-374">Safeguard it appropriately.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="c7ca9-376">Não há suporte para Olá anterior fluxo Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-376">hello preceding flow is not supported on hello Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="c7ca9-377">Usar um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="c7ca9-377">Use an existing application</span></span>
<span data-ttu-id="c7ca9-378">tooexecute Olá comandos a seguir, obtenha e use Olá [módulo PowerShell do AD do Azure](https://technet.microsoft.com/library/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-378">tooexecute hello following commands, obtain and use hello [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-379">Olá comandos a seguir devem ser executados de uma nova janela do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-379">hello following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="c7ca9-380">Não use o Azure PowerShell ou comandos Olá tooexecute da janela de saudação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-380">Do not use Azure PowerShell or hello Azure Resource Manager window tooexecute hello commands.</span></span> <span data-ttu-id="c7ca9-381">Recomendamos essa abordagem porque esses cmdlets no módulo de MSOnline de saudação ou o PowerShell do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-381">We recommend this approach because these cmdlets are in hello MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="c7ca9-382">Autenticação baseada em certificado do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7ca9-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="c7ca9-383">No momento, não há suporte para a autenticação baseada em certificado do Azure AD em VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="c7ca9-384">Olá seções a seguir mostram como tooconfigure uma autenticação baseada em certificado do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-384">hello sections that follow show how tooconfigure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="c7ca9-385">Criar um aplicativo Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7ca9-385">Create an Azure AD application</span></span>
<span data-ttu-id="c7ca9-386">toocreate um aplicativo do AD do Azure, execute Olá cmdlets do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-386">toocreate an Azure AD application, execute hello following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-387">Substitua o seguinte Olá `yourpassword` cadeia de caracteres com sua senha segura e a senha de saudação de proteção.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-387">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="c7ca9-388">Depois de concluir esta etapa, carregar um cofre de chaves de tooyour do arquivo PFX e habilitar Olá acesso política necessária toodeploy tooa esse certificado VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-388">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy needed toodeploy that certificate tooa VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="c7ca9-389">Usar um aplicativo existente do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7ca9-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="c7ca9-390">Se você estiver configurando a autenticação baseada em certificado para um aplicativo existente, use cmdlets do PowerShell Olá mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-390">If you are configuring certificate-based authentication for an existing application, use hello PowerShell cmdlets shown here.</span></span> <span data-ttu-id="c7ca9-391">Ser tooexecute-se de uma nova janela do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-391">Be sure tooexecute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="c7ca9-392">Depois de concluir esta etapa, carregue um cofre de chaves de tooyour do arquivo PFX e habilitar política de acesso de saudação que é necessário toodeploy Olá certificado tooa VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-392">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy that's needed toodeploy hello certificate tooa VM.</span></span>

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a><span data-ttu-id="c7ca9-393">Carregar um cofre de chaves de tooyour do arquivo PFX</span><span class="sxs-lookup"><span data-stu-id="c7ca9-393">Upload a PFX file tooyour key vault</span></span>
<span data-ttu-id="c7ca9-394">Para obter uma explicação detalhada desse processo, consulte [Olá oficial Blog da equipe do Azure Key Vault](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-394">For a detailed explanation of this process, see [hello Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="c7ca9-395">No entanto, Olá cmdlets do PowerShell a seguir é tudo o que precisa para tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-395">However, hello following PowerShell cmdlets are all you need for hello task.</span></span> <span data-ttu-id="c7ca9-396">Ser tooexecute se-las no console do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-396">Be sure tooexecute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-397">Substitua o seguinte Olá `yourpassword` cadeia de caracteres com sua senha segura e a senha de saudação de proteção.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-397">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

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

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a><span data-ttu-id="c7ca9-398">Implante um certificado em seu tooan de Cofre de chaves existente VM</span><span class="sxs-lookup"><span data-stu-id="c7ca9-398">Deploy a certificate in your key vault tooan existing VM</span></span>
<span data-ttu-id="c7ca9-399">Depois de terminar de carregar Olá PFX, implante um certificado no hello tooan de Cofre de chaves existente VM com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-399">After you finish uploading hello PFX, deploy a certificate in hello key vault tooan existing VM with hello following:</span></span>
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

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a><span data-ttu-id="c7ca9-400">Definir a política de acesso do Cofre de chaves Olá para o aplicativo hello AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ca9-400">Set up hello key vault access policy for hello Azure AD application</span></span>
<span data-ttu-id="c7ca9-401">Seu aplicativo do AD do Azure precisa de direitos tooaccess Olá as chaves ou os segredos no cofre hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-401">Your Azure AD application needs rights tooaccess hello keys or secrets in hello vault.</span></span> <span data-ttu-id="c7ca9-402">Saudação de uso [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permissões toohello aplicativo usando a ID do cliente hello (que foi gerado quando o aplicativo hello foi registrado) como Olá _– ServicePrincipalName_ valor do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-402">Use hello [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permissions toohello application, using hello client ID (which was generated when hello application was registered) as hello _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="c7ca9-403">toolearn mais, consulte Olá postagem de blog [Cofre de chaves do Azure - passo](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-403">toolearn more, see hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="c7ca9-404">Aqui está um exemplo de como tooperform essa tarefa por meio do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-404">Here is an example of how tooperform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="c7ca9-405">Criptografia de disco do Azure requer Olá tooconfigure após o aplicativo de cliente de tooyour AD do Azure de políticas de acesso: _WrapKey_ e _definir_ permissões.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-405">Azure Disk Encryption requires you tooconfigure hello following access policies tooyour Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="c7ca9-406">Terminologia</span><span class="sxs-lookup"><span data-stu-id="c7ca9-406">Terminology</span></span>
<span data-ttu-id="c7ca9-407">toounderstand alguns dos termos comuns Olá usados por esta tecnologia, use Olá terminologia a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-407">toounderstand some of hello common terms used by this technology, use hello following terminology table:</span></span>

| <span data-ttu-id="c7ca9-408">Terminologia</span><span class="sxs-lookup"><span data-stu-id="c7ca9-408">Terminology</span></span> | <span data-ttu-id="c7ca9-409">Definição</span><span class="sxs-lookup"><span data-stu-id="c7ca9-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="c7ca9-410">AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ca9-410">Azure AD</span></span> | <span data-ttu-id="c7ca9-411">Azure AD significa [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="c7ca9-412">Uma conta do Azure AD é um pré-requisito para autenticar, armazenar e recuperar segredos do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="c7ca9-413">Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ca9-413">Azure Key Vault</span></span> | <span data-ttu-id="c7ca9-414">O Key Vault é um serviço de gerenciamento de chaves criptográfico baseado em módulos de segurança de hardware validados pelo FIPS (Federal Information Processing Standards), que ajuda a proteger as chaves criptográficas e os segredos confidenciais.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="c7ca9-415">Para obter mais informações, confira a documentação do [Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="c7ca9-416">ARM</span><span class="sxs-lookup"><span data-stu-id="c7ca9-416">ARM</span></span> | <span data-ttu-id="c7ca9-417">Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ca9-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="c7ca9-418">BitLocker</span><span class="sxs-lookup"><span data-stu-id="c7ca9-418">BitLocker</span></span> |<span data-ttu-id="c7ca9-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) é uma reconhecido Windows volume tecnologia de criptografia que foi usada criptografia de disco tooenable em VMs de IaaS do Windows.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used tooenable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="c7ca9-420">BEK</span><span class="sxs-lookup"><span data-stu-id="c7ca9-420">BEK</span></span> | <span data-ttu-id="c7ca9-421">Chaves de criptografia do BitLocker são volume de inicialização Olá SO tooencrypt usados e os volumes de dados.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-421">BitLocker encryption keys are used tooencrypt hello OS boot volume and data volumes.</span></span> <span data-ttu-id="c7ca9-422">chaves do BitLocker Olá são protegidas em um cofre de chaves como segredos.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-422">hello BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="c7ca9-423">CLI</span><span class="sxs-lookup"><span data-stu-id="c7ca9-423">CLI</span></span> | <span data-ttu-id="c7ca9-424">Confira [Interface de linha de comando do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="c7ca9-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="c7ca9-425">DM-Crypt</span></span> |<span data-ttu-id="c7ca9-426">[DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) é subsistema de criptografia transparente de disco com base em Linux Olá que usou a criptografia de disco tooenable em VMs de IaaS do Linux.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is hello Linux-based, transparent disk-encryption subsystem that's used tooenable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="c7ca9-427">KEK</span><span class="sxs-lookup"><span data-stu-id="c7ca9-427">KEK</span></span> | <span data-ttu-id="c7ca9-428">Chave de criptografia de chave é Olá chave assimétrica (RSA de 2048) que você pode usar tooprotect ou encapsular segredo hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-428">Key encryption key is hello asymmetric key (RSA 2048) that you can use tooprotect or wrap hello secret.</span></span> <span data-ttu-id="c7ca9-429">Você pode fornecer uma chave protegida por HSM (módulos de segurança de hardware) ou uma chave protegida por software.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="c7ca9-430">Para obter mais detalhes, confira a [documentação do Azure Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="c7ca9-431">Cmdlets de DNS</span><span class="sxs-lookup"><span data-stu-id="c7ca9-431">PS cmdlets</span></span> | <span data-ttu-id="c7ca9-432">Confira [Cmdlets do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="c7ca9-433">Instalar e configurar o cofre de chaves de Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="c7ca9-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="c7ca9-434">Criptografia de disco do Azure ajuda a proteger chaves de criptografia de disco de hello e segredos no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-434">Azure Disk Encryption helps safeguard hello disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="c7ca9-435">tooset o seu Cofre de chaves de criptografia de disco do Azure, Olá concluído as etapas em cada uma das seguintes seções de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-435">tooset up your key vault for Azure Disk Encryption, complete hello steps in each of hello following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="c7ca9-436">Criar um cofre de chave</span><span class="sxs-lookup"><span data-stu-id="c7ca9-436">Create a key vault</span></span>
<span data-ttu-id="c7ca9-437">toocreate um cofre de chaves, use um dos Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-437">toocreate a key vault, use one of hello following options:</span></span>

* [<span data-ttu-id="c7ca9-438">Modelo "101-Key-Vault-Create" do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c7ca9-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="c7ca9-439">Cmdlets do cofre de chaves do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7ca9-439">Azure PowerShell key vault cmdlets</span></span>](/powershell/module/azurerm.keyvault/#key_vault)
* <span data-ttu-id="c7ca9-440">Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ca9-440">Azure Resource Manager</span></span>
* <span data-ttu-id="c7ca9-441">Como muito[proteger seu Cofre de chaves](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="c7ca9-441">How too[Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-442">Se você já tiver configurado um cofre de chaves para sua assinatura, ignore toohello próxima seção.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-442">If you have already set up a key vault for your subscription, skip toohello next section.</span></span>

![Cofre da Chave do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="c7ca9-444">Configurar uma chave de criptografia de chave (opcional)</span><span class="sxs-lookup"><span data-stu-id="c7ca9-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="c7ca9-445">Se você quiser toouse uma KEK para uma camada adicional de segurança para chaves de criptografia do BitLocker Olá, adicione um cofre de chaves do KEK tooyour.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-445">If you want toouse a KEK for an additional layer of security for hello BitLocker encryption keys, add a KEK tooyour key vault.</span></span> <span data-ttu-id="c7ca9-446">Saudação de uso [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) toocreate cmdlet uma chave de criptografia de chave no cofre de chave hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-446">Use hello [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate a key encryption key in hello key vault.</span></span> <span data-ttu-id="c7ca9-447">Você também pode importar a KEK do HSM do gerenciamento de chaves local.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="c7ca9-448">Para obter mais detalhes, confira a [Documentação do Key Vault](https://azure.microsoft.com/documentation/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="c7ca9-449">Você pode adicionar Olá KEK indo tooAzure Gerenciador de recursos ou usando a interface do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-449">You can add hello KEK by going tooAzure Resource Manager or by using your key vault interface.</span></span>

![Cofre da Chave do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="c7ca9-451">Definir permissões de cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="c7ca9-451">Set key vault permissions</span></span>
<span data-ttu-id="c7ca9-452">Olá plataforma Windows Azure precisa de chaves de criptografia do acesso toohello ou segredos em seu Cofre de chaves toomake-los disponível toohello VM para inicializar e descriptografia de volumes de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-452">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello VM for booting and decrypting hello volumes.</span></span> <span data-ttu-id="c7ca9-453">toogrant permissões toohello plataforma Windows Azure, Olá conjunto **EnabledForDiskEncryption** propriedade na chave Olá cofre usando o cmdlet do PowerShell Olá Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-453">toogrant permissions toohello Azure platform, set hello **EnabledForDiskEncryption** property in hello key vault by using hello key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="c7ca9-454">Você também pode definir Olá **EnabledForDiskEncryption** propriedade visitando Olá [Gerenciador de recursos do Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-454">You can also set hello **EnabledForDiskEncryption** property by visiting hello [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="c7ca9-455">Como mencionado anteriormente, você deve definir Olá **EnabledForDiskEncryption** propriedade em seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-455">As mentioned earlier, you must set hello **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="c7ca9-456">Caso contrário, ocorrerá falha na implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-456">Otherwise, hello deployment will fail.</span></span>

<span data-ttu-id="c7ca9-457">Você pode configurar políticas de acesso para seu aplicativo do AD do Azure na interface do Cofre de chaves hello, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-457">You can set up access policies for your Azure AD application from hello key vault interface, as shown here:</span></span>

![Cofre da Chave do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Cofre da Chave do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="c7ca9-460">Em Olá **políticas de acesso avançados** guia, certifique-se de que seu Cofre de chaves está habilitado para criptografia de disco do Azure:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-460">On hello **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Cofre de chaves do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="c7ca9-462">Cenários de implantação de criptografia de disco e experiências de usuário</span><span class="sxs-lookup"><span data-stu-id="c7ca9-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="c7ca9-463">Você pode habilitar muitos cenários de criptografia de disco e etapas de saudação podem variar de acordo cenário de toohello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-463">You can enable many disk-encryption scenarios, and hello steps may vary according toohello scenario.</span></span> <span data-ttu-id="c7ca9-464">Olá, seções a seguir abordam os cenários hello mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-464">hello following sections cover hello scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a><span data-ttu-id="c7ca9-465">Habilitar a criptografia em novas VMs de IaaS que são criados a partir Olá Marketplace</span><span class="sxs-lookup"><span data-stu-id="c7ca9-465">Enable encryption on new IaaS VMs that are created from hello Marketplace</span></span>
<span data-ttu-id="c7ca9-466">Você pode habilitar a criptografia de disco em nova VM do Windows IaaS de saudação Marketplace no Azure usando Olá [modelo do Gerenciador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-466">You can enable disk encryption on new IaaS Windows VM from hello Marketplace in Azure by using hello  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="c7ca9-467">No modelo de saudação de início rápido do Azure, clique em **implantar tooAzure**, insira a configuração de criptografia de saudação em Olá **parâmetros** folha e depois clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-467">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="c7ca9-468">Selecione a assinatura hello, grupo de recursos, local do grupo de recursos, os termos legais e contrato e, em seguida, clique em **criar** tooenable criptografia em uma nova VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-468">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-469">Este modelo cria uma nova VM criptografado do Windows que usa a imagem da Galeria Olá Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-469">This template creates a new encrypted Windows VM that uses hello Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="c7ca9-470">Você pode habilitar a criptografia de disco em uma nova VM IaaS do RedHat Linux 7.2 com uma matriz RAID 0 de 200 GB usando esse [modelo do Gerenciador de Recursos](https://aka.ms/fde-rhel).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="c7ca9-471">Depois de implantar o modelo hello, verificar o status de criptografia de VM de saudação usando Olá `Get-AzureRmVmDiskEncryptionStatus` cmdlet, conforme descrito em [SO com criptografia de unidade em uma VM do Linux em execução](#encrypting-os-drive-on-a-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-471">After you deploy hello template, verify hello VM encryption status by using hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="c7ca9-472">Quando a máquina Olá retorna um status de _VMRestartPending_, reinicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-472">When hello machine returns a status of _VMRestartPending_, restart hello VM.</span></span>

<span data-ttu-id="c7ca9-473">Olá tabela a seguir lista parâmetros de modelo do Gerenciador de recursos de saudação para novas VMs do cenário do Marketplace hello usando uma ID de cliente do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-473">hello following table lists hello Resource Manager template parameters for new VMs from hello Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="c7ca9-474">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c7ca9-474">Parameter</span></span> | <span data-ttu-id="c7ca9-475">Descrição</span><span class="sxs-lookup"><span data-stu-id="c7ca9-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7ca9-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="c7ca9-476">adminUserName</span></span> | <span data-ttu-id="c7ca9-477">Nome de usuário de administrador para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-477">Admin user name for hello virtual machine.</span></span> |
| <span data-ttu-id="c7ca9-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="c7ca9-478">adminPassword</span></span> | <span data-ttu-id="c7ca9-479">Senha do usuário administrador da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-479">Admin user password for hello virtual machine.</span></span> |
| <span data-ttu-id="c7ca9-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="c7ca9-480">newStorageAccountName</span></span> | <span data-ttu-id="c7ca9-481">Nome do toostore de conta de armazenamento Olá SO e VHDs de dados.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-481">Name of hello storage account toostore OS and data VHDs.</span></span> |
| <span data-ttu-id="c7ca9-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="c7ca9-482">vmSize</span></span> | <span data-ttu-id="c7ca9-483">Tamanho da VM de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-483">Size of hello VM.</span></span> <span data-ttu-id="c7ca9-484">Atualmente, há suporte somente para séries Standard A, D e G.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="c7ca9-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="c7ca9-485">virtualNetworkName</span></span> | <span data-ttu-id="c7ca9-486">Nome de rede virtual que Olá NIC de VM do hello deve pertencer ao.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-486">Name of hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="c7ca9-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="c7ca9-487">subnetName</span></span> | <span data-ttu-id="c7ca9-488">Nome da sub-rede Olá Olá VNet que Olá NIC de VM deve pertencer ao.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-488">Name of hello subnet in hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="c7ca9-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="c7ca9-489">AADClientID</span></span> | <span data-ttu-id="c7ca9-490">ID do cliente do aplicativo de saudação do AD do Azure que tenha permissões toowrite segredos tooyour chave de cofre.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-490">Client ID of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="c7ca9-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="c7ca9-491">AADClientSecret</span></span> | <span data-ttu-id="c7ca9-492">Segredo do cliente do aplicativo de saudação do AD do Azure que tenha permissões toowrite segredos tooyour chave de cofre.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-492">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="c7ca9-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="c7ca9-493">keyVaultURL</span></span> | <span data-ttu-id="c7ca9-494">URL da chave Olá cofre que Olá BitLocker chave deve ser carregada.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-494">URL of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="c7ca9-495">Você pode obtê-lo usando o cmdlet Olá `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-495">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="c7ca9-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="c7ca9-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="c7ca9-497">URL da chave de criptografia de chave de saudação que é usado tooencrypt hello gerada chave do BitLocker (opcional).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-497">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="c7ca9-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c7ca9-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="c7ca9-499">Grupo de recursos do Cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-499">Resource group of hello key vault.</span></span> |
| <span data-ttu-id="c7ca9-500">vmName</span><span class="sxs-lookup"><span data-stu-id="c7ca9-500">vmName</span></span> | <span data-ttu-id="c7ca9-501">Nome da saudação VM Olá a operação de criptografia é toobe executada em.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-501">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="c7ca9-502">_KeyEncryptionKeyURL_ é um parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="c7ca9-503">Você pode colocar sua própria chave de dados criptografia do KEK toofurther proteção hello (senha secreta) em seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-503">You can bring your own KEK toofurther safeguard hello data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="c7ca9-504">Habilite a criptografia na nova VM IaaS criada usando VHD criptografado pelo cliente e chaves de criptografia</span><span class="sxs-lookup"><span data-stu-id="c7ca9-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="c7ca9-505">Nesse cenário, você pode habilitar a criptografia usando o modelo do Gerenciador de recursos de hello, cmdlets do PowerShell ou CLI comandos.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-505">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="c7ca9-506">Olá seções a seguir explicam em modelo de Gerenciador de recursos do maior detalhe hello e comandos CLI.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-506">hello following sections explain in greater detail hello Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="c7ca9-507">Siga as instruções de saudação de uma dessas seções para preparar imagens previamente criptografadas que podem ser usadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-507">Follow hello instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="c7ca9-508">Após a criação de imagem Olá, você pode usar etapas Olá Olá toocreate próximo da seção uma VM do Azure criptografados.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-508">After hello image is created, you can use hello steps in hello next section toocreate an encrypted Azure VM.</span></span>

* [<span data-ttu-id="c7ca9-509">Preparar um VHD do Windows previamente criptografado</span><span class="sxs-lookup"><span data-stu-id="c7ca9-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="c7ca9-510">Preparar um VHD Linux previamente criptografado</span><span class="sxs-lookup"><span data-stu-id="c7ca9-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="c7ca9-511">Usando o modelo do Gerenciador de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="c7ca9-511">Using hello Resource Manager template</span></span>
<span data-ttu-id="c7ca9-512">Você pode habilitar a criptografia de disco em seu VHD criptografado usando Olá [modelo do Gerenciador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-512">You can enable disk encryption on your encrypted VHD by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="c7ca9-513">No modelo de saudação de início rápido do Azure, clique em **implantar tooAzure**, insira a configuração de criptografia de saudação em Olá **parâmetros** folha e depois clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-513">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="c7ca9-514">Selecione a assinatura hello, grupo de recursos, local do grupo de recursos, os termos legais e contrato e, em seguida, clique em **criar** tooenable criptografia em Olá nova VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-514">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello new IaaS VM.</span></span>

<span data-ttu-id="c7ca9-515">Olá tabela a seguir lista parâmetros de modelo do Gerenciador de recursos de saudação para seu VHD criptografado:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-515">hello following table lists hello Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="c7ca9-516">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c7ca9-516">Parameter</span></span> | <span data-ttu-id="c7ca9-517">Descrição</span><span class="sxs-lookup"><span data-stu-id="c7ca9-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7ca9-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="c7ca9-518">newStorageAccountName</span></span> | <span data-ttu-id="c7ca9-519">Nome do Olá Olá de toostore de conta de armazenamento criptografado VHD do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-519">Name of hello storage account toostore hello encrypted OS VHD.</span></span> <span data-ttu-id="c7ca9-520">Esta conta de armazenamento deve já ter sido criada no hello mesmo grupo de recursos e no mesmo local que Olá VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-520">This storage account should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="c7ca9-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="c7ca9-521">osVhdUri</span></span> | <span data-ttu-id="c7ca9-522">URI da saudação VHD do sistema operacional da conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-522">URI of hello OS VHD from hello storage account.</span></span> |
| <span data-ttu-id="c7ca9-523">osType</span><span class="sxs-lookup"><span data-stu-id="c7ca9-523">osType</span></span> | <span data-ttu-id="c7ca9-524">Tipo de produto do sistema operacional (Windows/Linux).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="c7ca9-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="c7ca9-525">virtualNetworkName</span></span> | <span data-ttu-id="c7ca9-526">Nome de rede virtual que Olá NIC de VM do hello deve pertencer ao.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-526">Name of hello VNet that hello VM NIC should belong to.</span></span> <span data-ttu-id="c7ca9-527">Olá nome deve já ter sido criado no hello mesmo grupo de recursos e no mesmo local que Olá VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-527">hello name should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="c7ca9-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="c7ca9-528">subnetName</span></span> | <span data-ttu-id="c7ca9-529">Nome da sub-rede Olá Olá VNet que Olá NIC de VM deve pertencer ao.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-529">Name of hello subnet on hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="c7ca9-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="c7ca9-530">vmSize</span></span> | <span data-ttu-id="c7ca9-531">Tamanho da VM de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-531">Size of hello VM.</span></span> <span data-ttu-id="c7ca9-532">Atualmente, há suporte somente para séries Standard A, D e G.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="c7ca9-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="c7ca9-533">keyVaultResourceID</span></span> | <span data-ttu-id="c7ca9-534">Olá ResourceID que identifica o recurso de Cofre de chaves Olá no Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-534">hello ResourceID that identifies hello key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="c7ca9-535">Você pode obtê-lo usando o cmdlet do PowerShell Olá `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-535">You can get it by using hello PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="c7ca9-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="c7ca9-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="c7ca9-537">URL da chave de criptografia de disco Olá configurado no cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-537">URL of hello disk-encryption key that's set up in hello key vault.</span></span> |
| <span data-ttu-id="c7ca9-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="c7ca9-538">keyVaultKekUrl</span></span> | <span data-ttu-id="c7ca9-539">URL Olá chave da chave de criptografia para criptografar a chave de criptografia de disco Olá gerado.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-539">URL of hello key encryption key for encrypting hello generated disk-encryption key.</span></span> |
| <span data-ttu-id="c7ca9-540">vmName</span><span class="sxs-lookup"><span data-stu-id="c7ca9-540">vmName</span></span> | <span data-ttu-id="c7ca9-541">Nome da saudação IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-541">Name of hello IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="c7ca9-542">Usando os cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7ca9-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="c7ca9-543">Você pode habilitar a criptografia de disco em seu VHD criptografado usando o cmdlet do PowerShell Olá [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-543">You can enable disk encryption on your encrypted VHD by using hello PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="c7ca9-544">Usando comandos da CLI</span><span class="sxs-lookup"><span data-stu-id="c7ca9-544">Using CLI commands</span></span>
<span data-ttu-id="c7ca9-545">criptografia de disco tooenable para este cenário, usando os comandos CLI, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-545">tooenable disk encryption for this scenario by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="c7ca9-546">Definir políticas de acesso no cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="c7ca9-547">Saudação de conjunto **EnabledForDiskEncryption** sinalizador:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-547">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="c7ca9-548">Conjunto de permissões tooAzure AD aplicativo toowrite segredos tooyour Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-548">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="c7ca9-549">criptografia tooenable em uma VM existente ou em execução, tipo:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-549">tooenable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="c7ca9-550">Obtenha o status de criptografia:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="c7ca9-551">criptografia de tooenable em uma nova VM em seu VHD criptografado, Olá use parâmetros com hello a seguir `azure vm create` comando:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-551">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="c7ca9-552">Habilitar a criptografia na VM IaaS do Windows existente ou em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="c7ca9-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="c7ca9-553">Nesse cenário, você pode habilitar a criptografia usando o modelo do Gerenciador de recursos de hello, cmdlets do PowerShell ou CLI comandos.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-553">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="c7ca9-554">Olá seções a seguir explicam mais detalhadamente como tooenable usando Olá modelo do Gerenciador de recursos e comandos CLI.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-554">hello following sections explain in greater detail how tooenable it by using hello Resource Manager template and CLI commands.</span></span>

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="c7ca9-555">Usando o modelo do Gerenciador de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="c7ca9-555">Using hello Resource Manager template</span></span>
<span data-ttu-id="c7ca9-556">Você pode habilitar a criptografia de disco existente ou VMs de IaaS do Windows em execução no Azure usando Olá [modelo do Gerenciador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="c7ca9-557">No modelo de saudação de início rápido do Azure, clique em **implantar tooAzure**, insira a configuração de criptografia de saudação em Olá **parâmetros** folha e depois clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-557">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="c7ca9-558">Selecione a assinatura hello, grupo de recursos, local do grupo de recursos, os termos legais e contrato e, em seguida, clique em **criar** tooenable criptografia Olá existente ou executando o IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-558">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="c7ca9-559">Hello tabela a seguir lista os parâmetros de modelo do Gerenciador de recursos Olá para existente ou a execução de máquinas virtuais que usam uma ID de cliente do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-559">hello following table lists hello Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="c7ca9-560">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c7ca9-560">Parameter</span></span> | <span data-ttu-id="c7ca9-561">Descrição</span><span class="sxs-lookup"><span data-stu-id="c7ca9-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7ca9-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="c7ca9-562">AADClientID</span></span> | <span data-ttu-id="c7ca9-563">ID do cliente do aplicativo de saudação do AD do Azure que tenha permissões toowrite segredos toohello chave de cofre.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-563">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="c7ca9-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="c7ca9-564">AADClientSecret</span></span> | <span data-ttu-id="c7ca9-565">Segredo do cliente do aplicativo de saudação do AD do Azure que tenha permissões toowrite segredos toohello chave de cofre.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-565">Client secret of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="c7ca9-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="c7ca9-566">keyVaultName</span></span> | <span data-ttu-id="c7ca9-567">Nome da chave de saudação cofre que Olá BitLocker chave deve ser carregada.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-567">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="c7ca9-568">Você pode obtê-lo usando o cmdlet Olá `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-568">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="c7ca9-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="c7ca9-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="c7ca9-570">URL da chave de criptografia de chave de saudação que é usado tooencrypt hello gerada chave do BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-570">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="c7ca9-571">Esse parâmetro é opcional se você selecionar **nokek** na lista de saudação UseExistingKek lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-571">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="c7ca9-572">Se você selecionar **kek** na lista de saudação UseExistingKek lista suspensa, você deve inserir Olá _keyEncryptionKeyURL_ valor.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-572">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="c7ca9-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="c7ca9-573">volumeType</span></span> | <span data-ttu-id="c7ca9-574">Tipo de volume Olá criptografia operação é executada.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-574">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="c7ca9-575">Os valores válidos são _OS_, _Data_ e _All_.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="c7ca9-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="c7ca9-576">sequenceVersion</span></span> | <span data-ttu-id="c7ca9-577">Versão da sequência de saudação operação do BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-577">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="c7ca9-578">Aumentar esse número de versão toda vez que uma operação de criptografia de disco é executada em Olá mesma VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-578">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="c7ca9-579">vmName</span><span class="sxs-lookup"><span data-stu-id="c7ca9-579">vmName</span></span> | <span data-ttu-id="c7ca9-580">Nome da saudação VM Olá a operação de criptografia é toobe executada em.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-580">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="c7ca9-581">_KeyEncryptionKeyURL_ é um parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="c7ca9-582">Você pode trazer sua própria chave de dados criptografia do KEK toofurther proteção hello (secreta de criptografia do BitLocker) no cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-582">You can bring your own KEK toofurther safeguard hello data encryption key (BitLocker encryption secret) in hello key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="c7ca9-583">Usando os cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7ca9-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="c7ca9-584">Para obter informações sobre como habilitar a criptografia com criptografia de disco do Azure usando cmdlets do PowerShell, consulte as postagens de blog de saudação [explorar criptografia de disco do Azure com o Azure PowerShell - parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) e [explorar criptografia de disco do Azure com o Azure PowerShell - parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="c7ca9-585">Usando comandos da CLI</span><span class="sxs-lookup"><span data-stu-id="c7ca9-585">Using CLI commands</span></span>
<span data-ttu-id="c7ca9-586">criptografia tooenable existente ou executando o IaaS VM do Windows no Azure usando comandos CLI, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-586">tooenable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="c7ca9-587">políticas de acesso tooset no cofre de chaves hello:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-587">tooset access policies in hello key vault:</span></span>
   * <span data-ttu-id="c7ca9-588">Saudação de conjunto **EnabledForDiskEncryption** sinalizador:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-588">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="c7ca9-589">Conjunto de permissões tooAzure AD aplicativo toowrite segredos tooyour Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-589">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="c7ca9-590">criptografia tooenable em uma VM existente ou em execução:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-590">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="c7ca9-591">status da criptografia tooget:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-591">tooget encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="c7ca9-592">criptografia de tooenable em uma nova VM em seu VHD criptografado, Olá use parâmetros com hello a seguir `azure vm create` comando:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-592">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="c7ca9-593">Habilitar a criptografia em uma VM IaaS do Linux existente ou em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="c7ca9-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="c7ca9-594">Você pode habilitar a criptografia de disco em uma VM do Linux de IaaS existentes ou em execução no Azure usando Olá [modelo do Gerenciador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="c7ca9-595">Clique em **implantar tooAzure** no modelo Olá início rápido do Azure, insira configuração de criptografia Olá nas Olá **parâmetros** folha e depois clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-595">Click **Deploy tooAzure** on hello Azure quick-start template, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="c7ca9-596">Selecione a assinatura hello, grupo de recursos, local do grupo de recursos, os termos legais e contrato e, em seguida, clique em **criar** tooenable criptografia Olá existente ou executando o IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-596">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="c7ca9-597">Olá, a tabela a seguir lista os parâmetros de modelo do Gerenciador de recursos para existente ou a execução de máquinas virtuais que usam uma ID de cliente do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-597">hello following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="c7ca9-598">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c7ca9-598">Parameter</span></span> | <span data-ttu-id="c7ca9-599">Descrição</span><span class="sxs-lookup"><span data-stu-id="c7ca9-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7ca9-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="c7ca9-600">AADClientID</span></span> | <span data-ttu-id="c7ca9-601">ID do cliente do aplicativo de saudação do AD do Azure que tenha permissões toowrite segredos toohello chave de cofre.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-601">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="c7ca9-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="c7ca9-602">AADClientSecret</span></span> | <span data-ttu-id="c7ca9-603">Segredo do cliente do aplicativo de saudação do AD do Azure que tenha permissões toowrite segredos tooyour chave de cofre.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-603">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="c7ca9-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="c7ca9-604">keyVaultName</span></span> | <span data-ttu-id="c7ca9-605">Nome da chave de saudação cofre que Olá BitLocker chave deve ser carregada.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-605">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="c7ca9-606">Você pode obtê-lo usando o cmdlet Olá `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-606">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="c7ca9-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="c7ca9-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="c7ca9-608">URL da chave de criptografia de chave de saudação que é usado tooencrypt hello gerada chave do BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-608">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="c7ca9-609">Esse parâmetro é opcional se você selecionar **nokek** na lista de saudação UseExistingKek lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-609">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="c7ca9-610">Se você selecionar **kek** na lista de saudação UseExistingKek lista suspensa, você deve inserir Olá _keyEncryptionKeyURL_ valor.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-610">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="c7ca9-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="c7ca9-611">volumeType</span></span> | <span data-ttu-id="c7ca9-612">Tipo de volume Olá criptografia operação é executada.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-612">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="c7ca9-613">Os valores válidos com suporte são _OS_ ou _Todos_ (para RHEL 7.2, CentOS 7.2 e Ubuntu 16.04) e _Dados_ (para todas as outras distribuições).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="c7ca9-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="c7ca9-614">sequenceVersion</span></span> | <span data-ttu-id="c7ca9-615">Versão da sequência de saudação operação do BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-615">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="c7ca9-616">Aumentar esse número de versão toda vez que uma operação de criptografia de disco é executada em Olá mesma VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-616">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="c7ca9-617">vmName</span><span class="sxs-lookup"><span data-stu-id="c7ca9-617">vmName</span></span> | <span data-ttu-id="c7ca9-618">Nome da saudação VM Olá a operação de criptografia é toobe executada em.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-618">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |
| <span data-ttu-id="c7ca9-619">Senha</span><span class="sxs-lookup"><span data-stu-id="c7ca9-619">passPhrase</span></span> | <span data-ttu-id="c7ca9-620">Digite uma senha forte como chave de criptografia de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-620">Type a strong passphrase as hello data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="c7ca9-621">_KeyEncryptionKeyURL_ é um parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="c7ca9-622">Você pode colocar sua própria chave de dados criptografia do KEK toofurther proteção hello (senha secreta) em seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-622">You can bring your own KEK toofurther safeguard hello data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="c7ca9-623">Comandos de CLI</span><span class="sxs-lookup"><span data-stu-id="c7ca9-623">CLI commands</span></span>
<span data-ttu-id="c7ca9-624">Você pode habilitar a criptografia de disco em seu VHD criptografado instalando e usando Olá [comando CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-624">You can enable disk encryption on your encrypted VHD by installing and using hello [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="c7ca9-625">criptografia tooenable existente ou IaaS Linux VMs em execução no Azure usando comandos CLI, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-625">tooenable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="c7ca9-626">Definir políticas de acesso no cofre de chaves hello:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-626">Set access policies in hello key vault:</span></span>

 * <span data-ttu-id="c7ca9-627">Saudação de conjunto **EnabledForDiskEncryption** sinalizador:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-627">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="c7ca9-628">Conjunto de permissões tooAzure AD aplicativo toowrite segredos tooyour Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-628">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="c7ca9-629">criptografia tooenable em uma VM existente ou em execução:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-629">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="c7ca9-630">Obtenha o status de criptografia:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="c7ca9-631">criptografia de tooenable em uma nova VM em seu VHD criptografado, Olá use parâmetros com hello a seguir `azure vm create` comando:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-631">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="c7ca9-632">Obter status de criptografia de saudação de uma VM IaaS criptografado</span><span class="sxs-lookup"><span data-stu-id="c7ca9-632">Get hello encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="c7ca9-633">Você pode obter o status da criptografia hello usando o Gerenciador de recursos do Azure, [cmdlets do PowerShell](/powershell/azure/overview), ou comandos CLI.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-633">You can get hello encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="c7ca9-634">Olá seções a seguir explica como Olá toouse portal clássico do Azure e CLI comandos tooget Olá status de criptografia.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-634">hello following sections explain how toouse hello Azure classic portal and CLI commands tooget hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="c7ca9-635">Obter status de criptografia de saudação de uma VM do Windows criptografado usando o Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="c7ca9-635">Get hello encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="c7ca9-636">Você pode obter o status de criptografia de saudação do hello IaaS VM do Gerenciador de recursos do Azure fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-636">You can get hello encryption status of hello IaaS VM from Azure Resource Manager by doing hello following:</span></span>

1. <span data-ttu-id="c7ca9-637">Entrar toohello [portal clássico do Azure](https://portal.azure.com/)e, em seguida, clique em **máquinas virtuais** no painel esquerdo de saudação toosee uma exibição resumida de máquinas virtuais de saudação em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-637">Sign in toohello [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in hello left pane toosee a summary view of hello virtual machines in your subscription.</span></span> <span data-ttu-id="c7ca9-638">Você pode filtrar a exibição de máquinas virtuais de hello, selecionando o nome da assinatura Olá no hello **assinatura** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-638">You can filter hello virtual machines view by selecting hello subscription name in hello **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="c7ca9-639">Na parte superior de saudação do hello **máquinas virtuais** , clique em **colunas**.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-639">At hello top of hello **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="c7ca9-640">Em Olá **coluna escolha** folha, selecione **criptografia de disco**e, em seguida, clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-640">On hello **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="c7ca9-641">Você deve ver o estado de criptografia de Olá Olá criptografia de disco coluna mostrando _habilitado_ ou _não habilitada_ para cada VM, conforme mostrado na figura a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-641">You should see hello disk-encryption column showing hello encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in hello following figure:</span></span>

 ![Microsoft Antimalware no Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="c7ca9-643">Obter status de criptografia de saudação de uma VM de IaaS (Windows/Linux) criptografado usando o cmdlet do PowerShell de criptografia de disco Olá</span><span class="sxs-lookup"><span data-stu-id="c7ca9-643">Get hello encryption status of an encrypted (Windows/Linux) IaaS VM by using hello disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="c7ca9-644">Você pode obter o status de criptografia de saudação do hello IaaS VM do cmdlet do PowerShell de criptografia de disco Olá `Get-AzureRmVMDiskEncryptionStatus`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-644">You can get hello encryption status of hello IaaS VM from hello disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="c7ca9-645">configurações de criptografia tooget Olá para sua VM, digite seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-645">tooget hello encryption settings for your VM, enter hello following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="c7ca9-646">Você pode inspecionar a saída de saudação do _AzureRmVMDiskEncryptionStatus Get_ para criptografia de chave URLs.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-646">You can inspect hello output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

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

<span data-ttu-id="c7ca9-647">Olá OSVolumeEncrypted e valores de configurações de DataVolumesEncrypted são definidos too_Encrypted_, que mostra que ambos os volumes são criptografados usando a criptografia de disco do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-647">hello OSVolumeEncrypted and DataVolumesEncrypted settings values are set too_Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="c7ca9-648">Para obter informações sobre como habilitar a criptografia com criptografia de disco do Azure usando cmdlets do PowerShell, consulte as postagens de blog de saudação [explorar criptografia de disco do Azure com o Azure PowerShell - parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) e [explorar criptografia de disco do Azure com o Azure PowerShell - parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-649">Em VMs do Linux, leva três minutos toofour para Olá `Get-AzureRmVMDiskEncryptionStatus` status de criptografia do cmdlet tooreport hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-649">On Linux VMs, it takes three toofour minutes for hello `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a><span data-ttu-id="c7ca9-650">Obter status de criptografia de saudação de Olá IaaS VM do comando CLI Olá criptografia de disco</span><span class="sxs-lookup"><span data-stu-id="c7ca9-650">Get hello encryption status of hello IaaS VM from hello disk-encryption CLI command</span></span>
<span data-ttu-id="c7ca9-651">Você pode obter o status de criptografia de saudação do hello IaaS VM usando o comando CLI de criptografia de disco Olá `azure vm show-disk-encryption-status`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-651">You can get hello encryption status of hello IaaS VM by using hello disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="c7ca9-652">configurações de criptografia tooget Olá para sua VM, insira sua sessão de CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-652">tooget hello encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="c7ca9-653">Desabilitar a criptografia em VMs IaaS do Windows em execução</span><span class="sxs-lookup"><span data-stu-id="c7ca9-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="c7ca9-654">Você pode desabilitar a criptografia em um VM de IaaS Linux ou do Windows em execução por meio do modelo do Gerenciador de recursos de criptografia de disco do Azure hello ou cmdlets do PowerShell e especificar a configuração de descriptografia hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-654">You can disable encryption on a running Windows or Linux IaaS VM via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify hello decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="c7ca9-655">VM Windows</span><span class="sxs-lookup"><span data-stu-id="c7ca9-655">Windows VM</span></span>
<span data-ttu-id="c7ca9-656">etapa de desabilitar a criptografia Olá desabilita a criptografia de Olá SO, volume de dados hello ou ambos em Olá executando Windows IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-656">hello disable-encryption step disables encryption of hello OS, hello data volume, or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="c7ca9-657">Você não pode desabilitar o volume do sistema operacional hello e deixe o volume de dados Olá criptografado.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-657">You cannot disable hello OS volume and leave hello data volume encrypted.</span></span> <span data-ttu-id="c7ca9-658">Quando Olá desabilitar criptografia etapa será executada, modelo de implantação clássico do Azure Olá atualiza o modelo de serviço VM Olá e Olá VM de IaaS do Windows está marcado como descriptografado.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-658">When hello disable-encryption step is performed, hello Azure classic deployment model updates hello VM service model, and hello Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="c7ca9-659">conteúdo de saudação do hello VM não é criptografado em repouso.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-659">hello contents of hello VM are no longer encrypted at rest.</span></span> <span data-ttu-id="c7ca9-660">descriptografia Olá não excluir o cofre e hello criptografia chave material de chave (chaves de criptografia do BitLocker para Windows e senha para Linux).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-660">hello decryption does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="c7ca9-661">VM Linux</span><span class="sxs-lookup"><span data-stu-id="c7ca9-661">Linux VM</span></span>
<span data-ttu-id="c7ca9-662">etapa de desabilitar a criptografia Olá desabilita a criptografia do volume de dados Olá Olá executando Linux IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-662">hello disable-encryption step disables encryption of hello data volume on hello running Linux IaaS VM.</span></span> <span data-ttu-id="c7ca9-663">Esta etapa só funciona se o disco do sistema operacional Olá não está criptografado.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-663">This step only works if hello OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-664">A desabilitação da criptografia no disco do sistema operacional Olá não é permitida em VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-664">Disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="c7ca9-665">Desabilitar a criptografia em uma VM IaaS existente ou em execução</span><span class="sxs-lookup"><span data-stu-id="c7ca9-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="c7ca9-666">Você pode desabilitar a criptografia de disco em executando as VMs de IaaS do Windows usando Olá [modelo do Gerenciador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-666">You can disable disk encryption on running Windows IaaS VMs by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="c7ca9-667">No modelo de saudação de início rápido do Azure, clique em **implantar tooAzure**, insira a configuração de descriptografia de saudação em Olá **parâmetros** folha e depois clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-667">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello decryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="c7ca9-668">Selecione a assinatura hello, grupo de recursos, local do grupo de recursos, os termos legais e contrato e, em seguida, clique em **criar** tooenable criptografia em uma nova VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-668">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="c7ca9-669">Para VMs do Linux, você pode desabilitar a criptografia usando Olá [desabilitar a criptografia em uma VM do Linux em execução](https://aka.ms/decrypt-linuxvm) modelo.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-669">For Linux VMs, you can disable encryption by using hello [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="c7ca9-670">Hello tabela a seguir lista os parâmetros de modelo do Gerenciador de recursos para desabilitar a criptografia em um IaaS VM em execução:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-670">hello following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="c7ca9-671">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c7ca9-671">Parameter</span></span> | <span data-ttu-id="c7ca9-672">Descrição</span><span class="sxs-lookup"><span data-stu-id="c7ca9-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7ca9-673">vmName</span><span class="sxs-lookup"><span data-stu-id="c7ca9-673">vmName</span></span> | <span data-ttu-id="c7ca9-674">Nome da saudação VM Olá a operação de criptografia é toobe executada em.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-674">Name of hello VM that hello encryption operation is toobe performed on.</span></span>
| <span data-ttu-id="c7ca9-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="c7ca9-675">volumeType</span></span> | <span data-ttu-id="c7ca9-676">Tipo de volume em que uma operação de descriptografia é executada.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="c7ca9-677">Os valores válidos são _OS_, _Data_ e _All_.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="c7ca9-678">Você não pode desabilitar a criptografia em execução o volume de inicialização/sistema operacional Windows IaaS VM sem a desabilitação da criptografia no hello _dados_ volume.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on hello _Data_ volume.</span></span> <span data-ttu-id="c7ca9-679">Observe também que a desabilitação da criptografia no disco do sistema operacional Olá não é permitida em VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-679">Also note that disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="c7ca9-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="c7ca9-680">sequenceVersion</span></span> | <span data-ttu-id="c7ca9-681">Versão da sequência de saudação operação do BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-681">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="c7ca9-682">Aumentar esse número de versão toda vez que uma operação de descriptografia de disco é executada em Olá mesma VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-682">Increment this version number every time a disk decryption operation is performed on hello same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="c7ca9-683">Desabilitar a criptografia em uma VM IaaS existente ou em execução</span><span class="sxs-lookup"><span data-stu-id="c7ca9-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="c7ca9-684">criptografia toodisable em uma VM IaaS existente ou em execução usando o cmdlet do PowerShell hello, consulte [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-684">toodisable encryption on an existing or running IaaS VM by using hello PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="c7ca9-685">Esse cmdlet dá suporte a VMs do Linux e do Windows.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="c7ca9-686">criptografia toodisable, ele instala uma extensão na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-686">toodisable encryption, it installs an extension on hello virtual machine.</span></span> <span data-ttu-id="c7ca9-687">Se hello _nome_ parâmetro não for especificado, uma extensão com o nome padrão Olá _AzureDiskEncryption para VMs do Windows_ é criado.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-687">If hello _Name_ parameter is not specified, an extension with hello default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="c7ca9-688">Em VMs do Linux, Olá AzureDiskEncryptionForLinux extensão é usado.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-688">On Linux VMs, hello AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca9-689">Esse cmdlet reinicia a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-689">This cmdlet reboots hello virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="c7ca9-690">Habilitar criptografia na VM da IaaS criptografada previamente com o Azure Managed Disk</span><span class="sxs-lookup"><span data-stu-id="c7ca9-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="c7ca9-691">Use Olá BRAÇO do disco do Azure gerenciados modelo toocreate uma VM criptografada em um VHD previamente criptografado usando o modelo do ARM Olá localizada em</span><span class="sxs-lookup"><span data-stu-id="c7ca9-691">Use hello Azure Managed Disk ARM template toocreate a encrypted VM from a pre-encrypted VHD using hello ARM template located at</span></span>   
<span data-ttu-id="c7ca9-692">[Criar um novo disco gerenciado criptografado a partir de um blob de armazenamento/VHD criptografado] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="c7ca9-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="c7ca9-693">Habilitar criptografia em uma nova VM de IaaS Linux com o Azure Managed Disk</span><span class="sxs-lookup"><span data-stu-id="c7ca9-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="c7ca9-694">Use Olá BRAÇO do disco do Azure gerenciados modelo toocreate criptografado uma nova VM de IaaS Linux usando o modelo do ARM Olá localizado em</span><span class="sxs-lookup"><span data-stu-id="c7ca9-694">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
<span data-ttu-id="c7ca9-695">[Implantação do RHEL 7.2 com criptografia de disco completo] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="c7ca9-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="c7ca9-696">Habilitar criptografia em uma nova VM de IaaS do Windows com o Azure Managed Disk</span><span class="sxs-lookup"><span data-stu-id="c7ca9-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="c7ca9-697">Use Olá BRAÇO do disco do Azure gerenciados modelo toocreate criptografado uma nova VM de IaaS Linux usando o modelo do ARM Olá localizado em</span><span class="sxs-lookup"><span data-stu-id="c7ca9-697">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
 <span data-ttu-id="c7ca9-698">[Criar uma nova VM do Disco Gerenciado de IaaS do Windows a partir da imagem da galeria] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="c7ca9-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="c7ca9-699">É obrigatório toosnapshot e/ou backup um disco gerenciado com base instância VM fora do e tooenabling anterior a criptografia de disco do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-699">It is mandatory toosnapshot and/or backup a managed disk based VM instance outside of and prior tooenabling Azure Disk Encryption.</span></span>  <span data-ttu-id="c7ca9-700">Um instantâneo do disco gerenciado Olá pode ser executado no portal de saudação ou Backup do Azure pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-700">A snapshot of hello managed disk can be taken from hello portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="c7ca9-701">Backups Certifique-se de que uma opção de recuperação é possível no caso de saudação de qualquer falha inesperada durante a criptografia.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-701">Backups ensure that a recovery option is possible in hello case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="c7ca9-702">Depois que um backup é realizado, Olá conjunto AzureRmVMDiskEncryptionExtension cmdlet pode ser usado tooencrypt gerenciado discos especificando o parâmetro - skipVmBackup de hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-702">Once a backup is made, hello Set-AzureRmVMDiskEncryptionExtension cmdlet can be used tooencrypt managed disks by specifying hello -skipVmBackup parameter.</span></span>  <span data-ttu-id="c7ca9-703">Este comando falhará em VMs baseadas em disco gerenciado até que um backup tenha sido feito e esse parâmetro tenha sido especificado.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="c7ca9-704">Atualizar configurações de criptografia de uma VM de armazenamento não premium criptografada existente</span><span class="sxs-lookup"><span data-stu-id="c7ca9-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="c7ca9-705">Use Olá disco Azure criptografia tem suportada interfaces existentes para executar a VM [cmdlets do PS, modelos CLI ou ARM] tooupdate configurações de criptografia de saudação que o cliente AAD ID/segredo, chave de criptografia [KEK], chave de criptografia do BitLocker para a máquina virtual do Windows ou a senha para Configuração de criptografia de atualização de Olá etc. de VM do Linux tem suporte apenas para VMs com o apoio de armazenamento não premium.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-705">Use hello existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] tooupdate hello encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. hello update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="c7ca9-706">Não oferece suporte para VMs com suporte de armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="c7ca9-707">Apêndice</span><span class="sxs-lookup"><span data-stu-id="c7ca9-707">Appendix</span></span>
### <a name="connect-tooyour-subscription"></a><span data-ttu-id="c7ca9-708">Conecte-se a assinatura de tooyour</span><span class="sxs-lookup"><span data-stu-id="c7ca9-708">Connect tooyour subscription</span></span>
<span data-ttu-id="c7ca9-709">Antes de prosseguir, verifique Olá *pré-requisitos* seção neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-709">Before you proceed, review hello *Prerequisites* section in this article.</span></span> <span data-ttu-id="c7ca9-710">Depois de garantir que todos os pré-requisitos foram atendidos, conecte-se tooyour assinatura fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-710">After you ensure that all prerequisites have been met, connect tooyour subscription by doing hello following:</span></span>

1. <span data-ttu-id="c7ca9-711">Iniciar uma sessão do PowerShell do Azure e entrar tooyour conta do Azure com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-711">Start an Azure PowerShell session, and sign in tooyour Azure account with hello following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="c7ca9-712">Se você tiver várias assinaturas e deseja um toouse toospecify, digite Olá assinaturas de saudação toosee para sua conta a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-712">If you have multiple subscriptions and want toospecify one toouse, type hello following toosee hello subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="c7ca9-713">assinatura de saudação toospecify deseja toouse, tipo:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-713">toospecify hello subscription you want toouse, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="c7ca9-714">tooverify que a assinatura de saudação configurada está correta, digite:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-714">tooverify that hello subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="c7ca9-715">Olá tooconfirm criptografia de disco de Azure cmdlets são instalados, tipo:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-715">tooconfirm hello Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="c7ca9-716">Olá saída a seguir confirma a instalação do PowerShell de criptografia de disco do Azure hello:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-716">hello following output confirms hello Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="c7ca9-717">Preparar um VHD do Windows previamente criptografado</span><span class="sxs-lookup"><span data-stu-id="c7ca9-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="c7ca9-718">seções Olá a seguir são necessária tooprepare um VHD do Windows previamente criptografado para implantação como um VHD criptografado no IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-718">hello sections that follow are necessary tooprepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="c7ca9-719">Use Olá informações tooprepare e inicializar uma nova VM (VHD do Windows) no Azure Site Recovery ou no Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-719">Use hello information tooprepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a><span data-ttu-id="c7ca9-720">Atualizar grupo política tooallow não-TPM para a proteção do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="c7ca9-720">Update group policy tooallow non-TPM for OS protection</span></span>
<span data-ttu-id="c7ca9-721">Configurar a política de grupo do BitLocker Olá **a criptografia de unidade de disco BitLocker**, que você encontrará em **política de computador Local** > **deconfiguraçãodocomputador**  >  **Modelos administrativos** > **componentes do Windows**.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-721">Configure hello BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="c7ca9-722">Alterar essa configuração muito**unidades do sistema operacional** > **exigir autenticação adicional na inicialização** > **Permitir BitLocker sem um TPM compatível**, conforme mostrado na figura a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-722">Change this setting too**Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in hello following figure:</span></span>

![Microsoft Antimalware no Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="c7ca9-724">Instalar componentes de recursos do BitLocker</span><span class="sxs-lookup"><span data-stu-id="c7ca9-724">Install BitLocker feature components</span></span>
<span data-ttu-id="c7ca9-725">Para o Windows Server 2012 e posterior, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-725">For Windows Server 2012 and later, use hello following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="c7ca9-726">Para Windows Server 2008 R2, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-726">For Windows Server 2008 R2, use hello following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="c7ca9-727">Preparar o volume do sistema operacional de saudação do BitLocker usando`bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="c7ca9-727">Prepare hello OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="c7ca9-728">toocompress Olá partição do sistema operacional e preparar o computador de saudação do BitLocker, executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-728">toocompress hello OS partition and prepare hello machine for BitLocker, execute hello following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a><span data-ttu-id="c7ca9-729">Proteger o volume do sistema operacional hello usando o BitLocker</span><span class="sxs-lookup"><span data-stu-id="c7ca9-729">Protect hello OS volume by using BitLocker</span></span>
<span data-ttu-id="c7ca9-730">Saudação de uso [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) criptografia do comando tooenable no volume de inicialização hello usando um protetor de chave externo.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-730">Use hello [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command tooenable encryption on hello boot volume using an external key protector.</span></span> <span data-ttu-id="c7ca9-731">Também coloca chave de externo de saudação (arquivo .bek) na unidade externa hello ou volume.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-731">Also place hello external key (.bek file) on hello external drive or volume.</span></span> <span data-ttu-id="c7ca9-732">Criptografia está habilitada no volume de inicialização do sistema Olá após a próxima reinicialização do hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-732">Encryption is enabled on hello system/boot volume after hello next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="c7ca9-733">Prepare Olá VM com um data separado/recurso VHD para obtenção de chave externa hello usando o BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-733">Prepare hello VM with a separate data/resource VHD for getting hello external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="c7ca9-734">Criptografando uma unidade do sistema operacional em uma VM do Linux em execução</span><span class="sxs-lookup"><span data-stu-id="c7ca9-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="c7ca9-735">Criptografia de unidade do sistema operacional em uma VM do Linux em execução é compatível com hello distribuições a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-735">Encryption of an OS drive on a running Linux VM is supported on hello following distributions:</span></span>

* <span data-ttu-id="c7ca9-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="c7ca9-736">RHEL 7.2</span></span>
* <span data-ttu-id="c7ca9-737">CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="c7ca9-737">CentOS 7.2</span></span>
* <span data-ttu-id="c7ca9-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c7ca9-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="c7ca9-739">Pré-requisitos para a criptografia de disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="c7ca9-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="c7ca9-740">Olá VM deve ser criada da imagem do Marketplace Olá no Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-740">hello VM must be created from hello Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="c7ca9-741">VM do Azure com, no mínimo, 4 GB de RAM (o tamanho recomendável é de 7 GB).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="c7ca9-742">(Para RHEL e CentOS) Desabilite o SELinux.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="c7ca9-743">toodisable SELinux, consulte "4.4.2.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-743">toodisable SELinux, see "4.4.2.</span></span> <span data-ttu-id="c7ca9-744">Desabilitar o SELinux"hello [guia do administrador e usuário SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-744">Disabling SELinux" in hello [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on hello VM.</span></span>
* <span data-ttu-id="c7ca9-745">Depois de desabilitar SELinux, reinicialize Olá VM pelo menos uma vez.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-745">After you disable SELinux, reboot hello VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="c7ca9-746">Etapas</span><span class="sxs-lookup"><span data-stu-id="c7ca9-746">Steps</span></span>
1. <span data-ttu-id="c7ca9-747">Crie uma máquina virtual usando uma das distribuições de saudação especificadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-747">Create a VM by using one of hello distributions specified previously.</span></span>

 <span data-ttu-id="c7ca9-748">Para o CentOS 7.2, há suporte para a criptografia de disco do sistema operacional por meio de uma imagem especial.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="c7ca9-749">toouse imagem, especifique "7.2n" como Olá SKU quando você cria Olá VM:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-749">toouse this image, specify "7.2n" as hello SKU when you create hello VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="c7ca9-750">Configure as necessidades de acordo tooyour Olá VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-750">Configure hello VM according tooyour needs.</span></span> <span data-ttu-id="c7ca9-751">Se você for tooencrypt todas as unidades de saudação (sistema operacional + dados), unidades de dados Olá necessário toobe especificado e pode ser montado em /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-751">If you are going tooencrypt all hello (OS + data) drives, hello data drives need toobe specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="c7ca9-752">Use o UUID =... toospecify unidades de dados/etc/fstab em vez de especificar o nome de dispositivo de bloco hello (por exemplo, /dev/sdb1).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-752">Use UUID=... toospecify data drives in /etc/fstab instead of specifying hello block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="c7ca9-753">Durante a criptografia, Olá ordem das alterações de unidades em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-753">During encryption, hello order of drives changes on hello VM.</span></span> <span data-ttu-id="c7ca9-754">Se sua VM se baseia em uma ordem específica de dispositivos de bloco, ele falhará toomount-las após a criptografia.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-754">If your VM relies on a specific order of block devices, it will fail toomount them after encryption.</span></span>

3. <span data-ttu-id="c7ca9-755">Saia de sessões SSH de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-755">Sign out of hello SSH sessions.</span></span>

4. <span data-ttu-id="c7ca9-756">Olá tooencrypt OS, especifique volumeType como **todos os** ou **OS** quando você [habilitar a criptografia](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-756">tooencrypt hello OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="c7ca9-757">Todos os processos de espaço de usuário que não estão sendo executados como serviços `systemd` deverão ser encerrados com um `SIGKILL`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="c7ca9-758">Reinicialize Olá VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-758">Reboot hello VM.</span></span> <span data-ttu-id="c7ca9-759">Ao habilitar a criptografia de disco do sistema operacional em uma VM em execução, planeje o tempo de inatividade da VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="c7ca9-760">Periodicamente monitorar o progresso de saudação de criptografia usando instruções Olá Olá [próxima seção](#monitoring-os-encryption-progress).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-760">Periodically monitor hello progress of encryption by using hello instructions in hello [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="c7ca9-761">Depois de Get-AzureRmVmDiskEncryptionStatus mostra "VMRestartPending", reinicie a VM entrando no tooit ou usando o portal de hello, PowerShell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in tooit or by using hello portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
<span data-ttu-id="c7ca9-762">Antes de reinicializar, recomendamos que você salve [diagnósticos de inicialização](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of hello VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="c7ca9-763">Monitorando o progresso da criptografia do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="c7ca9-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="c7ca9-764">Você pode monitorar o progresso de criptografia do sistema operacional de três maneiras:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="c7ca9-765">Saudação de uso `Get-AzureRmVmDiskEncryptionStatus` cmdlet e inspecione o campo de ProgressMessage hello:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-765">Use hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect hello ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="c7ca9-766">Depois de saudação VM atinge "Criptografia iniciada em disco do SO", que leva cerca de 40 minutos too50 em um armazenamento Premium feito VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-766">After hello VM reaches "OS disk encryption started," it takes about 40 too50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="c7ca9-767">Devido ao [problema 388](https://github.com/Azure/WALinuxAgent/issues/388) no WALinuxAgent, `OsVolumeEncrypted` e `DataVolumesEncrypted` são mostrados como `Unknown` em algumas distribuições.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="c7ca9-768">Com a versão 2.1.5 WALinuxAgent e posterior, esse problema é corrigido automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="c7ca9-769">Se você vir `Unknown` na saída de hello, você pode verificar o status de criptografia de disco usando Olá Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-769">If you see `Unknown` in hello output, you can verify disk-encryption status by using hello Azure Resource Explorer.</span></span>

 <span data-ttu-id="c7ca9-770">Vá muito[Gerenciador de recursos do Azure](https://resources.azure.com/)e, em seguida, expanda essa hierarquia no painel de seleção Olá esquerda:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-770">Go too[Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in hello selection panel on left:</span></span>

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

 <span data-ttu-id="c7ca9-771">No hello InstanceView, role para baixo de status da criptografia Olá toosee de suas unidades.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-771">In hello InstanceView, scroll down toosee hello encryption status of your drives.</span></span>

 ![Exibição de instância VM](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="c7ca9-773">Examine o [diagnóstico de inicialização](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="c7ca9-774">Mensagens de saudação extensão ADE devem ser prefixadas com `[AzureDiskEncryption]`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-774">Messages from hello ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="c7ca9-775">Entrar toohello VM por meio do SSH e obter o log de extensão de saudação do:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-775">Sign in toohello VM via SSH, and get hello extension log from:</span></span>

    <span data-ttu-id="c7ca9-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="c7ca9-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="c7ca9-777">É recomendável que você não entrar no toohello VM enquanto a criptografia de sistema operacional está em andamento.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-777">We recommend that you do not sign in toohello VM while OS encryption is in progress.</span></span> <span data-ttu-id="c7ca9-778">Copie os logs de saudação apenas quando hello outros dois métodos falharem.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-778">Copy hello logs only when hello other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="c7ca9-779">Preparar um VHD Linux previamente criptografado</span><span class="sxs-lookup"><span data-stu-id="c7ca9-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="c7ca9-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="c7ca9-780">Ubuntu 16</span></span>
<span data-ttu-id="c7ca9-781">Configure a criptografia durante a instalação de distribuição Olá Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-781">Configure encryption during hello distribution installation by doing hello following:</span></span>

1. <span data-ttu-id="c7ca9-782">Selecione **configurar volumes criptografados** quando você particionar os discos de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-782">Select **Configure encrypted volumes** when you partition hello disks.</span></span>

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="c7ca9-784">Crie uma unidade de inicialização separada que não deverá ser criptografada.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="c7ca9-785">Criptografe a unidade de inicialização.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-785">Encrypt your root drive.</span></span>

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="c7ca9-787">Forneça uma frase secreta.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-787">Provide a passphrase.</span></span> <span data-ttu-id="c7ca9-788">Isso é Olá que você carregue toohello Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-788">This is hello passphrase that you upload toohello key vault.</span></span>

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="c7ca9-790">Conclua o particionamento.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-790">Finish partitioning.</span></span>

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="c7ca9-792">Ao inicializar Olá VM e será solicitado para uma frase secreta, use Olá senha fornecida na etapa 3.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-792">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="c7ca9-794">Preparar Olá VM para carregar no Azure usando [estas instruções](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-794">Prepare hello VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="c7ca9-795">Ainda não executado última etapa do hello (Olá desprovisionamento VM).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-795">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="c7ca9-796">Configure criptografia toowork com o Azure fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-796">Configure encryption toowork with Azure by doing hello following:</span></span>

1. <span data-ttu-id="c7ca9-797">Crie um arquivo em /usr/local/sbin/azure_crypt_key.sh, com conteúdo Olá Olá script a seguir.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with hello content in hello following script.</span></span> <span data-ttu-id="c7ca9-798">Preste atenção toohello KeyFileName, porque ele é o nome do arquivo de senha Olá usado pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-798">Pay attention toohello KeyFileName, because it is hello passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
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
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="c7ca9-799">Altere Olá crypt configuração em */etc/crypttab*.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-799">Change hello crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="c7ca9-800">O resultado deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="c7ca9-801">Se você estiver editando *azure_crypt_key.sh* no Windows e você copiou tooLinux, execute `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it tooLinux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="c7ca9-802">Adicione permissões executável toohello script:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-802">Add executable permissions toohello script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="c7ca9-803">Edite */etc/initramfs-tools/modules* acrescentando linha:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="c7ca9-804">Executar `update-initramfs -u -k all` tooupdate Olá initramfs toomake Olá `keyscript` entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-804">Run `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` take effect.</span></span>

7. <span data-ttu-id="c7ca9-805">Agora você pode cancelar o provisionamento Olá VM.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-805">Now you can deprovision hello VM.</span></span>

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="c7ca9-807">Continuar toohello próxima etapa e [carregar o VHD](#upload-encrypted-vhd-to-an-azure-storage-account) no Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-807">Continue toohello next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="c7ca9-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="c7ca9-808">openSUSE 13.2</span></span>
<span data-ttu-id="c7ca9-809">criptografia tooconfigure durante a instalação de distribuição hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-809">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="c7ca9-810">Ao particionar discos hello, selecione **criptografar o grupo de volumes**e, em seguida, digite uma senha.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-810">When you partition hello disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="c7ca9-811">Esta é Olá senha que você fará o upload tooyour Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-811">This is hello password that you will upload tooyour key vault.</span></span>

 ![Instalação do openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="c7ca9-813">Saudação de inicialização VM usando sua senha.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-813">Boot hello VM using your password.</span></span>

 ![Instalação do openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="c7ca9-815">Preparar Olá VM para carregar tooAzure, seguindo as instruções de saudação do [preparar uma máquina virtual SLES ou openSUSE para o Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-815">Prepare hello VM for uploading tooAzure by following hello instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="c7ca9-816">Ainda não executado última etapa do hello (Olá desprovisionamento VM).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-816">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="c7ca9-817">tooconfigure toowork de criptografia com o Azure, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-817">tooconfigure encryption toowork with Azure, do hello following:</span></span>
1. <span data-ttu-id="c7ca9-818">Editar saudação /etc/dracut.conf e, em seguida, adicione Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-818">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="c7ca9-819">Comente essas linhas final Olá Olá /usr/lib/dracut/modules.d/90crypt/module-setup.sh do arquivo:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-819">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
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

3. <span data-ttu-id="c7ca9-820">Acrescente Olá a seguinte linha no início de saudação do hello arquivo /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-820">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="c7ca9-821">E altere todas as ocorrências de:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="c7ca9-822">para:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="c7ca9-823">Editar /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e acrescente muito "dispositivo de abrir LUKS #":</span><span class="sxs-lookup"><span data-stu-id="c7ca9-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it too“# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
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
5. <span data-ttu-id="c7ca9-824">Executar `/usr/sbin/dracut -f -v` tooupdate Olá initrd.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-824">Run `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span></span>

6. <span data-ttu-id="c7ca9-825">Agora você pode cancelar o provisionamento Olá VM e [carregar o VHD](#upload-encrypted-vhd-to-an-azure-storage-account) no Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-825">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="c7ca9-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c7ca9-826">CentOS 7</span></span>
<span data-ttu-id="c7ca9-827">criptografia tooconfigure durante a instalação de distribuição hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-827">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="c7ca9-828">Selecione **Criptografar meus dados** ao particionar os discos.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![Instalação do CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="c7ca9-830">Verifique se a opção **Criptografar** está selecionada para a partição raiz.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![Instalação do CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="c7ca9-832">Forneça uma frase secreta.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-832">Provide a passphrase.</span></span> <span data-ttu-id="c7ca9-833">Isso é Olá que você fará o upload tooyour Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-833">This is hello passphrase that you will upload tooyour key vault.</span></span>

 ![Instalação do CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="c7ca9-835">Ao inicializar Olá VM e será solicitado para uma frase secreta, use Olá senha fornecida na etapa 3.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-835">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Instalação do CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="c7ca9-837">Preparar Olá VM para carregar no Azure usando instruções "CentOS 7.0 +" hello [preparar uma máquina virtual com base em CentOS Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-837">Prepare hello VM for uploading into Azure by using hello "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="c7ca9-838">Ainda não executado última etapa do hello (Olá desprovisionamento VM).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-838">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

6. <span data-ttu-id="c7ca9-839">Agora você pode cancelar o provisionamento Olá VM e [carregar o VHD](#upload-encrypted-vhd-to-an-azure-storage-account) no Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-839">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="c7ca9-840">tooconfigure toowork de criptografia com o Azure, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-840">tooconfigure encryption toowork with Azure, do hello following:</span></span>

1. <span data-ttu-id="c7ca9-841">Editar saudação /etc/dracut.conf e, em seguida, adicione Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-841">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="c7ca9-842">Comente essas linhas final Olá Olá /usr/lib/dracut/modules.d/90crypt/module-setup.sh do arquivo:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-842">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
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

3. <span data-ttu-id="c7ca9-843">Acrescente Olá a seguinte linha no início de saudação do hello arquivo /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-843">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="c7ca9-844">E altere todas as ocorrências de:</span><span class="sxs-lookup"><span data-stu-id="c7ca9-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="c7ca9-845">para</span><span class="sxs-lookup"><span data-stu-id="c7ca9-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="c7ca9-846">Edite /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e anexá-lo após hello "dispositivo de abrir LUKS #":</span><span class="sxs-lookup"><span data-stu-id="c7ca9-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after hello “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
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
5. <span data-ttu-id="c7ca9-847">Executar hello "/ /sbin/Service/usr/dracut - f - v" tooupdate Olá initrd.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-847">Run hello “/usr/sbin/dracut -f -v” tooupdate hello initrd.</span></span>

![Instalação do CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a><span data-ttu-id="c7ca9-849">Carregar conta de armazenamento do Azure de tooan VHD criptografadas</span><span class="sxs-lookup"><span data-stu-id="c7ca9-849">Upload encrypted VHD tooan Azure storage account</span></span>
<span data-ttu-id="c7ca9-850">Depois de DM Crypt ou a criptografia do BitLocker é habilitado, Olá local criptografado conta de armazenamento do VHD necessidades toobe carregado tooyour.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-850">After BitLocker encryption or DM-Crypt encryption is enabled, hello local encrypted VHD needs toobe uploaded tooyour storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a><span data-ttu-id="c7ca9-851">Carregar secreta de criptografia de disco Olá para Olá previamente criptografado VM tooyour Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="c7ca9-851">Upload hello disk-encryption secret for hello pre-encrypted VM tooyour key vault</span></span>
<span data-ttu-id="c7ca9-852">segredo de criptografia de disco Olá que você obteve anteriormente deve ser carregado como um segredo no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-852">hello disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="c7ca9-853">Cofre de chaves Olá precisa de criptografia de disco toohave e permissões habilitadas para o cliente do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-853">hello key vault needs toohave disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="c7ca9-854">Segredo de criptografia de disco não criptografado com uma KEK</span><span class="sxs-lookup"><span data-stu-id="c7ca9-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="c7ca9-855">tooset o segredo de saudação em seu Cofre de chaves, use [AzureKeyVaultSecret conjunto](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-855">tooset up hello secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="c7ca9-856">Se você tiver uma máquina virtual do Windows, o arquivo de bek de saudação é codificado como uma cadeia de caracteres base64 e, em seguida, carregado tooyour Cofre de chaves usando Olá `Set-AzureKeyVaultSecret` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-856">If you have a Windows virtual machine, hello bek file is encoded as a base64 string and then uploaded tooyour key vault using hello `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="c7ca9-857">Para o Linux, Olá senha é codificada como uma cadeia de caracteres base64 e carregados toohello Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-857">For Linux, hello passphrase is encoded as a base64 string and then uploaded toohello key vault.</span></span> <span data-ttu-id="c7ca9-858">Além disso, certifique-se que Olá marcas a seguir são definidos quando você cria o segredo Olá no cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-858">In addition, make sure that hello following tags are set when you create hello secret in hello key vault.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="c7ca9-859">Saudação de uso `$secretUrl` na próxima etapa Olá para [anexando disco Olá SO sem usar KEK](#without-using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-859">Use hello `$secretUrl` in hello next step for [attaching hello OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="c7ca9-860">Segredo de criptografia de disco criptografado com uma KEK</span><span class="sxs-lookup"><span data-stu-id="c7ca9-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="c7ca9-861">Antes de carregar o cofre da chave secreta toohello hello, você pode opcionalmente criptografá-lo usando uma chave de criptografia de chave.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-861">Before you upload hello secret toohello key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="c7ca9-862">Quebra automática de saudação do uso [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst criptografar segredo hello usando a chave de criptografia de chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-862">Use hello wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst encrypt hello secret using hello key encryption key.</span></span> <span data-ttu-id="c7ca9-863">Olá, a saída dessa operação wrap é uma cadeia de URL codificada em base64, que, em seguida, você pode carregar como um segredo usando Olá [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-863">hello output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using hello [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
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

<span data-ttu-id="c7ca9-864">Use `$KeyEncryptionKey` e `$secretUrl` na próxima etapa Olá para [anexando disco Olá SO usando KEK](#using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-864">Use `$KeyEncryptionKey` and `$secretUrl` in hello next step for [attaching hello OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="c7ca9-865">Especificar uma URL secreta ao anexar um disco do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="c7ca9-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="c7ca9-866">Sem usar uma KEK</span><span class="sxs-lookup"><span data-stu-id="c7ca9-866">Without using a KEK</span></span>
<span data-ttu-id="c7ca9-867">Enquanto você está anexando disco Olá sistema operacional, você precisa toopass `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-867">While you are attaching hello OS disk, you need toopass `$secretUrl`.</span></span> <span data-ttu-id="c7ca9-868">Olá URL foi gerado na seção de "secreta de criptografia de disco não criptografada com uma KEK" hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-868">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="c7ca9-869">Usando uma KEK</span><span class="sxs-lookup"><span data-stu-id="c7ca9-869">Using a KEK</span></span>
<span data-ttu-id="c7ca9-870">Quando você anexa um disco Olá SO, passar `$KeyEncryptionKey` e `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-870">When you attach hello OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="c7ca9-871">Olá URL foi gerado na seção de "secreta de criptografia de disco não criptografada com uma KEK" hello.</span><span class="sxs-lookup"><span data-stu-id="c7ca9-871">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

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

## <a name="download-this-guide"></a><span data-ttu-id="c7ca9-872">Baixar este guia</span><span class="sxs-lookup"><span data-stu-id="c7ca9-872">Download this guide</span></span>
<span data-ttu-id="c7ca9-873">Você pode baixar este guia do hello [Galeria do TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span><span class="sxs-lookup"><span data-stu-id="c7ca9-873">You can download this guide from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="c7ca9-874">Para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="c7ca9-874">For more information</span></span>
[<span data-ttu-id="c7ca9-875">Explorar a Azure Disk Encryption com o Azure PowerShell - Parte 1</span><span class="sxs-lookup"><span data-stu-id="c7ca9-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="c7ca9-876">Explorar a Azure Disk Encryption com o Azure PowerShell - Parte 2</span><span class="sxs-lookup"><span data-stu-id="c7ca9-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
