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
ms.openlocfilehash: 31d0aa67b6ca58b75b432ae94f93ebcf6d730380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="76c9a-103">Perguntas frequentes sobre discos de VM IaaS do Azure e discos premium gerenciados e não gerenciados</span><span class="sxs-lookup"><span data-stu-id="76c9a-103">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="76c9a-104">Este artigo responde a algumas perguntas frequentes sobre o Azure Managed Disks e o Armazenamento Premium do Azure.</span><span class="sxs-lookup"><span data-stu-id="76c9a-104">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="76c9a-105">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="76c9a-105">Managed Disks</span></span>

<span data-ttu-id="76c9a-106">**O que é o Azure Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-106">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="76c9a-107">Managed Disks é um recurso que simplifica o gerenciamento de disco para VMs IaaS do Azure manipulando o gerenciamento de conta de armazenamento para você.</span><span class="sxs-lookup"><span data-stu-id="76c9a-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="76c9a-108">Para obter mais informações, consulte Olá [visão geral de discos gerenciados](storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="76c9a-108">For more information, see hello [Managed Disks overview](storage-managed-disks-overview.md).</span></span>

<span data-ttu-id="76c9a-109">**Se eu criar um disco gerenciado standard com base em um VHD existente que tem 80 GB, quanto isso custará?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-109">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="76c9a-110">Um disco gerenciado padrão criado a partir de um VHD de 80 GB é tratado como Olá próximo padrão tamanho de disco disponível, que é um disco S10.</span><span class="sxs-lookup"><span data-stu-id="76c9a-110">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="76c9a-111">Você será cobrado de acordo toohello S10 disco preços.</span><span class="sxs-lookup"><span data-stu-id="76c9a-111">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="76c9a-112">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="76c9a-112">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="76c9a-113">**Existem custos de transação de discos gerenciados standard?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-113">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="76c9a-114">Sim.</span><span class="sxs-lookup"><span data-stu-id="76c9a-114">Yes.</span></span> <span data-ttu-id="76c9a-115">Você é cobrado por cada transação.</span><span class="sxs-lookup"><span data-stu-id="76c9a-115">You're charged for each transaction.</span></span> <span data-ttu-id="76c9a-116">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="76c9a-116">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="76c9a-117">**Para um disco gerenciado standard, serei ser cobrado para tamanho real de Olá Olá dados hello ou para capacidade de saudação provisionada de disco Olá?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-117">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="76c9a-118">Você será cobrado com base na capacidade de saudação provisionada de disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="76c9a-118">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="76c9a-119">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="76c9a-119">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="76c9a-120">**O preço dos discos premium gerenciados é diferente do preço dos discos não gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-120">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="76c9a-121">saudação de preços de discos premium gerenciado é Olá igual a discos premium não gerenciado.</span><span class="sxs-lookup"><span data-stu-id="76c9a-121">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="76c9a-122">**Alterar Olá armazenamento tipo de conta (Standard ou Premium) de meus discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-122">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="76c9a-123">Sim.</span><span class="sxs-lookup"><span data-stu-id="76c9a-123">Yes.</span></span> <span data-ttu-id="76c9a-124">Você pode alterar o tipo de conta de armazenamento Olá discos gerenciados usando Olá portal do Azure, PowerShell ou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="76c9a-124">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="76c9a-125">**Há uma maneira que eu possa copiar ou exportar uma conta de armazenamento particular de tooa de disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-125">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="76c9a-126">Sim.</span><span class="sxs-lookup"><span data-stu-id="76c9a-126">Yes.</span></span> <span data-ttu-id="76c9a-127">Você pode exportar os discos gerenciados usando Olá portal do Azure, PowerShell ou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="76c9a-127">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="76c9a-128">**Pode usar um arquivo VHD em uma conta de armazenamento do Azure toocreate um disco gerenciado com uma assinatura diferente?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="76c9a-129">Não.</span><span class="sxs-lookup"><span data-stu-id="76c9a-129">No.</span></span>

<span data-ttu-id="76c9a-130">**Pode usar um arquivo VHD em uma conta de armazenamento do Azure toocreate um disco gerenciado em uma região diferente?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-130">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="76c9a-131">Não.</span><span class="sxs-lookup"><span data-stu-id="76c9a-131">No.</span></span>

<span data-ttu-id="76c9a-132">**Existem limitações de escala para clientes que usam discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-132">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="76c9a-133">Discos gerenciados elimina os limites de saudação associados às contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="76c9a-133">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="76c9a-134">No entanto, o número de saudação de discos gerenciados por assinatura é limitado too2, 000 por padrão.</span><span class="sxs-lookup"><span data-stu-id="76c9a-134">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="76c9a-135">Você pode chamar o suporte tooincrease esse número.</span><span class="sxs-lookup"><span data-stu-id="76c9a-135">You can call support tooincrease this number.</span></span>

<span data-ttu-id="76c9a-136">**Posso fazer um instantâneo incremental de um disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-136">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="76c9a-137">Não.</span><span class="sxs-lookup"><span data-stu-id="76c9a-137">No.</span></span> <span data-ttu-id="76c9a-138">recurso de instantâneo atual Olá cria uma cópia completa de um disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="76c9a-138">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="76c9a-139">No entanto, nós estamos planejando toosupport de instantâneos incrementais em Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="76c9a-139">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="76c9a-140">**As VMs em um conjunto de disponibilidade podem consistir de uma combinação de discos gerenciados e não gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-140">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="76c9a-141">Não.</span><span class="sxs-lookup"><span data-stu-id="76c9a-141">No.</span></span> <span data-ttu-id="76c9a-142">Olá VMs em um conjunto de disponibilidade deve usar discos todas gerenciados ou todos os discos não gerenciados.</span><span class="sxs-lookup"><span data-stu-id="76c9a-142">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="76c9a-143">Quando você cria um conjunto de disponibilidade, você pode escolher qual tipo de disco desejado toouse.</span><span class="sxs-lookup"><span data-stu-id="76c9a-143">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="76c9a-144">**É a opção de padrão de saudação de discos gerenciados no hello portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-144">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="76c9a-145">Não no momento, mas ela ficará padrão Olá Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="76c9a-145">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="76c9a-146">**É possível criar um disco gerenciado vazio?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-146">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="76c9a-147">Sim.</span><span class="sxs-lookup"><span data-stu-id="76c9a-147">Yes.</span></span> <span data-ttu-id="76c9a-148">Você pode criar um disco vazio.</span><span class="sxs-lookup"><span data-stu-id="76c9a-148">You can create an empty disk.</span></span> <span data-ttu-id="76c9a-149">Um disco gerenciado pode ser criado independentemente de uma VM, por exemplo, sem anexá-lo tooa VM.</span><span class="sxs-lookup"><span data-stu-id="76c9a-149">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="76c9a-150">**O que é a contagem de domínios de falha de saudação com suporte para um conjunto de disponibilidade que usa discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-150">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="76c9a-151">Dependendo da região de saudação onde o conjunto de disponibilidade de saudação que usa discos gerenciado está localizado, a contagem de domínios de falha de saudação com suporte é 2 ou 3.</span><span class="sxs-lookup"><span data-stu-id="76c9a-151">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="76c9a-152">**Como é a conta de armazenamento padrão de saudação para configurar um diagnóstico?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-152">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="76c9a-153">Você configura uma conta de armazenamento privado para diagnóstico da VM.</span><span class="sxs-lookup"><span data-stu-id="76c9a-153">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="76c9a-154">Em Olá futuro, planejamos diagnóstico tooswitch tooManaged discos também.</span><span class="sxs-lookup"><span data-stu-id="76c9a-154">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="76c9a-155">**O tipo de suporte ao Controle de Acesso Baseado em Função está disponível para o Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-155">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="76c9a-156">O Managed Disks oferece suporte a três funções principais padrão:</span><span class="sxs-lookup"><span data-stu-id="76c9a-156">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="76c9a-157">Proprietário: pode gerenciar tudo, incluindo o acesso</span><span class="sxs-lookup"><span data-stu-id="76c9a-157">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="76c9a-158">Colaborador: pode gerenciar tudo, exceto o acesso</span><span class="sxs-lookup"><span data-stu-id="76c9a-158">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="76c9a-159">Leitor: pode ver tudo, mas não pode fazer alterações</span><span class="sxs-lookup"><span data-stu-id="76c9a-159">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="76c9a-160">**Há uma maneira que eu possa copiar ou exportar uma conta de armazenamento particular de tooa de disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-160">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="76c9a-161">Você pode obter uma assinatura de acesso compartilhado somente leitura URI para Olá gerenciado em disco e usá-lo toocopy Olá conteúdo tooa privada local ou conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="76c9a-161">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="76c9a-162">**Posso criar uma cópia do meu disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-162">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="76c9a-163">Os clientes podem tirar um instantâneo dos seus discos gerenciados e usar Olá instantâneo toocreate outro disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="76c9a-163">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="76c9a-164">**Ainda há suporte para discos não gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-164">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="76c9a-165">Sim.</span><span class="sxs-lookup"><span data-stu-id="76c9a-165">Yes.</span></span> <span data-ttu-id="76c9a-166">Há suporte para discos gerenciados e não gerenciados.</span><span class="sxs-lookup"><span data-stu-id="76c9a-166">We support unmanaged and managed disks.</span></span> <span data-ttu-id="76c9a-167">É recomendável que você use discos gerenciados para novas cargas de trabalho e migra seus discos de toomanaged cargas de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="76c9a-167">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="76c9a-168">**Se eu criar um disco de 128 GB e, em seguida, aumentar Olá tamanho too130 GB, serei ser cobrado para tamanho de disco seguinte hello (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-168">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="76c9a-169">Sim.</span><span class="sxs-lookup"><span data-stu-id="76c9a-169">Yes.</span></span>

<span data-ttu-id="76c9a-170">**Posso criar armazenamento com redundância local, armazenamento com redundância geográfica e discos de armazenamento com redundância de zona gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-170">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="76c9a-171">O Azure Managed Disks atualmente dá suporte apenas a discos gerenciados de armazenamento com redundância local.</span><span class="sxs-lookup"><span data-stu-id="76c9a-171">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="76c9a-172">**Posso reduzir ou diminuir o tamanho de meus discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-172">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="76c9a-173">Não.</span><span class="sxs-lookup"><span data-stu-id="76c9a-173">No.</span></span> <span data-ttu-id="76c9a-174">Não há suporte para esse recurso no momento.</span><span class="sxs-lookup"><span data-stu-id="76c9a-174">This feature is not supported currently.</span></span> 

<span data-ttu-id="76c9a-175">**Alterar propriedade de nome de computador hello quando um especializada (não criada usando a ferramenta de preparação do sistema hello ou generalizado) operacional do disco do sistema é usado tooprovision uma máquina virtual?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-175">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="76c9a-176">Não.</span><span class="sxs-lookup"><span data-stu-id="76c9a-176">No.</span></span> <span data-ttu-id="76c9a-177">Você não pode atualizar a propriedade de nome de computador hello.</span><span class="sxs-lookup"><span data-stu-id="76c9a-177">You can't update hello computer name property.</span></span> <span data-ttu-id="76c9a-178">Olá nova VM herda-lo do hello pai VM, que era o disco do sistema operacional Olá toocreate usado.</span><span class="sxs-lookup"><span data-stu-id="76c9a-178">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="76c9a-179">**Onde encontrar o exemplo do Azure Resource Manager modelos toocreate VMs com discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-179">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="76c9a-180">Lista de modelos que usam o Managed Disks</span><span class="sxs-lookup"><span data-stu-id="76c9a-180">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="76c9a-181">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="76c9a-181">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="76c9a-182">Managed Disks e Criptografia de Serviço de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="76c9a-182">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="76c9a-183">**A Criptografia do Serviço de Armazenamento do Azure fica habilitada por padrão quando crio um disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-183">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="76c9a-184">Sim.</span><span class="sxs-lookup"><span data-stu-id="76c9a-184">Yes.</span></span>

<span data-ttu-id="76c9a-185">**Quem gerencia as chaves de criptografia Olá?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-185">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="76c9a-186">A Microsoft gerencia chaves de criptografia de saudação.</span><span class="sxs-lookup"><span data-stu-id="76c9a-186">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="76c9a-187">**Posso desabilitar a Criptografia do Serviço de Armazenamento para meus discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-187">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="76c9a-188">Não.</span><span class="sxs-lookup"><span data-stu-id="76c9a-188">No.</span></span>

<span data-ttu-id="76c9a-189">**A Criptografia do Serviço de Armazenamento só está disponível em regiões específicas?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-189">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="76c9a-190">Não.</span><span class="sxs-lookup"><span data-stu-id="76c9a-190">No.</span></span> <span data-ttu-id="76c9a-191">Ele está disponível em todas as regiões de saudação em discos gerenciado está disponível.</span><span class="sxs-lookup"><span data-stu-id="76c9a-191">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="76c9a-192">O Managed Disks está disponível em todas as regiões públicas e na Alemanha.</span><span class="sxs-lookup"><span data-stu-id="76c9a-192">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="76c9a-193">**Como posso descobrir se o disco gerenciado está criptografado?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-193">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="76c9a-194">Você pode descobrir a hora de saudação quando um disco gerenciado foi criado de saudação portal do Azure, Olá CLI do Azure e do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76c9a-194">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="76c9a-195">Se houver tempo Olá após 9 de junho de 2017, o disco está criptografado.</span><span class="sxs-lookup"><span data-stu-id="76c9a-195">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="76c9a-196">**Como faço para criptografar meus discos existentes que foram criados antes de 10 de junho de 2017?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-196">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="76c9a-197">A partir de 10 de junho de 2017, novos dados gravados discos tooexisting gerenciado são criptografados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="76c9a-197">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="76c9a-198">Nós também estamos planejando tooencrypt os dados existentes e criptografia Olá acontecerá assincronamente no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="76c9a-198">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="76c9a-199">Se você precisar criptografar os dados existentes agora, crie uma cópia do disco.</span><span class="sxs-lookup"><span data-stu-id="76c9a-199">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="76c9a-200">Os novos discos serão criptografados.</span><span class="sxs-lookup"><span data-stu-id="76c9a-200">New disks will be encrypted.</span></span>

* [<span data-ttu-id="76c9a-201">Copiar discos gerenciados usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="76c9a-201">Copy managed disks by using hello Azure CLI</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="76c9a-202">Copiar discos gerenciados usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="76c9a-202">Copy managed disks by using PowerShell</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="76c9a-203">**Os instantâneos gerenciados e as imagens são criptografados?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-203">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="76c9a-204">Sim.</span><span class="sxs-lookup"><span data-stu-id="76c9a-204">Yes.</span></span> <span data-ttu-id="76c9a-205">Todos os instantâneos e imagens criados após 9 de junho de 2017 são criptografados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="76c9a-205">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="76c9a-206">**Pode converter máquinas virtuais com discos não gerenciados que estão localizados em contas de armazenamento ou foram discos toomanaged previamente criptografado?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-206">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="76c9a-207">Sim</span><span class="sxs-lookup"><span data-stu-id="76c9a-207">Yes</span></span>

<span data-ttu-id="76c9a-208">**Um VHD exportado de um disco gerenciado ou instantâneo também será criptografado?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-208">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="76c9a-209">Não.</span><span class="sxs-lookup"><span data-stu-id="76c9a-209">No.</span></span> <span data-ttu-id="76c9a-210">Mas se você exportar um VHD tooan criptografado conta de armazenamento de um disco gerenciado criptografado ou instantâneo e, em seguida, ele é criptografado.</span><span class="sxs-lookup"><span data-stu-id="76c9a-210">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="76c9a-211">Discos Premium: gerenciados e não gerenciados</span><span class="sxs-lookup"><span data-stu-id="76c9a-211">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="76c9a-212">**Se uma VM usa uma série de tamanho que dá suporte ao Armazenamento Premium, como um DSv2, é possível anexar discos de dados standard e premium?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-212">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="76c9a-213">Sim.</span><span class="sxs-lookup"><span data-stu-id="76c9a-213">Yes.</span></span>

<span data-ttu-id="76c9a-214">**É possível anexar premium e standard discos tooa tamanho séries de dados não dá suporte a armazenamento Premium, como a série D, Dv2, G ou F?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-214">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="76c9a-215">Não.</span><span class="sxs-lookup"><span data-stu-id="76c9a-215">No.</span></span> <span data-ttu-id="76c9a-216">Você pode anexar apenas tooVMs de discos padrão para dados que não usam uma série de tamanho que dá suporte ao armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="76c9a-216">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="76c9a-217">**Se criar um disco de dados premium com base em um VHD existente que tinha 80 GB, quanto isso custará?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-217">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="76c9a-218">Um disco de dados premium criado a partir de um VHD de 80 GB é tratado como o tamanho de disco disponíveis para o próximo premium Olá, é um disco P10.</span><span class="sxs-lookup"><span data-stu-id="76c9a-218">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="76c9a-219">Você será cobrado de acordo toohello P10 disco preços.</span><span class="sxs-lookup"><span data-stu-id="76c9a-219">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="76c9a-220">**Há transações custos toouse armazenamento Premium?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-220">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="76c9a-221">Há um custo fixo para cada tamanho de disco, que vem provisionado com limites específicos de IOPS e taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="76c9a-221">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="76c9a-222">Olá outros custos são largura de banda de saída e a capacidade de instantâneo, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="76c9a-222">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="76c9a-223">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="76c9a-223">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="76c9a-224">**Quais são os limites de saudação de IOPS e taxa de transferência que posso obter do cache de disco Olá?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-224">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="76c9a-225">Olá combinado de limites para cache e SSD local para uma série DS são 4.000 IOPS por núcleo e 33 MB por segundo por núcleo.</span><span class="sxs-lookup"><span data-stu-id="76c9a-225">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="76c9a-226">Olá série GS oferece a 5.000 IOPS por núcleo e 50 MB por segundo por núcleo.</span><span class="sxs-lookup"><span data-stu-id="76c9a-226">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="76c9a-227">**É hello que SSD local tem suporte para uma VM de discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-227">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="76c9a-228">Olá SSD local é o armazenamento temporário que acompanha uma VM de discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="76c9a-228">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="76c9a-229">Não há custo adicional para esse armazenamento temporário.</span><span class="sxs-lookup"><span data-stu-id="76c9a-229">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="76c9a-230">É recomendável que você não use esse toostore SSD local os dados do aplicativo porque ele não é mantido no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="76c9a-230">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="76c9a-231">**São existe qualquer repercussões para Olá usar de TRIM em discos premium?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-231">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="76c9a-232">Não há nenhum uso de toohello desvantagem de TRIM em discos do Azure em uma premium ou discos padrão.</span><span class="sxs-lookup"><span data-stu-id="76c9a-232">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="76c9a-233">Novos tamanhos de disco: gerenciados e não gerenciados</span><span class="sxs-lookup"><span data-stu-id="76c9a-233">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="76c9a-234">**Qual é Olá maior tamanho de disco com suporte para o sistema operacional e discos de dados?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-234">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="76c9a-235">tipo de partição de Hello Azure oferece suporte para um disco do sistema operacional é Olá mestre de inicialização MBR (registro).</span><span class="sxs-lookup"><span data-stu-id="76c9a-235">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="76c9a-236">formato MBR Olá dá suporte a um tamanho de disco até too2 TB.</span><span class="sxs-lookup"><span data-stu-id="76c9a-236">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="76c9a-237">Olá maior tamanho que o Azure oferece suporte para um disco do sistema operacional é de 2 TB.</span><span class="sxs-lookup"><span data-stu-id="76c9a-237">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="76c9a-238">O Azure suporta até too4 TB para discos de dados.</span><span class="sxs-lookup"><span data-stu-id="76c9a-238">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="76c9a-239">**O que é Olá maior blob tamanho de página com suporte?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-239">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="76c9a-240">Olá página blob maior que o Azure suporta é 8 TB (8.191 GB).</span><span class="sxs-lookup"><span data-stu-id="76c9a-240">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="76c9a-241">Não há suporte para blobs de página maiores que 4 TB (4.095 GB) anexado tooa VM como dados ou discos do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="76c9a-241">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="76c9a-242">**É necessário toouse uma nova versão de ferramentas do Azure toocreate, anexar, redimensionar e carregar discos maiores que 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-242">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="76c9a-243">Você não precisa tooupgrade seu toocreate de ferramentas do Azure existente, anexar ou redimensionar discos maiores que 1 TB.</span><span class="sxs-lookup"><span data-stu-id="76c9a-243">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="76c9a-244">tooupload seu VHD arquivo local diretamente tooAzure como um blob de página ou disco não gerenciado, é necessário conjuntos de ferramentas toouse hello mais recentes:</span><span class="sxs-lookup"><span data-stu-id="76c9a-244">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="76c9a-245">Ferramentas do Azure</span><span class="sxs-lookup"><span data-stu-id="76c9a-245">Azure tools</span></span>      | <span data-ttu-id="76c9a-246">Versões com suporte</span><span class="sxs-lookup"><span data-stu-id="76c9a-246">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="76c9a-247">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="76c9a-247">Azure PowerShell</span></span> | <span data-ttu-id="76c9a-248">Número de versão 4.1.0: versão de junho de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="76c9a-248">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="76c9a-249">CLI do Azure v1</span><span class="sxs-lookup"><span data-stu-id="76c9a-249">Azure CLI v1</span></span>     | <span data-ttu-id="76c9a-250">Número de versão 0.10.13: versão de maio de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="76c9a-250">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="76c9a-251">AzCopy</span><span class="sxs-lookup"><span data-stu-id="76c9a-251">AzCopy</span></span>           | <span data-ttu-id="76c9a-252">Número de versão 6.1.0: versão de junho de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="76c9a-252">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="76c9a-253">suporte a saudação v2 CLI do Azure e o Azure Storage Explorer estará disponível em breve.</span><span class="sxs-lookup"><span data-stu-id="76c9a-253">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="76c9a-254">**Os tamanhos de disco P4 e P6 têm suporte para discos não gerenciados ou blobs de página?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-254">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="76c9a-255">Não.</span><span class="sxs-lookup"><span data-stu-id="76c9a-255">No.</span></span> <span data-ttu-id="76c9a-256">Os tamanhos de disco P4 (32 GB) e P6 (64 GB) têm suporte somente para discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="76c9a-256">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="76c9a-257">O suporte a discos não gerenciados e blobs de página será lançado em breve.</span><span class="sxs-lookup"><span data-stu-id="76c9a-257">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="76c9a-258">**Se o meu premium existente gerenciado disco menor do que 64 GB foi criado antes da habilitação do disco pequeno hello (em torno de 15 de junho de 2017), como ele é cobrado?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-258">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="76c9a-259">Discos premium pequeno existentes com menos de 64 GB continuar preço de acordo toohello P10 toobe cobrado.</span><span class="sxs-lookup"><span data-stu-id="76c9a-259">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="76c9a-260">**Como alternar da camada de disco Olá de discos premium pequeno menor do que 64 GB de tooP4 P10 ou P6?**</span><span class="sxs-lookup"><span data-stu-id="76c9a-260">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="76c9a-261">Você pode tirar um instantâneo dos discos pequenos e, em seguida, crie uma saudação de comutador do disco tooautomatically tooP4 da camada de preços ou P6 com base no tamanho de saudação provisionado.</span><span class="sxs-lookup"><span data-stu-id="76c9a-261">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="76c9a-262">E se dúvida não foi respondida aqui?</span><span class="sxs-lookup"><span data-stu-id="76c9a-262">What if my question isn't answered here?</span></span>

<span data-ttu-id="76c9a-263">Se sua pergunta não estiver listada aqui, fale conosco e nós ajudaremos a encontrar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="76c9a-263">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="76c9a-264">Você pode postar uma pergunta no final deste artigo Olá nos comentários de saudação.</span><span class="sxs-lookup"><span data-stu-id="76c9a-264">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="76c9a-265">tooengage com a equipe de armazenamento do Azure hello e outros membros da comunidade sobre neste artigo, use Olá MSDN [Fórum de armazenamento do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="76c9a-265">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="76c9a-266">recursos toorequest, enviar sua solicitações e ideias toohello [Fórum de comentários do armazenamento do Azure](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="76c9a-266">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
