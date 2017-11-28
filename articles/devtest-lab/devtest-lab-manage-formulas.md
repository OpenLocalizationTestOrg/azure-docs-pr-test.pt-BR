---
title: "fórmulas de aaaManage no Azure DevTest Labs toocreate VMs | Microsoft Docs"
description: "Saiba como tooupdate e remova fórmulas do Azure DevTest Labs"
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
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="02619-103">Gerenciar fórmulas do Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="02619-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="02619-104">Este artigo ilustra como toocreate uma fórmula de uma base (imagem personalizada, imagem do Marketplace ou outra fórmula) ou em uma VM existente.</span><span class="sxs-lookup"><span data-stu-id="02619-104">This article illustrates how toocreate a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="02619-105">Este artigo também orienta você por meio do gerenciamento de fórmulas existentes.</span><span class="sxs-lookup"><span data-stu-id="02619-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="02619-106">Criar uma fórmula</span><span class="sxs-lookup"><span data-stu-id="02619-106">Create a formula</span></span>
<span data-ttu-id="02619-107">Qualquer pessoa com DevTest Labs *usuários* permissões é capaz de toocreate VMs usando uma fórmula como base.</span><span class="sxs-lookup"><span data-stu-id="02619-107">Anyone with DevTest Labs *Users* permissions is able toocreate VMs using a formula as a base.</span></span> <span data-ttu-id="02619-108">Há duas maneiras de toocreate fórmulas:</span><span class="sxs-lookup"><span data-stu-id="02619-108">There are two ways toocreate formulas:</span></span> 

* <span data-ttu-id="02619-109">De uma base - Use quando desejar toodefine todas as características de saudação da fórmula hello.</span><span class="sxs-lookup"><span data-stu-id="02619-109">From a base - Use when you want toodefine all hello characteristics of hello formula.</span></span>
* <span data-ttu-id="02619-110">De um laboratório existente VM - Use quando desejar toocreate uma fórmula com base nas configurações de saudação de uma VM existente.</span><span class="sxs-lookup"><span data-stu-id="02619-110">From an existing lab VM - Use when you want toocreate a formula based on hello settings of an existing VM.</span></span>

