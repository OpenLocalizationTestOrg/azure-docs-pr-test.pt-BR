---
title: FAQ (perguntas frequentes) sobre discos de VM IaaS do Azure | Microsoft Docs
description: "Perguntas frequentes sobre discos de VM IaaS do Azure e discos premium (gerenciados e não gerenciados)"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 9e5eed35334f1b95441b8181c8e90645be78b389
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="ba408-103">Perguntas frequentes sobre discos de VM IaaS do Azure e discos premium gerenciados e não gerenciados</span><span class="sxs-lookup"><span data-stu-id="ba408-103">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="ba408-104">Este artigo responde a algumas perguntas frequentes sobre o Azure Managed Disks e o Armazenamento Premium do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba408-104">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="ba408-105">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="ba408-105">Managed Disks</span></span>

<span data-ttu-id="ba408-106">**O que é o Azure Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="ba408-106">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="ba408-107">Managed Disks é um recurso que simplifica o gerenciamento de disco para VMs IaaS do Azure manipulando o gerenciamento de conta de armazenamento para você.</span><span class="sxs-lookup"><span data-stu-id="ba408-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="ba408-108">Para saber mais, veja [Visão geral dos Managed Disks](storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba408-108">For more information, see the [Managed Disks overview](storage-managed-disks-overview.md).</span></span>

