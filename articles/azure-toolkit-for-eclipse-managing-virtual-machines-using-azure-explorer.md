---
title: "máquinas virtuais de aaaManage usando Olá Gerenciador do Azure para Eclipse | Microsoft Docs"
description: "Saiba como toomanage as máquinas virtuais do Azure usando Olá Explorer do Azure para Eclipse."
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
ms.openlocfilehash: aa83ec7546a0a8514842723b51ce8a5af81f98f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="60608-103">Gerenciar máquinas virtuais usando Olá pesquisador do Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="60608-103">Manage virtual machines by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="60608-104">Hello Azure Explorer, que faz parte da saudação Kit de ferramentas do Azure para Eclipse, fornece aos desenvolvedores de Java com uma solução fácil de usar para gerenciar as máquinas virtuais em sua conta do Azure de dentro do ambiente de desenvolvimento integrado (IDE) do Olá Eclipse.</span><span class="sxs-lookup"><span data-stu-id="60608-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="60608-105">Criar uma máquina virtual no Eclipse</span><span class="sxs-lookup"><span data-stu-id="60608-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="60608-106">toocreate uma máquina virtual usando hello Azure Explorer Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="60608-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="60608-107">Entrar tooyour conta do Azure usando Olá [instruções entrar para Olá Kit de ferramentas do Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="60608-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="60608-108">Em hello **Azure Explorer** exibir, expanda Olá **Azure** nó, clique com botão direito **máquinas virtuais**e, em seguida, clique em **criar VM**.</span><span class="sxs-lookup"><span data-stu-id="60608-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   <span data-ttu-id="60608-109">![Olá comando Criar VM][CR01]</span><span class="sxs-lookup"><span data-stu-id="60608-109">![hello Create VM command][CR01]</span></span>  
   <span data-ttu-id="60608-110">Olá **criar nova máquina Virtual** assistente é aberto.</span><span class="sxs-lookup"><span data-stu-id="60608-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="60608-111">Em Olá **escolher uma assinatura** janela, selecione sua assinatura e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="60608-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Olá janela Escolha uma assinatura][CR02]

