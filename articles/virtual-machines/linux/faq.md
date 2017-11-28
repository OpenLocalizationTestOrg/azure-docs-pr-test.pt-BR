---
title: aaaFrequently perguntado para VMs do Linux no Azure | Microsoft Docs
description: "Fornece toosome respostas das perguntas comuns sobre máquinas virtuais Linux criadas com o modelo do Gerenciador de recursos de saudação que hello."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="9ca93-103">Perguntas frequentes sobre as Máquinas Virtuais Linux</span><span class="sxs-lookup"><span data-stu-id="9ca93-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="9ca93-104">Este artigo aborda algumas perguntas comuns sobre máquinas virtuais Linux criadas no Azure usando o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ca93-104">This article addresses some common questions about Linux virtual machines created in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="9ca93-105">Para a versão do Windows hello deste tópico, consulte [perguntas frequentes sobre máquinas virtuais do Windows](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="9ca93-105">For hello Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="9ca93-106">O que eu posso executar em uma VM do Azure?</span><span class="sxs-lookup"><span data-stu-id="9ca93-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="9ca93-107">Todos os assinantes podem executar software para servidores em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca93-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="9ca93-108">Para saber mais, veja [Linux em distribuições endossadas pelo Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="9ca93-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="9ca93-109">Quanto armazenamento eu posso usar com uma máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="9ca93-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="9ca93-110">Cada disco de dados pode ser até too1 TB.</span><span class="sxs-lookup"><span data-stu-id="9ca93-110">Each data disk can be up too1 TB.</span></span> <span data-ttu-id="9ca93-111">número de saudação de discos de dados, que você pode usar depende Olá tamanho da saudação máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9ca93-111">hello number of data disks you can use depends on hello size of hello virtual machine.</span></span> <span data-ttu-id="9ca93-112">Para obter detalhes, consulte [Tamanhos das máquinas virtuais](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9ca93-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="9ca93-113">Uma conta de armazenamento do Azure fornece armazenamento para o disco do sistema operacional hello e eventuais discos de dados.</span><span class="sxs-lookup"><span data-stu-id="9ca93-113">An Azure storage account provides storage for hello operating system disk and any data disks.</span></span> <span data-ttu-id="9ca93-114">Cada disco é um arquivo .vhd armazenado como um blob de páginas.</span><span class="sxs-lookup"><span data-stu-id="9ca93-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="9ca93-115">Para obter detalhes sobre preços, veja [Detalhes de preços de armazenamento](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="9ca93-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="9ca93-116">Como posso acessar minha máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="9ca93-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="9ca93-117">Estabelece um toolog de conexão remota na máquina virtual de toohello, usando Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="9ca93-117">Establish a remote connection toolog on toohello virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="9ca93-118">Consulte as instruções de saudação em como tooconnect [do Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [do Linux e Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9ca93-118">See hello instructions on how tooconnect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9ca93-119">Por padrão, o SSH permite um máximo de 10 conexões simultâneas.</span><span class="sxs-lookup"><span data-stu-id="9ca93-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="9ca93-120">Você pode aumentar esse número editando o arquivo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ca93-120">You can increase this number by editing hello configuration file.</span></span>

<span data-ttu-id="9ca93-121">Se você estiver tendo problemas, confira [Solucionar problemas de conexões SSH (Secure Shell)](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9ca93-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a><span data-ttu-id="9ca93-122">É possível usar dados de toostore saudação em disco temporário (/dev/sdb1)?</span><span class="sxs-lookup"><span data-stu-id="9ca93-122">Can I use hello temporary disk (/dev/sdb1) toostore data?</span></span>
<span data-ttu-id="9ca93-123">Não use dados de toostore saudação em disco temporário (/dev/sdb1).</span><span class="sxs-lookup"><span data-stu-id="9ca93-123">Don't use hello temporary disk (/dev/sdb1) toostore data.</span></span> <span data-ttu-id="9ca93-124">Ele existe somente para armazenamento temporário.</span><span class="sxs-lookup"><span data-stu-id="9ca93-124">It is only there for temporary storage.</span></span> <span data-ttu-id="9ca93-125">Você corre o risco de perder dados que não podem ser recuperados.</span><span class="sxs-lookup"><span data-stu-id="9ca93-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="9ca93-126">Posso copiar ou clonar uma VM do Azure existente?</span><span class="sxs-lookup"><span data-stu-id="9ca93-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="9ca93-127">Sim.</span><span class="sxs-lookup"><span data-stu-id="9ca93-127">Yes.</span></span> <span data-ttu-id="9ca93-128">Para obter instruções, consulte [como toocreate uma cópia de uma máquina virtual do Linux no hello modelo de implantação do Gerenciador de recursos](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9ca93-128">For instructions, see [How toocreate a copy of a Linux virtual machine in hello Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="9ca93-129">Por que não vejo as regiões Central e Leste do Canadá por meio do Azure Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="9ca93-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="9ca93-130">Olá duas novas regiões da Central do Canadá e Leste do Canadá não são automaticamente registrados para a criação de máquina virtual de assinaturas do Azure existentes.</span><span class="sxs-lookup"><span data-stu-id="9ca93-130">hello two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="9ca93-131">Esse registro é feito automaticamente quando uma máquina virtual é implantada por meio de Olá tooany portal do Azure outra região usando o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca93-131">This registration is done automatically when a virtual machine is deployed through hello Azure portal tooany other region using Azure Resource Manager.</span></span> <span data-ttu-id="9ca93-132">Depois de uma máquina virtual é implantada tooany outra região do Azure, regiões novo Olá devem estar disponíveis para máquinas de virtuais subsequentes.</span><span class="sxs-lookup"><span data-stu-id="9ca93-132">After a virtual machine is deployed tooany other Azure region, hello new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a><span data-ttu-id="9ca93-133">Adicionar um toomy NIC VM depois que ela é criada?</span><span class="sxs-lookup"><span data-stu-id="9ca93-133">Can I add a NIC toomy VM after it's created?</span></span>
<span data-ttu-id="9ca93-134">Sim, agora isso é possível.</span><span class="sxs-lookup"><span data-stu-id="9ca93-134">Yes, this is now possible.</span></span> <span data-ttu-id="9ca93-135">Olá VM primeiro necessidades toobe parada desalocada.</span><span class="sxs-lookup"><span data-stu-id="9ca93-135">hello VM first needs toobe stopped deallocated.</span></span> <span data-ttu-id="9ca93-136">Em seguida, você pode adicionar ou remover uma NIC (a menos que ele seja Olá última NIC Olá VM).</span><span class="sxs-lookup"><span data-stu-id="9ca93-136">Then you can add or remove a NIC (unless it's hello last NIC on hello VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="9ca93-137">Há algum requisito de nome do computador?</span><span class="sxs-lookup"><span data-stu-id="9ca93-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="9ca93-138">Sim.</span><span class="sxs-lookup"><span data-stu-id="9ca93-138">Yes.</span></span> <span data-ttu-id="9ca93-139">nome do computador Olá pode ter no máximo 64 caracteres de comprimento.</span><span class="sxs-lookup"><span data-stu-id="9ca93-139">hello computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="9ca93-140">Confira [Regras e restrições de convenções de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações sobre como nomear recursos.</span><span class="sxs-lookup"><span data-stu-id="9ca93-140">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="9ca93-141">Há algum requisito de nome de grupo de recursos?</span><span class="sxs-lookup"><span data-stu-id="9ca93-141">Are there any resource group name requirements?</span></span>
<span data-ttu-id="9ca93-142">Sim.</span><span class="sxs-lookup"><span data-stu-id="9ca93-142">Yes.</span></span> <span data-ttu-id="9ca93-143">nome do grupo de recursos Olá pode ter no máximo 90 caracteres de comprimento.</span><span class="sxs-lookup"><span data-stu-id="9ca93-143">hello resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="9ca93-144">Confira [Regras e restrições de convenções de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações sobre grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="9ca93-144">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a><span data-ttu-id="9ca93-145">Quais são os requisitos de nome de usuário de saudação ao criar uma máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="9ca93-145">What are hello username requirements when creating a VM?</span></span>
<span data-ttu-id="9ca93-146">Os nomes de usuário devem ter de 1 a 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9ca93-146">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="9ca93-147">Olá, nomes de usuário a seguir não é permitido:</span><span class="sxs-lookup"><span data-stu-id="9ca93-147">hello following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="9ca93-148">administrator</span><span class="sxs-lookup"><span data-stu-id="9ca93-148">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-149">administrador</span><span class="sxs-lookup"><span data-stu-id="9ca93-149">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-150">usuário</span><span class="sxs-lookup"><span data-stu-id="9ca93-150">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-151">user1</span><span class="sxs-lookup"><span data-stu-id="9ca93-151">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="9ca93-152">test</span><span class="sxs-lookup"><span data-stu-id="9ca93-152">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-153">user2</span><span class="sxs-lookup"><span data-stu-id="9ca93-153">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-154">test1</span><span class="sxs-lookup"><span data-stu-id="9ca93-154">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-155">user3</span><span class="sxs-lookup"><span data-stu-id="9ca93-155">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="9ca93-156">admin1</span><span class="sxs-lookup"><span data-stu-id="9ca93-156">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-157">1</span><span class="sxs-lookup"><span data-stu-id="9ca93-157">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-158">123</span><span class="sxs-lookup"><span data-stu-id="9ca93-158">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-159">a</span><span class="sxs-lookup"><span data-stu-id="9ca93-159">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="9ca93-160">actuser</span><span class="sxs-lookup"><span data-stu-id="9ca93-160">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="9ca93-161">adm</span><span class="sxs-lookup"><span data-stu-id="9ca93-161">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-162">admin2</span><span class="sxs-lookup"><span data-stu-id="9ca93-162">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-163">aspnet</span><span class="sxs-lookup"><span data-stu-id="9ca93-163">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="9ca93-164">backup</span><span class="sxs-lookup"><span data-stu-id="9ca93-164">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-165">console</span><span class="sxs-lookup"><span data-stu-id="9ca93-165">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-166">david</span><span class="sxs-lookup"><span data-stu-id="9ca93-166">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-167">guest</span><span class="sxs-lookup"><span data-stu-id="9ca93-167">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="9ca93-168">julio</span><span class="sxs-lookup"><span data-stu-id="9ca93-168">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-169">proprietário</span><span class="sxs-lookup"><span data-stu-id="9ca93-169">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-170">root</span><span class="sxs-lookup"><span data-stu-id="9ca93-170">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-171">server</span><span class="sxs-lookup"><span data-stu-id="9ca93-171">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="9ca93-172">sql</span><span class="sxs-lookup"><span data-stu-id="9ca93-172">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-173">suporte</span><span class="sxs-lookup"><span data-stu-id="9ca93-173">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-174">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="9ca93-174">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-175">sys</span><span class="sxs-lookup"><span data-stu-id="9ca93-175">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="9ca93-176">test2</span><span class="sxs-lookup"><span data-stu-id="9ca93-176">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-177">test3</span><span class="sxs-lookup"><span data-stu-id="9ca93-177">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-178">user4</span><span class="sxs-lookup"><span data-stu-id="9ca93-178">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="9ca93-179">user5</span><span class="sxs-lookup"><span data-stu-id="9ca93-179">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a><span data-ttu-id="9ca93-180">Quais são os requisitos de senha Olá durante a criação de uma máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="9ca93-180">What are hello password requirements when creating a VM?</span></span>
<span data-ttu-id="9ca93-181">Senhas devem ter de 6 a 72 caracteres e atendem 3 fora Olá seguindo os requisitos de complexidade de 4:</span><span class="sxs-lookup"><span data-stu-id="9ca93-181">Passwords must be 6 - 72 characters in length and meet 3 out of hello following 4 complexity requirements:</span></span>

* <span data-ttu-id="9ca93-182">Ter caracteres minúsculos</span><span class="sxs-lookup"><span data-stu-id="9ca93-182">Have lower characters</span></span>
* <span data-ttu-id="9ca93-183">Tem caracteres maiúsculos</span><span class="sxs-lookup"><span data-stu-id="9ca93-183">Have upper characters</span></span>
* <span data-ttu-id="9ca93-184">Tem um dígito</span><span class="sxs-lookup"><span data-stu-id="9ca93-184">Have a digit</span></span>
* <span data-ttu-id="9ca93-185">Tem um caractere especial (Correspondência de regex [\W_])</span><span class="sxs-lookup"><span data-stu-id="9ca93-185">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="9ca93-186">Olá seguindo as senhas não é permitido:</span><span class="sxs-lookup"><span data-stu-id="9ca93-186">hello following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="9ca93-187">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="9ca93-187">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="9ca93-188">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="9ca93-188">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="9ca93-189">Password!</span><span class="sxs-lookup"><span data-stu-id="9ca93-189">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="9ca93-190">Password1</span><span class="sxs-lookup"><span data-stu-id="9ca93-190">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="9ca93-191">Password22</span><span class="sxs-lookup"><span data-stu-id="9ca93-191">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="9ca93-192">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="9ca93-192">iloveyou!</span></span></td>
    </tr>
</table>