<span data-ttu-id="ba408-109">**Se eu criar um disco gerenciado standard com base em um VHD existente que tem 80 GB, quanto isso custará?**</span><span class="sxs-lookup"><span data-stu-id="ba408-109">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="ba408-110">Um disco gerenciado standard criado com base em um VHD de 80 GB é tratado como o próximo tamanho de disco standard disponível, um disco S10.</span><span class="sxs-lookup"><span data-stu-id="ba408-110">A standard managed disk created from an 80-GB VHD is treated as the next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="ba408-111">Você será cobrado de acordo com o preço do disco S10.</span><span class="sxs-lookup"><span data-stu-id="ba408-111">You're charged according to the S10 disk pricing.</span></span> <span data-ttu-id="ba408-112">Para saber mais, confira a [página de preço](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="ba408-112">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="ba408-113">**Existem custos de transação de discos gerenciados standard?**</span><span class="sxs-lookup"><span data-stu-id="ba408-113">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="ba408-114">Sim.</span><span class="sxs-lookup"><span data-stu-id="ba408-114">Yes.</span></span> <span data-ttu-id="ba408-115">Você é cobrado por cada transação.</span><span class="sxs-lookup"><span data-stu-id="ba408-115">You're charged for each transaction.</span></span> <span data-ttu-id="ba408-116">Para saber mais, confira a [página de preço](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="ba408-116">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="ba408-117">**Para um disco gerenciado standard, eu serei cobrado pelo tamanho real dos dados no disco ou pela capacidade provisionada do disco?**</span><span class="sxs-lookup"><span data-stu-id="ba408-117">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span></span>

<span data-ttu-id="ba408-118">Você é cobrado com base na capacidade provisionada do disco.</span><span class="sxs-lookup"><span data-stu-id="ba408-118">You're charged based on the provisioned capacity of the disk.</span></span> <span data-ttu-id="ba408-119">Para saber mais, confira a [página de preço](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="ba408-119">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="ba408-120">**O preço dos discos premium gerenciados é diferente do preço dos discos não gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="ba408-120">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="ba408-121">O preço dos discos premium gerenciados é o mesmo que os discos premium não gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ba408-121">The pricing of premium managed disks is the same as unmanaged premium disks.</span></span>

<span data-ttu-id="ba408-122">**Posso alterar o tipo de conta de armazenamento (Standard ou Premium) de meus discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="ba408-122">**Can I change the storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="ba408-123">Sim.</span><span class="sxs-lookup"><span data-stu-id="ba408-123">Yes.</span></span> <span data-ttu-id="ba408-124">Você pode alterar o tipo de conta de armazenamento de seus discos gerenciados usando o portal do Azure, PowerShell ou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba408-124">You can change the storage account type of your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="ba408-125">**É possível copiar ou exportar um disco gerenciado para uma conta de armazenamento privado?**</span><span class="sxs-lookup"><span data-stu-id="ba408-125">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="ba408-126">Sim.</span><span class="sxs-lookup"><span data-stu-id="ba408-126">Yes.</span></span> <span data-ttu-id="ba408-127">Você pode exportar seus discos gerenciados usando o portal do Azure, PowerShell ou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba408-127">You can export your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="ba408-128">**Posso usar um arquivo VHD em uma conta de armazenamento do Azure para criar um disco gerenciado com uma assinatura diferente?**</span><span class="sxs-lookup"><span data-stu-id="ba408-128">**Can I use a VHD file in an Azure storage account to create a managed disk with a different subscription?**</span></span>

<span data-ttu-id="ba408-129">Não.</span><span class="sxs-lookup"><span data-stu-id="ba408-129">No.</span></span>

<span data-ttu-id="ba408-130">**Posso usar um arquivo VHD em uma conta de armazenamento do Azure para criar um disco gerenciado em uma região diferente?**</span><span class="sxs-lookup"><span data-stu-id="ba408-130">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span></span>

<span data-ttu-id="ba408-131">Não.</span><span class="sxs-lookup"><span data-stu-id="ba408-131">No.</span></span>

<span data-ttu-id="ba408-132">**Existem limitações de escala para clientes que usam discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="ba408-132">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="ba408-133">O Managed Disks elimina os limites associados a contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ba408-133">Managed Disks eliminates the limits associated with storage accounts.</span></span> <span data-ttu-id="ba408-134">No entanto, o número de discos gerenciados por assinatura é limitado a 2.000 por padrão.</span><span class="sxs-lookup"><span data-stu-id="ba408-134">However, the number of managed disks per subscription is limited to 2,000 by default.</span></span> <span data-ttu-id="ba408-135">Você pode chamar o suporte para aumentar esse número.</span><span class="sxs-lookup"><span data-stu-id="ba408-135">You can call support to increase this number.</span></span>

<span data-ttu-id="ba408-136">**Posso fazer um instantâneo incremental de um disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="ba408-136">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="ba408-137">Não.</span><span class="sxs-lookup"><span data-stu-id="ba408-137">No.</span></span> <span data-ttu-id="ba408-138">O recurso de instantâneo atual faz uma cópia completa de um disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="ba408-138">The current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="ba408-139">No entanto, estamos planejando oferecer suporte a instantâneos incrementais no futuro.</span><span class="sxs-lookup"><span data-stu-id="ba408-139">However, we are planning to support incremental snapshots in the future.</span></span>

<span data-ttu-id="ba408-140">**As VMs em um conjunto de disponibilidade podem consistir de uma combinação de discos gerenciados e não gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="ba408-140">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="ba408-141">Não.</span><span class="sxs-lookup"><span data-stu-id="ba408-141">No.</span></span> <span data-ttu-id="ba408-142">As VMs em um conjunto de disponibilidade devem usar todos os discos gerenciados ou não gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ba408-142">The VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="ba408-143">Ao criar um conjunto de disponibilidade, você pode escolher qual tipo de discos que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="ba408-143">When you create an availability set, you can choose which type of disks you want to use.</span></span>

<span data-ttu-id="ba408-144">**O Managed Disks é a opção padrão no portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="ba408-144">**Is Managed Disks the default option in the Azure portal?**</span></span>

<span data-ttu-id="ba408-145">Atualmente não, mas ele se tornará o padrão no futuro.</span><span class="sxs-lookup"><span data-stu-id="ba408-145">Not currently, but it will become the default in the future.</span></span>

<span data-ttu-id="ba408-146">**É possível criar um disco gerenciado vazio?**</span><span class="sxs-lookup"><span data-stu-id="ba408-146">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="ba408-147">Sim.</span><span class="sxs-lookup"><span data-stu-id="ba408-147">Yes.</span></span> <span data-ttu-id="ba408-148">Você pode criar um disco vazio.</span><span class="sxs-lookup"><span data-stu-id="ba408-148">You can create an empty disk.</span></span> <span data-ttu-id="ba408-149">Um disco gerenciado pode ser criado independentemente de uma VM, por exemplo, sem anexá-lo a uma VM.</span><span class="sxs-lookup"><span data-stu-id="ba408-149">A managed disk can be created independently of a VM, for example, without attaching it to a VM.</span></span>

<span data-ttu-id="ba408-150">**O que é a contagem de domínios de falha com suporte para um conjunto de disponibilidade que usa o Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="ba408-150">**What is the supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="ba408-151">Dependendo da região em que o conjunto de disponibilidade que usa o Managed Disks está localizado, a contagem de domínios de falha com suporte é 2 ou 3.</span><span class="sxs-lookup"><span data-stu-id="ba408-151">Depending on the region where the availability set that uses Managed Disks is located, the supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="ba408-152">**Como é conta de armazenamento standard para a configuração de diagnóstico?**</span><span class="sxs-lookup"><span data-stu-id="ba408-152">**How is the standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="ba408-153">Você configura uma conta de armazenamento privado para diagnóstico da VM.</span><span class="sxs-lookup"><span data-stu-id="ba408-153">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="ba408-154">No futuro, planejamos alternar o diagnóstico para o Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="ba408-154">In the future, we plan to switch diagnostics to Managed Disks as well.</span></span>

<span data-ttu-id="ba408-155">**O tipo de suporte ao Controle de Acesso Baseado em Função está disponível para o Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="ba408-155">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="ba408-156">O Managed Disks oferece suporte a três funções principais padrão:</span><span class="sxs-lookup"><span data-stu-id="ba408-156">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="ba408-157">Proprietário: pode gerenciar tudo, incluindo o acesso</span><span class="sxs-lookup"><span data-stu-id="ba408-157">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="ba408-158">Colaborador: pode gerenciar tudo, exceto o acesso</span><span class="sxs-lookup"><span data-stu-id="ba408-158">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="ba408-159">Leitor: pode ver tudo, mas não pode fazer alterações</span><span class="sxs-lookup"><span data-stu-id="ba408-159">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="ba408-160">**É possível copiar ou exportar um disco gerenciado para uma conta de armazenamento privado?**</span><span class="sxs-lookup"><span data-stu-id="ba408-160">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="ba408-161">Você pode obter um URI de assinatura de acesso compartilhado somente leitura para o disco gerenciado e usá-la para copiar o conteúdo para uma conta de armazenamento privado ou armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="ba408-161">You can get a read-only shared access signature URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span></span>

<span data-ttu-id="ba408-162">**Posso criar uma cópia do meu disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="ba408-162">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="ba408-163">Os clientes podem tirar um instantâneo de seus discos gerenciados e, em seguida, usar o instantâneo para criar outro disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="ba408-163">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span></span>

<span data-ttu-id="ba408-164">**Ainda há suporte para discos não gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="ba408-164">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="ba408-165">Sim.</span><span class="sxs-lookup"><span data-stu-id="ba408-165">Yes.</span></span> <span data-ttu-id="ba408-166">Há suporte para discos gerenciados e não gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ba408-166">We support unmanaged and managed disks.</span></span> <span data-ttu-id="ba408-167">Recomendamos que você use discos gerenciados para novas cargas de trabalho e migre suas cargas de trabalho atuais para discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ba408-167">We recommend that you use managed disks for new workloads and migrate your current workloads to managed disks.</span></span>


<span data-ttu-id="ba408-168">**Se eu criar um disco de 128 GB e aumentar o tamanho para 130 GB, serei cobrado pelo próximo tamanho de disco (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="ba408-168">**If I create a 128-GB disk and then increase the size to 130 GB, will I be charged for the next disk size (512 GB)?**</span></span>

<span data-ttu-id="ba408-169">Sim.</span><span class="sxs-lookup"><span data-stu-id="ba408-169">Yes.</span></span>

<span data-ttu-id="ba408-170">**Posso criar armazenamento com redundância local, armazenamento com redundância geográfica e discos de armazenamento com redundância de zona gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="ba408-170">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="ba408-171">O Azure Managed Disks atualmente dá suporte apenas a discos gerenciados de armazenamento com redundância local.</span><span class="sxs-lookup"><span data-stu-id="ba408-171">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="ba408-172">**Posso reduzir ou diminuir o tamanho de meus discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="ba408-172">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="ba408-173">Não.</span><span class="sxs-lookup"><span data-stu-id="ba408-173">No.</span></span> <span data-ttu-id="ba408-174">Não há suporte para esse recurso no momento.</span><span class="sxs-lookup"><span data-stu-id="ba408-174">This feature is not supported currently.</span></span> 

<span data-ttu-id="ba408-175">**Posso alterar a propriedade de nome do computador quando um disco do sistema operacional especializado (não criado usando a ferramenta de Preparação do Sistema ou generalizado) é usado para provisionar uma máquina virtual?**</span><span class="sxs-lookup"><span data-stu-id="ba408-175">**Can I change the computer name property when a specialized (not created by using the System Preparation tool or generalized) operating system disk is used to provision a VM?**</span></span>

<span data-ttu-id="ba408-176">Não.</span><span class="sxs-lookup"><span data-stu-id="ba408-176">No.</span></span> <span data-ttu-id="ba408-177">Não é possível atualizar a propriedade de nome do computador.</span><span class="sxs-lookup"><span data-stu-id="ba408-177">You can't update the computer name property.</span></span> <span data-ttu-id="ba408-178">A nova VM a herda do pai, que foi usado para criar o disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="ba408-178">The new VM inherits it from the parent VM, which was used to create the operating system disk.</span></span> 

<span data-ttu-id="ba408-179">**Onde posso encontrar modelos do Azure Resource Manager de exemplo para criar VMs com discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="ba408-179">**Where can I find sample Azure Resource Manager templates to create VMs with managed disks?**</span></span>
* [<span data-ttu-id="ba408-180">Lista de modelos que usam o Managed Disks</span><span class="sxs-lookup"><span data-stu-id="ba408-180">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="ba408-181">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="ba408-181">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="ba408-182">Managed Disks e Criptografia de Serviço de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="ba408-182">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="ba408-183">**A Criptografia do Serviço de Armazenamento do Azure fica habilitada por padrão quando crio um disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="ba408-183">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="ba408-184">Sim.</span><span class="sxs-lookup"><span data-stu-id="ba408-184">Yes.</span></span>

<span data-ttu-id="ba408-185">**Quem gerencia as chaves de criptografia?**</span><span class="sxs-lookup"><span data-stu-id="ba408-185">**Who manages the encryption keys?**</span></span>

<span data-ttu-id="ba408-186">A Microsoft gerencia as chaves de criptografia.</span><span class="sxs-lookup"><span data-stu-id="ba408-186">Microsoft manages the encryption keys.</span></span>

<span data-ttu-id="ba408-187">**Posso desabilitar a Criptografia do Serviço de Armazenamento para meus discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="ba408-187">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="ba408-188">Não.</span><span class="sxs-lookup"><span data-stu-id="ba408-188">No.</span></span>

<span data-ttu-id="ba408-189">**A Criptografia do Serviço de Armazenamento só está disponível em regiões específicas?**</span><span class="sxs-lookup"><span data-stu-id="ba408-189">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="ba408-190">Não.</span><span class="sxs-lookup"><span data-stu-id="ba408-190">No.</span></span> <span data-ttu-id="ba408-191">Ele está disponível em todas as regiões em que os discos gerenciados estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ba408-191">It's available in all the regions where Managed Disks is available.</span></span> <span data-ttu-id="ba408-192">O Managed Disks está disponível em todas as regiões públicas e na Alemanha.</span><span class="sxs-lookup"><span data-stu-id="ba408-192">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="ba408-193">**Como posso descobrir se o disco gerenciado está criptografado?**</span><span class="sxs-lookup"><span data-stu-id="ba408-193">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="ba408-194">Você pode descobrir a data em que um disco gerenciado foi criado no portal do Azure, na CLI do Azure e no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba408-194">You can find out the time when a managed disk was created from the Azure portal, the Azure CLI, and PowerShell.</span></span> <span data-ttu-id="ba408-195">Se a data é posterior a 9 de junho de 2017, o disco está criptografado.</span><span class="sxs-lookup"><span data-stu-id="ba408-195">If the time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="ba408-196">**Como faço para criptografar meus discos existentes que foram criados antes de 10 de junho de 2017?**</span><span class="sxs-lookup"><span data-stu-id="ba408-196">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="ba408-197">A partir de 10 de junho de 2017, os novos dados gravados em discos gerenciados existentes serão criptografados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ba408-197">As of June 10, 2017, new data written to existing managed disks is automatically encrypted.</span></span> <span data-ttu-id="ba408-198">Nós também estamos planejando criptografar os dados existentes e a criptografia ocorrerá assincronamente em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="ba408-198">We are also planning to encrypt existing data, and the encryption will happen asynchronously in the background.</span></span> <span data-ttu-id="ba408-199">Se você precisar criptografar os dados existentes agora, crie uma cópia do disco.</span><span class="sxs-lookup"><span data-stu-id="ba408-199">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="ba408-200">Os novos discos serão criptografados.</span><span class="sxs-lookup"><span data-stu-id="ba408-200">New disks will be encrypted.</span></span>

* [<span data-ttu-id="ba408-201">Copiar discos gerenciados usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ba408-201">Copy managed disks by using the Azure CLI</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="ba408-202">Copiar discos gerenciados usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba408-202">Copy managed disks by using PowerShell</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="ba408-203">**Os instantâneos gerenciados e as imagens são criptografados?**</span><span class="sxs-lookup"><span data-stu-id="ba408-203">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="ba408-204">Sim.</span><span class="sxs-lookup"><span data-stu-id="ba408-204">Yes.</span></span> <span data-ttu-id="ba408-205">Todos os instantâneos e imagens criados após 9 de junho de 2017 são criptografados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ba408-205">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="ba408-206">**Posso converter máquinas virtuais com discos não gerenciados que estão localizados em contas de armazenamento ou criptografados anteriormente em discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="ba408-206">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span></span>

<span data-ttu-id="ba408-207">Sim</span><span class="sxs-lookup"><span data-stu-id="ba408-207">Yes</span></span>

<span data-ttu-id="ba408-208">**Um VHD exportado de um disco gerenciado ou instantâneo também será criptografado?**</span><span class="sxs-lookup"><span data-stu-id="ba408-208">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="ba408-209">Não.</span><span class="sxs-lookup"><span data-stu-id="ba408-209">No.</span></span> <span data-ttu-id="ba408-210">Mas se você exportar um VHD para uma conta de armazenamento criptografada de um disco gerenciado ou instantâneo criptografado, ele estará criptografado.</span><span class="sxs-lookup"><span data-stu-id="ba408-210">But if you export a VHD to an encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="ba408-211">Discos Premium: gerenciados e não gerenciados</span><span class="sxs-lookup"><span data-stu-id="ba408-211">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="ba408-212">**Se uma VM usa uma série de tamanho que dá suporte ao Armazenamento Premium, como um DSv2, é possível anexar discos de dados standard e premium?**</span><span class="sxs-lookup"><span data-stu-id="ba408-212">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="ba408-213">Sim.</span><span class="sxs-lookup"><span data-stu-id="ba408-213">Yes.</span></span>

<span data-ttu-id="ba408-214">**É possível anexar discos de dados standard e premium a uma série de tamanho que não oferece suporte a armazenamento Premium, como as séries D, Dv2, G ou F?**</span><span class="sxs-lookup"><span data-stu-id="ba408-214">**Can I attach both premium and standard data disks to a size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="ba408-215">Não.</span><span class="sxs-lookup"><span data-stu-id="ba408-215">No.</span></span> <span data-ttu-id="ba408-216">Você só pode anexar discos de dados standard às VMs que não usam uma série de tamanho que dá suporte ao Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="ba408-216">You can attach only standard data disks to VMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="ba408-217">**Se criar um disco de dados premium com base em um VHD existente que tinha 80 GB, quanto isso custará?**</span><span class="sxs-lookup"><span data-stu-id="ba408-217">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="ba408-218">Um disco de dados premium criado com base em um VHD de 80 GB é tratado como o próximo tamanho de disco premium disponível, um disco P10.</span><span class="sxs-lookup"><span data-stu-id="ba408-218">A premium data disk created from an 80-GB VHD is treated as the next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="ba408-219">Você será cobrado de acordo com o preço do disco P10.</span><span class="sxs-lookup"><span data-stu-id="ba408-219">You're charged according to the P10 disk pricing.</span></span>

<span data-ttu-id="ba408-220">**Existem custos de transação para usar o Armazenamento Premium?**</span><span class="sxs-lookup"><span data-stu-id="ba408-220">**Are there transaction costs to use Premium Storage?**</span></span>

<span data-ttu-id="ba408-221">Há um custo fixo para cada tamanho de disco, que vem provisionado com limites específicos de IOPS e taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="ba408-221">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="ba408-222">Os outros custos são largura de banda de saída e recurso de instantâneos, caso aplicável.</span><span class="sxs-lookup"><span data-stu-id="ba408-222">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="ba408-223">Para saber mais, confira a [página de preço](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="ba408-223">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="ba408-224">**Quais são os limites de IOPS e taxa de transferência que posso obter do cache de disco?**</span><span class="sxs-lookup"><span data-stu-id="ba408-224">**What are the limits for IOPS and throughput that I can get from the disk cache?**</span></span>

<span data-ttu-id="ba408-225">Os limites combinados para cache e SSD local para um item da série DS são 4.000 IOPS por núcleo e 33 MB por segundo por núcleo.</span><span class="sxs-lookup"><span data-stu-id="ba408-225">The combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="ba408-226">A série GS oferece 5.000 IOPS por núcleo e 50 MB por segundo por núcleo.</span><span class="sxs-lookup"><span data-stu-id="ba408-226">The GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="ba408-227">**O SSD local tem suporte para uma VM do Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="ba408-227">**Is the local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="ba408-228">O SSD local é um armazenamento temporário fornecido com uma VM do Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="ba408-228">The local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="ba408-229">Não há custo adicional para esse armazenamento temporário.</span><span class="sxs-lookup"><span data-stu-id="ba408-229">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="ba408-230">Recomendamos que você não use esse SSD local para armazenar os dados do aplicativo porque ele não é mantido no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba408-230">We recommend that you do not use this local SSD to store your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="ba408-231">**Existem repercussões pelo uso de TRIM em discos premium?**</span><span class="sxs-lookup"><span data-stu-id="ba408-231">**Are there any repercussions for the use of TRIM on premium disks?**</span></span>

<span data-ttu-id="ba408-232">Não há nenhuma desvantagem em usar CORTE nos Discos do Azure Premium ou Standard.</span><span class="sxs-lookup"><span data-stu-id="ba408-232">There is no downside to the use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="ba408-233">Novos tamanhos de disco: gerenciados e não gerenciados</span><span class="sxs-lookup"><span data-stu-id="ba408-233">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="ba408-234">**Qual é o maior tamanho de disco com suporte para o sistema operacional e os discos de dados?**</span><span class="sxs-lookup"><span data-stu-id="ba408-234">**What is the largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="ba408-235">O tipo de partição a que o Azure dá suporte para um disco do sistema operacional é o MBR (registro mestre de inicialização).</span><span class="sxs-lookup"><span data-stu-id="ba408-235">The partition type that Azure supports for an operating system disk is the master boot record (MBR).</span></span> <span data-ttu-id="ba408-236">O formato do MBR dá suporte a tamanho de disco de até 2 TB.</span><span class="sxs-lookup"><span data-stu-id="ba408-236">The MBR format supports a disk size up to 2 TB.</span></span> <span data-ttu-id="ba408-237">O maior tamanho a que o Azure dá suporte para um disco do sistema operacional é 2 TB.</span><span class="sxs-lookup"><span data-stu-id="ba408-237">The largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="ba408-238">O Azure dá suporte a até 4 TB em discos de dados.</span><span class="sxs-lookup"><span data-stu-id="ba408-238">Azure supports up to 4 TB for data disks.</span></span> 

<span data-ttu-id="ba408-239">**Qual é o maior tamanho de blob de página com suporte?**</span><span class="sxs-lookup"><span data-stu-id="ba408-239">**What is the largest page blob size that's supported?**</span></span>

<span data-ttu-id="ba408-240">O maior tamanho de blob de página a que o Azure dá suporte é 8 TB (8.191 GB).</span><span class="sxs-lookup"><span data-stu-id="ba408-240">The largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="ba408-241">Não há suporte para blobs de página maiores que 4 TB (4.095 GB) anexados a uma VM como dados ou discos do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="ba408-241">We don't support page blobs larger than 4 TB (4,095 GB) attached to a VM as data or operating system disks.</span></span>

<span data-ttu-id="ba408-242">**Preciso usar uma nova versão das ferramentas do Azure para criar, anexar, redimensionar e carregar discos maiores que 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="ba408-242">**Do I need to use a new version of Azure tools to create, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="ba408-243">Você não precisa atualizar as ferramentas existentes do Azure para criar, anexar ou redimensionar discos maiores que 1 TB.</span><span class="sxs-lookup"><span data-stu-id="ba408-243">You don't need to upgrade your existing Azure tools to create, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="ba408-244">Para carregar o arquivo VHD local diretamente no Azure como um blob de página ou disco não gerenciado, você precisará usar os conjuntos de ferramentas mais recentes:</span><span class="sxs-lookup"><span data-stu-id="ba408-244">To upload your VHD file from on-premises directly to Azure as a page blob or unmanaged disk, you need to use the latest tool sets:</span></span>

|<span data-ttu-id="ba408-245">Ferramentas do Azure</span><span class="sxs-lookup"><span data-stu-id="ba408-245">Azure tools</span></span>      | <span data-ttu-id="ba408-246">Versões com suporte</span><span class="sxs-lookup"><span data-stu-id="ba408-246">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="ba408-247">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba408-247">Azure PowerShell</span></span> | <span data-ttu-id="ba408-248">Número de versão 4.1.0: versão de junho de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="ba408-248">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="ba408-249">CLI do Azure v1</span><span class="sxs-lookup"><span data-stu-id="ba408-249">Azure CLI v1</span></span>     | <span data-ttu-id="ba408-250">Número de versão 0.10.13: versão de maio de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="ba408-250">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="ba408-251">AzCopy</span><span class="sxs-lookup"><span data-stu-id="ba408-251">AzCopy</span></span>           | <span data-ttu-id="ba408-252">Número de versão 6.1.0: versão de junho de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="ba408-252">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="ba408-253">O suporte à CLI do Azure v2 e ao Gerenciador de Armazenamento do Azure estará disponível em breve.</span><span class="sxs-lookup"><span data-stu-id="ba408-253">The support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="ba408-254">**Os tamanhos de disco P4 e P6 têm suporte para discos não gerenciados ou blobs de página?**</span><span class="sxs-lookup"><span data-stu-id="ba408-254">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="ba408-255">Não.</span><span class="sxs-lookup"><span data-stu-id="ba408-255">No.</span></span> <span data-ttu-id="ba408-256">Os tamanhos de disco P4 (32 GB) e P6 (64 GB) têm suporte somente para discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ba408-256">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="ba408-257">O suporte a discos não gerenciados e blobs de página será lançado em breve.</span><span class="sxs-lookup"><span data-stu-id="ba408-257">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="ba408-258">**Se o meu disco gerenciado premium existente com menos de 64 GB foi criado antes da habilitação da pequeno disco (por volta de 15 de junho de 2017), como ele é cobrado?**</span><span class="sxs-lookup"><span data-stu-id="ba408-258">**If my existing premium managed disk less than 64 GB was created before the small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="ba408-259">Os discos pequenos premium com menos de 64 GB continuam a ser cobrados de acordo com o tipo de preços P10.</span><span class="sxs-lookup"><span data-stu-id="ba408-259">Existing small premium disks less than 64 GB continue to be billed according to the P10 pricing tier.</span></span> 

<span data-ttu-id="ba408-260">**Como alternar a camada de disco dos discos premium pequenos com menos de 64 GB de P10 para P4 ou P6?**</span><span class="sxs-lookup"><span data-stu-id="ba408-260">**How can I switch the disk tier of small premium disks less than 64 GB from P10 to P4 or P6?**</span></span>

<span data-ttu-id="ba408-261">Você pode tirar um instantâneo dos discos pequenos e criar um disco para alternar automaticamente o tipo de preço para P4 ou P6 com base no tamanho provisionado.</span><span class="sxs-lookup"><span data-stu-id="ba408-261">You can take a snapshot of your small disks and then create a disk to automatically switch the pricing tier to P4 or P6 based on the provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="ba408-262">E se dúvida não foi respondida aqui?</span><span class="sxs-lookup"><span data-stu-id="ba408-262">What if my question isn't answered here?</span></span>

<span data-ttu-id="ba408-263">Se sua pergunta não estiver listada aqui, fale conosco e nós ajudaremos a encontrar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="ba408-263">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="ba408-264">Você pode postar uma pergunta no final deste artigo nos comentários.</span><span class="sxs-lookup"><span data-stu-id="ba408-264">You can post a question at the end of this article in the comments.</span></span> <span data-ttu-id="ba408-265">Para se comunicar com a equipe do Armazenamento do Azure e outros membros da comunidade sobre este artigo, use o [Fórum do Armazenamento do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="ba408-265">To engage with the Azure Storage team and other community members about this article, use the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="ba408-266">Para solicitar recursos, envie suas solicitações e ideias para o [Fórum de comentários do Armazenamento do Azure](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="ba408-266">To request features, submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
