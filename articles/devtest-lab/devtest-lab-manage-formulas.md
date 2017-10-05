---
title: "Gerenciar fórmulas no Azure DevTest Labs para criar VMs | Microsoft Docs"
description: "Saiba como atualizar e remover fórmulas do Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfdab5def50158f9b764bbb1e50c2624cc6d5fb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="c0f46-103">Gerenciar fórmulas do Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="c0f46-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="c0f46-104">Este artigo ilustra como criar uma fórmula de uma base (imagem personalizada, imagem do Marketplace ou outra fórmula) ou de uma máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="c0f46-104">This article illustrates how to create a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="c0f46-105">Este artigo também orienta você por meio do gerenciamento de fórmulas existentes.</span><span class="sxs-lookup"><span data-stu-id="c0f46-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="c0f46-106">Criar uma fórmula</span><span class="sxs-lookup"><span data-stu-id="c0f46-106">Create a formula</span></span>
<span data-ttu-id="c0f46-107">Qualquer pessoa com permissões de *Usuários* no DevTest Labs pode criar VMs usando uma fórmula como base.</span><span class="sxs-lookup"><span data-stu-id="c0f46-107">Anyone with DevTest Labs *Users* permissions is able to create VMs using a formula as a base.</span></span> <span data-ttu-id="c0f46-108">Existem duas maneiras de criar fórmulas:</span><span class="sxs-lookup"><span data-stu-id="c0f46-108">There are two ways to create formulas:</span></span> 

* <span data-ttu-id="c0f46-109">De uma base – use quando quiser definir todas as características da fórmula.</span><span class="sxs-lookup"><span data-stu-id="c0f46-109">From a base - Use when you want to define all the characteristics of the formula.</span></span>
* <span data-ttu-id="c0f46-110">Com base em uma VM de laboratório existente: use quando desejar criar uma fórmula com base nas configurações de uma VM existente.</span><span class="sxs-lookup"><span data-stu-id="c0f46-110">From an existing lab VM - Use when you want to create a formula based on the settings of an existing VM.</span></span>

