---
title: "máquinas virtuais de aaaManage usando hello Azure Explorer para IntelliJ | Microsoft Docs"
description: "Saiba como toomanage as máquinas virtuais do Azure usando hello Azure Explorer para IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: a73dd4f73b311dd3413f6712e3b76c36ee464de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="c009f-103">Gerenciar máquinas virtuais usando hello Azure Explorer para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c009f-103">Manage virtual machines by using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="c009f-104">Hello Azure Explorer, que faz parte do hello Azure Toolkit for IntelliJ, fornece aos desenvolvedores de Java com uma solução fácil de usar para gerenciar as máquinas virtuais em sua conta do Azure de dentro do ambiente de desenvolvimento integrado Olá IntelliJ (IDE).</span><span class="sxs-lookup"><span data-stu-id="c009f-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="c009f-105">Criar uma máquina virtual no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c009f-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c009f-106">toocreate uma máquina virtual usando hello Azure Explorer Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c009f-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span> 

1. <span data-ttu-id="c009f-107">Entrar tooyour conta do Azure usando as etapas de Olá Olá [instruções entrar para hello Azure Toolkit for IntelliJ] artigo.</span><span class="sxs-lookup"><span data-stu-id="c009f-107">Sign in tooyour Azure account by using hello steps in hello [Sign-in instructions for hello Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="c009f-108">Em hello **Azure Explorer** exibir, expanda Olá **Azure** nó, clique com botão direito **máquinas virtuais**e, em seguida, clique em **criar VM**.</span><span class="sxs-lookup"><span data-stu-id="c009f-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="c009f-109">![Olá comando Criar VM][CR01]</span><span class="sxs-lookup"><span data-stu-id="c009f-109">![hello Create VM command][CR01]</span></span>  
    <span data-ttu-id="c009f-110">Olá **criar nova máquina Virtual** assistente é aberto.</span><span class="sxs-lookup"><span data-stu-id="c009f-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="c009f-111">Em Olá **escolher uma assinatura** janela, selecione sua assinatura e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="c009f-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![Olá janela Escolha uma assinatura][CR02]

4. <span data-ttu-id="c009f-113">Em Olá **selecionar uma imagem de máquina Virtual** janela, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="c009f-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="c009f-114">**Localização**: especifica o local no qual sua máquina virtual será criada (por exemplo, *Oeste dos EUA*).</span><span class="sxs-lookup"><span data-stu-id="c009f-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="c009f-115">**Imagem recomendada**: especifica que você escolherá uma imagem de uma lista abreviada de imagens usadas com frequência.</span><span class="sxs-lookup"><span data-stu-id="c009f-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="c009f-116">**Imagem personalizada**: Especifica que você escolherá uma imagem personalizada, fornecendo Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="c009f-116">**Custom image**: Specifies that you will choose a custom image by providing hello following information:</span></span>

      * <span data-ttu-id="c009f-117">**Publicador**: Especifica o publicador de saudação que criou a imagem de saudação que você usará para sua máquina virtual (por exemplo, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="c009f-117">**Publisher**: Specifies hello publisher that created hello image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="c009f-118">**Oferecer**: Especifica a máquina virtual de saudação toouse da oferta do publicador selecionado hello (por exemplo, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="c009f-118">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="c009f-119">**SKU**: especifica Olá toouse SKU (unidade) de manutenção de estoque de oferta de saudação selecionado (por exemplo, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="c009f-119">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="c009f-120">**Versão #**: especifica qual versão de saudação selecionada toouse SKU.</span><span class="sxs-lookup"><span data-stu-id="c009f-120">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

   ![Olá selecione uma janela de imagem de máquina Virtual][CR03]

5. <span data-ttu-id="c009f-122">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c009f-122">Click **Next**.</span></span> 

6. <span data-ttu-id="c009f-123">Em Olá **configurações básicas de máquina Virtual** janela, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="c009f-123">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="c009f-124">**Nome da máquina virtual**: Especifica o nome Olá para sua nova máquina virtual, que deve começar com uma letra e conter apenas letras, números e hifens.</span><span class="sxs-lookup"><span data-stu-id="c009f-124">**Virtual machine name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="c009f-125">**Tamanho**: Especifica o número de saudação de núcleos e memória tooallocate para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c009f-125">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="c009f-126">**Nome de usuário**: especifica Olá toocreate de conta de administrador para gerenciar sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c009f-126">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="c009f-127">**Senha** e **confirmar**: Especifica a senha Olá para sua conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="c009f-127">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

   ![janela de configurações básicas de máquina Virtual Olá][CR04]

7. <span data-ttu-id="c009f-129">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c009f-129">Click **Next**.</span></span> 

8. <span data-ttu-id="c009f-130">Em Olá **recursos associados** janela, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="c009f-130">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="c009f-131">**Grupo de recursos**: Especifica o grupo de recursos de saudação para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c009f-131">**Resource group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="c009f-132">Selecione uma saudação as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="c009f-132">Select one of hello following options:</span></span>
      * <span data-ttu-id="c009f-133">**Criar um novo**: Especifica que você deseja toocreate um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c009f-133">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="c009f-134">**Usar existente**: Especifica que você deseja tooselect em uma lista de grupos de recursos que estão associados com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c009f-134">**Use existing**: Specifies that you want tooselect from a list of resource groups that are associated with your Azure account.</span></span>

       ![janela de recursos associado Olá][CR07]

   * <span data-ttu-id="c009f-136">**Conta de armazenamento**: especifica Olá toouse de conta de armazenamento para armazenar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c009f-136">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="c009f-137">Escolha uma conta de armazenamento existente ou crie uma nova.</span><span class="sxs-lookup"><span data-stu-id="c009f-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="c009f-138">Se você escolher **criar novo**, Olá caixa de diálogo a seguir será exibida:</span><span class="sxs-lookup"><span data-stu-id="c009f-138">If you choose **Create New**, hello following dialog box appears:</span></span>

      ![caixa de diálogo Criar conta de armazenamento Olá][CR05]

   * <span data-ttu-id="c009f-140">**Rede virtual** e **sub-rede**: Especifica a rede virtual hello e a sub-rede que sua máquina virtual será conectado ao.</span><span class="sxs-lookup"><span data-stu-id="c009f-140">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="c009f-141">Use uma rede e sub-rede existentes ou crie uma nova rede e sub-rede.</span><span class="sxs-lookup"><span data-stu-id="c009f-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="c009f-142">Se você selecionar **criar novo**, Olá caixa de diálogo a seguir será exibida:</span><span class="sxs-lookup"><span data-stu-id="c009f-142">If you select **Create new**, hello following dialog box appears:</span></span>

      ![caixa de diálogo Criar rede Virtual Olá][CR06]

   * <span data-ttu-id="c009f-144">**Endereço IP público**: especifica um endereço IP externo para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c009f-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="c009f-145">Você pode escolher um novo endereço IP toocreate ou, se sua máquina virtual não terá um endereço IP público, você pode selecionar **(nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="c009f-145">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="c009f-146">**Grupo de segurança de rede**: especifica um firewall de rede opcional para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c009f-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="c009f-147">Selecione um firewall existente ou, se sua máquina virtual não for usar um firewall de rede, selecione **(Nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="c009f-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="c009f-148">**Conjunto de disponibilidade**: especifica um conjunto de disponibilidade opcional ao qual sua máquina virtual pode pertencer.</span><span class="sxs-lookup"><span data-stu-id="c009f-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="c009f-149">Você pode selecionar um conjunto de disponibilidade existente, crie um novo conjunto de disponibilidade ou, se sua máquina virtual não pertencerá tooan conjunto de disponibilidade, selecione **(nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="c009f-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong tooan availability set, select **(None)**.</span></span>

9. <span data-ttu-id="c009f-150">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="c009f-150">Click **Finish**.</span></span>  
    <span data-ttu-id="c009f-151">Sua nova máquina virtual é exibida na janela de ferramenta do Gerenciador do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c009f-151">Your new virtual machine appears in hello Azure Explorer tool window.</span></span> 

   ![Nova máquina virtual no hello exibição do Explorer do Azure][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="c009f-153">Reiniciar uma máquina virtual no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c009f-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c009f-154">toorestart uma máquina virtual usando hello Azure Explorer no IntelliJ, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c009f-154">toorestart a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="c009f-155">Em Olá **Azure Explorer** exibir, Olá VM e, em seguida, selecione **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="c009f-155">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![Olá comando de reinicialização de máquina virtual][RE01]

2. <span data-ttu-id="c009f-157">Na janela de confirmação de saudação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="c009f-157">In hello confirmation window, click **Yes**.</span></span> 

   ![Olá reiniciar a janela de confirmação da máquina virtual][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="c009f-159">Desligar uma máquina virtual no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c009f-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c009f-160">tooshut para baixo de uma máquina virtual em execução usando hello Azure Explorer no IntelliJ, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c009f-160">tooshut down a running virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="c009f-161">Em Olá **Azure Explorer** exibir, Olá VM e, em seguida, selecione **desligamento**.</span><span class="sxs-lookup"><span data-stu-id="c009f-161">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![comando de desligamento de máquina virtual Olá][SH01]

2. <span data-ttu-id="c009f-163">Na janela de confirmação de saudação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="c009f-163">In hello confirmation window, click **Yes**.</span></span> 

   ![Olá desligar a janela de confirmação da máquina virtual][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="c009f-165">Excluir uma máquina virtual no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c009f-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c009f-166">toodelete uma máquina virtual usando hello Azure Explorer no IntelliJ, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c009f-166">toodelete a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="c009f-167">Em Olá **Azure Explorer** exibir, Olá VM e, em seguida, selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="c009f-167">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![Olá comando de exclusão de máquina virtual][DE01]

2. <span data-ttu-id="c009f-169">Na janela de confirmação de saudação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="c009f-169">In hello confirmation window, click **Yes**.</span></span> 

   ![Olá excluir a janela de confirmação da máquina virtual][DE02]

## <a name="next-steps"></a><span data-ttu-id="c009f-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c009f-171">Next steps</span></span>
<span data-ttu-id="c009f-172">Para obter mais informações sobre preços e tamanhos de máquina virtual do Azure, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c009f-172">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="c009f-173">Tamanhos de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="c009f-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="c009f-174">[Tamanhos das máquinas virtuais do Windows no Azure]</span><span class="sxs-lookup"><span data-stu-id="c009f-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="c009f-175">[Tamanhos das máquinas virtuais do Linux no Azure]</span><span class="sxs-lookup"><span data-stu-id="c009f-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="c009f-176">Preços de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="c009f-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="c009f-177">[Preços de máquinas virtuais do Windows]</span><span class="sxs-lookup"><span data-stu-id="c009f-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="c009f-178">[Preços de máquinas virtuais do Linux]</span><span class="sxs-lookup"><span data-stu-id="c009f-178">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="c009f-179">Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c009f-179">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="c009f-180">[Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c009f-180">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c009f-181">[O que há de novo no hello Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c009f-181">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c009f-182">[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c009f-182">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c009f-183">[Instruções de entrada para Olá Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c009f-183">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c009f-184">[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c009f-184">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="c009f-185">[Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c009f-185">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c009f-186">[O que há de novo no hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c009f-186">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c009f-187">[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c009f-187">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c009f-188">[instruções entrar para hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c009f-188">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c009f-189">[Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c009f-189">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="c009f-190">Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="c009f-190">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instruções de entrada para Olá Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[instruções entrar para hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[O que há de novo no hello Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[O que há de novo no hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/

[Tamanhos das máquinas virtuais do Windows no Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamanhos das máquinas virtuais do Linux no Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preços de máquinas virtuais do Windows]: /pricing/details/virtual-machines/windows/
[Preços de máquinas virtuais do Linux]: /pricing/details/virtual-machines/linux/


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