4. <span data-ttu-id="60608-113">Em Olá **selecionar uma imagem de máquina Virtual** janela, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="60608-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="60608-114">**Localização**: especifica o local no qual sua máquina virtual será criada (por exemplo, *Oeste dos EUA*).</span><span class="sxs-lookup"><span data-stu-id="60608-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="60608-115">**Publicador**: Especifica o publicador de saudação que criou a imagem Olá usará toocreate sua máquina virtual (por exemplo, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="60608-115">**Publisher**: Specifies hello publisher that created hello image you'll use toocreate your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="60608-116">**Oferecer**: Especifica a máquina virtual de saudação toouse da oferta do publicador selecionado hello (por exemplo, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="60608-116">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="60608-117">**SKU**: especifica Olá toouse SKU (unidade) de manutenção de estoque de oferta de saudação selecionado (por exemplo, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="60608-117">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="60608-118">**Versão #**: especifica qual versão de saudação selecionada toouse SKU.</span><span class="sxs-lookup"><span data-stu-id="60608-118">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

    ![Olá selecione uma janela de imagem de máquina Virtual][CR03]

5. <span data-ttu-id="60608-120">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="60608-120">Click **Next**.</span></span>

6. <span data-ttu-id="60608-121">Em Olá **configurações básicas de máquina Virtual** janela, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="60608-121">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="60608-122">**Nome da máquina virtual**: Especifica o nome Olá para sua nova máquina virtual, que deve começar com uma letra e conter apenas letras, números e hifens.</span><span class="sxs-lookup"><span data-stu-id="60608-122">**Virtual Machine Name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="60608-123">**Tamanho**: Especifica o número de saudação de núcleos e memória tooallocate para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="60608-123">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="60608-124">**Nome de usuário**: especifica Olá toocreate de conta de administrador para gerenciar sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="60608-124">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="60608-125">**Senha** e **confirmar**: Especifica a senha Olá para sua conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="60608-125">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

    ![janela de configurações básicas de máquina Virtual Olá][CR04]

7. <span data-ttu-id="60608-127">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="60608-127">Click **Next**.</span></span>

8. <span data-ttu-id="60608-128">Em Olá **criar uma nova conta de armazenamento** janela, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="60608-128">In hello **Create New Storage Account** window, enter hello following information:</span></span>

   * <span data-ttu-id="60608-129">**Grupo de recursos**: Especifica o grupo de recursos de saudação para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="60608-129">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="60608-130">Selecione uma saudação as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="60608-130">Select one of hello following options:</span></span>
      * <span data-ttu-id="60608-131">**Criar um novo**: Especifica que você deseja toocreate um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="60608-131">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="60608-132">**Usar existente**: Especifica que você deseja tooselect um grupo de recursos já está associado à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="60608-132">**Use existing**: Specifies that you want tooselect a resource group that is already associated with your Azure account.</span></span>

      ![caixa de diálogo Criar nova conta de armazenamento Olá][CR05]

   * <span data-ttu-id="60608-134">**Conta de armazenamento**: especifica Olá toouse de conta de armazenamento para armazenar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="60608-134">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="60608-135">Você pode usar uma conta de armazenamento existente ou criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="60608-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="60608-136">**Rede virtual** e **sub-rede**: Especifica a rede virtual hello e a sub-rede que sua máquina virtual será conectado ao.</span><span class="sxs-lookup"><span data-stu-id="60608-136">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="60608-137">Use uma rede e sub-rede existentes ou crie uma nova rede e sub-rede.</span><span class="sxs-lookup"><span data-stu-id="60608-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="60608-138">Se você selecionar **criar novo**, Olá caixa de diálogo a seguir será exibida:</span><span class="sxs-lookup"><span data-stu-id="60608-138">If you select **Create new**, hello following dialog box is displayed:</span></span>

      ![caixa de diálogo Criar nova rede Virtual Olá][CR06]

9. <span data-ttu-id="60608-140">Em Olá **recursos associados** janela, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="60608-140">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="60608-141">**Endereço IP público**: especifica um endereço IP externo para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="60608-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="60608-142">Você pode escolher um novo endereço IP toocreate ou, se sua máquina virtual não terá um endereço IP público, você pode selecionar **(nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="60608-142">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="60608-143">**Grupo de segurança de rede**: especifica um firewall de rede opcional para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="60608-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="60608-144">Selecione um firewall existente ou, se sua máquina virtual não for usar um firewall de rede, selecione **(Nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="60608-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="60608-145">**Conjunto de disponibilidade**: especifica um conjunto de disponibilidade opcional ao qual sua máquina virtual pode pertencer.</span><span class="sxs-lookup"><span data-stu-id="60608-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="60608-146">Você pode selecionar um conjunto de disponibilidade existente ou criar um novo conjunto de disponibilidade ou, se sua máquina virtual não pertencerá tooan conjunto de disponibilidade, você pode selecionar **(nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="60608-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong tooan availability set, you can select **(None)**.</span></span>

   ![janela de recursos associado Olá][CR07]

9. <span data-ttu-id="60608-148">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="60608-148">Click **Finish**.</span></span>  
  <span data-ttu-id="60608-149">Sua nova máquina virtual é exibida na janela de ferramenta do Gerenciador do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="60608-149">Your new virtual machine is displayed in hello Azure Explorer tool window.</span></span>

   ![Nova máquina virtual][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="60608-151">Reiniciar uma máquina virtual no Eclipse</span><span class="sxs-lookup"><span data-stu-id="60608-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="60608-152">toorestart uma máquina virtual usando Olá pesquisador do Azure no Eclipse, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="60608-152">toorestart a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="60608-153">Em Olá **Azure Explorer** exibir, Olá VM e, em seguida, selecione **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="60608-153">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![Olá comando de reinicialização de máquina virtual][RE01]

2. <span data-ttu-id="60608-155">Na janela de confirmação de saudação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="60608-155">In hello confirmation window, click **Yes**.</span></span>

   ![janela de confirmação de reinicialização Olá][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="60608-157">Desligar uma máquina virtual no Eclipse</span><span class="sxs-lookup"><span data-stu-id="60608-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="60608-158">tooshut para baixo de uma máquina virtual em execução usando Olá pesquisador do Azure no Eclipse, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="60608-158">tooshut down a running virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="60608-159">Em Olá **Azure Explorer** exibir, Olá VM e, em seguida, selecione **desligamento**.</span><span class="sxs-lookup"><span data-stu-id="60608-159">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![comando de desligamento de máquina virtual Olá][SH01]

2. <span data-ttu-id="60608-161">Na janela de confirmação de saudação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="60608-161">In hello confirmation window, click **Yes**.</span></span>

   ![janela de confirmação de desligamento de máquina virtual Olá][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="60608-163">Excluir uma máquina virtual no Eclipse</span><span class="sxs-lookup"><span data-stu-id="60608-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="60608-164">toodelete uma máquina virtual usando Olá pesquisador do Azure no Eclipse, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="60608-164">toodelete a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="60608-165">Em Olá **Azure Explorer** exibir, Olá VM e, em seguida, selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="60608-165">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![Olá comando de exclusão de máquina virtual][DE01]

2. <span data-ttu-id="60608-167">Na janela de confirmação de saudação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="60608-167">In hello confirmation window, click **Yes**.</span></span>

   ![janela de confirmação de exclusão de máquina virtual Olá][DE02]

## <a name="next-steps"></a><span data-ttu-id="60608-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="60608-169">Next steps</span></span>
<span data-ttu-id="60608-170">Para obter mais informações sobre preços e tamanhos de máquina virtual do Azure, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="60608-170">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="60608-171">Tamanhos de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="60608-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="60608-172">[Tamanhos das máquinas virtuais do Windows no Azure]</span><span class="sxs-lookup"><span data-stu-id="60608-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="60608-173">[Tamanhos das máquinas virtuais do Linux no Azure]</span><span class="sxs-lookup"><span data-stu-id="60608-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="60608-174">Preços de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="60608-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="60608-175">[Preços de máquinas virtuais do Windows]</span><span class="sxs-lookup"><span data-stu-id="60608-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="60608-176">[Preços de máquinas virtuais do Linux]</span><span class="sxs-lookup"><span data-stu-id="60608-176">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="60608-177">Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="60608-177">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="60608-178">[Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="60608-178">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="60608-179">[O que há de novo no hello Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="60608-179">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="60608-180">[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="60608-180">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="60608-181">[instruções entrar para Olá Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="60608-181">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="60608-182">[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="60608-182">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="60608-183">[Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="60608-183">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="60608-184">[O que há de novo no hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="60608-184">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="60608-185">[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="60608-185">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="60608-186">[Instruções entrar para hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="60608-186">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="60608-187">[Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="60608-187">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="60608-188">Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="60608-188">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[instruções entrar para Olá Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instruções entrar para hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[O que há de novo no hello Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[O que há de novo no hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/

[Tamanhos das máquinas virtuais do Windows no Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamanhos das máquinas virtuais do Linux no Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preços de máquinas virtuais do Windows]: /pricing/details/virtual-machines/windows/
[Preços de máquinas virtuais do Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