<span data-ttu-id="c0f46-111">Para saber mais sobre como adicionar usuários e permissões, consulte [Adicionar proprietários e usuários no Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="c0f46-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="c0f46-112">Criar uma fórmula de uma base</span><span class="sxs-lookup"><span data-stu-id="c0f46-112">Create a formula from a base</span></span>
<span data-ttu-id="c0f46-113">As etapas a seguir o orientarão no processo de criação de uma fórmula usando uma imagem personalizada, uma imagem do Marketplace ou outra fórmula.</span><span class="sxs-lookup"><span data-stu-id="c0f46-113">The following steps guide you through the process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="c0f46-114">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c0f46-114">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="c0f46-115">Selecione **Mais Serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="c0f46-115">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>

3. <span data-ttu-id="c0f46-116">Na lista de laboratórios, selecione o laboratório desejado.</span><span class="sxs-lookup"><span data-stu-id="c0f46-116">From the list of labs, select the desired lab.</span></span>  

4. <span data-ttu-id="c0f46-117">Na folha do laboratório, selecione **Fórmulas (bases reutilizáveis)**.</span><span class="sxs-lookup"><span data-stu-id="c0f46-117">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu Fórmula](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="c0f46-119">Na folha **Fórmulas**, selecione **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c0f46-119">On the **Formulas** blade, select **+ Add**.</span></span>
   
    ![Adicionar uma fórmula](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="c0f46-121">Na folha **Escolher uma base** , selecione a base (imagem personalizada, imagem do Marketplace ou fórmula) por meio da qual você deseja criar a fórmula.</span><span class="sxs-lookup"><span data-stu-id="c0f46-121">On the **Choose a base** blade, select the base (custom image, Marketplace image, or formula) from which you want to create the formula.</span></span>
   
    ![Lista de base](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="c0f46-123">Na folha **Criar fórmula** , especifique os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="c0f46-123">On the **Create formula** blade, specify the following values:</span></span>
   
    * <span data-ttu-id="c0f46-124">**Nome da fórmula** – digite um nome para a fórmula.</span><span class="sxs-lookup"><span data-stu-id="c0f46-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="c0f46-125">Esse valor será exibido na lista de imagens de base quando você criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c0f46-125">This value is displayed in the list of base images when you create a VM.</span></span> <span data-ttu-id="c0f46-126">O nome é validado durante a digitação e, se não servir, uma mensagem indicará os requisitos para um nome válido.</span><span class="sxs-lookup"><span data-stu-id="c0f46-126">The name is validated as you type it, and if not valid, a message indicates the requirements for a valid name.</span></span>
    * <span data-ttu-id="c0f46-127">**Descrição** – digite uma descrição relevante para a fórmula.</span><span class="sxs-lookup"><span data-stu-id="c0f46-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="c0f46-128">Esse valor está disponível no menu de contexto da fórmula quando você cria uma VM.</span><span class="sxs-lookup"><span data-stu-id="c0f46-128">This value is available from the formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="c0f46-129">**Nome de usuário** – insira um nome de usuário para receber privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="c0f46-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="c0f46-130">**Senha** – digite – ou selecione na lista suspensa – um valor associado ao segredo (senha) que você deseja usar para o usuário especificado.</span><span class="sxs-lookup"><span data-stu-id="c0f46-130">**Password** - Enter - or select from the dropdown - a value that is associated with the secret (password) that you want to use for the specified user.</span></span> <span data-ttu-id="c0f46-131">Para saber mais sobre os segredos, consulte [Azure DevTest Labs: repositório secreto pessoal](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span><span class="sxs-lookup"><span data-stu-id="c0f46-131">For more information about the secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="c0f46-132">**Tipo de disco de máquina virtual** - especifique HDD (unidade de disco rígido) ou SSD (unidade de estado sólido) para indicar qual tipo de disco de armazenamento é permitido para as máquinas virtuais provisionadas usando essa imagem base.</span><span class="sxs-lookup"><span data-stu-id="c0f46-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) to indicate which storage disk type is allowed for the virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="c0f46-133">** Tamanho da máquina virtual** – Selecione um dos itens predefinidos que especificam os núcleos de processador, o tamanho da RAM e o tamanho do disco rígido da VM a ser criada.</span><span class="sxs-lookup"><span data-stu-id="c0f46-133">** Virtual machine size** - Select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span> 
    * <span data-ttu-id="c0f46-134">**Artefatos** – selecione para abrir a folha **Adicionar artefatos**, na qual você escolhe e configura os artefatos que você deseja adicionar à imagem base.</span><span class="sxs-lookup"><span data-stu-id="c0f46-134">**Artifacts** - Select to open the **Add artifacts** blade, in which you select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="c0f46-135">Para saber mais sobre artefatos, consulte [Gerenciar artefatos de VM no Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="c0f46-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="c0f46-136">**Configurações avançadas** - selecione para abrir a folha **Avançado** na qual é possível definir as configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="c0f46-136">**Advanced settings** - Select to open the **Advanced** blade where you configure the following settings:</span></span>
        * <span data-ttu-id="c0f46-137">**Rede virtual** – especifique a rede virtual desejada.</span><span class="sxs-lookup"><span data-stu-id="c0f46-137">**Virtual network** - Specify the desired virtual network.</span></span>
        * <span data-ttu-id="c0f46-138">**Sub-rede** – especifique a sub-rede desejada.</span><span class="sxs-lookup"><span data-stu-id="c0f46-138">**Subnet** - Specify the desired subnet.</span></span>    
        * <span data-ttu-id="c0f46-139">**Configuração de endereço IP** -especifique se você deseja os endereços de IP compartilhados, privados ou públicos.</span><span class="sxs-lookup"><span data-stu-id="c0f46-139">**IP address configuration** - Specify if you want the Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="c0f46-140">Para obter mais informações sobre endereços IP compartilhados, consulte [Noções básicas dos endereços IP compartilhados no Azure DevTest Labs](./devtest-lab-shared-ip.md).</span><span class="sxs-lookup"><span data-stu-id="c0f46-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="c0f46-141">**Tornar essa máquina reivindicável** - tornar uma máquina "reivindicável" significa que ela não será propriedade de ninguém no momento da criação.</span><span class="sxs-lookup"><span data-stu-id="c0f46-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at the time of creation.</span></span> <span data-ttu-id="c0f46-142">Em vez disso, os usuários do laboratório poderão assumir a propriedade ("reivindicar") a máquina na folha do laboratório.</span><span class="sxs-lookup"><span data-stu-id="c0f46-142">Instead lab users will be able to take ownership ("claim") the machine in the lab's blade.</span></span>     
    * <span data-ttu-id="c0f46-143">**Imagem** – este campo exibe o nome da imagem de base que você selecionou na folha anterior.</span><span class="sxs-lookup"><span data-stu-id="c0f46-143">**Image** - This field displays name of the base image you selected on the previous blade.</span></span> 
     
       ![Criar fórmula](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="c0f46-145">Selecione **Criar** para criar a fórmula.</span><span class="sxs-lookup"><span data-stu-id="c0f46-145">Select **Create** to create the formula.</span></span>

9. <span data-ttu-id="c0f46-146">Após a criação da fórmula, ela exibirá na lista na folha **Fórmulas**.</span><span class="sxs-lookup"><span data-stu-id="c0f46-146">When the formula has been created, it displays in the list on the **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="c0f46-147">Criar uma fórmula de uma VM</span><span class="sxs-lookup"><span data-stu-id="c0f46-147">Create a formula from a VM</span></span>
<span data-ttu-id="c0f46-148">As etapas a seguir o orientarão durante o processo de criação de uma fórmula com base em uma VM existente.</span><span class="sxs-lookup"><span data-stu-id="c0f46-148">The following steps guide you through the process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="c0f46-149">Para criar uma fórmula de uma VM, a VM deve ter sido criada após 30 de março de 2016.</span><span class="sxs-lookup"><span data-stu-id="c0f46-149">To create a formula from a VM, the VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="c0f46-150">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c0f46-150">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="c0f46-151">Selecione **Mais Serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="c0f46-151">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="c0f46-152">Na lista de laboratórios, selecione o laboratório desejado.</span><span class="sxs-lookup"><span data-stu-id="c0f46-152">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="c0f46-153">Na folha **Visão geral** do laboratório, selecione a VM com base na qual você deseja criar a fórmula.</span><span class="sxs-lookup"><span data-stu-id="c0f46-153">On the lab's **Overview** blade, select the VM from which you wish to create the formula.</span></span>
   
    ![VMs do Labs](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="c0f46-155">Na folha da VM, selecione **Criar fórmula (base reutilizável)**.</span><span class="sxs-lookup"><span data-stu-id="c0f46-155">On the VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Criar fórmula](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="c0f46-157">Na folha **Criar fórmula**, digite um **Nome** e uma **Descrição** para sua nova fórmula.</span><span class="sxs-lookup"><span data-stu-id="c0f46-157">On the **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Folha Criar fórmula](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="c0f46-159">Selecione **OK** para criar a fórmula.</span><span class="sxs-lookup"><span data-stu-id="c0f46-159">Select **OK** to create the formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="c0f46-160">Modificar uma Fórmula</span><span class="sxs-lookup"><span data-stu-id="c0f46-160">Modify a formula</span></span>
<span data-ttu-id="c0f46-161">Para modificar uma fórmula, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="c0f46-161">To modify a formula, follow these steps:</span></span>

1. <span data-ttu-id="c0f46-162">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c0f46-162">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="c0f46-163">Selecione **Mais Serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="c0f46-163">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="c0f46-164">Na lista de laboratórios, selecione o laboratório desejado.</span><span class="sxs-lookup"><span data-stu-id="c0f46-164">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="c0f46-165">Na folha do laboratório, selecione **Fórmulas (bases reutilizáveis)**.</span><span class="sxs-lookup"><span data-stu-id="c0f46-165">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu Fórmula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="c0f46-167">Na folha **Fórmulas do laboratório** , selecione a fórmula que você deseja modificar.</span><span class="sxs-lookup"><span data-stu-id="c0f46-167">On the **Lab formulas** blade, select the formula you wish to modify.</span></span>
6. <span data-ttu-id="c0f46-168">Na folha **Atualizar fórmula**, faça as edições desejadas e selecione **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="c0f46-168">On the **Update formula** blade, make the desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="c0f46-169">Excluir uma fórmula</span><span class="sxs-lookup"><span data-stu-id="c0f46-169">Delete a formula</span></span>
<span data-ttu-id="c0f46-170">Para excluir uma fórmula, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="c0f46-170">To delete a formula, follow these steps:</span></span>

1. <span data-ttu-id="c0f46-171">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c0f46-171">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="c0f46-172">Selecione **Mais Serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="c0f46-172">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="c0f46-173">Na lista de laboratórios, selecione o laboratório desejado.</span><span class="sxs-lookup"><span data-stu-id="c0f46-173">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="c0f46-174">Na folha **Configurações**, selecione **Fórmulas**.</span><span class="sxs-lookup"><span data-stu-id="c0f46-174">On the lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Menu Fórmula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="c0f46-176">Na folha **Fórmulas do laboratório** , clique nas reticências à direita da fórmula que você deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="c0f46-176">On the **Lab formulas** blade, select the ellipsis to the right of the formula you wish to delete.</span></span>
   
    ![Menu Fórmula](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="c0f46-178">No menu de contexto da fórmula, selecione **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="c0f46-178">On the formula's context menu, select **Delete**.</span></span>
   
    ![Menu de contexto da Fórmula](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="c0f46-180">Selecione **Sim** na caixa de diálogo de confirmação de exclusão.</span><span class="sxs-lookup"><span data-stu-id="c0f46-180">Select **Yes** to the deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="c0f46-181">Postagens de blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="c0f46-181">Related blog posts</span></span>
* [<span data-ttu-id="c0f46-182">Imagens personalizadas ou fórmulas?</span><span class="sxs-lookup"><span data-stu-id="c0f46-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="c0f46-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c0f46-183">Next steps</span></span>
<span data-ttu-id="c0f46-184">Depois de criar uma fórmula para uso durante a criação de uma VM, a próxima etapa será [adicionar uma VM ao seu laboratório](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="c0f46-184">Once you have created a formula for use when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