<span data-ttu-id="02619-111">Para saber mais sobre como adicionar usuários e permissões, consulte [Adicionar proprietários e usuários no Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="02619-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="02619-112">Criar uma fórmula de uma base</span><span class="sxs-lookup"><span data-stu-id="02619-112">Create a formula from a base</span></span>
<span data-ttu-id="02619-113">Olá etapas a seguir o guiará Olá o processo de criação de uma fórmula de uma imagem personalizada, imagem do Marketplace ou outra fórmula.</span><span class="sxs-lookup"><span data-stu-id="02619-113">hello following steps guide you through hello process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="02619-114">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="02619-114">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="02619-115">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="02619-115">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>

3. <span data-ttu-id="02619-116">Saudação de laboratórios, selecione lista laboratório desejado hello.</span><span class="sxs-lookup"><span data-stu-id="02619-116">From hello list of labs, select hello desired lab.</span></span>  

4. <span data-ttu-id="02619-117">Na folha do laboratório hello, selecione **fórmulas (bases reutilizáveis)**.</span><span class="sxs-lookup"><span data-stu-id="02619-117">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu Fórmula](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="02619-119">Em Olá **fórmulas** folha, selecione **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="02619-119">On hello **Formulas** blade, select **+ Add**.</span></span>
   
    ![Adicionar uma fórmula](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="02619-121">Em Olá **escolher uma base** folha, base select hello (imagem personalizada, imagem do Marketplace ou fórmula) do qual você deseja a fórmula de saudação toocreate.</span><span class="sxs-lookup"><span data-stu-id="02619-121">On hello **Choose a base** blade, select hello base (custom image, Marketplace image, or formula) from which you want toocreate hello formula.</span></span>
   
    ![Lista de base](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="02619-123">Em Olá **criar fórmula** folha, especifique Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="02619-123">On hello **Create formula** blade, specify hello following values:</span></span>
   
    * <span data-ttu-id="02619-124">**Nome da fórmula** – digite um nome para a fórmula.</span><span class="sxs-lookup"><span data-stu-id="02619-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="02619-125">Esse valor é exibido na lista de saudação de base imagens quando você cria uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="02619-125">This value is displayed in hello list of base images when you create a VM.</span></span> <span data-ttu-id="02619-126">nome da saudação é validado como digitá-lo e se não é válido, uma mensagem indica que os requisitos de saudação para um nome válido.</span><span class="sxs-lookup"><span data-stu-id="02619-126">hello name is validated as you type it, and if not valid, a message indicates hello requirements for a valid name.</span></span>
    * <span data-ttu-id="02619-127">**Descrição** – digite uma descrição relevante para a fórmula.</span><span class="sxs-lookup"><span data-stu-id="02619-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="02619-128">Esse valor está disponível no menu de contexto da fórmula hello quando você cria uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="02619-128">This value is available from hello formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="02619-129">**Nome de usuário** – insira um nome de usuário para receber privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="02619-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="02619-130">**Senha** - Insira - ou selecione na lista suspensa de saudação - um valor que está associado ao segredo hello (senha) que você deseja toouse para usuário especificado hello.</span><span class="sxs-lookup"><span data-stu-id="02619-130">**Password** - Enter - or select from hello dropdown - a value that is associated with hello secret (password) that you want toouse for hello specified user.</span></span> <span data-ttu-id="02619-131">Para obter mais informações sobre segredos hello, consulte [Azure DevTest Labs: repositório pessoal do segredo](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span><span class="sxs-lookup"><span data-stu-id="02619-131">For more information about hello secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="02619-132">**Tipo de disco de máquina virtual** – Especifique ou (unidade de disco rígido) de HDD ou SSD (unidade de estado sólido) tooindicate qual armazenamento em disco tipo é permitida para máquinas virtuais de saudação provisionadas usando essa imagem base.</span><span class="sxs-lookup"><span data-stu-id="02619-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) tooindicate which storage disk type is allowed for hello virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="02619-133">* * VM tamanho * * - selecione um dos itens de saudação predefinido que especificam os núcleos de processador hello, tamanho da RAM e tamanho de disco rígido de saudação do hello VM toocreate.</span><span class="sxs-lookup"><span data-stu-id="02619-133">** Virtual machine size** - Select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span> 
    * <span data-ttu-id="02619-134">**Artefatos** -Olá selecione tooopen **adicionar artefatos** folha, em que você selecionar e configurar artefatos Olá que deseja que a imagem base do tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="02619-134">**Artifacts** - Select tooopen hello **Add artifacts** blade, in which you select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="02619-135">Para saber mais sobre artefatos, consulte [Gerenciar artefatos de VM no Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="02619-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="02619-136">**Configurações avançadas** -Olá selecione tooopen **avançado** folha de onde você configura Olá configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="02619-136">**Advanced settings** - Select tooopen hello **Advanced** blade where you configure hello following settings:</span></span>
        * <span data-ttu-id="02619-137">**Rede virtual** -especificar Olá desejado de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="02619-137">**Virtual network** - Specify hello desired virtual network.</span></span>
        * <span data-ttu-id="02619-138">**Subrede** -especifique a sub-rede de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="02619-138">**Subnet** - Specify hello desired subnet.</span></span>    
        * <span data-ttu-id="02619-139">**Configuração do endereço IP** -Especifique se deseja Olá público, privado ou compartilhado endereços IP.</span><span class="sxs-lookup"><span data-stu-id="02619-139">**IP address configuration** - Specify if you want hello Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="02619-140">Para obter mais informações sobre endereços IP compartilhados, consulte [Noções básicas dos endereços IP compartilhados no Azure DevTest Labs](./devtest-lab-shared-ip.md).</span><span class="sxs-lookup"><span data-stu-id="02619-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="02619-141">**Tornar essa máquina claimable** -fazer uma máquina "claimable" significa que ele não será atribuído propriedade em tempo de saudação da criação.</span><span class="sxs-lookup"><span data-stu-id="02619-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at hello time of creation.</span></span> <span data-ttu-id="02619-142">Em vez disso, os usuários do laboratório será máquina de saudação tootake capaz de propriedade ("declaração") na folha do laboratório hello.</span><span class="sxs-lookup"><span data-stu-id="02619-142">Instead lab users will be able tootake ownership ("claim") hello machine in hello lab's blade.</span></span>     
    * <span data-ttu-id="02619-143">**Imagem** -este campo exibe o nome da imagem base do hello selecionada na folha de saudação anterior.</span><span class="sxs-lookup"><span data-stu-id="02619-143">**Image** - This field displays name of hello base image you selected on hello previous blade.</span></span> 
     
       ![Criar fórmula](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="02619-145">Selecione **criar** toocreate fórmula de saudação.</span><span class="sxs-lookup"><span data-stu-id="02619-145">Select **Create** toocreate hello formula.</span></span>

9. <span data-ttu-id="02619-146">Quando a fórmula Olá tiver sido criada, ele exibe na lista Olá Olá **fórmulas** folha.</span><span class="sxs-lookup"><span data-stu-id="02619-146">When hello formula has been created, it displays in hello list on hello **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="02619-147">Criar uma fórmula de uma VM</span><span class="sxs-lookup"><span data-stu-id="02619-147">Create a formula from a VM</span></span>
<span data-ttu-id="02619-148">Olá etapas a seguir orientará você durante saudação processo de criação de uma fórmula com base em uma VM existente.</span><span class="sxs-lookup"><span data-stu-id="02619-148">hello following steps guide you through hello process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="02619-149">toocreate uma fórmula de uma VM, Olá VM deve ter sido criado após 30 de março de 2016.</span><span class="sxs-lookup"><span data-stu-id="02619-149">toocreate a formula from a VM, hello VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="02619-150">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="02619-150">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="02619-151">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="02619-151">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="02619-152">Saudação de laboratórios, selecione lista laboratório desejado hello.</span><span class="sxs-lookup"><span data-stu-id="02619-152">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="02619-153">No laboratório de saudação **visão geral** folha, selecione Olá VM da qual você deseja toocreate fórmula de saudação.</span><span class="sxs-lookup"><span data-stu-id="02619-153">On hello lab's **Overview** blade, select hello VM from which you wish toocreate hello formula.</span></span>
   
    ![VMs do Labs](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="02619-155">Na folha de saudação da VM, selecione **criar fórmula (base reutilizável)**.</span><span class="sxs-lookup"><span data-stu-id="02619-155">On hello VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Criar fórmula](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="02619-157">Em Olá **criar fórmula** folha, insira um **nome** e **descrição** para sua nova fórmula.</span><span class="sxs-lookup"><span data-stu-id="02619-157">On hello **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Folha Criar fórmula](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="02619-159">Selecione **Okey** toocreate fórmula de saudação.</span><span class="sxs-lookup"><span data-stu-id="02619-159">Select **OK** toocreate hello formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="02619-160">Modificar uma Fórmula</span><span class="sxs-lookup"><span data-stu-id="02619-160">Modify a formula</span></span>
<span data-ttu-id="02619-161">toomodify uma fórmula, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="02619-161">toomodify a formula, follow these steps:</span></span>

1. <span data-ttu-id="02619-162">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="02619-162">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="02619-163">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="02619-163">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="02619-164">Saudação de laboratórios, selecione lista laboratório desejado hello.</span><span class="sxs-lookup"><span data-stu-id="02619-164">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="02619-165">Na folha do laboratório hello, selecione **fórmulas (bases reutilizáveis)**.</span><span class="sxs-lookup"><span data-stu-id="02619-165">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu Fórmula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="02619-167">Em Olá **fórmulas de laboratório** folha, a fórmula Olá selecione desejar toomodify.</span><span class="sxs-lookup"><span data-stu-id="02619-167">On hello **Lab formulas** blade, select hello formula you wish toomodify.</span></span>
6. <span data-ttu-id="02619-168">Em Olá **atualizar fórmula** folha, faça edições de saudação desejada e selecione **atualização**.</span><span class="sxs-lookup"><span data-stu-id="02619-168">On hello **Update formula** blade, make hello desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="02619-169">Excluir uma fórmula</span><span class="sxs-lookup"><span data-stu-id="02619-169">Delete a formula</span></span>
<span data-ttu-id="02619-170">toodelete uma fórmula, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="02619-170">toodelete a formula, follow these steps:</span></span>

1. <span data-ttu-id="02619-171">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="02619-171">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="02619-172">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="02619-172">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="02619-173">Saudação de laboratórios, selecione lista laboratório desejado hello.</span><span class="sxs-lookup"><span data-stu-id="02619-173">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="02619-174">Laboratório Olá **configurações** folha, selecione **fórmulas**.</span><span class="sxs-lookup"><span data-stu-id="02619-174">On hello lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Menu Fórmula](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="02619-176">Em Olá **fórmulas de laboratório** folha, selecione Olá toohello de reticências à direita da fórmula Olá desejar toodelete.</span><span class="sxs-lookup"><span data-stu-id="02619-176">On hello **Lab formulas** blade, select hello ellipsis toohello right of hello formula you wish toodelete.</span></span>
   
    ![Menu Fórmula](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="02619-178">No menu de contexto da fórmula hello, selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="02619-178">On hello formula's context menu, select **Delete**.</span></span>
   
    ![Menu de contexto da Fórmula](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="02619-180">Selecione **Sim** toohello caixa de diálogo de confirmação de exclusão.</span><span class="sxs-lookup"><span data-stu-id="02619-180">Select **Yes** toohello deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="02619-181">Postagens de blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="02619-181">Related blog posts</span></span>
* [<span data-ttu-id="02619-182">Imagens personalizadas ou fórmulas?</span><span class="sxs-lookup"><span data-stu-id="02619-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="02619-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="02619-183">Next steps</span></span>
<span data-ttu-id="02619-184">Depois de criar uma fórmula para uso durante a criação de uma máquina virtual, a próxima etapa de saudação é muito[adicionar um laboratório de tooyour VM](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="02619-184">Once you have created a formula for use when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

